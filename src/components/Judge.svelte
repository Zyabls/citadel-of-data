<script>
  let teams = [];
  let roundCount = 3;
  let additionalRoundCount = 2;
  let teamCount = 2;

  function initializeTeams() {
    teams = Array(teamCount).fill().map((_, i) => ({
      name: `Команда ${i + 1}`,
      rounds: Array(roundCount).fill(0),
      additionalRounds: Array(additionalRoundCount).fill(0),
      additionalPoints: 0,
      reputation: 0,
      total: 0
    }));
  }

  function addTeam() {
    teams = [...teams, {
      name: `Команда ${teams.length + 1}`,
      rounds: Array(roundCount).fill(0),
      additionalRounds: Array(additionalRoundCount).fill(0),
      additionalPoints: 0,
      reputation: 0,
      total: 0
    }];
  }

  function addRound() {
    roundCount++;
    teams = teams.map(team => ({
      ...team,
      rounds: [...team.rounds, 0]
    }));
  }

  function addAdditionalRound() {
    additionalRoundCount++;
    teams = teams.map(team => ({
      ...team,
      additionalRounds: [...team.additionalRounds, 0]
    }));
  }

  function calculateTotal(team) {
    const roundsSum = team.rounds.reduce((sum, score) => sum + Number(score || 0), 0);
    const additionalRoundsSum = team.additionalRounds.reduce((sum, score) => sum + Number(score || 0), 0);
    const additionalPoints = Number(team.additionalPoints || 0);
    const reputation = Number(team.reputation || 0);
    return roundsSum + additionalRoundsSum + additionalPoints + reputation;
  }

  function updateScore(teamIndex, field, value, subIndex = null) {
    if (subIndex !== null) {
      teams[teamIndex][field][subIndex] = Math.min(
        field === 'rounds' ? 15 : field === 'additionalRounds' ? 3 : 4,
        Math.max(0, Number(value) || 0)
      );
    } else {
      teams[teamIndex][field] = Math.min(
        field === 'additionalPoints' ? 4 : Infinity,
        Math.max(0, Number(value) || 0)
      );
    }
    teams[teamIndex].total = calculateTotal(teams[teamIndex]);
    teams = [...teams];
  }
</script>

