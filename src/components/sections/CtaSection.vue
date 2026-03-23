<script setup>
/* CtaSection — карточка призыва к действию.
   По клику на кнопку открывает модальное окно через emit. */

const emit = defineEmits(['open-modal'])

function handleClick() {
  emit('open-modal')
}
</script>

<template>
  <section class="cta">
    <div class="cta__container">
      <div class="cta__card">
        <div class="cta__content">

          <div class="cta__text">
            <h2 class="cta__title">Обсудим ваш проект</h2>
            <p class="cta__subtitle">
              Поможем спроектировать и внедрить технологическое решение под задачи вашего банка или финтех-проекта
            </p>
          </div>

          <button class="cta__btn" type="button" @click="handleClick">
            Запросить консультацию
            <img src="/icon-arrow-circle.svg" alt="" class="cta__btn-icon" aria-hidden="true" />
          </button>

        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* ==========================================================================
   CTA SECTION — карточка призыва к действию
   ========================================================================== */

.cta {
  /* ↓ Задай background-color и padding по дизайну */
  width: 100%;
  background-color: #F5F5F5;
  padding: 0;
  display: flex;
  justify-content: center;
}

/* --- Контейнер: на всю ширину экрана, боковые поля как у сайта --- */
.cta__container {
  width: 100%;
  max-width: none;
  margin: 0;
  padding: 0 var(--container-padding);
  box-sizing: border-box;
}

/* --- Карточка: почти на всю ширину вьюпорта (минус padding контейнера) --- */
.cta__card {
  display: flex;
  align-items: stretch;
  justify-content: center;
  padding: 115px 0 67px;
  box-sizing: border-box;

  width: 100%;
  height: 596px;
  border-radius: 30px;
  background-image: url('/cta-bg.png');
  background-size: cover;
  background-position: center;
}

/* --- Контент карточки — колонка с фиксированным зазором текст ↔ кнопка на всех ширинах --- */
.cta__content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: var(--spacing-3xl);
  text-align: center;
  width: 100%;
  max-width: 874px;
  box-sizing: border-box;
}

/* --- Группа заголовок + подзаголовок --- */
.cta__text {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 61px;
}

.cta__title {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 700;
  font-size: 30px;
  line-height: 30px;
  text-align: center;
  letter-spacing: -0.03em;
  color: #43359C;
}

.cta__subtitle {
font-family: 'Inter', sans-serif;
font-style: normal;
font-weight: 400;
font-size: 28px;
line-height: 35px;
text-align: center;

color: #000000;
}

/* --- Кнопка --- */
.cta__btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 467px;
  height: 90px;
  padding: 0 var(--spacing-2xl);
  border-radius: 53.8658px;
  background: #306AF2;
  font-family: 'Inter';
  font-style: normal;
  font-weight: 400;
  font-size: 25.7143px;
  line-height: 1;
  color: #FFFFFF;
  transition: background-color var(--transition-fast), transform var(--transition-fast);
}

.cta__btn:hover {
  background-color: #1a57de;
  transform: translateY(-2px);
}

.cta__btn-icon {
  width: 75px;
  height: 75px;
  margin-left: 23px;
  flex-shrink: 0;
}

/* --- Адаптив --- */
@media (max-width: 1440px) {
  .cta__card {
    width: 100%;
    height: auto;
    padding: 80px var(--spacing-3xl);
  }

  .cta__title {
    font-size: 23px;
    line-height: 22px;
  }

  .cta__subtitle {
    font-size: 21px;
    line-height: 26px;
  }

  .cta__content {
    width: 100%;
    max-width: 874px;
  }
}

@media (max-width: 1024px) {
  .cta__card {
    padding: 60px var(--spacing-2xl);
    border-radius: 20px;
  }

  .cta__title {
    font-size: 19px;
    line-height: 19px;
  }

  .cta__subtitle {
    font-size: 18px;
    line-height: 22px;
  }

  .cta__btn {
    width: 360px;
    height: 72px;
    font-size: 20px;
  }

  .cta__btn-icon {
    width: 58px;
    height: 58px;
  }

  .cta__text {
    gap: 40px;
  }

  .cta__content {
    gap: var(--spacing-2xl);
  }
}

@media (max-width: 793px) {
  .cta__card {
    padding: 48px var(--spacing-xl);
    border-radius: 16px;
  }

  .cta__title {
    font-size: 15px;
    line-height: 15px;
  }

  .cta__subtitle {
    font-size: 14px;
    line-height: 18px;
  }

  .cta__btn {
    width: 280px;
    height: 60px;
    font-size: 16px;
    padding: 0 var(--spacing-lg);
  }

  .cta__btn-icon {
    width: 46px;
    height: 46px;
    margin-left: 12px;
  }

  .cta__text {
    gap: 28px;
  }

  .cta__content {
    gap: var(--spacing-xl);
  }

}

@media (max-width: 375px) {
  .cta__card {
    padding: 36px var(--spacing-md);
    border-radius: 12px;
  }

  .cta__title {
    font-size: 14px;
    line-height: 14px;
  }

  .cta__subtitle {
    font-size: 13px;
    line-height: 17px;
  }

  .cta__btn {
    width: 100%;
    height: 54px;
    font-size: 14px;
  }

  .cta__btn-icon {
    width: 38px;
    height: 38px;
    margin-left: 8px;
  }

  .cta__content {
    gap: var(--spacing-lg);
  }

}

</style>
