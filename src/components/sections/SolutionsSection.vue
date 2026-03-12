<script setup>
/* SolutionsSection — блок «Наши решения», Grid 2×2 из четырёх карточек */

const solutions = [
  {
    id: 1,
    title: 'Кредитно-рисковый Отдел',
    description: 'Автоматизация процессов кредитного анализа и управления рисками в реальном времени.',
    advantages: {
      heading: 'Продукт',
      items: [
        'Оценка кредитоспособности заёмщиков',
        'Мониторинг кредитного портфеля',
        'Управление дефолтами и реструктуризацией',
        'Автоматическая генерация отчётности',
      ],
    },
  },
  {
    id: 2,
    title: 'Грант-Сервис',
    description: 'Платформа для управления государственными и корпоративными грантовыми программами.',
    advantages: {
      heading: 'Возможности',
      items: [
        'Подача и рассмотрение заявок онлайн',
        'Мониторинг исполнения условий гранта',
        'Управление платёжными транзакциями',
        'Интеграция с государственными реестрами',
      ],
    },
  },
  {
    id: 3,
    title: 'Автоматизированная система для МФО',
    description: 'Комплексное решение для автоматизации микрофинансовых организаций любого масштаба.',
    advantages: {
      heading: 'Продукт',
      items: [
        'Выдача и погашение займов',
        'KYC / AML-проверки',
        'Расчёт платёжного графика',
        'Формирование резервов по МСФО',
        'Гибкий конструктор продуктов',
      ],
    },
  },
  {
    id: 4,
    title: 'Банковские потоки',
    description: 'Система управления финансовыми потоками и расчётами внутри банковской экосистемы.',
    advantages: {
      heading: 'Преимущества',
      items: [
        'Обработка транзакций в реальном времени',
        'Высокая отказоустойчивость',
        'Интеграция по API с внешними системами',
        'Масштабируемая микросервисная архитектура',
      ],
    },
  },
]
</script>

<template>
  <section class="solutions" id="solutions">
    <div class="solutions__container">

      <!-- Заголовок секции по центру -->
      <h2 class="solutions__heading">Наши решения</h2>

      <!-- Grid 2×2 из карточек -->
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
            <ul class="solution-card__advantages-list">
              <li
                v-for="(item, idx) in solution.advantages.items"
                :key="idx"
                class="solution-card__advantage-item"
              >
                <!-- Иконка галочки -->
                <span class="solution-card__check-icon" aria-hidden="true">
                  <svg width="18" height="18" viewBox="0 0 18 18" fill="none">
                    <circle cx="9" cy="9" r="9" fill="currentColor" fill-opacity="0.1"/>
                    <path d="M4.5 9.5L7.5 12.5L13.5 6.5" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </span>
                <span class="solution-card__advantage-text">{{ item }}</span>
              </li>
            </ul>
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
  /* ↓ Задай background-color и padding по дизайну */
  background-color: var(--bg-section-alt);
  padding: var(--spacing-4xl) 0;
}

/* --- Контейнер --- */
.solutions__container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--container-padding);
}

/* --- Заголовок секции --- */
.solutions__heading {
  text-align: center;
  margin-bottom: var(--spacing-3xl);

  /* ↓ Задай font-size, font-weight и color по дизайну */
  font-size: var(--font-size-3xl);
  font-weight: var(--font-weight-bold);
  color: var(--color-text-primary);
}

/* --- Grid 2×2 --- */
.solutions__grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: var(--spacing-xl);

  /* ↓ Настрой gap между карточками по дизайну */
}

/* ==========================================================================
   SOLUTION CARD — одна карточка
   ========================================================================== */

.solution-card {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);

  padding: var(--spacing-xl);
  border-radius: var(--radius-lg);

  /* ↓ Задай background-color, border и box-shadow карточки по дизайну */
  background-color: var(--bg-card);
  box-shadow: var(--shadow-md);
}

.solution-card__title {
  /* ↓ Задай font-size, font-weight и color по дизайну */
  font-size: var(--font-size-xl);
  font-weight: var(--font-weight-semibold);
  color: var(--color-text-primary);
}

.solution-card__description {
  /* ↓ Задай font-size и color по дизайну */
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
  line-height: var(--line-height-relaxed);
}

/* --- Секция преимуществ --- */
.solution-card__advantages {
  margin-top: auto;          /* прижать к нижней части карточки */
  padding-top: var(--spacing-md);

  /* ↓ Добавь border-top для визуального разделения если нужно */
  border-top: 1px solid var(--color-divider);
}

.solution-card__advantages-heading {
  margin-bottom: var(--spacing-sm);
  /* ↓ Задай font-size, font-weight и color по дизайну */
  font-size: var(--font-size-sm);
  font-weight: var(--font-weight-semibold);
  color: var(--color-text-secondary);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

/* --- Список преимуществ --- */
.solution-card__advantages-list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
}

.solution-card__advantage-item {
  display: flex;             /* флекс: иконка слева, текст справа */
  align-items: flex-start;
  gap: var(--spacing-sm);
}

.solution-card__check-icon {
  flex-shrink: 0;
  color: var(--color-icon-check);
  margin-top: 2px;
}

.solution-card__advantage-text {
  /* ↓ Задай font-size и color по дизайну */
  font-size: var(--font-size-sm);
  color: var(--color-text-primary);
  line-height: var(--line-height-normal);
}

/* --- Адаптив --- */
@media (max-width: 768px) {
  .solutions__grid {
    grid-template-columns: 1fr;
  }

  .solutions__heading {
    font-size: var(--font-size-2xl);
  }
}
</style>
