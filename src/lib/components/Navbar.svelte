<script>
  import { onMount } from 'svelte';

  let scrolled = $state(false);
  let menuOpen = $state(false);

  onMount(() => {
    const handleScroll = () => {
      scrolled = window.scrollY > 50;
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  });

  function closeMenu() {
    menuOpen = false;
  }
</script>

<header class:scrolled>
  <nav class="nav-container">
    <a href="#hero" class="logo" onclick={closeMenu}>
      <span class="logo-bracket">&lt;</span>Franco<span class="logo-accent">X</span><span class="logo-bracket">/&gt;</span>
    </a>

    <button
      class="burger"
      class:open={menuOpen}
      onclick={() => (menuOpen = !menuOpen)}
      aria-label="Toggle menu"
    >
      <span></span>
      <span></span>
      <span></span>
    </button>

    <ul class="nav-links" class:open={menuOpen}>
      <li><a href="#about" onclick={closeMenu}>Sobre mí</a></li>
      <li><a href="#skills" onclick={closeMenu}>Skills</a></li>
      <li><a href="#experience" onclick={closeMenu}>Experiencia</a></li>
      <li><a href="#projects" onclick={closeMenu}>Proyectos</a></li>
      <li><a href="#contact" onclick={closeMenu}>Contacto</a></li>
    </ul>
  </nav>
</header>

<style>
  header {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    padding: 1rem 0;
    transition: all 0.4s ease;
  }

  header.scrolled {
    background: rgba(5, 10, 20, 0.85);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(14, 165, 233, 0.15);
    padding: 0.6rem 0;
    box-shadow: 0 4px 30px rgba(0, 0, 0, 0.3);
  }

  .nav-container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 2rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .logo {
    font-family: 'Kanit', sans-serif;
    font-size: 1.4rem;
    font-weight: 700;
    color: #f0f6ff;
    text-decoration: none;
    letter-spacing: -0.02em;
  }

  .logo-bracket {
    color: #64748b;
  }

  .logo-accent {
    color: #0ea5e9;
  }

  .nav-links {
    display: flex;
    list-style: none;
    gap: 2rem;
    align-items: center;
  }

  .nav-links a {
    color: #94a3b8;
    text-decoration: none;
    font-size: 0.9rem;
    font-weight: 500;
    letter-spacing: 0.03em;
    transition: color 0.3s ease;
    position: relative;
    padding-bottom: 2px;
  }

  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 0;
    height: 2px;
    background: linear-gradient(90deg, #0ea5e9, #38bdf8);
    border-radius: 99px;
    transition: width 0.3s ease;
  }

  .nav-links a:hover {
    color: #0ea5e9;
  }

  .nav-links a:hover::after {
    width: 100%;
  }

  /* Burger */
  .burger {
    display: none;
    flex-direction: column;
    gap: 5px;
    background: none;
    border: none;
    cursor: pointer;
    padding: 4px;
  }

  .burger span {
    display: block;
    width: 24px;
    height: 2px;
    background: #94a3b8;
    border-radius: 99px;
    transition: all 0.3s ease;
  }

  .burger.open span:nth-child(1) {
    transform: translateY(7px) rotate(45deg);
    background: #0ea5e9;
  }

  .burger.open span:nth-child(2) {
    opacity: 0;
  }

  .burger.open span:nth-child(3) {
    transform: translateY(-7px) rotate(-45deg);
    background: #0ea5e9;
  }

  @media (max-width: 768px) {
    .burger {
      display: flex;
    }

    .nav-links {
      position: fixed;
      top: 0;
      right: -100%;
      width: 260px;
      height: 100vh;
      background: rgba(5, 10, 20, 0.97);
      backdrop-filter: blur(20px);
      flex-direction: column;
      justify-content: center;
      gap: 2.5rem;
      padding: 2rem;
      border-left: 1px solid rgba(14, 165, 233, 0.15);
      transition: right 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .nav-links.open {
      right: 0;
    }

    .nav-links a {
      font-size: 1.1rem;
    }
  }
</style>
