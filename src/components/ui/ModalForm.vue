<script setup>
import { ref } from 'vue'

const emit = defineEmits(['close'])

/* Состояние формы */
const form = ref({
  name: '',
  company: '',
  phone: '',
})

/* Флаг согласия с политикой */
const agreed = ref(false)

function handleSubmit() {
  if (!agreed.value) return
  /* ↓ Здесь добавь логику отправки формы (fetch / axios) */
  console.log('Form submitted:', form.value)
  emit('close')
}

function handleBackdropClick(event) {
  /* Закрываем модалку при клике на оверлей (не на контент) */
  if (event.target === event.currentTarget) {
    emit('close')
  }
}
</script>

<template>
  <!-- Оверлей (backdrop) -->
  <div
    class="modal-overlay"
    role="dialog"
    aria-modal="true"
    aria-labelledby="modal-title"
    @click="handleBackdropClick"
  >
    <div class="modal">

      <!-- Кнопка закрытия -->
      <button class="modal__close" type="button" aria-label="Закрыть" @click="$emit('close')">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
          <path d="M15 5L5 15M5 5L15 15" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"/>
        </svg>
      </button>

      <!-- Двухколонный layout: 1/3 (инфо) + 2/3 (форма) -->
      <div class="modal__body">

        <!-- Левая треть: заголовок и подпись -->
        <div class="modal__info">
          <h2 class="modal__info-title" id="modal-title">Обратная связь</h2>
          <p class="modal__info-text">
            Свяжемся с вами в ближайшее время и подберём оптимальное решение под ваши задачи
          </p>
        </div>

        <!-- Правые две трети: форма -->
        <form class="modal__form" @submit.prevent="handleSubmit" novalidate>

          <div class="modal__fields">
            <!-- Поле: Имя -->
            <div class="modal__field">
              <label class="modal__label" for="modal-name">Имя</label>
              <input
                id="modal-name"
                v-model="form.name"
                class="modal__input"
                type="text"
                placeholder="Иван Иванов"
                required
                autocomplete="name"
              />
            </div>

            <!-- Поле: Компания -->
            <div class="modal__field">
              <label class="modal__label" for="modal-company">Компания</label>
              <input
                id="modal-company"
                v-model="form.company"
                class="modal__input"
                type="text"
                placeholder="ООО «Финтех»"
                autocomplete="organization"
              />
            </div>

            <!-- Поле: Телефон -->
            <div class="modal__field">
              <label class="modal__label" for="modal-phone">Телефон</label>
              <input
                id="modal-phone"
                v-model="form.phone"
                class="modal__input"
                type="tel"
                placeholder="+7 (999) 000-00-00"
                required
                autocomplete="tel"
              />
            </div>
          </div>

          <!-- Кнопка отправки -->
          <button
            class="modal__submit"
            type="submit"
            :disabled="!agreed"
          >
            Отправить
          </button>

          <!-- Согласие с политикой -->
          <label class="modal__policy">
            <input
              v-model="agreed"
              class="modal__policy-checkbox"
              type="checkbox"
            />
            <span class="modal__policy-text">
              Нажимая кнопку «Отправить», вы соглашаетесь с
              <a href="/privacy" class="modal__policy-link" target="_blank">
                политикой обработки персональных данных
              </a>
            </span>
          </label>

        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* ==========================================================================
   MODAL FORM — модальное окно с формой обратной связи
   ========================================================================== */

/* --- Оверлей (backdrop) --- */
.modal-overlay {
  position: fixed;
  inset: 0;                  /* top/right/bottom/left: 0 */
  z-index: 200;

  display: flex;
  align-items: center;
  justify-content: center;

  /* ↓ Задай цвет затемнения фона по дизайну */
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(2px);
}

/* --- Контейнер модального окна --- */
.modal {
  position: relative;
  width: 100%;
  max-width: 800px;
  max-height: 90vh;
  overflow-y: auto;

  border-radius: var(--radius-xl);
  padding: var(--spacing-2xl);

  /* ↓ Задай background-color и box-shadow по дизайну */
  background-color: var(--bg-card);
  box-shadow: var(--shadow-lg);

  margin: var(--spacing-md);
}

