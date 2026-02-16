<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HIOKA VPN · FREE VLESS</title>
    <style>
        body {
            background: #0a0a0a;
            color: #33ff33;
            font-family: 'Courier New', monospace;
            padding: 20px;
            margin: 0;
        }
        .container {
            max-width: 900px;
            margin: 0 auto;
            border: 1px solid #33ff33;
            padding: 20px;
        }
        h1 {
            text-align: center;
            border-bottom: 1px solid #33ff33;
            padding-bottom: 10px;
            letter-spacing: 2px;
        }
        .config {
            background: #111;
            border-left: 3px solid #33ff33;
            margin: 20px 0;
            padding: 15px;
            word-break: break-all;
            font-size: 14px;
        }
        .label {
            color: #88ff88;
            font-weight: bold;
            margin-bottom: 5px;
        }
        button {
            background: #1a1a1a;
            border: 1px solid #33ff33;
            color: #33ff33;
            padding: 8px 15px;
            font-family: 'Courier New', monospace;
            cursor: pointer;
            margin-right: 10px;
        }
        button:hover {
            background: #33ff33;
            color: #0a0a0a;
        }
        .footer {
            margin-top: 30px;
            text-align: center;
            font-size: 12px;
            color: #226622;
            border-top: 1px solid #226622;
            padding-top: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>█ HIOKA VPN █ FREE VLESS</h1>

        <div class="label">▶ MTProto (для Telegram)</div>
        <div class="config" id="mtproto">https://t.me/proxy?server=xfs1.gbird.top&port=6443&secret=ddecad3d673e42dc10cae6fa9bcebcd5f6</div>
        <button onclick="copyText('mtproto')">КОПИРОВАТЬ</button>
        <a href="https://t.me/proxy?server=xfs1.gbird.top&port=6443&secret=ddecad3d673e42dc10cae6fa9bcebcd5f6" target="_blank"><button>ОТКРЫТЬ В TG</button></a>

        <div class="label" style="margin-top:30px;">▶ VLESS Reality (VK mirror)</div>
        <div class="config" id="vless1">vless://83a11d95-1b15-4668-a675-00148622b2b1@95.163.183.205:443?mode=auto&path=%2F&security=reality&encryption=none&pbk=pQYGdr-ee0TotzdikPWnqJgKbX8OYcPNkJpH9scxjB0&fp=chrome&allowinsecure=0&type=xhttp&sni=sun6-21.userapi.com&sid=dde66ef1#tg%3Ahiokaaa++%5Bfree%5D+VK2</div>
        <button onclick="copyText('vless1')">КОПИРОВАТЬ</button>

        <div class="label" style="margin-top:30px;">▶ VLESS + TLS + WS (Dragon)</div>
        <div class="config" id="vless2">vless://c0c3dc30-4ed9-e13d-50e8-0a84a84815e3@ndded2.subsvdragontoo.online:7443?path=%2F&security=tls&encryption=none&alpn=h2,http/1.1&host=ndded2.subsvdragontoo.online&fp=chrome&allowinsecure=0&type=ws&sni=ndded2.subsvdragontoo.online#tg%3A+hiokaa+%5Bfree%5D+VK</div>
        <button onclick="copyText('vless2')">КОПИРОВАТЬ</button>

        <div style="margin-top:40px; background:#111; padding:15px;">
            <div class="label">КАК ИСПОЛЬЗОВАТЬ:</div>
            <p>1. Скопировать нужную ссылку</p>
            <p>2. Вставить в клиент (Happ, v2Ray, Nekobox, Matsuri)</p>
            <p>3. Подключиться</p>
            <p>Бесплатно. Без регистрации. Пока работают.</p>
        </div>

        <div class="footer">
            HIOKA VPN · FREE VLESS · 2025
        </div>
    </div>

    <script>
        function copyText(elementId) {
            const text = document.getElementById(elementId).innerText;
            navigator.clipboard.writeText(text).then(() => {
                alert('✅ Скопировано: ' + text.substring(0, 30) + '...');
            }).catch(() => {
                alert('❌ Ошибка копирования');
            });
        }
    </script>
</body>
</html>