<div class="judge-page">
  <div class="page-header">
    <h2>Страница судьи</h2>
  </div>

  {#if teams.length === 0}
    <section class="setup-section">
      <h3>Настройка игры</h3>
      <div class="setup-form">
        <div class="form-group">
          <label for="teamCount">Количество команд:</label>
          <input 
            type="number" 
            id="teamCount" 
            bind:value={teamCount} 
            min="2"
          >
        </div>
        <div class="form-group">
          <label for="roundCount">Количество раундов:</label>
          <input 
            type="number" 
            id="roundCount" 
            bind:value={roundCount} 
            min="1"
          >
        </div>
        <div class="form-group">
          <label for="additionalRoundCount">Количество доп. раундов:</label>
          <input 
            type="number" 
            id="additionalRoundCount" 
            bind:value={additionalRoundCount} 
            min="0"
          >
        </div>
        <button class="start-button" on:click={initializeTeams}>Начать игру</button>
      </div>
    </section>
  {:else}
    <section class="score-table">
      <div class="controls">
        <button on:click={addTeam}>Добавить команду</button>
        <button on:click={addRound}>Добавить раунд</button>
        <button on:click={addAdditionalRound}>Добавить доп. раунд</button>
      </div>
      <div class="table-container">
        <table>
          <thead>
            <tr>
              <th></th>
              {#each teams as team}
                <th>{team.name}</th>
              {/each}
            </tr>
          </thead>
          <tbody>
            {#each Array(roundCount) as _, roundIndex}
              <tr>
                <td>Раунд {roundIndex + 1} (0-15)</td>
                {#each teams as team, teamIndex}
                  <td>
                    <input
                      type="number"
                      min="0"
                      max="15"
                      value={team.rounds[roundIndex]}
                      on:input={(e) => updateScore(teamIndex, 'rounds', e.currentTarget.value, roundIndex)}
                    >
                  </td>
                {/each}
              </tr>
            {/each}
            
            {#each Array(additionalRoundCount) as _, roundIndex}
              <tr>
                <td>Доп. раунд {roundIndex + 1} (1-3)</td>
                {#each teams as team, teamIndex}
                  <td>
                    <input
                      type="number"
                      min="0"
                      max="3"
                      value={team.additionalRounds[roundIndex]}
                      on:input={(e) => updateScore(teamIndex, 'additionalRounds', e.currentTarget.value, roundIndex)}
                    >
                  </td>
                {/each}
              </tr>
            {/each}
            
            <tr>
              <td>Доп. баллы (0-4)</td>
              {#each teams as team, teamIndex}
                <td>
                  <input
                    type="number"
                    min="0"
                    max="4"
                    value={team.additionalPoints}
                    on:input={(e) => updateScore(teamIndex, 'additionalPoints', e.currentTarget.value)}
                  >
                </td>
              {/each}
            </tr>
            
            <tr>
              <td>Репутация</td>
              {#each teams as team, teamIndex}
                <td>
                  <input
                    type="number"
                    min="0"
                    value={team.reputation}
                    on:input={(e) => updateScore(teamIndex, 'reputation', e.currentTarget.value)}
                  >
                </td>
              {/each}
            </tr>
            
            <tr class="total-row">
              <td>Итого:</td>
              {#each teams as team}
                <td>{team.total}</td>
              {/each}
            </tr>
          </tbody>
        </table>
      </div>
    </section>
  {/if}
</div>

<style>
  .judge-page {
    padding: 2rem;
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    box-sizing: border-box;
  }

  .page-header {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 2rem;
  }

  .page-header h2 {
    color: #ff5c5c;
    font-size: 2.5rem;
    margin: 0;
    font-weight: 800;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  .setup-section {
    background-color: #292929;
    padding: 2rem;
    border-radius: 12px;
    margin-bottom: 2rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
  }

  .setup-section h3 {
    color: #ff5c5c;
    font-size: 1.8rem;
    margin-bottom: 1.5rem;
    text-align: center;
  }

  .setup-form {
    max-width: 400px;
    margin: 0 auto;
  }

  .form-group {
    margin-bottom: 1.5rem;
  }

  .form-group label {
    display: block;
    margin-bottom: 0.5rem;
    color: #f4f4f4;
  }

  .form-group input {
    width: 100%;
    padding: 0.8rem;
    background-color: #1a1a1a;
    border: 1px solid #444;
    border-radius: 4px;
    color: #f4f4f4;
  }

  .start-button {
    width: 100%;
    padding: 1rem;
    background-color: #ff5c5c;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 1.1rem;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .start-button:hover {
    background-color: #ff7878;
  }

  .controls {
    display: flex;
    gap: 1rem;
    margin-bottom: 1rem;
  }

  .controls button {
    padding: 0.5rem 1rem;
    background-color: #1a1a1a;
    color: #f4f4f4;
    border: 1px solid #444;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.3s;
  }

  .controls button:hover {
    background-color: #333;
    border-color: #ff5c5c;
  }

  .score-table {
    background-color: #292929;
    padding: 2rem;
    border-radius: 12px;
    margin-bottom: 2rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
    width: 100%;
    box-sizing: border-box;
  }

  .table-container {
    overflow-x: auto;
    width: 100%;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 1rem;
    background-color: #333;
  }

  th, td {
    padding: 1rem;
    text-align: center;
    border: 1px solid #444;
    color: #f4f4f4;
  }

  th {
    background-color: #1a1a1a;
    color: #ff5c5c;
    font-weight: bold;
  }

  td:first-child {
    background-color: #1a1a1a;
    color: #ff5c5c;
    font-weight: bold;
    text-align: left;
    white-space: nowrap;
  }

  input {
    width: 60px;
    padding: 0.5rem;
    text-align: center;
    background-color: #292929;
    border: 1px solid #444;
    border-radius: 4px;
    color: #f4f4f4;
    font-size: 1rem;
  }

  input:focus {
    outline: none;
    border-color: #ff5c5c;
  }

  .total-row {
    background-color: #1a1a1a;
    font-weight: bold;
  }

  .total-row td {
    color: #ff5c5c;
  }

  @media (max-width: 768px) {
    .judge-page {
      padding: 1rem;
    }

    .page-header h2 {
      font-size: 2rem;
    }

    .score-table {
      padding: 1rem;
    }

    .controls {
      flex-direction: column;
    }

    th, td {
      padding: 0.5rem;
      font-size: 0.9rem;
    }

    input {
      width: 50px;
      padding: 0.3rem;
      font-size: 0.9rem;
    }
  }
</style> 