<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const navLinks = [
  { label: 'Наши решения', href: '#solutions' },
  { label: 'Экспертиза и технологии', href: '#expertise' },
  { label: 'Контакты', href: '#footer' },
]

const isScrolled = ref(false)

function onScroll() {
  isScrolled.value = window.scrollY > 10
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

      <!-- Навигация -->
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

    </div>
  </header>
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

  height: var(--header-height);

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
  display: flex;             /* логотип слева, навигация справа */
  align-items: center;
  justify-content: space-between;

  max-width: var(--container-max);
  height: 100%;
  margin: 0 auto;
  padding: 0 var(--container-padding);
}

/* --- Логотип --- */
.header__logo {
  display: inline-flex;
  transition: opacity var(--transition-fast);
}

.header__logo:hover {
  opacity: 0.8;
}

.header__logo-img {
  width: 285px;
  height: 61px;
  object-fit: contain;
}

/* --- Навигация --- */
.header__nav-list {
  display: flex;             /* три ссылки в ряд */
  align-items: center;
  gap: var(--spacing-xl);   /* ↓ Настрой расстояние между ссылками */
  padding-right: 260px;
}

.header__nav-link {
  font-family: 'Inter';
  font-style: normal;
  font-weight: 400;
  font-size: 25px;
  line-height: 47px;
  text-align: center;
  color: #000000;
  transition: color var(--transition-fast);
  white-space: nowrap;
}

.header__nav-link:hover {
  color: var(--color-primary);
}
</style>
