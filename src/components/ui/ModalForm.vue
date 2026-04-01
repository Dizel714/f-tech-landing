<script setup>
import { ref } from 'vue'

const emit = defineEmits(['close'])

const YC_FUNCTION_URL = 'https://functions.yandexcloud.net/d4eojpdddb0saav6rfo2'

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
    const response = await fetch(YC_FUNCTION_URL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        name: form.value.name,
        company: form.value.company,
        phone: form.value.phone,
      }),
    })

    if (!response.ok) {
      throw new Error(`Ошибка сервера: ${response.status}`)
    }

    // Если всё ок, закрываем модалку
    emit('close')

  } catch (err) {
    console.error('Ошибка при отправке формы:', err)
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
  <div class="modal-overlay" role="dialog" aria-modal="true" aria-labelledby="modal-title" @click="handleBackdropClick">
    <div class="modal">

      <!-- Кнопка закрытия -->
      <button class="modal__close" type="button" aria-label="Закрыть" @click="$emit('close')">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
          <path d="M15 5L5 15M5 5L15 15" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />
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
              <input id="modal-name" v-model="form.name" class="modal__input" type="text" placeholder="Иван" required
                autocomplete="name" />
            </div>

            <!-- Поле: Компания -->
            <div class="modal__field">
              <label class="modal__label" for="modal-company">Компания*</label>
              <input id="modal-company" v-model="form.company" class="modal__input" type="text"
                placeholder="Название компании»" autocomplete="organization" />
            </div>

            <!-- Поле: Телефон -->
            <div class="modal__field">
              <label class="modal__label" for="modal-phone">Телефон*</label>
              <input id="modal-phone" v-model="form.phone" class="modal__input" type="tel" placeholder="+7..." required
                autocomplete="tel" />
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
                                <a
                  href="/privacy-policy.docx"
                  class="modal__policy-link"
                  download="Политика в области ПНд.docx"
                >
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
  inset: 0;
  /* top/right/bottom/left: 0 */
  z-index: 200;

  display: flex;
  align-items: center;
  justify-content: center;

  /* ↓ Задай цвет затемнения фона по дизайну */
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(2px);
}

/* --- Контейнер модального окна (размеры по макету Figma) --- */
.modal {
  position: relative;
  /* 1920: 908×688 */
  width: 908px;
  height: 688px;
  max-width: min(908px, calc(100vw - 32px));
  max-height: min(688px, calc(100vh - 32px));
  overflow-y: auto;

  border-radius: 12px;
  display: flex;
  flex-direction: column;
  padding: var(--spacing-2xl);

  background: #FFFFFF;
  box-shadow: 0px 0px 10px 4px #A3C3F8;

  margin: var(--spacing-md);
}

