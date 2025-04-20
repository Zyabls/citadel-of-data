<script>
  const currentYear = new Date().getFullYear();
</script>

<footer>
  <div class="footer-container">
    <div class="footer-logo">
      <img src="/mnt/data/image.png" alt="Цитадель данных" class="footer-logo-image">
    </div>
    
    <div class="footer-links">
      <a href="/">Главная</a>
      <a href="/how-to-play">Как играть</a>
      <a href="/encyclopedia">Энциклопедия</a>
      <a href="/judge">Судья</a>
    </div>
    
    <div class="footer-social">
      <a href="#" class="social-icon">📘</a>
      <a href="#" class="social-icon">📱</a>
      <a href="#" class="social-icon">📸</a>
    </div>
    
    <div class="footer-bottom">
      <p>&copy; {currentYear} Цитадель данных. Все права защищены.</p>
    </div>
  </div>
</footer>

<style>
  footer {
    background-color: #1a1a1a;
    color: #f4f4f4;
    padding: 2rem 0 1rem;
    margin-top: 3rem;
    border-top: 1px solid #333;
  }
  
  .footer-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .footer-logo {
    margin-bottom: 1.5rem;
  }
  
  .footer-logo-image {
    height: 60px;
    width: auto;
  }
  
  .footer-links {
    display: flex;
    justify-content: center;
    gap: 2rem;
    margin-bottom: 1.5rem;
    flex-wrap: wrap;
  }
  
  .footer-links a {
    color: #f4f4f4;
    text-decoration: none;
    font-size: 0.9rem;
    transition: color 0.3s ease;
  }
  
  .footer-links a:hover {
    color: #999;
  }
  
  .footer-social {
    display: flex;
    gap: 1.5rem;
    margin-bottom: 1.5rem;
  }
  
  .social-icon {
    color: #f4f4f4;
    text-decoration: none;
    font-size: 1.2rem;
    transition: color 0.3s ease;
  }
  
  .social-icon:hover {
    color: #999;
  }
  
  .footer-bottom {
    text-align: center;
    padding-top: 1rem;
    border-top: 1px solid #333;
    width: 100%;
  }
  
  .footer-bottom p {
    color: #999;
    font-size: 0.8rem;
  }
  
  @media (max-width: 768px) {
    footer {
      padding: 1.5rem 0 1rem;
    }
    
    .footer-container {
      padding: 0 1rem;
    }
    
    .footer-logo-image {
      height: 50px;
    }
    
    .footer-links {
      gap: 1rem;
    }
  }
</style> 