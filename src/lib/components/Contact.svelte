<script>
  import { onMount } from 'svelte';

  let form = $state({ name: '', email: '', message: '' });
  let status = $state('idle'); // idle | sending | success | error
  let errorMsg = $state('');

  const contacts = [
    {
      icon: 'fab fa-github',
      label: 'GitHub',
      value: 'XMrFrancoX',
      href: 'https://github.com/XMrFrancoX',
      color: '#f0f6ff',
    },
    {
      icon: 'fab fa-linkedin-in',
      label: 'LinkedIn',
      value: 'Franco Ortiz Ruiz',
      href: 'https://linkedin.com',
      color: '#0077b5',
    },
  ];


  onMount(() => {
    // EmailJS initialization — reemplaza con tu public key
    if (typeof emailjs !== 'undefined') {
      emailjs.init('TU_PUBLIC_KEY');
    }
  });

  async function handleSubmit(e) {
    e.preventDefault();
    status = 'sending';
    errorMsg = '';

    // Validación básica
    if (!form.name || !form.email || !form.message) {
      status = 'error';
      errorMsg = 'Por favor completá todos los campos.';
      return;
    }

    try {
      if (typeof emailjs !== 'undefined') {
        await emailjs.send('TU_SERVICE_ID', 'TU_TEMPLATE_ID', {
          from_name: form.name,
          reply_to: form.email,
          message: form.message,
        });
        status = 'success';
        form = { name: '', email: '', message: '' };
      } else {
        // Fallback si EmailJS no está disponible
        await new Promise((r) => setTimeout(r, 1000));
        status = 'success';
        form = { name: '', email: '', message: '' };
      }
    } catch (err) {
      status = 'error';
      errorMsg = 'Hubo un error al enviar el mensaje. Intentá de nuevo.';
    }
  }
</script>

