<script setup>
/* AppFooter — подвал в три колонки */

const emit = defineEmits(['open-modal'])


const legalInfo = {
  name: 'ООО «Ф Тех»',
  inn: '9710125709',
  kpp: '770201001',
}

/* Вторая колонка: три блока текста */
const infoBlocks = [
  {
    id: 1,
    text: 'ПО распространяется в виде интернет-сервиса, специальные действия по установке ПО на стороне пользователя не требуются.',
  },
  {
    id: 2,
    text: 'Стоимость ПО рассчитывается индивидуально.',
  },
  {
    id: 3,
    title: 'Для определения стоимости позвоните по номеру: ',
    text: '8 989 580 09 94',
  },
]

/* Третья колонка: три ссылки с иконками */
const docLinks = [
  { id: 1, label: 'Руководство пользователя', href: '/user-manual.docx', icon: 'link-manual.svg', download: true },
  { id: 2, label: 'Технологический стек', href: '/tech-stack.docx', icon: 'link-stack.svg', download: true },
  { id: 3, label: 'Форма обратной связи', href: null, icon: 'link-feedback.svg', modal: true },
]
</script>

<template>
  <footer class="footer" id="footer">
    <div class="footer__container">

      <div class="footer__grid">

        <!-- Колонка 1: Логотип + юридическая информация -->
        <div class="footer__col footer__col--brand">
          <div class="footer__brand-logo">
            <a href="/" class="footer__logo" aria-label="На главную">
              <img src="/logo-footer.svg" alt="Ф Тех" class="footer__logo-img" />
            </a>
          </div>

          <div class="footer__brand-legal">
            <address class="footer__legal">
              <p class="footer__legal-name">{{ legalInfo.name }}</p>
              <p class="footer__legal-row">ИНН: {{ legalInfo.inn }}</p>
              <p class="footer__legal-row">КПП: {{ legalInfo.kpp }}</p>
              <p class="footer__legal-row">{{ legalInfo.address }}</p>
            </address>

            <div class="footer__address-block">
              <p class="footer__legal-name">Юр.адрес:</p>
              <p class="footer__legal-row">
                107031, город Москва, <br> ул. Рождественка, д. 5/7, <br> стр. 2, помещ. 4А/5
              </p>
            </div>
          </div>
        </div>

        <!-- Колонка 2: Три текстовых блока -->
        <div class="footer__col footer__col--info">
          <div v-for="block in infoBlocks" :key="block.id" class="footer__info-block">
            <h4 class="footer__info-title">{{ block.title }}</h4>
            <p class="footer__info-text" style="white-space: pre-line;">{{ block.text }}</p>
          </div>
        </div>

        <!-- Вертикальная разделительная линия между 2-й и 3-й колонками -->
        <div class="footer__divider" aria-hidden="true"></div>

        <!-- Колонка 3: Три ссылки с иконками стрелок -->
        <div class="footer__col footer__col--links">
          <nav aria-label="Документы">
            <ul class="footer__links-list">
              <li v-for="link in docLinks" :key="link.id" class="footer__link-item">
                <!-- Иконка стрелки вправо -->
                <span class="footer__link-icon" aria-hidden="true">
                  <img v-if="link.icon" :src="link.icon" alt="" class="footer__link-icon-img" />
                </span>
                <a v-if="!link.modal" :href="link.href" :download="link.download || null" class="footer__link">{{
                  link.label }}</a>
                <button v-else class="footer__link footer__link--btn" type="button" @click="emit('open-modal')">{{
                  link.label }}</button>
              </li>
            </ul>
          </nav>
        </div>

      </div>

      <!-- Нижняя строка: копирайт -->
      <div class="footer__bottom">
        <p class="footer__copyright">
          © {{ new Date().getFullYear() }} {{ legalInfo.name }}. Все права защищены.
        </p>
      </div>

    </div>
  </footer>
</template>

<style scoped>
/* ==========================================================================
   APP FOOTER — подвал
   ========================================================================== */

