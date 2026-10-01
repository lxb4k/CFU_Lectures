---
title: Физтех | ПИ
---

Официальное расписание на [cfuv.ru](https://cfuv.ru/raspisanie/): **ПИ-б-о-262** · **ПИ-б-о-261**

Ещё: [[Учёба/index|Учёба]] (в разработке)

<div class="next-box" id="next-box"></div>

<!-- CSS СТИЛИ -->
<style>
  .controls-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
    margin: 1.2rem 0;
    align-items: center;
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

  .week-btn, .group-btn, .ics-btn {
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
    color: #ffffff;
    border-color: var(--secondary);
  }

  .ics-btn {
    color: var(--secondary);
    border-color: var(--secondary);
    text-decoration: none;
    display: inline-flex;
    align-items: center;
  }

  .ics-btn:hover {
    background: var(--secondary);
    color: #ffffff;
  }

  .schedule-block {
    display: none;
  }

  /* ПК ВЕРСИЯ: 5 дней на экран + скролл для субботы */
  .schedule-block.active {
    display: flex;
    gap: 8px;
    overflow-x: auto;
    padding-bottom: 10px;
    scroll-behavior: smooth;
    align-items: flex-start;
  }

  .day-column {
    background-color: var(--lightbg);
    border: 1px solid var(--lightgray);
    border-radius: 8px;
    padding: 8px;
    display: flex;
    flex-direction: column;
    min-width: calc((100% - 32px) / 5);
    flex: 0 0 calc((100% - 32px) / 5);
    box-sizing: border-box;
  }

  /* МОБИЛЬНАЯ ВЕРСИЯ: Вертикальный список */
  @media (max-width: 768px) {
    .schedule-block.active {
      flex-direction: column;
      overflow-x: visible;
      align-items: stretch;
    }

    .day-column {
      min-width: 100%;
      flex: 1 1 100%;
    }
  }

  /* Стилизация полосы прокрутки */
  .schedule-block.active::-webkit-scrollbar {
    height: 6px;
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

  .day-header {
    font-weight: bold;
    font-size: 0.95rem;
    color: var(--secondary);
    border-bottom: 2px solid var(--tertiary);
    padding-bottom: 4px;
    margin-bottom: 8px;
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
    font-size: 0.75rem;
    font-weight: 700;
    color: var(--tertiary);
    margin-bottom: 2px;
  }

  .lesson-type {
    display: inline-block;
    font-size: 0.62rem;
    font-weight: 700;
    letter-spacing: 0.04em;
    line-height: 1.5;
    padding: 0 6px;
    margin-left: 4px;
    border-radius: 999px;
    border: 1px solid var(--lightgray);
    color: var(--gray);
    vertical-align: middle;
  }

  /* ЛК: синий цвет темы */
  .lesson-type.lk {
    color: var(--secondary);
    background: rgba(123, 151, 170, 0.16);
    background: color-mix(in srgb, var(--secondary) 16%, transparent);
    border-color: rgba(123, 151, 170, 0.5);
    border-color: color-mix(in srgb, var(--secondary) 50%, transparent);
  }

  /* ПЗ: мягкий сиреневый */
  .lesson-type.pz {
    color: #6b5b95;
    background: rgba(155, 138, 196, 0.16);
    border-color: rgba(155, 138, 196, 0.5);
  }

  :root[saved-theme="dark"] .lesson-type.pz { color: #b3a4dc; }

  .type-legend {
    display: flex;
    align-items: center;
    gap: 6px;
    flex-wrap: wrap;
    font-size: 0.78rem;
    color: var(--gray);
    margin: -0.4rem 0 1rem;
  }

  .type-legend .lesson-type {
    margin-left: 0;
  }

  .lesson-name {
    font-size: 0.8rem;
    line-height: 1.2;
    color: var(--dark);
    margin-bottom: 4px;
  }

  .lesson-room {
    font-size: 0.7rem;
    display: inline-block;
    background-color: var(--lightgray);
    color: var(--gray);
    padding: 1px 4px;
    border-radius: 3px;
    font-family: monospace;
  }

  .no-lessons {
    font-size: 0.8rem;
    color: var(--gray);
    text-align: center;
    padding: 12px 0;
  }

  /* Блок контактов */
  .contact-box {
    margin-top: 2rem;
    padding: 12px 16px;
    background-color: var(--lightbg);
    border: 1px solid var(--lightgray);
    border-radius: 6px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    flex-wrap: wrap;
  }

  .contact-text {
    font-size: 0.8rem;
    color: var(--gray);
    line-height: 1.3;
  }

  .contact-btn {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 5px 12px;
    border-radius: 5px;
    font-size: 0.8rem;
    font-weight: 600;
    text-decoration: none !important;
    background-color: #2AABEE;
    color: #ffffff !important;
    transition: opacity 0.2s ease;
  }

  .contact-btn:hover {
    opacity: 0.85;
  }

  /* ===== Новое: преподаватель, сегодня, текущая пара, блок «Следующая пара» ===== */
  .lesson-meta {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    gap: 3px 8px;
  }

  .lesson-teacher {
    font-size: 0.7rem;
    color: var(--gray);
  }

  .day-column.today {
    border-color: var(--secondary);
    box-shadow: 0 0 0 1px var(--secondary);
  }

  .day-column.today .day-header::after {
    content: "сегодня";
    display: inline-block;
    margin-left: 6px;
    padding: 0 7px;
    font-size: 0.6rem;
    font-weight: 700;
    letter-spacing: 0.04em;
    line-height: 1.6;
    vertical-align: middle;
    border-radius: 999px;
    background: var(--secondary);
    color: #ffffff;
  }

  .lesson-card.now {
    background-color: rgba(123, 151, 170, 0.28);
    background-color: color-mix(in srgb, var(--secondary) 28%, transparent);
    box-shadow: 0 0 0 1px var(--secondary);
  }

  .lesson-card.now .lesson-time::after {
    content: "идёт сейчас";
    display: inline-block;
    margin-left: 6px;
    padding: 0 7px;
    font-size: 0.6rem;
    font-weight: 700;
    line-height: 1.6;
    vertical-align: middle;
    border-radius: 999px;
    background: var(--tertiary);
    color: #ffffff;
  }

  .week-btn.cur::after {
    content: " ●";
    font-size: 0.55em;
    vertical-align: middle;
  }

  .next-box {
    margin: 1rem 0;
    padding: 10px 14px;
    background-color: var(--lightbg);
    border: 1px solid var(--lightgray);
    border-radius: 8px;
    font-size: 0.9rem;
    line-height: 1.5;
  }

  .next-box:empty {
    display: none;
  }

  .nb-title {
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 0.05em;
    text-transform: uppercase;
    color: var(--gray);
    margin-bottom: 2px;
  }

  .nb-row {
    color: var(--darkgray);
  }

  .nb-row b {
    color: var(--dark);
  }

  .nb-tag {
    display: inline-block;
    min-width: 5.2em;
    font-size: 0.7rem;
    font-weight: 700;
    color: var(--tertiary);
  }

  .nb-sub {
    color: var(--gray);
    font-size: 0.8rem;
  }

  .install-hint {
    font-size: 0.8rem;
    color: var(--gray);
    margin: -0.4rem 0 1rem;
  }

  /* Телефон: сегодняшний день показываем первым */
  @media (max-width: 768px) {
    .day-column.today {
      order: -1;
    }
  }
</style>

<!-- ПЕРЕКЛЮЧАТЕЛИ, КАЛЕНДАРЬ И УСТАНОВКА -->
<div class="controls-wrapper">
  <div class="toggle-group">
    <span class="toggle-label">Моя группа:</span>
    <button class="group-btn active" data-group="262" onclick="setGroup('262', this)">ПИ-б-о-262</button>
    <button class="group-btn" data-group="261" onclick="setGroup('261', this)">ПИ-б-о-261</button>
  </div>

  <div class="toggle-group">
    <span class="toggle-label">Неделя:</span>
    <button class="week-btn active" data-week="a" onclick="setWeek('a', this)">Неделя А</button>
    <button class="week-btn" data-week="b" onclick="setWeek('b', this)">Неделя Б</button>
  </div>

  <button class="ics-btn" onclick="downloadStaticICS()">В календарь (.ics)</button>
  <button class="ics-btn" id="install-btn" style="display:none" onclick="installApp()">Установить приложение</button>
</div>

<div class="install-hint" id="ios-hint" style="display:none">Чтобы добавить на экран «Домой»: в Safari нажми «Поделиться» и выбери «На экран „Домой“».</div>

<div class="type-legend">
  <span class="lesson-type lk">ЛК</span> лекция
  <span class="lesson-type pz">ПЗ</span> практика
</div>

<!-- ================= ПИ-262 / НЕДЕЛЯ А ================= -->
<div id="sched-262-a" class="schedule-block active">
  <div class="day-column" data-d="0">
    <div class="day-header">Пн</div>
    <div class="lesson-card lk" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">История России</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Манаев А.Ю.</span></div>
    </div>
    <div class="lesson-card lk" data-start="800" data-end="890">
      <div class="lesson-time">13:20–14:50 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Русский язык как государственный</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Прадид О.Ю.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="1">
    <div class="day-header">Вт</div>
    <div class="lesson-card pz" data-start="480" data-end="570">
      <div class="lesson-time">08:00–09:30 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Проектная деятельность</div>
      <div class="lesson-meta"><span class="lesson-room">315А</span><span class="lesson-teacher">Нестеренко Н.А.</span></div>
    </div>
    <div class="lesson-card lk" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <div class="lesson-meta"><span class="lesson-room">302А</span><span class="lesson-teacher">Чабанов В.В.</span></div>
    </div>
    <div class="lesson-card lk" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Высшая математика</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Смирнова С.И.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="2">
    <div class="day-header">Ср</div>
    <div class="lesson-card pz" data-start="480" data-end="570">
      <div class="lesson-time">08:00–09:30 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык</div>
      <div class="lesson-meta"><span class="lesson-room">531Б</span><span class="lesson-teacher">Мельниченко Т.В.</span></div>
    </div>
    <div class="lesson-card pz" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Высшая математика</div>
      <div class="lesson-meta"><span class="lesson-room">211А</span><span class="lesson-teacher">Смирнова С.И.</span></div>
    </div>
    <div class="lesson-card pz" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">История России</div>
      <div class="lesson-meta"><span class="lesson-room">302В</span><span class="lesson-teacher">Манаев А.Ю.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="3">
    <div class="day-header">Чт</div>
    <div class="lesson-card pz" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Физическая культура</div>
      <div class="lesson-meta"><span class="lesson-room">спортзал</span><span class="lesson-teacher">Мищенко С.Г.</span></div>
    </div>
    <div class="lesson-card pz" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Русский язык как государственный</div>
      <div class="lesson-meta"><span class="lesson-room">412В</span><span class="lesson-teacher">Прадид О.Ю.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="4">
    <div class="day-header">Пт</div>
    <div class="lesson-card pz" data-start="900" data-end="990">
      <div class="lesson-time">15:00–16:30 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <div class="lesson-meta"><span class="lesson-room">117А</span><span class="lesson-teacher">Чабанов В.В.</span></div>
    </div>
    <div class="lesson-card pz" data-start="1000" data-end="1090">
      <div class="lesson-time">16:40–18:10 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования</div>
      <div class="lesson-meta"><span class="lesson-room">119А</span><span class="lesson-teacher">ас.Абдурахманова Ф.Э.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="5">
    <div class="day-header">Сб</div>
    <div class="no-lessons">Пар нет</div>
  </div>
</div>

<!-- ================= ПИ-262 / НЕДЕЛЯ Б ================= -->
<div id="sched-262-b" class="schedule-block">
  <div class="day-column" data-d="0">
    <div class="day-header">Пн</div>
    <div class="lesson-card lk" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">История России</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Манаев А.Ю.</span></div>
    </div>
    <div class="lesson-card lk" data-start="800" data-end="890">
      <div class="lesson-time">13:20–14:50 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Информатика и основы программирования</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Брецько М.В.</span></div>
    </div>
    <div class="lesson-card lk" data-start="900" data-end="990">
      <div class="lesson-time">15:00–16:30 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Горская И.Ю.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="1">
    <div class="day-header">Вт</div>
    <div class="lesson-card lk" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <div class="lesson-meta"><span class="lesson-room">302А</span><span class="lesson-teacher">Чабанов В.В.</span></div>
    </div>
    <div class="lesson-card lk" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Высшая математика</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Смирнова С.И.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="2">
    <div class="day-header">Ср</div>
    <div class="lesson-card pz" data-start="480" data-end="570">
      <div class="lesson-time">08:00–09:30 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык</div>
      <div class="lesson-meta"><span class="lesson-room">525Б</span><span class="lesson-teacher">Мельниченко Т.В.</span></div>
    </div>
    <div class="lesson-card pz" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Высшая математика</div>
      <div class="lesson-meta"><span class="lesson-room">211А</span><span class="lesson-teacher">Смирнова С.И.</span></div>
    </div>
    <div class="lesson-card pz" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">История России</div>
      <div class="lesson-meta"><span class="lesson-room">302В</span><span class="lesson-teacher">Манаев А.Ю.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="3">
    <div class="day-header">Чт</div>
    <div class="lesson-card pz" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Физическая культура</div>
      <div class="lesson-meta"><span class="lesson-room">спортзал</span><span class="lesson-teacher">Мищенко С.Г.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="4">
    <div class="day-header">Пт</div>
    <div class="lesson-card pz" data-start="900" data-end="990">
      <div class="lesson-time">15:00–16:30 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <div class="lesson-meta"><span class="lesson-room">117А</span><span class="lesson-teacher">Чабанов В.В.</span></div>
    </div>
    <div class="lesson-card pz" data-start="1000" data-end="1090">
      <div class="lesson-time">16:40–18:10 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования</div>
      <div class="lesson-meta"><span class="lesson-room">119А</span><span class="lesson-teacher">ас.Абдурахманова Ф.Э.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="5">
    <div class="day-header">Сб</div>
    <div class="lesson-card pz" data-start="800" data-end="890">
      <div class="lesson-time">13:20–14:50 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных</div>
      <div class="lesson-meta"><span class="lesson-room">308А</span><span class="lesson-teacher">Горская И.Ю.</span></div>
    </div>
  </div>
</div>

<!-- ================= ПИ-261 / НЕДЕЛЯ А ================= -->
<div id="sched-261-a" class="schedule-block">
  <div class="day-column" data-d="0">
    <div class="day-header">Пн</div>
    <div class="lesson-card lk" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">История России</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Манаев А.Ю.</span></div>
    </div>
    <div class="lesson-card lk" data-start="800" data-end="890">
      <div class="lesson-time">13:20–14:50 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Русский язык как государственный</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Прадид О.Ю.</span></div>
    </div>
    <div class="lesson-card pz" data-start="900" data-end="990">
      <div class="lesson-time">15:00–16:30 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Русский язык как государственный</div>
      <div class="lesson-meta"><span class="lesson-room">411В</span><span class="lesson-teacher">Прадид О.Ю.</span></div>
    </div>
    <div class="lesson-card pz" data-start="1000" data-end="1090">
      <div class="lesson-time">16:40–18:10 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык (п/гр 2)</div>
      <div class="lesson-meta"><span class="lesson-room">531Б</span><span class="lesson-teacher">Мельниченко Т.В.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="1">
    <div class="day-header">Вт</div>
    <div class="lesson-card lk" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <div class="lesson-meta"><span class="lesson-room">302А</span><span class="lesson-teacher">Чабанов В.В.</span></div>
    </div>
    <div class="lesson-card lk" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Высшая математика</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Смирнова С.И.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="2">
    <div class="day-header">Ср</div>
    <div class="lesson-card pz" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">История России</div>
      <div class="lesson-meta"><span class="lesson-room">302В</span><span class="lesson-teacher">Манаев А.Ю.</span></div>
    </div>
    <div class="lesson-card pz" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык (п/гр 1)</div>
      <div class="lesson-meta"><span class="lesson-room">500Б</span><span class="lesson-teacher">Шестакова Е.С.</span></div>
    </div>
    <div class="lesson-card pz" data-start="800" data-end="890">
      <div class="lesson-time">13:20–14:50 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Высшая математика</div>
      <div class="lesson-meta"><span class="lesson-room">211А</span><span class="lesson-teacher">Смирнова С.И.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="3">
    <div class="day-header">Чт</div>
    <div class="lesson-card pz" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Физическая культура</div>
      <div class="lesson-meta"><span class="lesson-room">спортзал</span><span class="lesson-teacher">Ковальчук Е.С.</span></div>
    </div>
    <div class="lesson-card pz" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования (п/гр 1)</div>
      <div class="lesson-meta"><span class="lesson-room">119А</span><span class="lesson-teacher">ас.Абдурахманова Ф.Э.</span></div>
    </div>
    <div class="lesson-card pz" data-start="800" data-end="890">
      <div class="lesson-time">13:20–14:50 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования (п/гр 2)</div>
      <div class="lesson-meta"><span class="lesson-room">119А</span><span class="lesson-teacher">ас.Абдурахманова Ф.Э.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="4">
    <div class="day-header">Пт</div>
    <div class="lesson-card pz" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование (п/гр 1)</div>
      <div class="lesson-meta"><span class="lesson-room">8А</span><span class="lesson-teacher">Чабанов В.В.</span></div>
    </div>
    <div class="lesson-card pz" data-start="800" data-end="890">
      <div class="lesson-time">13:20–14:50 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование (п/гр 2)</div>
      <div class="lesson-meta"><span class="lesson-room">8А</span><span class="lesson-teacher">Чабанов В.В.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="5">
    <div class="day-header">Сб</div>
    <div class="no-lessons">Пар нет</div>
  </div>
</div>

<!-- ================= ПИ-261 / НЕДЕЛЯ Б ================= -->
<div id="sched-261-b" class="schedule-block">
  <div class="day-column" data-d="0">
    <div class="day-header">Пн</div>
    <div class="lesson-card lk" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">История России</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Манаев А.Ю.</span></div>
    </div>
    <div class="lesson-card lk" data-start="800" data-end="890">
      <div class="lesson-time">13:20–14:50 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Информатика и основы программирования</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Брецько М.В.</span></div>
    </div>
    <div class="lesson-card lk" data-start="900" data-end="990">
      <div class="lesson-time">15:00–16:30 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Горская И.Ю.</span></div>
    </div>
    <div class="lesson-card pz" data-start="1000" data-end="1090">
      <div class="lesson-time">16:40–18:10 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык (п/гр 2)</div>
      <div class="lesson-meta"><span class="lesson-room">531Б</span><span class="lesson-teacher">Мельниченко Т.В.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="1">
    <div class="day-header">Вт</div>
    <div class="lesson-card pz" data-start="480" data-end="570">
      <div class="lesson-time">08:00–09:30 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Проектная деятельность</div>
      <div class="lesson-meta"><span class="lesson-room">315А</span><span class="lesson-teacher">Нестеренко Н.А.</span></div>
    </div>
    <div class="lesson-card lk" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <div class="lesson-meta"><span class="lesson-room">302А</span><span class="lesson-teacher">Чабанов В.В.</span></div>
    </div>
    <div class="lesson-card lk" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type lk">ЛК</span></div>
      <div class="lesson-name">Высшая математика</div>
      <div class="lesson-meta"><span class="lesson-room">323А</span><span class="lesson-teacher">Смирнова С.И.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="2">
    <div class="day-header">Ср</div>
    <div class="lesson-card pz" data-start="480" data-end="570">
      <div class="lesson-time">08:00–09:30 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Высшая математика</div>
      <div class="lesson-meta"><span class="lesson-room">211А</span><span class="lesson-teacher">Смирнова С.И.</span></div>
    </div>
    <div class="lesson-card pz" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">История России</div>
      <div class="lesson-meta"><span class="lesson-room">302В</span><span class="lesson-teacher">Манаев А.Ю.</span></div>
    </div>
    <div class="lesson-card pz" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык (п/гр 1)</div>
      <div class="lesson-meta"><span class="lesson-room">500Б</span><span class="lesson-teacher">Шестакова Е.С.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="3">
    <div class="day-header">Чт</div>
    <div class="lesson-card pz" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Физическая культура</div>
      <div class="lesson-meta"><span class="lesson-room">спортзал</span><span class="lesson-teacher">Ковальчук Е.С.</span></div>
    </div>
    <div class="lesson-card pz" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования (п/гр 1)</div>
      <div class="lesson-meta"><span class="lesson-room">120А</span><span class="lesson-teacher">ас.Абдурахманова Ф.Э.</span></div>
    </div>
    <div class="lesson-card pz" data-start="800" data-end="890">
      <div class="lesson-time">13:20–14:50 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования (п/гр 2)</div>
      <div class="lesson-meta"><span class="lesson-room">120А</span><span class="lesson-teacher">ас.Абдурахманова Ф.Э.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="4">
    <div class="day-header">Пт</div>
    <div class="lesson-card pz" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование (п/гр 1)</div>
      <div class="lesson-meta"><span class="lesson-room">8А</span><span class="lesson-teacher">Чабанов В.В.</span></div>
    </div>
    <div class="lesson-card pz" data-start="800" data-end="890">
      <div class="lesson-time">13:20–14:50 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование (п/гр 2)</div>
      <div class="lesson-meta"><span class="lesson-room">8А</span><span class="lesson-teacher">Чабанов В.В.</span></div>
    </div>
  </div>
  <div class="day-column" data-d="5">
    <div class="day-header">Сб</div>
    <div class="lesson-card pz" data-start="590" data-end="680">
      <div class="lesson-time">09:50–11:20 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных (п/гр 1)</div>
      <div class="lesson-meta"><span class="lesson-room">308А</span><span class="lesson-teacher">Горская И.Ю.</span></div>
    </div>
    <div class="lesson-card pz" data-start="690" data-end="780">
      <div class="lesson-time">11:30–13:00 <span class="lesson-type pz">ПЗ</span></div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных (п/гр 2)</div>
      <div class="lesson-meta"><span class="lesson-room">308А</span><span class="lesson-teacher">Горская И.Ю.</span></div>
    </div>
  </div>
</div>

<!-- БЛОК ОБ АВТОРЕ -->
<div class="contact-box">
  <span class="contact-text">Заметили ошибку в расписании или есть предложения?</span>
  <a href="https://t.me/lxb4k" target="_blank" class="contact-btn">
    Telegram
  </a>
</div>

<!-- СКРИПТ: переключатели, сегодня, текущая пара, календарь, веб-приложение -->
<script>
var currentGroup = '262';
var currentWeek = 'a';
var realWeek = 'a';
var schedTimer = null;
var installPrompt = null;
var BASE = Date.UTC(2026, 8, 7);
var DAY_NAMES = ['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб'];
var DAY_ON = ['в понедельник', 'во вторник', 'в среду', 'в четверг', 'в пятницу', 'в субботу'];

var icsFiles = {
  '261': '/files/pi-261.ics',
  '262': '/files/pi-262.ics'
};

function esc(s) {
  return String(s).replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;');
}

function hm(m) {
  var h = Math.floor(m / 60), x = m % 60;
  return (h < 10 ? '0' : '') + h + ':' + (x < 10 ? '0' : '') + x;
}

function weekOf(utcMs) {
  var w = Math.floor((utcMs - BASE) / 86400000 / 7);
  return (((w % 2) + 2) % 2) ? 'b' : 'a';
}

function nowInfo() {
  var n = new Date();
  return {
    utc: Date.UTC(n.getFullYear(), n.getMonth(), n.getDate()),
    dow: (n.getDay() + 6) % 7,
    mins: n.getHours() * 60 + n.getMinutes()
  };
}

function lessonsOf(g, w, d) {
  var col = document.querySelector('#sched-' + g + '-' + w + ' .day-column[data-d="' + d + '"]');
  if (!col) return [];
  return Array.prototype.map.call(col.querySelectorAll('.lesson-card'), function (c) {
    var room = c.querySelector('.lesson-room');
    var teacher = c.querySelector('.lesson-teacher');
    return {
      start: Number(c.getAttribute('data-start')),
      end: Number(c.getAttribute('data-end')),
      name: c.querySelector('.lesson-name').textContent,
      room: room ? room.textContent : '',
      teacher: teacher ? teacher.textContent : ''
    };
  });
}

function markToday() {
  var n = nowInfo();
  Array.prototype.forEach.call(document.querySelectorAll('.day-column.today, .lesson-card.now'), function (el) {
    el.classList.remove('today');
    el.classList.remove('now');
  });
  if (n.dow > 5) return;
  ['262', '261'].forEach(function (g) {
    var col = document.querySelector('#sched-' + g + '-' + realWeek + ' .day-column[data-d="' + n.dow + '"]');
    if (!col) return;
    col.classList.add('today');
    Array.prototype.forEach.call(col.querySelectorAll('.lesson-card'), function (c) {
      var s = Number(c.getAttribute('data-start'));
      var e = Number(c.getAttribute('data-end'));
      if (n.mins >= s && n.mins < e) c.classList.add('now');
    });
  });
}

function scrollToToday() {
  var blk = document.getElementById('sched-' + currentGroup + '-' + currentWeek);
  if (!blk) return;
  var col = blk.querySelector('.day-column.today');
  if (!col || blk.scrollWidth <= blk.clientWidth) return;
  var r = col.getBoundingClientRect();
  var b = blk.getBoundingClientRect();
  if (r.right > b.right || r.left < b.left) blk.scrollLeft += r.left - b.left;
}

function renderNext() {
  var box = document.getElementById('next-box');
  if (!box) return;
  var n = nowInfo();
  var cur = null, nxt = null, nxtDay = 0, nxtD = 0;
  for (var i = 0; i < 14 && !nxt; i++) {
    var d = (n.dow + i) % 7;
    if (d > 5) continue;
    var list = lessonsOf(currentGroup, weekOf(n.utc + i * 86400000), d);
    for (var k = 0; k < list.length; k++) {
      var l = list[k];
      if (i === 0 && n.mins >= l.start && n.mins < l.end) { cur = l; continue; }
      if (i > 0 || l.start > n.mins) { nxt = l; nxtDay = i; nxtD = d; break; }
    }
  }
  var html = '<div class="nb-title">ПИ-б-о-' + currentGroup + '</div>';
  if (cur) {
    html += '<div class="nb-row"><span class="nb-tag">Сейчас</span><b>' + esc(cur.name) + '</b> · до ' + hm(cur.end) +
      (cur.room ? ' · ' + esc(cur.room) : '') + '</div>';
  }
  if (nxt) {
    var when;
    if (nxtDay === 0) {
      var diff = nxt.start - n.mins;
      var h = Math.floor(diff / 60), m = diff % 60;
      when = ('через ' + (h ? h + ' ч ' : '') + (m || !h ? m + ' мин' : '')).trim();
    } else if (nxtDay === 1) {
      when = 'завтра, ' + hm(nxt.start);
    } else {
      when = DAY_ON[nxtD] + ', ' + hm(nxt.start);
    }
    var sub = [nxt.room, nxt.teacher].filter(Boolean).join(' · ');
    html += '<div class="nb-row"><span class="nb-tag">Следующая</span><b>' + esc(nxt.name) + '</b> · ' + when +
      (sub ? ' <span class="nb-sub">· ' + esc(sub) + '</span>' : '') + '</div>';
  }
  if (!cur && !nxt) html += '<div class="nb-row">Ближайших пар нет</div>';
  box.innerHTML = html;
}

function syncButtons() {
  Array.prototype.forEach.call(document.querySelectorAll('.group-btn'), function (b) {
    b.classList.toggle('active', b.getAttribute('data-group') === currentGroup);
  });
  Array.prototype.forEach.call(document.querySelectorAll('.week-btn'), function (b) {
    b.classList.toggle('active', b.getAttribute('data-week') === currentWeek);
    b.classList.toggle('cur', b.getAttribute('data-week') === realWeek);
  });
}

function tick() {
  realWeek = weekOf(nowInfo().utc);
  markToday();
  syncButtons();
  renderNext();
}

function updateDisplay() {
  Array.prototype.forEach.call(document.querySelectorAll('.schedule-block'), function (el) {
    el.classList.remove('active');
  });
  var target = document.getElementById('sched-' + currentGroup + '-' + currentWeek);
  if (target) target.classList.add('active');
  tick();
  scrollToToday();
}

function setGroup(group) {
  currentGroup = group;
  try { localStorage.setItem('sched-group', group); } catch (e) {}
  updateDisplay();
}

function setWeek(week) {
  currentWeek = week;
  updateDisplay();
}

function downloadStaticICS() {
  var filePath = icsFiles[currentGroup];
  if (filePath) {
    var link = document.createElement('a');
    link.href = filePath;
    link.download = 'ПИ-б-о-' + currentGroup + '.ics';
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  }
}

function installApp() {
  if (!installPrompt) return;
  installPrompt.prompt();
  installPrompt.userChoice.then(function () {
    installPrompt = null;
    var b = document.getElementById('install-btn');
    if (b) b.style.display = 'none';
  });
}

function setupPWA() {
  var head = document.head;
  function add(tag, attrs) {
    var el = document.createElement(tag);
    Object.keys(attrs).forEach(function (k) { el.setAttribute(k, attrs[k]); });
    head.appendChild(el);
  }
  if (!document.querySelector('link[rel="manifest"]')) add('link', { rel: 'manifest', href: '/manifest.json' });
  if (!document.querySelector('link[rel="apple-touch-icon"]')) add('link', { rel: 'apple-touch-icon', href: '/icons/apple-touch-icon.png' });
  if (!document.querySelector('meta[name="apple-mobile-web-app-capable"]')) {
    add('meta', { name: 'apple-mobile-web-app-capable', content: 'yes' });
    add('meta', { name: 'apple-mobile-web-app-title', content: 'Расписание' });
    add('meta', { name: 'mobile-web-app-capable', content: 'yes' });
  }
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js').catch(function () {});
  }
  var standalone = (window.matchMedia && window.matchMedia('(display-mode: standalone)').matches) || window.navigator.standalone;
  var hint = document.getElementById('ios-hint');
  if (hint && !standalone && /iphone|ipad|ipod/i.test(navigator.userAgent)) hint.style.display = 'block';
}

function initSchedule() {
  if (!document.getElementById('sched-262-a')) return;
  var n = nowInfo();
  realWeek = weekOf(n.utc);
  currentWeek = n.dow > 5 ? (realWeek === 'a' ? 'b' : 'a') : realWeek;
  try {
    var sg = localStorage.getItem('sched-group');
    if (sg === '261' || sg === '262') currentGroup = sg;
  } catch (e) {}
  updateDisplay();
  if (schedTimer) clearInterval(schedTimer);
  schedTimer = setInterval(tick, 30000);
  setupPWA();
}

if (!window.__schedBound) {
  window.__schedBound = true;
  document.addEventListener('nav', initSchedule);
  window.addEventListener('beforeinstallprompt', function (e) {
    e.preventDefault();
    installPrompt = e;
    var b = document.getElementById('install-btn');
    if (b) b.style.display = 'inline-flex';
  });
  window.addEventListener('appinstalled', function () {
    var b = document.getElementById('install-btn');
    if (b) b.style.display = 'none';
  });
  document.addEventListener('visibilitychange', function () {
    if (!document.hidden) tick();
  });
}

initSchedule();

</script>
