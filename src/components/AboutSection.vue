<template>
  <section class="about-section" ref="sectionRef" id="about">
    <div class="section-header">
      <div class="section-number">01</div>
      <h2 class="section-title">О студии</h2>
    </div>

    <div class="about-content">
      <div class="about-text">
        <p class="text-xl">Мы объединяем дизайн, технологии и стратегическое мышление, чтобы создавать продукты, которые оставляют впечатления.</p>

        <p class="text-regular">Наша студия специализируется на создании цифровых продуктов, которые не только выглядят стильно, но и приносят реальные результаты. Мы работаем на стыке дизайна и технологий, постоянно исследуя новые подходы и возможности.</p>
      </div>

      <div class="about-stats">
        <div
            class="stat-item"
            v-for="(stat, idx) in stats"
            :key="`stat-${idx}`"
            @mouseenter="$emit('cursor-event', 'md')"
            @mouseleave="$emit('cursor-event', 'leave')"
        >
          <div class="stat-number">{{ stat.number }}</div>
          <div class="stat-label">{{ stat.label }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  stats: Array
});

const emit = defineEmits(['cursor-event']);
const sectionRef = ref(null);

defineExpose({
  sectionRef
});
</script>
