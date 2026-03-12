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
      <FeaturesSection />

      <!-- 3. Декоративный разделитель -->
      <DecorativeDivider />

      <!-- 4. Наши решения (Grid 2×2) -->
      <SolutionsSection />

      <!-- 5. Декоративный разделитель -->
      <DecorativeDivider />

      <!-- 6. Экспертиза + Технологический стек (layout 1/3 + 2/3) -->
      <ExpertiseSection>
        <!-- TechStackSection рендерится в слоте ExpertiseSection -->
        <TechStackSection />
      </ExpertiseSection>

      <!-- 7. CTA — карточка призыва к действию -->
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
  /* Нет дополнительного padding-top — каждая секция сама управляет отступами */
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
