<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Кластеры WB</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-weight: 200;
            color: var(--tg-theme-text-color);
            background: var(--tg-theme-bg-color);
        }

        #main {
            width: 100%;
            padding: 2%;
            text-align: center;
        }

        h3 {
            margin-top: 10px;
            margin-bottom: 10px;
        }

        button {
            border: 0;
            border-radius: 5px;
            margin-top: 10px;
            height: 50px;
            width: 120px;
            font-size: 20px;
            cursor: pointer;
            transition: all 500ms ease;
            color: var(--tg-theme-button-color);
            background: var(--tg-theme-button-text-color);
        }

        button:hover {
            background: var(--tg-theme-secondary-bg-color);
        }
    </style>
</head>
<body>
    <div id="main">
        <h3>Необходимо ввести строку в поле</h3>
        <form>
            <textarea placeholder="Вставите строку" cols="30" rows="15" id="text_cluster"></textarea><br><br>
            <div id="error"></div>
            <div id="process"></div>
            <button id="send">Отправить</button>
        </form>
    </div>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <script>
        let tg = window.Telegram.WebApp;
        let send = document.getElementById("send");
        tg.expand();
        send.addEventListener("click", () => {
            document.getElementById("error").innerText = '';
            let text = document.getElementById("text_cluster").value;
            if(text.length == 0) {
                document.getElementById("error").innerText = 'Пустое значение';
                return;
            } else if (!(text.startsWith('{"words"'))){
                document.getElementById("error").innerText = 'Не верная строка в начале';
                return;
            } else if (!(text.endsWith('}}'))){
                document.getElementById("error").innerText = 'Не верная строка в конце';
                return;
            }

            let data = {
                text: text
            }
            document.getElementById("process").innerText = 'Let data';
            tg.sendData(JSON.stringify(data));
            document.getElementById("process").innerText = 'sendData';
            tg.close();
        });
    </script>
</body>
</html>
