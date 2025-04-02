// src/App.vue
<template>
  <div class="landing-wrapper">
    <!-- Кастомный курсор -->
    <div class="custom-cursor" ref="cursorRef">
      <div class="cursor-dot"></div>
      <div class="cursor-circle"></div>
    </div>

    <!-- Прелоадер -->
    <div class="preloader" v-if="!isLoaded">
      <div class="preloader-content">
        <div class="preloader-logo">N</div>
        <div class="preloader-bar">
          <div class="preloader-progress" ref="preloaderProgressRef"></div>
        </div>
      </div>
    </div>

    <!-- Основной контейнер -->
    <div class="main-container" :class="{ loaded: isLoaded }">
      <!-- Шапка сайта -->
      <header class="site-header" :class="{ 'header-scrolled': isScrolled }">
        <div class="header-logo" @mouseenter="cursorEnter('lg')" @mouseleave="cursorLeave()" @click="scrollToTop">
          <span>NOVA</span>
        </div>
        <nav class="header-nav">
          <ul>
            <li v-for="(item, idx) in menuItems" :key="`nav-${idx}`">
              <a
              href="#"
              @click.prevent="scrollToSection(item.section)"
              @mouseenter="cursorEnter('md')"
              @mouseleave="cursorLeave()"
              :class="{ active: activeSection === item.section }"
              >
              {{ item.simple }}
              </a>
            </li>
          </ul>
        </nav>
        <div class="header-menu-toggle" @click="toggleMenu" @mouseenter="cursorEnter('md')" @mouseleave="cursorLeave()">
          <span>{{ menuOpen ? 'Закрыть' : 'Меню' }}</span>
        </div>
      </header>

      <!-- Полноэкранное меню -->
      <div class="fullscreen-menu" :class="{ active: menuOpen }">
        <div class="menu-bg"></div>
        <div class="menu-content">
          <div class="menu-links">
            <div
                v-for="(item, idx) in menuItems"
                :key="`menu-${idx}`"
                class="menu-link"
                @mouseenter="cursorEnter('xl')"
                @mouseleave="cursorLeave()"
                @click="scrollToSection(item.section); toggleMenu()"
            >
              <span class="menu-link-text" v-html="item.text"></span>
              <span class="menu-link-number">0{{ idx + 1 }}</span>
            </div>
          </div>
          <div class="menu-footer">
            <div class="menu-contact">
              <div class="contact-title">Связаться</div>
              <a href="mailto:hello@nova.ru" class="contact-link" @mouseenter="cursorEnter('lg')" @mouseleave="cursorLeave()">hello@nova.ru</a>
              <a href="tel:+74951234567" class="contact-link" @mouseenter="cursorEnter('lg')" @mouseleave="cursorLeave()">+7 495 123-45-67</a>
            </div>
            <div class="menu-social">
              <div class="social-title">Социальные сети</div>
              <div class="social-links">
                <a href="#" class="social-link" @mouseenter="cursorEnter('md')" @mouseleave="cursorLeave()">Instagram</a>
                <a href="#" class="social-link" @mouseenter="cursorEnter('md')" @mouseleave="cursorLeave()">Behance</a>
                <a href="#" class="social-link" @mouseenter="cursorEnter('md')" @mouseleave="cursorLeave()">Dribbble</a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Основное содержимое -->
      <main>
        <!-- Секции сайта -->
        <HeroSection
            ref="heroSectionRef"
            :isLoaded="isLoaded"
            @cursor-event="handleCursorEvent"
            @section-scroll="scrollToSection"
        />

        <AboutSection
            ref="aboutSectionRef"
            :stats="stats"
            @cursor-event="handleCursorEvent"
        />

        <ServicesSection
            ref="servicesSectionRef"
            :services="services"
            @cursor-event="handleCursorEvent"
        />

        <ProjectsSection
            ref="projectsSectionRef"
            :projects="projects"
            @cursor-event="handleCursorEvent"
        />

        <ContactSection
            ref="contactSectionRef"
            @cursor-event="handleCursorEvent"
        />
      </main>

      <!-- Футер -->
      <footer class="site-footer">
        <div class="footer-main">
          <div class="footer-logo" @mouseenter="cursorEnter('lg')" @mouseleave="cursorLeave()" @click="scrollToTop">NOVA</div>

          <div class="footer-links">
            <div class="footer-links-group">
              <div class="group-title">Навигация</div>
              <ul class="group-links">
                <li v-for="(item, idx) in menuItems" :key="`footer-${idx}`">
                  <a href="#" @click.prevent="scrollToSection(item.section)" @mouseenter="cursorEnter('md')" @mouseleave="cursorLeave()">{{ item.simple }}</a>
                </li>
              </ul>
            </div>

            <div class="footer-links-group">
              <div class="group-title">Социальные сети</div>
              <ul class="group-links">
                <li><a href="#" @mouseenter="cursorEnter('md')" @mouseleave="cursorLeave()">Instagram</a></li>
                <li><a href="#" @mouseenter="cursorEnter('md')" @mouseleave="cursorLeave()">Behance</a></li>
                <li><a href="#" @mouseenter="cursorEnter('md')" @mouseleave="cursorLeave()">Dribbble</a></li>
              </ul>
            </div>
          </div>
        </div>

        <div class="footer-bottom">
          <div class="copyright">© NOVA Studio 2025. Все права защищены.</div>
          <a href="#" class="back-to-top" @click.prevent="scrollToTop" @mouseenter="cursorEnter('md')" @mouseleave="cursorLeave()">
            <span>Наверх</span>
            <span class="arrow-up">↑</span>
          </a>
        </div>
      </footer>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';

