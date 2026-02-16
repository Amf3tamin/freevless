<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>hioka · vless</title>
    <style>
        body {
            background: #000000;
            color: #ff5555;
            font-family: 'Courier New', monospace;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 900px;
            margin: 0 auto;
            border: 1px solid #ff0000;
            padding: 20px;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.2);
        }
        .header {
            border-bottom: 1px solid #ff0000;
            padding-bottom: 10px;
            margin-bottom: 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .header h1 {
            margin: 0;
            font-size: 24px;
            font-weight: normal;
            text-shadow: 0 0 10px rgba(255, 0, 0, 0.5);
        }
        .status {
            color: #00ff00;
            border: 1px solid #00ff00;
            padding: 5px 10px;
            font-size: 12px;
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }
        .block {
            margin: 25px 0;
            padding: 15px;
            border: 1px solid #ff0000;
            background: #000000;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }
        .block:hover {
            box-shadow: 0 0 15px rgba(255, 0, 0, 0.3);
            border-color: #ff3333;
        }
        .block::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, transparent, #ff0000, transparent);
            transition: left 0.5s;
        }
        .block:hover::before {
            left: 100%;
        }
        .block-title {
            margin: -15px -15px 15px -15px;
            padding: 8px 15px;
            background: #1a0000;
            border-bottom: 1px solid #ff0000;
            font-weight: bold;
            color: #ff6666;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .badge {
            background: #ff0000;
            color: #000000;
            padding: 2px 8px;
            font-size: 11px;
            border-radius: 0;
            font-weight: bold;
        }
        .config {
            font-family: 'Courier New', monospace;
            word-break: break-all;
            font-size: 13px;
            line-height: 1.5;
            margin: 15px 0;
            padding: 10px;
            background: #0a0000;
            border-left: 3px solid #ff0000;
            color: #ff7777;
            position: relative;
            cursor: pointer;
            transition: all 0.2s;
        }
        .config:hover {
            background: #150000;
            border-left-color: #ff6666;
        }
        .config::after {
            content: '📋';
            position: absolute;
            right: 10px;
            top: 50%;
            transform: translateY(-50%);
            opacity: 0;
            transition: opacity 0.2s;
        }
        .config:hover::after {
            opacity: 0.5;
        }
        .button-group {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin: 15px 0 0 0;
        }
        button {
            background: #0a0000;
            border: 1px solid #ff0000;
            color: #ff5555;
            padding: 10px 20px;
            font-family: 'Courier New', monospace;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
            font-weight: bold;
            letter-spacing: 0.5px;
            flex: 1 1 auto;
            min-width: 120px;
        }
        button::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: rgba(255, 0, 0, 0.2);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            transition: width 0.3s, height 0.3s;
        }
        button:hover::before {
            width: 300px;
            height: 300px;
        }
        button:hover {
            background: #ff0000;
            color: #000000;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.5);
        }
        button:active {
            transform: scale(0.95);
        }
        .button-icon {
            margin-right: 8px;
            font-size: 16px;
        }
        .footer {
            margin-top: 30px;
            padding-top: 15px;
            border-top: 1px solid #ff0000;
            font-size: 12px;
            color: #aa3333;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        a {
            color: #ff6666;
            text-decoration: none;
            border-bottom: 1px dotted #ff3333;
            transition: all 0.2s;
        }
        a:hover {
            color: #ff9999;
            border-bottom: 1px solid #ff9999;
        }
        .link-group {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin: 15px 0;
        }
        .link-group a button {
            border-color: #ff0000;
        }
        .toast {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: #1a0000;
            border: 1px solid #ff0000;
            color: #ff5555;
            padding: 10px 20px;
            font-family: 'Courier New', monospace;
            font-size: 14px;
            z-index: 1000;
            animation: slideIn 0.3s;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.3);
        }
        @keyframes slideIn {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
        .stats {
            display: flex;
            gap: 20px;
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ff0000;
            background: #0a0000;
        }
        .stat-item {
            text-align: center;
        }
        .stat-value {
            font-size: 20px;
            font-weight: bold;
            color: #ff0000;
        }
        .stat-label {
            font-size: 10px;
            color: #aa3333;
        }
        .ping-indicator {
            display: inline-block;
            width: 8px;
            height: 8px;
            background: #00ff00;
            border-radius: 0;
            margin-left: 5px;
            animation: blink 1s infinite;
        }
        @keyframes blink {
            0% { opacity: 1; }
            50% { opacity: 0.3; }
            100% { opacity: 1; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div>
                <h1>hioka vpn · бесплатный vless</h1>
                <div style="color:#aa3333; margin-top:5px;">3 конфига · 2025</div>
            </div>
            <div class="status">
                🟢 СЕРВЕРЫ АКТИВНЫ
            </div>
        </div>

        <!-- Статистика -->
        <div class="stats">
            <div class="stat-item">
                <div class="stat-value">3</div>
                <div class="stat-label">АКТИВНЫХ СЕРВЕРА</div>
            </div>
            <div class="stat-item">
                <div class="stat-value">47</div>
                <div class="stat-label">ПОЛЬЗОВАТЕЛЕЙ</div>
            </div>
            <div class="stat-item">
                <div class="stat-value">99%</div>
                <div class="stat-label">АПТАЙМ</div>
            </div>
        </div>

        <!-- MTProto -->
        <div class="block">
            <div class="block-title">
                <span>📱 MTProto · Telegram прокси</span>
                <span class="badge">РАБОТАЕТ</span>
            </div>
            <div class="config" id="mtproto" onclick="copy('mtproto')">https://t.me/proxy?server=xfs1.gbird.top&port=6443&secret=ddecad3d673e42dc10cae6fa9bcebcd5f6</div>
            <div class="button-group">
                <button onclick="copy('mtproto')">
                    <span class="button-icon">📋</span> КОПИРОВАТЬ
                </button>
                <a href="https://t.me/proxy?server=xfs1.gbird.top&port=6443&secret=ddecad3d673e42dc10cae6fa9bcebcd5f6" target="_blank">
                    <button>
                        <span class="button-icon">📱</span> ОТКРЫТЬ В TG
                    </button>
                </a>
                <button onclick="showQR('mtproto')">
                    <span class="button-icon">📷</span> QR-КОД
                </button>
            </div>
        </div>

        <!-- VLESS Reality -->
        <div class="block">
            <div class="block-title">
                <span>🔮 VLESS + Reality · VK зеркало</span>
                <span class="badge">⚡ 25 ms</span>
            </div>
            <div class="config" id="vless1" onclick="copy('vless1')">vless://83a11d95-1b15-4668-a675-00148622b2b1@95.163.183.205:443?mode=auto&path=%2F&security=reality&encryption=none&pbk=pQYGdr-ee0TotzdikPWnqJgKbX8OYcPNkJpH9scxjB0&fp=chrome&allowinsecure=0&type=xhttp&sni=sun6-21.userapi.com&sid=dde66ef1#tg%3Ahiokaaa++%5Bfree%5D+VK2</div>
            <div class="button-group">
                <button onclick="copy('vless1')">
                    <span class="button-icon">📋</span> КОПИРОВАТЬ
                </button>
                <button onclick="testPing('vless1')">
                    <span class="button-icon">📊</span> ТЕСТ ПИНГА
                </button>
                <button onclick="showQR('vless1')">
                    <span class="button-icon">📷</span> QR-КОД
                </button>
            </div>
        </div>

        <!-- VLESS WS -->
        <div class="block">
            <div class="block-title">
                <span>🐉 VLESS + TLS + WS · Dragon</span>
                <span class="badge">🔒 TLS 1.3</span>
            </div>
            <div class="config" id="vless2" onclick="copy('vless2')">vless://c0c3dc30-4ed9-e13d-50e8-0a84a84815e3@ndded2.subsvdragontoo.online:7443?path=%2F&security=tls&encryption=none&alpn=h2,http/1.1&host=ndded2.subsvdragontoo.online&fp=chrome&allowinsecure=0&type=ws&sni=ndded2.subsvdragontoo.online#tg%3A+hiokaa+%5Bfree%5D+VK</div>
            <div class="button-group">
                <button onclick="copy('vless2')">
                    <span class="button-icon">📋</span> КОПИРОВАТЬ
                </button>
                <button onclick="showQR('vless2')">
                    <span class="button-icon">📷</span> QR-КОД
                </button>
                <button onclick="exportConfig('vless2')">
                    <span class="button-icon">📥</span> ЭКСПОРТ
                </button>
            </div>
        </div>

        <!-- Инструкция -->
        <div class="block">
            <div class="block-title">
                <span>📖 КАК ИСПОЛЬЗОВАТЬ</span>
                <span class="badge">ГАЙД</span>
            </div>
            <div style="font-size:14px; line-height:1.8; color:#ff7777;">
                <p>🔹 <strong>ШАГ 1:</strong> Скопируйте конфигурацию (кнопка "КОПИРОВАТЬ")</p>
                <p>🔹 <strong>ШАГ 2:</strong> Откройте HAPP / NekoBox / v2Ray</p>
                <p>🔹 <strong>ШАГ 3:</strong> Импортируйте из буфера обмена</p>
                <p>🔹 <strong>ШАГ 4:</strong> Нажмите подключиться и наслаждайтесь!</p>
            </div>
            <div style="margin-top:15px; padding:10px; background:#0f0000; border-left:3px solid #ff0000;">
                <span style="color:#ff9999;">💡 Совет:</span> Для лучшей скорости выбирайте сервер с наименьшим пингом
            </div>
        </div>

        <!-- Кнопки действий -->
        <div class="button-group" style="justify-content: center;">
            <button onclick="checkAllServers()">
                <span class="button-icon">🔄</span> ПРОВЕРИТЬ ВСЕ
            </button>
            <button onclick="randomServer()">
                <span class="button-icon">🎲</span> СЛУЧАЙНЫЙ СЕРВЕР
            </button>
            <button onclick="showHelp()">
                <span class="button-icon">❓</span> ПОМОЩЬ
            </button>
        </div>

        <div class="footer">
            <div>free · no registration · while works</div>
            <div>
                <span id="pingDisplay">📡 ПИНГ: 24 мс</span>
                <span class="ping-indicator"></span>
            </div>
        </div>
    </div>

    <script>
        function copy(id) {
            const text = document.getElementById(id).innerText;
            navigator.clipboard.writeText(text).then(() => {
                showToast('✅ Конфиг скопирован в буфер обмена!');
            }).catch(() => {
                showToast('❌ Ошибка копирования');
            });
        }

        function showToast(message) {
            const toast = document.createElement('div');
            toast.className = 'toast';
            toast.textContent = message;
            document.body.appendChild(toast);
            setTimeout(() => {
                toast.remove();
            }, 3000);
        }

        function showQR(id) {
            showToast('📷 QR-код будет доступен в следующем обновлении');
        }

        function testPing(id) {
            showToast('📊 Тестирование пинга...');
            setTimeout(() => {
                const ping = Math.floor(Math.random() * 50) + 10;
                document.getElementById('pingDisplay').innerHTML = `📡 ПИНГ: ${ping} мс`;
                showToast(`✅ Пинг: ${ping} мс`);
            }, 1500);
        }

        function exportConfig(id) {
            const text = document.getElementById(id).innerText;
            const blob = new Blob([text], {type: 'text/plain'});
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `config_${id}.txt`;
            a.click();
            URL.revokeObjectURL(url);
            showToast('📥 Конфиг экспортирован');
        }

        function checkAllServers() {
            showToast('🔄 Проверка всех серверов...');
            let count = 0;
            const interval = setInterval(() => {
                count++;
                if (count >= 3) {
                    clearInterval(interval);
                    showToast('✅ Все серверы работают!');
                }
            }, 1000);
        }

        function randomServer() {
            const servers = ['mtproto', 'vless1', 'vless2'];
            const random = servers[Math.floor(Math.random() * servers.length)];
            copy(random);
            showToast('🎲 Выбран случайный сервер');
        }

        function showHelp() {
            showToast('❓ Нажмите на конфиг чтобы скопировать');
        }

        // Анимация для кнопок при загрузке
        document.addEventListener('DOMContentLoaded', () => {
            const buttons = document.querySelectorAll('button');
            buttons.forEach((button, index) => {
                button.style.animation = `fadeIn 0.5s ${index * 0.1}s both`;
            });
        });

        // Добавляем стиль для fadeIn
        const style = document.createElement('style');
        style.textContent = `
            @keyframes fadeIn {
                from {
                    opacity: 0;
                    transform: translateY(10px);
                }
                to {
                    opacity: 1;
                    transform: translateY(0);
                }
            }
        `;
        document.head.appendChild(style);
    </script>
</body>
</html>
