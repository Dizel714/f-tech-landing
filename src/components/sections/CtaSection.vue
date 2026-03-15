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

          <h2 class="cta__title">Обсудим ваш проект</h2>

          <p class="cta__subtitle">
            Поможем спроектировать и внедрить технологическое решение под задачи вашего банка или финтех-проекта
          </p>

          <button class="cta__btn" type="button" @click="handleClick">
            Запросить консультацию
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
  padding: var(--spacing-3xl) 0;
  display: flex;
  justify-content: center;
}

/* --- Контейнер --- */
.cta__container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--container-padding);
}

/* --- Карточка: большой прямоугольник с центрированным контентом --- */
.cta__card {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 1600px;
  height: 596px;
  border-radius: 30px;
  background-image: url('/cta-bg.png');
  background-size: cover;
  background-position: center;
}

/* --- Контент карточки — центрирован по вертикали и горизонтали --- */
.cta__content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--spacing-lg);
  text-align: center;
  width: 874px;
  height: 66px;
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
font-family: 'Inter';
font-style: normal;
font-weight: 400;
font-size: 28px;
line-height: 35px;
text-align: center;

color: #000000;
}

/* --- Кнопка --- */
.cta__btn {
  display: inline-block;
  padding: var(--spacing-md) var(--spacing-2xl);
  border-radius: var(--radius-md);

  /* ↓ Задай цвет фона кнопки и hover-эффект по дизайну */
  background: #306AF2;
  border-radius: 53.8658px;
  font-size: var(--font-size-base);
  font-weight: var(--font-weight-semibold);
  font-family: 'Inter';
  font-style: normal;
  font-weight: 400;
  font-size: 25.7143px;
  line-height: 62px;

  display: flex;
  align-items: center;

  color: #FFFFFF;

  transition: background-color var(--transition-fast), transform var(--transition-fast);
}

.cta__btn:hover {
  background-color: var(--color-gray-100);
  transform: translateY(-2px);
}

</style>
