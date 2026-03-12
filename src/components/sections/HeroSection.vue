<script setup>
/* HeroSection — первый экран */
</script>

<template>
  <section class="hero" id="hero">
    <div class="hero__container">

      <div class="hero__content">
        <h1 class="hero__title">
          Ф Тех — Технологический партнёр для банков и финтехов
        </h1>
        <p class="hero__description">
          Создаём автоматизированные системы под задачи клиента: от аналитики до промышленной эксплуатации
        </p>
        <a href="#solutions" class="hero__btn">
          Ознакомиться с проектом
        </a>
      </div>

      <!-- Декоративная зона справа — сюда вставь изображение или анимацию из Figma -->
      <div class="hero__visual" aria-hidden="true">
        <!-- ↓ Замени на <img src="..." alt="..."> или Vue-компонент с анимацией -->
        <div class="hero__visual-placeholder"></div>
      </div>

    </div>
  </section>
</template>

<style scoped>
/* ==========================================================================
   HERO SECTION — первый экран
   ========================================================================== */

.hero {
  /* Занимает минимум первую треть экрана (33.3vh) — при необходимости
     замени на min-height: 100vh если нужен полноэкранный вариант */
  min-height: calc(100vh / 3 * 2); /* ~67vh, чтобы заголовок хорошо читался */
  padding-top: var(--header-height); /* отступ из-за fixed шапки */

  display: flex;
  align-items: center;

  /* ↓ Задай background: цвет, градиент или изображение по дизайну */
  background-color: var(--bg-section-alt);
}

/* --- Внутренний контейнер --- */
.hero__container {
  display: flex;             /* контент слева, визуал справа */
  align-items: center;
  gap: var(--spacing-3xl);

  max-width: var(--container-max);
  width: 100%;
  margin: 0 auto;
  padding: var(--spacing-3xl) var(--container-padding);
}

/* --- Текстовый блок --- */
.hero__content {
  flex: 1;                   /* занимает доступное пространство */
  max-width: 600px;

  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);    /* ↓ Настрой расстояние между заголовком, описанием и кнопкой */
}

.hero__title {
  /* ↓ Задай font-size, font-weight, line-height и цвет по дизайну */
  font-size: var(--font-size-4xl);
  font-weight: var(--font-weight-bold);
  line-height: var(--line-height-tight);
  color: var(--color-text-primary);
}

.hero__description {
  /* ↓ Задай font-size, цвет и max-width по дизайну */
  font-size: var(--font-size-md);
  color: var(--color-text-secondary);
  line-height: var(--line-height-relaxed);
}

/* --- Кнопка CTA --- */
.hero__btn {
  display: inline-block;
  align-self: flex-start;    /* не растягивать на всю ширину */

  padding: var(--spacing-md) var(--spacing-xl);
  border-radius: var(--radius-md);

  /* ↓ Задай цвет фона, цвет текста и hover-эффект по дизайну */
  background-color: var(--color-primary);
  color: var(--color-white);
  font-weight: var(--font-weight-semibold);
  font-size: var(--font-size-base);

  transition: background-color var(--transition-fast), transform var(--transition-fast);
}

.hero__btn:hover {
  background-color: var(--color-primary-dark);
  transform: translateY(-1px);
}

/* --- Декоративная зона --- */
.hero__visual {
  flex: 0 0 40%;             /* фиксированная ширина визуала */
  max-width: 480px;
}

.hero__visual-placeholder {
  /* ↓ Задай размеры и стили заглушки или удали после добавления реального изображения */
  width: 100%;
  aspect-ratio: 4 / 3;
  border-radius: var(--radius-xl);
  background-color: var(--color-gray-200);

  /* ↓ Если нужен border или box-shadow — добавь здесь */
}

/* --- Адаптив --- */
@media (max-width: 768px) {
  .hero__container {
    flex-direction: column;
  }

  .hero__title {
    font-size: var(--font-size-2xl);
  }

  .hero__visual {
    flex: none;
    width: 100%;
    max-width: 100%;
  }
}
</style>
