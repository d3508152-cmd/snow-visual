<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Snow Visual</title>
  <style>
    :root {
      --bg: #090e18;
      --panel: #101927;
      --panel-light: #152235;
      --line: #26374d;
      --text: #eaf4ff;
      --muted: #8295aa;
      --blue: #72c9ff;
      --cyan: #8ff4ee;
      --green: #8dffc2;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      min-height: 100vh;
      display: grid;
      place-items: center;
      padding: 24px;
      color: var(--text);
      font-family: Inter, "Segoe UI", Arial, sans-serif;
      background:
        radial-gradient(ellipse at 15% 10%, #183556 0, transparent 36%),
        radial-gradient(ellipse at 90% 90%, #12313c 0, transparent 32%),
        var(--bg);
    }

    .app {
      width: min(100%, 980px);
      min-height: 610px;
      display: grid;
      grid-template-columns: 220px 1fr;
      overflow: hidden;
      border: 1px solid #344a62;
      border-radius: 22px;
      background: #0c1420ee;
      box-shadow: 0 30px 100px #0009, 0 0 45px #72c9ff12;
    }

    aside {
      padding: 25px 16px;
      border-right: 1px solid var(--line);
      background: linear-gradient(180deg, #111e2e, #0c1420);
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      padding: 0 9px 27px;
    }

    .logo {
      width: 39px;
      height: 39px;
      display: grid;
      place-items: center;
      border-radius: 13px;
      color: #08131d;
      font-size: 20px;
      background: linear-gradient(135deg, var(--cyan), var(--blue));
      box-shadow: 0 0 22px #72c9ff55;
    }

    .brand strong { display: block; letter-spacing: .8px; }
    .brand small { color: var(--muted); font-size: 11px; }

    .nav-label {
      margin: 10px 10px 9px;
      color: #637991;
      font-size: 10px;
      font-weight: 700;
      letter-spacing: 1.5px;
      text-transform: uppercase;
    }

    .nav-btn {
      width: 100%;
      display: flex;
      align-items: center;
      gap: 11px;
      padding: 12px;
      margin: 4px 0;
      border: 1px solid transparent;
      border-radius: 11px;
      color: #9aacc0;
      background: transparent;
      text-align: left;
      cursor: pointer;
      transition: .2s;
    }

    .nav-btn:hover, .nav-btn.active {
      color: var(--text);
      border-color: #29435c;
      background: linear-gradient(90deg, #1a344b, #142438);
    }

    .nav-btn.active { box-shadow: inset 3px 0 var(--blue); }
    .nav-icon { width: 19px; text-align: center; }

    .side-status {
      margin: 34px 5px 0;
      padding: 13px;
      border: 1px solid #234137;
      border-radius: 12px;
      color: #a9c6ba;
      background: #10231e;
      font-size: 11px;
    }

    .dot {
      display: inline-block;
      width: 7px;
      height: 7px;
      margin-right: 7px;
      border-radius: 50%;
      background: var(--green);
      box-shadow: 0 0 10px var(--green);
    }

    main { padding: 29px 34px; }

    header {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 15px;
      margin-bottom: 25px;
    }

    h1 { margin: 0; font-size: 25px; letter-spacing: -.5px; }
    .subtitle { margin-top: 6px; color: var(--muted); font-size: 12px; }

    .version {
      padding: 7px 10px;
      border: 1px solid #29445c;
      border-radius: 8px;
      color: var(--cyan);
      background: #112538;
      font: 11px monospace;
    }

    .tab-content { display: none; }
    .tab-content.active { display: block; }

    .section-title {
      display: flex;
      align-items: center;
      gap: 8px;
      margin: 22px 0 11px;
      color: #b6c9da;
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 1.3px;
      text-transform: uppercase;
    }

    .section-title::after {
      content: "";
      height: 1px;
      flex: 1;
      background: var(--line);
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
    }

    .option {
      min-height: 64px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      padding: 12px 14px;
      border: 1px solid var(--line);
      border-radius: 12px;
      background: linear-gradient(135deg, #142133, #101a28);
      transition: .2s;
    }

    .option:hover { border-color: #45627b; transform: translateY(-1px); }
    .option strong { display: block; font-size: 12px; font-weight: 600; }
    .option small { display: block; margin-top: 4px; color: var(--muted); font-size: 10px; }

    .switch {
      position: relative;
      flex: 0 0 auto;
      width: 36px;
      height: 20px;
      border: 1px solid #42546a;
      border-radius: 20px;
      background: #202d3c;
      cursor: pointer;
      transition: .2s;
    }

    .switch::after {
      content: "";
      position: absolute;
      top: 3px;
      left: 3px;
      width: 12px;
      height: 12px;
      border-radius: 50%;
      background: #9aabbd;
      transition: .2s;
    }

    .switch.on {
      border-color: #65cfff;
      background: #267eb0;
      box-shadow: 0 0 12px #72c9ff35;
    }

    .switch.on::after {
      left: 19px;
      background: white;
    }

    .slider-card {
      margin-top: 11px;
      padding: 14px;
      border: 1px solid var(--line);
      border-radius: 12px;
      background: #121e2d;
    }

    .slider-head {
      display: flex;
      justify-content: space-between;
      margin-bottom: 12px;
      font-size: 12px;
    }

    .slider-head span:last-child { color: var(--cyan); font-family: monospace; }

    input[type="range"] {
      width: 100%;
      accent-color: var(--blue);
      cursor: pointer;
    }

    .color-row {
      display: flex;
      gap: 9px;
      margin-top: 13px;
    }

    .swatch {
      width: 22px;
      height: 22px;
      border: 2px solid transparent;
      border-radius: 7px;
      cursor: pointer;
    }

    .swatch.selected { outline: 2px solid #eaf4ff; outline-offset: 2px; }
    .blue { background: #72c9ff; }
    .mint { background: #8ff4ee; }
    .purple { background: #b39bff; }
    .pink { background: #ff8fc8; }
    .green { background: #8dffc2; }

    .preview {
      position: relative;
      min-height: 142px;
      display: grid;
      place-items: center;
      margin-top: 11px;
      overflow: hidden;
      border: 1px solid #274057;
      border-radius: 14px;
      background:
        linear-gradient(#ffffff08 1px, transparent 1px),
        linear-gradient(90deg, #ffffff08 1px, transparent 1px),
        radial-gradient(ellipse at center, #173047, #0b1420);
      background-size: 22px 22px, 22px 22px, auto;
    }

    .preview-label {
      position: absolute;
      top: 10px;
      left: 12px;
      color: #7892aa;
      font: 10px monospace;
    }

    .target {
      position: relative;
      padding: 11px 17px;
      border: 1px solid #8ff4ee;
      border-radius: 8px;
      color: white;
      background: #08131dcc;
      box-shadow: 0 0 20px #8ff4ee35;
      font-size: 11px;
    }

    .target::before, .target::after {
      content: "";
      position: absolute;
      width: 9px;
      height: 9px;
      border-color: var(--cyan);
      border-style: solid;
    }

    .target::before { top: -4px; left: -4px; border-width: 1px 0 0 1px; }
    .target::after { right: -4px; bottom: -4px; border-width: 0 1px 1px 0; }

    .target small { display: block; margin-top: 5px; color: var(--cyan); }

    .footer {
      display: flex;
      justify-content: space-between;
      margin-top: 22px;
      color: #64788d;
      font-size: 10px;
    }

    .reset {
      border: 0;
      color: #8fb2ce;
      background: none;
      cursor: pointer;
    }

    .reset:hover { color: white; }

    @media (max-width: 680px) {
      body { padding: 10px; }
      .app { grid-template-columns: 1fr; }
      aside { padding: 15px; border-right: 0; border-bottom: 1px solid var(--line); }
      .brand { padding-bottom: 12px; }
      .nav-label, .side-status { display: none; }
      nav { display: flex; gap: 5px; overflow-x: auto; }
      .nav-btn { width: auto; white-space: nowrap; }
      main { padding: 22px 16px; }
    }

    @media (max-width: 450px) {
      .grid { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
  <div class="app">
    <aside>
      <div class="brand">
        <div class="logo">❄</div>
        <div>
          <strong>SNOW VISUAL</strong>
          <small>visual settings</small>
        </div>
      </div>

      <div class="nav-label">Меню</div>
      <nav>
        <button class="nav-btn active" data-tab="visual"><span class="nav-icon">◈</span> Визуалы</button>
        <button class="nav-btn" data-tab="players"><span class="nav-icon">♙</span> Игроки</button>
        <button class="nav-btn" data-tab="world"><span class="nav-icon">▦</span> Мир</button>
        <button class="nav-btn" data-tab="settings"><span class="nav-icon">⚙</span> Настройки</button>
      </nav>

      <div class="side-status"><span class="dot"></span>Интерфейс запущен</div>
    </aside>

    <main>
      <header>
        <div>
          <h1 id="pageTitle">Визуалы</h1>
          <div class="subtitle">Настрой внешний вид Snow Visual</div>
        </div>
        <div class="version">SNOW · 1.0</div>
      </header>

      <section class="tab-content active" id="visual">
        <div class="section-title">Отображение</div>
        <div class="grid">
          <div class="option"><div><strong>Метки игроков</strong><small>Подсветка и рамка</small></div><button class="switch on" aria-label="Метки игроков"></button></div>
          <div class="option"><div><strong>Чайна хет</strong><small>Декоративная шляпа</small></div><button class="switch on" aria-label="Чайна хет"></button></div>
          <div class="option"><div><strong>Никнеймы</strong><small>Показывать над персонажами</small></div><button class="switch on" aria-label="Никнеймы"></button></div>
          <div class="option"><div><strong>Полоска здоровья</strong><small>Индикатор рядом с целью</small></div><button class="switch" aria-label="Полоска здоровья"></button></div>
          <div class="option"><div><strong>Трассеры</strong><small>Линии до игроков</small></div><button class="switch" aria-label="Трассеры"></button></div>
          <div class="option"><div><strong>Предмет в руке</strong><small>Отображать выбранный предмет</small></div><button class="switch" aria-label="Предмет в руке"></button></div>
        </div>

        <div class="section-title">Настройка вида</div>
        <div class="slider-card">
          <div class="slider-head"><span>Размер меток</span><span id="sizeValue">65%</span></div>
          <input id="sizeSlider" type="range" min="20" max="100" value="65">
          <div class="color-row" aria-label="Цвет интерфейса">
            <button class="swatch blue selected" title="Голубой"></button>
            <button class="swatch mint" title="Мятный"></button>
            <button class="swatch purple" title="Фиолетовый"></button>
            <button class="swatch pink" title="Розовый"></button>
            <button class="swatch green" title="Зелёный"></button>
          </div>
        </div>

        <div class="preview">
          <span class="preview-label">ПРЕДПРОСМОТР · ДЕМО</span>
          <div class="target">PlayerName<small>❤ 20 · 12.4 м</small></div>
        </div>
      </section>

      <section class="tab-content" id="players">
        <div class="section-title">Игроки</div>
        <div class="grid">
          <div class="option"><div><strong>Рамка игрока</strong><small>Контур в выбранном цвете</small></div><button class="switch on"></button></div>
          <div class="option"><div><strong>Дистанция</strong><small>Расстояние до персонажа</small></div><button class="switch on"></button></div>
          <div class="option"><div><strong>Эффекты статусов</strong><small>Иконки эффектов в метке</small></div><button class="switch"></button></div>
          <div class="option"><div><strong>Анимация меток</strong><small>Плавное появление</small></div><button class="switch on"></button></div>
        </div>
      </section>

      <section class="tab-content" id="world">
        <div class="section-title">Мир</div>
        <div class="grid">
          <div class="option"><div><strong>Метки мобов</strong><small>Декоративные метки существ</small></div><button class="switch"></button></div>
          <div class="option"><div><strong>Метки предметов</strong><small>Выделение предметов на земле</small></div><button class="switch"></button></div>
          <div class="option"><div><strong>Координаты</strong><small>Панель координат в интерфейсе</small></div><button class="switch on"></button></div>
          <div class="option"><div><strong>Мини-карта</strong><small>Визуальный элемент в углу</small></div><button class="switch"></button></div>
        </div>
      </section>

      <section class="tab-content" id="settings">
        <div class="section-title">Настройки интерфейса</div>
        <div class="grid">
          <div class="option"><div><strong>Снежные частицы</strong><small>Фоновый эффект меню</small></div><button class="switch on"></button></div>
          <div class="option"><div><strong>Компактный режим</strong><small>Уменьшить отступы</small></div><button class="switch"></button></div>
          <div class="option"><div><strong>Показывать подсказки</strong><small>Короткие описания функций</small></div><button class="switch on"></button></div>
          <div class="option"><div><strong>Плавные переходы</strong><small>Анимация элементов меню</small></div><button class="switch on"></button></div>
        </div>
      </section>

      <div class="footer">
        <span>SNOW VISUAL · DEMO UI</span>
        <button class="reset" id="resetBtn">Сбросить демо</button>
      </div>
    </main>
  </div>

  <script>
    const tabNames = {
      visual: "Визуалы",
      players: "Игроки",
      world: "Мир",
      settings: "Настройки"
    };

    document.querySelectorAll(".nav-btn").forEach(button => {
      button.addEventListener("click", () => {
        document.querySelectorAll(".nav-btn").forEach(item => item.classList.remove("active"));
        document.querySelectorAll(".tab-content").forEach(item => item.classList.remove("active"));
        button.classList.add("active");
        document.getElementById(button.dataset.tab).classList.add("active");
        document.getElementById("pageTitle").textContent = tabNames[button.dataset.tab];
      });
    });

    document.querySelectorAll(".switch").forEach(toggle => {
      toggle.addEventListener("click", () => toggle.classList.toggle("on"));
    });

    document.querySelectorAll(".swatch").forEach(color => {
      color.addEventListener("click", () => {
        document.querySelectorAll(".swatch").forEach(item => item.classList.remove("selected"));
        color.classList.add("selected");
      });
    });

    const slider = document.getElementById("sizeSlider");
    slider.addEventListener("input", () => {
      document.getElementById("sizeValue").textContent = slider.value + "%";
    });

    document.getElementById("resetBtn").addEventListener("click", () => {
      document.querySelectorAll(".switch").forEach((toggle, index) => {
        toggle.classList.toggle("on", [0, 1, 2, 7, 10, 14, 15, 16].includes(index));
      });
      slider.value = 65;
      document.getElementById("sizeValue").textContent = "65%";
    });
  </script>
</body>
</html>
