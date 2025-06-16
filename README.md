Prob wont work?
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Key Shop</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #1a1a1a;
      color: white;
      margin: 0;
      padding: 0;
    }

    .container {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      padding: 40px;
      justify-content: center;
    }

    .product-card {
      background: #2b2b2b;
      padding: 20px;
      border-radius: 8px;
      text-align: center;
      width: 200px;
      transition: transform 0.3s;
    }

    .product-card:hover {
      transform: scale(1.05);
    }

    .product-title {
      font-size: 18px;
      margin-bottom: 10px;
    }

    .product-price {
      font-size: 16px;
      margin-bottom: 20px;
    }

    .buy-button {
      background: #4caf50;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 4px;
      cursor: pointer;
    }

    .modal,
    .verification-modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.8);
      align-items: center;
      justify-content: center;
    }

    .modal.active,
    .verification-modal.active {
      display: flex;
    }

    .modal-content,
    .verification-content {
      background: #333;
      padding: 30px;
      border-radius: 8px;
      text-align: center;
    }

    .modal input[type="text"] {
      padding: 10px;
      width: 80%;
      margin-bottom: 10px;
      border-radius: 4px;
      border: none;
    }

    .modal label {
      display: block;
      margin-bottom: 10px;
      font-size: 14px;
    }

    .submit-button {
      background: #2196f3;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 4px;
      cursor: pointer;
    }

    .submit-button:disabled {
      background: #888;
      cursor: not-allowed;
    }

    .ok-button {
      background: #4caf50;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 4px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="product-card">
      <div class="product-title">Product A</div>
      <div class="product-price">$10</div>
      <button class="buy-button" onclick="openModal('Product A')">Buy</button>
    </div>
    <div class="product-card">
      <div class="product-title">Product B</div>
      <div class="product-price">$20</div>
      <button class="buy-button" onclick="openModal('Product B')">Buy</button>
    </div>
    <div class="product-card">
      <div class="product-title">Product C</div>
      <div class="product-price">$30</div>
      <button class="buy-button" onclick="openModal('Product C')">Buy</button>
    </div>
  </div>

  <!-- Modal -->
  <div class="modal" id="modal">
    <div class="modal-content">
      <h2>Enter Discord Username</h2>
      <input type="text" id="discordUsername" placeholder="example#0000" />
      <label>
        <input type="checkbox" id="confirmCheckbox" />
        I confirm my username is correct.
      </label>
      <button class="submit-button" id="submitButton" disabled>Submit</button>
    </div>
  </div>

  <!-- Verification Modal -->
  <div class="verification-modal" id="verificationModal">
    <div class="verification-content">
      <h2>Submitted!</h2>
      <p>We’ve received your request. You’ll be contacted shortly.</p>
      <button class="ok-button" id="okButton">OK</button>
    </div>
  </div>

  <script>
    let selectedProduct = null;

    const modal = document.getElementById('modal');
    const verificationModal = document.getElementById('verificationModal');
    const discordUsernameInput = document.getElementById('discordUsername');
    const confirmCheckbox = document.getElementById('confirmCheckbox');
    const submitButton = document.getElementById('submitButton');
    const okButton = document.getElementById('okButton');

    function openModal(productName) {
      selectedProduct = productName;
      modal.classList.add('active');
      verificationModal.classList.remove('active');
      discordUsernameInput.value = '';
      confirmCheckbox.checked = false;
      submitButton.disabled = true;
      discordUsernameInput.focus();
    }

    function closeModal() {
      modal.classList.remove('active');
    }

    function validateForm() {
      submitButton.disabled = !(confirmCheckbox.checked && discordUsernameInput.value.trim() !== '');
    }

    confirmCheckbox.addEventListener('change', validateForm);
    discordUsernameInput.addEventListener('input', validateForm);

    submitButton.addEventListener('click', () => {
      if (discordUsernameInput.value.trim() === '') return;

      const webhookUrl = 'https://your-webhook-url.com'; // 🔗 Replace with your webhook

      const payload = {
        username: 'Key Shop Logger',
        embeds: [{
          title: 'New Purchase Request',
          color: 5814783,
          fields: [
            { name: 'Product', value: selectedProduct, inline: true },
            { name: 'Discord Username', value: discordUsernameInput.value.trim(), inline: true }
          ],
          timestamp: new Date().toISOString()
        }]
      };

      fetch(webhookUrl, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
      }).catch(console.error);

      closeModal();
      showVerification();
    });

    function showVerification() {
      verificationModal.classList.add('active');
    }

    okButton.addEventListener('click', () => {
      verificationModal.classList.remove('active');
    });

    window.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') {
        if (modal.classList.contains('active')) closeModal();
        if (verificationModal.classList.contains('active')) verificationModal.classList.remove('active');
      }
    });
  </script>
</body>
</html>
