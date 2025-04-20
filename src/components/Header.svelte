<script>
  import { onMount } from 'svelte';
  
  let currentPath = window.location.pathname;
  
  function navigate(path) {
    window.history.pushState({}, '', path);
    window.dispatchEvent(new PopStateEvent('popstate'));
    currentPath = path;
  }
  
  onMount(() => {
    window.addEventListener('popstate', () => {
      currentPath = window.location.pathname;
    });
    
    return () => {
      window.removeEventListener('popstate', () => {
        currentPath = window.location.pathname;
      });
    };
  });
</script>

<header>
  <div class="header-container">
    <div class="logo-container">
      <div class="logo" on:click={() => navigate('/')}>
        <img src="/mnt/data/image.png" alt="Цитадель данных" class="logo-image">
      </div>
    </div>
    <nav>
      <a href="/" on:click|preventDefault={() => navigate('/')} class:active={currentPath === '/'}>Главная</a>
      <a href="/how-to-play" on:click|preventDefault={() => navigate('/how-to-play')} class:active={currentPath === '/how-to-play'}>Как играть</a>
      <a href="/encyclopedia" on:click|preventDefault={() => navigate('/encyclopedia')} class:active={currentPath === '/encyclopedia'}>Энциклопедия</a>
      <a href="/judge" on:click|preventDefault={() => navigate('/judge')} class:active={currentPath === '/judge'}>Судья</a>
    </nav>
  </div>
</header>

<style>
  header {
    background-color: #1a1a1a;
    width: 100%;
    position: relative;
    padding-bottom: 60px;
    border-bottom: 1px solid #333;
  }

  .header-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 1rem 2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    box-sizing: border-box;
  }

  .logo-container {
    display: flex;
    justify-content: center;
    width: 100%;
    margin-bottom: 1rem;
  }

  .logo {
    cursor: pointer;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .logo-image {
    height: 170px;
    width: auto;
  }

  nav {
    display: flex;
    gap: 2rem;
    margin-top: 1rem;
    background-color: #292929;
    padding: 1rem 2rem;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
  }

  a {
    color: #f4f4f4;
    text-decoration: none;
    font-size: 1.1rem;
    transition: all 0.3s ease;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    font-weight: 600;
  }

  a:hover {
    color: #ff5c5c;
    background-color: #333;
  }

  a.active {
    color: #ff5c5c;
    background-color: #333;
  }

  @media (max-width: 768px) {
    header {
      padding-bottom: 40px;
    }

    .header-container {
      padding: 1rem;
    }

    .logo-image {
      height: 120px;
    }

    nav {
      flex-direction: column;
      align-items: center;
      gap: 1rem;
      padding: 1rem;
    }

    a {
      width: 100%;
      text-align: center;
    }
  }
</style> 