<script setup>
import TechChip from '../ui/TechChip.vue'

/* Технологический стек по направлениям.
   iconSrc: замени на пути к реальным иконкам (например /icons/react.svg) */
const techStack = [
  {
    id: 'backend',
    label: 'Backend:',
    technologies: [
      { name: 'C#', iconSrc: null },
      { name: '.NET 7-9', iconSrc: null },
      { name: 'Java', sublabel: 'Spring Boot', iconSrc: null },
      { name: 'Python', iconSrc: null },
      { name: 'Go', iconSrc: null },
    ],
  },
  {
    id: 'frontend',
    label: 'Frontend:',
    technologies: [
      { name: 'Angular', iconSrc: '/angular.svg' },
      { name: 'React', iconSrc: '/react.svg' },
    ],
  },
  {
    id: 'db',
    label: 'БД:',
    technologies: [
      { name: 'PostgreSQL', iconSrc: '/postgresql.svg' },
    ],
  },
  {
    id: 'monitoring',
    label: 'Мониторинг:',
    technologies: [
      { name: 'Prometheus', iconSrc: '/prometheus.svg' },
      { name: 'Grafana', iconSrc: '/grafana.svg' },
    ],
  },
  {
    id: 'devops',
    label: 'DevOps',
    technologies: [
      { name: null, iconSrc: '/docker.svg', iconWidth: 114, iconHeight: 29 },
      { name: 'CI/CD', sublabel: 'GitHub, GitLab, Jenkins', iconSrc: null },
    ],
  },
]
</script>

<template>
  <section class="tech-stack" id="tech-stack">
    <img src="/techstack-visual.png" alt="" class="tech-stack__visual" />
    <div class="tech-stack__container">
      <h2 class="tech-stack__heading">Технологический стек:</h2>

      <ul class="tech-stack__list">
        <li
          v-for="category in techStack"
          :key="category.id"
          class="tech-stack__row"
        >
          <!-- Название направления -->
          <span class="tech-stack__category">{{ category.label }}</span>

          <!-- Строка с чипсами — flex-row -->
          <div class="tech-stack__chips">
          <TechChip
            v-for="tech in category.technologies"
            :key="tech.name"
            :label="tech.name"
            :sublabel="tech.sublabel"
            :icon-src="tech.iconSrc"
            :icon-size="tech.iconSize ?? 36"
            :icon-width="tech.iconWidth ?? null"
            :icon-height="tech.iconHeight ?? null"
          />
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>
/* ==========================================================================
   TECH STACK SECTION — правая часть ExpertiseSection
   ========================================================================== */

.tech-stack {
  position: relative;
  width: 100%;
  background-color: #F5F5F5;
  padding: var(--spacing-4xl) 0;
  display: flex;
  justify-content: center;
  overflow: hidden;
}

.tech-stack__visual {
  position: absolute;
  bottom: 0;
  right: 37%;
  width: 338px;
  height: 338px;
  object-fit: contain;
}

.tech-stack__container {
  width: 100%;
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--container-padding);
  padding-left: 3%;
}

/* --- Подзаголовок --- */
.tech-stack__heading {
  margin-bottom: var(--spacing-3xl);
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 800;
  font-size: 30px;
  line-height: 38px;
  color: #43359C;
}

/* --- Список направлений в колонку --- */
.tech-stack__list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

/* --- Одна строка: название + чипсы --- */
.tech-stack__row {
  display: flex;
  align-items: center;
  gap: var(--spacing-lg);

  /* ↓ Если нужно визуально разделять строки — добавь padding-bottom и border-bottom */
}

.tech-stack__category {
  flex: 0 0 150px;
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 28px;
  line-height: 70px;
  color: #43359C;
}

/* --- Строка чипсов — flex-row с переносом --- */
.tech-stack__chips {
  display: flex;
  flex-wrap: wrap;           /* перенос на новую строку если не влезают */
  gap: var(--spacing-sm);    /* ↓ Настрой расстояние между чипсами */
  flex: 1;
}

/* --- Адаптив --- */
@media (max-width: 600px) {
  .tech-stack__row {
    flex-direction: column;
    align-items: flex-start;
  }

  .tech-stack__category {
    flex: none;
  }
}
</style>
