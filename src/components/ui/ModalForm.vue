<script setup>
import { ref } from 'vue'
import emailjs from '@emailjs/browser'

const emit = defineEmits(['close'])

/* EmailJS — замени на свои значения из личного кабинета emailjs.com */
const EMAILJS_SERVICE_ID  = 'YOUR_SERVICE_ID'
const EMAILJS_TEMPLATE_ID = 'YOUR_TEMPLATE_ID'
const EMAILJS_PUBLIC_KEY  = 'YOUR_PUBLIC_KEY'

/* Состояние формы */
const form = ref({
  name: '',
  company: '',
  phone: '',
})

const isSending = ref(false)
const sendError = ref(false)

async function handleSubmit() {
  isSending.value = true
  sendError.value = false

  try {
    await emailjs.send(
      EMAILJS_SERVICE_ID,
      EMAILJS_TEMPLATE_ID,
      {
        from_name:    form.value.name,
        company:      form.value.company,
        phone:        form.value.phone,
        to_email:     'info@ftech.group',
      },
      EMAILJS_PUBLIC_KEY
    )
    emit('close')
  } catch (err) {
    console.error('EmailJS error:', err)
    sendError.value = true
  } finally {
    isSending.value = false
  }
}

function handleBackdropClick(event) {

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
            Свяжемся с Вами в ближайшее время!
          </p>
        </div>

        <!-- Правые две трети: форма -->
        <form class="modal__form" @submit.prevent="handleSubmit" novalidate>

          <div class="modal__fields">
            <!-- Поле: Имя* -->
            <div class="modal__field">
              <label class="modal__label" for="modal-name">Имя*</label>
              <input
                id="modal-name"
                v-model="form.name"
                class="modal__input"
                type="text"
                placeholder="Иван"
                required
                autocomplete="name"
              />
            </div>

            <!-- Поле: Компания -->
            <div class="modal__field">
              <label class="modal__label" for="modal-company">Компания*</label>
              <input
                id="modal-company"
                v-model="form.company"
                class="modal__input"
                type="text"
                placeholder="Название компании»"
                autocomplete="organization"
              />
            </div>

            <!-- Поле: Телефон -->
            <div class="modal__field">
              <label class="modal__label" for="modal-phone">Телефон*</label>
              <input
                id="modal-phone"
                v-model="form.phone"
                class="modal__input"
                type="tel"
                placeholder="+7..."
                required
                autocomplete="tel"
              />
            </div>
          </div>

          <!-- Нижний блок: кнопка и текст по центру -->
          <div class="modal__form-footer">
            <button class="modal__submit" type="submit" :disabled="isSending">
              {{ isSending ? 'Отправка...' : 'Отправить' }}
            </button>
            <p v-if="sendError" class="modal__send-error">Ошибка отправки. Попробуйте ещё раз.</p>
            <div class="modal__policy">
              <span class="modal__policy-text">
                Нажимая кнопку «Отправить», Вы соглашаетесь с
                <a href="/privacy" class="modal__policy-link" target="_blank">
                  политикой обработки персональных данных
                </a>
              </span>
            </div>
          </div>

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
  width: 908px;
  height: 688px;
  max-width: 90vw;
  overflow-y: auto;

  border-radius: 12px;
  display: flex;
  flex-direction: column;
  padding: var(--spacing-2xl);

  background: #FFFFFF;
  box-shadow: 0px 0px 10px 4px #A3C3F8;

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
  align-items: stretch;
  flex: 1;
  min-height: 0;
}

/* --- Левая треть: информационный блок --- */
.modal__info {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
  padding-top: var(--spacing-2xl);

  /* ↓ Добавь padding-right или разделительную линию если нужно */
}

.modal__info-title {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 700;
  font-size: 30px;
  line-height: 30px;
  letter-spacing: -0.03em;
  color: #43359C;
}

.modal__info-text {
font-family: 'Inter', sans-serif;
font-style: normal;
font-weight: 400;
font-size: 20px;
line-height: 31px;
color: #000000;

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
    flex: 1;
  min-height: 0;
}

/* --- Нижний блок: кнопка и текст по центру --- */
.modal__form-footer {
  position: absolute;
  left: 50%;
  bottom: var(--spacing-2xl);
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
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
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 35px;
  color: #000000;
}

.modal__input {
  width: 480px;
  padding: var(--spacing-sm) var(--spacing-md);
  border-radius: 5px;

  border: 1px solid var(--color-gray-200);
  background: rgba(201, 225, 250, 0.57);
  
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 35px;
  color: #000000;

  outline: none;
  transition: border-color var(--transition-fast), box-shadow var(--transition-fast);
}

.modal__input:focus {
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px var(--color-primary-light);
}

.modal__input::placeholder {
  color: rgba(0, 0, 0, 0.36);
}

/* --- Кнопка отправки --- */
.modal__submit {
  width: 325px;
  height: 63px;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  border-radius: 37.5246px;
  background: #306AF2;
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 17.9134px;
  line-height: 43px;
  color: #FFFFFF;

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
  display: block;
}

.modal__policy-text {
  font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 20px;
  line-height: 31px;
  text-align: center;
  color: #7A7A7A;
}

.modal__send-error {
  font-size: 14px;
  color: #e53935;
  text-align: center;
}

.modal__policy-link {
    font-family: 'Inter', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 20px;
  line-height: 31px;
  text-align: center;
  color: #306AF2;
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
