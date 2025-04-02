<template>
  <section class="contact-section" ref="sectionRef" id="contact">
    <div class="section-header">
      <div class="section-number">04</div>
      <h2 class="section-title">Контакты</h2>
    </div>

    <div class="contact-content">
      <div class="contact-info">
        <div class="contact-text">
          <p class="text-xl">Давайте работать вместе.</p>
          <p class="text-regular">Напишите нам, чтобы обсудить ваш проект или просто поздороваться.</p>
        </div>

        <div class="contact-details">
          <div class="contact-item">
            <div class="contact-label">Email</div>
            <a
                href="mailto:hello@nova.ru"
                class="contact-value"
                @mouseenter="$emit('cursor-event', 'lg')"
                @mouseleave="$emit('cursor-event', 'leave')"
            >
              hello@nova.ru
            </a>
          </div>

          <div class="contact-item">
            <div class="contact-label">Телефон</div>
            <a
                href="tel:+74951234567"
                class="contact-value"
                @mouseenter="$emit('cursor-event', 'lg')"
                @mouseleave="$emit('cursor-event', 'leave')"
            >
              +7 495 123-45-67
            </a>
          </div>

          <div class="contact-item">
            <div class="contact-label">Адрес</div>
            <div class="contact-value">Москва, ул. Цифровая, 42</div>
          </div>
        </div>
      </div>

      <div class="contact-form-wrapper">
        <form class="contact-form" @submit.prevent="submitForm">
          <div class="form-group">
            <label class="form-label">Имя</label>
            <input
                type="text"
                class="form-input"
                v-model="formData.name"
                @focus="$emit('cursor-event', 'input')"
                @blur="$emit('cursor-event', 'leave')"
            >
          </div>

          <div class="form-group">
            <label class="form-label">Email</label>
            <input
                type="email"
                class="form-input"
                v-model="formData.email"
                @focus="$emit('cursor-event', 'input')"
                @blur="$emit('cursor-event', 'leave')"
            >
          </div>

          <div class="form-group">
            <label class="form-label">Проект</label>
            <textarea
                class="form-textarea"
                rows="4"
                v-model="formData.project"
                @focus="$emit('cursor-event', 'input')"
                @blur="$emit('cursor-event', 'leave')"
            ></textarea>
          </div>

          <button
              type="submit"
              class="btn-submit"
              @mouseenter="$emit('cursor-event', 'lg')"
              @mouseleave="$emit('cursor-event', 'leave')"
          >
            <span>Отправить</span>
            <span class="btn-arrow">→</span>
          </button>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['cursor-event']);
const sectionRef = ref(null);

const formData = ref({
  name: '',
  email: '',
  project: ''
});

const submitForm = () => {
  // Здесь будет логика отправки формы
  console.log('Форма отправлена:', formData.value);

  // Сброс формы после отправки
  formData.value = {
    name: '',
    email: '',
    project: ''
  };
};

defineExpose({
  sectionRef
});
</script>

