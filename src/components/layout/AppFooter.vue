<script setup>
/* AppFooter — подвал в три колонки */

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
  { id: 1, label: 'Руководство пользователя', href: '/docs/manual', icon: 'link-manual.svg' },
  { id: 2, label: 'Технологический стек', href: '#expertise', icon: 'link-stack.svg' },
  { id: 3, label: 'Форма обратной связи', href: '#cta', icon: 'link-feedback.svg' },
]
</script>

<template>
  <footer class="footer" id="footer">
    <div class="footer__container">

      <div class="footer__grid">

        <!-- Колонка 1: Логотип + юридическая информация -->
        <div class="footer__col footer__col--brand">
          <a href="/" class="footer__logo" aria-label="На главную">
            <img src="/logo-footer.svg" alt="Ф Тех" class="footer__logo-img" />
          </a>

          <address class="footer__legal">
            <p class="footer__legal-name">{{ legalInfo.name }}</p>
            <p class="footer__legal-row">ИНН: {{ legalInfo.inn }}</p>
            <p class="footer__legal-row">КПП: {{ legalInfo.kpp }}</p>
            <p class="footer__legal-row">{{ legalInfo.address }}</p>
          </address>

          <div class="footer__address-block">
            <p class="footer__legal-name">Юр.адрес:</p>
            <p class="footer__legal-row">107031, г. Москва, <br> вн.тер.г. МО Мещанский, <br> ул. Кузнецкий Мост, 21/5</p>
          </div>
        </div>

        <!-- Колонка 2: Три текстовых блока -->
        <div class="footer__col footer__col--info">
          <div
            v-for="block in infoBlocks"
            :key="block.id"
            class="footer__info-block"
          >
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
              <li
                v-for="link in docLinks"
                :key="link.id"
                class="footer__link-item"
              >
                <!-- Иконка стрелки вправо -->
                <span class="footer__link-icon" aria-hidden="true">
                  <img
                    v-if="link.icon"
                    :src="link.icon"
                    alt=""
                    class="footer__link-icon-img"
                  />
                </span>
                <a :href="link.href" class="footer__link">{{ link.label }}</a>
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
  font-size: var(--font-size-sm);
}

.footer__legal-row {
  /* ↓ Задай font-size и color по дизайну */
  font-size: var(--font-size-xs);
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
  font-family: 'Inter';
  font-style: normal;
  font-weight: 400;
  font-size: 30px;
  line-height: 40px;
  color: #306AF2;
}

.footer__info-block:nth-child(2) .footer__info-text {
  font-family: 'Inter';
  font-style: normal;
  font-weight: 700;
  font-size: 20px;
  line-height: 36px;
  color: #306AF2;
}

.footer__info-block:nth-child(3) .footer__info-title {
  font-family: 'Inter';
  font-style: normal;
  font-weight: 700;
  font-size: 20px;
  line-height: 36px;
  color: #306AF2;
}

.footer__info-block:nth-child(3) .footer__info-text {
  font-family: 'Inter';
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
  padding-left: 120px;
}

.footer__links-list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-3xl);
}

.footer__link-item {
  display: flex;             /* флекс: иконка слева, текст справа */
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
  font-family: 'Inter';
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
@media (max-width: 900px) {
  .footer__grid {
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto auto;
  }

  .footer__divider {
    display: none;
  }

  .footer__col--links {
    grid-column: 1 / -1;
  }
}

@media (max-width: 600px) {
  .footer__grid {
    grid-template-columns: 1fr;
  }
}
</style>