// Импорт компонентов секций
import HeroSection from './components/Hero/HeroSection.vue';
import AboutSection from './components/AboutSection.vue';
import ServicesSection from './components/ServicesSection.vue';
import ProjectsSection from './components/ProjectsSection.vue';
import ContactSection from './components/ContactSection.vue';

// Регистрация плагинов GSAP
gsap.registerPlugin(ScrollTrigger);

// Реактивные переменные состояния
const isLoaded = ref(false);
const isScrolled = ref(false);
const menuOpen = ref(false);
const activeService = ref(null);
const activeProject = ref(null);
const activeSection = ref('hero');

// Refs для DOM-элементов
const cursorRef = ref(null);
const preloaderProgressRef = ref(null);
const heroSectionRef = ref(null);
const aboutSectionRef = ref(null);
const servicesSectionRef = ref(null);
const projectsSectionRef = ref(null);
const contactSectionRef = ref(null);

// Данные для компонентов
// Данные для компонентов (продолжение)
const menuItems = [
  { text: 'Главная', simple: 'Главная', section: 'hero' },
  { text: 'О <em>Студии</em>', simple: 'О студии', section: 'about' },
  { text: 'Услуги', simple: 'Услуги', section: 'services' },
  { text: 'Проекты', simple: 'Проекты', section: 'projects' },
  { text: 'Контакты', simple: 'Контакты', section: 'contact' }
];

const stats = [
  { number: '7+', label: 'лет опыта' },
  { number: '50+', label: 'проектов' },
  { number: '30+', label: 'клиентов' },
  { number: '12', label: 'наград' }
];

const services = [
  {
    title: 'Веб-дизайн',
    description: 'Создаем современные веб-сайты и приложения с фокусом на пользовательский опыт и конверсию.'
  },
  {
    title: 'Брендинг',
    description: 'Разрабатываем уникальные айдентики для компаний, которые хотят выделяться на рынке.'
  },
  {
    title: 'Разработка',
    description: 'Превращаем дизайн в функциональные цифровые продукты с использованием современных технологий.'
  },
  {
    title: 'Стратегия',
    description: 'Помогаем брендам определить правильное направление для достижения бизнес-целей.'
  }
];

const projects = [
  {
    title: 'ARTUM Gallery',
    category: 'Веб-дизайн, Разработка',
    description: 'Современный веб-сайт для галереи современного искусства с уникальной системой онлайн-выставок и интерактивными экспонатами.'
  },
  {
    title: 'MONO Fashion',
    category: 'Брендинг, Дизайн',
    description: 'Полный ребрендинг для модного бренда, включающий новый логотип, фирменный стиль, упаковку и дизайн флагманского магазина.'
  },
  {
    title: 'SPARK Platform',
    category: 'UX/UI, Разработка',
    description: 'Образовательная платформа с адаптивным интерфейсом, продвинутой аналитикой и системой персонализированного обучения.'
  }
];

