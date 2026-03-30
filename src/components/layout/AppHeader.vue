<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const navLinks = [
  { label: 'Наши решения', href: '#solutions' },
  { label: 'Экспертиза и технологии', href: '#expertise' },
  { label: 'Контакты', href: '#footer' },
]

const isScrolled = ref(false)
const isMenuOpen = ref(false)

function onScroll() {
  isScrolled.value = window.scrollY > 10
}

function closeMenu() {
  isMenuOpen.value = false
}

onMounted(() => window.addEventListener('scroll', onScroll))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>

<template>
  <header class="header" :class="{ 'header--scrolled': isScrolled }">
    <div class="header__container">

      <a href="/" class="header__logo" aria-label="На главную">
        <img src="/logo-footer.svg" alt="Ф Тех" class="header__logo-img" />
      </a>

      <!-- Навигация — десктоп -->
      <nav class="header__nav" aria-label="Основная навигация">
        <ul class="header__nav-list">
          <li
            v-for="link in navLinks"
            :key="link.href"
            class="header__nav-item"
          >
            <a :href="link.href" class="header__nav-link">{{ link.label }}</a>
          </li>
        </ul>
      </nav>

      <!-- Кнопка бургера -->
      <button
        class="header__burger"
        type="button"
        :aria-label="isMenuOpen ? 'Закрыть меню' : 'Открыть меню'"
        :aria-expanded="isMenuOpen"
        @click="isMenuOpen = !isMenuOpen"
      >
        <svg width="46" height="40" viewBox="0 0 46 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect width="46" height="4.44444" fill="#306AF2"/>
          <rect y="17.7778" width="46" height="4.44444" fill="#306AF2"/>
          <rect y="35.5555" width="46" height="4.44444" fill="#306AF2"/>
        </svg>
      </button>

    </div>
  </header>

  <!-- Затемнение фона -->
  <Transition name="overlay-fade">
    <div
      v-if="isMenuOpen"
      class="menu-overlay"
      @click="closeMenu"
    />
  </Transition>

  <!-- Карточка меню -->
  <Transition name="menu-drop">
    <div v-if="isMenuOpen" class="menu-card" role="dialog" aria-modal="true" aria-label="Меню навигации">

      <!-- Кнопка закрытия -->
      <button class="menu-card__close" type="button" aria-label="Закрыть меню" @click="closeMenu">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <line x1="2" y1="2" x2="22" y2="22" stroke="#306AF2" stroke-width="2.5" stroke-linecap="round"/>
          <line x1="22" y1="2" x2="2" y2="22" stroke="#306AF2" stroke-width="2.5" stroke-linecap="round"/>
        </svg>
      </button>

      <nav aria-label="Мобильная навигация">
        <ul class="menu-card__list">
          <li v-for="link in navLinks" :key="link.href" class="menu-card__item">
            <a :href="link.href" class="menu-card__link" @click="closeMenu">
              {{ link.label }}
            </a>
          </li>
        </ul>
      </nav>

    </div>
  </Transition>
</template>

<style scoped>
/* ==========================================================================
   HEADER — фиксированная шапка
   ========================================================================== */

.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  overflow: hidden;

  height: 150px;

  background: linear-gradient(180deg, rgba(154, 194, 255, 0.15) 0%, rgba(255, 255, 255, 0.15) 100%);
  backdrop-filter: blur(8px);
  box-shadow: none;
  transition: background var(--transition-base), box-shadow var(--transition-base);
}

.header--scrolled {
  background-color: var(--bg-header);
  box-shadow: var(--shadow-header);
}

/* --- Внутренний контейнер --- */
.header__container {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;

  max-width: var(--container-max);
  height: 100%;
  margin: 10px;
  padding: 0 var(--container-padding);
}

/* --- Логотип --- */
.header__logo {
  display: inline-flex;
  transition: opacity var(--transition-fast);
  margin-left: 100px;
}

.header__logo:hover {
  opacity: 0.8;
}

.header__logo-img {
  width: 285px;
  height: 61px;
  object-fit: contain;
}

