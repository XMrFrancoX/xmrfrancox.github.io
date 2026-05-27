<script>
  import Navbar from '$lib/components/Navbar.svelte';
  import Hero from '$lib/components/Hero.svelte';
  import Skills from '$lib/components/Skills.svelte';
  import Experience from '$lib/components/Experience.svelte';
  import Projects from '$lib/components/Projects.svelte';
  import Contact from '$lib/components/Contact.svelte';
  import Footer from '$lib/components/Footer.svelte';
  import { onMount } from 'svelte';

  onMount(() => {
    // Scroll reveal global via IntersectionObserver
    const reveals = document.querySelectorAll('.reveal');
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add('visible');
            observer.unobserve(entry.target);
          }
        });
      },
      { threshold: 0.15 }
    );
    reveals.forEach((el) => observer.observe(el));
    return () => observer.disconnect();
  });
</script>

<svelte:head>
  <title>Franco Ortiz Ruiz — Portfolio</title>
  <meta name="description" content="Portfolio de Franco Ortiz Ruiz, Desarrollador Full Stack con experiencia en JavaScript, Python y Desarrollo Web." />
</svelte:head>

<Navbar />

<main>
  <Hero />
  <Skills />
  <Experience />
  <Projects />
  <Contact />
</main>

<Footer />

<style>
  main {
    position: relative;
    z-index: 1;
  }
</style>
