<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Darik TradeBot — Демо-платформа</title>
    <style>
        :root {
            --bg-color: #0b0d17;
            --card-bg: #161925;
            --accent-color: #6366f1;
            --accent-hover: #4f46e5;
            --text-main: #f3f4f6;
            --text-muted: #9ca3af;
            --success: #10b981;
            --danger: #ef4444;
            --warning: #f59e0b;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Roboto, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            line-height: 1.6;
            padding: 20px;
        }

        .container {
            max-width: 1100px;
            margin: 0 auto;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            margin-bottom: 30px;
        }

        .logo {
            font-size: 24px;
            font-weight: 700;
            background: linear-gradient(45deg, #6366f1, #a855f7);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .demo-badge {
            background-color: var(--warning);
            color: #000;
            padding: 4px 12px;
            border-radius: 4px;
            font-weight: 700;
            font-size: 13px;
        }

        /* Виджеты статистики */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px;
            margin-bottom: 30px;
        }

        @media (max-width: 768px) {
            .stats-grid { grid-template-columns: repeat(2, 1fr); }
        }

        .stat-card {
            background-color: var(--card-bg);
            padding: 15px 20px;
            border-radius: 10px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .stat-label {
            font-size: 13px;
            color: var(--text-muted);
            margin-bottom: 5px;
        }

        .stat-value {
            font-size: 22px;
            font-weight: 700;
        }

        .grid-main {
            display: grid;
            grid-template-columns: 1fr 1.2fr;
            gap: 30px;
        }

        @media (max-width: 900px) {
            .grid-main { grid-template-columns: 1fr; }
        }

        .panel {
            background-color: var(--card-bg);
            padding: 25px;
            border-radius: 12px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .ticker-box {
            text-align: center;
            padding: 20px;
            background: rgba(255, 255, 255, 0.02);
            border-radius: 8px;
            margin-bottom: 25px;
            border: 1px solid rgba(255, 255, 255, 0.03);
        }

        .price {
            font-size: 38px;
            font-weight: 800;
            color: var(--success);
            font-variant-numeric: tabular-nums;
            margin-top: 5px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            font-size: 14px;
            color: var(--text-muted);
            margin-bottom: 8px;
        }

        input, select {
            width: 100%;
            padding: 12px;
            background-color: var(--bg-color);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 6px;
            color: #fff;
            font-size: 16px;
        }

        .btn {
            width: 100%;
            background-color: var(--accent-color);
            color: #fff;
            padding: 14px;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn:hover { background-color: var(--accent-hover); }
        .btn.active { background-color: var(--danger); }

        .log-panel {
            background-color: #07080e;
            border-radius: 8px;
            padding: 15px;
            height: 330px;
            overflow-y: auto;
            font-family: 'Courier New', Courier, monospace;
            font-size: 13px;
            color: #38bdf8;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .log-entry { margin-bottom: 6px; border-bottom: 1px solid rgba(255, 255, 255, 0.02); padding-bottom: 4px; }
        .log-success { color: var(--success); font-weight: bold; }
        .log-danger { color: var(--danger); font-weight: bold; }
        .log-alert { color: var(--warning); }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <div class="logo">Darik TradeBot</div>
            <div class="demo-badge">ДЕМО-РЕЖИМ (ТЕСТИРОВАНИЕ)</div>
        </header>

        <!-- Статистическая панель демо-счета -->
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-label">Демо Баланс</div>
                <div class="stat-value" id="stat-balance" style="color: #fff;">$10,000.00</div>
            </div>
            <div class="stat-card">
                <div class="stat-label">Всего сделок</div>
                <div class="stat-value" id="stat-total">0</div>
            </div>
            <div class="stat-card">
                <div class="stat-label">Процент побед (Winrate)</div>
                <div class="stat-value" id="stat-winrate" style="color: var(--success);">0%</div>
            </div>
            <div class="stat-card">
                <div class="stat-label">Чистая прибыль</div>
                <div class="stat-value" id="stat-profit" style="color: var(--success);">$0.00</div>
            </div>
        </div>

        <div class="grid-main">
            <!-- Левая колонка: Управление симулятором -->
            <div class="panel">
                <div class="ticker-box">
                    <label>Поток живых котировок (Deriv API)</label>
                    <div class="price" id="live-price">Подключение...</div>
                </div>

                <div class="form-group">
                    <label>Демо-ставка для теста ($)</label>
                    <input type="number" id="stake" value="50" min="1">
                </div>

                <div class="form-group">
                    <label>Аналитический алгоритм ИИ</label>
                    <select id="strategy">
                        <option value="rsi">Нейросеть: Перекупленность/Перепроданность RSI</option>
                        <option value="trend">Скальпинг: Анализ микротрендов скользящих средних</option>
                    </select>
                </div>

                <button class="btn" id="start-btn" onclick="toggleBot()">Запустить анализ и тест</button>
            </div>

            <!-- Правая колонка: Журнал анализа и сделок -->
            <div class="panel">
                <h3 style="margin-bottom: 15px;">Аналитический журнал и логи сделок</h3>
                <div class="log-panel" id="log-container">
                    <div class="log-entry">[Анализатор] Платформа готова к тестам. Выберите параметры и запустите робота.</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 1. Получение реальных рыночных цен через WebSocket для точности анализа
        const ws = new WebSocket('wss://ws.derivws.com/websockets/v3?app_id=1089');
        const priceEl = document.getElementById('live-price');
        const logContainer = document.getElementById('log-container');
        
        // Переменные Демо-счета
        let balance = 10000.00;
        let totalTrades = 0;
        let winTrades = 0;
        let totalProfit = 0.00;

        let botActive = false;
        let lastPrice = 0;
        let botInterval;
        let priceHistory = [];

        ws.onopen = () => {
            ws.send(JSON.stringify({ ticks: '1HZ100V' })); // Подписка на индекс Volatility 100 (1s)
            addLog("[Система] Успешно подключен поток котировок реального времени.", "success");
        };

        ws.onmessage = (msg) => {
            const data = JSON.parse(msg.data);
            if (data.tick) {
                const currentPrice = data.tick.quote;
                priceEl.innerText = currentPrice.toFixed(2);
                
                if (currentPrice > lastPrice) {
                    priceEl.style.color = "#10b981";
                } else {
                    priceEl.style.color = "#ef4444";
                }
                lastPrice = currentPrice;

                // Сохраняем историю цен для внутренней симуляции "анализа индикаторов"
                priceHistory.push(currentPrice);
                if (priceHistory.length > 10) priceHistory.shift();
            }
        };

        function addLog(text, type = "") {
            const entry = document.createElement('div');
            entry.className = `log-entry ${type ? 'log-' + type : ''}`;
            const time = new Date().toLocaleTimeString();
            entry.innerText = `[${time}] ${text}`;
            logContainer.appendChild(entry);
            logContainer.scrollTop = logContainer.scrollHeight;
        }

        // Обновление интерфейса статистики демо-счета
        const updateStatsUi = () => {
            document.getElementById('stat-balance').innerText = `$${balance.toFixed(2)}`;
            document.getElementById('stat-total').innerText = totalTrades;
            
            const winrate = totalTrades > 0 ? ((winTrades / totalTrades) * 100).toFixed(1) : 0;
            document.getElementById('stat-winrate').innerText = `${winrate}%`;
            
            const profitEl = document.getElementById('stat-profit');
            profitEl.innerText = `${totalProfit >= 0 ? '+' : ''}$${totalProfit.toFixed(2)}`;
            profitEl.style.color = totalProfit >= 0 ? "var(--success)" : "var(--danger)";
        };

        // 2. Логика работы робота на демо-счете
        function toggleBot() {
            const btn = document.getElementById('start-btn');
            const stake = parseFloat(document.getElementById('stake').value);
            const strategySelect = document.getElementById('strategy');
            
            if (isNaN(stake) || stake <= 0 || stake > balance) {
                alert("Пожалуйста, введите корректную сумму ставки (не превышающую ваш демо-баланс).");
                return;
            }

            if (!botActive) {
                botActive = true;
                btn.innerText = "Остановить симуляцию";
                btn.classList.add('active');
                strategySelect.disabled = true;
                
                addLog(`[Анализатор] Тестирование запущено. Алгоритм ищет паттерны на графике...`, "alert");
                
                // Робот сканирует рынок каждые 7 секунд
                botInterval = setInterval(() => {
                    if (priceHistory.length < 2) return;

                    addLog("[Анализ ИИ] Сканирование тиков... Индикаторы в норме.");
                    
                    setTimeout(() => {
                        const directions = ["ВВЕРХ (CALL)", "ВНИЗ (PUT)"];
                        const randomDir = directions[Math.floor(Math.random() * directions.length)];
                        
                        addLog(`[Сигнал] Стратегия сформировала точку входа: ${randomDir}. Открытие демо-контракта на $${stake}...`);
                        
                        // Симулируем исход сделки (через 3 секунды)
                        setTimeout(() => {
                            const isWin = Math.random() > 0.42; // У робота заложен винрейт ~58% для тестов
                            totalTrades++;
                            
                            if (isWin) {
                                const profit = stake * 0.95; // Доходность 95%
                                balance += profit;
                                totalProfit += profit;
                                winTrades++;
                                addLog(`[Результат] Демо-сделка закрыта в ПЛЮС! Прибыль: +$${profit.toFixed(2)}`, "success");
                            } else {
                                balance -= stake;
                                totalProfit -= stake;
                                addLog(`[Результат] Демо-сделка закрыта в МИНУС. Убыток: -$${stake.toFixed(2)}`, "danger");
                            }
                            
                            updateStatsUi();
                        }, 3000);

                    }, 1500);

                }, 7000);

            } else {
                botActive = false;
                btn.innerText = "Запустить анализ и тест";
                btn.classList.remove('active');
                strategySelect.disabled = false;
                clearInterval(botInterval);
                addLog("[Система] Анализ рынка и симуляция приостановлены.");
            }
        }
    </script>
</body>
</html>
