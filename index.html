<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RGB_PIG // 01</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #050505;
            color: #ffffff;
            font-family: 'Courier New', Courier, monospace;
            height: 100vh;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }

        /* Эффект старого монитора (сканлайны) */
        body::after {
            content: "";
            position: absolute;
            inset: 0;
            background: repeating-linear-gradient(
                0deg,
                rgba(0, 0, 0, 0.25) 0px,
                rgba(0, 0, 0, 0.25) 1px,
                transparent 1px,
                transparent 3px
            );
            pointer-events: none;
            z-index: 10;
        }

        /* Кнопка со сдвигом RGB красок */
        #start-btn {
            position: relative;
            z-index: 5;
            padding: 22px 54px;
            font-size: 28px;
            font-weight: 900;
            font-family: inherit;
            letter-spacing: 6px;
            color: #fff;
            background: #080808;
            border: 2px solid #fff;
            cursor: pointer;
            text-transform: uppercase;
            box-shadow: -5px 0 0 #ff003c, 5px 0 0 #00f0ff, 0 0 25px rgba(255, 0, 60, 0.3);
            text-shadow: -2px 0 #ff003c, 2px 0 #00f0ff;
            transition: transform 0.1s ease;
            animation: idle-glitch 3s infinite;
        }

        #start-btn:hover {
            animation: hard-glitch 0.25s infinite;
            background: #111;
        }

        #start-btn:active {
            transform: scale(0.95);
        }

        /* Холст для 3D свиньи */
        canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: none;
            z-index: 2;
        }

        /* Подсказка снизу */
        #hint {
            position: absolute;
            bottom: 20px;
            font-size: 12px;
            letter-spacing: 2px;
            color: #666;
            text-shadow: -1px 0 #ff003c, 1px 0 #00f0ff;
            display: none;
            z-index: 5;
            pointer-events: none;
        }

        @keyframes idle-glitch {
            0%, 92%, 100% {
                box-shadow: -4px 0 0 #ff003c, 4px 0 0 #00f0ff;
                text-shadow: -2px 0 #ff003c, 2px 0 #00f0ff;
            }
            94% {
                box-shadow: 6px -2px 0 #ff003c, -6px 2px 0 #00f0ff;
                text-shadow: 3px 0 #00ff41, -3px 0 #ff003c;
                transform: translate(-2px, 1px);
            }
            96% {
                box-shadow: -6px 2px 0 #00ff41, 6px -2px 0 #ff003c;
                transform: translate(2px, -1px);
            }
        }

        @keyframes hard-glitch {
            0% {
                transform: translate(0);
                box-shadow: -6px 0 0 #ff003c, 6px 0 0 #00f0ff;
            }
            25% {
                transform: translate(-3px, 2px);
                box-shadow: 7px -2px 0 #00ff41, -7px 2px 0 #ff003c;
            }
            50% {
                transform: translate(3px, -2px);
                box-shadow: -5px 3px 0 #00f0ff, 5px -3px 0 #ff003c;
            }
            75% {
                transform: translate(-2px, -2px);
                box-shadow: 6px 0 0 #ff003c, -6px 0 0 #00ff41;
            }
            100% {
                transform: translate(0);
            }
        }
    </style>
