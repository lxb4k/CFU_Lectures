---
title: Физтех | ПИ
---
---


Официальное расписание на [cfuv.ru](https://cfuv.ru): **ПИ-б-о-262** · **ПИ-б-о-261**

<!-- CSS СТИЛИ -->
<style>
  .controls-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
    margin: 1.2rem 0;
  }

  .toggle-group {
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .toggle-label {
    font-size: 0.85rem;
    font-weight: bold;
    color: var(--gray);
    margin-right: 4px;
  }

  .week-btn, .group-btn {
    background: var(--lightbg);
    color: var(--gray);
    border: 1px solid var(--lightgray);
    padding: 6px 14px;
    border-radius: 6px;
    cursor: pointer;
    font-weight: 600;
    font-size: 0.85rem;
    transition: all 0.2s ease;
  }

  .week-btn:hover, .group-btn:hover {
    border-color: var(--secondary);
    color: var(--secondary);
  }

  .week-btn.active, .group-btn.active {
    background: var(--secondary);
    color: var(--bg);
    border-color: var(--secondary);
  }

  .schedule-block {
    display: none;
  }

/* Горизонтальная прокрутка для всех дней недели */
  .schedule-block.active {
    display: flex;
    gap: 12px;
    overflow-x: auto; /* Включает горизонтальную прокрутку */
    padding-bottom: 10px; /* Зазор для полосы прокрутки */
    scroll-behavior: smooth;
  }

  /* Фиксируем ширину каждого дня, чтобы они не сжимались */
  .day-column {
    background-color: var(--lightbg);
    border: 1px solid var(--lightgray);
    border-radius: 8px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    min-width: 170px; /* Минимальная ширина колонки дня */
    flex: 1 0 170px;  /* Колонки не будут сжиматься меньше 170px */
  }

  /* Красивая полоса прокрутки (Scrollbar) */
  .schedule-block.active::-webkit-scrollbar {
    height: 8px;
  }

  .schedule-block.active::-webkit-scrollbar-track {
    background: var(--lightbg);
    border-radius: 4px;
  }

  .schedule-block.active::-webkit-scrollbar-thumb {
    background: var(--lightgray);
    border-radius: 4px;
  }

  .schedule-block.active::-webkit-scrollbar-thumb:hover {
    background: var(--secondary);
  }

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

  .contact-box {
    background-color: var(--lightbg);
    border: 1px dashed var(--secondary);
    border-radius: 8px;
    padding: 16px 20px;
    margin-top: 1.5rem;
    text-align: center;
  }

  .contact-box h3 {
    margin-top: 0;
    margin-bottom: 8px;
    color: var(--secondary);
    font-size: 1.1rem;
  }

  .contact-box p {
    font-size: 0.85rem;
    color: var(--gray);
    margin-bottom: 12px;
  }

  .contact-buttons {
    display: flex;
    justify-content: center;
    gap: 10px;
    flex-wrap: wrap;
  }

  .contact-btn {
    display: inline-block;
    padding: 6px 14px;
    border-radius: 6px;
    font-size: 0.85rem;
    font-weight: 600;
    text-decoration: none !important;
    transition: opacity 0.2s;
  }

  .contact-btn:hover {
    opacity: 0.85;
  }

  .telegram {
    background-color: #2AABEE;
    color: #ffffff !important;
  }
</style>

<!-- ПЕРЕКЛЮЧАТЕЛИ -->
<div class="controls-wrapper">
  <div class="toggle-group">
    <span class="toggle-label">Группа:</span>
    <button class="group-btn active" onclick="setGroup('262', this)">ПИ-б-о-262</button>
    <button class="group-btn" onclick="setGroup('261', this)">ПИ-б-о-261</button>
  </div>

  <div class="toggle-group">
    <span class="toggle-label">Неделя:</span>
    <button class="week-btn active" onclick="setWeek('a', this)">Неделя А</button>
    <button class="week-btn" onclick="setWeek('b', this)">Неделя Б</button>
  </div>
</div>

<!-- ================= ПИ-262 / НЕДЕЛЯ А ================= -->
<div id="sched-262-a" class="schedule-block active">
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

<!-- ================= ПИ-262 / НЕДЕЛЯ Б ================= -->
<div id="sched-262-b" class="schedule-block">
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

  <div class="day-column">
    <div class="day-header">Сб</div>
    <div class="lesson-card">
      <div class="lesson-time">9:50</div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных п1</div>
      <span class="lesson-room">ПЗ-3084</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30</div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных п2</div>
      <span class="lesson-room">ПЗ-3084</span>
    </div>
  </div>
</div>

<!-- ================= ПИ-261 / НЕДЕЛЯ А ================= -->
<div id="sched-261-a" class="schedule-block">
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
      <div class="lesson-time">9:50 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <span class="lesson-room">302А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Высшая математика</div>
      <span class="lesson-room">323А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Проектная деятельность</div>
      <span class="lesson-room">315А</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Ср</div>
    <div class="lesson-card">
      <div class="lesson-time">8:00 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Высшая математика</div>
      <span class="lesson-room">211А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">9:50 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">История России</div>
      <span class="lesson-room">302В</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык</div>
      <span class="lesson-room">531Б</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Чт</div>
    <div class="lesson-card">
      <div class="lesson-time">9:50 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Физическая культура</div>
      <span class="lesson-room">спортзал</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Пт</div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования</div>
      <span class="lesson-room">119А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <span class="lesson-room">117А</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Сб</div>
    <div class="no-lessons">Пар нет</div>
  </div>
</div>

<!-- ================= ПИ-261 / НЕДЕЛЯ Б ================= -->
<div id="sched-261-b" class="schedule-block">
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
  </div>

  <div class="day-column">
    <div class="day-header">Вт</div>
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
  </div>

  <div class="day-column">
    <div class="day-header">Чт</div>
    <div class="lesson-card">
      <div class="lesson-time">9:50</div>
      <div class="lesson-name">Физическая культура</div>
      <span class="lesson-room">ПЗ-спортзал</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Пт</div>
    <div class="lesson-card">
      <div class="lesson-time">11:30</div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <span class="lesson-room">ПЗ-8А</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Сб</div>
    <div class="no-lessons">Пар нет</div>
  </div>
</div>

<!-- БЛОК ОБРАТНОЙ СВЯЗИ -->
<div class="contact-box">
  <h3>💡 Есть вопросы или замечания по расписанию?</h3>
  <p>Если заметили ошибку в кабинетах или времени пар, напишите автору проекта:</p>
  <div class="contact-buttons">
    <a href="https://t.me/ваш_username" target="_blank" class="contact-btn telegram">
      📱 Написать в Telegram
    </a>
  </div>
</div>

<!-- СКРИПТ ПЕРЕКЛЮЧЕНИЯ ГРУПП И НЕДЕЛЬ -->
<script>
  let currentGroup = '262';
  let currentWeek = 'a';

  function updateDisplay() {
    document.querySelectorAll('.schedule-block').forEach(el => el.classList.remove('active'));
    const targetId = `sched-${currentGroup}-${currentWeek}`;
    const target = document.getElementById(targetId);
    if (target) {
      target.classList.add('active');
    }
  }

  function setGroup(group, btn) {
    currentGroup = group;
    btn.parentElement.querySelectorAll('.group-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    updateDisplay();
  }

  function setWeek(week, btn) {
    currentWeek = week;
    btn.parentElement.querySelectorAll('.week-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    updateDisplay();
  }
</script>