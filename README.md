<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Кавказский квиз · Мозгобойня</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Montserrat', Roboto, system-ui, sans-serif;
        }

        body {
            background: #0b2f1f;  /* глубокий зелёный */
            background-image: radial-gradient(circle at 30% 40%, #1c4e3a 0%, #0a281c 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            position: relative;
        }

        /* стилизованные горы на заднем плане */
        body::before {
            content: "";
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 800" opacity="0.1"><path fill="%233d5d42" d="M0,600 L200,400 L350,550 L500,300 L700,500 L850,350 L1000,450 L1200,200 L1200,800 L0,800 Z"/><path fill="%232a4b33" d="M0,700 L150,500 L280,650 L420,450 L600,650 L780,500 L930,600 L1100,400 L1200,550 L1200,800 L0,800 Z"/><path fill="%231d3b23" d="M0,750 L100,620 L240,720 L400,550 L550,720 L720,600 L860,720 L1050,550 L1200,680 L1200,800 L0,800 Z"/></svg>') repeat-x bottom;
            background-size: 1200px 300px;
            pointer-events: none;
            z-index: 0;
        }

        .quiz-container {
            max-width: 1300px;
            width: 100%;
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border-radius: 60px 60px 40px 40px;
            box-shadow: 0 30px 50px rgba(0, 20, 5, 0.5), inset 0 2px 4px rgba(255, 255, 200, 0.3);
            border: 2px solid rgba(255, 215, 140, 0.4);
            padding: 35px;
            position: relative;
            z-index: 10;
        }

        /* декоративный элемент – солнце */
        .quiz-container::after {
            content: "☀️";
            font-size: 60px;
            position: absolute;
            top: 20px;
            right: 40px;
            opacity: 0.15;
            transform: rotate(15deg);
            pointer-events: none;
        }

        h1 {
            font-size: 3rem;
            font-weight: 800;
            color: #ffe9c7;
            text-shadow: 4px 4px 0 #3c6b4b, 8px 8px 0 rgba(0,0,0,0.2);
            margin-bottom: 15px;
            padding-left: 25px;
            letter-spacing: 2px;
            word-break: break-word;
        }

        .subtitle {
            color: #eedbba;
            font-size: 1.3rem;
            margin-bottom: 35px;
            padding-left: 33px;
            font-weight: 500;
            text-shadow: 2px 2px 0 #1e4a2e;
        }

        .round-tabs {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 30px;
            justify-content: center;
        }

        .round-btn {
            background: rgba(30, 50, 35, 0.7);
            backdrop-filter: blur(4px);
            border: 2px solid #e9c891;
            padding: 14px 28px;
            border-radius: 60px;
            font-weight: 700;
            font-size: 1.2rem;
            color: #fef5e1;
            cursor: pointer;
            transition: 0.3s;
            box-shadow: 0 6px 0 #2c5438;
            text-transform: uppercase;
            letter-spacing: 1px;
            flex: 0 1 auto;
        }

        .round-btn.active {
            background: #e5b05f;
            color: #1e3d2a;
            border-color: #ffd78c;
            box-shadow: 0 8px 0 #7b4f1e;
            transform: translateY(-2px);
        }

        .round-btn:hover {
            background: #4f7b5f;
            border-color: #fde3b5;
            transform: translateY(-3px);
            box-shadow: 0 9px 0 #2b4f33;
        }

        .score-panel {
            background: rgba(20, 45, 30, 0.7);
            backdrop-filter: blur(8px);
            border-radius: 80px;
            padding: 18px 32px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 45px;
            border: 2px solid #cfb175;
            box-shadow: inset 0 2px 5px #b9944e, 0 10px 15px rgba(0,0,0,0.3);
            flex-wrap: wrap;
            gap: 20px;
        }

        .total-score {
            font-size: 1.9rem;
            font-weight: 700;
            color: #f7e9cf;
            text-shadow: 2px 2px 0 #40674a;
        }

        .total-score span {
            color: #ffbc6e;
            font-size: 2.5rem;
            margin-left: 15px;
            font-weight: 900;
            text-shadow: 3px 3px 0 #694e1f;
        }

        .action-buttons {
            display: flex;
            gap: 18px;
            flex-wrap: wrap;
        }

        .btn {
            border: none;
            padding: 14px 34px;
            border-radius: 50px;
            font-weight: 700;
            font-size: 1.2rem;
            cursor: pointer;
            transition: 0.2s;
            border: 2px solid transparent;
            letter-spacing: 1px;
        }

        .btn-check {
            background: #f4b643;
            color: #1f452b;
            box-shadow: 0 7px 0 #9e701f;
            border-color: #ffe1a3;
        }

        .btn-check:hover {
            background: #ffcc6a;
            transform: translateY(-3px);
            box-shadow: 0 10px 0 #9e701f;
        }

        .btn-reset {
            background: #4f6b5a;
            color: #fef7e6;
            box-shadow: 0 7px 0 #2c4a38;
            border-color: #b1aa8b;
        }

        .btn-reset:hover {
            background: #658b74;
            transform: translateY(-3px);
            box-shadow: 0 10px 0 #2c4a38;
        }

        .round-title {
            font-size: 2.5rem;
            font-weight: 800;
            margin-bottom: 35px;
            color: #fff3d3;
            text-shadow: 3px 3px 0 #2d633b, 6px 6px 0 #00000040;
            display: flex;
            align-items: center;
            gap: 20px;
            flex-wrap: wrap;
        }

        .round-title span {
            background: #c19242;
            color: #102015;
            padding: 10px 28px;
            border-radius: 60px;
            font-size: 1.8rem;
            box-shadow: inset 0 -3px 0 #614b24, 0 8px 0 #3d5a45;
        }

        .questions-grid {
            display: flex;
            flex-direction: column;
            gap: 40px;
            margin-bottom: 50px;
        }

        .question-card {
            background: rgba(255, 250, 235, 0.85);
            backdrop-filter: blur(5px);
            border-radius: 50px;
            padding: 30px 35px;
            box-shadow: 0 20px 30px rgba(0, 20, 0, 0.5), inset 0 0 0 2px #ffeecc, inset 0 0 20px #b3a577;
            border: 1px solid #cfb27e;
            transition: 0.3s;
        }

        .question-card:hover {
            box-shadow: 0 25px 40px rgba(0, 0, 0, 0.6), inset 0 0 0 3px #fce3b5;
            transform: scale(1.01);
            background: rgba(255, 252, 240, 0.95);
        }

        .question-text {
            font-weight: 700;
            font-size: 1.7rem;
            margin-bottom: 25px;
            color: #1d3929;
            text-shadow: 2px 2px 0 #e5d7b0;
            padding-left: 15px;
            border-left: 12px solid #c5963f;
        }

        .media-content {
            margin: 25px 0;
            text-align: center;
            background: #2f4d38;
            padding: 15px;
            border-radius: 40px;
            box-shadow: inset 0 0 20px #1c2f20, 0 10px 10px rgba(0,0,0,0.3);
        }

        .media-content img {
            max-width: 100%;
            max-height: 350px;
            border-radius: 30px;
            border: 5px solid #b99e5d;
            box-shadow: 0 10px 25px black;
            object-fit: cover;
        }

        .media-content iframe {
            width: 100%;
            max-width: 700px;
            height: 380px;
            border-radius: 30px;
            border: 5px solid #b99e5d;
            box-shadow: 0 10px 25px black;
        }

        /* варианты ответов столбиком, без бейджей */
        .options {
            display: flex;
            flex-direction: column;
            gap: 16px;
            margin-top: 20px;
        }

        .option-item {
            background: #fcf5e6;
            border: 3px solid #b38633;
            border-radius: 50px;
            padding: 18px 28px;
            display: flex;
            align-items: center;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 7px 0 #6f5429;
            font-size: 1.2rem;
            font-weight: 500;
            color: #202f1c;
        }

        .option-item.selected {
            background: #fff1cc;
            border-color: #e5b05f;
            box-shadow: 0 7px 0 #b87e2e;
            transform: translateY(-2px);
        }

        .option-item.correct-answer {
            background: #b9e6b9;
            border-color: #1f9e4a;
            box-shadow: 0 7px 0 #0f722f;
        }

        .option-item.incorrect-answer {
            background: #fbc1c1;
            border-color: #c53a3a;
            box-shadow: 0 7px 0 #922020;
        }

        .option-item input[type="radio"] {
            appearance: none;
            width: 28px;
            height: 28px;
            border: 3px solid #a57337;
            border-radius: 50%;
            margin-right: 25px;
            position: relative;
            flex-shrink: 0;
            background: #fffbee;
            transition: 0.1s;
        }

        .option-item input[type="radio"]:checked {
            border-color: #b5540e;
            background: #d68d44;
            box-shadow: inset 0 0 0 6px #ffeedd;
        }

        .option-item input[type="radio"]:disabled {
            opacity: 0.7;
        }

        .option-label {
            font-size: 1.25rem;
            line-height: 1.4;
            color: #1f3d2b;
            font-weight: 600;
        }

        /* поля ввода (для раундов 3,4,5) */
        .input-group {
            margin-top: 20px;
            display: flex;
            flex-direction: column;
            gap: 18px;
        }

        .input-field {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 15px;
            background: #f7efda;
            border-radius: 50px;
            padding: 10px 25px;
            border: 3px solid #ba8d48;
            box-shadow: inset 0 2px 5px #836e3e, 0 6px 0 #66522b;
        }

        .input-field label {
            font-weight: 700;
            color: #2d4e32;
            min-width: 130px;
            font-size: 1.2rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .input-field input {
            flex: 1;
            border: none;
            background: transparent;
            padding: 15px 8px;
            font-size: 1.2rem;
            outline: none;
            border-bottom: 3px solid transparent;
            transition: 0.2s;
            color: #0e2f1c;
            font-weight: 600;
        }

        .input-field input:focus {
            border-bottom-color: #d99f4c;
        }

        .input-field.correct-answer {
            background: #c8eac8;
            border-color: #2a9134;
            box-shadow: inset 0 2px 5px #377e3a, 0 6px 0 #1d6723;
        }

        .input-field.incorrect-answer {
            background: #fad1d1;
            border-color: #c73b3b;
            box-shadow: inset 0 2px 5px #a14242, 0 6px 0 #942b2b;
        }

        .correct-badge, .incorrect-badge {
            margin-left: auto;
            font-weight: 700;
            font-size: 1.1rem;
            padding: 5px 15px;
            border-radius: 40px;
            white-space: nowrap;
        }
        .correct-badge { background: #1d8b3c; color: white; }
        .incorrect-badge { background: #b33c3c; color: white; }

        .round-result {
            background: #2e5b41e0;
            backdrop-filter: blur(6px);
            border-radius: 60px;
            padding: 25px 35px;
            text-align: center;
            font-size: 2rem;
            font-weight: 700;
            color: #f9f0ce;
            border: 3px solid #eac175;
            box-shadow: 0 15px 20px black;
            margin-top: 40px;
        }

        .round-result span {
            color: #ffd78c;
            font-size: 2.8rem;
            margin: 0 15px;
            text-shadow: 3px 3px 0 #333;
        }

        footer {
            margin-top: 45px;
            color: #d4c8a8;
            text-align: center;
            font-size: 1rem;
            text-shadow: 1px 1px 0 #1f4a2d;
        }

        @media (max-width: 700px) {
            .quiz-container { padding: 20px; }
            h1 { font-size: 2.5rem; }
            .round-btn { font-size: 1rem; padding: 12px 18px; }
            .question-text { font-size: 1.3rem; }
            .option-item { padding: 15px 20px; font-size: 1rem; }
            .option-label { font-size: 1rem; }
            .input-field { flex-direction: column; align-items: stretch; }
            .input-field label { min-width: auto; }
        }
    </style>
</head>
<body>
<div class="quiz-container" id="quizContainer">
    <h1>⛰️ КАВКАЗ · МОЗГОБОЙНЯ</h1>
    <div class="subtitle">5 раундов · 35 вопросов · погружение в горы</div>

    <div class="round-tabs" id="roundTabs"></div>

    <div class="score-panel">
        <div class="total-score">🏔️ ВЕРШИНЫ ВЗЯТО: <span id="totalScoreDisplay">0</span></div>
        <div class="action-buttons">
            <button class="btn btn-check" id="checkRoundBtn">✅ ПРОВЕРИТЬ РАУНД</button>
            <button class="btn btn-reset" id="resetRoundBtn">🔄 СБРОС</button>
        </div>
    </div>

    <div class="round-title" id="roundTitle"></div>
    <div id="questionsContainer" class="questions-grid"></div>
    <div id="roundResult" class="round-result" style="display: none;"></div>

    <footer>атмосфера гор · каждый ответ приближает к Эльбрусу</footer>
</div>

<script>
(function() {
    // ===================== ДАННЫЕ =====================
    const rounds = [
        // раунд 1: обзорный (choice)
        { 
            name: 'РАУНД 1 · ОБЗОРНЫЙ',
            type: 'choice',
            questions: [
                { text: 'Почему в горах часто зарождаются романтические отношения?', options: [
                    'А) В тесной кабинке подъёмника — хочешь не хочешь, познакомишься',
                    'Б) Инструкторы по сноуборду носят очень облегающие костюмы',
                    'В) Совместное падение в снег сближает быстрее Tinder',
                    'Г) Особая атмосфера и высота обостряют чувства'
                ], correct: 3 },
                { text: 'В каком историческом периоде процветала цивилизация в районе Архыза?', options: [
                    'А) X–XIII вв.', 'Б) XV–XVI вв.', 'В) XVIII в.', 'Г) XIX в.'
                ], correct: 0 },
                { text: 'Что является главной особенностью древних храмов Архыза?', options: [
                    'А) Богатое убранство', 'Б) Древность и простота',
                    'В) Золотые украшения', 'Г) Необычная форма куполов'
                ], correct: 1 },
                { text: 'Что делает курорт Архыз привлекательным для инвесторов?', options: [
                    'А) Близость к морю', 'Б) Памятники',
                    'В) Стратегическое расположение', 'Г) Тёплый климат'
                ], correct: 2 },
                { text: 'Что делает землю у подъёмников особенно ценной?', options: [
                    'А) Плодородность', 'Б) Близость к подъёмникам',
                    'В) Памятники', 'Г) Виды'
                ], correct: 1 },
                { text: 'Какой вопрос на Кавказе звучит чаще, чем «Сколько ты зарабатываешь?»', options: [
                    'А) «Кто ты?» / «Чьё слово держишь?»', 'Б) «Какая машина?»',
                    'В) «Где отдыхал?»', 'Г) «Сколько недвижимости?»'
                ], correct: 0 },
                { text: 'Что аланы спрятали в пещерах перед нашествием?', options: [
                    'А) Священные книги', 'Б) Оружие',
                    'В) Останки царей', 'Г) Золото и сокровища'
                ], correct: 3 }
            ]
        },
        // раунд 2: визуальный (choice)
        {
            name: 'РАУНД 2 · ВИЗУАЛЬНЫЙ',
            type: 'choice',
            questions: [
                { text: 'В чём живут вахтовики на Севере?', image: 'https://sun9-83.userapi.com/s/v1/ig2/4q1xlU7uxwh0m61oJhXkSspXWb1l59tl4OY3wBB_09bDT0BAnh_fGSdTkFlSxOhKCYAnSrZXyCVuxEKCaKpH02v4.jpg?quality=95&as=32x18,48x27,72x40,108x61,160x90,240x135,360x202,480x270,540x304,640x360,720x405,1080x607,1280x720&from=bu&cs=1280x0', options: ['А) Общежития', 'Б) Контейнеры', 'В) Палатки', 'Г) Землянки'], correct: 1 },
                { text: 'О каких храмах речь (Северный, Средний, Южный)?', image: 'https://sun9-27.userapi.com/s/v1/ig2/FXCwdTi8Hbf4CcGtmOD2Itn12WQcla_mCd39Hq6OJ9jcfl4uDdbX8F7_lQGwK-zrGTuD54ksZ3fydIRZpwh6YZmo.jpg?quality=95&as=32x18,48x27,72x40,108x61,160x90,240x135,360x202,480x270,540x304,640x360,720x405,1080x607,1280x720&from=bu&cs=1280x0', options: ['А) Петропавловский и др.', 'Б) Старый, Новый, Забытый', 'В) Северный, Средний, Южный', 'Г) Византийский, Аланский, Хазарский'], correct: 2 },
                { text: 'Чем для алан были горы на торговых путях (кроме дохода)?', image: 'https://sun9-32.userapi.com/s/v1/ig2/aBt_mw-d45qFaqXxCNlN-evwEycrFDNK5G0iBoDFYLKhPDtcESKO0W0d6Q2r0Kg7MRn-nSn14sz8WlcWWkX-9SnQ.jpg?quality=95&as=32x18,48x27,72x40,108x61,160x90,240x135,360x202,480x270,540x304,640x360,720x405,1080x607,1280x720&from=bu&cs=1280x0', options: ['А) Препятствие', 'Б) Религиозный центр', 'В) Место засад', 'Г) Защита'], correct: 3 },
                { text: 'Условие окончательности решения в традиц. обществе?', image: 'https://sun9-22.userapi.com/s/v1/ig2/AMRgG3CCZotD9_o3mIRtu39J-cKEuxLIYijfhLZWnmNS7iLvjo1gwXIlokwlKe48y1cWYE19QApLlFxpV66waZVV.jpg?quality=95&as=32x18,48x27,72x40,108x61,160x90,240x135,360x202,480x270,540x304,640x360,720x405,1080x607,1280x720&from=bu&cs=1280x0', options: ['А) Принято уважаемыми людьми, не обсуждалось', 'Б) Запись с печатью', 'В) Кровная клятва', 'Г) Одобрено большинством'], correct: 0 },
                { text: 'Рациональное объяснение странных явлений (пастухи)?', image: 'https://sun9-15.userapi.com/s/v1/ig2/Ouy0ZkTtQCTkX7l_3noOlL2ksWi6C6ErCm0TvBVhD5PpfCZjmm7kF-3FrTsDP0IleB1s3rlFiZzrlsmVCY3WXMht.jpg?quality=95&as=32x18,48x27,72x40,108x61,160x90,240x135,360x202,480x270,540x304,640x360,720x405,1080x607,1280x720&from=bu&cs=1280x0', options: ['А) Свет фар', 'Б) Ветер, туман, игра света', 'В) Костры', 'Г) Отблески снега'], correct: 1 },
                { text: 'Зарождающаяся традиция в Архызе?', image: 'https://sun9-33.userapi.com/s/v1/ig2/J_tYtiYu-1WjTO8ZxjcXLCMZ1IvaXRlsZHE69_kv8xmVNtjvN0H5fNZwjRnZfFO0wFtC7k4aJB8R4jEIJ3cVJOwH.jpg?quality=95&as=32x18,48x27,72x40,108x61,160x90,240x135,360x202,480x270,540x304,640x360,720x405,1080x607,1280x720&from=bu&cs=1280x0', options: ['А) Замочки', 'Б) Венчания в храмах', 'В) Катание с невестой', 'Г) Предложение на склоне'], correct: 3 },
                { text: 'Что находят учёные (труднообъяснимое)?', image: 'https://sun9-31.userapi.com/s/v1/ig2/tDuLHk59U6OHUxQo5B1-rVS7jTcNMIjtQknOo9cmZqzTbR9M3jcfuSXfPyC3Rbhh-iPXJL1fWpww76LCoUU1b1Hd.jpg?quality=95&as=32x18,48x27,72x40,108x61,160x90,240x135,360x202,480x270,540x304,640x360,720x405,1080x607,1280x720&from=bu&cs=1280x0', options: ['А) Предметы быта в неожиданных местах', 'Б) Каменные плиты', 'В) Византийская посуда', 'Г) Золото'], correct: 0 }
            ]
        },
        // раунд 3: музыкальный (два текстовых поля)
        {
            name: 'РАУНД 3 · МУЗЫКАЛЬНЫЙ',
            type: 'multi-text',
            questions: [
                { text: 'Трек 1', iframe: '<iframe width="720" height="405" src="https://rutube.ru/play/embed/8e2308d20b8447fd7d5c1613e6f3d991/?p=4lwEaCd2S_Vjn5YbwdIQMA" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>', fields: [
                    { label: 'Название', correct: 'Чёрные глаза' },
                    { label: 'Исполнитель', correct: 'Айдамир Мугу' }
                ]},
                { text: 'Трек 2', iframe: '<iframe width="720" height="405" src="https://rutube.ru/play/embed/d11393d6d569805ad6da57b0fb3559f4/?p=A0mqaGqWTE-yyDr9p6dIQQ" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>', fields: [
                    { label: 'Название', correct: 'Возьми меня в Балкарию' },
                    { label: 'Исполнитель', correct: 'Алим Газаев' }
                ]},
                { text: 'Трек 3', iframe: '<iframe width="720" height="405" src="https://rutube.ru/play/embed/00571a7e20b0c512feefb28af10183a8/?p=1DImK_b1-lC1KdZoIpP3cg" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>', fields: [
                    { label: 'Название', correct: 'Кобра' },
                    { label: 'Исполнитель', correct: 'Ислам Итляшев' }
                ]},
                { text: 'Трек 4', iframe: '<iframe width="720" height="405" src="https://rutube.ru/play/embed/274132a1b74e4be4f3270be1f2417c0e/?p=4FfE4ffQt11Xrm5Hsxhsew" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>', fields: [
                    { label: 'Название', correct: 'Калым' },
                    { label: 'Исполнитель', correct: 'Мурат Тхагалегов' }
                ]},
                { text: 'Трек 5', iframe: '<iframe width="720" height="405" src="https://rutube.ru/play/embed/30d6a8120e4e773b1848db7e172824d0/?p=exAQqlb7R9s_YsE6z-1Jcg" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>', fields: [
                    { label: 'Название', correct: 'Что же ты медлишь' },
                    { label: 'Исполнитель', correct: 'Муслим Магомаев, Константин Кримец' }
                ]},
                { text: 'Трек 6', iframe: '<iframe width="720" height="405" src="https://rutube.ru/play/embed/cc5038d6c4612643404c12af508ecea3/?p=ddS2N9Cm1y5A1PcONue5jg" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>', fields: [
                    { label: 'Название', correct: 'Горячая, гремучая' },
                    { label: 'Исполнитель', correct: 'Султан Лагучев' }
                ]},
                { text: 'Трек 7', iframe: '<iframe width="720" height="405" src="https://rutube.ru/play/embed/9249e6e2507ff381ec0fbe20e175d3b3/?p=ZWxyN3geE2MKEGVKeqf2lA" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>', fields: [
                    { label: 'Название', correct: 'Да, да, да - это Кавказ' },
                    { label: 'Исполнитель', correct: 'Шамхан Далдаев' }
                ]}
            ]
        },
        // раунд 4: ребусы (текстовый ввод)
        {
            name: 'РАУНД 4 · РЕБУСЫ',
            type: 'text',
            questions: [
                { text: 'Что зашифровано?', image: 'https://sun9-48.userapi.com/s/v1/ig2/6xSJcW51q8H8RtvwncXpi4QMFhV8TEJb8JCpQWVvC5L2XI01qaKSdT7VUBEvgBJOJyQCiEKFta2q4i0V05Hblbj9.jpg?quality=95&as=32x30,48x46,72x68,108x103,160x152,200x190&from=bu&cs=200x0', correct: 'Нягань' },
                { text: 'Что зашифровано?', image: 'https://sun9-70.userapi.com/s/v1/ig2/WxylH2KUshh08dj1bVtweh8OlNU9CdbPjoczJRIencQkAQFKu6YswZeRlAzbKK78Uhlj0NlApEQzciXgPllQWyAQ.jpg?quality=95&as=32x16,48x24,72x36,108x54,160x80,240x120,360x180,380x190&from=bu&cs=380x0', correct: 'Кавказ' },
                { text: 'Что зашифровано?', image: 'https://sun9-60.userapi.com/s/v1/ig2/l4L18ESTuRA1uruk7ApX8-8OCb1ZngKq-oYt9MP5Y9obJ994-J2peu6S-7PU0zA3ot1ZeVzXHjE0yYMeS-caXtxT.jpg?quality=95&as=32x10,48x15,72x23,108x34,160x51,240x76,360x114,480x152,540x171,601x190&from=bu&cs=601x0', correct: 'Курорт' },
                { text: 'Что зашифровано?', image: 'https://sun9-87.userapi.com/s/v1/ig2/bCJIQP0FDAFW2iV3E63w3tjVMb1vUBuXzel6aDFTdLAe_xIRIWSUo_DjAah6o7nO_kUtrwl_vizHdk9qrJoPfpEx.jpg?quality=95&as=32x14,48x21,72x32,108x47,160x70,240x106,360x158,432x190&from=bu&cs=432x0', correct: 'Византия' },
                { text: 'Что зашифровано?', image: 'https://sun9-1.userapi.com/s/v1/ig2/VHH020D0eiCYVh8RydTcKNTiDOamopVmZxCuS4XJpK_LMTe_p3qhQqu3KSTa9x42bmpmXOtb8NhJC-JwRE_fbN8Z.jpg?quality=95&as=32x14,48x21,72x31,108x47,160x69,240x103,360x155,441x190&from=bu&cs=441x0', correct: 'Архыз' },
                { text: 'Что зашифровано?', image: 'https://sun9-21.userapi.com/s/v1/ig2/g_uihrYlkPO5Z0fCu83QHk04cakdMZx3Xn1C8LNZokSz3bhw7GGVPQ0JDMOlJddeL4AOkmb03G3csaAdLBMk0vyw.jpg?quality=95&as=32x10,48x15,72x22,108x33,160x49,240x74,360x110,480x147,540x166,619x190&from=bu&cs=619x0', correct: 'Вдохновение' },
                { text: 'Что зашифровано?', image: 'https://sun9-45.userapi.com/s/v1/ig2/-daPuFV3uZzV6SNG0afJBYgqaRHDIM_2vX1OmtT_OvjgYymQXkWXQgQWHy6WD4q0eJn65mVPtS5__jrC5W_y3uXW.jpg?quality=95&as=32x19,48x29,72x43,108x64,160x95,240x143,319x190&from=bu&cs=319x0', correct: 'Пейзаж' }
            ]
        },
        // раунд 5: лестница (текстовый ввод)
        {
            name: 'РАУНД 5 · ЛЕСТНИЦА',
            type: 'text',
            questions: [
                { text: '3 буквы. Что стоит за человеком на Кавказе?', correct: 'род' },
                { text: '4 буквы. Древняя христианская постройка в Архызе', correct: 'храм' },
                { text: '5 букв. Как называют древних жителей этих мест?', correct: 'аланы' },
                { text: '6 букв. Что в горах находят туристы?', correct: 'тишину' },
                { text: '7 букв. Точка, с которой мир кажется больше', correct: 'вершина' },
                { text: '8 букв. Какой ветер закаляет характер?', correct: 'северный' },
                { text: '9 букв. Непродаваемая ценность кавказских народов', correct: 'репутация' }
            ]
        }
    ];

    // Хранилище ответов. Для choice – число (индекс), для text – строка, для multi-text – массив строк (по полям)
    let userAnswers = rounds.map(r => {
        if (r.type === 'choice') return Array(r.questions.length).fill(null);
        else if (r.type === 'text') return Array(r.questions.length).fill('');
        else if (r.type === 'multi-text') return Array(r.questions.length).fill().map(() => Array(r.questions[0].fields.length).fill(''));
    });

    let currentRound = 0;
    let roundChecked = false; // был ли текущий раунд проверен
    let totalCorrect = 0;

    // DOM
    const roundTabsDiv = document.getElementById('roundTabs');
    const roundTitleDiv = document.getElementById('roundTitle');
    const questionsContainer = document.getElementById('questionsContainer');
    const totalScoreSpan = document.getElementById('totalScoreDisplay');
    const roundResultDiv = document.getElementById('roundResult');
    const checkBtn = document.getElementById('checkRoundBtn');
    const resetBtn = document.getElementById('resetRoundBtn');

    // Подсчёт общего количества правильных ответов
    function recalcTotalScore() {
        let total = 0;
        for (let r = 0; r < rounds.length; r++) {
            const round = rounds[r];
            for (let q = 0; q < round.questions.length; q++) {
                const ans = userAnswers[r][q];
                if (ans === null || ans === '') continue;
                if (round.type === 'choice') {
                    if (ans === round.questions[q].correct) total++;
                } else if (round.type === 'text') {
                    if (ans.trim().toLowerCase() === round.questions[q].correct.toLowerCase()) total++;
                } else if (round.type === 'multi-text') {
                    const fields = round.questions[q].fields;
                    for (let f = 0; f < fields.length; f++) {
                        if (ans[f] && ans[f].trim().toLowerCase() === fields[f].correct.toLowerCase()) total++;
                    }
                }
            }
        }
        totalCorrect = total;
        totalScoreSpan.innerText = totalCorrect;
    }

    // Отрисовка табов
    function renderTabs() {
        roundTabsDiv.innerHTML = '';
        rounds.forEach((round, idx) => {
            const btn = document.createElement('button');
            btn.className = `round-btn ${idx === currentRound ? 'active' : ''}`;
            btn.innerText = round.name;
            btn.dataset.round = idx;
            btn.addEventListener('click', () => {
                currentRound = idx;
                roundChecked = false;
                roundResultDiv.style.display = 'none';
                renderTabs();
                renderCurrentRound();
            });
            roundTabsDiv.appendChild(btn);
        });
    }

    // Отрисовка текущего раунда
    function renderCurrentRound() {
        const round = rounds[currentRound];
        roundTitleDiv.innerHTML = `<span>⚡</span> ${round.name}`;

        let html = '';
        round.questions.forEach((q, qIdx) => {
            html += `<div class="question-card" id="q-${qIdx}" data-qindex="${qIdx}">`;
            html += `<div class="question-text">${qIdx+1}. ${q.text}</div>`;

            if (q.image) {
                html += `<div class="media-content"><img src="${q.image}" alt="иллюстрация" loading="lazy"></div>`;
            } else if (q.iframe) {
                html += `<div class="media-content">${q.iframe}</div>`;
            }

            // Варианты ввода в зависимости от типа раунда
            if (round.type === 'choice') {
                html += `<div class="options">`;
                q.options.forEach((opt, optIdx) => {
                    const selected = userAnswers[currentRound][qIdx];
                    let optionClass = 'option-item';
                    if (selected === optIdx) optionClass += ' selected';
                    if (roundChecked) {
                        if (optIdx === q.correct) optionClass += ' correct-answer';
                        if (selected === optIdx && selected !== q.correct) optionClass += ' incorrect-answer';
                    }
                    const checkedAttr = (selected === optIdx) ? 'checked' : '';
                    const disabledAttr = roundChecked ? 'disabled' : '';
                    html += `
                        <label class="${optionClass}" data-q="${qIdx}" data-opt="${optIdx}">
                            <input type="radio" name="q${qIdx}" value="${optIdx}" ${checkedAttr} ${disabledAttr}>
                            <span class="option-label">${opt}</span>
                        </label>
                    `;
                });
                html += `</div>`;
            }
            else if (round.type === 'text') {
                const answer = userAnswers[currentRound][qIdx] || '';
                const disabled = roundChecked ? 'disabled' : '';
                const isCorrect = roundChecked && answer.trim().toLowerCase() === q.correct.toLowerCase();
                const isWrong = roundChecked && !isCorrect && answer.trim() !== '';
                let fieldClass = 'input-field';
                if (isCorrect) fieldClass += ' correct-answer';
                if (isWrong) fieldClass += ' incorrect-answer';
                html += `<div class="input-group">`;
                html += `<div class="${fieldClass}">`;
                html += `<label>Ответ:</label>`;
                html += `<input type="text" value="${answer.replace(/"/g, '&quot;')}" ${disabled} data-q="${qIdx}" data-field="0" placeholder="введите ответ">`;
                if (roundChecked) {
                    if (isCorrect) html += `<span class="correct-badge">✓ верно</span>`;
                    else if (isWrong) html += `<span class="incorrect-badge">✗ правильно: ${q.correct}</span>`;
                    else if (answer.trim() === '') html += `<span class="incorrect-badge">✗ нужно: ${q.correct}</span>`;
                }
                html += `</div></div>`;
            }
            else if (round.type === 'multi-text') {
                const answers = userAnswers[currentRound][qIdx] || Array(q.fields.length).fill('');
                const disabled = roundChecked ? 'disabled' : '';
                html += `<div class="input-group">`;
                q.fields.forEach((field, fIdx) => {
                    const val = answers[fIdx] || '';
                    const isCorrect = roundChecked && val.trim().toLowerCase() === field.correct.toLowerCase();
                    const isWrong = roundChecked && !isCorrect && val.trim() !== '';
                    let fieldClass = 'input-field';
                    if (isCorrect) fieldClass += ' correct-answer';
                    if (isWrong) fieldClass += ' incorrect-answer';
                    html += `<div class="${fieldClass}">`;
                    html += `<label>${field.label}:</label>`;
                    html += `<input type="text" value="${val.replace(/"/g, '&quot;')}" ${disabled} data-q="${qIdx}" data-field="${fIdx}" placeholder="введите ${field.label}">`;
                    if (roundChecked) {
                        if (isCorrect) html += `<span class="correct-badge">✓ верно</span>`;
                        else if (isWrong) html += `<span class="incorrect-badge">✗ правильно: ${field.correct}</span>`;
                        else if (val.trim() === '') html += `<span class="incorrect-badge">✗ нужно: ${field.correct}</span>`;
                    }
                    html += `</div>`;
                });
                html += `</div>`;
            }
            html += `</div>`;
        });

        questionsContainer.innerHTML = html;

        // Если раунд не проверен — добавляем слушатели на поля ввода
        if (!roundChecked) {
            if (round.type === 'choice') {
                document.querySelectorAll('.option-item input[type=radio]').forEach(radio => {
                    radio.addEventListener('change', (e) => {
                        const label = e.target.closest('.option-item');
                        const qIdx = parseInt(label.dataset.q);
                        const optIdx = parseInt(label.dataset.opt);
                        userAnswers[currentRound][qIdx] = optIdx;
                        document.querySelectorAll(`.option-item[data-q="${qIdx}"]`).forEach(el => {
                            el.classList.remove('selected');
                        });
                        label.classList.add('selected');
                        recalcTotalScore();
                    });
                });
            } else {
                document.querySelectorAll('.input-field input').forEach(input => {
                    input.addEventListener('input', (e) => {
                        const qIdx = parseInt(e.target.dataset.q);
                        const fieldIdx = e.target.dataset.field;
                        const value = e.target.value;
                        if (round.type === 'text') {
                            userAnswers[currentRound][qIdx] = value;
                        } else if (round.type === 'multi-text') {
                            if (!userAnswers[currentRound][qIdx]) userAnswers[currentRound][qIdx] = Array(round.questions[qIdx].fields.length).fill('');
                            userAnswers[currentRound][qIdx][fieldIdx] = value;
                        }
                        recalcTotalScore();
                    });
                });
            }
        }

        if (roundChecked) {
            const correctInRound = countCorrectInRound(currentRound);
            const maxInRound = getMaxScoreInRound(currentRound);
            roundResultDiv.style.display = 'block';
            roundResultDiv.innerHTML = `🏔️ РЕЗУЛЬТАТ РАУНДА: <span>${correctInRound}/${maxInRound}</span> ПРАВИЛЬНЫХ`;
        } else {
            roundResultDiv.style.display = 'none';
        }
    }

    function countCorrectInRound(roundIdx) {
        const round = rounds[roundIdx];
        let count = 0;
        round.questions.forEach((q, qIdx) => {
            const ans = userAnswers[roundIdx][qIdx];
            if (round.type === 'choice') {
                if (ans !== null && ans === q.correct) count++;
            } else if (round.type === 'text') {
                if (ans && ans.trim().toLowerCase() === q.correct.toLowerCase()) count++;
            } else if (round.type === 'multi-text') {
                if (Array.isArray(ans)) {
                    q.fields.forEach((field, fIdx) => {
                        if (ans[fIdx] && ans[fIdx].trim().toLowerCase() === field.correct.toLowerCase()) count++;
                    });
                }
            }
        });
        return count;
    }

    function getMaxScoreInRound(roundIdx) {
        const round = rounds[roundIdx];
        if (round.type === 'choice' || round.type === 'text') return round.questions.length;
        else if (round.type === 'multi-text') {
            return round.questions.reduce((acc, q) => acc + q.fields.length, 0);
        }
        return 0;
    }

    function checkRound() {
        roundChecked = true;
        renderCurrentRound();
        recalcTotalScore();
    }

    function resetRound() {
        const round = rounds[currentRound];
        if (round.type === 'choice') {
            userAnswers[currentRound] = Array(round.questions.length).fill(null);
        } else if (round.type === 'text') {
            userAnswers[currentRound] = Array(round.questions.length).fill('');
        } else if (round.type === 'multi-text') {
            userAnswers[currentRound] = Array(round.questions.length).fill().map(() => Array(round.questions[0].fields.length).fill(''));
        }
        roundChecked = false;
        roundResultDiv.style.display = 'none';
        renderCurrentRound();
        recalcTotalScore();
    }

    function init() {
        renderTabs();
        renderCurrentRound();
        recalcTotalScore();
        checkBtn.addEventListener('click', checkRound);
        resetBtn.addEventListener('click', resetRound);
    }

    init();
})();
</script>
</body>
</html>