@media (max-width: 1440px) {
  .modal {
    /* 1440: 681×516 */
    width: 681px;
    height: 516px;
    max-width: min(681px, calc(100vw - 32px));
    max-height: min(516px, calc(100vh - 32px));
    padding: var(--spacing-xl);
  }
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
  width: 100%;
  max-width: 480px;
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
  font-size: 18px;
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
  font-family: 'Inter', sans-serif;
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

/* --- Адаптив (размеры окна по макету) --- */
@media (max-width: 1440px) {
  .modal__info-title {
    font-size: 22px;
    line-height: 22px;
  }

  .modal__info-text {
    font-size: 15px;
    line-height: 23px;
  }

    .modal__label {
    font-size: 14px;
    line-height: 26px;
  }

    .modal__submit {
    width: 243px;
    height: 47px;
    font-size: 13px;
    line-height: 32px;
  }

  .modal__policy-text,
  .modal__policy-link {
    font-size: 15px;
    line-height: 23px;
  }

  /* 1440: поля 359×37 */
  .modal__input {
    width: 359px;
    max-width: 100%;
    height: 37px;
    padding: 0 var(--spacing-sm);
    font-size: 15px;
    line-height: 37px;
  }
}

@media (max-width: 1024px) {
  .modal {
    /* 1024: 484×367 */
    width: 484px;
    height: 367px;
    max-width: min(484px, calc(100vw - 32px));
    max-height: min(367px, calc(100vh - 32px));
    padding: var(--spacing-md);
  }

  .modal__body {
    gap: var(--spacing-md);
  }

  .modal__info {
    padding-top: var(--spacing-sm);
  }

  .modal__info-title {
    font-size: 16px;
    line-height: 16px;
  }

  .modal__info-text {
    font-size: 11px;
    line-height: 17px;
  }

  .modal__label {
    font-size: 10px;
    line-height: 19px;
  }

 /* 1024: поля 255×26 */
  .modal__input {
    width: 255px;
    max-width: 100%;
    height: 26px;
    padding: 0 8px;
    font-size: 15px;
    line-height: 26px;
  }

  /* футер остаётся position:absolute от .modal — кнопка по центру окна, не колонки формы */
  .modal__form-footer {
    left: var(--spacing-md);
    right: var(--spacing-md);
    transform: none;
    bottom: var(--spacing-md);
    gap: var(--spacing-xs);
    width: auto;
    max-width: none;
    /* блок текста под кнопкой — на всю ширину между боковыми padding модалки */
  }

  .modal__policy {
    padding: 0 var(--spacing-2xl);
    margin: 0;
    width: 100%;
    max-width: 100%;
    text-align: center;
  }

  .modal__submit {
    width: 173px;
    height: 33px;
    /* 1024 */
    font-size: 10px;
    line-height: 23px;
  }

  .modal__policy-text,
  .modal__policy-link {
    font-size: 11px;
    line-height: 17px;
    text-align: center;
  }
}

@media (max-width: 793px) {
  .modal {
    /* 793: 378×286 */
    width: 378px;
    height: 286px;
    max-width: min(378px, calc(100vw - 32px));
    max-height: min(286px, calc(100vh - 32px));
    padding: var(--spacing-sm);
  }

  .modal__body {
    gap: var(--spacing-sm);
  }

  .modal__info {
    padding-top: var(--spacing-sm);
  }

  .modal__info-title {
    font-size: 12px;
    line-height: 12px;
  }

  .modal__info-text {
    font-size: 12px;
    line-height: 13px;
  }

  .modal__form {
    padding-top: 0;
    gap: var(--spacing-sm);
  }

  .modal__fields {
    gap: var(--spacing-sm);
  }

  .modal__form-footer {
    bottom: var(--spacing-sm);
    gap: var(--spacing-xs);
  }

  .modal__label {
    font-size: 8px;
    line-height: 15px;
  }

  .modal__send-error {
  font-size: 11px;
  }

  /* 793: поля 200×21 */
  .modal__input {
    width: 200px;
    max-width: 100%;
    height: 21px;
    padding: 0 6px;
    font-size: 13px;
    line-height: 21px;
  }

  .modal__submit {
    width: 135px;
    height: 26px;
    font-size: 7px;
    line-height: 18px;
  }

  .modal__policy-text,
  .modal__policy-link {
    font-size: 8px;
    line-height: 13px;
  }
}

@media (max-width: 500px) {
  .modal {
    /* 375: 241×326 */
    width: 340px;
    height: 385px;
    max-width: min(340px, calc(100vw - 24px));
    max-height: min(385px, calc(100vh - 24px));
    padding: var(--spacing-3xl);
    border-radius: 10px;
  }

  .modal__policy {
    padding: 0 var(--spacing-xs);
  }

  .modal__body {
    grid-template-columns: 1fr;
    gap: var(--spacing-xs);
  }

  .modal__info-title {
    font-size: 12px;
    line-height: 12px;
  }

  .modal__info-text {
    font-size: 12px;
    line-height: 12px;
  }

  .modal__label {
    font-size: 7px;
    line-height: 14px;
  }

  /* кнопка и политика — в потоке под полями, без наложения */
  .modal__form-footer {
    position: static;
    left: auto;
    right: auto;
    bottom: auto;
    transform: none;
    width: 100%;
    max-width: 100%;
    margin-top: var(--spacing-sm);
    gap: var(--spacing-xs);
  }

  .modal__form {
    gap: var(--spacing-sm);
    min-height: 0;
  }

  .modal__fields {
    flex: 0 0 auto;
  }

  /* 375: поля 188×20 */
  .modal__input {
    width: 220px;
    max-width: 100%;
    height: 20px;
    padding: 0 6px;
    font-size: 12px;
    line-height: 20px;
  }

  .modal__submit {
    width: 158px;
    height: 25px;
    font-size: 7px;
    line-height: 17px;
  }

  .modal__policy-text,
  .modal__policy-link {
    font-size: 8px;
    line-height: 12px;
  }

  .modal__send-error {
  font-size: 10px;
  }
}

@media (max-width: 375px) {
  .modal {
    /* 375: 241×326 */
    width: 241px;
    height: 326px;
    max-width: min(241px, calc(100vw - 24px));
    max-height: min(326px, calc(100vh - 24px));
    padding: var(--spacing-lg);
    border-radius: 10px;
  }

  .modal__policy {
    padding: 0 var(--spacing-xs);
  }

  .modal__body {
    grid-template-columns: 1fr;
    gap: var(--spacing-xs);
  }

  .modal__info-title {
    font-size: 12px;
    line-height: 12px;
  }

  .modal__info-text {
    font-size: 12px;
    line-height: 12px;
  }

  .modal__label {
    font-size: 7px;
    line-height: 14px;
  }

  /* кнопка и политика — в потоке под полями, без наложения */
  .modal__form-footer {
    position: static;
    left: auto;
    right: auto;
    bottom: auto;
    transform: none;
    width: 100%;
    max-width: 100%;
    margin-top: var(--spacing-sm);
    gap: var(--spacing-xs);
  }

  .modal__form {
    gap: var(--spacing-sm);
    min-height: 0;
  }

  .modal__fields {
    flex: 0 0 auto;
  }

  /* 375: поля 188×20 */
  .modal__input {
    width: 188px;
    max-width: 100%;
    height: 20px;
    padding: 0 6px;
    font-size: 12px;
    line-height: 20px;
  }

  .modal__submit {
    width: 128px;
    height: 25px;
    font-size: 7px;
    line-height: 17px;
  }

  .modal__policy-text,
  .modal__policy-link {
    font-size: 8px;
    line-height: 12px;
  }
}
</style>
