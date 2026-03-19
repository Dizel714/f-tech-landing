<script setup>
/* HeroSection — первый экран */
</script>

<template>
  <section class="hero" id="hero">
    <div class="hero__container">

      <div class="hero__content">
        <h1 class="hero__title">
          Ф Тех — технологический партнёр для банков и финтехов
        </h1>
        <p class="hero__description">
                   <strong>Создаём автоматизированные системы под задачи клиента:</strong> от аналитики до промышленной эксплуатации
        </p>
        <a href="#solutions" class="hero__btn">
          Ознакомиться с проектом
          <img src="/icon-arrow-circle.svg" alt="" class="cta__btn-circle" aria-hidden="true" />
                    <span class="hero__btn-circle">
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
  width: 100%;
  min-height: calc(100vh / 3 * 2);
  padding-top: var(--header-height);

  display: flex;
  justify-content: center;
  align-items: flex-end;

  background: linear-gradient(180deg, rgba(154, 194, 255, 0.15) 0%, rgba(255, 255, 255, 0.15) 100%);
  border-radius: 10px;
}

/* --- Внутренний контейнер --- */
.hero__container {
  display: flex;             /* контент слева, визуал справа */
  align-items: flex-end;
  
  max-width: var(--container-max);
  width: 100%;
  margin: 0 auto;
  padding: var(--spacing-3xl) 0 var(--spacing-3xl) var(--container-padding);
}

/* --- Текстовый блок --- */
.hero__content {
  flex: 1;
  max-width: 812px;

  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  gap: var(--spacing-lg);
}

.hero__title {
  width: 842px;
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-size: 50px;
  font-weight: 700;
  line-height: 67px;
  color: #000000;
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
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  

  width: 460px;
  height: 90px;
  padding: 0 24px;
  border-radius: 50px;
  border: 3.85px solid #FFFFFF;

  /* ↓ Задай цвет фона, цвет текста и hover-эффект по дизайну */
  background-color: #306AF2;
  font-family: 'Inter', sans-serif; 
  font-style: normal;
  font-weight: 400;
  font-size: 21px;
  line-height: 44px;
  color: #FFFFFF;

  transition: background-color var(--transition-fast), transform var(--transition-fast);
}

.hero__btn:hover {
  background-color: var(--color-primary-dark);
  transform: translateY(-1px);
}

.hero__btn-circle {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 75px;
  height: 75px;
  flex-shrink: 0;
}

.hero__btn-icon {
  width: 100%;
  height: 100%;
  object-fit: contain;
}


/* --- Декоративная зона --- */
.hero__visual {
  flex: 0 0 875px;
  max-width: 875px;
  margin-bottom: calc(-1 * var(--spacing-3xl));
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
