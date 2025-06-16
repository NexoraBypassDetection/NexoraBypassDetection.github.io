Purchase valid keys for an limited time period of use below!
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Keys Shop - Discord Username Input</title>
  <style>
    /* Reset & basics */
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #050d1a, #0b1224);
      color: #dce3f0;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
      padding: 40px 20px;
    }

    .shop-container {
      max-width: 900px;
      width: 100%;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 30px;
    }

    .product-card {
      background: #111827;
      border-radius: 16px;
      box-shadow: 0 8px 20px rgba(10, 20, 40, 0.7);
      padding: 24px 20px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      border: 1px solid #1f2937;
      user-select: none;
    }

    .product-card:hover {
      transform: translateY(-8px);
      box-shadow: 0 18px 40px rgba(37, 99, 235, 0.4);
      border-color: #3b82f6;
    }

    .product-title {
      font-size: 1.6rem;
      font-weight: 700;
      margin: 0 0 14px 0;
      color: #e2e8f0;
    }

    .product-price {
      font-size: 1.2rem;
      margin-bottom: 28px;
      color: #94a3b8;
    }

    .purchase-button {
      background: #3b82f6;
      border: none;
      border-radius: 14px;
      padding: 16px 0;
      color: white;
      font-weight: 700;
      font-size: 1.1rem;
      cursor: pointer;
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
      box-shadow: 0 6px 12px rgba(59,130,246,0.5);
      user-select: none;
    }

    .purchase-button:hover {
      background: #2563eb;
      box-shadow: 0 10px 24px rgba(37,99,235,0.7);
    }

    .purchase-button:active {
      background: #1e40af;
      box-shadow: 0 4px 10px rgba(30,64,175,0.8);
      transform: scale(0.96);
    }

    /* Modal styles */
    .modal-overlay {
      position: fixed;
      inset: 0;
      background: rgba(5, 12, 25, 0.88);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 1000;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.3s ease;
    }

    .modal-overlay.active {
      opacity: 1;
      pointer-events: auto;
    }

    .modal {
      background: #111827;
      border-radius: 16px;
      padding: 30px 28px;
      width: 320px;
      box-shadow: 0 12px 30px rgba(20,40,80,0.9);
      display: flex;
      flex-direction: column;
      user-select: none;
      position: relative;
    }

    .modal h3 {
      color: #e2e8f0;
      margin: 0 0 16px 0;
      font-weight: 700;
      font-size: 1.5rem;
      text-align: center;
    }

    .modal p {
      color: #94a3b8;
      font-size: 0.9rem;
      margin: 0 0 24px 0;
      text-align: center;
    }

    .modal input[type="text"] {
      padding: 12px 14px;
      border-radius: 12px;
      border: none;
      font-size: 1rem;
      outline: none;
      background: #1f2937;
      color: #e2e8f0;
      box-shadow: inset 0 0 6px rgba(20,40,80,0.8);
      margin-bottom: 16px;
      user-select: text;
    }

    .modal input::placeholder {
      color: #6b7280;
    }

    .modal label {
      display: flex;
      align-items: center;
      gap: 8px;
      color: #94a3b8;
      font-size: 0.9rem;
      margin-bottom: 20px;
      user-select: none;
    }

    .modal input[type="checkbox"] {
      width: 18px;
      height: 18px;
      cursor: pointer;
    }

    .modal button.submit-button,
    .modal button.ok-button {
      background: #3b82f6;
      border: none;
      border-radius: 14px;
      padding: 14px 0;
      color: white;
      font-weight: 700;
      font-size: 1.1rem;
      cursor: pointer;
      box-shadow: 0 6px 12px rgba(59,130,246,0.6);
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
      user-select: none;
    }

    .modal button.submit-button:hover,
    .modal button.ok-button:hover {
      background: #2563eb;
      box-shadow: 0 10px 24px rgba(37,99,235,0.8);
    }

    .modal button.submit-button:active,
    .modal button.ok-button:active {
      background: #1e40af;
      box-shadow: 0 4px 10px rgba(30,64,175,0.9);
      transform: scale(0.96);
    }

    .modal button.submit-button:disabled {
      background: #94a3b8;
      cursor: not-allowed;
      box-shadow: none;
      transform: none;
    }

    .modal .close-button {
      position: absolute;
      top: 14px;
      right: 14px;
      background: transparent;
      border: none;
      font-size: 1.5rem;
      color: #94a3b8;
      cursor: pointer;
      user-select: none;
      transition: color 0.2s ease;
    }

    .modal .close-button:hover {
      color: #e2e8f0;
    }
  </style>
</head>
<body>
  <main class="shop-container">
    <div class="product-card">
      <h2 class="product-title">1 Week Key</h2>
      <p class="product-price">Price: $1</p>
      <button class="purchase-button" onclick="openModal('1 Week Key')">Purchase</button>
    </div>
    <div class="product-card">
      <h2 class="product-title">1 Month Key</h2>
      <p class="product-price">Price: $5</p>
      <button class="purchase-button" onclick="openModal('1 Month Key')">Purchase</button>
    </div>
    <div class="product-card">
      <h2 class="product-title">1 Year Key</h2>
      <p class="product-price">Price: $50</p>
      <button class="purchase-button" onclick="openModal('1 Year Key')">Purchase</button>
    </div>
  </main>

  <!-- Modal: Input form -->
  <div class="modal-overlay" id="modal" aria-hidden="true">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
      <button class="close-button" aria-label="Close modal" onclick="closeModal()">&times;</button>
      <h3 id="modalTitle">Input your Discord username</h3>
      <p>We need your Discord username to contact you!</p>
      <input type="text" id="discordUsername" placeholder="Discord#1234" autocomplete="off" />
      
      <label>
        <input type="checkbox" id="confirmCheckbox" />
        I confirm the information is correct.
      </label>

      <button class="submit-button" id="submitButton" disabled>Submit</button>
    </div>
  </div>

  <!-- Modal: Verification -->
  <div class="modal-overlay" id="verificationModal" aria-hidden="true">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="verificationTitle">
      <h3 id="verificationTitle">Thank you!</h3>
      <p>Thanks, we will contact you as soon as possible!</p>
      <button class="ok-button" id="okButton">Ok</button>
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

    submitButton.addEventListener('click', async () => {
      const username = discordUsernameInput.value.trim();
      if (!username) return;

      const webhookUrl = 'https://discord.com/api/webhooks/1384168262199410690/Mf56mxY1uHTQBBNuUghceqLC-qQpDLNjIzrT4isDtqKpSwPi6Xevmsh1hpdpJ-pWwG-X';

      const payload = {
        username: "Key Shop Bot",
        embeds: [{
          title: "New Key Purchase",
          color: 0x3b82f6,
          fields: [
            { name: "Discord Username", value: username, inline: true },
            { name: "Product", value: selectedProduct || "Unknown", inline: true }
          ],
          timestamp: new Date().toISOString()
        }]
      };

      try {
        await fetch(webhookUrl, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(payload)
        });
      } catch (err) {
        console.error("Webhook Error:", err);
      }

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
