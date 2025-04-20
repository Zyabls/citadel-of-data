<script lang="ts">
  import Header from './components/Header.svelte';
  import GameCard from './components/GameCard.svelte';
  import Encyclopedia from './components/Encyclopedia.svelte';
  import HowToPlay from './components/HowToPlay.svelte';
  import Judge from './components/Judge.svelte';
  import Footer from './components/Footer.svelte';
  import cardImage from './assets/images/card-image-1.png';
  import cardImage_2 from './assets/images/card-image-2.png';
  import cardImage_3 from './assets/images/card-image-3.png';

  // Game cards data
  const gameCards = [
    {
      imageUrl: cardImage
    },
    {
      imageUrl: cardImage_2
    },
    {
      imageUrl: cardImage_3
    },
    // Add more cards as needed
  ];

  // Handle scroll animation for cards
  function handleScroll() {
    const cards = document.querySelectorAll('.game-card') as NodeListOf<HTMLElement>;
    const scrollPosition = window.scrollY + window.innerHeight;

    cards.forEach((card, index) => {
      const cardTop = card.offsetTop;
      if (scrollPosition - 500 > cardTop) {
        card.style.opacity = '1';
        card.style.transform = 'translateX(0)';
      } else {
        card.style.opacity = '0.3';
        card.style.transform = 'translateX(-50%)';
      }
    });
  }

  // Simple routing
  let currentPath = window.location.pathname;
</script>

<svelte:window on:scroll={handleScroll} on:popstate={() => currentPath = window.location.pathname}/>

<div class="app-container">
  <Header />

  <main>
    {#if currentPath === '/'}
      <section class="game-description">
        <h2>Описание игры</h2>
        <div class="content-text">
          <p>
            Добро пожаловать в «Цитадели данных» – захватывающий ролевой симулятор, где вы погрузитесь в битву за информационную безопасность. Это не просто игра, а испытание для вашего отдела ИБ, где вам предстоит не только строить защиту от киберугроз, но и оттачивать свои навыки. Ваша цель – стать лучшим в мире, где каждая ошибка может стать фатальной.
            В «Цитаделях данных» вы и ваша команда защищаете предприятие, проектируя систему безопасности, управляя ресурсами и реагируя на инциденты. Но берегитесь, это ещё не всё: конкуренты готовы ударить в любой момент, а глобальные события способны внести хаос в самые продуманные планы. Помните о коварстве случая – нужно быть готовым ко всему.
            Игра предлагает два режима: обычный для начинающих и усложненный для экспертов. Каждый режим проверит ваши знания, умения и способность работать в команде. Пройдите шторм кибератак и докажите, что ваша команда – лучшие в информационной безопасности!
            Этот сайт – ваш помощник в «Цитаделях данных». Здесь вы найдете правила, описания карточек, механики, а также базу знаний по ИБ. Изучайте СЗИ, кибератаки и уязвимости, чтобы всегда быть на шаг впереди. Погрузитесь в мир знаний и ведите свою команду к победе!
          </p>
        </div>

        <div class="game-cards">
          {#each gameCards as card, index}
            <GameCard 
              imageUrl={card.imageUrl}
              isThirdCard={index === 2}
            />
          {/each}
        </div>

        <div class="reviews">
          <h3>Отзывы</h3>
          <div class="review-cards">
            <div class="review-card">
              <p>"Прекрасная игра, которая учит основам безопасности в IT!"</p>
              <span class="reviewer">- Иван П.</span>
            </div>
            <div class="review-card">
              <p>"Интересные механики и отличная подача материала."</p>
              <span class="reviewer">- Мария Л.</span>
            </div>
          </div>
        </div>
      </section>
    {:else if currentPath === '/encyclopedia'}
      <Encyclopedia />
    {:else if currentPath === '/how-to-play'}
      <HowToPlay />
    {:else if currentPath === '/judge'}
      <Judge />
    {/if}
  </main>
  
  <Footer />
</div>

<style>
  :global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :global(body) {
    font-family: 'Arial', sans-serif;
    background-color: #1a1a1a;
    color: #f4f4f4;
    line-height: 1.6;
    width: 100%;
    overflow-x: hidden;
  }

  .app-container {
    width: 100%;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  main {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
    width: 100%;
    box-sizing: border-box;
    flex: 1;
  }

  .game-description {
    text-align: center;
    padding: 2rem;
    position: relative;
    width: 100%;
  }

  .content-text {
    background-color: #292929;
    padding: 2rem;
    border-radius: 12px;
    margin: 2rem 0;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
    width: 100%;
    border: 1px solid #333;
  }

  .game-cards {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 30px;
    margin-top: 2rem;
    overflow: visible;
    width: 100%;
  }

  .reviews {
    margin-top: 3rem;
    width: 100%;
  }

  .review-cards {
    display: flex;
    justify-content: center;
    gap: 2rem;
    margin-top: 1.5rem;
    width: 100%;
  }

  .review-card {
    background-color: #292929;
    padding: 1.5rem;
    border-radius: 12px;
    max-width: 400px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
    width: 100%;
    border: 1px solid #333;
    transition: transform 0.3s ease;
  }

  .review-card:hover {
    transform: translateY(-5px);
  }

  .review-card p {
    font-style: italic;
    margin-bottom: 1rem;
  }

  .reviewer {
    color: #ff5c5c;
    font-weight: bold;
  }

  h2 {
    color: #ff5c5c;
    font-size: 2.5rem;
    margin-bottom: 1rem;
    font-weight: 800;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  h3 {
    color: #ff5c5c;
    font-size: 1.8rem;
    margin-bottom: 1rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  @media (max-width: 768px) {
    main {
      padding: 1rem;
    }

    .review-cards {
      flex-direction: column;
      align-items: center;
    }

    .review-card {
      width: 100%;
    }

    h2 {
      font-size: 2rem;
    }

    h3 {
      font-size: 1.5rem;
    }
  }
</style> 