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
          <span class="decrypt-text" ref="decryptText1Ref">СОЗДАЁМ</span>
        </div>
        <div class="hero-title-line">
          <span class="decrypt-text" ref="decryptText2Ref">ЦИФРОВЫЕ</span>
        </div>
        <div class="hero-title-line">
          <span class="decrypt-text" ref="decryptText3Ref">ВПЕЧАТ<span class="accent-letter">Л</span>ЕНИЯ</span>
        </div>
      </h1>

      <div class="hero-subtitle">
        <span class="decrypt-text" ref="decryptSubtitleRef">
          Мы — креативная студия, создающая запоминающиеся цифровые решения для брендов, которые хотят выделяться
        </span>
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
import { ref, onMounted } from 'vue';

const props = defineProps({
  isLoaded: Boolean
});

const emit = defineEmits(['cursor-event', 'section-scroll']);

const sectionRef = ref(null);
const decryptText1Ref = ref(null);
const decryptText2Ref = ref(null);
const decryptText3Ref = ref(null);
const decryptSubtitleRef = ref(null);

// Символы для анимации дешифровки
const decryptChars = 'АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ!@#$%^&*()_+-={}[]|:;"<>,.?/\\';

const textDecryptAnimation = (element, finalText) => {
  if (!element) return;

  let duration = 3; // 3 секунды
  let interval = 60; // 60мс для более плавной анимации
  let steps = duration * 1000 / interval;
  let currentStep = 0;

  // Создаем случайный текст такой же длины
  const generateRandomText = () => {
    let result = '';
    for (let i = 0; i < finalText.length; i++) {
      result += decryptChars.charAt(Math.floor(Math.random() * decryptChars.length));
    }
    return result;
  };

  // Начинаем с случайного текста
  element.textContent = generateRandomText();

  // Функция одного шага анимации
  const updateText = () => {
    currentStep++;
    let result = '';

    for (let i = 0; i < finalText.length; i++) {
      // Более плавная вероятностная модель
      let progress = currentStep / steps;

      // Более плавное затухание для символов в конце строки
      let charProgress = progress - (i * 0.05);

      // Добавим немного случайности для "органичности"
      if (charProgress >= 0.75 || (charProgress >= 0.4 && Math.random() > 0.85)) {
        // Символ дешифрован
        result += finalText[i];
      } else {
        // Символ еще "шифрован" - иногда оставляем тот же символ для большей стабильности
        if (Math.random() > 0.3 && element.textContent[i]) {
          result += element.textContent[i];
        } else {
          result += decryptChars.charAt(Math.floor(Math.random() * decryptChars.length));
        }
      }
    }

    element.textContent = result;

    // Продолжаем анимацию, если не закончили
    if (currentStep < steps) {
      setTimeout(updateText, interval);
    } else {
      // Убеждаемся, что финальный текст точно соответствует нужному
      element.textContent = finalText;
    }
  };

  // Запускаем анимацию
  updateText();
};

const initTextDecryptAnimation = () => {
  // Анимация дешифровки для заголовков с задержкой
  setTimeout(() => {
    textDecryptAnimation(decryptText1Ref.value, 'СОЗДАЁМ');
  }, 200);

  setTimeout(() => {
    textDecryptAnimation(decryptText2Ref.value, 'ЦИФРОВЫЕ');
  }, 400);

  setTimeout(() => {
    textDecryptAnimation(decryptText3Ref.value, 'ВПЕЧАТЛЕНИЯ');
  }, 600);

  setTimeout(() => {
    textDecryptAnimation(decryptSubtitleRef.value, 'Мы — креативная студия, создающая запоминающиеся цифровые решения для брендов, которые хотят выделяться');
  }, 1000);
};

defineExpose({
  initTextDecryptAnimation,
  sectionRef
});
</script>
