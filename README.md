
<html lang="hu">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Szerencsekerék</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
            font-family: Arial, sans-serif;
        }

        #wheel-container {
            position: relative;
            width: 90vmin;
            height: 90vmin;
            max-width: 350px;
            max-height: 350px;
            text-align: center;
        }

        #wheel {
            width: 100%;
            height: 100%;
            transition: transform 4s ease-out;
        }

        #spin-button {
            position: absolute;
            bottom: -60px;
            left: 50%;
            transform: translateX(-50%);
            padding: 12px 24px;
            font-size: 18px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
        }

        #spin-button:hover {
            background-color: #45a049;
        }

        #arrow {
            position: absolute;
            top: 10px;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 0;
            border-left: 20px solid transparent;
            border-right: 20px solid transparent;
            border-bottom: 30px solid red;
        }

        #result {
            position: absolute;
            bottom: -110px;
            width: 100%;
            font-size: 18px;
            color: #333;
            font-weight: bold;
        }

        /* Mobil képernyőre optimalizált stílusok */
        @media (max-width: 768px) {
            body {
                background-color: #e0e0e0;
            }

            #wheel-container {
                width: 80vmin;
                height: 80vmin;
                max-width: 300px;
                max-height: 300px;
            }

            #spin-button {
                padding: 10px 20px;
                font-size: 16px;
            }
        }
    </style>
</head>
<body>
    <div id="wheel-container">
        <div id="arrow"></div>
        <img src="wheel.png" id="wheel" alt="Szerencsekerék">
        <button id="spin-button" onclick="spinWheel()">Pörgetés</button>
        <div id="result"></div>
    </div>

    <script>
        let rotation = 0;

        // Számok és azok esélyei
        const probabilities = [
            { number: 1, chance: 5 },
            { number: 2, chance: 5 },
            { number: 3, chance: 5 },
            { number: 4, chance: 5 },
            { number: 5, chance: 10 },
            { number: 6, chance: 10 },
            { number: 7, chance: 5 },
            { number: 8, chance: 5 },
            { number: 9, chance: 10 },
            { number: 10, chance: 5 },
            { number: 11, chance: 5 },
            { number: 12, chance: 5 },
            { number: 13, chance: 5 },
            { number: 14, chance: 5 },
            { number: 15, chance: 5 },
            { number: 16, chance: 5 },
            { number: 17, chance: 5 },
            { number: 18, chance: 5 },
            { number: 19, chance: 5 },
            { number: 20, chance: 10 },
            { number: 21, chance: 5 },
            { number: 22, chance: 5 },
            { number: 23, chance: 5 },
            { number: 24, chance: 5 },
            { number: 25, chance: 10 }
        ];

        // Kiválaszt egy számot az esélyek alapján
        function getRandomNumber() {
            const totalChance = probabilities.reduce((sum, item) => sum + item.chance, 0);
            let random = Math.random() * totalChance;
            for (let item of probabilities) {
                if (random < item.chance) {
                    return item.number;
                }
                random -= item.chance;
            }
            return probabilities[probabilities.length - 1].number;
        }

        // Pörgetés funkció
        function spinWheel() {
            const randomDegree = Math.floor(Math.random() * 360) + 360 * 4; // Legalább 4 teljes fordulat
            rotation += randomDegree;
            document.getElementById("wheel").style.transform = `rotate(${rotation}deg)`;

            setTimeout(() => {
                const resultNumber = getRandomNumber();
                document.getElementById("result").innerText = `Kipörgetett szám: ${resultNumber}`;
            }, 4000); // Várakozás a forgás befejezéséig
        }
    </script>
</body>
</html>
