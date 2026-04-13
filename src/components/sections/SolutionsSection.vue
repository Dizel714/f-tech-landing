<script setup>
/* SolutionsSection — блок «Наши решения», одна карточка "Фабрика платежей" на всю ширину */

const solutions = [
  {
    id: 4,
    title: 'Фабрика платежей',
    description: 'Централизованная маршрутизация и обработка платежей',
    advantages: {
      heading: 'Преимущества:',
      items: [
        'Снижение операционных рисков',
        'Повышение отказоустойчивости',
        'Контроль статусов и жизненного цикла',
        'Масштабируемость под высокие нагрузки',
      ],
    },
  },
]
</script>

<template>
  <section class="solutions" id="solutions">
    <div class="solutions__container">
      <!-- Grid с одной карточкой на всю ширину -->
      <div class="solutions__grid">
        <article
          v-for="solution in solutions"
          :key="solution.id"
          class="solution-card"
        >
          <h3 class="solution-card__title">{{ solution.title }}</h3>
          <p class="solution-card__description">{{ solution.description }}</p>

          <!-- Секция преимуществ: заголовок + список с галочками -->
          <div class="solution-card__advantages">
            <h4 class="solution-card__advantages-heading">
              {{ solution.advantages.heading }}
            </h4>
            <div class="solution-card__advantages-wrapper">
              <ul class="solution-card__advantages-list">
                <li
                  v-for="(item, idx) in solution.advantages.items"
                  :key="idx"
                  class="solution-card__advantage-item"
                >
                  <!-- Иконка галочки -->
                  <span class="solution-card__check-icon" aria-hidden="true">
                    <img src="/icon-check-solution.svg" alt="" />
                  </span>
                  <span class="solution-card__advantage-text">{{ item }}</span>
                </li>
              </ul>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* ==========================================================================
   SOLUTIONS SECTION — «Наши решения»
   ========================================================================== */

.solutions {
  width: 100%;
  background-image: url('/solutions-bg.png');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  padding: var(--spacing-4xl) 0;
  display: flex;
  justify-content: center;
}

/* Одна колонка: отдельный фон (файл: public/solutions-bg-mobile.png) */
@media (max-width: 1024px) {
  .solutions {
    background-color: var(--bg-section-alt);
    background-image: url('/solutions-bg-mobile.png');
    background-size: cover;
    background-position: center top;
    background-repeat: no-repeat;
  }
}

/* --- Контейнер --- */
.solutions__container {
  max-width: var(--container-max);
  width: 100%;
  margin: 0 auto;
  padding: 0 var(--container-padding);
}

/* --- Grid: одна карточка на всю ширину --- */
.solutions__grid {
  display: flex;
  justify-content: center;
  width: 100%;
}

/* ==========================================================================
   SOLUTION CARD — карточка на всю ширину с отступами и центрированием
   ========================================================================== */

.solution-card {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
  width: 100%;
  
  padding: var(--spacing-xl);
  border-radius: var(--radius-lg);

  background-color: var(--bg-card);
  /* Мягкая голубая оконтовка: размытое свечение по периметру */
  box-shadow:
    0 0 12px rgba(130, 175, 255, 0.5),
    0 0 26px rgba(154, 194, 255, 0.32),
    0 6px 20px rgba(0, 0, 0, 0.06);
  
  /* Центрирование всего содержимого */
  text-align: center;
}

.solution-card {
  height: auto;
}

.solution-card__title {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 38px;
  line-height: 30px;
  letter-spacing: -0.05em;
  color: #000000;
  margin-bottom: var(--spacing-xl);
}

.solution-card__description {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 26px;
  line-height: 30px;
  letter-spacing: -0.05em;
  color: #5688F4;
}

/* --- Секция преимуществ --- */
.solution-card__advantages {
  margin-top: auto;
  padding-top: var(--spacing-md);
  display: flex;
  flex-direction: column;
  align-items: center; /* Центрируем контейнер с обёрткой */
}

/* Обёртка для списка, которая ограничивает ширину и выравнивает по левому краю */
.solution-card__advantages-wrapper {
  display: inline-block;
  text-align: left; /* Выравнивание содержимого по левому краю */
}

.solution-card__advantages-heading {
  margin-bottom: var(--spacing-sm);
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 700;
  font-size: 28px;
  line-height: 51px;
  letter-spacing: -0.05em;
  color: #000000;
  text-align: center; /* Заголовок по центру */
}

