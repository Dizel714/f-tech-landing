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
        <a href="/presentation.pdf" download class="hero__btn">
          <span class="hero__btn-text">Ознакомиться с проектом</span>
          <img src="/icon-arrow-circle.svg" alt="" class="hero__btn-icon" aria-hidden="true" />
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
  min-height: 100vh;
  padding-top: var(--header-height);
  display: flex;
  justify-content: center;
  align-items: flex-end;
  background: linear-gradient(180deg, rgba(154, 194, 255, 0.15) 0%, rgba(255, 255, 255, 0.15) 100%);
  background-size: 100% 100%;
  background-repeat: no-repeat;
  
  /* Клипинг без создания scroll-контекста: горизонтальное переполнение от картинки
     обрезается по правому краю секции, а вертикальный overlap на следующую секцию сохраняется */
  overflow-x: clip;
}

/* --- Внутренний контейнер --- */
.hero__container {
  display: flex;             /* контент слева, визуал справа */
  align-items: flex-end;
  gap: var(--spacing-xl);    /* зазор между текстом и картинкой — без наложения */
  
  max-width: var(--container-max);
  width: 100%;
  margin: 0 auto;
  padding: var(--spacing-3xl) 0 0 var(--container-padding);
}

/* --- Текстовый блок --- */
.hero__content {
  flex: 1 0 320px; /* flex-shrink: 0 — текст не сжимается, картинка уступает место */
  min-width: 0;
  max-width: 812px;

  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  gap: var(--spacing-lg);
}

.hero__title {
  width: 100%;
  max-width: 100%;
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-size: 50px;
  font-weight: 700;
  line-height: 67px;
  color: #000000;
  text-align: left;
}

.hero__description {
  font-family: 'Inter', sans-serif;
  font-size: 38px;
  font-weight: 400;
  line-height: 50px;
  letter-spacing: 0%;
  color: var(--color-text-1);
  text-align: left;
  }

.hero__description strong {
  font-weight: 700;
}

/* --- Кнопка CTA --- */
.hero__btn {
  display: inline-flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  white-space: nowrap;

    /* зазор до следующего блока (фичи / картинка в колонке); у .hero__visual отступа нет */
  margin-bottom: var(--spacing-3xl);

  width: 460px;
  height: 90px;
  padding: 0 10px 0 24px;
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

.hero__btn-text {
  flex: 1;
}

.hero__btn-icon {
  width: 75px;
  height: 75px;
  flex-shrink: 0;
  object-fit: contain;
}



/* --- Декоративная зона --- */
.hero__visual {
  flex: 0 1 875px; /* flex-shrink: 1 — картинка сжимается, не расширяя контейнер */
  min-width: 0;
  max-width: 875px;
  margin-bottom: 0;
  margin-left: auto;
  margin-right: 0;
  align-self: flex-end;
}

.hero__visual-img {
  width: 100%;
  height: auto;
  display: block;
  object-fit: contain;
}

/* --- Адаптив --- */
@media (max-width: 1440px) {
  .hero__title {
    width: 100%;
    font-size: 37.5px;
    line-height: 50px;
    font-style: normal;
  }

  .hero__visual {
    flex: 0 1 700px;
    max-width: 700px;
  }

  .hero__description {
    font-size: 28.5px;
    line-height: 38px;
  }

  .hero__btn {
  font-size: 21px;
  line-height: 44px;
}
}

@media (max-width: 1024px) {
  .hero__container {
    padding: var(--spacing-2xl) 0 0 var(--container-padding);
  }

  .hero__title {
    width: 100%;
    font-size: 32px;
    line-height: 43px;
  }

  .hero__description {
    font-size: 24.32px;
    line-height: 32px;
  }

  .hero__btn {
    width: 360px;
    height: 72px;
    font-size: 16px;
  }

  .hero__btn-icon {
    width: 58px;
    height: 58px;
  }

  .hero__visual {
    flex: 0 1 480px;
    max-width: 480px;
    margin-bottom: 0;
  }
}

/* Планшет 794–1024: без «провала» внизу экрана — контент сразу под шапкой */
@media (max-width: 1024px) and (min-width: 794px) {
  .hero {
    min-height: auto;
    align-items: flex-start;
    padding-bottom: var(--spacing-3xl);
  }

  .hero__container {
    padding-top: var(--spacing-lg);
  }
}

@media (max-width: 793px) {
  .hero {
    align-items: flex-end;
  }

  .hero__container {
    flex-direction: column;
    align-items: center; /* колонка: заголовок → текст → кнопка → картинка по центру */
    justify-content: flex-end;
    /* Больше отступов от краёв — уже колонка с текстом */
    padding: var(--spacing-2xl) 0 0 45px;
  }

  .hero__content {
    flex: none;
    width: 100%;
    max-width: 100%;
    align-items: center;
    text-align: center;
    justify-content: flex-start;
    padding-right: var(--spacing-3xl);
  }

  .hero__title {
    font-size: 25px;
    line-height: 34px;
  }

  .hero__description {
    font-size: 19px;
    line-height: 25px;
  }

  .hero__btn {
    width: 300px;
    max-width: 100%;
    height: 60px;
    font-size: 14px;
    align-self: center;
    margin-left: 15px;
  }

  .hero__visual {
    flex: none;
    width: 100%;
    max-width: 100%;
    margin: 0;
    display: block;
    line-height: 0;
    font-size: 0;
  }

  .hero__visual-img {
    width: 100%;
    height: auto;
    display: block;
  }

  .hero__btn-icon {
  width: 37px;
  height: 37px;
  }
}


@media (max-width: 375px) {
  .hero__container {
    padding: var(--spacing-xl) 0 0 var(--spacing-md);
  }
    .hero__content {
    padding-right: var(--spacing-xl);
  }
  
  .hero__title {
    font-size: 24px;
    line-height: 32px;
  }

  .hero__description {
    font-size: 18px;
    line-height: 24px;
  }

  .hero__btn {
    width: 100%;
    height: 54px;
    font-size: 10px;
    padding: 0 16px;
  }

  .hero__btn-icon {
    width: 35px;
    height: 35px;
  }
}
</style>
