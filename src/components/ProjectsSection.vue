<template>
  <section class="projects-section" ref="sectionRef" id="projects">
    <div class="section-header">
      <div class="section-number">03</div>
      <h2 class="section-title">Проекты</h2>
    </div>

    <div class="projects-showcase">
      <div
          class="project-item"
          v-for="(project, idx) in projects"
          :key="`project-${idx}`"
          :class="{ 'project-active': activeProject === idx }"
          @mouseenter="setActiveProject(idx); $emit('cursor-event', 'view')"
          @mouseleave="clearActiveProject(); $emit('cursor-event', 'leave')"
      >
        <div class="project-image-container">
          <div class="project-image" :class="`project-${idx + 1}`"></div>
          <div class="project-overlay"></div>
        </div>
        <div class="project-content">
          <div class="project-meta">
            <div class="project-number">0{{ idx + 1 }}</div>
            <div class="project-category">{{ project.category }}</div>
          </div>
          <h3 class="project-title">{{ project.title }}</h3>
          <div class="project-description">{{ project.description }}</div>
          <div class="project-link">
            <span class="link-text">Смотреть проект</span>
            <span class="link-arrow">→</span>
          </div>
        </div>
      </div>
    </div>

    <div class="projects-cta">
      <a
          href="#"
          class="btn-outline"
          @mouseenter="$emit('cursor-event', 'lg')"
          @mouseleave="$emit('cursor-event', 'leave')"
      >
        <span>Все проекты</span>
        <span class="btn-arrow">→</span>
      </a>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';
import { gsap } from 'gsap';

const props = defineProps({
  projects: Array
});

const emit = defineEmits(['cursor-event']);
const sectionRef = ref(null);
const activeProject = ref(null);

const setActiveProject = (idx) => {
  activeProject.value = idx;

  // Добавляем анимацию при наведении
  const projectItems = document.querySelectorAll('.project-item');

  projectItems.forEach((item, i) => {
    if (i === idx) {
      gsap.to(item, {
        y: -20,
        scale: 1.02,
        duration: 0.4,
        ease: 'power2.out'
      });

      gsap.to(item.querySelector('.project-title'), {
        y: -10,
        duration: 0.3,
        ease: 'power2.out'
      });

      gsap.to(item.querySelector('.project-link'), {
        opacity: 1,
        y: -5,
        duration: 0.3,
        ease: 'power2.out'
      });

      gsap.to(item.querySelector('.link-arrow'), {
        x: 8,
        duration: 0.3,
        ease: 'power2.out'
      });
    } else {
      gsap.to(item, {
        opacity: 0.5,
        scale: 0.98,
        duration: 0.4,
        ease: 'power2.out'
      });
    }
  });
};

const clearActiveProject = () => {
  activeProject.value = null;

  // Возвращаем все проекты в исходное состояние
  const projectItems = document.querySelectorAll('.project-item');

  projectItems.forEach((item) => {
    gsap.to(item, {
      y: 0,
      scale: 1,
      opacity: 1,
      duration: 0.4,
      ease: 'power2.out'
    });

    gsap.to(item.querySelector('.project-title'), {
      y: 0,
      duration: 0.3,
      ease: 'power2.out'
    });

    gsap.to(item.querySelector('.project-link'), {
      opacity: 0.8,
      y: 0,
      duration: 0.3,
      ease: 'power2.out'
    });

    gsap.to(item.querySelector('.link-arrow'), {
      x: 0,
      duration: 0.3,
      ease: 'power2.out'
    });
  });
};

defineExpose({
  sectionRef
});
</script>