/* --- Список преимуществ --- */
.solution-card__advantages-list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
  list-style: none;
  margin: 0;
  padding: 0;
}

.solution-card__advantage-item {
  display: flex;
  align-items: center;
  gap: var(--spacing-2xl);
  /* Убираем justify-content, оставляем левое выравнивание */
}

.solution-card__check-icon {
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 33px;
  height: 33px;
  color: var(--color-icon-check);
}

.solution-card__check-icon img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.solution-card__advantage-text {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 28px;
  line-height: 51px;
  letter-spacing: -0.05em;
  color: #000000;
}

/* --- Адаптив --- */
@media (max-width: 1440px) {
  .solutions__heading {
    font-size: 38px;
    line-height: 38px;
  }

  .solution-card {
    gap: var(--spacing-lg);
  }

  .solution-card__title {
    font-size: 29px;
    line-height: 22px;
  }

  .solution-card__description {
    font-size: 20px;
    line-height: 22px;
  }

  .solution-card__advantage-text,
  .solution-card__advantages-heading {
    font-size: 20px;
    line-height: 22px;
  }

  .solution-card__advantages-list {
    gap: var(--spacing-md);
  }

  .solution-card__advantages-heading {
    margin-bottom: var(--spacing-lg);
  }

  .solution-card__check-icon {
    width: 24px;
    height: 24px;
  }
}

@media (max-width: 1024px) {
  .solutions__heading {
    font-size: 28px;
    line-height: 27px;
  }

  .solution-card {
    gap: var(--spacing-lg);
  }

  .solutions__grid {
    display: flex;
  }

  .solution-card__title {
    font-size: 24px;
    line-height: 19px;
  }

  .solution-card__description {
    font-size: 17px;
    line-height: 19px;
  }

  .solution-card__advantage-text,
  .solution-card__advantages-heading {
    font-size: 17px;
    line-height: 19px;
  }

  .solution-card__advantages-list {
    gap: var(--spacing-md);
  }

  .solution-card__advantages-heading {
    margin-bottom: var(--spacing-lg);
  }

  .solution-card__check-icon {
    width: 21px;
    height: 21px;
  }
}

@media (max-width: 793px) {
  .solutions {
    background-color: var(--bg-section-alt);
    background-image: url('/solutions-bg-mobile793.png');
    background-size: cover;
    background-position: center top;
    background-repeat: no-repeat;
    padding: var(--spacing-2xl) 0;
  }

  .solutions__heading {
    font-size: 22px;
    line-height: 21px;
  }

  .solution-card {
    gap: var(--spacing-xs);
  }

  .solution-card__title {
    font-size: 19px;
    line-height: 15px;
    margin-bottom: var(--spacing-lg);
  }

  .solution-card__description {
    font-size: 13px;
    line-height: 15px;
  }

  .solution-card__advantage-text,
  .solution-card__advantages-heading {
    font-size: 13px;
    line-height: 15px;
  }

  .solution-card__advantages-list {
    gap: var(--spacing-xs);
  }

  .solution-card__advantages-heading {
    margin-bottom: var(--spacing-lg);
  }

  .solution-card__check-icon {
    width: 16px;
    height: 16px;
  }

  .solutions__grid {
    gap: var(--spacing-lg);
  }
}

@media (max-width: 580px) {
  .solutions {
    background-color: var(--bg-section-alt);
    background-image: url('/solutions-bg-mobile375.png');
    background-size: cover;
    background-position: center top;
    background-repeat: no-repeat;
    padding: var(--spacing-2xl) 0;
  }
}

@media (max-width: 375px) {
  .solutions__heading {
    font-size: 12px;
    line-height: 14px;
  }

  .solution-card {
    padding: var(--spacing-md);
  }

  .solution-card__title {
    font-size: 18px;
    line-height: 14px;
    margin-bottom: var(--spacing-sm);
  }

  .solution-card__description {
    font-size: 12px;
    line-height: 14px;
  }

  .solution-card__advantage-text,
  .solution-card__advantages-heading {
    font-size: 14px;
    line-height: 26px;
  }

  .solution-card__advantage-item {
    gap: var(--spacing-md);
  }

  .solution-card__advantages-list {
    gap: var(--spacing-lg);
  }

  .solution-card__advantages-heading {
    margin-bottom: var(--spacing-lg);
  }

  .solution-card__check-icon {
    width: 15px;
    height: 15px;
  }
}
</style>