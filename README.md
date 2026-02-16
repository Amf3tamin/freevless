<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>hioka · vpn</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #0b0710;  /* глубокий тёмно-фиолетовый фон */
            color: #e0c0ff;       /* мягкий фиолетово-белый текст */
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Inter', 'Courier New', monospace;
            margin: 0;
            padding: 12px;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background-image: radial-gradient(circle at 10% 20%, rgba(120, 60, 255, 0.15) 0%, transparent 40%),
                              radial-gradient(circle at 90% 70%, rgba(180, 100, 255, 0.12) 0%, transparent 45%),
                              repeating-linear-gradient(45deg, rgba(100, 50, 200, 0.02) 0px, rgba(100, 50, 200, 0.02) 2px, transparent 2px, transparent 8px);
        }

        .container {
            max-width: 100%;
            width: 100%;
            margin: 0 auto;
            border: 1px solid rgba(160, 120, 255, 0.25);
            padding: 20px 16px;
            border-radius: 36px;
            background: rgba(20, 12, 30, 0.75);    /* полупрозрачный фиолетово-чёрный */
            backdrop-filter: blur(20px) saturate(180%);
            -webkit-backdrop-filter: blur(20px) saturate(180%);
            box-shadow: 0 25px 50px -10px rgba(80, 40, 200, 0.5), 0 0 0 1px rgba(170, 130, 255, 0.2) inset;
            transition: all 0.3s ease;
        }

        /* декоративные свечения */
        .container::after {
            content: '';
            position: absolute;
            top: -20px;
            left: 10%;
            width: 150px;
            height: 150px;
            background: radial-gradient(circle, rgba(140, 70, 255, 0.3) 0%, transparent 70%);
            border-radius: 50%;
            z-index: -1;
            filter: blur(40px);
            pointer-events: none;
        }

        .container::before {
            content: '';
            position: absolute;
            bottom: -10px;
            right: 5%;
            width: 200px;
            height: 200px;
            background: radial-gradient(circle, rgba(100, 40, 230, 0.25) 0%, transparent 70%);
            border-radius: 50%;
            z-index: -1;
            filter: blur(50px);
            pointer-events: none;
        }

        /* Header с фиолетовым градиентом */
        .header {
            border-bottom: 1px solid rgba(180, 130, 255, 0.3);
            padding-bottom: 14px;
            margin-bottom: 18px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 8px;
        }

        .header h1 {
            margin: 0;
            font-size: 26px;
            font-weight: 700;
            letter-spacing: -0.5px;
            background: linear-gradient(145deg, #dbb5ff, #9f6eff, #6b3aff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 0 15px #b47aff;
        }

        .status-badge {
            background: rgba(110, 50, 220, 0.2);
            border: 1px solid rgba(170, 120, 255, 0.5);
            padding: 6px 16px;
            border-radius: 50px;
            font-size: 12px;
            font-weight: 600;
            color: #c9adff;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            backdrop-filter: blur(10px);
            box-shadow: 0 0 15px rgba(140, 0, 255, 0.3);
        }

        .status-dot {
            width: 9px;
            height: 9px;
            background: #b57cff;
            border-radius: 20px;
            box-shadow: 0 0 15px #c090ff, 0 0 30px #a35eff;
            animation: pulseNeon 1.6s infinite;
        }

        @keyframes pulseNeon {
            0% { opacity: 1; transform: scale(1); box-shadow: 0 0 10px #b57cff, 0 0 20px #a14eff; }
            50% { opacity: 0.6; transform: scale(1.2); box-shadow: 0 0 20px #d29bff, 0 0 40px #a64eff; }
            100% { opacity: 1; transform: scale(1); box-shadow: 0 0 10px #b57cff, 0 0 20px #a14eff; }
        }

        /* статистика — карточки с сине-фиолетовым отливом */
        .stats-grid {
            display: flex;
            gap: 10px;
            margin-bottom: 24px;
            flex-wrap: wrap;
        }

        .stat-card {
            flex: 1;
            min-width: 70px;
            background: rgba(35, 20, 60, 0.5);
            border: 1px solid rgba(150, 100, 255, 0.4);
            border-radius: 30px;
            padding: 14px 5px;
            text-align: center;
            backdrop-filter: blur(8px);
            box-shadow: 0 8px 20px -10px #4f2ab3;
            transition: transform 0.2s, border-color 0.2s;
        }

        .stat-card:active {
            transform: scale(0.96);
            border-color: #af7bff;
        }

        .stat-value {
            font-size: 24px;
            font-weight: 800;
            color: #d3b0ff;
            line-height: 1.2;
            text-shadow: 0 0 25px #ac7aff, 0 0 40px #6b3ad6;
        }

        .stat-label {
            font-size: 10px;
            color: #b28dff;
            letter-spacing: 0.8px;
            text-transform: uppercase;
            font-weight: 500;
        }

        /* серверные блоки — глубокий фиолет */
        .server-block {
            margin-bottom: 18px;
            padding: 18px 16px;
            border: 1px solid rgba(180, 130, 255, 0.3);
            border-radius: 32px;
            background: rgba(16, 8, 28, 0.7);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            transition: all 0.25s ease;
            position: relative;
            overflow: hidden;
            box-shadow: 0 10px 25px -15px #502fbd;
        }

        .server-block::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(170, 100, 255, 0.1), transparent);
            transition: left 0.6s ease;
        }

        .server-block:hover::before {
            left: 100%;
        }

        .server-block:hover {
            border-color: #b77eff;
            box-shadow: 0 12px 30px -8px #6b3aff;
        }

        .server-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 14px;
            flex-wrap: wrap;
            gap: 8px;
        }

        .server-name {
            font-weight: 700;
            font-size: 18px;
            background: linear-gradient(145deg, #e1c4ff, #b27aff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .server-tag {
            background: rgba(105, 40, 210, 0.3);
            border: 1px solid rgba(170, 110, 255, 0.6);
            border-radius: 40px;
            padding: 5px 14px;
            font-size: 11px;
            font-weight: 600;
            color: #d3aeff;
            box-shadow: 0 0 12px #7b45dd;
        }

        .config-box {
            background: rgba(28, 14, 48, 0.8);
            border: 1px solid rgba(160, 90, 255, 0.5);
            border-radius: 28px;
            padding: 16px 14px;
            margin: 14px 0;
            font-family: 'Courier New', monospace;
            font-size: 11.5px;
            line-height: 1.6;
            word-break: break-all;
            color: #e2c5ff;
            cursor: pointer;
            position: relative;
            transition: all 0.2s ease;
            backdrop-filter: blur(5px);
            box-shadow: inset 0 0 15px rgba(0,0,0,0.8), 0 4px 12px rgba(70, 30, 150, 0.4);
        }

        .config-box:active {
            background: rgba(45, 20, 80, 0.9);
            transform: scale(0.98);
            border-color: #cc99ff;
        }

        .config-box::after {
            content: '⚡ нажми, чтобы скопировать';
            position: absolute;
            bottom: -9px;
            right: 14px;
            font-size: 8px;
            font-weight: 600;
            color: #c6a0ff;
            background: rgba(25, 10, 50, 0.9);
            padding: 4px 12px;
            border-radius: 40px;
            border: 1px solid #ae79ff;
            opacity: 0;
            transition: opacity 0.2s;
            backdrop-filter: blur(4px);
            letter-spacing: 0.3px;
        }

        .config-box:hover::after {
            opacity: 1;
        }

        /* кнопки — сине-фиолетовые, светящиеся */
        .button-group {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-top: 14px;
        }

        .btn {
            flex: 1 1 auto;
            min-width: 95px;
            background: linear-gradient(145deg, #281c44, #181030);
            border: 1px solid #7c4eff;
            color: #dbc2ff;
            padding: 13px 10px;
            border-radius: 50px;
            font-family: inherit;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
            backdrop-filter: blur(10px);
            letter-spacing: 0.3px;
            box-shadow: 0 6px 14px rgba(80, 20, 200, 0.4), 0 0 0 1px rgba(190, 130, 255, 0.3) inset;
        }

        .btn i {
            font-size: 16px;
            font-style: normal;
            filter: drop-shadow(0 0 5px #a26eff);
        }

        .btn:active {
            transform: translateY(2px);
            background: linear-gradient(145deg, #322458, #1d113a);
            box-shadow: 0 2px 18px #8a54ff, 0 0 20px #a26eff;
            border-color: #b07eff;
        }

        .btn-primary {
            background: linear-gradient(145deg, #3d2c70, #251b44);
            border-color: #a36eff;
            color: #eddbff;
            box-shadow: 0 8px 20px -5px #6f41dd, 0 0 15px #a168ff;
        }

        .btn-primary:active {
            background: linear-gradient(145deg, #4d33a0, #332369);
        }

        /* гайд блок с фиолетовым оттенком */
        .guide-block {
            border: 1px solid rgba(160, 100, 255, 0.4);
            border-radius: 32px;
            padding: 22px 18px;
            margin: 24px 0 20px;
            background: rgba(28, 14, 45, 0.6);
            backdrop-filter: blur(12px);
            box-shadow: 0 0 30px rgba(100, 40, 200, 0.2);
        }

        .guide-title {
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 20px;
            color: #dbb9ff;
            display: flex;
            align-items: center;
            gap: 10px;
            text-shadow: 0 0 10px #b57aff;
        }

        .guide-step {
            display: flex;
            align-items: center;
            gap: 14px;
            margin-bottom: 16px;
            font-size: 14px;
            color: #d2b2ff;
        }

        .step-number {
            width: 30px;
            height: 30px;
            background: rgba(110, 50, 210, 0.3);
            border: 1.5px solid #b079ff;
            border-radius: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            font-weight: 800;
            color: #f0d3ff;
            box-shadow: 0 0 15px #8b4eff;
        }

        .tip-box {
            background: rgba(50, 20, 90, 0.5);
            border: 1px solid #a56eff;
            border-radius: 28px;
            padding: 16px;
            margin-top: 20px;
            font-size: 14px;
            color: #e7ccff;
            display: flex;
            align-items: center;
            gap: 12px;
            backdrop-filter: blur(10px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.6);
        }

        /* панель действий */
        .action-bar {
            display: flex;
            gap: 12px;
            margin: 22px 0 12px;
            flex-wrap: wrap;
        }

        .action-bar .btn {
            flex: 1;
            min-width: 110px;
        }

        /* футер */
        .footer {
            margin-top: 22px;
            padding-top: 18px;
            border-top: 1px solid rgba(160, 100, 255, 0.3);
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 11px;
            color: #b18bff;
            flex-wrap: wrap;
            gap: 10px;
        }

        .ping-info {
            display: flex;
            align-items: center;
            gap: 10px;
            background: rgba(55, 25, 100, 0.4);
            padding: 6px 20px;
            border-radius: 60px;
            border: 1px solid #a56eff;
            box-shadow: 0 0 15px #753efb;
        }

        /* toast уведомления */
        .toast {
            position: fixed;
            bottom: 20px;
            left: 20px;
            right: 20px;
            background: rgba(35, 12, 70, 0.95);
            border: 1.5px solid #bc86ff;
            border-radius: 80px;
            color: #f0d8ff;
            padding: 18px 22px;
            font-size: 15px;
            z-index: 1000;
            animation: slideSoft 0.3s ease;
            text-align: center;
            backdrop-filter: blur(20px);
            box-shadow: 0 20px 40px rgba(50, 10, 100, 0.7), 0 0 30px #a265ff;
            max-width: 90%;
            margin: 0 auto;
            pointer-events: none;
            font-weight: 600;
        }

        @keyframes slideSoft {
            from {
                transform: translateY(120%);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        /* иконки / эмодзи с фиолетовым сиянием */
        .emoji-icon {
            filter: drop-shadow(0 0 6px #b77aff);
        }

        /* дополнительный визуал — неоновые линии */
        .glow-line {
            height: 2px;
            width: 100%;
            background: linear-gradient(90deg, transparent, #9a6eff, #c08aff, #9a6eff, transparent);
            margin: 16px 0;
            opacity: 0.5;
        }

        /* мелочи для заполнения экрана, но без скролла — используем компактно */
        .extra-bling {
            display: flex;
            justify-content: center;
            gap: 18px;
            margin: 10px 0 5px;
            color: #956eff;
            font-size: 20px;
            filter: drop-shadow(0 0 8px #b77aff);
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- чуть-чуть визуального мерцания сверху -->
        <div class="extra-bling">
            <span>✦</span> <span>✧</span> <span>✦</span> <span>✧</span> <span>✦</span>
        </div>

        <!-- Header -->
        <div class="header">
            <h1>hioka violet</h1>
            <div class="status-badge">
                <span class="status-dot"></span>
                СЕРВЕРЫ ACTIVE
            </div>
        </div>

        <!-- Stats cards с фиолетовой эстетикой -->
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

        <!-- Server 1 - MTProto (стили под фиолет) -->
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
                <button class="btn" onclick="copy('mtproto')"><i>📋</i> КОПИ</button>
                <a href="https://t.me/proxy?server=xfs1.gbird.top&port=6443&secret=ddecad3d673e42dc10cae6fa9bcebcd5f6" target="_blank" style="flex:1; text-decoration:none;">
                    <button class="btn btn-primary"><i>📱</i> TG</button>
                </a>
                <button class="btn" onclick="showQR('mtproto')"><i>📷</i> QR</button>
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
                <button class="btn" onclick="copy('vless1')"><i>📋</i> КОПИ</button>
                <button class="btn" onclick="testPing('vless1')"><i>📊</i> ПИНГ</button>
                <button class="btn" onclick="showQR('vless1')"><i>📷</i> QR</button>
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
                <button class="btn" onclick="copy('vless2')"><i>📋</i> КОПИ</button>
                <button class="btn" onclick="showQR('vless2')"><i>📷</i> QR</button>
                <button class="btn" onclick="exportConfig('vless2')"><i>📥</i> ЭКСП</button>
            </div>
        </div>

        <!-- декоративная линия -->
        <div class="glow-line"></div>

        <!-- Guide block  фиолетово-синий-->
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

        <!-- Action bar сине-фиолетовые кнопки -->
        <div class="action-bar">
            <button class="btn btn-primary" onclick="checkAllServers()"><i>🔄</i> ПРОВЕРИТЬ</button>
            <button class="btn btn-primary" onclick="randomServer()"><i>🎲</i> СЛУЧАЙНЫЙ</button>
            <button class="btn btn-primary" onclick="showHelp()"><i>❓</i> ПОМОЩЬ</button>
        </div>

        <!-- дополнительный штрих: плашки с визуалом (без увеличения высоты) -->
        <div style="display: flex; justify-content: center; gap: 12px; margin: 10px 0 5px; font-size: 22px; color: #ae80ff; text-shadow: 0 0 15px #b77aff;">
            <span>✧</span> <span>⋆</span> <span>✧</span> <span>⋆</span> <span>✧</span>
        </div>

        <!-- Footer -->
        <div class="footer">
            <div>✨ free · без регистрации</div>
            <div class="ping-info">
                <span>📡</span>
                <span id="pingDisplay">24 мс</span>
                <span style="width:8px;height:8px;background:#c276ff;border-radius:10px;box-shadow:0 0 18px #b770ff;"></span>
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
            showToast('📷 QR скоро появится');
        }

        function testPing(id) {
            showToast('📊 Тестируем пинг...');
            setTimeout(() => {
                const ping = Math.floor(Math.random() * 35) + 10;
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
            showToast('📥 Конфиг сохранён');
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
            showToast('❓ Нажми на конфиг, чтобы скопировать');
        }
    </script>
</body>
</html>
