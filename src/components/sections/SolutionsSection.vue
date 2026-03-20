<script setup>
/* SolutionsSection — блок «Наши решения», Grid 2×2 из четырёх карточек */

const solutions = [
  {
    id: 1,
    title: 'Кредитный конвейер Octasoft',
    description: 'Гибкая BPMN-платформа для розничного и корпоративного кредитования',
    advantages: {
      heading: 'Что даёт:',
      items: [
        'Оркестрация кредитных процессов',
        'Интеграция риск-моделей',
        'Поддержка кредитных комитетов',
        'Быстрый вывод новых продуктов',
      ],
    },
  },
  {
    id: 2,
    title: 'Примус Финанс',
    description: 'Цифровые платформы для факторинга и управления агентской сетью',
    advantages: {
      heading: 'Возможности:',
      items: [
        'Онлайн-факторинг',
        'Контроль дебиторской задолженности',
        'Управление агентами и комиссиями',
        'Интеграция с CRM и АБС',
      ],
    },
  },
  {
    id: 3,
    title: 'Автоматизированная система для МСБ',
    description: 'Единая цифровая платформа для сквозной автоматизации работы с клиентами МСБ',
    advantages: {
      heading: 'Что решает:',
      items: [
        'Приём и обработка заявок',
        'KYC / KYB',
        'Подбор банковских продуктов',
        'Интеграция со скорингами и АБС',
        'Управление жизненным циклом клиента',
      ],
    },
  },
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
                  <img src="/icon-check-solution.svg" alt="" width="33" height="33" />
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
  width: 100%;
  background-image: url('/solutions-bg.png');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  padding: var(--spacing-4xl) 0;
  display: flex;
  justify-content: center;
}

/* --- Контейнер --- */
.solutions__container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--container-padding);
}

/* --- Заголовок секции --- */
.solutions__heading {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 700;
  font-size: 50px;
  line-height: 50px;
  text-align: center;
  margin-bottom: var(--spacing-3xl);
  color: #000000;

}

/* --- Grid 2×2 --- */
.solutions__grid {
  display: grid;
  grid-template-columns: repeat(2, 848px);
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
  width: 848px;

  padding: var(--spacing-xl);
  border-radius: var(--radius-lg);

  /* ↓ Задай background-color, border и box-shadow карточки по дизайну */
  background-color: var(--bg-card);
  box-shadow: var(--shadow-md);
}

/* Верхний ряд (карточки 1 и 2) */
.solution-card:nth-child(1),
.solution-card:nth-child(2) {
  height: 492px;
}

/* Нижний ряд (карточки 3 и 4) */
.solution-card:nth-child(3),
.solution-card:nth-child(4) {
  height: 543px;
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

  padding-left: var(--spacing-xl);

}

.solution-card__advantages-heading {
  margin-bottom: var(--spacing-sm);
  padding-left: calc(33px + var(--spacing-2xl));
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 700;
  font-size: 28px;
  line-height: 51px;
  letter-spacing: -0.05em;
  color: #000000;
}

/* --- Список преимуществ --- */
.solution-card__advantages-list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
}

/* Карточка 4 имеет на 1 пункт меньше — выравниваем заголовок по карточке 3 */
.solution-card:nth-child(4) .solution-card__advantages-list {
  padding-bottom: 51px;
}

.solution-card__advantage-item {
  display: flex;
  align-items: center;
  gap: var(--spacing-2xl);
}

.solution-card__check-icon {
  flex-shrink: 0;
  color: var(--color-icon-check);
  margin-top: 2px;
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
  .solutions__grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .solution-card {
    width: 100%;
  }

  .solution-card:nth-child(1),
  .solution-card:nth-child(2),
  .solution-card:nth-child(3),
  .solution-card:nth-child(4) {
    height: auto;
  }
}

@media (max-width: 1024px) {
  .solutions__heading {
    font-size: 36px;
  }

  .solution-card__title {
    font-size: 28px;
  }

  .solution-card__description {
    font-size: 20px;
  }

  .solution-card__advantage-text,
  .solution-card__advantages-heading {
    font-size: 20px;
    line-height: 36px;
  }
}

@media (max-width: 793px) {
  .solutions__grid {
    grid-template-columns: 1fr;
  }

  .solutions__heading {
    font-size: 28px;
  }

  .solution-card__title {
    font-size: 22px;
  }

  .solution-card__description {
    font-size: 17px;
  }

  .solution-card__advantage-text,
  .solution-card__advantages-heading {
    font-size: 17px;
    line-height: 30px;
  }
}

@media (max-width: 375px) {
  .solutions__heading {
    font-size: 22px;
  }

  .solution-card {
    padding: var(--spacing-md);
  }

  .solution-card__title {
    font-size: 18px;
    margin-bottom: var(--spacing-sm);
  }

  .solution-card__description {
    font-size: 14px;
  }

  .solution-card__advantage-text,
  .solution-card__advantages-heading {
    font-size: 14px;
    line-height: 26px;
  }

  .solution-card__advantage-item {
    gap: var(--spacing-md);
  }
}

</style>
