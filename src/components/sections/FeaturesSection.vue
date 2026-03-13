<script setup>
import CheckItem from '../ui/CheckItem.vue'

/* 5 элементов — один содержит цепочку аналитика → разработка → внедрение → сопровождение */
const features = [
  { id: 1, text: '100+ специалистов в команде' },
  { id: 2, text: 'Применяем самые передовые решения рынка' },
  {
    id: 3,
    text: 'Полный цикл: аналитика → разработка → внедрение → сопровождение',
    hasArrowChain: true,
  },
  { id: 4, text: 'Надёжный технологический партнёр для бизнеса' },
  { id: 5, text: 'Ориентация на конечный бизнес-результат' },
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
  background: #9AC2FF26;
  padding: var(--spacing-3xl) 0;
}

/* --- Контейнер --- */
.features__container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--container-padding);
}

/* --- Grid 5 элементов в 2 колонки ---
   При нечётном количестве последний элемент растягивается на полную ширину */
.features__grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: var(--spacing-lg) var(--spacing-2xl);

  /* ↓ Настрой gap между строками и колонками по дизайну */
}

/* --- Один элемент: флекс (иконка + текст) --- */

.features__item {
  display: flex;
  align-items: center;
  gap: var(--spacing-md);
  
}

.features__item-icon {
  flex-shrink: 0;
  display: flex;
  align-items: center;
}

.features__item-text {
  width: 624px;
  height: 108px;
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
  letter-spacing: 0%;
  vertical-align: middle;
  color: #000000;
}

.features__chain-arrow {
  color: #7DA6F6;
  font-weight: var(--font-weight-bold);
}

/* --- Адаптив --- */
@media (max-width: 600px) {
  .features__grid {
    grid-template-columns: 1fr;
  }
}
</style>
