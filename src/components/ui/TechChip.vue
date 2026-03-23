<script setup>
defineProps({
  label: {
    type: String,
    required: true,
  },
    sublabel: {
    type: String,
    default: null,
  },
  iconSrc: {
    type: String,
    default: null,
  },
    iconSize: {
    type: Number,
    default: 36,
  },
    iconWidth: {
    type: Number,
    default: null,
  },
  iconHeight: {
    type: Number,
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
      :width="iconWidth ?? iconSize"
      :height="iconHeight ?? iconSize"
    />
      <span class="tech-chip__label">{{ label }}<span v-if="sublabel" class="tech-chip__sublabel"> ({{ sublabel }})</span></span>
  </span>
</template>

<style scoped>
/* --- TechChip: чип с названием технологии ---
   Используется в TechStackSection для каждого инструмента */

.tech-chip {
  display: inline-flex;
  align-items: center;
  gap: var(--spacing-xs);

  background: #E5E6F4;
  border-radius: 55px;
  padding: var(--spacing-xs) var(--spacing-md);

  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 700;
  font-size: 28px;
  line-height: 35px;
  color: #43359C;
  white-space: nowrap;


}

.tech-chip__icon {
  flex-shrink: 0;
  object-fit: contain;
}

.tech-chip__label {
}

.tech-chip__sublabel {
  font-weight: 400;
}

@media (max-width: 1440px) {
  .tech-chip {
    font-size: 21px;
    line-height: 26px;
  }
}

@media (max-width: 1024px) {
  .tech-chip {
    font-size: 18px;
    line-height: 22px;
  }
}

@media (max-width: 793px) {
  .tech-chip {
    font-size: 14px;
    line-height: 18px;
  }
}

@media (max-width: 375px) {
  .tech-chip {
    font-size: 13px;
    line-height: 17px;
  }
}
</style>
