# Calculator
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
            transition: background-color 0.3s;
        }
        .calculator {
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            width: 300px;
            transition: background-color 0.3s;
        }
        #display {
            width: 100%;
            height: 50px;
            font-size: 24px;
            text-align: right;
            margin-bottom: 10px;
            border: none;
            background-color: #f5f5f5;
            border-radius: 5px;
            padding: 5px;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }
        button {
            padding: 15px;
            font-size: 18px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            opacity: 0.8;
        }
        .number {
            background-color: #e0e0e0;
        }
        .operator {
            background-color: #ff9800;
            color: white;
        }
        #equals {
            background-color: #4caf50;
            color: white;
        }
        #clear {
            background-color: #f44336;
            color: white;
        }
        #theme-toggle {
            position: absolute;
            top: 20px;
            right: 20px;
            padding: 10px;
            background-color: #333;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        #history {
            margin-top: 20px;
            max-height: 100px;
            overflow-y: auto;
        }
        .dark-mode {
            background-color: #333;
            color: white;
        }
        .dark-mode .calculator {
            background-color: #444;
        }
        .dark-mode #display {
            background-color: #555;
            color: white;
        }
        .dark-mode .number {
            background-color: #666;
            color: white;
        }
    </style>
</head>
<body>
    <button id="theme-toggle">Toggle Theme</button>
    <div class="calculator">
        <input type="text" id="display" readonly>
        <div class="buttons">
            <button class="number">7</button>
            <button class="number">8</button>
            <button class="number">9</button>
            <button class="operator">/</button>
            <button class="number">4</button>
            <button class="number">5</button>
            <button class="number">6</button>
            <button class="operator">*</button>
            <button class="number">1</button>
            <button class="number">2</button>
            <button class="number">3</button>
            <button class="operator">-</button>
            <button class="number">0</button>
            <button class="number">.</button>
            <button id="equals">=</button>
            <button class="operator">+</button>
            <button id="clear">C</button>
        </div>
        <div id="history"></div>
    </div>
    <script>
        const display = document.getElementById('display');
        const buttons = document.querySelectorAll('.buttons button');
        const history = document.getElementById('history');
        const themeToggle = document.getElementById('theme-toggle');

        let currentInput = '';
        let currentCalculation = '';

        buttons.forEach(button => {
            button.addEventListener('click', () => {
                const value = button.textContent;
                
                if (value === 'C') {
                    currentInput = '';
                    currentCalculation = '';
                    display.value = '';
                } else if (value === '=') {
                    try {
                        const result = eval(currentCalculation);
                        display.value = result;
                        addToHistory(`${currentCalculation} = ${result}`);
                        currentInput = result;
                        currentCalculation = result;
                    } catch (error) {
                        display.value = 'Error';
                    }
                } else {
                    currentInput += value;
                    currentCalculation += value;
                    display.value = currentInput;
                }
            });
        });

        function addToHistory(calculation) {
            const historyItem = document.createElement('div');
            historyItem.textContent = calculation;
            history.prepend(historyItem);
        }

        themeToggle.addEventListener('click', () => {
            document.body.classList.toggle('dark-mode');
        });
    </script>
</body>
</html>
