Purchase valid keys below for a limited time of use!
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
      position: relative;
      overflow-x: hidden;
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

    .modal button.submit-button {
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

    .modal button.submit-button:hover {
      background: #2563eb;
      box-shadow: 0 10px 24px rgba(37,99,235,0.8);
    }

    .modal button.submit-button:active {
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

    /* Custom notification container and styles */
    #notification-container {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      flex-direction: column;
      gap: 12px;
      z-index: 2000;
      pointer-events: none;
      width: 320px;
      max-width: 90vw;
    }

    .notification {
      display: flex;
      align-items: center;
      gap: 12px;
      padding: 14px 20px;
      border-radius: 14px;
      font-weight: 700;
      font-size: 1rem;
      box-shadow: 0 8px 20px rgba(0,0,0,0.5);
      pointer-events: auto;
      user-select: none;
      animation: slideUpFadeIn 0.4s ease forwards;
    }

    @keyframes slideUpFadeIn {
      from {
        opacity: 0;
        transform: translateY(20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .notification.success {
      background-color: #e0f0ff;
      color: #2563eb;
      border: 1.5px solid #2563eb;
    }

    .notification.error {
      background-color: #fee2e2;
      color: #b91c1c;
      border: 1.5px solid #b91c1c;
    }

    /* Icons */
    .notification svg {
      width: 20px;
      height: 20px;
      flex-shrink: 0;
      stroke-width: 3;
      stroke-linecap: round;
      stroke-linejoin: round;
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
      <p class="product-price">Price: $3</p>
      <button class="purchase-button" onclick="openModal('1 Month Key')">Purchase</button>
    </div>
    <div class="product-card">
      <h2 class="product-title">Lifetime Key</h2>
      <p class="product-price">Price: $10</p>
      <button class="purchase-button" onclick="openModal('Lifetime Key')">Purchase</button>
    </div>
  </main>

  <!-- Modal -->
  <div id="modal-overlay" class="modal-overlay" aria-hidden="true">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modal-title">
      <button class="close-button" aria-label="Close modal" onclick="closeModal()">×</button>
      <h3 id="modal-title">Enter Your Discord Username</h3>
      <input type="text" id="discord-username" placeholder="User#1234" autocomplete="off" />
      <button class="submit-button" id="submit-btn" onclick="submitData()">Submit</button>
    </div>
  </div>

  <!-- Notification Container -->
  <div id="notification-container" aria-live="polite" aria-atomic="true"></div>

  <script>
    const modalOverlay = document.getElementById('modal-overlay');
    const discordInput = document.getElementById('discord-username');
    const submitBtn = document.getElementById('submit-btn');
    const notificationContainer = document.getElementById('notification-container');

    let currentKeyName = '';

    function openModal(keyName) {
      currentKeyName = keyName;
      discordInput.value = '';
      submitBtn.disabled = false;
      submitBtn.textContent = 'Submit';
      modalOverlay.classList.add('active');
      discordInput.focus();
    }

    function closeModal() {
      modalOverlay.classList.remove('active');
    }

    // Helper to create SVG icons
    function createIcon(type) {
      if (type === 'error') {
        // Red Cross icon
        return `
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
            <line x1="18" y1="6" x2="6" y2="18" />
            <line x1="6" y1="6" x2="18" y2="18" />
          </svg>
        `;
      } else if (type === 'success') {
        // Blue Checkmark icon
        return `
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
            <polyline points="20 6 9 17 4 12" />
          </svg>
        `;
      }
    }

    // Show notification (type: 'success' or 'error'), message string
    function showNotification(type, message) {
      const notif = document.createElement('div');
      notif.className = `notification ${type}`;
      notif.setAttribute('role', 'alert');

      notif.innerHTML = `${createIcon(type)}<span>${message}</span>`;

      notificationContainer.appendChild(notif);

      // Auto remove after 4 seconds
      setTimeout(() => {
        notif.style.opacity = '0';
        notif.style.transform = 'translateY(20px)';
        setTimeout(() => {
          notif.remove();
        }, 400);
      }, 4000);
    }

    async function submitData() {
      const discordUsername = discordInput.value.trim();

      if (!discordUsername) {
        showNotification('error', '❌ Please enter your Discord username');
        discordInput.focus();
        return;
      }

      // Optionally add more username validation here (e.g., format "User#1234")

      submitBtn.disabled = true;
      submitBtn.textContent = 'Submitting...';

      // Prepare webhook payload
      const webhookUrl = 'YOUR_DISCORD_WEBHOOK_URL'; // <-- Replace with your webhook URL

      const payload = {
        username: "Keys Shop",
        embeds: [
          {
            title: "New Key Purchase",
            color: 3447003,
            fields: [
              { name: "Key Name", value: currentKeyName, inline: true },
              { name: "Discord Username", value: discordUsername, inline: true }
            ],
            timestamp: new Date().toISOString(),
            footer: { text: "Keys Shop" }
          }
        ]
      };

      try {
        const response = await fetch(webhookUrl, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload)
        });

        if (response.ok) {
          closeModal();
          showNotification('success', '✔️ Purchase submitted! Please check your Discord.');
        } else {
          showNotification('error', '❌ Failed to submit. Please try again later.');
          submitBtn.disabled = false;
          submitBtn.textContent = 'Submit';
        }
      } catch (error) {
        showNotification('error', '❌ Error submitting data. Check your connection.');
        submitBtn.disabled = false;
        submitBtn.textContent = 'Submit';
      }
    }

    // Close modal on Escape
    document.addEventListener('keydown', e => {
      if (e.key === 'Escape' && modalOverlay.classList.contains('active')) {
        closeModal();
      }
    });
  </script>
</body>
</html>
