<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¡Ábreme! ❤️</title>
    <style>
        :root {
            --bg: #000000;
            --star-color-1: #ffffff;
            --star-color-2: #add8e6;
            --star-color-3: #ffc0cb;
            --star-color-4: #ffd700;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: var(--bg);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            flex-direction: column;
            margin: 0;
            padding: 20px;
            text-align: center;
            overflow: hidden;
            position: relative;
        }

        /* FONDO DE ESTRELLAS REFORZADO */
        body::before, body::after {
            content: "";
            position: absolute; 
            inset: -100%; 
            background-repeat: repeat;
            z-index: -1;
            pointer-events: none;
        }

        body::before {
            background-size: 250px 250px;
            background-image: 
                radial-gradient(2px 2px at 25px 35px, var(--star-color-1) 50%, transparent 51%),
                radial-gradient(3px 3px at 60px 90px, var(--star-color-2) 50%, transparent 51%),
                radial-gradient(2px 2px at 120px 50px, var(--star-color-3) 50%, transparent 51%),
                radial-gradient(4px 4px at 150px 160px, var(--star-color-4) 50%, transparent 51%),
                radial-gradient(2px 2px at 200px 240px, var(--star-color-1) 50%, transparent 51%),
                radial-gradient(3px 3px at 240px 60px, var(--star-color-2) 50%, transparent 51%),
                radial-gradient(2px 2px at 40px 210px, var(--star-color-3) 50%, transparent 51%),
                radial-gradient(3px 3px at 90px 170px, var(--star-color-4) 50%, transparent 51%);
            animation: twinkleA 3s infinite ease-in-out;
        }

        body::after {
            background-size: 400px 400px;
            background-image: 
                radial-gradient(2px 2px at 100px 100px, var(--star-color-1) 50%, transparent 51%),
                radial-gradient(4px 4px at 210px 310px, var(--star-color-4) 50%, transparent 51%),
                radial-gradient(2px 2px at 310px 110px, var(--star-color-2) 50%, transparent 51%),
                radial-gradient(3px 3px at 55px 355px, var(--star-color-3) 50%, transparent 51%),
                radial-gradient(2px 2px at 350px 250px, var(--star-color-1) 50%, transparent 51%),
                radial-gradient(3px 3px at 150px 50px, var(--star-color-4) 50%, transparent 51%);
            animation: twinkleB 5s infinite ease-in-out;
        }

        @keyframes twinkleA { 
            0%, 100% { opacity: 1; transform: scale(1); } 
            50% { opacity: 0.4; transform: scale(1.05); } 
        }

        @keyframes twinkleB { 
            0%, 100% { opacity: 0.8; } 
            50% { opacity: 0.2; } 
        }

        .title {
            font-size: 26px;
            font-weight: bold;
            color: #ff4d6d;
            margin-bottom: 30px;
            max-width: 600px;
            line-height: 1.4;
            text-shadow: 0 0 15px rgba(255, 77, 109, 0.8);
            z-index: 1;
        }

        .container {
            display: flex;
            gap: 20px;
            align-items: center;
            justify-content: center;
            flex-wrap: wrap;
            z-index: 1;
        }

        .option {
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(255, 43, 79, 0.5);
            padding: 10px;
            min-width: 100px;
            min-height: 60px;
            border: none;
        }

        #yes {
            background-color: #ff4d6d;
            color: white;
            width: 100px;
            height: 100px;
        }

        #no {
            background-color: #fb6f92;
            color: white;
            padding: 15px 25px;
        }

        .message {
            margin-top: 30px;
            font-size: 28px;
            font-weight: bold;
            color: #ff4d6d;
            display: none;
            animation: aparecer 0.5s ease-out;
            text-shadow: 0 0 20px rgba(255, 77, 109, 1);
            z-index: 1;
        }

        @keyframes aparecer {
            from { opacity: 0; transform: scale(0.5); }
            to { opacity: 1; transform: scale(1); }
        }

        .emoji {
            font-size: 100px;
            margin-top: 20px;
            z-index: 1;
        }
    </style>
</head>
<body>
    <div class="title" id="mainTitle">Hola Valentina, ¿cómo estás? Quería preguntarte si quieres ser mi San Valentín este año, así sea virtual, ¿qué dices? Eres libre de decir que no.</div>
    
    <div class="container" id="buttonsContainer">
        <button class="option" id="yes">Sí</button>
        <button class="option" id="no">No</button>
    </div>

    <div class="message" id="message">¡Sabía que dirías que sí! ❤️</div>
    <div class="emoji" id="emojiContainer">☀️</div>
    
    <script>
        let yesButton = document.getElementById('yes');
        let noButton = document.getElementById('no');
        let message = document.getElementById('message');
        let mainTitle = document.getElementById('mainTitle');
        let emojiContainer = document.getElementById('emojiContainer');
        
        let size = 100;
        let noClickCount = 0;

        let noMessages = [
            "¿Segura, vale? 🤨",
            "¿Vale? 🫠",
            "Tengo todo el día 😌",
            "¿Segura, segura? 🤔",
            "Piénsalo bien, vale 🌹",
            "¿A lo bien? 🤨",
            "Yo sé que quieres 🧐",
            "¿Segura? 😑"
        ];

        yesButton.addEventListener('click', () => {
            message.style.display = 'block';
            mainTitle.style.display = 'none';
            document.getElementById('buttonsContainer').style.display = 'none';
            emojiContainer.innerText = '💖☀️🥰';
            emojiContainer.style.fontSize = '120px';
        });

        noButton.addEventListener('click', () => {
            size += 45;
            yesButton.style.width = `${size}px`;
            yesButton.style.height = `${size}px`;
            yesButton.style.fontSize = `${size / 4}px`;
            
            if (noClickCount < noMessages.length) {
                noButton.innerText = noMessages[noClickCount];
                noClickCount++;
            } else {
                noButton.style.display = 'none';
            }
        });
    </script>
</body>
</html>
