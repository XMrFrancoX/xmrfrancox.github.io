<script>
  const timeline = [
    {
      period: '2024 – Presente',
      role: 'Desarrollador Web Freelance',
      company: 'Independiente',
      description: 'Desarrollo de sitios y aplicaciones web para clientes. Diseño de interfaces, integración de APIs y deployment en plataformas cloud.',
      tags: ['JavaScript', 'Python', 'HTML/CSS'],
      icon: 'fas fa-laptop-code',
    },
    {
      period: '2023 – 2024',
      role: 'Pasante en Sistemas',
      company: 'Institución Educativa (Escuela)',
      description: 'Pasantía en el área de sistemas de la institución. Desarrollé 3 aplicaciones web internas: sistema de gestión de carros de laptops, sistema de registro de ingresos, egresos y alumnos, y sistema de inventario del pañol.',
      tags: ['HTML', 'CSS', 'JavaScript', 'PHP', 'MySQL'],
      icon: 'fas fa-school',
      projects: [
        { name: 'Gestión de carros de laptops', desc: 'Control de préstamo y devolución de laptops' },
        { name: 'Ingresos, Egresos y Alumnos', desc: 'Sistema de registro y seguimiento de movimientos' },
        { name: 'Inventario Pañol', desc: 'Gestión del inventario de herramientas y materiales' },
      ],
    },
    {
      period: '2022 – 2023',
      role: 'Estudiante de Desarrollo Web',
      company: 'Formación propia + cursos online',
      description: 'Aprendizaje autodidacta de desarrollo web full stack. Completé cursos en Udemy, freeCodeCamp y construcción de proyectos personales.',
      tags: ['HTML', 'CSS', 'JavaScript', 'Python', 'Git'],
      icon: 'fas fa-graduation-cap',
    },
  ];

</script>

<section id="experience">
  <div class="section-container">
    <h2 class="section-title">Mi <span>Experiencia</span></h2>

    <div class="timeline">
      {#each timeline as item, i}
        <div class="timeline-item" class:right={i % 2 === 1}>
          <div class="timeline-dot">
            <i class={item.icon}></i>
          </div>

          <div class="timeline-card glass-card">
            <div class="card-period">
              <i class="far fa-calendar-alt"></i>
              {item.period}
            </div>
            <h3 class="card-role">{item.role}</h3>
            <p class="card-company">
              <i class="fas fa-building"></i>
              {item.company}
            </p>
            <p class="card-desc">{item.description}</p>
            {#if item.projects}
              <ul class="card-projects">
                {#each item.projects as p}
                  <li>
                    <span class="proj-name">{p.name}</span>
                    <span class="proj-desc"> — {p.desc}</span>
                  </li>
                {/each}
              </ul>
            {/if}
            <div class="card-tags">
              {#each item.tags as tag}
                <span class="tag">{tag}</span>
              {/each}
            </div>
          </div>
        </div>
      {/each}

      <!-- Timeline vertical line -->
      <div class="timeline-line"></div>
    </div>
  </div>
</section>

<style>
  section {
    padding: 6rem 0;
    background: linear-gradient(180deg, transparent, rgba(14, 165, 233, 0.03), transparent);
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
    margin-bottom: 4rem;
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

  /* Timeline */
  .timeline {
    position: relative;
    display: flex;
    flex-direction: column;
    gap: 3rem;
    padding: 0 0 2rem;
  }

  .timeline-line {
    position: absolute;
    left: 50%;
    top: 0;
    bottom: 0;
    width: 2px;
    background: linear-gradient(180deg, transparent, #0ea5e9 20%, #38bdf8 80%, transparent);
    transform: translateX(-50%);
    opacity: 0.4;
  }

  .timeline-item {
    display: flex;
    align-items: flex-start;
    gap: 2rem;
    justify-content: flex-start;
    position: relative;
    padding-right: calc(50% + 2rem);
  }

  .timeline-item.right {
    flex-direction: row-reverse;
    justify-content: flex-start;
    padding-right: 0;
    padding-left: calc(50% + 2rem);
  }

  .timeline-dot {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    width: 44px;
    height: 44px;
    border-radius: 50%;
    background: linear-gradient(135deg, #0ea5e9, #38bdf8);
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    font-size: 1rem;
    box-shadow: 0 0 20px rgba(14, 165, 233, 0.5);
    z-index: 2;
    flex-shrink: 0;
    top: 1.5rem;
  }

  .timeline-card {
    flex: 1;
    padding: 1.5rem;
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 16px;
    backdrop-filter: blur(12px);
    transition: all 0.3s ease;
    max-width: calc(50% - 3rem);
    width: 100%;
  }

  .timeline-card:hover {
    background: rgba(255, 255, 255, 0.08);
    border-color: rgba(14, 165, 233, 0.4);
    box-shadow: 0 0 30px rgba(14, 165, 233, 0.15);
    transform: translateY(-4px);
  }

  .card-period {
    display: flex;
    align-items: center;
    gap: 0.4rem;
    font-size: 0.8rem;
    color: #0ea5e9;
    font-weight: 600;
    margin-bottom: 0.5rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .card-role {
    font-family: 'Kanit', sans-serif;
    font-size: 1.2rem;
    font-weight: 700;
    color: #f0f6ff;
    margin-bottom: 0.3rem;
  }

  .card-company {
    display: flex;
    align-items: center;
    gap: 0.4rem;
    font-size: 0.9rem;
    color: #64748b;
    margin-bottom: 0.8rem;
  }

  .card-desc {
    font-size: 0.9rem;
    color: #94a3b8;
    line-height: 1.7;
    margin-bottom: 1rem;
  }

  .card-projects {
    list-style: none;
    padding: 0;
    margin: 0 0 1rem;
    display: flex;
    flex-direction: column;
    gap: 0.4rem;
  }

  .card-projects li {
    font-size: 0.85rem;
    line-height: 1.5;
    padding: 0.3rem 0.6rem;
    background: rgba(14, 165, 233, 0.06);
    border-left: 2px solid #0ea5e9;
    border-radius: 0 6px 6px 0;
  }

  .proj-name {
    color: #f0f6ff;
    font-weight: 600;
  }

  .proj-desc {
    color: #64748b;
  }

  .card-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .tag {
    padding: 0.25rem 0.75rem;
    background: rgba(14, 165, 233, 0.1);
    border: 1px solid rgba(14, 165, 233, 0.25);
    border-radius: 99px;
    font-size: 0.75rem;
    color: #38bdf8;
    font-weight: 500;
  }

  @media (max-width: 768px) {
    .timeline-line {
      left: 22px;
    }

    .timeline-item,
    .timeline-item.right {
      padding: 0;
      padding-left: 4rem;
      flex-direction: row;
    }

    .timeline-dot {
      left: 0;
      transform: none;
      width: 36px;
      height: 36px;
      font-size: 0.85rem;
    }

    .timeline-card {
      max-width: 100%;
    }
  }
</style>