// Символы для анимации дешифровки
const decryptChars = 'АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ!@#$%^&*()_+-={}[]|:;"<>,.?/\\';

// Методы
const handleCursorEvent = (type) => {
  if (type === 'leave') {
    cursorLeave();
  } else {
    cursorEnter(type);
  }
};

const initPreloader = () => {
  // Анимация прелоадера
  gsap.to(preloaderProgressRef.value, {
    width: '100%',
    duration: 2,
    ease: 'power2.inOut',
    onComplete: () => {
      isLoaded.value = true;
      setTimeout(() => {
        initHeroAnimation();
      }, 400);
    }
  });
};

const initHeroAnimation = () => {
  // Эта функция будет вызывать метод в компоненте HeroSection
  if (heroSectionRef.value && heroSectionRef.value.initTextDecryptAnimation) {
    heroSectionRef.value.initTextDecryptAnimation();
  }
};

const initCursor = () => {
  const cursor = cursorRef.value;
  const cursorDot = cursor.querySelector('.cursor-dot');
  const cursorCircle = cursor.querySelector('.cursor-circle');

  // Начальное состояние
  gsap.set(cursor, { xPercent: -50, yPercent: -50 });

  // Следование за мышью
  document.addEventListener('mousemove', (e) => {
    gsap.to(cursorDot, {
      x: e.clientX,
      y: e.clientY,
      duration: 0.1,
      ease: 'power1.out'
    });

    gsap.to(cursorCircle, {
      x: e.clientX,
      y: e.clientY,
      duration: 0.5,
      ease: 'power3.out'
    });
  });

  // Скрываем стандартный курсор
  document.body.style.cursor = 'none';
};

const cursorEnter = (type) => {
  const cursor = cursorRef.value;
  if (!cursor) return;

  // Разные стили для разных типов интерактивных элементов
  switch(type) {
    case 'lg':
      gsap.to(cursor.querySelector('.cursor-circle'), {
        scale: 2.5,
        opacity: 0.2,
        duration: 0.3
      });
      break;
    case 'md':
      gsap.to(cursor.querySelector('.cursor-circle'), {
        scale: 1.5,
        opacity: 0.3,
        duration: 0.3
      });
      break;
    case 'xl':
      gsap.to(cursor.querySelector('.cursor-circle'), {
        scale: 4,
        opacity: 0.1,
        duration: 0.3
      });
      break;
    case 'input':
      gsap.to(cursor.querySelector('.cursor-circle'), {
        scale: 0,
        opacity: 0,
        duration: 0.3
      });
      gsap.to(cursor.querySelector('.cursor-dot'), {
        scale: 0,
        opacity: 0,
        duration: 0.3
      });
      break;
    case 'view':
      gsap.to(cursor.querySelector('.cursor-circle'), {
        scale: 3,
        opacity: 0.2,
        duration: 0.3
      });
      cursor.querySelector('.cursor-circle').textContent = 'Смотреть';
      cursor.querySelector('.cursor-circle').style.display = 'flex';
      break;
  }
};

const cursorLeave = () => {
  const cursor = cursorRef.value;
  if (!cursor) return;

  gsap.to(cursor.querySelector('.cursor-circle'), {
    scale: 1,
    opacity: 1,
    duration: 0.3
  });

  gsap.to(cursor.querySelector('.cursor-dot'), {
    scale: 1,
    opacity: 1,
    duration: 0.3
  });

  cursor.querySelector('.cursor-circle').textContent = '';
};

const handleScroll = () => {
  const scrollY = window.scrollY;
  isScrolled.value = scrollY > 50;

  // Определение активной секции на основе скролла
  updateActiveSection();

  // Паралакс-эффект для размытых форм
  gsap.to('.blur-shape', {
    y: scrollY * 0.1,
    stagger: 0.05,
    ease: 'none'
  });
};

