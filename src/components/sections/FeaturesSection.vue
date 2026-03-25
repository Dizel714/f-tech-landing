<script setup>
import CheckItem from '../ui/CheckItem.vue'

/* 5 элементов — один содержит цепочку аналитика → разработка → внедрение → сопровождение */
const features = [
  { id: 1, text: '100+ специалистов' },
  { id: 2, text: 'Промышленная эксплуатация решений' },
  {
    id: 3,
    text: 'Полный цикл: аналитика → разработка → внедрение → сопровождение',
    hasArrowChain: true,
  },
  { id: 4, text: 'Надёжный технологический партнёр' },
  { id: 5, text: 'Ориентация на измеримый бизнес-результат' },
]
</script>

<template>
  <section class="features" id="features">
    <div class="features__container">

      <ul class="features__grid">
        <li
          v-for="item in features"
          :key="item.id"
          class="features__item"
          :class="`features__item--id-${item.id}`"
        >
          <!-- Иконка -->
          <span class="features__item-icon" aria-hidden="true">
           <img src="/icon-check.svg" alt="" width="100" height="100" />
          </span>

          <!-- Текст: обычный или цепочка со стрелками -->
          <span v-if="!item.hasArrowChain" class="features__item-text">
            {{ item.text }}
          </span>

          <!-- Цепочка: «аналитика → разработка → внедрение → сопровождение» -->
          <span v-else class="features__item-text features__item-text--chain">
            Полный цикл:
            <span class="features__chain">
              <span class="features__chain-step">аналитика</span>
              <span class="features__chain-arrow" aria-hidden="true">→</span>
              <span class="features__chain-step">разработка</span>
              <span class="features__chain-arrow" aria-hidden="true">→</span>
              <span class="features__chain-step">внедрение</span>
              <span class="features__chain-arrow" aria-hidden="true">→</span>
              <span class="features__chain-step">сопровождение</span>
            </span>
          </span>
        </li>
      </ul>

    </div>
  </section>
</template>

<style scoped>
/* ==========================================================================
   FEATURES SECTION — блок с 5 ключевыми преимуществами
   ========================================================================== */

.features {
  width: 100%;
  background: rgba(154, 194, 255, 0.15);
  padding: var(--spacing-3xl) 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* --- Контейнер --- */
.features__container {
  width: 100%;
  max-width: 1920px;
  margin: 0 auto;
  padding: 0 var(--container-padding);
  display: flex;
  justify-content: center;
}

/* --- Grid 5 элементов в 2 колонки ---
   При нечётном количестве последний элемент растягивается на полную ширину */
.features__grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: var(--spacing-4xl) var(--spacing-2xl);
  margin: 0 auto;

  /* ↓ Настрой gap между строками и колонками по дизайну */
}

/* --- Один элемент: флекс (иконка + текст) --- */

.features__item {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: var(--spacing-md);
}

.features__item-icon {
  flex-shrink: 0;
  display: flex;
  align-items: center;
}

.features__item-text {
  font-family: 'Inter', sans-serif;
  font-size: 34px;
  font-weight: 700;
  line-height: 35px;
  letter-spacing: 0%;
  vertical-align: middle;
  color: #000000;
  
}

/* --- Цепочка шагов --- */
.features__item-text--chain {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
}

.features__chain {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: var(--spacing-xs);
}

.features__chain-step {
  font-family: 'Inter', sans-serif;
  font-size: 34px;
  font-weight: 700;
  line-height: 35px;
  letter-spacing: 0;
  color: #000000;
}

.features__chain-arrow {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 700;
  font-size: 34px;
  line-height: 35px;
  display: inline-flex;
  align-items: center;
  color: #5688F4;
}

/* --- Адаптив --- */
@media (max-width: 1440px) {
  .features__item-text {
  font-size: 25px;
  line-height: 26px;
  }

  .features__chain-step {
    font-size: 25px;
    line-height: 26px;
  }

  .features__item-icon img {
    width: 80px;
    height: 80px;
  }
}

@media (max-width: 1024px) {
    .features__item-text {
  font-size: 22px;
  line-height: 22px;
  text-align: center;
  text-align: left;
  }

  .features__chain-step {
    font-size: 22px;
    line-height: 1.2;
  }

  .features__chain-arrow {
    font-size: 22px;
    line-height: 1.2;
  }

  .features__item-text--chain {
    gap: 4px;
  }

  .features__chain {
    row-gap: 4px;
  }

  .features__container {
    padding-left: var(--spacing-4xl);
    padding-right: var(--spacing-4xl);
  }

  .features__grid {
    grid-template-columns: 1fr;
    justify-items: stretch;
    width: 100%;
    gap: var(--spacing-xl);
  }

    /* В столбик: 1 → 3 → 5 → 2 → 4 */
  .features__item--id-1 {
    order: 1;
  }

  .features__item--id-2 {
    order: 4;
  }

  .features__item--id-3 {
    order: 2;
  }

  .features__item--id-4 {
    order: 5;
  }

  .features__item--id-5 {
    order: 3;
  }

  .features__item {
    justify-content: flex-start;
    align-items: center; /* середина текста по вертикали = середина иконки */
    width: 100%;
    max-width: 100%;
  }

  .features__item-text--chain {
    text-align: left;
  }

  .features__chain {
    justify-content: flex-start;
  }

  .features__item-icon img {
    width: 69px;
    height: 69px;
  }
}

@media (max-width: 793px) {
  .features__container {
    padding-left: var(--spacing-3xl);
    padding-right: var(--spacing-3xl);
  }

  .features__item-text {
  font-size: 17px;
  line-height: 18px;
  }

  .features__chain-step {
    font-size: 17px;
    line-height: 18px;
  }

  .features__chain-arrow {
      font-size: 18px;
    line-height: 1.15;
  }

  .features__item-text--chain {
    gap: 2px;
  }

  .features__chain {
    row-gap: 2px;
    column-gap: var(--spacing-xs);
  }

  .features__item-icon img {
    width: 54px;
    height: 54px;
  }
}

@media (max-width: 375px) {
  .features__grid {
    grid-template-columns: 1fr;
    gap: var(--spacing-xl);
  }

  .features__item-text {
  font-size: 16px;
  line-height: 17px;
  }
  .features__chain-step {
    font-size: 16px;
    line-height: 1.2;
  }

  .features__chain-arrow {
      font-size: 15px;
    line-height: 1.15;
  }

  .features__item-text--chain {
    gap: 2px;
  }

  .features__chain {
    row-gap: 2px;
    column-gap: 6px;
  }

  .features__item {
    gap: var(--spacing-sm);
  }

  .features__item-icon img {
    width: 50px;
    height: 50px;
  }
}
</style>
