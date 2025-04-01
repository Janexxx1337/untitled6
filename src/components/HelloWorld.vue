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

  // Увеличим длительность и замедлим обновление
  let duration = 3; // Увеличено с 2.5 до 3 секунд
  let interval = 60; // Увеличено с 45 до 60мс для более плавной анимации
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
      let charProgress = progress - (i * 0.05); // Уменьшено с 0.08 до 0.05

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

  // Анимация секции услуг - ИСПРАВЛЕННАЯ ЧАСТЬ
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

        // Сначала установим все карточки в видимое состояние
        gsap.set(servicesSectionRef.value.querySelectorAll('.service-card'), {
          opacity: 1,
          y: 0
        });

        // Затем анимируем их появление (но без stagger, который вызывает проблему)
        gsap.from(servicesSectionRef.value.querySelectorAll('.service-card'), {
          y: 30,
          opacity: 0,
          duration: 0.5,
          ease: 'power2.out',
          onComplete: () => {
            // Убедимся, что все карточки видимы после анимации
            gsap.set(servicesSectionRef.value.querySelectorAll('.service-card'), {
              clearProps: 'opacity,transform'
            });
          }
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

    // ДОБАВЛЕНО: Если переходим к секции услуг, убедимся, что все карточки видны
    if (sectionId === 'services' && servicesSectionRef.value) {
      gsap.to(servicesSectionRef.value.querySelectorAll('.service-card'), {
        opacity: 1,
        y: 0,
        duration: 0.3,
        overwrite: true,
        ease: 'power2.out'
      });
    }
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

  // ДОБАВЛЕНО: Убедимся, что все карточки услуг будут видны
  setTimeout(() => {
    if (servicesSectionRef.value) {
      gsap.set(servicesSectionRef.value.querySelectorAll('.service-card'), {
        opacity: 1,
        y: 0,
        clearProps: 'transform'
      });
    }
  }, 1000);
});

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style>
@import 'style.css';
</style>