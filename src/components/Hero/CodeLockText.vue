<template>
  <div class="code-lock-container" :class="{ 'small-text': size === 'small' }">
    <div
        v-for="(char, index) in characters"
        :key="index"
        class="char-drum-container"
        :style="{
        width: size === 'small' ? '0.55em' : '0.8em',
        fontSize: size === 'small' ? '1em' : 'inherit'
      }"
    >
      <div
          ref="drums"
          class="char-drum"
          :style="{ transform: `translateY(${char.position}px)` }"
      >
        <div
            v-for="(drumChar, drumIndex) in char.drumChars"
            :key="drumIndex"
            class="drum-char"
            :class="{ 'accent-char': char.isAccent }"
        >
          {{ drumChar }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted, defineProps, defineExpose } from 'vue';
import gsap from 'gsap';

const props = defineProps({
  text: {
    type: String,
    required: true
  },
  startDelay: {
    type: Number,
    default: 0
  },
  duration: {
    type: Number,
    default: 2500
  },
  size: {
    type: String,
    default: 'normal'
  },
  accentIndex: {
    type: Number,
    default: -1
  }
});

const allChars = 'АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ!@#$%^&*()_+-={}[]|:;"<>,.?/\\абвгдеёжзийклмнопрстуфхцчшщъыьэюя0123456789 —';
const drums = ref([]);

// Создаем реактивный массив для барабанов
const characters = reactive([]);

onMounted(() => {
  // Инициализация барабанов для каждого символа
  for (let i = 0; i < props.text.length; i++) {
    const targetChar = props.text[i];

    // Создаем массив символов для барабана
    const drumChars = [];

    // Добавляем 15-25 случайных символов
    const randomCount = 15 + Math.floor(Math.random() * 10);
    for (let j = 0; j < randomCount; j++) {
      drumChars.push(allChars[Math.floor(Math.random() * allChars.length)]);
    }

    // Добавляем целевой символ в конец
    drumChars.push(targetChar);

    // Добавляем информацию о барабане
    characters.push({
      targetChar,
      drumChars,
      position: 0, // начальная позиция
      isAccent: i === props.accentIndex // является ли символ акцентным
    });
  }
});

// Функция для запуска анимации
const startAnimation = () => {
  // Для каждого барабана с символами
  characters.forEach((char, index) => {
    // Рассчитываем задержку в зависимости от позиции символа
    const delay = props.startDelay + index * 50;

    // Рассчитываем позицию конечного символа (который нужно показать)
    const finalPosition = -(char.drumChars.length - 1) * 100; // высота символа в процентах

    // Создаем промежуточную позицию для более реалистичной анимации
    const intermediatePosition = finalPosition * 0.6;

    // Используем GSAP для плавной анимации
    gsap.timeline({ delay: delay / 1000 })
        // Быстро прокручиваем барабан вниз
        .to(char, {
          position: intermediatePosition,
          duration: props.duration / 1000 * 0.6,
          ease: "power2.inOut"
        })
        // Затем медленнее прокручиваем до финальной позиции
        .to(char, {
          position: finalPosition,
          duration: props.duration / 1000 * 0.4,
          ease: "power3.out"
        });
  });
};

defineExpose({
  startAnimation
});
</script>

<style scoped>
.code-lock-container {
  display: inline-flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: flex-start;
  overflow: visible;
}

.small-text {
  font-size: 1rem;
  line-height: 1.4;
}

.char-drum-container {
  display: inline-block;
  height: 1em;
  overflow: hidden;
  position: relative;
}

.char-drum {
  position: absolute;
  left: 0;
  transition: transform 0.05s linear;
  will-change: transform;
}

.drum-char {
  height: 1em;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Space Grotesk', sans-serif;
}

.accent-char {
  color: #4A00E0;
}
</style>