/* --- Кнопка закрытия --- */
.modal__close {
  position: absolute;
  top: var(--spacing-md);
  right: var(--spacing-md);

  display: flex;
  align-items: center;
  justify-content: center;
  padding: var(--spacing-xs);
  border-radius: var(--radius-sm);

  /* ↓ Задай цвет иконки и hover-эффект по дизайну */
  color: var(--color-gray-400);
  transition: color var(--transition-fast), background-color var(--transition-fast);
}

.modal__close:hover {
  color: var(--color-text-primary);
  background-color: var(--color-gray-100);
}

/* --- Двухколонный layout: 1/3 + 2/3 --- */
.modal__body {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: var(--spacing-2xl);
  align-items: start;

  /* ↓ Настрой gap по дизайну */
}

/* --- Левая треть: информационный блок --- */
.modal__info {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);

  /* ↓ Добавь padding-right или разделительную линию если нужно */
}

.modal__info-title {
  /* ↓ Задай font-size, font-weight и color по дизайну */
  font-size: var(--font-size-xl);
  font-weight: var(--font-weight-bold);
  color: var(--color-text-primary);
  line-height: var(--line-height-tight);
}

.modal__info-text {
  /* ↓ Задай font-size и color по дизайну */
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
  line-height: var(--line-height-relaxed);
}

/* --- Правые две трети: форма --- */
.modal__form {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}

/* --- Список полей в столбец --- */
.modal__fields {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

/* --- Одно поле: label + input --- */
.modal__field {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
}

.modal__label {
  /* ↓ Задай font-size, font-weight и color по дизайну */
  font-size: var(--font-size-sm);
  font-weight: var(--font-weight-medium);
  color: var(--color-text-secondary);
}

.modal__input {
  width: 100%;
  padding: var(--spacing-sm) var(--spacing-md);
  border-radius: var(--radius-md);

  /* ↓ Задай border, background-color и цвет placeholder по дизайну */
  border: 1px solid var(--color-gray-200);
  background-color: var(--color-gray-50);
  color: var(--color-text-primary);

  font-size: var(--font-size-base);
  outline: none;
  transition: border-color var(--transition-fast), box-shadow var(--transition-fast);
}

.modal__input:focus {
  /* ↓ Задай стиль фокуса (border-color, box-shadow) по дизайну */
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px var(--color-primary-light);
}

.modal__input::placeholder {
  color: var(--color-gray-400);
}

/* --- Кнопка отправки --- */
.modal__submit {
  padding: var(--spacing-md) var(--spacing-xl);
  border-radius: var(--radius-md);

  /* ↓ Задай цвет фона и hover-эффект по дизайну */
  background-color: var(--color-primary);
  color: var(--color-white);
  font-size: var(--font-size-base);
  font-weight: var(--font-weight-semibold);

  align-self: flex-start;
  transition: background-color var(--transition-fast);
}

.modal__submit:hover:not(:disabled) {
  background-color: var(--color-primary-dark);
}

.modal__submit:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

/* --- Политика конфиденциальности --- */
.modal__policy {
  display: flex;
  align-items: flex-start;
  gap: var(--spacing-sm);
  cursor: pointer;
}

.modal__policy-checkbox {
  flex-shrink: 0;
  margin-top: 3px;
  cursor: pointer;
  accent-color: var(--color-primary);
  /* ↓ Задай размер чекбокса */
  width: 16px;
  height: 16px;
}

.modal__policy-text {
  /* ↓ Задай font-size и color по дизайну — это мелкий текст */
  font-size: var(--font-size-xs);
  color: var(--color-text-muted);
  line-height: var(--line-height-relaxed);
}

.modal__policy-link {
  color: var(--color-primary);
  text-decoration: underline;
}

/* --- Адаптив --- */
@media (max-width: 640px) {
  .modal__body {
    grid-template-columns: 1fr;
  }

  .modal {
    padding: var(--spacing-lg);
  }
}
</style>
