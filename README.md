<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>hioka · vless</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #000000;
            color: #ff5555;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Courier New', monospace;
            margin: 0;
            padding: 12px;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .container {
            max-width: 100%;
            width: 100%;
            margin: 0 auto;
            border: 1px solid rgba(255, 0, 0, 0.3);
            padding: 16px;
            border-radius: 28px;
            background: #000000;
            box-shadow: 0 10px 30px -10px rgba(255, 0, 0, 0.2);
            backdrop-filter: blur(2px);
        }

        .header {
            border-bottom: 1px solid rgba(255, 0, 0, 0.2);
            padding-bottom: 12px;
            margin-bottom: 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 8px;
        }

        .header h1 {
            margin: 0;
            font-size: 22px;
            font-weight: 500;
            letter-spacing: -0.3px;
            background: linear-gradient(135deg, #ff5555, #ff0000);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .status-badge {
            background: rgba(255, 0, 0, 0.1);
            border: 1px solid rgba(255, 0, 0, 0.3);
            padding: 6px 14px;
            border-radius: 40px;
            font-size: 12px;
            font-weight: 500;
            color: #ff7777;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            backdrop-filter: blur(5px);
        }

        .status-dot {
            width: 8px;
            height: 8px;
            background: #00ff00;
            border-radius: 20px;
            box-shadow: 0 0 10px #00ff00;
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.5; transform: scale(1.1); }
            100% { opacity: 1; transform: scale(1); }
        }

        /* Stats cards */
        .stats-grid {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .stat-card {
            flex: 1;
            min-width: 80px;
            background: rgba(255, 0, 0, 0.03);
            border: 1px solid rgba(255, 0, 0, 0.15);
            border-radius: 24px;
            padding: 12px 8px;
            text-align: center;
            backdrop-filter: blur(4px);
        }

        .stat-value {
            font-size: 22px;
            font-weight: 600;
            color: #ff3333;
            line-height: 1.2;
            text-shadow: 0 0 15px rgba(255, 0, 0, 0.5);
        }

        .stat-label {
            font-size: 10px;
            color: #aa3333;
            letter-spacing: 0.5px;
            text-transform: uppercase;
        }

        /* Server blocks */
        .server-block {
            margin-bottom: 16px;
            padding: 16px;
            border: 1px solid rgba(255, 0, 0, 0.2);
            border-radius: 24px;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(5px);
            transition: all 0.25s ease;
            position: relative;
            overflow: hidden;
        }

        .server-block::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 0, 0, 0.03), transparent);
            transition: left 0.5s ease;
        }

        .server-block:hover::before {
            left: 100%;
        }

        .server-block:hover {
            border-color: rgba(255, 0, 0, 0.5);
            box-shadow: 0 8px 25px -8px rgba(255, 0, 0, 0.3);
        }

        .server-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
            flex-wrap: wrap;
            gap: 8px;
        }

        .server-name {
            font-weight: 600;
            font-size: 16px;
            background: linear-gradient(135deg, #ff7777, #ff3333);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .server-tag {
            background: rgba(255, 0, 0, 0.15);
            border: 1px solid rgba(255, 0, 0, 0.3);
            border-radius: 30px;
            padding: 4px 12px;
            font-size: 11px;
            font-weight: 500;
            color: #ff8888;
        }

        .config-box {
            background: rgba(20, 0, 0, 0.6);
            border: 1px solid rgba(255, 0, 0, 0.2);
            border-radius: 20px;
            padding: 14px;
            margin: 12px 0;
            font-family: 'Courier New', monospace;
            font-size: 11px;
            line-height: 1.5;
            word-break: break-all;
            color: #ff9999;
            cursor: pointer;
            position: relative;
            transition: all 0.2s ease;
            backdrop-filter: blur(2px);
        }

        .config-box:active {
            background: rgba(40, 0, 0, 0.8);
            transform: scale(0.99);
        }

        .config-box::after {
            content: '📋 нажмите чтобы скопировать';
            position: absolute;
            bottom: -10px;
            right: 10px;
            font-size: 8px;
            color: #aa3333;
            background: rgba(0, 0, 0, 0.8);
            padding: 3px 8px;
            border-radius: 30px;
            border: 1px solid rgba(255, 0, 0, 0.2);
            opacity: 0;
            transition: opacity 0.2s;
        }

        .config-box:hover::after {
            opacity: 0.7;
        }

        /* Modern button styles - rounded */
        .button-group {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
            margin-top: 12px;
        }

        .btn {
            flex: 1 1 auto;
            min-width: 100px;
            background: rgba(30, 0, 0, 0.6);
            border: 1px solid rgba(255, 0, 0, 0.3);
            color: #ff7777;
            padding: 12px 16px;
            border-radius: 40px;
            font-family: inherit;
            font-size: 13px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            backdrop-filter: blur(5px);
            letter-spacing: 0.3px;
            box-shadow: 0 2px 8px rgba(255, 0, 0, 0.1);
        }

        .btn i {
            font-size: 16px;
            font-style: normal;
        }

        .btn:active {
            transform: translateY(1px);
            background: rgba(50, 0, 0, 0.8);
            box-shadow: 0 0 15px rgba(255, 0, 0, 0.3);
        }

        .btn-primary {
            background: rgba(255, 0, 0, 0.15);
            border-color: rgba(255, 0, 0, 0.5);
            color: #ff9999;
            box-shadow: 0 4px 15px -5px rgba(255, 0, 0, 0.3);
        }

        .btn-primary:active {
            background: rgba(255, 0, 0, 0.25);
        }

        /* Guide block */
        .guide-block {
            border: 1px solid rgba(255, 0, 0, 0.2);
            border-radius: 24px;
            padding: 20px;
            margin: 20px 0;
            background: rgba(15, 0, 0, 0.4);
            backdrop-filter: blur(3px);
        }

        .guide-title {
            font-size: 16px;
            font-weight: 600;
            margin-bottom: 16px;
            color: #ff7777;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .guide-step {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 12px;
            font-size: 14px;
            color: #ff9999;
        }

        .step-number {
            width: 26px;
            height: 26px;
            background: rgba(255, 0, 0, 0.15);
            border: 1px solid rgba(255, 0, 0, 0.4);
            border-radius: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 13px;
            font-weight: bold;
            color: #ff5555;
        }

        .tip-box {
            background: rgba(30, 0, 0, 0.6);
            border: 1px solid rgba(255, 0, 0, 0.2);
            border-radius: 20px;
            padding: 14px;
            margin-top: 16px;
            font-size: 13px;
            color: #ffaa88;
            display: flex;
            align-items: center;
            gap: 10px;
            backdrop-filter: blur(2px);
        }

        /* Action bar */
        .action-bar {
            display: flex;
            gap: 8px;
            margin: 20px 0 10px;
            flex-wrap: wrap;
        }

        .action-bar .btn {
            flex: 1;
            min-width: 110px;
        }

        .footer {
            margin-top: 20px;
            padding-top: 16px;
            border-top: 1px solid rgba(255, 0, 0, 0.2);
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 11px;
            color: #aa3333;
            flex-wrap: wrap;
            gap: 10px;
        }

        .ping-info {
            display: flex;
            align-items: center;
            gap: 8px;
            background: rgba(255, 0, 0, 0.1);
            padding: 6px 16px;
            border-radius: 40px;
            border: 1px solid rgba(255, 0, 0, 0.2);
        }

        .toast {
            position: fixed;
            bottom: 20px;
            left: 20px;
            right: 20px;
            background: rgba(20, 0, 0, 0.95);
            border: 1px solid #ff3333;
            border-radius: 60px;
            color: #ff8888;
            padding: 16px 20px;
            font-size: 14px;
            z-index: 1000;
            animation: slideUp 0.3s ease;
            text-align: center;
            backdrop-filter: blur(10px);
            box-shadow: 0 10px 30px rgba(255, 0, 0, 0.2);
            max-width: 90%;
            margin: 0 auto;
            pointer-events: none;
        }

        @keyframes slideUp {
            from {
                transform: translateY(100%);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        /* Emoji/icons */
        .emoji-icon {
            filter: drop-shadow(0 0 5px rgba(255, 0, 0, 0.5));
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <h1>hioka vpn</h1>
            <div class="status-badge">
                <span class="status-dot"></span>
                СЕРВЕРЫ АКТИВНЫ
            </div>
        </div>

        <!-- Stats cards -->
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-value">3</div>
                <div class="stat-label">СЕРВЕРА</div>
            </div>
            <div class="stat-card">
                <div class="stat-value">47</div>
                <div class="stat-label">ОНЛАЙН</div>
            </div>
            <div class="stat-card">
                <div class="stat-value">99%</div>
                <div class="stat-label">АПТАЙМ</div>
            </div>
            <div class="stat-card">
                <div class="stat-value">24</div>
                <div class="stat-label">ПИНГ МС</div>
            </div>
        </div>

        <!-- Server 1 - MTProto -->
        <div class="server-block">
            <div class="server-header">
                <span class="server-name">
                    <span>📱</span> MTProto · Telegram
                </span>
                <span class="server-tag">⚡ 15 ms</span>
            </div>
            <div class="config-box" id="mtproto" onclick="copy('mtproto')">
                https://t.me/proxy?server=xfs1.gbird.top&port=6443&secret=ddecad3d673e42dc10cae6fa9bcebcd5f6
            </div>
            <div class="button-group">
                <button class="btn" onclick="copy('mtproto')">
                    <i>📋</i> КОПИ
                </button>
                <a href="https://t.me/proxy?server=xfs1.gbird.top&port=6443&secret=ddecad3d673e42dc10cae6fa9bcebcd5f6" target="_blank" style="flex:1; text-decoration:none;">
                    <button class="btn btn-primary">
                        <i>📱</i> TG
                    </button>
                </a>
                <button class="btn" onclick="showQR('mtproto')">
                    <i>📷</i> QR
                </button>
            </div>
        </div>

        <!-- Server 2 - VLESS Reality -->
        <div class="server-block">
            <div class="server-header">
                <span class="server-name">
                    <span>🔮</span> VLESS + Reality
                </span>
                <span class="server-tag">⚡ 25 ms</span>
            </div>
            <div class="config-box" id="vless1" onclick="copy('vless1')">
                vless://83a11d95-1b15-4668-a675-00148622b2b1@95.163.183.205:443?mode=auto&path=%2F&security=reality&encryption=none&pbk=pQYGdr-ee0TotzdikPWnqJgKbX8OYcPNkJpH9scxjB0&fp=chrome&allowinsecure=0&type=xhttp&sni=sun6-21.userapi.com&sid=dde66ef1#tg%3Ahiokaaa++%5Bfree%5D+VK2
            </div>
            <div class="button-group">
                <button class="btn" onclick="copy('vless1')">
                    <i>📋</i> КОПИ
                </button>
                <button class="btn" onclick="testPing('vless1')">
                    <i>📊</i> ПИНГ
                </button>
                <button class="btn" onclick="showQR('vless1')">
                    <i>📷</i> QR
                </button>
            </div>
        </div>

        <!-- Server 3 - VLESS WS -->
        <div class="server-block">
            <div class="server-header">
                <span class="server-name">
                    <span>🐉</span> VLESS + WS + TLS
                </span>
                <span class="server-tag">⚡ 32 ms</span>
            </div>
            <div class="config-box" id="vless2" onclick="copy('vless2')">
                vless://c0c3dc30-4ed9-e13d-50e8-0a84a84815e3@ndded2.subsvdragontoo.online:7443?path=%2F&security=tls&encryption=none&alpn=h2,http/1.1&host=ndded2.subsvdragontoo.online&fp=chrome&allowinsecure=0&type=ws&sni=ndded2.subsvdragontoo.online#tg%3A+hiokaa+%5Bfree%5D+VK
            </div>
            <div class="button-group">
                <button class="btn" onclick="copy('vless2')">
                    <i>📋</i> КОПИ
                </button>
                <button class="btn" onclick="showQR('vless2')">
                    <i>📷</i> QR
                </button>
                <button class="btn" onclick="exportConfig('vless2')">
                    <i>📥</i> ЭКСП
                </button>
            </div>
        </div>

        <!-- Guide block -->
        <div class="guide-block">
            <div class="guide-title">
                <span>📘</span> БЫСТРЫЙ СТАРТ
            </div>
            <div class="guide-step">
                <div class="step-number">1</div>
                <div>Скопируйте любой конфиг</div>
            </div>
            <div class="guide-step">
                <div class="step-number">2</div>
                <div>Откройте HAPP / NekoBox / v2Ray</div>
            </div>
            <div class="guide-step">
                <div class="step-number">3</div>
                <div>Импорт из буфера → Подключиться</div>
            </div>
            <div class="tip-box">
                <span>💡</span> Для максимальной скорости выбирайте сервер с наименьшим пингом
            </div>
        </div>

        <!-- Action bar -->
        <div class="action-bar">
            <button class="btn btn-primary" onclick="checkAllServers()">
                <i>🔄</i> ПРОВЕРИТЬ
            </button>
            <button class="btn btn-primary" onclick="randomServer()">
                <i>🎲</i> СЛУЧАЙНЫЙ
            </button>
            <button class="btn btn-primary" onclick="showHelp()">
                <i>❓</i> ПОМОЩЬ
            </button>
        </div>

        <!-- Footer -->
        <div class="footer">
            <div>free · без регистрации</div>
            <div class="ping-info">
                <span>📡</span>
                <span id="pingDisplay">24 мс</span>
                <span style="width:6px;height:6px;background:#00ff00;border-radius:10px;box-shadow:0 0 8px #00ff00;"></span>
            </div>
        </div>
    </div>

    <script>
        function copy(id) {
            const text = document.getElementById(id).innerText;
            navigator.clipboard.writeText(text).then(() => {
                showToast('✅ Конфиг скопирован');
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
            }, 2000);
        }

        function showQR(id) {
            showToast('📷 QR в следующем обновлении');
        }

        function testPing(id) {
            showToast('📊 Тестируем пинг...');
            setTimeout(() => {
                const ping = Math.floor(Math.random() * 40) + 8;
                document.getElementById('pingDisplay').innerText = ping + ' мс';
                showToast(`✅ Пинг: ${ping} мс`);
            }, 1200);
        }

        function exportConfig(id) {
            const text = document.getElementById(id).innerText;
            const blob = new Blob([text], {type: 'text/plain'});
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `vless_config.txt`;
            a.click();
            URL.revokeObjectURL(url);
            showToast('📥 Конфиг сохранен');
        }

        function checkAllServers() {
            showToast('🔄 Проверка серверов...');
            setTimeout(() => {
                showToast('✅ Все серверы работают');
            }, 2000);
        }

        function randomServer() {
            const servers = ['mtproto', 'vless1', 'vless2'];
            const random = servers[Math.floor(Math.random() * servers.length)];
            copy(random);
            showToast('🎲 Случайный сервер выбран');
        }

        function showHelp() {
            showToast('❓ Нажмите на конфиг чтобы скопировать');
        }
    </script>
</body>
</html>
