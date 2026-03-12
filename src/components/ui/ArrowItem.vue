<script setup>
defineProps({
  text: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <li class="arrow-item">
    <!-- Иконка стрелки вправо -->
    <span class="arrow-item__icon" aria-hidden="true">
      <svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <!-- Замени путь на SVG-иконку из Figma -->
        <path d="M3.75 9H14.25M14.25 9L9.75 4.5M14.25 9L9.75 13.5" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </span>
    <span class="arrow-item__text">{{ text }}</span>
  </li>
</template>

<style scoped>
/* --- ArrowItem: элемент списка со стрелкой вправо ---
   Используется в ExpertiseSection (список направлений) и FooterSection */

.arrow-item {
  display: flex;          /* флекс: иконка слева, текст справа */
  align-items: center;
  gap: var(--spacing-sm);
  /* ↓ Добавь вертикальный padding между элементами снаружи */
}

.arrow-item__icon {
  flex-shrink: 0;
  color: var(--color-icon-arrow);
  /* ↓ Настрой цвет и размер иконки под дизайн */
}

.arrow-item__text {
  /* ↓ Пропиши font-size и color по дизайну */
  line-height: var(--line-height-normal);
}
</style>
