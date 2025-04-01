<template>
  <div class="wrapper">
    <header class="header">
      <div class="logo">AESTHETICS</div>
      <nav class="nav">
        <a href="#" class="nav-link">Work</a>
        <a href="#" class="nav-link">About</a>
        <a href="#" class="nav-link">Contact</a>
      </nav>
    </header>

    <main>
      <section class="hero">
        <h1 class="title">
          <span class="title-line">Crafting</span>
          <span class="title-line">Digital</span>
          <span class="title-line">Experiences</span>
        </h1>
        <div class="scroll-indicator">
          <span>Scroll</span>
          <div class="scroll-line"></div>
        </div>
      </section>

      <section class="projects">
        <h2 class="section-title">Selected Work</h2>
        <div class="project-grid">
          <div class="project" v-for="(project, index) in projects" :key="index"
               @mouseover="activeProject = index"
               @mouseleave="activeProject = null">
            <div class="project-number">{{ index + 1 < 10 ? '0' + (index + 1) : index + 1 }}</div>
            <div class="project-info">
              <h3 class="project-title">{{ project.title }}</h3>
              <div class="project-meta">{{ project.category }}</div>
            </div>
            <div class="project-image" :class="{ 'active': activeProject === index }">
              <div class="image-placeholder"></div>
            </div>
          </div>
        </div>
      </section>

      <section class="manifesto">
        <div class="manifesto-content">
          <h2 class="section-title">Our Approach</h2>
          <div class="manifesto-text">
            <p>We combine <span class="highlight">DRY</span>, <span class="highlight">KISS</span>, <span class="highlight">SOLID</span>, and <span class="highlight">YAGNI</span> principles to create digital experiences that are both beautiful and functional.</p>
            <p>Every pixel has purpose. Every interaction has meaning.</p>
          </div>
        </div>
      </section>
    </main>

    <footer class="footer">
      <div class="footer-content">
        <div class="footer-logo">AESTHETICS</div>
        <div class="footer-links">
          <div class="footer-column">
            <h4>Connect</h4>
            <a href="#">Instagram</a>
            <a href="#">Twitter</a>
            <a href="#">LinkedIn</a>
          </div>
          <div class="footer-column">
            <h4>Contact</h4>
            <a href="mailto:hello@aesthetics.design">hello@aesthetics.design</a>
            <a href="tel:+1234567890">+1 234 567 890</a>
          </div>
        </div>
      </div>
      <div class="copyright">
        © {{ new Date().getFullYear() }} Aesthetics Studio. All rights reserved.
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      activeProject: null,
      projects: [
        { title: 'Harmony', category: 'Interactive Experience' },
        { title: 'Monochrome', category: 'E-Commerce' },
        { title: 'Perspective', category: 'Digital Art' },
        { title: 'Synthesis', category: 'Brand Identity' }
      ]
    }
  },
  mounted() {
    this.initAnimations();
  },
  methods: {
    initAnimations() {
      // Here you would initialize animations
      // For example with GSAP or other animation libraries
      this.animateHeroText();
    },
    animateHeroText() {
      // Animation logic would go here
      // This is where you'd implement smooth reveal animations
    }
  }
}
</script>

<style>
/* Base Styles */
:root {
  --bg-color: #000;
  --text-color: #fff;
  --accent-color: #f7f7f7;
  --spacing-unit: 8px;
  --transition-time: 0.5s;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: var(--bg-color);
  color: var(--text-color);
  font-family: 'Space Grotesk', sans-serif;
  font-size: 16px;
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* Typography */
h1, h2, h3, h4 {
  font-weight: 400;
  letter-spacing: -0.02em;
}

/* Header */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: calc(var(--spacing-unit) * 4);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 100;
  mix-blend-mode: difference;
}

.logo {
  font-size: 1.5rem;
  letter-spacing: 0.1em;
  font-weight: 700;
}

.nav {
  display: flex;
  gap: calc(var(--spacing-unit) * 4);
}

.nav-link {
  color: var(--text-color);
  text-decoration: none;
  position: relative;
  padding-bottom: var(--spacing-unit);
  transition: all var(--transition-time) ease;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 1px;
  background-color: var(--text-color);
  transition: width var(--transition-time) ease;
}

.nav-link:hover::after {
  width: 100%;
}

/* Hero Section */
.hero {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 0 calc(var(--spacing-unit) * 6);
  position: relative;
}

