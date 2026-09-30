---
title: Лекции ПИ
---
---

Официальное расписание на [cfuv.ru](https://cfuv.ru): **ПИ-б-о-262** · **ПИ-б-о-261**

<!-- CSS стили расписания -->
<style>
  /* Переключатели недель */
  .week-toggle {
    display: flex;
    gap: 10px;
    margin: 1.2rem 0;
  }

  .week-btn {
    background: var(--lightbg);
    color: var(--gray);
    border: 1px solid var(--lightgray);
    padding: 8px 18px;
    border-radius: 6px;
    cursor: pointer;
    font-weight: 600;
    font-size: 0.9rem;
    transition: all 0.2s ease;
  }

  .week-btn:hover {
    border-color: var(--secondary);
    color: var(--secondary);
  }

  .week-btn.active {
    background: var(--secondary);
    color: var(--bg);
    border-color: var(--secondary);
  }

  /* Контейнер сетки дней */
  .week-content {
    display: none;
  }

  .week-content.active {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 12px;
  }

  /* Колонки дней */
  .day-column {
    background-color: var(--lightbg);
    border: 1px solid var(--lightgray);
    border-radius: 8px;
    padding: 10px;
    display: flex;
    flex-direction: column;
  }

  .day-header {
    font-weight: bold;
    font-size: 1rem;
    color: var(--secondary);
    border-bottom: 2px solid var(--tertiary);
    padding-bottom: 6px;
    margin-bottom: 10px;
    text-align: center;
  }

  /* Карточки пар */
  .lesson-card {
    background-color: var(--highlight);
    border-left: 3px solid var(--secondary);
    border-radius: 4px;
    padding: 6px 8px;
    margin-bottom: 8px;
  }

  .lesson-card:last-child {
    margin-bottom: 0;
  }

  .lesson-time {
    font-size: 0.8rem;
    font-weight: 700;
    color: var(--tertiary);
    margin-bottom: 2px;
  }

  .lesson-type {
    font-size: 0.7rem;
    font-weight: 600;
    text-transform: uppercase;
    color: var(--gray);
    margin-left: 4px;
  }

  .lesson-name {
    font-size: 0.85rem;
    line-height: 1.25;
    color: var(--dark);
    margin-bottom: 4px;
  }

  .lesson-room {
    font-size: 0.75rem;
    display: inline-block;
    background-color: var(--lightgray);
    color: var(--gray);
    padding: 1px 5px;
    border-radius: 3px;
    font-family: monospace;
  }

  .no-lessons {
    font-size: 0.85rem;
    color: var(--gray);
    text-align: center;
    margin: auto 0;
    padding: 20px 0;
  }
</style>

<!-- Кнопки переключения -->
<div class="week-toggle">
  <button class="week-btn active" onclick="switchWeek('week-a', this)">Неделя А</button>
  <button class="week-btn" onclick="switchWeek('week-b', this)">Неделя Б</button>
</div>

<!-- ================= НЕДЕЛЯ А ================= -->
<div id="week-a" class="week-content active">
  <div class="day-column">
    <div class="day-header">Пн</div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">История России</div>
      <span class="lesson-room">323А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Русский язык как государственный</div>
      <span class="lesson-room">323А</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Вт</div>
    <div class="lesson-card">
      <div class="lesson-time">8:00 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Проектная деятельность</div>
      <span class="lesson-room">315А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">9:50 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <span class="lesson-room">302А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Высшая математика</div>
      <span class="lesson-room">323А</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Ср</div>
    <div class="lesson-card">
      <div class="lesson-time">8:00 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык</div>
      <span class="lesson-room">531Б/525Б</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">9:50 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Высшая математика</div>
      <span class="lesson-room">211А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">История России</div>
      <span class="lesson-room">302В</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Чт</div>
    <div class="lesson-card">
      <div class="lesson-time">9:50 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Физическая культура</div>
      <span class="lesson-room">спортзал</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Русский язык как государственный</div>
      <span class="lesson-room">412В</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Пт</div>
    <div class="lesson-card">
      <div class="lesson-time">15:00 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <span class="lesson-room">117А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">16:40 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования</div>
      <span class="lesson-room">119А</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Сб</div>
    <div class="no-lessons">Пар нет</div>
  </div>
</div>

<!-- ================= НЕДЕЛЯ Б ================= -->
<div id="week-b" class="week-content">
  <div class="day-column">
    <div class="day-header">Пн</div>
    <div class="lesson-card">
      <div class="lesson-time">11:30</div>
      <div class="lesson-name">История России</div>
      <span class="lesson-room">ОК-322А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20</div>
      <div class="lesson-name">Информатика и основы программирования</div>
      <span class="lesson-room">ОК-322А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">15:00</div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных</div>
      <span class="lesson-room">ОК-323А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">16:40</div>
      <div class="lesson-name">Иностранный язык п2</div>
      <span class="lesson-room">ПЗ-531Б</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Вт</div>
    <div class="lesson-card">
      <div class="lesson-time">8:00</div>
      <div class="lesson-name">Проектная деятельность</div>
      <span class="lesson-room">ПЗ-3184</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">9:50</div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <span class="lesson-room">СК-322А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30</div>
      <div class="lesson-name">Высшая математика</div>
      <span class="lesson-room">ОК-303б</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Ср</div>
    <div class="lesson-card">
      <div class="lesson-time">8:00</div>
      <div class="lesson-name">Высшая математика</div>
      <span class="lesson-room">ПЗ-2114</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">9:50</div>
      <div class="lesson-name">История России</div>
      <span class="lesson-room">ПЗ-3028</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30</div>
      <div class="lesson-name">Иностранный язык п1</div>
      <span class="lesson-room">ПЗ-500Б</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Чт</div>
    <div class="lesson-card">
      <div class="lesson-time">9:50</div>
      <div class="lesson-name">Физическая культура</div>
      <span class="lesson-room">ПЗ-спортзал</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30</div>
      <div class="lesson-name">Информатика и основы программирования п1</div>
      <span class="lesson-room">ПЗ-1194/2ОК</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20</div>
      <div class="lesson-name">Информатика и основы программирования п2</div>
      <span class="lesson-room">ПЗ-1194/2ОК</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Пт</div>
    <div class="lesson-card">
      <div class="lesson-time">11:30</div>
      <div class="lesson-name">Алгоритмизация и программирование п1</div>
      <span class="lesson-room">ПЗ-8А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20</div>
      <div class="lesson-name">Алгоритмизация и программирование п2</div>
      <span class="lesson-room">ПЗ-8А</span>
    </div>
  </div>

<!-- Скрипт переключения -->
<script>
function switchWeek(weekId, btn) {
  document.querySelectorAll('.week-content').forEach(el => el.classList.remove('active'));
  document.querySelectorAll('.week-btn').forEach(el => el.classList.remove('active'));
  
  document.getElementById(weekId).classList.add('active');
  btn.classList.add('active');
}
</script>

<!-- Контакты -->
<hr style="margin-top: 2rem; border-color: var(--lightgray);" />

<div class="contact-box">
  <h3>💡 Нашли ошибку или есть предложения?</h3>
  <p>Если изменилось аудитория, перенеслась пара или вы хотите предложить улучшение для сайта:</p>
  <div class="contact-buttons">
    <a href="https://t.me/ваш_username" target="_blank" class="contact-btn telegram">
      📱 Написать в Telegram
    </a>
    <a href="mailto:ваш_email@example.com" class="contact-btn email">
      ✉️ Отправить на почту
    </a>
  </div>
</div>