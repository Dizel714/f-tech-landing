<script setup>
/* ExpertiseSection — «Технологическая экспертиза полного цикла»
   Левая треть: подзаголовок + 8 направлений */

const directions = [
  'Анализ бизнес-требований и архитектуры',
  'Fullstack-разработка сложных систем',
  'BI-аналитика и отчётность',
  'API management и интеграции',
  'AI/ML-модели для финтеха',
  'Cloud migrations',
  'DevSecOps и CI/CD пайплайны',
  'Нагрузочное тестирование и оптимизация',
]
</script>

<template>
  <section class="expertise" id="expertise">
    <div class="expertise__container">

      <!-- Главный заголовок -->
      <h2 class="expertise__heading">
        Технологическая экспертиза полного цикла
      </h2>

      <!-- Основной layout: первая треть — список направлений, остальное — стек -->
      <div class="expertise__body">

        <!-- Левая треть: список направлений -->
        <div class="expertise__directions">
          <h3 class="expertise__directions-title">Наши направления</h3>
          <ul class="expertise__directions-list">
            <li
              v-for="(dir, idx) in directions"
              :key="idx"
              class="expertise__direction-item"
            >
              <!-- Иконка стрелки вправо -->
              <span class="expertise__direction-icon" aria-hidden="true">
                <svg width="18" height="18" viewBox="0 0 18 18" fill="none">
                  <path d="M3.75 9H14.25M14.25 9L9.75 4.5M14.25 9L9.75 13.5"
                    stroke="currentColor" stroke-width="1.6"
                    stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </span>
              <span class="expertise__direction-text">{{ dir }}</span>
            </li>
          </ul>
        </div>

        <!-- Правые две трети: слот для TechStackSection -->
        <div class="expertise__stack-area">
          <slot />
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
/* ==========================================================================
   EXPERTISE SECTION — «Технологическая экспертиза полного цикла»
   ========================================================================== */

.expertise {
  /* ↓ Задай background-color и padding по дизайну */
  width: 100%;
  background-color: var(--bg-page);
  padding: var(--spacing-4xl) 0;
  display: flex;
  justify-content: center;
}

/* --- Контейнер --- */
.expertise__container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--container-padding);
}

/* --- Главный заголовок --- */
.expertise__heading {
  margin-bottom: var(--spacing-3xl);
  /* ↓ Задай font-size, font-weight и color по дизайну */
  font-size: var(--font-size-3xl);
  font-weight: var(--font-weight-bold);
  color: var(--color-text-primary);
  line-height: var(--line-height-tight);
}

/* --- Двухколонный layout: 1/3 + 2/3 --- */
.expertise__body {
  display: grid;
  grid-template-columns: 1fr 2fr; /* первая треть + остаток */
  gap: var(--spacing-3xl);

  /* ↓ Настрой gap по дизайну */
}

/* --- Левая колонка: направления --- */
.expertise__directions {
  /* Ничего лишнего — содержимое идёт в колонку по умолчанию */
}

.expertise__directions-title {
  margin-bottom: var(--spacing-lg);
  /* ↓ Задай font-size, font-weight и color по дизайну */
  font-size: var(--font-size-lg);
  font-weight: var(--font-weight-semibold);
  color: var(--color-text-primary);
}

/* --- Список направлений в колонку --- */
.expertise__directions-list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.expertise__direction-item {
  display: flex;             /* флекс: иконка стрелки слева, текст справа */
  align-items: flex-start;
  gap: var(--spacing-sm);
}

.expertise__direction-icon {
  flex-shrink: 0;
  color: var(--color-icon-arrow);
  margin-top: 3px;
}

.expertise__direction-text {
  /* ↓ Задай font-size и color по дизайну */
  font-size: var(--font-size-base);
  color: var(--color-text-primary);
  line-height: var(--line-height-normal);
}

/* --- Правая область (слот для TechStackSection) --- */
.expertise__stack-area {
  /* Стили задаются в TechStackSection — эта область только даёт место */
}

/* --- Адаптив --- */
@media (max-width: 900px) {
  .expertise__body {
    grid-template-columns: 1fr;
  }

  .expertise__heading {
    font-size: var(--font-size-2xl);
  }
}
</style>
