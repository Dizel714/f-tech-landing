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
                   <strong>Создаём автоматизированные системы под задачи клиента:</strong> от аналитики до промышленной эксплуатации
        </p>
        <a href="#solutions" class="hero__btn">
          Ознакомиться с проектом
                    <span class="hero__btn-circle">
            <svg width="15" height="18" viewBox="0 0 15 18" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M2 2L12.5 9L2 16" stroke="#FFFFFF" stroke-width="3.85" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </span>
        </a>
      </div>

            <div class="hero__visual">
        <img src="/hero-visual.png" alt="Декоративный элемент" class="hero__visual-img" />
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
  align-items: flex-end;

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
  flex: 1;
  max-width: 600px;

  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  gap: var(--spacing-lg);
}

.hero__title {
  font-family: 'Inter', sans-serif;
  font-size: 50px;
  font-weight: 700;
  line-height: 67px;
  letter-spacing: 0%;
}

.hero__description {
  font-family: 'Inter', sans-serif;
  font-size: 38px;
  font-weight: 400;
  line-height: 50px;
  letter-spacing: 0%;
  color: var(--color-text-1);
  }

.hero__description strong {
  font-weight: 700;
}

/* --- Кнопка CTA --- */
.hero__btn {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  align-self: flex-start;

  padding: var(--spacing-md) var(--spacing-xl);
  border-radius: 50px;
  border: 3.85px solid #FFFFFF;

  /* ↓ Задай цвет фона, цвет текста и hover-эффект по дизайну */
  background-color: var(--color-primary);
  color: var(--color-white);
  font-weight: var(--font-weight-semibold);
  font-size: var(--font-size-xl);

  transition: background-color var(--transition-fast), transform var(--transition-fast);
}

.hero__btn:hover {
  background-color: var(--color-primary-dark);
  transform: translateY(-1px);
}

.hero__btn-circle {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 75px;
  height: 75px;
  border-radius: 50%;
  background-color: #A3C3F8;
  flex-shrink: 0;
}


/* --- Декоративная зона --- */
.hero__visual {
  flex: 0 0 40%;             /* фиксированная ширина визуала */
  max-width: 480px;
}

.hero__visual-img {
  width: 100%;
  height: auto;
  display: block;
  object-fit: contain;
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
