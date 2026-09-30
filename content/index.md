---
title: Физтех | ПИ
---

Официальное расписание на [cfuv.ru](https://cfuv.ru/raspisanie/): **ПИ-б-о-262** · **ПИ-б-о-261**

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
    font-size: 0.65rem;
    font-weight: 600;
    text-transform: uppercase;
    color: var(--gray);
    margin-left: 2px;
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

<!-- ПЕРЕКЛЮЧАТЕЛИ И КНОПКА СКАЧИВАНИЯ ICS -->
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

  <button class="ics-btn" onclick="downloadStaticICS()">📅 Скачать .ics</button>
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
      <div class="lesson-time">11:30 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">История России</div>
      <span class="lesson-room">323А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20<span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Информатика и основы программирования</div>
      <span class="lesson-room">323А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">15:00<span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных</div>
      <span class="lesson-room">323А</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Вт</div>
    <div class="lesson-card">
      <div class="lesson-time">9:50<span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Алгоритмизация и программирование</div>
      <span class="lesson-room">302А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30<span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Высшая математика</div>
      <span class="lesson-room">323А</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Ср</div>
    <div class="lesson-card">
      <div class="lesson-time">8:00<span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык</div>
      <span class="lesson-room">525Б</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">9:50<span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Высшая математика</div>
      <span class="lesson-room">211А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30<span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">История России</div>
      <span class="lesson-room">302В</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Чт</div>
    <div class="lesson-card">
      <div class="lesson-time">9:50<span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Физическая культура</div>
      <span class="lesson-room">спортзал</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Пт</div>
    <div class="lesson-card">
      <div class="lesson-time">15:00<span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование п1</div>
      <span class="lesson-room">117А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">16:40<span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования</div>
      <span class="lesson-room">119А</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Сб</div>
    <div class="lesson-card">
      <div class="lesson-time">13:20<span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных п1</div>
      <span class="lesson-room">308А</span>
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
    <div class="lesson-card">
      <div class="lesson-time">15:00 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Русский язык как государственный</div>
      <span class="lesson-room">411В</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">16:40 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык (п/гр 2)</div>
      <span class="lesson-room">521Б</span>
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
  </div>

  <div class="day-column">
    <div class="day-header">Ср</div>
    <div class="lesson-card">
      <div class="lesson-time">9:50 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">История России</div>
      <span class="lesson-room">302В</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык (п/гр 1)</div>
      <span class="lesson-room">211АВ</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Высшая математика</div>
      <span class="lesson-room">211А</span>
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
      <div class="lesson-name">Информатика и основы программирования (п/гр 1)</div>
      <span class="lesson-room">119А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования (п/гр 2)</div>
      <span class="lesson-room">119А</span>
    </div>
  </div>

  <div class="day-column">
    <div class="day-header">Пт</div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование (п/гр 1)</div>
      <span class="lesson-room">8А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование (п/гр 2)</div>
      <span class="lesson-room">8А</span>
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
      <div class="lesson-time">11:30 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">История России</div>
      <span class="lesson-room">323А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Информатика и основы программирования</div>
      <span class="lesson-room">323А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">15:00 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных</div>
      <span class="lesson-room">323А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">16:40 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык (п/гр 2)</div>
      <span class="lesson-room">531Б</span>
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
      <div class="lesson-name">Высшая математика)</div>
      <span class="lesson-room">323А</span>
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
      <div class="lesson-time">0 <span class="lesson-type">ЛК</span></div>
      <div class="lesson-name">Высшая математика</div>
      <span class="lesson-room">302А</span>
    </div>
	<div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Иностранный язык (п/гр 1)</div>
      <span class="lesson-room">500Б</span>
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
      <div class="lesson-time">9:50 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования (т/гр 1)</div>
      <span class="lesson-room">120А</span>
    </div>
	<div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Информатика и основы программирования (и/гр 2)</div>
      <span class="lesson-room">120А</span>
    </div>
  </div>

 <div class="day-column">
    <div class="day-header">Пт</div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование (п/гр 1)</div>
      <span class="lesson-room">8А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">13:20 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Алгоритмизация и программирование (п/гр 2)</div>
      <span class="lesson-room">8А</span>
    </div>
  </div>

<div class="day-column">
    <div class="day-header">Пт</div>
    <div class="lesson-card">
      <div class="lesson-time">9:50 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных(п/гр 1)</div>
      <span class="lesson-room">308А</span>
    </div>
    <div class="lesson-card">
      <div class="lesson-time">11:30 <span class="lesson-type">ПЗ</span></div>
      <div class="lesson-name">Структуры и алгоритмы обработки данных (п/гр 2)</div>
      <span class="lesson-room">308А</span>
    </div>
  </div>



<!-- БЛОК ОБ АВТОРЕ -->
<div class="contact-box">
  <span class="contact-text">Заметили ошибку в расписании или есть предложения?</span>
  <a href="https://t.me/lxb4k" target="_blank" class="contact-btn">
    Telegram
  </a>
</div>

<!-- СКРИПТ ПЕРЕКЛЮЧЕНИЯ И СКАЧИВАНИЯ ICS -->
<script>
  let currentGroup = '262';
  let currentWeek = 'a';

  const icsFiles = {
    '261': '/files/pi-261.ics',
    '262': '/files/pi-262.ics'
  };

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

  function downloadStaticICS() {
    const filePath = icsFiles[currentGroup];
    if (filePath) {
      const link = document.createElement('a');
      link.href = filePath;
      link.download = `ПИ-б-о-${currentGroup}.ics`;
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }
  }
</script>