const updateActiveSection = () => {
  const sections = [
    { id: 'hero', ref: document.getElementById('hero') },
    { id: 'about', ref: document.getElementById('about') },
    { id: 'services', ref: document.getElementById('services') },
    { id: 'projects', ref: document.getElementById('projects') },
    { id: 'contact', ref: document.getElementById('contact') }
  ];

  // Находим активную секцию
  for (let i = sections.length - 1; i >= 0; i--) {
    const section = sections[i];
    if (!section.ref) continue;

    const rect = section.ref.getBoundingClientRect();
    if (rect.top <= 200) {
      activeSection.value = section.id;
      break;
    }
  }
};

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value;

  if (menuOpen.value) {
    // Блокируем скролл
    document.body.style.overflow = 'hidden';

    // Анимация открытия меню
    gsap.to('.menu-bg', {
      opacity: 1,
      duration: 0.5
    });

    gsap.from('.menu-link', {
      y: 50,
      opacity: 0,
      stagger: 0.1,
      duration: 0.6,
      delay: 0.2
    });

    gsap.from('.menu-footer', {
      y: 30,
      opacity: 0,
      duration: 0.6,
      delay: 0.5
    });
  } else {
    // Разблокируем скролл
    document.body.style.overflow = '';

    // Анимация закрытия меню
    gsap.to('.menu-bg', {
      opacity: 0,
      duration: 0.5
    });
  }
};

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
};

const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId);
  if (element) {
    const offset = 100; // Отступ от верха для учета фиксированной шапки
    const elementPosition = element.getBoundingClientRect().top;
    const offsetPosition = elementPosition + window.pageYOffset - offset;

    window.scrollTo({
      top: offsetPosition,
      behavior: 'smooth'
    });

    // Устанавливаем активную секцию
    activeSection.value = sectionId;

    // Если меню открыто, закрываем его
    if (menuOpen.value) {
      toggleMenu();
    }
  }
};

const initScrollAnimations = () => {
  // Инициализация анимаций при скролле для каждой секции
  // О нас
  if (aboutSectionRef.value) {
    ScrollTrigger.create({
      trigger: '#about',
      start: "top 80%",
      onEnter: () => {
        gsap.from('#about .section-title', {
          y: 50,
          opacity: 0,
          duration: 0.8
        });

        gsap.from('#about .about-text p', {
          y: 30,
          opacity: 0,
          stagger: 0.2,
          duration: 0.6
        });

        gsap.from('#about .stat-item', {
          y: 20,
          opacity: 0,
          stagger: 0.1,
          duration: 0.5
        });
      }
    });
  }

  // Услуги
  if (servicesSectionRef.value) {
    ScrollTrigger.create({
      trigger: '#services',
      start: "top 80%",
      onEnter: () => {
        gsap.from('#services .section-title', {
          y: 50,
          opacity: 0,
          duration: 0.8
        });

        // Modified animation for service cards
        gsap.from('#services .service-card', {
          y: 30,
          opacity: 0,
          duration: 0.8,
          stagger: 0.15, // Increased stagger time
          ease: 'power2.out',
          onComplete: () => {
            // Ensure all cards are fully visible after animation
            gsap.set('#services .service-card', { clearProps: "all" });
          }
        });
      }
    });
  }

  // Проекты
  if (projectsSectionRef.value) {
    ScrollTrigger.create({
      trigger: '#projects',
      start: "top 80%",
      onEnter: () => {
        gsap.from('#projects .section-title', {
          y: 50,
          opacity: 0,
          duration: 0.8
        });

        gsap.from('#projects .project-item', {
          y: 100,
          opacity: 0,
          stagger: 0.2,
          duration: 1
        });
      }
    });
  }

  // Контакты
  if (contactSectionRef.value) {
    ScrollTrigger.create({
      trigger: '#contact',
      start: "top 80%",
      onEnter: () => {
        gsap.from('#contact .section-title', {
          y: 50,
          opacity: 0,
          duration: 0.8
        });

        gsap.from('#contact .contact-text', {
          y: 30,
          opacity: 0,
          duration: 0.6
        });

        gsap.from('#contact .contact-item', {
          y: 20,
          opacity: 0,
          stagger: 0.15,
          duration: 0.5
        });

        gsap.from('#contact .contact-form-wrapper', {
          y: 50,
          opacity: 0,
          duration: 0.8,
          delay: 0.2
        });
      }
    });
  }
};

// Хуки жизненного цикла
onMounted(() => {
  // Имитация загрузки
  initPreloader();

  // Инициализация курсора
  initCursor();

  // Инициализация скролла
  window.addEventListener('scroll', handleScroll);

  // Инициализация анимаций при скролле
  initScrollAnimations();
});

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style lang="scss">
@import './assets/styles/main.scss';
</style>