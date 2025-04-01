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
        <!-- Героическая секция -->
        <section class="hero-section" ref="heroSectionRef" id="hero">
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
              <span class="decrypt-text" ref="decryptSubtitleRef">Мы — креативная студия, создающая запоминающиеся цифровые решения для брендов, которые хотят выделяться</span>
            </div>
          </div>

          <div class="scroll-indicator" @mouseenter="cursorEnter('md')" @mouseleave="cursorLeave()" @click="scrollToSection('about')">
            <div class="indicator-text">Скролл</div>
            <div class="indicator-line"></div>
          </div>
        </section>

        <!-- Секция о нас -->
        <section class="about-section" ref="aboutSectionRef" id="about">
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
              <div class="stat-item" v-for="(stat, idx) in stats" :key="`stat-${idx}`">
                <div class="stat-number">{{ stat.number }}</div>
                <div class="stat-label">{{ stat.label }}</div>
              </div>
            </div>
          </div>
        </section>

        <!-- Секция услуг -->
        <section class="services-section" ref="servicesSectionRef" id="services">
          <div class="section-header">
            <div class="section-number">02</div>
            <h2 class="section-title">Услуги</h2>
          </div>

          <div class="services-grid">
            <div
                class="service-card"
                v-for="(service, idx) in services"
                :key="`service-${idx}`"
                @mouseenter="cursorEnter('lg'); hoverService(idx)"
                @mouseleave="cursorLeave(); leaveService()"
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

        <!-- Секция проектов -->
        <section class="projects-section" ref="projectsSectionRef" id="projects">
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
                @mouseenter="cursorEnter('view'); setActiveProject(idx)"
                @mouseleave="cursorLeave(); clearActiveProject()"
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
            <a href="#" class="btn-outline" @mouseenter="cursorEnter('lg')" @mouseleave="cursorLeave()">
              <span>Все проекты</span>
              <span class="btn-arrow">→</span>
            </a>
          </div>
        </section>

        <!-- Секция контактов -->
        <section class="contact-section" ref="contactSectionRef" id="contact">
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
                  <a href="mailto:hello@nova.ru" class="contact-value" @mouseenter="cursorEnter('lg')" @mouseleave="cursorLeave()">hello@nova.ru</a>
                </div>

                <div class="contact-item">
                  <div class="contact-label">Телефон</div>
                  <a href="tel:+74951234567" class="contact-value" @mouseenter="cursorEnter('lg')" @mouseleave="cursorLeave()">+7 495 123-45-67</a>
                </div>

                <div class="contact-item">
                  <div class="contact-label">Адрес</div>
                  <div class="contact-value">Москва, ул. Цифровая, 42</div>
                </div>
              </div>
            </div>

            <div class="contact-form-wrapper">
              <form class="contact-form">
                <div class="form-group">
                  <label class="form-label">Имя</label>
                  <input type="text" class="form-input" @focus="cursorEnter('input')" @blur="cursorLeave()">
                </div>

                <div class="form-group">
                  <label class="form-label">Email</label>
                  <input type="email" class="form-input" @focus="cursorEnter('input')" @blur="cursorLeave()">
                </div>

                <div class="form-group">
                  <label class="form-label">Проект</label>
                  <textarea class="form-textarea" rows="4" @focus="cursorEnter('input')" @blur="cursorLeave()"></textarea>
                </div>

                <button type="submit" class="btn-submit" @mouseenter="cursorEnter('lg')" @mouseleave="cursorLeave()">
                  <span>Отправить</span>
                  <span class="btn-arrow">→</span>
                </button>
              </form>
            </div>
          </div>
        </section>
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
const decryptText1Ref = ref(null);
const decryptText2Ref = ref(null);
const decryptText3Ref = ref(null);
const decryptSubtitleRef = ref(null);

// Данные для компонента
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
const initPreloader = () => {
  // Анимация прелоадера
  gsap.to(preloaderProgressRef.value, {
    width: '100%',
    duration: 2,
    ease: 'power2.inOut',
    onComplete: () => {
      isLoaded.value = true;
      initHeroAnimation();
    }
  });
};