</head>
<body>

    <button id="start-btn">НАЖМИ</button>
    <div id="hint">[ ДВИГАЙ МЫШЬЮ ДЛЯ ВРАЩЕНИЯ // СКРОЛЛ ДЛЯ ЗУМА ]</div>
    <canvas id="scene"></canvas>

    <script>
        const btn = document.getElementById('start-btn');
        const canvas = document.getElementById('scene');
        const hint = document.getElementById('hint');
        const ctx = canvas.getContext('2d');

        let width, height;
        let points = [];
        let isRunning = false;
        let buildProgress = 0;

        // Углы вращения 3D модели
        let rotX = 0.25;
        let rotY = 0.6;
        let targetRotX = 0.25;
        let targetRotY = 0.6;
        let zoom = 1;
        let isDragging = false;
        let prevMouse = { x: 0, y: 0 };

        function resize() {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resize);
        resize();

        // Генератор 3D точек в форме свиньи
        function generatePigPoints() {
            const pts = [];

            // Вспомогательная функция для создания эллипсоидов и цилиндров
            function addEllipsoid(cx, cy, cz, rx, ry, rz, count, part) {
                for (let i = 0; i < count; i++) {
                    const u = Math.random() * Math.PI * 2;
                    const v = Math.acos(2 * Math.random() - 1);
                    // Слегка распределяем точки по поверхности и внутри оболочки
                    const shell = 0.88 + Math.random() * 0.12;
                    const x = cx + rx * shell * Math.sin(v) * Math.cos(u);
                    const y = cy + ry * shell * Math.sin(v) * Math.sin(u);
                    const z = cz + rz * shell * Math.cos(v);
                    pts.push(createPoint(x, y, z, part));
                }
            }

            function addCylinder(x1, y1, z1, x2, y2, z2, r, count, part) {
                for (let i = 0; i < count; i++) {
                    const t = Math.random();
                    const angle = Math.random() * Math.PI * 2;
                    const rad = r * (0.85 + Math.random() * 0.15);
                    const x = x1 + (x2 - x1) * t + Math.cos(angle) * rad;
                    const y = y1 + (y2 - y1) * t;
                    const z = z1 + (z2 - z1) * t + Math.sin(angle) * rad;
                    pts.push(createPoint(x, y, z, part));
                }
            }

            // 1. Туловище
            addEllipsoid(0, 0, 0, 1.45, 0.92, 0.88, 950, 'body');

            // 2. Голова
            addEllipsoid(1.38, -0.18, 0, 0.68, 0.62, 0.60, 480, 'head');

            // 3. Пятачок
            addEllipsoid(2.02, -0.10, 0, 0.22, 0.27, 0.29, 170, 'snout');

            // 4. Уши (левое и правое)
            addEllipsoid(1.30, -0.78, 0.36, 0.24, 0.32, 0.08, 95, 'ear');
            addEllipsoid(1.30, -0.78, -0.36, 0.24, 0.32, 0.08, 95, 'ear');

            // 5. Четыре ноги
            addCylinder(0.78, 0.55, 0.44, 0.78, 1.38, 0.44, 0.20, 110, 'leg');
            addCylinder(0.78, 0.55, -0.44, 0.78, 1.38, -0.44, 0.20, 110, 'leg');
            addCylinder(-0.82, 0.55, 0.44, -0.82, 1.38, 0.44, 0.20, 110, 'leg');
            addCylinder(-0.82, 0.55, -0.44, -0.82, 1.38, -0.44, 0.20, 110, 'leg');

            // 6. Хвостик крючком
            for (let i = 0; i < 85; i++) {
                const t = i / 85;
                const angle = t * Math.PI * 3.5;
                const x = -1.42 - t * 0.42;
                const y = -0.25 + Math.sin(angle) * 0.16 - t * 0.15;
                const z = Math.cos(angle) * 0.16;
                pts.push(createPoint(x, y, z, 'tail'));
            }

            // Перемешиваем точки для красивой отрисовки появления
            return pts.sort(() => Math.random() - 0.5);
        }

        function createPoint(x, y, z, part) {
            return {
                x, y, z,
                // Случайная стартовая позиция для эффекта сборки
                sx: (Math.random() - 0.5) * 12,
                sy: (Math.random() - 0.5) * 12,
                sz: (Math.random() - 0.5) * 12,
                char: Math.random() > 0.5 ? '1' : '0',
                part,
                flickerSpeed: 0.02 + Math.random() * 0.08
            };
        }

        // Управление мышью и тачскрином
        window.addEventListener('mousedown', (e) => {
            isDragging = true;
            prevMouse = { x: e.clientX, y: e.clientY };
        });
        window.addEventListener('mouseup', () => isDragging = false);
        window.addEventListener('mousemove', (e) => {
            if (!isDragging) return;
            const dx = e.clientX - prevMouse.x;
            const dy = e.clientY - prevMouse.y;
            targetRotY += dx * 0.008;
            targetRotX += dy * 0.008;
            prevMouse = { x: e.clientX, y: e.clientY };
        });

        window.addEventListener('wheel', (e) => {
            zoom -= e.deltaY * 0.001;
            zoom = Math.max(0.5, Math.min(2.2, zoom));
        });

        // Сенсорное управление для телефонов
        window.addEventListener('touchstart', (e) => {
            isDragging = true;
            prevMouse = { x: e.touches[0].clientX, y: e.touches[0].clientY };
        });
        window.addEventListener('touchend', () => isDragging = false);
        window.addEventListener('touchmove', (e) => {
            if (!isDragging) return;
            const dx = e.touches[0].clientX - prevMouse.x;
            const dy = e.touches[0].clientY - prevMouse.y;
            targetRotY += dx * 0.01;
            targetRotX += dy * 0.01;
            prevMouse = { x: e.touches[0].clientX, y: e.touches[0].clientY };
        });

        // Запуск при клике на кнопку
        btn.addEventListener('click', () => {
            btn.style.display = 'none';
            canvas.style.display = 'block';
            hint.style.display = 'block';
            points = generatePigPoints();
            isRunning = true;
            animate();
        });

        function animate() {
            if (!isRunning) return;
            requestAnimationFrame(animate);

