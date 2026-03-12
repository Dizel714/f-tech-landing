<script setup>
defineProps({
  label: {
    type: String,
    required: true,
  },
  /* Опциональная иконка: передавай URL или SVG-строку.
     Если не передана — иконка не рендерится */
  iconSrc: {
    type: String,
    default: null,
  },
})
</script>

<template>
  <span class="tech-chip">
    <img
      v-if="iconSrc"
      class="tech-chip__icon"
      :src="iconSrc"
      :alt="label"
      width="16"
      height="16"
    />
    <span class="tech-chip__label">{{ label }}</span>
  </span>
</template>

<style scoped>
/* --- TechChip: чип с названием технологии ---
   Используется в TechStackSection для каждого инструмента */

.tech-chip {
  display: inline-flex;   /* иконка слева, текст справа */
  align-items: center;
  gap: var(--spacing-xs);

  /* ↓ Настрой padding, цвета фона и текста по дизайну */
  padding: var(--spacing-xs) var(--spacing-md);
  border-radius: var(--radius-full);
  background-color: var(--color-primary-light);
  color: var(--color-primary);

  font-size: var(--font-size-sm);
  font-weight: var(--font-weight-medium);
  white-space: nowrap;

  /* ↓ Если нужна рамка — раскомментируй:
  border: 1px solid var(--color-primary); */
}

.tech-chip__icon {
  flex-shrink: 0;
  object-fit: contain;
  /* ↓ Подбери размер иконки под дизайн */
}

.tech-chip__label {
  /* дополнительные стили текста — font-size уже задан на .tech-chip */
}
</style>