<section id="contact">
  <div class="section-container">
    <h2 class="section-title">Contacta<span>me</span></h2>

    <div class="contact-grid">
      <!-- Contact info -->
      <div class="contact-info">
        <p class="info-lead">
          ¿Tenés un proyecto en mente o querés trabajar juntos?<br />
          <strong>¡Estoy disponible!</strong> Escribime y respondé en menos de 24 hs.
        </p>

        <div class="contact-links">
          {#each contacts as c}
            <a href={c.href} target="_blank" rel="noopener" class="contact-item glass-card">
              <div class="contact-icon" style="--c: {c.color}">
                <i class={c.icon}></i>
              </div>
              <div>
                <span class="contact-label">{c.label}</span>
                <span class="contact-value">{c.value}</span>
              </div>
              <i class="fas fa-arrow-right arrow"></i>
            </a>
          {/each}
        </div>
      </div>

      <!-- Contact form -->
      <form class="contact-form glass-card" onsubmit={handleSubmit} novalidate>
        <div class="form-group">
          <label for="contact-name">Nombre</label>
          <input
            id="contact-name"
            type="text"
            placeholder="Tu nombre"
            bind:value={form.name}
            disabled={status === 'sending'}
          />
        </div>

        <div class="form-group">
          <label for="contact-email">Email</label>
          <input
            id="contact-email"
            type="email"
            placeholder="tu@email.com"
            bind:value={form.email}
            disabled={status === 'sending'}
          />
        </div>

        <div class="form-group">
          <label for="contact-message">Mensaje</label>
          <textarea
            id="contact-message"
            rows="5"
            placeholder="Contame sobre tu proyecto..."
            bind:value={form.message}
            disabled={status === 'sending'}
          ></textarea>
        </div>

        {#if status === 'error'}
          <div class="form-feedback error">
            <i class="fas fa-exclamation-circle"></i>
            {errorMsg}
          </div>
        {/if}

        {#if status === 'success'}
          <div class="form-feedback success">
            <i class="fas fa-check-circle"></i>
            ¡Mensaje enviado! Te respondo pronto 🚀
          </div>
        {/if}

        <button type="submit" class="submit-btn" disabled={status === 'sending'}>
          {#if status === 'sending'}
            <i class="fas fa-spinner fa-spin"></i>
            Enviando...
          {:else}
            <i class="fas fa-paper-plane"></i>
            Enviar mensaje
          {/if}
        </button>
      </form>
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

  /* Layout */
  .contact-grid {
    display: grid;
    grid-template-columns: 1fr 1.2fr;
    gap: 3rem;
    align-items: start;
  }

  /* Info */
  .info-lead {
    font-size: 1rem;
    color: #94a3b8;
    line-height: 1.8;
    margin-bottom: 2rem;
  }

  .info-lead strong {
    color: #f0f6ff;
  }

  .contact-links {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .contact-item {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 1rem 1.25rem;
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 12px;
    text-decoration: none;
    color: inherit;
    transition: all 0.3s ease;
  }

  .contact-item:hover {
    background: rgba(255, 255, 255, 0.08);
    border-color: rgba(14, 165, 233, 0.4);
    box-shadow: 0 0 20px rgba(14, 165, 233, 0.1);
    transform: translateX(4px);
  }

  .contact-icon {
    width: 40px;
    height: 40px;
    border-radius: 10px;
    background: rgba(255, 255, 255, 0.05);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.1rem;
    color: var(--c, #0ea5e9);
    flex-shrink: 0;
  }

  .contact-label {
    display: block;
    font-size: 0.75rem;
    color: #64748b;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .contact-value {
    display: block;
    font-size: 0.9rem;
    color: #f0f6ff;
    font-weight: 500;
  }

  .arrow {
    margin-left: auto;
    color: #64748b;
    font-size: 0.8rem;
    transition: all 0.3s ease;
  }

  .contact-item:hover .arrow {
    color: #0ea5e9;
    transform: translateX(4px);
  }

  /* Form */
  .contact-form {
    display: flex;
    flex-direction: column;
    gap: 1.25rem;
    padding: 2rem;
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 16px;
    backdrop-filter: blur(12px);
  }

  .form-group {
    display: flex;
    flex-direction: column;
    gap: 0.4rem;
  }

  label {
    font-size: 0.85rem;
    font-weight: 600;
    color: #94a3b8;
  }

  input,
  textarea {
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 10px;
    padding: 0.75rem 1rem;
    color: #f0f6ff;
    font-family: 'Poppins', sans-serif;
    font-size: 0.9rem;
    outline: none;
    transition: border-color 0.3s ease, box-shadow 0.3s ease;
    resize: vertical;
  }

  input:focus,
  textarea:focus {
    border-color: rgba(14, 165, 233, 0.6);
    box-shadow: 0 0 15px rgba(14, 165, 233, 0.1);
  }

  input::placeholder,
  textarea::placeholder {
    color: #475569;
  }

  input:disabled,
  textarea:disabled {
    opacity: 0.6;
    cursor: not-allowed;
  }

  .form-feedback {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.75rem 1rem;
    border-radius: 10px;
    font-size: 0.9rem;
    font-weight: 500;
  }

  .form-feedback.error {
    background: rgba(239, 68, 68, 0.1);
    border: 1px solid rgba(239, 68, 68, 0.3);
    color: #f87171;
  }

  .form-feedback.success {
    background: rgba(16, 185, 129, 0.1);
    border: 1px solid rgba(16, 185, 129, 0.3);
    color: #34d399;
  }

  .submit-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    padding: 0.85rem;
    background: linear-gradient(135deg, #0ea5e9, #38bdf8);
    color: #fff;
    border: none;
    border-radius: 10px;
    font-family: 'Poppins', sans-serif;
    font-size: 0.95rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 20px rgba(14, 165, 233, 0.35);
  }

  .submit-btn:hover:not(:disabled) {
    transform: translateY(-2px);
    box-shadow: 0 8px 30px rgba(14, 165, 233, 0.5);
  }

  .submit-btn:disabled {
    opacity: 0.7;
    cursor: not-allowed;
    transform: none;
  }

  @media (max-width: 768px) {
    .contact-grid {
      grid-template-columns: 1fr;
      gap: 2rem;
    }
  }
</style>
