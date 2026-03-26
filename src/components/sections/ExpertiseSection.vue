<script setup>
/* ExpertiseSection — «Технологическая экспертиза полного цикла»
   Левая треть: подзаголовок + 8 направлений */

const directions = [
  'Интеллектуальные BPMN-платформы',
  'CRM и клиентские платформы',
  'ESB / Integration Layer',
  'API Management',
  'OCR + LLM решения для договоров',
  'AI-скоринг',
  'Case Management',
  'Интеграция legacy-систем',
]
</script>

<template>
  <section class="expertise" id="expertise">
    <div class="expertise__container">

      <!-- Главный заголовок -->
      <h2 class="expertise__heading">
        Технологическая экспертиза полного цикла
      </h2>

      <!-- Основной layout: первая треть — список направлений, остальное — стек -->
      <div class="expertise__body">

        <!-- Левая треть: список направлений -->
        <div class="expertise__directions">
          <h3 class="expertise__directions-title">Наши направления</h3>
          <ul class="expertise__directions-list">
            <li
              v-for="(dir, idx) in directions"
              :key="idx"
              class="expertise__direction-item"
            >
              <!-- Иконка стрелки вправо -->
              <span class="expertise__direction-icon" aria-hidden="true">
                <img src="/icon-arrow.svg" alt="" width="31" height="23" />
              </span>
              <span class="expertise__direction-text">{{ dir }}</span>
            </li>
          </ul>
        </div>

        <!-- Правая часть: картинка -->
        <div class="expertise__image-area">
          <img src="/expertise-visual.png" alt="Экспертиза" class="expertise__visual-img" />
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
/* ==========================================================================
   EXPERTISE SECTION — «Технологическая экспертиза полного цикла»
   ========================================================================== */

.expertise {
  /* ↓ Задай background-color и padding по дизайну */
  width: 100%;
  background-color: var(--bg-page);
  padding: var(--spacing-4xl) 0 0;
  display: flex;
  justify-content: center;
  overflow: hidden;
}

/* --- Контейнер --- */
.expertise__container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--container-padding) 0 120px;
}

/* --- Главный заголовок --- */
.expertise__heading {
  margin-bottom: var(--spacing-3xl);
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 700;
  font-size: 50px;
  line-height: 50px;
  text-align: center;
  color: #000000;
  white-space: nowrap;
}

/* --- Двухколонный layout: 1/3 + 2/3 --- */
.expertise__body {
  display: grid;
  grid-template-columns: 1fr 2fr; /* первая треть + остаток */
  gap: var(--spacing-3xl);

  /* ↓ Настрой gap по дизайну */
}

/* --- Левая колонка: направления --- */
.expertise__directions {
  padding-top: var(--spacing-4xl);
}

.expertise__directions-title {
  margin-bottom: var(--spacing-lg);
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 800;
  font-size: 30px;
  line-height: 38px;
  color: #43359C;
  white-space: nowrap;
}

/* --- Список направлений в колонку --- */
.expertise__directions-list {
  display: flex;
  flex-direction: column;
  gap: 0;
}

.expertise__direction-item {
  display: flex;
  align-items: center;
  gap: var(--spacing-xl);
}

.expertise__direction-icon {
  flex-shrink: 0;
  color: var(--color-icon-arrow);
  margin-top: 3px;
}

.expertise__direction-text {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 28px;
  line-height: 71px;
  color: #43359C;
  white-space: nowrap;
}

/* --- Правая область под картинку --- */
.expertise__image-area {
  display: flex;
  align-items: flex-end;
  justify-content: flex-end;
  padding-top: var(--spacing-4xl);
}

.expertise__visual-img {
  width: 808px;
  height: 808px;
  object-fit: contain;
  display: block;
  transform: scaleX(-1);
  margin-bottom: 0;
  vertical-align: bottom;
}

/* --- Адаптив --- */

@media (max-width: 1600px) {
  .expertise__heading {
  font-size: 44px;
  line-height: 44px;
  }

  .expertise__directions-title {
    font-size: 24px;
    line-height: 24px;
  }

  .expertise__direction-text {
    font-size: 24px;
    line-height: 58px;
  }

  .expertise__direction-icon img {
    width: 21px;
    height: 15px;
  }

  .expertise__visual-img {
  width: 500px;
  height: 585px;
  }
}

@media (max-width: 1440px) {
  .expertise__heading {
  font-size: 38px;
  line-height: 38px;
  }

  .expertise__directions-title {
    font-size: 22px;
    line-height: 28px;
  }

  .expertise__direction-text {
    font-size: 21px;
    line-height: 53px;
  }

  .expertise__direction-icon img {
    width: 19px;
    height: 13px;
  }

  .expertise__visual-img {
  width: 464px;
  height: 535px;
  }
}

@media (max-width: 1024px) {
  .expertise__container {
    padding: 0 var(--container-padding);
  }

  .expertise__body {
    grid-template-columns: 1fr;
    gap: var(--spacing-xs);
  }

  .expertise__directions {
    padding-top: var(--spacing-xl);
    padding-right: 0;
    justify-self: center;
    width: fit-content;
    max-width: 100%;
    text-align: left;
  }

  .expertise__directions-list {
    text-align: left;
  }
  
  .expertise__heading {
    font-size: 28px;
    line-height: 32px;
  }

  .expertise__directions-title {
    text-align: left;
    font-size: 19px;
    line-height: 24px;
  }

  .expertise__direction-text {
    font-size: 18px;
    line-height: 36px;
  }

  .expertise__image-area {
    align-items: center;
    justify-content: center;
    padding-top: var(--spacing-2xl);
  }

  .expertise__visual-img {
    width: 100%;
    height: auto;
    max-width: 390px;
    max-height: 450px;
  }

  .expertise__direction-icon img {
    width: 16px;
    height: 11px;
  }
}

@media (max-width: 793px) {
  .expertise__body {
    grid-template-columns: 1fr;
  }

  .expertise__heading {
    font-size: 22px;
    line-height: 25px;
    white-space: normal;
    overflow-wrap: anywhere;
    padding-inline: var(--spacing-lg);
    box-sizing: border-box;
  }

  .expertise__container {
    min-width: 0;
    padding-inline: var(--spacing-sm);
  }

  .expertise__directions-title {
    font-size: 15px;
    line-height: 19px;
  }

  .expertise__direction-text {
    font-size: 14px;
    line-height: 30px;
  }

  .expertise__image-area {
    justify-content: center;
  }

  .expertise__visual-img {
    max-width: 304px;
    max-height: 351px;
  }

  .expertise__direction-icon img {
    width: 12px;
    height: 9px;
  }
}

@media (max-width: 375px) {
  .expertise__heading {
    font-size: 20px;
    line-height: 24px;
    margin-bottom: var(--spacing-xl);
  }

  .expertise__directions-title {
    font-size: 14px;
    line-height: 18px;
  }

  .expertise__direction-text {
    font-size: 13px;
    line-height: 25px;
  }

  .expertise__direction-item {
    gap: var(--spacing-md);
  }

  .expertise__visual-img {
    max-width: 288px;
    max-height: 332px;
  }

  .expertise__direction-icon img {
    width: 12px;
    height: 8px;
  }
}
</style>