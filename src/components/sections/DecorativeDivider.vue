<script setup>
defineProps({
  /* Необязательный alt-текст для изображения */
  alt: {
    type: String,
    default: '',
  },
  /* Необязательный src для реального изображения */
  imageSrc: {
    type: String,
    default: null,
  },
})
</script>

<template>
  <div class="divider" role="presentation" aria-hidden="true">
    <div class="divider__container">
      <!-- Если передан src — показываем изображение, иначе заглушка -->
      <img
        v-if="imageSrc"
        class="divider__image"
        :src="imageSrc"
        :alt="alt"
      />
    </div>
  </div>
</template>

<style scoped>
/* ==========================================================================
   DECORATIVE DIVIDER — компонент-разделитель между секциями
   Используется дважды: между Features/Solutions и между Solutions/Expertise
   ========================================================================== */

.divider {
  /* ↓ Задай высоту и background-color разделителя по дизайну */
  width: 100%;
  overflow: hidden;
}

.divider__container {
  max-width: var(--container-max);
  margin: 0 auto;
  /* ↓ Если изображение должно быть на всю ширину — убери max-width */
}

.divider__image {
  width: 100%;
  height: auto;
  display: block;
  /* ↓ При необходимости задай object-fit и height */
}

</style>
