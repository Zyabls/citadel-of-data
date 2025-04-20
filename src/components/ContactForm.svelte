<script>
  // No form handling needed
</script>

<section class="contact-section">
  <h2>Контакты</h2>
  
  <div class="contact-info">
    <div class="contact-card">
      <div class="icon">📧</div>
      <h3>Email</h3>
      <p>info@citadel-of-data.ru</p>
    </div>
    
    <div class="contact-card">
      <div class="icon">📱</div>
      <h3>Телефон</h3>
      <p>+7 (999) 123-45-67</p>
    </div>
    
    <div class="contact-card">
      <div class="icon">📍</div>
      <h3>Адрес</h3>
      <p>г. Москва, ул. Цифровая, д. 42</p>
    </div>
  </div>
  
  <div class="social-links">
    <a href="#" class="social-link">
      <div class="icon">📘</div>
      <span>VK</span>
    </a>
    <a href="#" class="social-link">
      <div class="icon">📱</div>
      <span>Telegram</span>
    </a>
    <a href="#" class="social-link">
      <div class="icon">📸</div>
      <span>Instagram</span>
    </a>
  </div>
</section>

<style>
  .contact-section {
    padding: 3rem 2rem;
    background-color: #292929;
    border-radius: 12px;
    margin-top: 3rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
    text-align: center;
  }
  
  h2 {
    color: #ff5c5c;
    font-size: 2rem;
    margin-bottom: 2rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 1px;
  }
  
  .contact-info {
    display: flex;
    justify-content: center;
    gap: 2rem;
    margin-bottom: 2rem;
    flex-wrap: wrap;
  }
  
  .contact-card {
    background-color: #333;
    padding: 1.5rem;
    border-radius: 10px;
    width: 250px;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .contact-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 15px rgba(0, 0, 0, 0.3);
  }
  
  .icon {
    font-size: 2rem;
    margin-bottom: 1rem;
  }
  
  h3 {
    color: #ff5c5c;
    font-size: 1.2rem;
    margin-bottom: 0.5rem;
  }
  
  p {
    color: #f4f4f4;
    font-size: 1rem;
  }
  
  .social-links {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    margin-top: 2rem;
  }
  
  .social-link {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-decoration: none;
    color: #f4f4f4;
    transition: transform 0.3s ease;
  }
  
  .social-link:hover {
    transform: scale(1.1);
    color: #ff5c5c;
  }
  
  .social-link .icon {
    font-size: 1.8rem;
    margin-bottom: 0.5rem;
  }
  
  .social-link span {
    font-size: 0.9rem;
    font-weight: 600;
  }
  
  @media (max-width: 768px) {
    .contact-section {
      padding: 2rem 1rem;
    }
    
    .contact-info {
      gap: 1rem;
    }
    
    .contact-card {
      width: 100%;
    }
    
    .social-links {
      flex-wrap: wrap;
    }
  }
</style> 