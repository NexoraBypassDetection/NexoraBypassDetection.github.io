<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Modern Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      padding: 0;
      font-family: 'Inter', sans-serif;
      background: linear-gradient(135deg, #1f1c2c, #928dab);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .calculator {
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(15px);
      border-radius: 20px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.3);
      padding: 30px;
      width: 320px;
    }

    .display {
      background-color: rgba(255, 255, 255, 0.2);
      border-radius: 12px;
      padding: 20px;
      font-size: 2rem;
      color: #fff;
      text-align: right;
      margin-bottom: 20px;
      word-wrap: break-word;
      min-height: 50px;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 15px;
    }

    button {
      background: rgba(255, 255, 255, 0.15);
      border: none;
      border-radius: 12px;
      padding: 20px;
      font-size: 1.2rem;
      color: #fff;
      cursor: pointer;
      transition: all 0.2s ease-in-out;
    }

    button:hover {
      background: rgba(255, 255, 255, 0.25);
      transform: scale(1.05);
    }

    button.operator {
      background-color: #ff6f61;
    }

    button.equals {
      background-color: #28c76f;
      grid-column: span 2;
    }

    button.clear {
      background-color: #ff3f34;
    }
  </style>
</head>
<body>
  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">C</button>
      <button onclick="appendValue('(')">(</button>
      <button onclick="appendValue(')')">)</button>
      <button class="operator" onclick="appendValue('/')">÷</button>
      <button onclick="appendValue('7')">7</button>
      <button onclick="appendValue('8')">8</button>
      <button onclick="appendValue('9')">9</button>
      <button class="operator" onclick="appendValue('*')">×</button>
      <button onclick="appendValue('4')">4</button>
      <button onclick="appendValue('5')">5</button>
      <button onclick="appendValue('6')">6</button>
      <button class="operator" onclick="appendValue('-')">−</button>
      <button onclick="appendValue('1')">1</button>
      <button onclick="appendValue('2')">2</button>
      <button onclick="appendValue('3')">3</button>
      <button class="operator" onclick="appendValue('+')">+</button>
      <button onclick="appendValue('0')">0</button>
      <button onclick="appendValue('.')">.</button>
      <button class="equals" onclick="calculate()">=</button>
    </div>
  </div>

  <script>
    const display = document.getElementById('display');

    function appendValue(val) {
      if (display.innerText === '0') display.innerText = '';
      display.innerText += val;
    }

    function clearDisplay() {
      display.innerText = '0';
    }

    function calculate() {
      try {
        display.innerText = eval(display.innerText.replace(/÷/g, '/').replace(/×/g, '*'));
      } catch {
        display.innerText = 'Error';
      }
    }
  </script>
</body>
</html>