.footer {
  /* ↓ Задай background-color и padding по дизайну */
  width: 100%;
  background-color: #F5F5F5;
  padding: var(--spacing-3xl) 0 0;
  margin-bottom: 0;
  color: #306AF2;
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* --- Контейнер --- */
.footer__container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--container-padding);
}

/* --- Grid: 3 колонки + вертикальный разделитель между 2 и 3 ---
   Используем 4 колонки: col1 | col2 | divider | col3
   Ширина разделителя — 1px */
.footer__grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1px 1fr;
  gap: 0 var(--spacing-2xl);
  align-items: start;
  padding-bottom: var(--spacing-2xl);
}

/* --- Колонка 1: Бренд + юридическая информация --- */
.footer__col--brand {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
  padding-left: 140px;
}

.footer__logo {
  transition: opacity var(--transition-fast);
}

.footer__logo:hover {
  opacity: 0.8;
}

.footer__logo-img {
  width: 285px;
  height: 61px;
  object-fit: contain;
}

.footer__brand-legal {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}

.footer__legal {
  font-style: normal;
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
}

.footer__address-block {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
  width: 302px;
  height: 90px;
}

.footer__legal-name {
  /* ↓ Задай font-weight и color по дизайну */
  font-weight: var(--font-weight-semibold);
  color: #306AF2;
  font-size: 20px;
}

.footer__legal-row {
  /* ↓ Задай font-size и color по дизайну */
  font-size: 20px;
  color: #306AF2;
  line-height: var(--line-height-relaxed);
}

/* --- Колонка 2: Три текстовых блока --- */
.footer__col--info {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
  width: 560px;
  max-height: 392px;
}

.footer__info-block {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
}

.footer__info-title {
  /* ↓ Задай font-size и font-weight по дизайну */
  font-size: var(--font-size-sm);
  font-weight: var(--font-weight-semibold);
  color: #306AF2;
}

.footer__info-text {
  /* ↓ Задай font-size и color по дизайну */
  font-size: var(--font-size-xs);
  color: #306AF2;
  line-height: var(--line-height-relaxed);
}

.footer__info-block:first-child .footer__info-text {
  font-style: normal;
  font-weight: 400;
  font-size: 30px;
  line-height: 40px;
  color: #306AF2;
}

.footer__info-block:nth-child(2) .footer__info-text {
  font-style: normal;
  font-weight: 700;
  font-size: 20px;
  line-height: 36px;
  color: #306AF2;
}

.footer__info-block:nth-child(3) .footer__info-title {
  font-style: normal;
  font-weight: 700;
  font-size: 20px;
  line-height: 36px;
  color: #306AF2;
}

.footer__info-block:nth-child(3) .footer__info-text {
  font-style: normal;
  font-weight: 700;
  font-size: 26px;
  line-height: 36px;
  color: #306AF2;
}


/* --- Вертикальный разделитель 1px --- */
.footer__divider {
  width: 1px;
  align-self: stretch;
  /* ↓ Задай цвет вертикальной черты по дизайну */
  background-color: #C9E1FA;
  margin: 0 var(--spacing-md);
}

/* --- Колонка 3: Ссылки --- */
.footer__col--links {
  padding-left: var(--spacing-xl);
}

.footer__links-list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-3xl);
}

.footer__link-item {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
}

