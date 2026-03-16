<script setup>
import { ref } from 'vue'

import AppHeader from './components/layout/AppHeader.vue'
import AppFooter from './components/layout/AppFooter.vue'

import HeroSection from './components/sections/HeroSection.vue'
import FeaturesSection from './components/sections/FeaturesSection.vue'
import DecorativeDivider from './components/sections/DecorativeDivider.vue'
import SolutionsSection from './components/sections/SolutionsSection.vue'
import ExpertiseSection from './components/sections/ExpertiseSection.vue'
import TechStackSection from './components/sections/TechStackSection.vue'
import CtaSection from './components/sections/CtaSection.vue'

import ModalForm from './components/ui/ModalForm.vue'

/* Состояние модального окна */
const isModalOpen = ref(false)

function openModal() {
  isModalOpen.value = true
  document.body.style.overflow = 'hidden' /* блокируем скролл страницы */
}

function closeModal() {
  isModalOpen.value = false
  document.body.style.overflow = '' /* восстанавливаем скролл */
}
</script>

<template>
  <div class="app">

    <!-- Фиксированная шапка -->
    <AppHeader />

    <!-- Основной контент: отступ сверху на высоту шапки -->
    <main class="app__main">

      <!-- 1. Первый экран (Hero) -->
      <HeroSection />

      <!-- 2. Блок с преимуществами (5 элементов, Grid 2 колонки) -->
      <!-- 4. Наши решения (Grid 2×2) — секции соприкасаются, куб на границе -->
      <div class="sections-joint">
        <FeaturesSection />
        <div class="sections-joint__bridge" aria-hidden="true">
          <img src="/cube-divider.png" alt="" class="sections-joint__cube sections-joint__cube--first" />
          <img src="/cube-divider-2.png" alt="" class="sections-joint__cube sections-joint__cube--second" />
        </div>
        <SolutionsSection />
      </div>

      <!-- 5. Декоративный разделитель + куб на границе с экспертизой -->
      <div class="divider-joint">
        <DecorativeDivider />
        <div class="divider-joint__bridge" aria-hidden="true">
          <img src="/cube-divider-2.png" alt="" class="divider-joint__cube" />
        </div>
        <!-- 6. Экспертиза (Наши направления + картинка справа) -->
        <ExpertiseSection />
      </div>

      <!-- 7. Технологический стек — отдельная секция -->
      <TechStackSection />

      <!-- 8. CTA — карточка призыва к действию -->
      <CtaSection @open-modal="openModal" />

    </main>

    <!-- Подвал -->
    <AppFooter />

    <!-- Модальное окно — рендерится поверх всего через Teleport -->
    <Teleport to="body">
      <Transition name="modal-fade">
        <ModalForm
          v-if="isModalOpen"
          @close="closeModal"
        />
      </Transition>
    </Teleport>

  </div>
</template>

<style>
/* ==========================================================================
   ГЛОБАЛЬНЫЕ СТИЛИ APP
   (не scoped — применяются ко всей странице)
   ========================================================================== */

.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;

  /* ↓ Задай font-family и base color по дизайну */
  font-family: var(--font-sans);
  color: var(--color-text-primary);
  background-color: var(--bg-page);
}

.app__main {
  flex: 1;
}

.sections-joint {
  position: relative;
}

/* Нулевой div точно на границе двух секций */
.sections-joint__bridge {
  position: relative;
  height: 0;
  overflow: visible;
  z-index: 10;
}

.sections-joint__cube {
  position: absolute;
  top: -121px;
  width: 220px;
  height: 243px;
  object-fit: contain;
  pointer-events: none;
}

.sections-joint__cube--first {
  right: 80px;
  z-index: 1;
}

/* Второй куб правее первого, перекрытие ~10% (22px от ширины первого) */
.sections-joint__cube--second {
  right: 280px; /* = -118px */
  top: calc(-113px / 2); /* центр по границе по своей высоте */
  width: 166px;
  height: 183px;
  z-index: 2;
  }

  /* Граница DecorativeDivider / ExpertiseSection — куб слева */
.divider-joint {
  position: relative;
}

.divider-joint__bridge {
  position: relative;
  height: 0;
  overflow: visible;
  z-index: 10;
}

.divider-joint__cube {
  position: absolute;
  left: 80px;
  top: -68px; /* половина высоты 196px */
  width: 178px;
  height: 196px;
  object-fit: contain;
  pointer-events: none;
  z-index: 2;
}

/* --- Анимация появления/исчезновения модального окна --- */
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity var(--transition-base);
}

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}
</style>
