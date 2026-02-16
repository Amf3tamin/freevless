# freevless
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Hiokaaa VPN · GitHub Pages</title>
    <!-- Полностью самодостаточный HTML, готовый для GitHub Pages.
         После загрузки на GitHub репозиторий и включения GitHub Pages,
         ссылка будет вида https://твой-логин.github.io/имя-репозитория/ -->
    <style>
        /* Сброс и базовые стили */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background: #0e1621;  /* Telegram Dark Theme */
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 12px;
        }

        /* Карточка как в Telegram Mini App */
        .tg-card {
            max-width: 420px;
            width: 100%;
            background: #17212b;
            border-radius: 24px;
            padding: 20px 16px 24px;
            box-shadow: 0 20px 30px -10px rgba(0, 0, 0, 0.8);
            border: 1px solid #2b3f51;
            position: relative;
        }

        /* Верхняя панель с временем (имитация телеграма) */
        .status-bar {
            display: flex;
            justify-content: space-between;
            padding: 0 4px 16px;
            color: #7f91a4;
            font-size: 14px;
        }

        /* Шапка с аватаром */
        .profile {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 16px;
        }

        .avatar {
            width: 52px;
            height: 52px;
            background: linear-gradient(145deg, #2a7de0, #1f5bb5);
            border-radius: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 28px;
            font-weight: 700;
            color: white;
            box-shadow: 0 6px 12px rgba(0, 80, 200, 0.3);
        }

        .info h2 {
            color: white;
            font-size: 20px;
            font-weight: 600;
        }

        .info p {
            color: #8a9fb0;
            font-size: 14px;
            display: flex;
            align-items: center;
            gap: 6px;
            margin-top: 4px;
        }

        .info p span {
            background: #203d54;
            padding: 2px 10px;
            border-radius: 30px;
            font-size: 12px;
            color: #9bc2e6;
        }

        /* Бейдж протокола VLESS */
        .vless-tag {
            background: #0d2a3b;
            border: 1px solid #3a6d94;
            border-radius: 40px;
            padding: 8px 16px;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            margin: 16px 0 18px;
        }

        .green-dot {
            width: 10px;
            height: 10px;
            background: #40d876;
            border-radius: 50%;
            box-shadow: 0 0 10px #40d876;
            animation: pulse 1.8s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.7; transform: scale(1.15); }
            100% { opacity: 1; transform: scale(1); }
        }

        .vless-tag span {
            color: #d3e6ff;
            font-weight: 500;
        }

        /* Блок с конфигурацией */
        .config-panel {
            background: #0e1a24;
            border-radius: 22px;
            padding: 16px 14px;
            border: 1px solid #274153;
            margin: 16px 0;
        }

        .config-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid #1f3648;
        }

        .config-row:last-child {
            border-bottom: none;
        }

        .config-label {
            color: #a0b9ce;
            font-size: 15px;
        }

        .config-value {
            background: #1d3b52;
            padding: 5px 14px;
            border-radius: 40px;
            font-size: 14px;
            color: white;
            border: 1px solid #386282;
            max-width: 210px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }

        .config-value.uuid-style {
            background: #1b4c73;
            color: #e2f0ff;
            font-family: monospace;
        }

        /* Ссылка vless:// */
        .vless-url-container {
            background: #0e1a24;
            border-radius: 40px;
            padding: 12px 18px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid #386282;
            margin: 18px 0;
        }

        .vless-url {
            font-family: 'SF Mono', 'Fira Code', monospace;
            font-size: 13px;
            color: #c4def7;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            max-width: 210px;
        }

        .copy-action {
            background: #2a608b;
            padding: 8px 18px;
            border-radius: 40px;
            color: white;
            font-weight: 500;
            cursor: pointer;
            transition: 0.1s;
            border: none;
            font-size: 14px;
        }

        .copy-action:active {
            background: #1d4a70;
            transform: scale(0.95);
        }

        /* Основные кнопки */
        .btn-primary {
            background: #2f87e0;
            border: none;
            color: white;
            padding: 16px;
            border-radius: 20px;
            font-weight: 600;
            font-size: 18px;
            width: 100%;
            cursor: pointer;
            margin: 8px 0;
            box-shadow: 0 6px 0 #1b5ca0;
            transition: 0.1s;
            border: 1px solid #62a9ff;
        }

        .btn-primary:active {
            transform: translateY(4px);
            box-shadow: 0 2px 0 #1b5ca0;
        }

        .btn-secondary {
            background: #1d3649;
            border: 1px solid #3f6585;
            color: #d5eaff;
            padding: 14px;
            border-radius: 20px;
            font-size: 16px;
            width: 100%;
            cursor: pointer;
            margin-top: 10px;
        }

        .btn-secondary:active {
            background: #142b3c;
        }

        /* Уведомление-тост */
        .toast-message {
            background: #1b4f78;
            color: white;
            text-align: center;
            padding: 12px;
            border-radius: 40px;
            font-size: 14px;
            margin: 10px 0 0;
            opacity: 0;
            transition: 0.2s;
        }

        .toast-message.show {
            opacity: 1;
        }

        /* Футер с пометкой GitHub */
        .gh-footer {
            text-align: center;
            margin-top: 20px;
            color: #4c6f8c;
            font-size: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .gh-footer img {
            width: 14px;
            height: 14px;
            filter: invert(0.5);
        }
    </style>
</head>
<body>
    <div class="tg-card">
        <!-- Статус бар -->
        <div class="status-bar">
            <span>🕒 19:24</span>
            <span>📶 🔋 87%</span>
        </div>

        <!-- Шапка профиля (как в телеге) -->
        <div class="profile">
            <div class="avatar">H</div>
            <div class="info">
                <h2>Hiokaaa VPN</h2>
                <p>@hiokaaa_vpn_bot <span>бот</span></p>
            </div>
        </div>

        <!-- Сообщение от бота (для атмосферы) -->
        <div style="background: #1d3345; border-radius: 18px 18px 18px 4px; padding: 14px; margin: 10px 0; color: #c6defa;">
            🔐 <b>VLESS</b> протокол активен. Сервер: Амстердам. Нажми кнопку подключения.
        </div>

        <!-- Бейдж VLESS -->
        <div class="vless-tag">
            <span class="green-dot"></span>
            <span>⚡ VLESS / XTLS / grpc</span>
        </div>

        <!-- Параметры конфигурации -->
        <div class="config-panel">
            <div class="config-row">
                <span class="config-label">Server</span>
                <span class="config-value">ams.hiokaaa.xyz</span>
            </div>
            <div class="config-row">
                <span class="config-label">UUID</span>
                <span class="config-value uuid-style">c8b7f21e-4d3a-9f6c-b82e-1e7a3d9f4c6a</span>
            </div>
            <div class="config-row">
                <span class="config-label">Port</span>
                <span class="config-value">2053 (grpc)</span>
            </div>
            <div class="config-row">
                <span class="config-label">Flow/TLS</span>
                <span class="config-value">xtls-rprx-vision</span>
            </div>
        </div>

        <!-- Блок с vless:// ссылкой (то что надо копировать) -->
        <div class="vless-url-container" id="vlessBlock">
            <span class="vless-url" id="vlessText">vless://c8b7f21e-4d3a-9f6c-b82e-1e7a3d9f4c6a@ams.hiokaaa.xyz:2053?type=grpc&security=tls&flow=xtls-rprx-vision&sni=hiokaaa.xyz#Hiokaaa_GitHub</span>
            <button class="copy-action" id="copyBtn">Копировать</button>
        </div>

        <!-- Тоаст для уведомлений -->
        <div class="toast-message" id="toast">✨ Скопировано</div>

        <!-- Кнопки управления -->
        <button class="btn-primary" id="connectBtn">🔌 ПОДКЛЮЧИТЬСЯ</button>
        <button class="btn-secondary" id="configBtn">📋 ПОЛНАЯ КОНФИГУРАЦИЯ</button>

        <!-- Футер с пометкой GitHub Pages -->
        <div class="gh-footer">
            <span>🌐 GitHub Pages</span>
            <span>•</span>
            <span>Открыто в Telegram</span>
        </div>
    </div>

    <script>
        (function() {
            const toast = document.getElementById('toast');
            const copyBtn = document.getElementById('copyBtn');
            const vlessText = document.getElementById('vlessText');
            const connectBtn = document.getElementById('connectBtn');
            const configBtn = document.getElementById('configBtn');

            // Функция показа тоста
            function showToast(msg) {
                toast.textContent = msg || '✅ Скопировано';
                toast.classList.add('show');
                setTimeout(() => toast.classList.remove('show'), 1700);
            }

            // Копирование ссылки (работает везде, включая Telegram WebView)
            function copyVlessLink() {
                const link = vlessText.innerText; // получаем vless://.....

                if (navigator.clipboard && navigator.clipboard.writeText) {
                    navigator.clipboard.writeText(link).then(() => {
                        showToast('🔁 VLESS скопирована');
                    }).catch(() => {
                        fallbackCopy(link);
                    });
                } else {
                    fallbackCopy(link);
                }
            }

            function fallbackCopy(text) {
                const textArea = document.createElement('textarea');
                textArea.value = text;
                textArea.style.position = 'fixed';
                textArea.style.opacity = '0';
                document.body.appendChild(textArea);
                textArea.focus();
                textArea.select();
                try {
                    document.execCommand('copy');
                    showToast('📋 Скопировано (резервный метод)');
                } catch (err) {
                    showToast('❌ Ошибка копирования');
                }
                document.body.removeChild(textArea);
            }

            // Обработчик кнопки копирования
            copyBtn.addEventListener('click', copyVlessLink);

            // Клик на самой ссылке тоже копирует
            vlessText.addEventListener('click', copyVlessLink);

            // Кнопка подключения
            connectBtn.addEventListener('click', () => {
                showToast('🔄 Запрос подключения (имитация)');
                const dot = document.querySelector('.green-dot');
                dot.style.background = '#ffaa33';
                setTimeout(() => dot.style.background = '#40d876', 700);
            });

            // Кнопка полной конфигурации
            configBtn.addEventListener('click', () => {
                showToast('📦 JSON config в консоли');
                console.log('Full VLESS config for Hiokaaa:', {
                    version: 'v1',
                    protocol: 'vless',
                    uuid: 'c8b7f21e-4d3a-9f6c-b82e-1e7a3d9f4c6a',
                    server: 'ams.hiokaaa.xyz',
                    port: 2053,
                    network: 'grpc',
                    tls: 'tls',
                    flow: 'xtls-rprx-vision',
                    sni: 'hiokaaa.xyz'
                });
            });

            // Определяем, открыто ли в Telegram
            const isTelegram = navigator.userAgent.includes('Telegram') || navigator.userAgent.includes('TelegramBot');
            console.log('Hiokaaa VPN — запущен в Telegram:', isTelegram);

            // Для красоты: поддержим Telegram WebApp, если есть
            if (window.Telegram && Telegram.WebApp) {
                Telegram.WebApp.ready();
                Telegram.WebApp.expand();
            } else {
                // Заглушка, чтобы не было ошибок
                window.Telegram = { WebApp: { ready: () => {}, expand: () => {} } };
            }

            // Добавляем маленькую анимацию при загрузке (чисто косметика)
            setTimeout(() => {
                document.querySelector('.green-dot').style.transform = 'scale(1.2)';
                setTimeout(() => document.querySelector('.green-dot').style.transform = 'scale(1)', 200);
            }, 300);
        })();
    </script>
</body>
</html>