/* --- Навигация десктоп --- */
.header__nav {
  position: absolute;
  left: 70%;
  transform: translateX(-50%);
}

.header__nav-list {
  display: flex;
  align-items: center;
  gap: var(--spacing-xl);
}

.header__nav-link {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 25px;
  line-height: 47px;
  text-align: center;
  color: #000000;
  transition: color var(--transition-fast);
  white-space: nowrap;
  text-decoration: none;
}

/* Эффекты при наведении для десктопных ссылок */
.header__nav-link:hover {
  color: #306AF2;
  text-decoration: underline;
  text-decoration-thickness: 2px;
  text-underline-offset: 4px;
}

/* --- Кнопка бургера (скрыта на десктопе) --- */
.header__burger {
  display: none;
  align-items: center;
  justify-content: center;
  background: none;
  border: none;
  padding: 4px;
  cursor: pointer;
  flex-shrink: 0;
  z-index: 101;
}

/* ==========================================================================
   DROPDOWN MENU CARD
   ========================================================================== */

/* Затемнение страницы */
.menu-overlay {
  position: fixed;
  inset: 0;
  z-index: 200;
  background: rgba(0, 0, 0, 0.25);
}

/* Карточка меню */
.menu-card {
  position: fixed;
  top: calc(var(--header-height) + 12px);
  left: 50%;
  transform: translateX(-50%);
  z-index: 201;

  width: min(400px, calc(100vw - 32px));
  padding: 28px 32px 36px;

  background: #ffffff;
  border-radius: 20px;
  box-shadow: 0 8px 40px rgba(0, 0, 0, 0.15);
}

/* Кнопка X — правый верхний угол */
.menu-card__close {
  position: absolute;
  top: 16px;
  right: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 32px;
  height: 32px;
  padding: 0;
  background: none;
  border: none;
  cursor: pointer;
  transition: opacity var(--transition-fast);
}

.menu-card__close:hover {
  opacity: 0.7;
}

/* Список ссылок */
.menu-card__list {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--spacing-lg);
  margin-top: 12px;
}

.menu-card__link {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 20px;
  line-height: 30px;
  color: #000000;
  text-align: center;
  transition: color var(--transition-fast);
  text-decoration: none;
}

.menu-card__link:hover {
  color: #306AF2;
  text-decoration: underline;
  text-decoration-thickness: 2px;
  text-underline-offset: 4px;
}

/* --- Анимации --- */
.overlay-fade-enter-active,
.overlay-fade-leave-active {
  transition: opacity var(--transition-base);
}
.overlay-fade-enter-from,
.overlay-fade-leave-to {
  opacity: 0;
}

.menu-drop-enter-active,
.menu-drop-leave-active {
  transition: opacity var(--transition-base), transform var(--transition-base);
}
.menu-drop-enter-from,
.menu-drop-leave-to {
  opacity: 0;
  transform: translateX(-50%) translateY(-8px);
}

/* --- Адаптив --- */
@media (max-width: 1600px) {
.header__logo {
  margin-left: 80px;
}
}

@media (max-width: 1440px) {
.header {
  height: 120px;
}

  .header__logo-img {
    width: 251px;
    height: 54px;
  }

    .header__nav-link {
  font-size: 19px;
  line-height: 36px;
  }
}

@media (max-width: 1200px) {
.header__logo {
  margin-left: 50px;
}
}

@media (max-width: 1024px) {
.header {
  height: 100px;
}

  .header__logo-img {
    width: 215px;
    height: 46px;
  }

  .header__logo {
  margin-left: 40px;
}

  .header__nav {
    display: none;
  }

  .header__burger {
    display: flex;
  }
}

@media (max-width: 793px) {
 .header {
  height: 90px;
}

  .header__logo-img {
    width: 167px;
    height: 36px;
  }

  .menu-card__link {
    font-size: 18px;
  }

    .header__logo {
  margin-left: 30px;
}
}

@media (max-width: 375px) {
  .header {
  height: 80px;
}

  .header__logo-img {
    width: 156px;
    height: 34px;
  }

  .menu-card__link {
    font-size: 16px;
  }

  .header__logo {
  margin-left: 15px;
}
}
</style>