const initHeroAnimation = () => {
  // Анимация дешифровки для заголовков
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

const textDecryptAnimation = (element, finalText) => {
  if (!element) return;

  let duration = 2.5; // Увеличенная продолжительность анимации (было 1.5)
  let interval = 45; // Увеличенный интервал обновления символов (было 30)
  let steps = duration * 1000 / interval; // количество шагов анимации
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
      // Вероятность того, что символ "дешифрован" на этом шаге
      let progress = currentStep / steps;

      // Чем дальше в тексте, тем позже дешифруем
      let charProgress = progress - (i * 0.08); // Увеличено замедление для символов в конце

      if (charProgress >= Math.random() || charProgress > 0.9) {
        // Символ дешифрован
        result += finalText[i];
      } else {
        // Символ еще "шифрован"
        result += decryptChars.charAt(Math.floor(Math.random() * decryptChars.length));
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
    { ref: heroSectionRef.value, id: 'hero' },
    { ref: aboutSectionRef.value, id: 'about' },
    { ref: servicesSectionRef.value, id: 'services' },
    { ref: projectsSectionRef.value, id: 'projects' },
    { ref: contactSectionRef.value, id: 'contact' }
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

const initScrollAnimations = () => {
  // Анимация секции о нас
  if (aboutSectionRef.value) {
    ScrollTrigger.create({
      trigger: aboutSectionRef.value,
      start: "top 80%",
      onEnter: () => {
        gsap.from(aboutSectionRef.value.querySelector('.section-title'), {
          y: 50,
          opacity: 0,
          duration: 0.8
        });

        gsap.from(aboutSectionRef.value.querySelectorAll('.about-text p'), {
          y: 30,
          opacity: 0,
          stagger: 0.2,
          duration: 0.6
        });

        gsap.from(aboutSectionRef.value.querySelectorAll('.stat-item'), {
          y: 20,
          opacity: 0,
          stagger: 0.1,
          duration: 0.5
        });
      }
    });
  }

  // Анимация секции услуг
  if (servicesSectionRef.value) {
    ScrollTrigger.create({
      trigger: servicesSectionRef.value,
      start: "top 80%",
      onEnter: () => {
        gsap.from(servicesSectionRef.value.querySelector('.section-title'), {
          y: 50,
          opacity: 0,
          duration: 0.8
        });

        gsap.from(servicesSectionRef.value.querySelectorAll('.service-card'), {
          y: 50,
          opacity: 0,
          stagger: 0.15,
          duration: 0.8
        });
      }
    });
  }

  // Анимация секции проектов
  if (projectsSectionRef.value) {
    ScrollTrigger.create({
      trigger: projectsSectionRef.value,
      start: "top 80%",
      onEnter: () => {
        gsap.from(projectsSectionRef.value.querySelector('.section-title'), {
          y: 50,
          opacity: 0,
          duration: 0.8
        });

        gsap.from(projectsSectionRef.value.querySelectorAll('.project-item'), {
          y: 100,
          opacity: 0,
          stagger: 0.2,
          duration: 1
        });
      }
    });
  }

  // Анимация секции контактов
  if (contactSectionRef.value) {
    ScrollTrigger.create({
      trigger: contactSectionRef.value,
      start: "top 80%",
      onEnter: () => {
        gsap.from(contactSectionRef.value.querySelector('.section-title'), {
          y: 50,
          opacity: 0,
          duration: 0.8
        });

        gsap.from(contactSectionRef.value.querySelector('.contact-text'), {
          y: 30,
          opacity: 0,
          duration: 0.6
        });

        gsap.from(contactSectionRef.value.querySelectorAll('.contact-item'), {
          y: 20,
          opacity: 0,
          stagger: 0.15,
          duration: 0.5
        });

        gsap.from(contactSectionRef.value.querySelector('.contact-form'), {
          y: 50,
          opacity: 0,
          duration: 0.8,
          delay: 0.2
        });
      }
    });
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

const hoverService = (idx) => {
  activeService.value = idx;
};

const leaveService = () => {
  activeService.value = null;
};

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

<style>
@import url('https://fonts.googleapis.com/css2?family=Manrope:wght@300;400;500;600;700;800&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@700;800;900&display=swap');

/* Основные стили */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body {
  overflow-x: hidden;
  background-color: #0A0A0A;
  color: #FFFFFF;
  font-family: 'Manrope', sans-serif;
  font-size: 16px;
  line-height: 1.5;
  height: 100%;
  scroll-behavior: smooth;
}

/* Прелоадер */
.preloader {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #0A0A0A;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.preloader-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.preloader-logo {
  font-size: 5rem;
  font-weight: 800;
  letter-spacing: -2px;
  font-family: 'Space Grotesk', sans-serif;
}

.preloader-bar {
  width: 200px;
  height: 2px;
  background-color: rgba(255, 255, 255, 0.1);
  position: relative;
}

.preloader-progress {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 0;
  background-color: #FFFFFF;
}

/* Основной контейнер */
.landing-wrapper {
  position: relative;
  min-height: 100vh;
}

.main-container {
  opacity: 0;
  transition: opacity 0.8s ease;
}

.main-container.loaded {
  opacity: 1;
}

/* Кастомный курсор */
.custom-cursor {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9999;
  pointer-events: none;
  mix-blend-mode: difference;
}

.cursor-dot {
  position: absolute;
  width: 8px;
  height: 8px;
  background-color: #FFFFFF;
  border-radius: 50%;
  transform: translate(-50%, -50%);
}

.cursor-circle {
  position: absolute;
  width: 40px;
  height: 40px;
  border: 1px solid #FFFFFF;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  transition: all 0.3s ease;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #FFFFFF;
  font-size: 0.7rem;
  font-weight: 500;
  text-transform: uppercase;
}

/* Шапка сайта */
.site-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  padding: 2rem 3rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 100;
  transition: all 0.3s ease;
  mix-blend-mode: difference;
}

.header-scrolled {
  padding: 1.5rem 3rem;
}

.header-logo {
  font-size: 1.8rem;
  font-weight: 800;
  letter-spacing: -1px;
  font-family: 'Space Grotesk', sans-serif;
  cursor: pointer;
}

.header-nav {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}

.header-nav ul {
  display: flex;
  gap: 2rem;
  list-style: none;
}

.header-nav a {
  font-size: 0.9rem;
  font-weight: 500;
  color: #FFFFFF;
  text-decoration: none;
  opacity: 0.8;
  transition: opacity 0.3s ease;
  position: relative;
}

.header-nav a:hover {
  opacity: 1;
}

.header-nav a::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 1px;
  background-color: #FFFFFF;
  transition: width 0.3s ease;
}

.header-nav a:hover::after, .header-nav a.active::after {
  width: 100%;
}

.header-nav a.active {
  opacity: 1;
}

.header-menu-toggle {
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
}

/* Полноэкранное меню */
.fullscreen-menu {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 99;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.5s ease, visibility 0.5s ease;
}

.fullscreen-menu.active {
  opacity: 1;
  visibility: visible;
}

.menu-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #FFFFFF;
  opacity: 0;
}

.menu-content {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 6rem 3rem 3rem;
  color: #0A0A0A;
}

.menu-links {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.menu-link {
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
  padding: 1rem 0;
  border-bottom: 1px solid rgba(10, 10, 10, 0.1);
}

.menu-link-text {
  font-size: 3.5rem;
  font-weight: 800;
  letter-spacing: -2px;
  font-family: 'Space Grotesk', sans-serif;
  line-height: 1;
}

.menu-link-text em {
  font-style: normal;
  color: #555555;
}

.menu-link-number {
  font-size: 1rem;
  font-weight: 500;
  opacity: 0.5;
}

.menu-footer {
  display: flex;
  justify-content: space-between;
  margin-top: 3rem;
}

.contact-title, .social-title {
  font-size: 0.9rem;
  font-weight: 600;
  margin-bottom: 1rem;
  opacity: 0.5;
}

.contact-link {
  display: block;
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.5rem;
  color: #0A0A0A;
  text-decoration: none;
}

.social-links {
  display: flex;
  gap: 1.5rem;
}

.social-link {
  font-size: 1rem;
  color: #0A0A0A;
  text-decoration: none;
}

/* Героическая секция */
.hero-section {
  min-height: 100vh;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 0 3rem;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

.blur-shape {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.2;
}

.shape-1 {
  width: 500px;
  height: 500px;
  background: linear-gradient(45deg, #4A00E0, #8E2DE2);
  top: 20%;
  left: -5%;
}

.shape-2 {
  width: 400px;
  height: 400px;
  background: linear-gradient(45deg, #8E2DE2, #4A00E0);
  bottom: 10%;
  right: -5%;
}

.shape-3 {
  width: 300px;
  height: 300px;
  background: linear-gradient(45deg, #2DE28E, #00E0A5);
  top: 60%;
  left: 20%;
}

.hero-content {
  text-align: center;
  max-width: 1200px;
}

.hero-title {
  font-size: 7vw;
  line-height: 0.9;
  font-weight: 800;
  letter-spacing: -3px;
  margin-bottom: 3rem;
  font-family: 'Space Grotesk', sans-serif;
  text-transform: uppercase;
}

.hero-title-line {
  overflow: hidden;
  position: relative;
}

.accent-letter {
  color: #4A00E0;
}

.hero-subtitle {
  font-size: 1.2rem;
  font-weight: 300;
  max-width: 600px;
  margin: 0 auto;
  opacity: 0.8;
}

.decrypt-text {
  display: inline-block;
  font-family: inherit;
  text-transform: inherit;
}

.scroll-indicator {
  position: absolute;
  bottom: 3rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  opacity: 0.6;
  cursor: pointer;
}

.indicator-text {
  font-size: 0.9rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.indicator-line {
  width: 1px;
  height: 60px;
  background: linear-gradient(to bottom, #FFFFFF, transparent);
  animation: scrollPulse 2s infinite;
}

@keyframes scrollPulse {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(10px);
  }
}

/* Стили для всех секций */
section {
  padding: 8rem 3rem;
  position: relative;
}

.section-header {
  margin-bottom: 4rem;
  position: relative;
}

.section-number {
  font-size: 1rem;
  font-weight: 500;
  opacity: 0.5;
  margin-bottom: 0.5rem;
}

.section-title {
  font-size: 3.5rem;
  font-weight: 800;
  letter-spacing: -2px;
  font-family: 'Space Grotesk', sans-serif;
}

/* Секция о нас */
.about-content {
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  gap: 4rem;
}

.text-xl {
  font-size: 2rem;
  font-weight: 500;
  line-height: 1.3;
  margin-bottom: 2rem;
}

.text-regular {
  font-size: 1.1rem;
  opacity: 0.8;
}

.about-stats {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 2rem;
}

.stat-item {
  text-align: center;
}

.stat-number {
  font-size: 3.5rem;
  font-weight: 700;
  line-height: 1;
  background: linear-gradient(45deg, #FFFFFF, #A0A0A0);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.stat-label {
  font-size: 1rem;
  opacity: 0.7;
  margin-top: 0.5rem;
}

/* Секция услуг */
.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.service-card {
  background-color: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 1rem;
  padding: 2rem;
  transition: all 0.3s ease;
  cursor: pointer;
}

.service-card:hover {
  background-color: rgba(255, 255, 255, 0.05);
  transform: translateY(-10px);
  border-color: rgba(255, 255, 255, 0.1);
}

.service-number {
  font-size: 0.9rem;
  opacity: 0.5;
  margin-bottom: 1rem;
}

.service-title {
  font-size: 1.8rem;
  font-weight: 700;
  margin-bottom: 1rem;
  font-family: 'Space Grotesk', sans-serif;
}

.service-description {
  font-size: 1rem;
  opacity: 0.8;
  margin-bottom: 2rem;
}

.service-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.link-text {
  font-size: 1rem;
  font-weight: 500;
}

.link-arrow {
  font-size: 1.2rem;
  transition: transform 0.3s ease;
}

.service-card:hover .link-arrow {
  transform: translateX(5px);
}

/* Секция проектов */
.projects-showcase {
  display: flex;
  flex-direction: column;
  gap: 3rem;
}

.project-item {
  display: flex;
  flex-direction: column;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  border-radius: 1rem;
  height: 450px;
  transition: all 0.5s ease;
  transform-origin: center;
}

.project-item:not(:first-child) {
  margin-top: -100px;
}

.project-active, .project-item:hover {
  margin-top: 0;
  margin-bottom: 0;
  transform: translateY(0) scale(1.02);
  z-index: 2;
}

.project-image-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.project-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.7s ease;
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.9), rgba(0, 0, 0, 0.5) 50%, rgba(0, 0, 0, 0.2));
  z-index: 1;
}

.project-item:hover .project-image, .project-active .project-image {
  transform: scale(1.05);
}

.project-1 {
  background: linear-gradient(45deg, #121212, #2a2a2a);
}

.project-2 {
  background: linear-gradient(45deg, #1c1c1c, #3a3a3a);
}

.project-3 {
  background: linear-gradient(45deg, #252525, #444444);
}

.project-content {
  position: relative;
  z-index: 2;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  height: 100%;
}

.project-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.project-number {
  font-size: 0.9rem;
  opacity: 0.7;
}

.project-category {
  font-size: 0.9rem;
  opacity: 0.7;
}

.project-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  font-family: 'Space Grotesk', sans-serif;
  transition: transform 0.4s ease, color 0.3s ease;
}

.project-description {
  font-size: 1rem;
  opacity: 0.8;
  max-width: 90%;
  margin-bottom: 1.5rem;
  transition: opacity 0.4s ease;
}

.project-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  opacity: 0.8;
  transition: all 0.4s ease;
}

.project-item:hover .project-title, .project-active .project-title {
  transform: translateY(-5px);
  color: #FFFFFF;
}

.project-item:hover .project-description, .project-active .project-description {
  opacity: 1;
}

.project-item:hover .project-link, .project-active .project-link {
  opacity: 1;
}

.project-item:hover .link-arrow, .project-active .link-arrow {
  transform: translateX(5px);
}

.projects-cta {
  display: flex;
  justify-content: center;
  margin-top: 3rem;
}

.btn-outline {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 1rem;
  font-weight: 500;
  padding: 1rem 2rem;
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 3rem;
  background: transparent;
  color: #FFFFFF;
  text-decoration: none;
  transition: all 0.3s ease;
}

.btn-outline:hover {
  background-color: rgba(255, 255, 255, 0.05);
  border-color: rgba(255, 255, 255, 0.3);
}

.btn-outline:hover .btn-arrow {
  transform: translateX(5px);
}

.btn-arrow {
  transition: transform 0.3s ease;
}

/* Секция контактов */
.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
}

.contact-details {
  margin-top: 3rem;
}

.contact-item {
  margin-bottom: 2rem;
}

.contact-label {
  font-size: 0.9rem;
  opacity: 0.6;
  margin-bottom: 0.5rem;
}

.contact-value {
  font-size: 1.4rem;
  font-weight: 500;
  color: #FFFFFF;
  text-decoration: none;
}

.contact-form-wrapper {
  background-color: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 1rem;
  padding: 3rem;
}

.form-group {
  margin-bottom: 2rem;
}

.form-label {
  display: block;
  font-size: 0.9rem;
  opacity: 0.6;
  margin-bottom: 0.5rem;
}

.form-input, .form-textarea {
  width: 100%;
  padding: 1rem;
  background-color: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 0.5rem;
  color: #FFFFFF;
  font-family: 'Manrope', sans-serif;
  font-size: 1rem;
}

.form-input:focus, .form-textarea:focus {
  outline: none;
  border-color: rgba(255, 255, 255, 0.3);
}

.btn-submit {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 1rem;
  font-weight: 500;
  padding: 1rem 2rem;
  border: none;
  border-radius: 3rem;
  background: linear-gradient(45deg, #4A00E0, #8E2DE2);
  color: #FFFFFF;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-submit:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(74, 0, 224, 0.3);
}

.btn-submit:hover .btn-arrow {
  transform: translateX(5px);
}

/* Футер */
.site-footer {
  padding: 5rem 3rem 2rem;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.footer-main {
  display: flex;
  justify-content: space-between;
  margin-bottom: 4rem;
}

.footer-logo {
  font-size: 2rem;
  font-weight: 800;
  letter-spacing: -1px;
  font-family: 'Space Grotesk', sans-serif;
  cursor: pointer;
}

.footer-links {
  display: flex;
  gap: 4rem;
}

.group-title {
  font-size: 0.9rem;
  font-weight: 600;
  opacity: 0.5;
  margin-bottom: 1.5rem;
}

.group-links {
  list-style: none;
}

.group-links li {
  margin-bottom: 0.8rem;
}

.group-links a {
  color: #FFFFFF;
  text-decoration: none;
  opacity: 0.7;
  transition: opacity 0.3s ease;
}

.group-links a:hover {
  opacity: 1;
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 2rem;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.copyright {
  font-size: 0.9rem;
  opacity: 0.5;
}

.back-to-top {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #FFFFFF;
  text-decoration: none;
  opacity: 0.7;
  transition: all 0.3s ease;
}

.back-to-top:hover {
  opacity: 1;
}

.arrow-up {
  transition: transform 0.3s ease;
}

.back-to-top:hover .arrow-up {
  transform: translateY(-5px);
}

/* Медиа запросы */
@media (max-width: 1200px) {
  .hero-title {
    font-size: 5rem;
  }

  .menu-link-text {
    font-size: 3rem;
  }

  .about-content {
    grid-template-columns: 1fr;
    gap: 3rem;
  }

  .contact-content {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}

@media (max-width: 768px) {
  .site-header {
    padding: 1.5rem;
  }

  .header-nav {
    display: none;
  }

  section {
    padding: 5rem 1.5rem;
  }

  .hero-title {
    font-size: 3.5rem;
    letter-spacing: -2px;
  }

  .hero-subtitle {
    font-size: 1rem;
  }

  .section-title {
    font-size: 2.5rem;
  }

  .text-xl {
    font-size: 1.5rem;
  }

  .menu-link-text {
    font-size: 2rem;
  }

  .menu-footer {
    flex-direction: column;
    gap: 2rem;
  }

  .about-stats {
    grid-template-columns: 1fr;
  }

  .footer-main {
    flex-direction: column;
    gap: 3rem;
  }

  .footer-links {
    flex-direction: column;
    gap: 2rem;
  }

  .contact-form-wrapper {
    padding: 1.5rem;
  }

  .project-item:not(:first-child) {
    margin-top: 0;
  }
}


::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #0A0A0A;
}

::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.2);
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: rgba(255, 255, 255, 0.3);
}

/* Дополнительные анимации */
@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

@keyframes pulse {
  0%, 100% {
    opacity: 0.5;
  }
  50% {
    opacity: 1;
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Эффект для проектов при загрузке страницы */
.projects-showcase {
  perspective: 1000px;
}

/* 3D Эффект при наведении на кнопки */
.btn-submit, .btn-outline {
  transition: transform 0.3s ease, box-shadow 0.3s ease, background-color 0.3s ease;
}

.btn-submit:hover, .btn-outline:hover {
  transform: translateY(-5px) scale(1.01);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
}

/* Улучшенный эффект для активного проекта */
.project-active {
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
}

/* Эффект наведения для всей карточки проекта */
.project-item {
  backface-visibility: hidden;
  will-change: transform;
}

.project-image {
  will-change: transform;
  transform: scale(1);
  transition: transform 0.7s cubic-bezier(0.215, 0.61, 0.355, 1);
}

.project-item:hover .project-image {
  transform: scale(1.05);
}

/* Эффект для оверлея проекта */
.project-overlay {
  background: linear-gradient(
      to top,
      rgba(0, 0, 0, 0.95) 0%,
      rgba(0, 0, 0, 0.7) 50%,
      rgba(0, 0, 0, 0.2) 100%
  );
  opacity: 0.8;
  transition: opacity 0.5s ease;
}

.project-item:hover .project-overlay {
  opacity: 1;
}

/* Плавная анимация для текста проекта */
.project-content {
  transform: translateY(0);
  transition: transform 0.4s cubic-bezier(0.215, 0.61, 0.355, 1);
}

.project-item:hover .project-content {
  transform: translateY(-10px);
}

/* Стили активного состояния для меню */
.header-nav a.active {
  opacity: 1;
}

.header-nav a.active::after {
  width: 100%;
}

/* Анимированный фон для формы при фокусе */
.form-input:focus, .form-textarea:focus {
  background-color: rgba(255, 255, 255, 0.05);
  box-shadow: 0 0 0 1px rgba(255, 255, 255, 0.3), 0 5px 15px rgba(0, 0, 0, 0.1);
}

/* Подсветка для поля формы при фокусе */
.form-group {
  position: relative;
}

.form-group::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(45deg, #4A00E0, #8E2DE2);
  transition: width 0.3s ease;
}

.form-group:focus-within::after {
  width: 100%;
}

/* Более плавный эффект для blur-shape */
.blur-shape {
  transition: transform 0.8s ease;
}

.blur-shape.shape-1 {
  animation: float 15s ease-in-out infinite;
}

.blur-shape.shape-2 {
  animation: float 20s ease-in-out infinite reverse;
}

.blur-shape.shape-3 {
  animation: float 18s ease-in-out infinite;
  animation-delay: 2s;
}
</style>