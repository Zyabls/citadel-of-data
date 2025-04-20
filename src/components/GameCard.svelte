<script>
  export let imageUrl;
  export let isThirdCard = false;
</script>

<div class="game-card" class:third-card={isThirdCard}>
    <img src={imageUrl} alt="Game Card">
</div>

<style>
    .game-card {
        width: 250px;
        height: 350px;
        background-color: #333;
        border-radius: 15px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        position: relative;
        overflow: hidden;
        opacity: 0.3;
        transform: translateX(-50%);
        transition: transform 0.5s ease, opacity 0.5s ease, box-shadow 0.3s ease;
        margin: 0 auto;
    }
    .game-card.third-card {
        height: 350px;
        width: 225px;
    }
    .game-card img {
        width: 100%;
        height: 100%;
        object-fit: contain;
        transition: transform 0.3s ease;
    }
    .game-card:hover img {
        transform: scale(1.1);
    }
    .game-card:hover {
        transform: translateX(0) scale(1.05);
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
    }
</style> 