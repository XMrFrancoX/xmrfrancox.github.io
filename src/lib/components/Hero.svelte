<script>
  import { onMount } from 'svelte';

  let visible = $state(false);

  onMount(() => {
    setTimeout(() => (visible = true), 100);
  });
</script>

<section id="hero">
  <div class="hero-container" class:visible>
    <!-- Profile Image -->
    <div class="hero-image-wrap">
      <div class="glow-ring"></div>
      <img src="/Perfil.png" alt="Franco Ortiz Ruiz" class="hero-img" />
    </div>

    <!-- Text content -->
    <div class="hero-text">
      <p class="hero-greeting">Hola, soy</p>
      <h1 class="hero-name">Franco <span>Ortiz</span></h1>
      <p class="hero-subtitle">
        Desarrollador <span>Full Stack</span> · Backend & Frontend
      </p>
      <p class="hero-desc">
        Apasionado por el desarrollo de aplicaciones web modernas, con experiencia
        en JavaScript, Python y tecnologías cloud.
      </p>

      <div class="hero-actions">
        <a href="#projects" class="btn-primary">
          <i class="fas fa-rocket"></i>
          Ver proyectos
        </a>
        <a href="#contact" class="btn-outline">
          <i class="fas fa-envelope"></i>
          Contactame
        </a>
      </div>

      <div class="hero-socials">
        <a href="https://github.com/XMrFrancoX" target="_blank" rel="noopener" aria-label="GitHub">
          <i class="fab fa-github"></i>
        </a>
        <a href="https://linkedin.com" target="_blank" rel="noopener" aria-label="LinkedIn">
          <i class="fab fa-linkedin-in"></i>
        </a>
      </div>
    </div>
  </div>

  <!-- Scroll indicator -->
  <div class="scroll-indicator">
    <div class="scroll-dot"></div>
  </div>
</section>

<style>
  section {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 6rem 2rem 4rem;
    position: relative;
  }

  .hero-container {
    max-width: 1100px;
    width: 100%;
    display: flex;
    align-items: center;
    gap: 5rem;
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.9s ease, transform 0.9s ease;
  }

  .hero-container.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* Image */
  .hero-image-wrap {
    position: relative;
    flex-shrink: 0;
  }

  .glow-ring {
    position: absolute;
    inset: -8px;
    border-radius: 50%;
    background: conic-gradient(
      from 0deg,
      #0ea5e9,
      #38bdf8,
      #0ea5e9,
      transparent 60%,
      #0ea5e9
    );
    animation: spin 4s linear infinite;
    filter: blur(2px);
  }

  @keyframes spin {
    to { transform: rotate(360deg); }
  }

  .hero-img {
    position: relative;
    width: 240px;
    height: 240px;
    border-radius: 50%;
    object-fit: cover;
    border: 4px solid var(--bg-primary, #050a14);
    z-index: 1;
    display: block;
  }

  /* Text */
  .hero-text {
    flex: 1;
  }

  .hero-greeting {
    font-size: 1.1rem;
    color: #94a3b8;
    margin-bottom: 0.5rem;
    font-weight: 400;
  }

  .hero-name {
    font-family: 'Kanit', sans-serif;
    font-size: clamp(3rem, 7vw, 5rem);
    font-weight: 800;
    line-height: 1;
    margin-bottom: 0.8rem;
    color: #f0f6ff;
  }

  .hero-name span {
    color: #0ea5e9;
  }

  .hero-subtitle {
    font-size: 1.1rem;
    font-weight: 600;
    color: #94a3b8;
    margin-bottom: 1rem;
  }

  .hero-subtitle span {
    color: #38bdf8;
  }

  .hero-desc {
    font-size: 1rem;
    color: #64748b;
    max-width: 480px;
    margin-bottom: 2rem;
    line-height: 1.8;
  }

  .hero-actions {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    margin-bottom: 2rem;
  }

  /* Buttons from global */
  :global(.btn-primary), :global(.btn-outline) {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.75rem 1.75rem;
    font-family: 'Poppins', sans-serif;
    font-weight: 600;
    font-size: 0.95rem;
    text-decoration: none;
    border-radius: 50px;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  :global(.btn-primary) {
    background: linear-gradient(135deg, #0ea5e9, #38bdf8);
    color: #fff;
    border: none;
    box-shadow: 0 4px 20px rgba(14, 165, 233, 0.35);
  }

  :global(.btn-primary):hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 30px rgba(14, 165, 233, 0.5);
  }

  :global(.btn-outline) {
    background: transparent;
    color: #0ea5e9;
    border: 2px solid #0ea5e9;
  }

  :global(.btn-outline):hover {
    background: #0ea5e9;
    color: #fff;
    transform: translateY(-2px);
  }

  /* Socials */
  .hero-socials {
    display: flex;
    gap: 1rem;
  }

  .hero-socials a {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 42px;
    height: 42px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    color: #94a3b8;
    text-decoration: none;
    font-size: 1.1rem;
    transition: all 0.3s ease;
  }

  .hero-socials a:hover {
    background: rgba(14, 165, 233, 0.15);
    border-color: #0ea5e9;
    color: #0ea5e9;
    transform: translateY(-3px);
  }

  /* Scroll indicator */
  .scroll-indicator {
    position: absolute;
    bottom: 2rem;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .scroll-dot {
    width: 6px;
    height: 6px;
    background: #0ea5e9;
    border-radius: 50%;
    animation: bounce 2s ease-in-out infinite;
    box-shadow: 0 0 10px #0ea5e9;
  }

  @keyframes bounce {
    0%, 100% { transform: translateY(0); opacity: 1; }
    50% { transform: translateY(12px); opacity: 0.4; }
  }

  /* Responsive */
  @media (max-width: 768px) {
    .hero-container {
      flex-direction: column;
      text-align: center;
      gap: 2.5rem;
    }

    .hero-desc {
      max-width: 100%;
    }

    .hero-actions {
      justify-content: center;
    }

    .hero-socials {
      justify-content: center;
    }

    .hero-img {
      width: 180px;
      height: 180px;
    }
  }
</style>
