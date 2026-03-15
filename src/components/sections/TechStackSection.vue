<script setup>
import TechChip from '../ui/TechChip.vue'

/* Технологический стек по направлениям.
   iconSrc: замени на пути к реальным иконкам (например /icons/react.svg) */
const techStack = [
  {
    id: 'backend',
    label: 'Backend',
    technologies: [
      { name: 'Java', iconSrc: null },
      { name: 'Spring Boot', iconSrc: null },
      { name: 'Python', iconSrc: null },
      { name: 'Go', iconSrc: null },
      { name: 'Node.js', iconSrc: null },
    ],
  },
  {
    id: 'frontend',
    label: 'Frontend',
    technologies: [
      { name: 'Vue', iconSrc: null },
      { name: 'Angular', iconSrc: null },
      { name: 'React', iconSrc: null },
      { name: 'TypeScript', iconSrc: null },
    ],
  },
  {
    id: 'db',
    label: 'БД',
    technologies: [
      { name: 'PostgreSQL', iconSrc: null },
      { name: 'MongoDB', iconSrc: null },
      { name: 'Redis', iconSrc: null },
      { name: 'Elasticsearch', iconSrc: null },
    ],
  },
  {
    id: 'monitoring',
    label: 'Мониторинг',
    technologies: [
      { name: 'Prometheus', iconSrc: null },
      { name: 'Grafana', iconSrc: null },
      { name: 'Kibana', iconSrc: null },
    ],
  },
  {
    id: 'devops',
    label: 'DevOps',
    technologies: [
      { name: 'Docker', iconSrc: null },
      { name: 'Kubernetes', iconSrc: null },
      { name: 'GitLab CI', iconSrc: null },
      { name: 'Terraform', iconSrc: null },
      { name: 'Ansible', iconSrc: null },
    ],
  },
]
</script>

<template>

  <section class="tech-stack" id="tech-stack">
    <div class="tech-stack__container">
      <h2 class="tech-stack__heading">Технологический стек</h2>

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
              :icon-src="tech.iconSrc"
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
  width: 100%;
  background-color: var(--bg-page);
  padding: var(--spacing-4xl) 0;
  display: flex;
  justify-content: center;
}

.tech-stack__container {
  width: 100%;
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--container-padding);
}

/* --- Подзаголовок --- */
.tech-stack__heading {
  margin-bottom: var(--spacing-xl);
  /* ↓ Задай font-size, font-weight и color по дизайну */
  font-size: var(--font-size-lg);
  font-weight: var(--font-weight-semibold);
  color: var(--color-text-primary);
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
  /* Фиксированная ширина для выравнивания колонки */
  flex: 0 0 100px;

  /* ↓ Задай font-size, font-weight и color по дизайну */
  font-size: var(--font-size-sm);
  font-weight: var(--font-weight-semibold);
  color: var(--color-text-secondary);
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
