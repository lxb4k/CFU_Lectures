---
title: Физтех | ПИ
---

---

<!-- Метатеги для PWA / Веб-приложения -->
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Расписание ПИ">
<meta name="theme-color" content="#2AABEE">
<link rel="manifest" href='data:application/manifest+json,{"name":"Физтех ПИ Расписание","short_name":"Расписание","start_url":".","display":"standalone","background_color":"#ffffff","theme_color":"#2AABEE"}'>

Официальное расписание на [cfuv.ru](https://cfuv.ru/raspisanie/): **ПИ-б-о-262** · **ПИ-б-о-261**[cite: 1]

<!-- CSS СТИЛИ -->
<style>
  /* Переключатель вкладок */
  .nav-tabs {
    display: flex;
    gap: 10px;
    margin-bottom: 1.2rem;
    border-bottom: 2px solid var(--lightgray);
    padding-bottom: 8px;
  }

  .nav-tab-btn {
    background: none;
    border: none;
    font-size: 0.95rem;
    font-weight: 700;
    color: var(--gray);
    cursor: pointer;
    padding: 6px 14px;
    border-radius: 6px;
    transition: all 0.2s ease;
  }

  .nav-tab-btn.active {
    background: var(--secondary);
    color: #ffffff;
  }

  .tab-content {
    display: none;
  }

  .tab-content.active {
    display: block;
  }

  /* Заглушка В разработке */
  .study-stub {
    text-align: center;
    padding: 3rem 1rem;
    background: var(--lightbg);
    border: 2px dashed var(--lightgray);
    border-radius: 8px;
    margin: 1.5rem 0;
  }

  .study-stub h3 {
    margin-bottom: 0.5rem;
    color: var(--secondary);
  }

  .study-stub p {
    color: var(--gray);
    font-size: 0.85rem;
  }

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

  .week-btn, .group-btn, .pwa-btn {
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

  .week-btn:hover, .group-btn:hover, .pwa-btn:hover {
    border-color: var(--secondary);
    color: var(--secondary);
  }

  .week-btn.active, .group-btn.active {
    background: var(--secondary);
    color: #ffffff;
    border-color: var(--secondary);
  }

  .pwa-btn {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    background: var(--lightbg);
    color: var(--secondary);
    border-color: var(--secondary);
  }

  .pwa-btn:hover {
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
    transition: all 0.2s ease;
  }

  /* Подсветка текущего дня */
  .day-column.today {
    border: 2px solid var(--secondary);
    box-shadow: 0 0 8px rgba(42, 171, 238, 0.25);
  }

  .day-column.today .day-header {
    background-color: var(--secondary);
    color: #ffffff;
    border-radius: 4px;
    padding: 2px 0;
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
    transition: all 0.2s ease;
  }

  /* Подсветка текущей пары */
  .lesson-card.active-lesson {
    border-left: 5px solid #ff9800;
    background-color: rgba(255, 152, 0, 0.15);
    box-shadow: 0 0 6px rgba(255, 152, 0, 0.3);
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
</style>

<!-- ВКЛАДКИ -->
<div class="nav-tabs">
  <button class="nav-tab-btn active" onclick="switchTab('schedule', this)">Расписание</button>
  <button class="nav-tab-btn" onclick="switchTab('study', this)">Учёба <small style="font-size:0.7em; opacity:0.8;">(в разработке)</small></button>
</div>

<!-- ВКЛАДКА: РАСПИСАНИЕ -->
<div id="tab-schedule" class="tab-content active">

  <!-- ПЕРЕКЛЮЧАТЕЛИ И КНОПКА ДОБАВЛЕНИЯ НА ЭКРАН -->
  <div class="controls-wrapper">
    <div class="toggle-group">
      <span class="toggle-label">Группа:</span>
      <button class="group-btn" data-group="262" onclick="setGroup('262', this)">ПИ-б-о-262</button>
      <button class="group-btn" data-group="261" onclick="setGroup('261', this)">ПИ-б-о-261</button>
    </div>

    <div class="toggle-group">
      <span class="toggle-label">Неделя:</span>
      <button class="week-btn" data-week="a" onclick="setWeek('a', this)">Неделя А</button>
      <button class="week-btn" data-week="b" onclick="setWeek('b', this)">Неделя Б</button>
    </div>

    <button class="pwa-btn" onclick="installPWA()">📱 На рабочий стол</button>
  </div>

  <div class="type-legend">
    <span class="lesson-type lk">ЛК</span> лекция
    <span class="lesson-type pz">ПЗ</span> практика
  </div>

  <!-- ================= ПИ-262 / НЕДЕЛЯ А ================= -->
  <div id="sched-262-a" class="schedule-block">
    <div class="day-column" data-day="1">
      <div class="day-header">Пн</div>
      <div class="lesson-card lk" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">История России</div>
        <span class="lesson-room">323А</span>
      </div>
      <div class="lesson-card lk" data-start="13:20" data-end="14:50">
        <div class="lesson-time">13:20 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Русский язык как государственный</div>
        <span class="lesson-room">323А</span>
      </div>
    </div>

    <div class="day-column" data-day="2">
      <div class="day-header">Вт</div>
      <div class="lesson-card pz" data-start="08:00" data-end="09:30">
        <div class="lesson-time">8:00 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Проектная деятельность</div>
        <span class="lesson-room">315А</span>
      </div>
      <div class="lesson-card lk" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Алгоритмизация и программирование</div>
        <span class="lesson-room">302А</span>
      </div>
      <div class="lesson-card lk" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Высшая математика</div>
        <span class="lesson-room">323А</span>
      </div>
    </div>

    <div class="day-column" data-day="3">
      <div class="day-header">Ср</div>
      <div class="lesson-card pz" data-start="08:00" data-end="09:30">
        <div class="lesson-time">8:00 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Иностранный язык</div>
        <span class="lesson-room">531Б/525Б</span>
      </div>
      <div class="lesson-card pz" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Высшая математика</div>
        <span class="lesson-room">211А</span>
      </div>
      <div class="lesson-card pz" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">История России</div>
        <span class="lesson-room">302В</span>
      </div>
    </div>

    <div class="day-column" data-day="4">
      <div class="day-header">Чт</div>
      <div class="lesson-card pz" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Физическая культура</div>
        <span class="lesson-room">спортзал</span>
      </div>
      <div class="lesson-card pz" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Русский язык как государственный</div>
        <span class="lesson-room">412В</span>
      </div>
    </div>

    <div class="day-column" data-day="5">
      <div class="day-header">Пт</div>
      <div class="lesson-card pz" data-start="15:00" data-end="16:30">
        <div class="lesson-time">15:00 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Алгоритмизация и программирование</div>
        <span class="lesson-room">117А</span>
      </div>
      <div class="lesson-card pz" data-start="16:40" data-end="18:10">
        <div class="lesson-time">16:40 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Информатика и основы программирования</div>
        <span class="lesson-room">119А</span>
      </div>
    </div>

    <div class="day-column" data-day="6">
      <div class="day-header">Сб</div>
      <div class="no-lessons">Пар нет</div>
    </div>
  </div>

  <!-- ================= ПИ-262 / НЕДЕЛЯ Б ================= -->
  <div id="sched-262-b" class="schedule-block">
    <div class="day-column" data-day="1">
      <div class="day-header">Пн</div>
      <div class="lesson-card lk" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">История России</div>
        <span class="lesson-room">323А</span>
      </div>
      <div class="lesson-card lk" data-start="13:20" data-end="14:50">
        <div class="lesson-time">13:20 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Информатика и основы программирования</div>
        <span class="lesson-room">323А</span>
      </div>
      <div class="lesson-card lk" data-start="15:00" data-end="16:30">
        <div class="lesson-time">15:00 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Структуры и алгоритмы обработки данных</div>
        <span class="lesson-room">323А</span>
      </div>
    </div>

    <div class="day-column" data-day="2">
      <div class="day-header">Вт</div>
      <div class="lesson-card lk" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Алгоритмизация и программирование</div>
        <span class="lesson-room">302А</span>
      </div>
      <div class="lesson-card lk" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Высшая математика</div>
        <span class="lesson-room">323А</span>
      </div>
    </div>

    <div class="day-column" data-day="3">
      <div class="day-header">Ср</div>
      <div class="lesson-card pz" data-start="08:00" data-end="09:30">
        <div class="lesson-time">8:00 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Иностранный язык</div>
        <span class="lesson-room">525Б</span>
      </div>
      <div class="lesson-card pz" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Высшая математика</div>
        <span class="lesson-room">211А</span>
      </div>
      <div class="lesson-card pz" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">История России</div>
        <span class="lesson-room">302В</span>
      </div>
    </div>

    <div class="day-column" data-day="4">
      <div class="day-header">Чт</div>
      <div class="lesson-card pz" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Физическая культура</div>
        <span class="lesson-room">спортзал</span>
      </div>
    </div>

    <div class="day-column" data-day="5">
      <div class="day-header">Пт</div>
      <div class="lesson-card pz" data-start="15:00" data-end="16:30">
        <div class="lesson-time">15:00 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Алгоритмизация и программирование п1</div>
        <span class="lesson-room">117А</span>
      </div>
      <div class="lesson-card pz" data-start="16:40" data-end="18:10">
        <div class="lesson-time">16:40 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Информатика и основы программирования</div>
        <span class="lesson-room">119А</span>
      </div>
    </div>

    <div class="day-column" data-day="6">
      <div class="day-header">Сб</div>
      <div class="lesson-card pz" data-start="13:20" data-end="14:50">
        <div class="lesson-time">13:20 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Структуры и алгоритмы обработки данных п1</div>
        <span class="lesson-room">308А</span>
      </div>
    </div>
  </div>

  <!-- ================= ПИ-261 / НЕДЕЛЯ А ================= -->
  <div id="sched-261-a" class="schedule-block">
    <div class="day-column" data-day="1">
      <div class="day-header">Пн</div>
      <div class="lesson-card lk" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">История России</div>
        <span class="lesson-room">323А</span>
      </div>
      <div class="lesson-card lk" data-start="13:20" data-end="14:50">
        <div class="lesson-time">13:20 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Русский язык как государственный</div>
        <span class="lesson-room">323А</span>
      </div>
      <div class="lesson-card pz" data-start="15:00" data-end="16:30">
        <div class="lesson-time">15:00 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Русский язык как государственный</div>
        <span class="lesson-room">411В</span>
      </div>
      <div class="lesson-card pz" data-start="16:40" data-end="18:10">
        <div class="lesson-time">16:40 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Иностранный язык (п/гр 2)</div>
        <span class="lesson-room">521Б</span>
      </div>
    </div>

    <div class="day-column" data-day="2">
      <div class="day-header">Вт</div>
      <div class="lesson-card lk" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Алгоритмизация и программирование</div>
        <span class="lesson-room">302А</span>
      </div>
      <div class="lesson-card lk" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Высшая математика</div>
        <span class="lesson-room">323А</span>
      </div>
    </div>

    <div class="day-column" data-day="3">
      <div class="day-header">Ср</div>
      <div class="lesson-card pz" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">История России</div>
        <span class="lesson-room">302В</span>
      </div>
      <div class="lesson-card pz" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Иностранный язык (п/гр 1)</div>
        <span class="lesson-room">211АВ</span>
      </div>
      <div class="lesson-card pz" data-start="13:20" data-end="14:50">
        <div class="lesson-time">13:20 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Высшая математика</div>
        <span class="lesson-room">211А</span>
      </div>
    </div>

    <div class="day-column" data-day="4">
      <div class="day-header">Чт</div>
      <div class="lesson-card pz" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Физическая культура</div>
        <span class="lesson-room">спортзал</span>
      </div>
      <div class="lesson-card pz" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Информатика и основы программирования (п/гр 1)</div>
        <span class="lesson-room">119А</span>
      </div>
      <div class="lesson-card pz" data-start="13:20" data-end="14:50">
        <div class="lesson-time">13:20 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Информатика и основы программирования (п/гр 2)</div>
        <span class="lesson-room">119А</span>
      </div>
    </div>

    <div class="day-column" data-day="5">
      <div class="day-header">Пт</div>
      <div class="lesson-card pz" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Алгоритмизация и программирование (п/гр 1)</div>
        <span class="lesson-room">8А</span>
      </div>
      <div class="lesson-card pz" data-start="13:20" data-end="14:50">
        <div class="lesson-time">13:20 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Алгоритмизация и программирование (п/гр 2)</div>
        <span class="lesson-room">8А</span>
      </div>
    </div>

    <div class="day-column" data-day="6">
      <div class="day-header">Сб</div>
      <div class="no-lessons">Пар нет</div>
    </div>
  </div>

  <!-- ================= ПИ-261 / НЕДЕЛЯ Б ================= -->
  <div id="sched-261-b" class="schedule-block">
    <div class="day-column" data-day="1">
      <div class="day-header">Пн</div>
      <div class="lesson-card lk" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">История России</div>
        <span class="lesson-room">323А</span>
      </div>
      <div class="lesson-card lk" data-start="13:20" data-end="14:50">
        <div class="lesson-time">13:20 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Информатика и основы программирования</div>
        <span class="lesson-room">323А</span>
      </div>
      <div class="lesson-card lk" data-start="15:00" data-end="16:30">
        <div class="lesson-time">15:00 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Структуры и алгоритмы обработки данных</div>
        <span class="lesson-room">323А</span>
      </div>
      <div class="lesson-card pz" data-start="16:40" data-end="18:10">
        <div class="lesson-time">16:40 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Иностранный язык (п/гр 2)</div>
        <span class="lesson-room">531Б</span>
      </div>
    </div>

    <div class="day-column" data-day="2">
      <div class="day-header">Вт</div>
      <div class="lesson-card pz" data-start="08:00" data-end="09:30">
        <div class="lesson-time">8:00 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Проектная деятельность</div>
        <span class="lesson-room">315А</span>
      </div>
      <div class="lesson-card lk" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Алгоритмизация и программирование</div>
        <span class="lesson-room">302А</span>
      </div>
      <div class="lesson-card lk" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Высшая математика</div>
        <span class="lesson-room">323А</span>
      </div>
    </div>

    <div class="day-column" data-day="3">
      <div class="day-header">Ср</div>
      <div class="lesson-card pz" data-start="08:00" data-end="09:30">
        <div class="lesson-time">8:00 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Высшая математика</div>
        <span class="lesson-room">211А</span>
      </div>
      <div class="lesson-card lk" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type lk">ЛК</span></div>
        <div class="lesson-name">Высшая математика</div>
        <span class="lesson-room">302А</span>
      </div>
      <div class="lesson-card pz" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Иностранный язык (п/гр 1)</div>
        <span class="lesson-room">500Б</span>
      </div>
    </div>

    <div class="day-column" data-day="4">
      <div class="day-header">Чт</div>
      <div class="lesson-card pz" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Физическая культура</div>
        <span class="lesson-room">спортзал</span>
      </div>
      <div class="lesson-card pz" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Информатика и основы программирования (т/гр 1)</div>
        <span class="lesson-room">120А</span>
      </div>
      <div class="lesson-card pz" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Информатика и основы программирования (и/гр 2)</div>
        <span class="lesson-room">120А</span>
      </div>
    </div>

    <div class="day-column" data-day="5">
      <div class="day-header">Пт</div>
      <div class="lesson-card pz" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Алгоритмизация и программирование (п/гр 1)</div>
        <span class="lesson-room">8А</span>
      </div>
      <div class="lesson-card pz" data-start="13:20" data-end="14:50">
        <div class="lesson-time">13:20 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Алгоритмизация и программирование (п/гр 2)</div>
        <span class="lesson-room">8А</span>
      </div>
    </div>

    <div class="day-column" data-day="6">
      <div class="day-header">Сб</div>
      <div class="lesson-card pz" data-start="09:50" data-end="11:20">
        <div class="lesson-time">9:50 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Структуры и алгоритмы обработки данных(п/гр 1)</div>
        <span class="lesson-room">308А</span>
      </div>
      <div class="lesson-card pz" data-start="11:30" data-end="13:00">
        <div class="lesson-time">11:30 <span class="lesson-type pz">ПЗ</span></div>
        <div class="lesson-name">Структуры и алгоритмы обработки данных (п/гр 2)</div>
        <span class="lesson-room">308А</span>
      </div>
    </div>
  </div>

</div>

<!-- ВКЛАДКА: УЧЁБА -->
<div id="tab-study" class="tab-content">
  <div class="study-stub">
    <h3>📖 Раздел «Учёба»</h3>
    <p>Данный раздел находится в разработке. Скоро здесь появятся учебные материалы, ссылки и полезные файлы.</p>
  </div>
</div>

<!-- БЛОК ОБ АВТОРЕ -->
<div class="contact-box">
  <span class="contact-text">Заметили ошибку в расписании или есть предложения?</span>[cite: 1]
  <a href="https://t.me/lxb4k" target="_blank" class="contact-btn">
    Telegram
  </a>[cite: 1]
</div>

<!-- СКРИПТЫ -->
<script>
  let currentGroup = localStorage.getItem('userGroup') || '262';
  let currentWeek = getAutoWeek();
  let deferredPrompt = null;

  // Автоопределение недели А/Б
  function getAutoWeek() {
    const now = new Date();
    const startOfYear = new Date(now.getFullYear(), 0, 1);
    const weekNumber = Math.ceil((((now - startOfYear) / 86400000) + startOfYear.getDay() + 1) / 7);
    return (weekNumber % 2 === 0) ? 'b' : 'a';
  }

  // Переключение вкладок
  function switchTab(tabName, btn) {
    document.querySelectorAll('.nav-tab-btn').forEach(b => b.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));

    btn.classList.add('active');
    document.getElementById(`tab-${tabName}`).classList.add('active');
  }

  // Обновление отображения
  function updateDisplay() {
    document.querySelectorAll('.schedule-block').forEach(el => el.classList.remove('active'));

    document.querySelectorAll('.group-btn').forEach(btn => {
      btn.classList.toggle('active', btn.dataset.group === currentGroup);
    });

    document.querySelectorAll('.week-btn').forEach(btn => {
      btn.classList.toggle('active', btn.dataset.week === currentWeek);
    });

    const targetId = `sched-${currentGroup}-${currentWeek}`;
    const target = document.getElementById(targetId);
    if (target) {
      target.classList.add('active');
      highlightTodayAndLesson(target);
    }
  }

  function setGroup(group, btn) {
    currentGroup = group;
    localStorage.setItem('userGroup', group);
    updateDisplay();
  }

  function setWeek(week, btn) {
    currentWeek = week;
    updateDisplay();
  }

  // Подсветка текущего дня и текущей пары
  function highlightTodayAndLesson(container) {
    const now = new Date();
    const dayOfWeek = now.getDay(); // 0 - Вс, 1 - Пн... 6 - Сб
    const currentMins = now.getHours() * 60 + now.getMinutes();

    container.querySelectorAll('.day-column').forEach(c => c.classList.remove('today'));
    container.querySelectorAll('.lesson-card').forEach(c => c.classList.remove('active-lesson'));

    if (dayOfWeek === 0) return; // В воскресенье расписания нет

    const todayCol = container.querySelector(`.day-column[data-day="${dayOfWeek}"]`);
    if (todayCol) {
      todayCol.classList.add('today');

      // Автопрокрутка к текущему дню
      todayCol.scrollIntoView({ behavior: 'smooth', block: 'nearest', inline: 'center' });

      // Подсветка пары по времени
      todayCol.querySelectorAll('.lesson-card').forEach(card => {
        const start = card.getAttribute('data-start');
        const end = card.getAttribute('data-end');

        if (start && end) {
          const [sH, sM] = start.split(':').map(Number);
          const [eH, eM] = end.split(':').map(Number);
          const startMins = sH * 60 + sM;
          const endMins = eH * 60 + eM;

          if (currentMins >= startMins && currentMins <= endMins) {
            card.classList.add('active-lesson');
          }
        }
      });
    }
  }

  // PWA Установка
  window.addEventListener('beforeinstallprompt', (e) => {
    e.preventDefault();
    deferredPrompt = e;
  });

  function installPWA() {
    if (deferredPrompt) {
      deferredPrompt.prompt();
      deferredPrompt.userChoice.then(() => { deferredPrompt = null; });
    } else {
      alert('Инструкция по установке:\n\n• iOS (Safari): Нажмите «Поделиться» -> «На экран «Домой»»\n• Android (Chrome): Откройте меню браузера (3 точки) -> «Добавить на главный экран»');
    }
  }

  document.addEventListener('DOMContentLoaded', updateDisplay);
</script>