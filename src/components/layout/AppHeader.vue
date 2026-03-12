<script setup>
/* Якорные ссылки навигации */
const navLinks = [
  { label: 'Наши решения', href: '#solutions' },
  { label: 'Экспертиза и технологии', href: '#expertise' },
  { label: 'Контакты', href: '#footer' },
]
</script>

<template>
  <header class="header">
    <div class="header__container">

      <!-- Логотип — замени содержимое на SVG или img из Figma -->
      <a href="/" class="header__logo" aria-label="На главную">
        <span class="header__logo-icon" aria-hidden="true">
          <!-- ↓ Сюда вставь SVG-логотип из Figma -->
          <svg width="32" height="32" viewBox="0 0 32 32" fill="none">
            <rect width="32" height="32" rx="8" fill="currentColor" fill-opacity="0.15"/>
            <text x="50%" y="55%" dominant-baseline="middle" text-anchor="middle"
                  font-size="14" font-weight="700" fill="currentColor">ФТ</text>
          </svg>
        </span>
        <span class="header__logo-text">Ф Тех</span>
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

  /* ↓ Задай цвет фона шапки, тень и border-bottom по дизайну */
  background-color: var(--bg-header);
  backdrop-filter: blur(8px); /* матовый эффект стекла */
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
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);

  /* ↓ Настрой цвет логотипа */
  color: var(--color-primary);
  transition: opacity var(--transition-fast);
}

.header__logo:hover {
  opacity: 0.8;
}

.header__logo-icon {
  flex-shrink: 0;
}

.header__logo-text {
  /* ↓ Задай font-size, font-weight, letter-spacing по дизайну */
  font-weight: var(--font-weight-bold);
  font-size: var(--font-size-lg);
  color: var(--color-text-primary);
}

/* --- Навигация --- */
.header__nav-list {
  display: flex;             /* три ссылки в ряд */
  align-items: center;
  gap: var(--spacing-xl);   /* ↓ Настрой расстояние между ссылками */
}

.header__nav-link {
  /* ↓ Задай font-size, цвет и hover-эффект по дизайну */
  font-size: var(--font-size-base);
  font-weight: var(--font-weight-medium);
  color: var(--color-text-secondary);
  transition: color var(--transition-fast);
  white-space: nowrap;
}

.header__nav-link:hover {
  color: var(--color-primary);
}
</style>
