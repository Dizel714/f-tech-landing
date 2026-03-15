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
            Расскажите о задаче — предложим оптимальное архитектурное и технологическое решение
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
  background-color: var(--bg-section-alt);
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

  padding: var(--spacing-4xl) var(--spacing-3xl);
  border-radius: var(--radius-xl);

  /* ↓ Задай background (градиент или цвет), box-shadow и border по дизайну */
  background-color: var(--color-primary);
}

/* --- Контент карточки — центрирован по вертикали и горизонтали --- */
.cta__content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--spacing-lg);
  text-align: center;
  max-width: 600px;
}

.cta__title {
  /* ↓ Задай font-size, font-weight и color по дизайну */
  font-size: var(--font-size-3xl);
  font-weight: var(--font-weight-bold);
  color: var(--color-white);
  line-height: var(--line-height-tight);
}

.cta__subtitle {
  /* ↓ Задай font-size и color по дизайну */
  font-size: var(--font-size-md);
  color: rgba(255, 255, 255, 0.85);
  line-height: var(--line-height-relaxed);
}

/* --- Кнопка --- */
.cta__btn {
  display: inline-block;
  padding: var(--spacing-md) var(--spacing-2xl);
  border-radius: var(--radius-md);

  /* ↓ Задай цвет фона кнопки и hover-эффект по дизайну */
  background-color: var(--color-white);
  color: var(--color-primary);
  font-size: var(--font-size-base);
  font-weight: var(--font-weight-semibold);

  transition: background-color var(--transition-fast), transform var(--transition-fast);
}

.cta__btn:hover {
  background-color: var(--color-gray-100);
  transform: translateY(-2px);
}

/* --- Адаптив --- */
@media (max-width: 600px) {
  .cta__card {
    padding: var(--spacing-2xl) var(--spacing-lg);
  }

  .cta__title {
    font-size: var(--font-size-2xl);
  }
}
</style>
