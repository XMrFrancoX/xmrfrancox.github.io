<footer>
  <div class="footer-container">
    <div class="footer-top">
      <span class="logo">
        <span class="logo-bracket">&lt;</span>Franco<span class="logo-accent">X</span><span class="logo-bracket">/&gt;</span>
      </span>
      <p class="footer-text">Desarrollador Full Stack · Siempre aprendiendo, siempre construyendo.</p>
    </div>

    <div class="footer-links">
      <a href="https://github.com/XMrFrancoX" target="_blank" rel="noopener" aria-label="GitHub">
        <i class="fab fa-github"></i>
      </a>
      <a href="https://linkedin.com" target="_blank" rel="noopener" aria-label="LinkedIn">
        <i class="fab fa-linkedin-in"></i>
      </a>
    </div>

    <div class="footer-bottom">
      <p>© {new Date().getFullYear()} Franco Ortiz Ruiz · Hecho con <span class="heart">♥</span> y SvelteKit</p>
    </div>
  </div>
</footer>

<style>
  footer {
    padding: 3rem 0 2rem;
    border-top: 1px solid rgba(255, 255, 255, 0.06);
    background: rgba(5, 10, 20, 0.8);
  }

  .footer-container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1.5rem;
    text-align: center;
  }

  .footer-top {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
  }

  .logo {
    font-family: 'Kanit', sans-serif;
    font-size: 1.4rem;
    font-weight: 700;
    color: #f0f6ff;
  }

  .logo-bracket { color: #64748b; }
  .logo-accent { color: #0ea5e9; }

  .footer-text {
    font-size: 0.9rem;
    color: #64748b;
  }

  .footer-links {
    display: flex;
    gap: 1rem;
  }

  .footer-links a {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.08);
    color: #64748b;
    text-decoration: none;
    font-size: 1rem;
    transition: all 0.3s ease;
  }

  .footer-links a:hover {
    background: rgba(14, 165, 233, 0.15);
    border-color: #0ea5e9;
    color: #0ea5e9;
    transform: translateY(-3px);
  }

  .footer-bottom p {
    font-size: 0.82rem;
    color: #334155;
  }

  .heart {
    color: #0ea5e9;
  }
</style>
