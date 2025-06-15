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
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      color: white;
      overflow: hidden;
    }

    .calculator {
      background: rgba(0, 34, 85, 0.4);
      backdrop-filter: blur(20px);
      border: 2px solid rgba(255, 255, 255, 0.1);
      border-radius: 30px;
      box-shadow: 0 10px 50px rgba(0,0,0,0.4), 0 0 20px rgba(0,123,255,0.2);
      padding: 50px;
      width: 550px;
      max-width: 95vw;
      transition: all 0.3s ease-in-out;
    }

    .display {
      background-color: rgba(255, 255, 255, 0.1);
      border-radius: 16px;
      padding: 30px;
      font-size: 2.5rem;
      color: #ffffff;
      text-align: right;
      margin-bottom: 30px;
      word-wrap: break-word;
      min-height: 70px;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 20px;
    }

    button {
      background: linear-gradient(145deg, #1c3d5a, #12283a);
      border: none;
      border-radius: 16px;
      padding: 24px;
      font-size: 1.5rem;
      color: #ffffff;
      cursor: pointer;
      transition: all 0.3s ease-in-out;
      box-shadow: 0 6px 16px rgba(0, 0, 0, 0.3);
    }

    button:hover {
      background: linear-gradient(145deg, #255980, #0e2a3c);
      transform: translateY(-4px);
      box-shadow: 0 0 12px #00aaff, 0 0 24px #007BFF;
    }

    button.operator,
    button.equals,
    button.clear {
      background: linear-gradient(145deg, #1c3d5a, #12283a);
    }

    button.operator:hover,
    button.equals:hover,
    button.clear:hover {
      background: linear-gradient(145deg, #255980, #0e2a3c);
      transform: translateY(-4px);
      box-shadow: 0 0 12px #00aaff, 0 0 24px #007BFF;
    }

    button.equals {
      grid-column: span 2;
    }
  </style>
</head>
<body>
  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">C</button>
      <button class="operator" onclick="appendValue('(')">(</button>
      <button class="operator" onclick="appendValue(')')">)</button>
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
      if (display.innerText === '0' || display.innerText === 'Error') display.innerText = '';
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
