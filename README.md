<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>hioka · vless</title>
    <style>
        body {
            background: #0a0000;
            color: #ff3333;
            font-family: 'Courier New', monospace;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 900px;
            margin: 0 auto;
            border: 1px solid #ff3333;
            padding: 20px;
        }
        .header {
            border-bottom: 1px solid #ff3333;
            padding-bottom: 10px;
            margin-bottom: 25px;
        }
        .header h1 {
            margin: 0;
            font-size: 24px;
            font-weight: normal;
        }
        .block {
            margin: 25px 0;
            padding: 15px;
            border: 1px solid #ff3333;
            background: #050000;
        }
        .block-title {
            margin: -15px -15px 15px -15px;
            padding: 8px 15px;
            background: #1f0000;
            border-bottom: 1px solid #ff3333;
            font-weight: bold;
        }
        .config {
            font-family: 'Courier New', monospace;
            word-break: break-all;
            font-size: 13px;
            line-height: 1.5;
            margin: 15px 0;
            padding: 10px;
            background: #0f0000;
            border-left: 3px solid #ff3333;
        }
        button {
            background: #0f0000;
            border: 1px solid #ff3333;
            color: #ff3333;
            padding: 8px 15px;
            font-family: 'Courier New', monospace;
            cursor: pointer;
            margin-right: 10px;
        }
        button:hover {
            background: #ff3333;
            color: #0a0000;
        }
        .footer {
            margin-top: 30px;
            padding-top: 15px;
            border-top: 1px solid #ff3333;
            font-size: 12px;
            color: #5f0000;
        }
        a {
            color: #ff3333;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
        .link-group {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin: 15px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>hioka vpn · free vless</h1>
            <div style="color:#5f0000; margin-top:5px;">3 configs · 2025</div>
        </div>

        <!-- MTProto -->
        <div class="block">
            <div class="block-title">mtproto · telegram proxy</div>
            <div class="config" id="mtproto">https://t.me/proxy?server=xfs1.gbird.top&port=6443&secret=ddecad3d673e42dc10cae6fa9bcebcd5f6</div>
            <div class="link-group">
                <button onclick="copy('mtproto')">copy</button>
                <a href="https://t.me/proxy?server=xfs1.gbird.top&port=6443&secret=ddecad3d673e42dc10cae6fa9bcebcd5f6" target="_blank"><button>open in tg</button></a>
            </div>
        </div>

        <!-- VLESS Reality -->
        <div class="block">
            <div class="block-title">vless + reality · vk mirror</div>
            <div class="config" id="vless1">vless://83a11d95-1b15-4668-a675-00148622b2b1@95.163.183.205:443?mode=auto&path=%2F&security=reality&encryption=none&pbk=pQYGdr-ee0TotzdikPWnqJgKbX8OYcPNkJpH9scxjB0&fp=chrome&allowinsecure=0&type=xhttp&sni=sun6-21.userapi.com&sid=dde66ef1#tg%3Ahiokaaa++%5Bfree%5D+VK2</div>
            <button onclick="copy('vless1')">copy</button>
        </div>

        <!-- VLESS WS -->
        <div class="block">
            <div class="block-title">vless + tls + ws · dragon</div>
            <div class="config" id="vless2">vless://c0c3dc30-4ed9-e13d-50e8-0a84a84815e3@ndded2.subsvdragontoo.online:7443?path=%2F&security=tls&encryption=none&alpn=h2,http/1.1&host=ndded2.subsvdragontoo.online&fp=chrome&allowinsecure=0&type=ws&sni=ndded2.subsvdragontoo.online#tg%3A+hiokaa+%5Bfree%5D+VK</div>
            <button onclick="copy('vless2')">copy</button>
        </div>

        <!-- how to use -->
        <div class="block">
            <div class="block-title">how to use</div>
            <div style="font-size:14px; line-height:1.8;">
                1. copy config<br>
                2. open happ / nekobox / v2ray<br>
                3. import from clipboard<br>
                4. connect
            </div>
        </div>

        <div class="footer">
            free · no registration · while works
        </div>
    </div>

    <script>
        function copy(id) {
            const text = document.getElementById(id).innerText;
            navigator.clipboard.writeText(text);
        }
    </script>
</body>
</html>
