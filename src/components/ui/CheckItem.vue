<script setup>
defineProps({
  text: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <li class="check-item">
    <!-- Иконка галочки — можешь заменить на SVG-спрайт или img -->
    <span class="check-item__icon" aria-hidden="true">
      <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
        <!-- Замени путь на нужную иконку из Figma -->
        <circle cx="10" cy="10" r="10" fill="currentColor" fill-opacity="0.1"/>
        <path d="M5.5 10.5L8.5 13.5L14.5 7.5" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </span>
    <span class="check-item__text">{{ text }}</span>
  </li>
</template>

<style scoped>
/* --- CheckItem: элемент списка с галочкой слева ---
   Используется в FeaturesSection и карточках SolutionsSection */

.check-item {
  display: flex;          /* флекс: иконка слева, текст справа */
  align-items: flex-start;
  gap: var(--spacing-sm);
  /* ↓ Добавь вертикальный отступ между элементами списка */
}

.check-item__icon {
  flex-shrink: 0;         /* не сжимать иконку */
  color: var(--color-icon-check);
  /* ↓ Настрой размер иконки под дизайн */
  margin-top: 2px;        /* небольшой сдвиг для выравнивания с текстом */
}

.check-item__text {
  /* ↓ Пропиши font-size и color по дизайну */
  line-height: var(--line-height-normal);
}
</style>