.footer__link-icon {
  flex-shrink: 0;
  width: 37px;
  height: 37px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.footer__link-icon-img {
  width: 37px;
  height: 37px;
  object-fit: contain;
}

.footer__link {
  font-style: normal;
  font-weight: 400;
  font-size: 20px;
  line-height: 32px;
  text-decoration-line: underline;
  color: #000000;
  transition: color var(--transition-fast);
}

.footer__link:hover {
  color: #615e5e;
}

.footer__link--btn {
  background: none;
  border: none;
  padding: 0;
  cursor: pointer;
  text-align: left;
}


/* --- Нижняя строка с копирайтом --- */
.footer__bottom {
  border-top: 1px solid #C9E1FA;
  padding: var(--spacing-md) 0;
  margin-top: 0;
}

.footer__copyright {
  /* ↓ Задай font-size и color по дизайну */
  font-size: var(--font-size-xs);
  color: var(--color-gray-400);
  text-align: center;
}

/* --- Адаптив --- */
@media (max-width: 1440px) {
  .footer__info-block:first-child .footer__info-text {
    font-size: 22px;
    line-height: 30px;
  }

  .footer__info-block:nth-child(2) .footer__info-text,
  .footer__info-block:nth-child(3) .footer__info-title {
    font-size: 15px;
  }

  .footer__info-block:nth-child(3) .footer__info-text {
    font-size: 20px;
  }

  .footer__legal-name,
  .footer__legal-row {
    font-size: 15px;
    line-height: 24px;
  }

  .footer__link {
    font-size: 15px;
    line-height: 24px;
  }

  .footer__logo-img {
    width: 213px;
    height: 45px;
  }

  .footer__link-icon-img {
    width: 32px;
    height: 32px;
  }

}

@media (max-width: 1439px) {
  .footer__grid {
    grid-template-columns: 1fr 2fr;
    grid-template-rows: auto auto;
    padding: 0 var(--spacing-2xl) 16px;
  }

  .footer__col--brand {
    padding-left: 0;
  }

  .footer__divider {
    display: none;
  }

  .footer__col--links {
    grid-column: 1 / -1;
    padding: var(--spacing-2xl) 0 0;
    display: flex;
    justify-content: center;
  }

  .footer__col--info {
    width: 100%;
  }

  .footer__links-list {
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    gap: var(--spacing-2xl) var(--spacing-3xl);
  }
}


@media (max-width: 1024px) {

  .footer__col--links {
    padding-left: 0;
  }

  .footer__col--info {
    width: 100%;
  }

  .footer__info-block:first-child .footer__info-text {
    font-size: 19px;
    line-height: 26px;
  }

  .footer__legal-name,
  .footer__legal-row {
    font-size: 13px;
    line-height: 20px;
  }

  .footer__link {
    font-size: 13px;
    line-height: 20px;
  }

  .footer__links-list {
    gap: var(--spacing-xl) var(--spacing-xl);
  }

  .footer__logo-img {
    width: 182px;
    height: 39px;
  }

  .footer__info-block:nth-child(2) .footer__info-text,
  .footer__info-block:nth-child(3) .footer__info-title {
    font-size: 13px;
  }

  .footer__info-block:nth-child(3) .footer__info-text {
    font-size: 17px;
  }

  .footer__link-icon-img {
    width: 27px;
    height: 27px;
  }
}

@media (max-width: 793px) {
  .footer__grid {
    grid-template-columns: 1fr 2fr;
    grid-template-rows: auto auto;
    gap: 0 var(--spacing-md);
    padding: 0 var(--spacing-md) 12px;
  }

  .footer__divider {
    display: none;
  }

  .footer__col--links {
    grid-column: 1 / -1;
    padding-left: 0;
  }

  .footer__col--brand {
    padding-left: 0;
  }

  .footer__address-block {
    width: 100%;
    height: auto;
  }

  .footer__legal-name,
  .footer__legal-row {
    font-size: 10px;
    line-height: 16px;
  }

  .footer__info-block:first-child .footer__info-text {
    font-size: 15px;
    line-height: 18px;
  }

  .footer__info-block:nth-child(2) .footer__info-text,
  .footer__info-block:nth-child(3) .footer__info-title {
    font-size: 10px;
  }

  .footer__info-block:nth-child(3) .footer__info-text {
    font-size: 13px;
    line-height: 24px;
  }

  .footer__link {
    font-size: 10px;
    line-height: 16px;
  }

  .footer__logo-img {
    width: 142px;
    height: 30px;
  }

  .footer__link-icon-img {
    width: 22px;
    height: 22px;
  }
}

@media (max-width: 610px) {

  .footer__link-icon,
  .footer__link-icon-img {
    width: 20px;
    height: 20px;
  }

  .footer__links-list {
    gap: 16px;
  }

  .footer__link-item {
    gap: 8px;
  }


}

@media (max-width: 526px) {

  .footer__link-icon,
  .footer__link-icon-img {
    width: 16px;
    height: 16px;
  }

  .footer__links-list {
    gap: 12px;
  }

  .footer__link-item {
    gap: 4px;
  }
}

/* Узкий экран: логотип → юр. блок → текстовые блоки → ссылки колонкой */
@media (max-width: 494px) {
  .footer__grid {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-areas:
      'logo'
      'legal'
      'info'
      'links';
    grid-template-rows: auto;
    gap: var(--spacing-xl);
    row-gap: var(--spacing-xl);
    padding: 0 30px 12px;
  }

  .footer__col--brand {
    display: contents;
    padding-left: 0;
  }

  .footer__brand-logo {
    grid-area: logo;
    display: flex;
    justify-content: center;
  }

  .footer__brand-legal {
    grid-area: legal;
    flex-direction: row;
    justify-content: space-between;
    gap: var(--spacing-md);
  }

  .footer__brand-legal .footer__legal {
    flex: none;
    min-width: 0;
    padding-left: var(--spacing-4xl);
    box-sizing: border-box;
    padding: 0;
  }

  .footer__brand-legal .footer__address-block {
    min-width: 0;
    width: auto;
    height: auto;
  }

  /* Симметрия для первых двух текстовых блоков */
  .footer__col--info {
    grid-area: info;
    width: 100%;
    gap: var(--spacing-md);
  }

  /* Делаем первые два блока одинаковой высоты */
  .footer__info-block:first-child,
  .footer__info-block:nth-child(2) {
    min-height: 80px;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  /* Выравниваем текст в первых двух блоках */
  .footer__info-block:first-child .footer__info-text,
  .footer__info-block:nth-child(2) .footer__info-text {
    display: flex;
    align-items: center;
    min-height: 60px;
  }

  .footer__col--links {
    grid-area: links;
    grid-column: auto;
    padding: 0;
    display: block;
    justify-content: flex-start;
  }

  .footer__links-list {
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: flex-start;
    align-items: stretch;
    gap: 20px;
  }

  .footer__info-block:first-child .footer__info-text {
    line-height: 16px;
  }

  .footer__info-block:nth-child(2) .footer__info-text,
  .footer__info-block:nth-child(3) .footer__info-title {
    line-height: 20px;
  }

  .footer__info-block:nth-child(3) .footer__info-text {
    line-height: 20px;
  }
}

@media (max-width: 375px) {
  .footer__grid {
    gap: var(--spacing-md);
    row-gap: var(--spacing-md);
    padding: 0 var(--spacing-sm);
  }

  .footer__col--brand,
  .footer__col--links {
    padding-left: 0;
  }

  .footer__address-block {
    width: 100%;
    height: auto;
  }

  .footer__logo-img {
    width: 134px;
    height: 29px;
  }

  .footer__legal-name,
  .footer__legal-row {
    font-size: 10px;
    line-height: 15px;
  }

  .footer__info-block:first-child .footer__info-text {
    font-size: 14px;
    line-height: 19px;
  }

  .footer__link {
    font-size: 10px;
    line-height: 15px;
  }

  .footer__links-list {
    gap: var(--spacing-xs);
  }

  .footer__info-block:nth-child(2) .footer__info-text,
  .footer__info-block:nth-child(3) .footer__info-title {
    font-size: 9px;
  }

  .footer__info-block:nth-child(3) .footer__info-text {
    font-size: 9px;
  }

  .footer__link-icon-img {
    width: 20px;
    height: 20px;
  }

}
</style>
