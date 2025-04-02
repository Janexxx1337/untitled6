<template>
  <section class="hero-section" ref="sectionRef" id="hero">
    <div class="hero-bg">
      <div class="blur-shape shape-1"></div>
      <div class="blur-shape shape-2"></div>
      <div class="blur-shape shape-3"></div>
    </div>

    <div class="hero-content">
      <h1 class="hero-title">
        <div class="hero-title-line">
          <code-lock-text
              ref="decryptText1Ref"
              :text="'СОЗДАЁМ'"
              :start-delay="200"
          />
        </div>
        <div class="hero-title-line">
          <code-lock-text
              ref="decryptText2Ref"
              :text="'ЦИФРОВЫЕ'"
              :start-delay="500"
          />
        </div>
        <div class="hero-title-line">
          <code-lock-text
              ref="decryptText3Ref"
              :text="'ВПЕЧАТЛЕНИЯ'"
              :start-delay="800"
              :accent-index="6"
          />
        </div>
      </h1>

      <div class="hero-subtitle">
        <code-lock-text
            ref="decryptSubtitleRef"
            :text="'Мы — креативная студия, создающая запоминающиеся цифровые решения для брендов, которые хотят выделяться'"
            :start-delay="1100"
            :duration="1500"
            size="small"
        />
      </div>
    </div>

    <div
        class="scroll-indicator"
        @mouseenter="$emit('cursor-event', 'md')"
        @mouseleave="$emit('cursor-event', 'leave')"
        @click="$emit('section-scroll', 'about')"
    >
      <div class="indicator-text">Скролл</div>
      <div class="indicator-line"></div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, defineEmits, defineExpose, defineProps } from 'vue';
import CodeLockText from './CodeLockText.vue';

const props = defineProps({
  isLoaded: Boolean
});

const emit = defineEmits(['cursor-event', 'section-scroll']);

const sectionRef = ref(null);
const decryptText1Ref = ref(null);
const decryptText2Ref = ref(null);
const decryptText3Ref = ref(null);
const decryptSubtitleRef = ref(null);

const initTextDecryptAnimation = () => {
  // Запускаем анимацию для всех текстов
  decryptText1Ref.value?.startAnimation();
  decryptText2Ref.value?.startAnimation();
  decryptText3Ref.value?.startAnimation();
  decryptSubtitleRef.value?.startAnimation();
};

defineExpose({
  initTextDecryptAnimation,
  sectionRef
});
</script>

<style scoped>
.hero-title-line {
  overflow: visible;
  margin-bottom: 10px;
}
</style>