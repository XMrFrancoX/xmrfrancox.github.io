<script>
  import { onMount } from 'svelte';

  const skills = [
    { name: 'HTML & CSS', icon: 'fab fa-html5', level: 90, color: '#e34f26' },
    { name: 'JavaScript', icon: 'fab fa-js', level: 75, color: '#f7df1e' },
    { name: 'Python', icon: 'fab fa-python', level: 70, color: '#3776ab' },
    { name: 'Git & GitHub', icon: 'fab fa-github', level: 80, color: '#f0f6ff' },
    { name: 'Node.js', icon: 'fab fa-node-js', level: 45, color: '#68a063' },
    { name: 'SQL / Databases', icon: 'fas fa-database', level: 50, color: '#0ea5e9' },
  ];

  let section;
  let animated = $state(false);

  onMount(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          animated = true;
          observer.disconnect();
        }
      },
      { threshold: 0.3 }
    );
    if (section) observer.observe(section);
    return () => observer.disconnect();
  });
</script>

<section id="skills" bind:this={section}>
  <div class="section-container">
    <h2 class="section-title">Mis <span>Skills</span></h2>

    <div class="skills-grid">
      {#each skills as skill, i}
        <div
          class="skill-card glass-card"
          style="--delay: {i * 0.1}s"
          class:animated
        >
          <div class="skill-header">
            <div class="skill-icon" style="--icon-color: {skill.color}">
              <i class={skill.icon}></i>
            </div>
            <div class="skill-info">
              <span class="skill-name">{skill.name}</span>
              <span class="skill-percent">{animated ? skill.level : 0}%</span>
            </div>
          </div>

          <div class="progress-track">
            <div
              class="progress-bar"
              style="
                --target-width: {skill.level}%;
                --bar-color: {skill.color};
                animation-delay: {i * 0.1 + 0.3}s;
              "
              class:animated
            ></div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  section {
    padding: 6rem 0;
  }

  .section-container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  .section-title {
    font-family: 'Kanit', sans-serif;
    font-size: clamp(2rem, 5vw, 2.8rem);
    font-weight: 700;
    text-align: center;
    margin-bottom: 3.5rem;
    color: #f0f6ff;
    position: relative;
    display: inline-block;
    left: 50%;
    transform: translateX(-50%);
  }

  .section-title span {
    color: #0ea5e9;
  }

  .section-title::after {
    content: '';
    position: absolute;
    bottom: -12px;
    left: 50%;
    transform: translateX(-50%);
    width: 60px;
    height: 3px;
    background: linear-gradient(90deg, #0ea5e9, #38bdf8);
    border-radius: 99px;
  }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
  }

  .skill-card {
    padding: 1.5rem;
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 16px;
    backdrop-filter: blur(12px);
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.5s ease var(--delay), transform 0.5s ease var(--delay),
      background 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
  }

  .skill-card.animated {
    opacity: 1;
    transform: translateY(0);
  }

  .skill-card:hover {
    background: rgba(255, 255, 255, 0.08);
    border-color: rgba(14, 165, 233, 0.4);
    box-shadow: 0 0 30px rgba(14, 165, 233, 0.1);
    transform: translateY(-4px);
  }

  .skill-header {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 1rem;
  }

  .skill-icon {
    width: 44px;
    height: 44px;
    border-radius: 10px;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.08);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.4rem;
    color: var(--icon-color);
    flex-shrink: 0;
  }

  .skill-info {
    display: flex;
    flex-direction: column;
    gap: 2px;
    flex: 1;
  }

  .skill-name {
    font-weight: 600;
    font-size: 0.95rem;
    color: #f0f6ff;
  }

  .skill-percent {
    font-size: 0.85rem;
    color: #0ea5e9;
    font-weight: 700;
  }

  .progress-track {
    height: 6px;
    background: rgba(255, 255, 255, 0.08);
    border-radius: 99px;
    overflow: hidden;
  }

  .progress-bar {
    height: 100%;
    width: 0;
    border-radius: 99px;
    background: linear-gradient(90deg, var(--bar-color, #0ea5e9), #38bdf8);
    box-shadow: 0 0 10px var(--bar-color, #0ea5e9);
    transition: width 0s;
  }

  .progress-bar.animated {
    animation: fillBar 1.2s cubic-bezier(0.4, 0, 0.2, 1) var(--delay, 0s) forwards;
  }

  @keyframes fillBar {
    from { width: 0; }
    to { width: var(--target-width); }
  }
</style>
