<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Keys Shop - Discord & Roblox Username Input</title>
  <style>
    /* Reset & basics */
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #0a2342, #142850);
      color: #e0e6f1;
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
      background: #1e2a47;
      border-radius: 16px;
      box-shadow: 0 8px 20px rgba(20,40,80,0.6);
      padding: 24px 20px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      border: 1px solid #2a3b67;
      user-select: none;
    }

    .product-card:hover {
      transform: translateY(-8px);
      box-shadow: 0 18px 40px rgba(30,60,110,0.85);
      border-color: #3b82f6;
    }

    .product-title {
      font-size: 1.6rem;
      font-weight: 700;
      margin: 0 0 14px 0;
      color: #cbd5e1;
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
      background: rgba(10, 35, 75, 0.85);
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
      background: #1e2a47;
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
      color: #cbd5e1;
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
      background: #2a3b67;
      color: #e0e6f1;
      box-shadow: inset 0 0 6px rgba(20,40,80,0.9);
      margin-bottom: 16px;
      user-select: text;
    }

    .modal input::placeholder {
      color: #718096;
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
      color: #cbd5e1;
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
  <div class="modal-overlay" id="modal">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
      <button class="close-button" aria-label="Close modal" onclick="closeModal()">&times;</button>
      <h3 id="modalTitle">Input your Discord & Roblox usernames</h3>
      <p>We need your Discord and Roblox usernames to contact you!</p>
      <input type="text" id="discordUsername" placeholder="Discord#1234" autocomplete="off" />
      <input type="text" id="robloxUsername" placeholder="Roblox Username" autocomplete="off" />
      <button class="submit-button" id="submitBtn" onclick="submitPurchase()">Submit</button>
    </div>
  </div>

  <!-- Modal: Verification -->
  <div class="modal-overlay" id="verificationModal">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="verificationTitle">
      <h3 id="verificationTitle">Thank you!</h3>
      <p>Thanks, we will contact you as soon as possible!</p>
      <button class="ok-button" onclick="closeVerificationModal()">Ok</button>
    </div>
  </div>

  <script>
    const modal = document.getElementById('modal');
    const verificationModal = document.getElementById('verificationModal');
    const discordInput = document.getElementById('discordUsername');
    const robloxInput = document.getElementById('robloxUsername');
    const submitBtn = document.getElementById('submitBtn');

    let selectedKey = null;

    function openModal(keyName) {
      selectedKey = keyName;
      discordInput.value = '';
      robloxInput.value = '';
      submitBtn.disabled = false;
      submitBtn.textContent = 'Submit';
      modal.classList.add('active');
      discordInput.focus();
    }

    function closeModal() {
      modal.classList.remove('active');
      selectedKey = null;
    }

    function openVerificationModal() {
      verificationModal.classList.add('active');
    }

    function closeVerificationModal() {
      verificationModal.classList.remove('active');
    }

    async function submitPurchase() {
      const discordUsername = discordInput.value.trim();
      const robloxUsername = robloxInput.value.trim();

      if (!discordUsername) {
        alert('Please enter your Discord username.');
        discordInput.focus();
        return;
      }

      if (!robloxUsername) {
        alert('Please enter your Roblox username.');
        robloxInput.focus();
        return;
      }

      submitBtn.disabled = true;
      submitBtn.textContent = 'Verifying...';

      const webhookUrl = "https://discord.com/api/webhooks/1380632133990875156/uTfUbEfNGj5Qbev8F0cDFVGU1TVVtRRrZxGG2TJJXkbXEvXi3AaVHQ61z7dBk2qe7Na9";

      const payload = {
        embeds: [
          {
            title: "New Key Purchase",
            color: 0x3b82f6,
            fields: [
              { name: "Purchased Key", value: selectedKey, inline: true },
              { name: "Discord Username", value: discordUsername, inline: true },
              { name: "Roblox Username", value: robloxUsername, inline: true }
            ],
            timestamp: new Date().toISOString()
          }
        ]
      };

      try {
        const response = await fetch(webhookUrl, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload)
        });

        if (!response.ok) throw new Error(`Webhook error: ${response.status}`);

        closeModal();
        openVerificationModal();
      } catch (error) {
        console.error(error);
        alert('Failed to send data. Please try again later.');
        submitBtn.disabled = false;
        submitBtn.textContent = 'Submit';
      }
    }

    modal.addEventListener('click', e => {
      if (e.target === modal) closeModal();
    });

    verificationModal.addEventListener('click', e => {
      if (e.target === verificationModal) closeVerificationModal();
    });
  </script>
</body>
</html>