.title {
  font-size: 8vw;
  line-height: 0.9;
  margin-bottom: calc(var(--spacing-unit) * 8);
}

.title-line {
  display: block;
}

.scroll-indicator {
  position: absolute;
  bottom: calc(var(--spacing-unit) * 6);
  left: calc(var(--spacing-unit) * 6);
  display: flex;
  align-items: center;
  gap: calc(var(--spacing-unit) * 2);
  font-size: 0.875rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.scroll-line {
  width: calc(var(--spacing-unit) * 8);
  height: 1px;
  background-color: var(--text-color);
  animation: scrollPulse 2s infinite;
}

@keyframes scrollPulse {
  0% { transform: scaleX(1); opacity: 1; }
  50% { transform: scaleX(1.5); opacity: 0.5; }
  100% { transform: scaleX(1); opacity: 1; }
}

/* Projects Section */
.projects {
  padding: calc(var(--spacing-unit) * 12) calc(var(--spacing-unit) * 6);
}

.section-title {
  font-size: 1.25rem;
  margin-bottom: calc(var(--spacing-unit) * 8);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  opacity: 0.7;
}

.project-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: calc(var(--spacing-unit) * 8);
}

.project {
  display: flex;
  flex-direction: column;
  position: relative;
  cursor: pointer;
}

.project-number {
  font-size: 12vw;
  font-weight: 700;
  opacity: 0.1;
  position: absolute;
  top: -0.2em;
  right: 0;
  z-index: -1;
}

.project-info {
  margin-bottom: calc(var(--spacing-unit) * 4);
}

.project-title {
  font-size: 2.5rem;
  margin-bottom: calc(var(--spacing-unit) * 2);
  transition: transform var(--transition-time) ease;
}

.project:hover .project-title {
  transform: translateX(calc(var(--spacing-unit) * 2));
}

.project-meta {
  font-size: 0.875rem;
  opacity: 0.7;
}

.project-image {
  width: 100%;
  aspect-ratio: 16/9;
  overflow: hidden;
  position: relative;
}

.image-placeholder {
  width: 100%;
  height: 100%;
  background-color: #1a1a1a;
  transform: scale(0.95);
  transition: transform var(--transition-time) ease;
}

.project-image.active .image-placeholder {
  transform: scale(1);
}

/* Manifesto Section */
.manifesto {
  padding: calc(var(--spacing-unit) * 12) calc(var(--spacing-unit) * 6);
  display: flex;
  justify-content: center;
}

.manifesto-content {
  max-width: 800px;
}

.manifesto-text {
  font-size: 2rem;
  line-height: 1.3;
}

.manifesto-text p {
  margin-bottom: calc(var(--spacing-unit) * 4);
}

.highlight {
  display: inline-block;
  position: relative;
  z-index: 1;
}

.highlight::after {
  content: '';
  position: absolute;
  bottom: 0.1em;
  left: -0.1em;
  right: -0.1em;
  height: 0.3em;
  background-color: rgba(255, 255, 255, 0.1);
  z-index: -1;
  transition: height var(--transition-time) ease;
}

.highlight:hover::after {
  height: 100%;
}

/* Footer */
.footer {
  margin-top: auto;
  padding: calc(var(--spacing-unit) * 12) calc(var(--spacing-unit) * 6) calc(var(--spacing-unit) * 6);
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.footer-content {
  display: flex;
  justify-content: space-between;
  margin-bottom: calc(var(--spacing-unit) * 8);
}

.footer-logo {
  font-size: 1.5rem;
  letter-spacing: 0.1em;
  font-weight: 700;
}

.footer-links {
  display: flex;
  gap: calc(var(--spacing-unit) * 12);
}

.footer-column h4 {
  margin-bottom: calc(var(--spacing-unit) * 3);
  font-size: 0.875rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  opacity: 0.7;
}

.footer-column a {
  display: block;
  color: var(--text-color);
  text-decoration: none;
  margin-bottom: calc(var(--spacing-unit) * 2);
  transition: opacity var(--transition-time) ease;
}

.footer-column a:hover {
  opacity: 0.7;
}

.copyright {
  font-size: 0.875rem;
  opacity: 0.5;
  text-align: center;
  padding-top: calc(var(--spacing-unit) * 6);
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

/* Responsive */
@media (min-width: 768px) {
  .project-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .title {
    font-size: 6vw;
  }

  .manifesto-text {
    font-size: 3vw;
  }
}

/* Additional animations would be added with JavaScript */
</style>