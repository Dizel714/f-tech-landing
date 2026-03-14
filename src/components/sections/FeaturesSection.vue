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
  display: flex;
  justify-content: center;
  align-items: center;
}

/* --- Контейнер --- */
.features__container {
  max-width: 1920px;
  margin: 0 auto;
  padding: 0 var(--container-padding);
  width: 1920px;
  display: flex;
  justify-content: center;
}

/* --- Grid 5 элементов в 2 колонки ---
   При нечётном количестве последний элемент растягивается на полную ширину */
.features__grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: var(--spacing-lg) var(--spacing-2xl);
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
