<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Roblox Design Shop</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 600px; margin: auto; padding: 20px; }
    canvas { border: 1px solid #ccc; }
    .form-group { margin: 10px 0; }
    button { padding: 10px 20px; cursor: pointer; }
  </style>
</head>
<body>
  <h1>Create Your Roblox Shirt Design</h1>

  <canvas id="shirtCanvas" width="300" height="400"></canvas>
  <div class="form-group">
    <label for="colorPicker">Pick color: </label>
    <input type="color" id="colorPicker" value="#ff0000" />
  </div>
  <div class="form-group">
    <label for="username">Enter your Roblox username:</label><br />
    <input type="text" id="username" placeholder="Roblox username" />
  </div>
  <button id="buyGamepass">Buy Gamepass to Download</button>

  <div id="message" style="margin-top: 20px;"></div>

  <script>
    const canvas = document.getElementById('shirtCanvas');
    const ctx = canvas.getContext('2d');
    const colorPicker = document.getElementById('colorPicker');
    const usernameInput = document.getElementById('username');
    const messageDiv = document.getElementById('message');
    const buyButton = document.getElementById('buyGamepass');

    // Simple "design": fill the shirt canvas with chosen color
    function drawShirt(color) {
      ctx.fillStyle = color;
      ctx.fillRect(50, 100, 200, 200); // simplified shirt rectangle
    }

    colorPicker.addEventListener('input', () => {
      drawShirt(colorPicker.value);
    });

    drawShirt(colorPicker.value);

    buyButton.onclick = () => {
      const username = usernameInput.value.trim();
      if (!username) {
        alert('Please enter your Roblox username.');
        return;
      }

      // Redirect to your Roblox gamepass purchase URL with instructions
      // Replace 'YOUR_GAMEPASS_URL' with actual gamepass URL
      messageDiv.innerHTML = `
        <p>Click the link below to buy the gamepass:</p>
        <a href="https://www.roblox.com/game-pass/YOUR_GAMEPASS_ID" target="_blank" rel="noopener noreferrer">Buy Gamepass</a>
        <p>After purchase, come back here and enter your username again to verify ownership.</p>
        <button id="verifyOwnership">Verify Ownership</button>
      `;

      document.getElementById('verifyOwnership').onclick = async () => {
        messageDiv.textContent = 'Checking ownership...';

        // MOCK: Simulate API call to backend to check ownership
        // Replace with actual call to your backend that checks Roblox gamepass ownership
        await new Promise(r => setTimeout(r, 1500));

        // For demo, always allow
        const ownsGamepass = true;

        if (ownsGamepass) {
          messageDiv.innerHTML = `
            <p>Ownership verified! You can now download your design.</p>
            <a href="#" id="downloadLink" download="shirt-design.png">Download Design</a>
          `;

          // Create downloadable PNG from canvas
          document.getElementById('downloadLink').href = canvas.toDataURL();
        } else {
          messageDiv.textContent = 'Ownership not verified. Please buy the gamepass.';
        }
      };
    };
  </script>
</body>
</html>
