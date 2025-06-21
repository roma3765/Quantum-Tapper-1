<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quantum Clicker</title>
    <style>
        :root {
            --primary: #6a11cb;
            --secondary: #2575fc;
            --accent: #ff3e9d;
            --text: #f8f9fa;
            --bg: #121212;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--bg);
            color: var(--text);
            margin: 0;
            padding: 0;
            overflow-x: hidden;
            line-height: 1.6;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        header {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            padding: 20px;
            border-radius: 0 0 15px 15px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.3);
            margin-bottom: 30px;
        }
        .currency-display {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 30px;
            background: rgba(255,255,255,0.05);
            padding: 15px;
            border-radius: 10px;
        }
        .currency {
            display: flex;
            align-items: center;
            background: rgba(0,0,0,0.3);
            padding: 8px 15px;
            border-radius: 20px;
            min-width: 150px;
        }
        .currency-icon {
            width: 24px;
            height: 24px;
            margin-right: 10px;
            background: var(--accent);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .clicker-area {
            position: relative;
            width: 250px;
            height: 250px;
            margin: 30px auto;
            background: radial-gradient(circle, var(--primary), var(--bg));
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            user-select: none;
            transition: transform 0.1s, box-shadow 0.3s;
            box-shadow: 0 0 30px rgba(106, 17, 203, 0.5);
            overflow: hidden;
        }
        .clicker-area:active {
            transform: scale(0.98);
        }
        .clicker-area::before {
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, transparent 60%, rgba(255,255,255,0.1) 100%);
            opacity: 0;
            transition: opacity 0.3s;
        }
        .clicker-area:active::before {
            opacity: 1;
        }
        .clicker-text {
            font-size: 24px;
            font-weight: bold;
            z-index: 2;
            text-align: center;
        }
        .click-effect {
            position: absolute;
            width: 20px;
            height: 20px;
            background: rgba(255,255,255,0.8);
            border-radius: 50%;
            pointer-events: none;
            animation: float 1s ease-out forwards;
            z-index: 1;
        }
        @keyframes float {
            0% {
                transform: translate(0, 0) scale(1);
                opacity: 1;
            }
            100% {
                transform: translate(var(--tx), var(--ty)) scale(0);
                opacity: 0;
            }
        }
        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }
        .tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all 0.3s;
        }
        .tab.active {
            border-bottom: 3px solid var(--accent);
            color: var(--accent);
        }
        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: block;
        }
        .upgrade-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 15px;
        }
        .upgrade {
            background: rgba(255,255,255,0.05);
            border-radius: 10px;
            padding: 15px;
            transition: all 0.3s;
            border-left: 3px solid var(--primary);
        }
        .upgrade:hover {
            background: rgba(255,255,255,0.1);
            transform: translateY(-3px);
        }
        .upgrade-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }
        .upgrade-name {
            font-weight: bold;
            color: var(--accent);
        }
        .upgrade-cost {
            color: #ffcc00;
        }
        .upgrade-btn {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border: none;
            color: white;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 10px;
            width: 100%;
        }
        .upgrade-btn:disabled {
            background: rgba(255,255,255,0.1);
            cursor: not-allowed;
        }
        .upgrade-btn:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }
        .progress-container {
            width: 100%;
            height: 5px;
            background: rgba(255,255,255,0.1);
            border-radius: 5px;
            margin-top: 10px;
            overflow: hidden;
        }
        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--accent), #ff8a00);
            width: 0%;
            transition: width 0.5s;
        }
        .prestige-btn {
            background: linear-gradient(135deg, #ff3e9d, #ff8a00);
            border: none;
            color: white;
            padding: 15px 30px;
            border-radius: 30px;
            cursor: pointer;
            font-size: 18px;
            font-weight: bold;
            margin: 30px auto;
            display: block;
            transition: all 0.3s;
        }
        .prestige-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 10px 25px rgba(255, 62, 157, 0.4);
        }
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(0,0,0,0.7);
            color: white;
            padding: 15px;
            border-radius: 10px;
            transform: translateX(200%);
            transition: transform 0.3s;
            z-index: 100;
        }
        .notification.show {
            transform: translateX(0);
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <h1>Quantum Clicker</h1>
        </div>
    </header>

    <div class="container">
        <div class="currency-display">
            <div class="currency">
                <div class="currency-icon"></div>
                <span id="quantum-points">0</span> Квантовых точек
            </div>
            <div class="currency">
                <div class="currency-icon"></div>
                <span id="energy">0</span> Энергии
            </div>
            <div class="currency">
                <div class="currency-icon"></div>
                <span id="knowledge">0</span> Знаний
            </div>
            <div class="currency">
                <div class="currency-icon"></div>
                <span id="prestige">0</span> Престижа
            </div>
        </div>

        <div class="clicker-area" id="clicker">
            <div class="clicker-text">
                <div>Квантовый реактор</div>
                <div id="click-power">1 квант/клик</div>
            </div>
        </div>

        <div class="tabs">
            <div class="tab active" data-tab="generators">Генераторы</div>
            <div class="tab" data-tab="upgrades">Улучшения</div>
            <div class="tab" data-tab="research">Исследования</div>
            <div class="tab" data-tab="prestige">Престиж</div>
        </div>

        <div class="tab-content active" id="generators">
            <div class="upgrade-grid">
                <div class="upgrade">
                    <div class="upgrade-header">
                        <span class="upgrade-name">Солнечная панель</span>
                        <span class="upgrade-cost" id="solar-cost">10 энергии</span>
                    </div>
                    <div>Производит 0.1 энергии/сек</div>
                    <div class="progress-container">
                        <div class="progress-bar" id="solar-progress"></div>
                    </div>
                    <button class="upgrade-btn" id="buy-solar">Купить (<span id="solar-count">0</span>)</button>
                </div>
                <!-- More generators would go here -->
            </div>
        </div>

        <div class="tab-content" id="upgrades">
            <div class="upgrade-grid">
                <div class="upgrade">
                    <div class="upgrade-header">
                        <span class="upgrade-name">Квантовый усилитель</span>
                        <span class="upgrade-cost">50 квантов</span>
                    </div>
                    <div>Увеличивает силу клика в 2 раза</div>
                    <button class="upgrade-btn">Купить</button>
                </div>
                <!-- More upgrades would go here -->
            </div>
        </div>

        <div class="tab-content" id="research">
            <div class="upgrade-grid">
                <div class="upgrade">
                    <div class="upgrade-header">
                        <span class="upgrade-name">Квантовая физика</span>
                        <span class="upgrade-cost">100 знаний</span>
                    </div>
                    <div>Разблокирует новые улучшения</div>
                    <div class="progress-container">
                        <div class="progress-bar" style="width: 0%"></div>
                    </div>
                    <button class="upgrade-btn">Исследовать</button>
                </div>
                <!-- More research would go here -->
            </div>
        </div>

        <div class="tab-content" id="prestige">
            <h2>Престижная система</h2>
            <p>Престиж сбросит ваш прогресс, но даст постоянные бонусы</p>
            <p>Доступно престижных очков: <span id="prestige-to-gain">0</span></p>
            <button class="prestige-btn" id="prestige-button">Престиж</button>
        </div>
    </div>

    <div class="notification" id="notification">
        Улучшение куплено!
    </div>

    <script>
        // Game state
        const game = {
            points: 0,
            energy: 0,
            knowledge: 0,
            prestige: 0,
            clickPower: 1,
            generators: {
                solar: {
                    count: 0,
                    cost: 10,
                    production: 0.1,
                    progress: 0
                }
            },
            upgrades: {},
            research: {},
            multipliers: {
                click: 1,
                energy: 1,
                knowledge: 1
            },
            lastUpdate: Date.now()
        };

        // DOM elements
        const elements = {
            points: document.getElementById('quantum-points'),
            energy: document.getElementById('energy'),
            knowledge: document.getElementById('knowledge'),
            prestige: document.getElementById('prestige'),
            clickPower: document.getElementById('click-power'),
            clicker: document.getElementById('clicker'),
            notification: document.getElementById('notification'),
            tabs: document.querySelectorAll('.tab'),
            tabContents: document.querySelectorAll('.tab-content'),
            // Generator elements
            solarCost: document.getElementById('solar-cost'),
            solarCount: document.getElementById('solar-count'),
            solarProgress: document.getElementById('solar-progress'),
            buySolar: document.getElementById('buy-solar'),
            // Prestige
            prestigeButton: document.getElementById('prestige-button'),
            prestigeToGain: document.getElementById('prestige-to-gain')
        };

        // Initialize the game
        function init() {
            loadGame();
            setupEventListeners();
            gameLoop();
            updateUI();
        }

        // Load saved game
        function loadGame() {
            const savedGame = localStorage.getItem('quantumClicker');
            if (savedGame) {
                const parsed = JSON.parse(savedGame);
                Object.assign(game, parsed);
                game.lastUpdate = Date.now();
            }
        }

        // Save game
        function saveGame() {
            game.lastUpdate = Date.now();
            localStorage.setItem('quantumClicker', JSON.stringify(game));
        }

        // Set up event listeners
        function setupEventListeners() {
            // Clicker
            elements.clicker.addEventListener('click', () => {
                game.points += game.clickPower * game.multipliers.click;
                createClickEffect(event);
                updateUI();
                saveGame();
            });

            // Tabs
            elements.tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    elements.tabs.forEach(t => t.classList.remove('active'));
                    elements.tabContents.forEach(c => c.classList.remove('active'));
                    
                    tab.classList.add('active');
                    document.getElementById(tab.dataset.tab).classList.add('active');
                });
            });

            // Buy solar panel
            elements.buySolar.addEventListener('click', () => {
                if (game.energy >= game.generators.solar.cost) {
                    game.energy -= game.generators.solar.cost;
                    game.generators.solar.count++;
                    game.generators.solar.cost = Math.floor(game.generators.solar.cost * 1.15);
                    
                    showNotification(`Куплена солнечная панель (${game.generators.solar.count})`);
                    updateUI();
                    saveGame();
                }
            });

            // Prestige
            elements.prestigeButton.addEventListener('click', () => {
                const prestigePoints = calculatePrestige();
                if (prestigePoints > 0) {
                    if (confirm(`Вы получите ${prestigePoints} престижных очков. Продолжить?`)) {
                        prestige(prestigePoints);
                        showNotification(`Престиж получен! +${prestigePoints} очков`);
                    }
                } else {
                    alert('Нужно больше квантовых точек для престижа!');
                }
            });

            // Auto-save every 30 seconds
            setInterval(saveGame, 30000);
        }

        // Game loop
        function gameLoop() {
            const now = Date.now();
            const delta = (now - game.lastUpdate) / 1000; // in seconds
            game.lastUpdate = now;

            // Generate resources
            game.energy += game.generators.solar.count * game.generators.solar.production * delta * game.multipliers.energy;
            game.generators.solar.progress = (game.generators.solar.progress + delta) % 1;

            updateUI();
            requestAnimationFrame(gameLoop);
        }

        // Update UI
        function updateUI() {
            // Resources
            elements.points.textContent = formatNumber(game.points);
            elements.energy.textContent = formatNumber(game.energy);
            elements.knowledge.textContent = formatNumber(game.knowledge);
            elements.prestige.textContent = formatNumber(game.prestige);
            elements.clickPower.textContent = `${formatNumber(game.clickPower * game.multipliers.click)} квант/клик`;

            // Solar panel
            elements.solarCost.textContent = `${formatNumber(game.generators.solar.cost)} энергии`;
            elements.solarCount.textContent = game.generators.solar.count;
            elements.solarProgress.style.width = `${game.generators.solar.progress * 100}%`;
            elements.buySolar.disabled = game.energy < game.generators.solar.cost;

            // Prestige
            const prestigePoints = calculatePrestige();
            elements.prestigeToGain.textContent = prestigePoints;
            elements.prestigeButton.disabled = prestigePoints < 1;
        }

        // Create click effect
        function createClickEffect(event) {
            const rect = elements.clicker.getBoundingClientRect();
            const x = event.clientX - rect.left;
            const y = event.clientY - rect.top;

            const effect = document.createElement('div');
            effect.className = 'click-effect';
            effect.style.left = `${x}px`;
            effect.style.top = `${y}px`;
            
            // Random direction
            const angle = Math.random() * Math.PI * 2;
            const distance = 50 + Math.random() * 50;
            effect.style.setProperty('--tx', `${Math.cos(angle) * distance}px`);
            effect.style.setProperty('--ty', `${Math.sin(angle) * distance}px`);

            elements.clicker.appendChild(effect);
            setTimeout(() => effect.remove(), 1000);
        }

        // Show notification
        function showNotification(message) {
            elements.notification.textContent = message;
            elements.notification.classList.add('show');
            setTimeout(() => {
                elements.notification.classList.remove('show');
            }, 3000);
        }

        // Calculate prestige points
        function calculatePrestige() {
            return Math.floor(Math.sqrt(game.points / 1e6));
        }

        // Prestige reset
        function prestige(points) {
            game.prestige += points;
            game.points = 0;
            game.energy = 0;
            game.knowledge = 0;
            game.clickPower = 1;
            game.generators = {
                solar: {
                    count: 0,
                    cost: 10,
                    production: 0.1,
                    progress: 0
                }
            };
            game.multipliers.click += points * 0.1;
            saveGame();
        }

        // Format numbers
        function formatNumber(num) {
            if (num < 1000) return Math.floor(num);
            if (num < 1e6) return (num / 1e3).toFixed(1) + 'K';
            if (num < 1e9) return (num / 1e6).toFixed(1) + 'M';
            return (num / 1e9).toFixed(1) + 'B';
        }

        // Start the game
        init();
    </script>
</body>
</html>
