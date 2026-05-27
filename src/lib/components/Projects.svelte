<script>
  const projects = [
    {
      title: 'Portfolio Personal',
      description: 'Mi sitio web de portfolio hecho con SvelteKit y adaptador estático para GitHub Pages. Diseño glassmorphism con animaciones CSS.',
      image: null,
      tech: ['SvelteKit', 'CSS', 'JavaScript'],
      github: 'https://github.com/XMrFrancoX/xmrfrancox.github.io',
      demo: 'https://xmrfrancox.github.io',
      featured: true,
    },
    {
      title: 'Proyecto 2',
      description: 'Descripción de tu segundo proyecto. ¡Actualizá esta información con tus proyectos reales!',
      image: null,
      tech: ['JavaScript', 'HTML', 'CSS'],
      github: 'https://github.com/XMrFrancoX',
      demo: null,
      featured: false,
    },
    {
      title: 'Proyecto 3',
      description: 'Descripción de tu tercer proyecto. Podés agregar APIs, backends, o cualquier stack que uses.',
      image: null,
      tech: ['Python', 'Flask', 'SQL'],
      github: 'https://github.com/XMrFrancoX',
      demo: null,
      featured: false,
    },
  ];

  function getPlaceholderGradient(i) {
    const gradients = [
      'linear-gradient(135deg, #0ea5e9 0%, #38bdf8 50%, #0284c7 100%)',
      'linear-gradient(135deg, #6366f1 0%, #818cf8 50%, #4f46e5 100%)',
      'linear-gradient(135deg, #10b981 0%, #34d399 50%, #059669 100%)',
    ];
    return gradients[i % gradients.length];
  }
</script>

<section id="projects">
  <div class="section-container">
    <h2 class="section-title">Mis <span>Proyectos</span></h2>

    <div class="projects-grid">
      {#each projects as project, i}
        <article class="project-card glass-card" class:featured={project.featured}>
          <!-- Preview image / placeholder -->
          <div class="card-preview" style="background: {getPlaceholderGradient(i)}">
            {#if project.image}
              <img src={project.image} alt={project.title} />
            {:else}
              <div class="preview-icon">
                <i class="fas fa-code"></i>
              </div>
            {/if}
            {#if project.featured}
              <span class="featured-badge">
                <i class="fas fa-star"></i> Featured
              </span>
            {/if}
          </div>

          <div class="card-body">
            <h3 class="card-title">{project.title}</h3>
            <p class="card-desc">{project.description}</p>

            <div class="card-tech">
              {#each project.tech as t}
                <span class="tech-badge">{t}</span>
              {/each}
            </div>

            <div class="card-links">
              <a href={project.github} target="_blank" rel="noopener" class="link-btn">
                <i class="fab fa-github"></i>
                GitHub
              </a>
              {#if project.demo}
                <a href={project.demo} target="_blank" rel="noopener" class="link-btn primary">
                  <i class="fas fa-external-link-alt"></i>
                  Demo
                </a>
              {/if}
            </div>
          </div>
        </article>
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

  /* Grid */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.75rem;
    margin-bottom: 4rem;
  }

  /* Card */
  .project-card {
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 16px;
    overflow: hidden;
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
  }

  .project-card:hover {
    background: rgba(255, 255, 255, 0.08);
    border-color: rgba(14, 165, 233, 0.4);
    box-shadow: 0 0 35px rgba(14, 165, 233, 0.15);
    transform: translateY(-6px);
  }

  .project-card.featured {
    border-color: rgba(14, 165, 233, 0.3);
  }

  /* Preview */
  .card-preview {
    position: relative;
    height: 160px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .card-preview img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .preview-icon {
    font-size: 3rem;
    color: rgba(255, 255, 255, 0.3);
  }

  .featured-badge {
    position: absolute;
    top: 0.75rem;
    right: 0.75rem;
    padding: 0.25rem 0.6rem;
    background: rgba(14, 165, 233, 0.85);
    color: #fff;
    font-size: 0.72rem;
    font-weight: 700;
    border-radius: 99px;
    display: flex;
    align-items: center;
    gap: 0.25rem;
    backdrop-filter: blur(8px);
  }

  /* Body */
  .card-body {
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
    flex: 1;
    gap: 0.75rem;
  }

  .card-title {
    font-family: 'Kanit', sans-serif;
    font-size: 1.2rem;
    font-weight: 700;
    color: #f0f6ff;
  }

  .card-desc {
    font-size: 0.9rem;
    color: #94a3b8;
    line-height: 1.7;
    flex: 1;
  }

  .card-tech {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
  }

  .tech-badge {
    padding: 0.2rem 0.65rem;
    background: rgba(14, 165, 233, 0.08);
    border: 1px solid rgba(14, 165, 233, 0.2);
    border-radius: 99px;
    font-size: 0.72rem;
    color: #38bdf8;
    font-weight: 500;
  }

  .card-links {
    display: flex;
    gap: 0.75rem;
    margin-top: 0.5rem;
  }

  .link-btn {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    padding: 0.45rem 1rem;
    border-radius: 99px;
    font-size: 0.85rem;
    font-weight: 600;
    text-decoration: none;
    border: 1px solid rgba(255, 255, 255, 0.12);
    color: #94a3b8;
    transition: all 0.3s ease;
    background: rgba(255, 255, 255, 0.04);
  }

  .link-btn:hover {
    border-color: rgba(14, 165, 233, 0.5);
    color: #0ea5e9;
    background: rgba(14, 165, 233, 0.08);
  }

  .link-btn.primary {
    border-color: rgba(14, 165, 233, 0.4);
    color: #0ea5e9;
    background: rgba(14, 165, 233, 0.08);
  }

  .link-btn.primary:hover {
    background: rgba(14, 165, 233, 0.2);
  }

  /* GitHub Stats */
  .github-stats {
    text-align: center;
  }

  .stats-title {
    font-family: 'Kanit', sans-serif;
    font-size: 1.6rem;
    font-weight: 600;
    color: #f0f6ff;
    margin-bottom: 2rem;
  }

  .stats-title span {
    color: #0ea5e9;
  }

  .stats-row {
    display: flex;
    flex-wrap: wrap;
    gap: 1.5rem;
    justify-content: center;
    margin-bottom: 1.5rem;
  }

  .streak-wrap {
    display: flex;
    justify-content: center;
    margin-bottom: 2rem;
  }

  .streak-img {
    max-width: 500px;
    width: 100%;
  }

  .calendar-wrap {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }

  .calendar-label {
    font-size: 0.85rem;
    color: #64748b;
    display: flex;
    align-items: center;
    gap: 0.4rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    font-weight: 600;
  }

  .calendar-img {
    max-width: 800px;
    width: 100%;
    border-radius: 12px;
    filter: brightness(1.1) saturate(1.1);
  }

  .stats-img {
    border-radius: 12px;
    border: 1px solid rgba(255, 255, 255, 0.08);
    max-width: 100%;
    height: auto;
    transition: all 0.3s ease;
  }

  .stats-img:hover {
    border-color: rgba(14, 165, 233, 0.3);
    box-shadow: 0 0 25px rgba(14, 165, 233, 0.1);
    transform: translateY(-4px);
  }

  @media (max-width: 600px) {
    .projects-grid {
      grid-template-columns: 1fr;
    }
  }
</style>
