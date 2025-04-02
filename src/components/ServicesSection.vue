<template>
  <section class="services-section" ref="sectionRef" id="services">
    <div class="section-header">
      <div class="section-number">02</div>
      <h2 class="section-title">Услуги</h2>
    </div>

    <div class="services-grid">
      <div
          class="service-card"
          v-for="(service, idx) in services"
          :key="`service-${idx}`"
          @mouseenter="serviceHover(idx); $emit('cursor-event', 'lg')"
          @mouseleave="serviceLeave(); $emit('cursor-event', 'leave')"
      >
        <div class="service-number">0{{ idx + 1 }}</div>
        <h3 class="service-title">{{ service.title }}</h3>
        <div class="service-description">{{ service.description }}</div>
        <div class="service-link">
          <span class="link-text">Подробнее</span>
          <span class="link-arrow">→</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  services: Array
});

const emit = defineEmits(['cursor-event']);
const sectionRef = ref(null);
const activeService = ref(null);

const serviceHover = (idx) => {
  activeService.value = idx;
};

const serviceLeave = () => {
  activeService.value = null;
};

defineExpose({
  sectionRef
});
</script>
