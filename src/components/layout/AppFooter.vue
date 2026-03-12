<script setup>
/* AppFooter — подвал в три колонки */

const legalInfo = {
  name: 'ООО «Ф Тех»',
  inn: '7743123456',
  kpp: '774301001',
  address: '123456, г. Москва, ул. Новинский бульвар, д. 8, офис 301',
}

/* Вторая колонка: три блока текста */
const infoBlocks = [
  {
    id: 1,
    title: 'О компании',
    text: 'Технологический партнёр для банков и финтех-компаний. Разрабатываем автоматизированные системы с 2015 года.',
  },
  {
    id: 2,
    title: 'Контакты',
    text: 'info@ftech.ru\n+7 (495) 000-00-00',
  },
  {
    id: 3,
    title: 'Режим работы',
    text: 'Пн–Пт: 09:00–18:00 МСК',
  },
]

/* Третья колонка: три ссылки с иконками */
const docLinks = [
  { id: 1, label: 'Руководство пользователя', href: '/docs/manual' },
  { id: 2, label: 'Технологический стек', href: '#expertise' },
  { id: 3, label: 'Форма обратной связи', href: '#cta' },
]
</script>

<template>
  <footer class="footer" id="footer">
    <div class="footer__container">

      <div class="footer__grid">

        <!-- Колонка 1: Логотип + юридическая информация -->
        <div class="footer__col footer__col--brand">
          <!-- Логотип — замени на SVG из Figma -->
          <a href="/" class="footer__logo" aria-label="На главную">
            <span class="footer__logo-icon" aria-hidden="true">
              <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
                <rect width="28" height="28" rx="7" fill="currentColor" fill-opacity="0.15"/>
                <text x="50%" y="55%" dominant-baseline="middle" text-anchor="middle"
                      font-size="12" font-weight="700" fill="currentColor">ФТ</text>
              </svg>
            </span>
            <span class="footer__logo-text">Ф Тех</span>
          </a>

          <address class="footer__legal">
            <p class="footer__legal-name">{{ legalInfo.name }}</p>
            <p class="footer__legal-row">ИНН: {{ legalInfo.inn }}</p>
            <p class="footer__legal-row">КПП: {{ legalInfo.kpp }}</p>
            <p class="footer__legal-row">{{ legalInfo.address }}</p>
          </address>
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
                  <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
                    <path d="M3.33 8H12.67M12.67 8L8.67 4M12.67 8L8.67 12"
                      stroke="currentColor" stroke-width="1.5"
                      stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
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
  background-color: var(--color-gray-800);
  padding: var(--spacing-3xl) 0 0;
  color: var(--color-gray-200);
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
}

.footer__logo {
  display: inline-flex;
  align-items: center;
  gap: var(--spacing-sm);
  /* ↓ Задай цвет логотипа */
  color: var(--color-primary);
  transition: opacity var(--transition-fast);
}

.footer__logo:hover {
  opacity: 0.8;
}

.footer__logo-text {
  font-size: var(--font-size-lg);
  font-weight: var(--font-weight-bold);
  color: var(--color-white);
}

.footer__legal {
  font-style: normal;
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
}

.footer__legal-name {
  /* ↓ Задай font-weight и color по дизайну */
  font-weight: var(--font-weight-semibold);
  color: var(--color-white);
  font-size: var(--font-size-sm);
}

.footer__legal-row {
  /* ↓ Задай font-size и color по дизайну */
  font-size: var(--font-size-xs);
  color: var(--color-gray-400);
  line-height: var(--line-height-relaxed);
}

/* --- Колонка 2: Три текстовых блока --- */
.footer__col--info {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
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
  color: var(--color-white);
}

.footer__info-text {
  /* ↓ Задай font-size и color по дизайну */
  font-size: var(--font-size-xs);
  color: var(--color-gray-400);
  line-height: var(--line-height-relaxed);
}

/* --- Вертикальный разделитель 1px --- */
.footer__divider {
  width: 1px;
  align-self: stretch;
  /* ↓ Задай цвет вертикальной черты по дизайну */
  background-color: var(--color-gray-600);
  margin: 0 var(--spacing-md);
}

/* --- Колонка 3: Ссылки --- */
.footer__col--links {
  /* Флекс-колонка ссылок задаётся через список */
}

.footer__links-list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.footer__link-item {
  display: flex;             /* флекс: иконка слева, текст справа */
  align-items: center;
  gap: var(--spacing-sm);
}

.footer__link-icon {
  flex-shrink: 0;
  color: var(--color-primary);
}

.footer__link {
  /* ↓ Задай font-size и hover-эффект по дизайну */
  font-size: var(--font-size-sm);
  color: var(--color-gray-200);
  transition: color var(--transition-fast);
}

.footer__link:hover {
  color: var(--color-white);
}

/* --- Нижняя строка с копирайтом --- */
.footer__bottom {
  border-top: 1px solid var(--color-gray-600);
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
