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
      max-width: 700px;
      width: 100%;
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(260px,1fr));
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

    .purchase-button, .add-cart-button {
      background: #3b82f6;
      border: none;
      border-radius: 14px;
      padding: 12px 0;
      color: white;
      font-weight: 700;
      font-size: 1.1rem;
      cursor: pointer;
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
      box-shadow: 0 6px 12px rgba(59,130,246,0.5);
      user-select: none;
      margin-top: auto;
    }

    .purchase-button:hover, .add-cart-button:hover {
      background: #2563eb;
      box-shadow: 0 10px 24px rgba(37,99,235,0.7);
    }

    .purchase-button:active, .add-cart-button:active {
      background: #1e40af;
      box-shadow: 0 4px 10px rgba(30,64,175,0.8);
      transform: scale(0.96);
    }

    /* Cart sidebar */
    .cart-sidebar {
      position: fixed;
      top: 40px;
      right: 20px;
      width: 320px;
      max-height: 80vh;
      background: #1e2a47;
      border-radius: 16px;
      box-shadow: 0 12px 30px rgba(20,40,80,0.9);
      padding: 20px 24px;
      color: #cbd5e1;
      display: flex;
      flex-direction: column;
      user-select: none;
      z-index: 1100;
    }

    .cart-sidebar h3 {
      margin-top: 0;
      font-weight: 700;
      font-size: 1.5rem;
      margin-bottom: 16px;
      text-align: center;
    }

    .cart-list {
      flex-grow: 1;
      overflow-y: auto;
      margin-bottom: 16px;
    }

    .cart-item {
      display: flex;
      justify-content: space-between;
      padding: 8px 0;
      border-bottom: 1px solid #2a3b67;
      font-size: 1.1rem;
      color: #94a3b8;
    }

    .cart-item:last-child {
      border-bottom: none;
    }

    .cart-total {
      font-weight: 700;
      font-size: 1.3rem;
      margin-bottom: 16px;
      text-align: right;
      color: #3b82f6;
    }

    .checkout-button {
      background: #22c55e;
      border: none;
      border-radius: 14px;
      padding: 14px 0;
      color: white;
      font-weight: 700;
      font-size: 1.2rem;
      cursor: pointer;
      box-shadow: 0 6px 12px rgba(34,197,94,0.7);
      user-select: none;
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
    }

    .checkout-button:hover {
      background: #16a34a;
      box-shadow: 0 10px 24px rgba(22,163,74,0.8);
    }

    .checkout-button:disabled {
      background: #94a3b8;
      cursor: not-allowed;
      box-shadow: none;
      transform: none;
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
      top: 12px;
      right: 14px;
      background: transparent;
      border: none;
      font-size: 1.6rem;
      color: #94a3b8;
      cursor: pointer;
      user-select: none;
      transition: color 0.3s ease;
    }
    .modal .close-button:hover {
      color: #cbd5e1;
    }

    /* Scrollbar for cart */
    .cart-list::-webkit-scrollbar {
      width: 6px;
    }
    .cart-list::-webkit-scrollbar-thumb {
      background: #3b82f6;
      border-radius: 10px;
    }
  </style>
</head>
<body>
  <main class="shop-container" id="shopContainer">
    <div class="product-card" data-key="discord_key_1" data-price="15">
      <h2 class="product-title">Discord Nitro Key</h2>
      <p class="product-price">$15</p>
      <button class="add-cart-button">Add to Cart</button>
    </div>
    <div class="product-card" data-key="roblox_key_1" data-price="10">
      <h2 class="product-title">Roblox Premium Key</h2>
      <p class="product-price">$10</p>
      <button class="add-cart-button">Add to Cart</button>
    </div>
    <div class="product-card" data-key="steam_key_1" data-price="20">
      <h2 class="product-title">Steam Gift Card</h2>
      <p class="product-price">$20</p>
      <button class="add-cart-button">Add to Cart</button>
    </div>
  </main>

  <!-- Cart Sidebar -->
  <aside class="cart-sidebar" id="cartSidebar" aria-label="Shopping Cart">
    <h3>Your Cart</h3>
    <div class="cart-list" id="cartList">
      <p style="color:#718096;text-align:center;">Your cart is empty.</p>
    </div>
    <div class="cart-total" id="cartTotal">$0</div>
    <button id="checkoutButton" class="checkout-button" disabled>Checkout</button>
  </aside>

  <!-- Modal Overlay & Content -->
  <div class="modal-overlay" id="modalOverlay" role="dialog" aria-modal="true" aria-labelledby="modalTitle" aria-describedby="modalDesc">
    <div class="modal" role="document">
      <button class="close-button" id="modalClose" aria-label="Close">&times;</button>
      <h3 id="modalTitle">Enter Your Details</h3>
      <p id="modalDesc">Please enter your Discord and Roblox usernames below.</p>
      <input type="text" id="discordInput" placeholder="Discord username (e.g. User#1234)" autocomplete="off" />
      <input type="text" id="robloxInput" placeholder="Roblox username" autocomplete="off" />
      <button class="submit-button" id="submitPurchase">Submit Purchase</button>
    </div>
  </div>

  <!-- Success Modal -->
  <div class="modal-overlay" id="successOverlay" role="alertdialog" aria-modal="true" aria-labelledby="successTitle">
    <div class="modal" role="document">
      <button class="close-button" id="successClose" aria-label="Close">&times;</button>
      <h3 id="successTitle">Purchase Successful!</h3>
      <p>Thank you for your purchase. Your keys will be delivered soon.</p>
      <button class="ok-button" id="successOk">OK</button>
    </div>
  </div>

  <script>
    (() => {
      // DOM Elements
      const addCartButtons = document.querySelectorAll('.add-cart-button');
      const cartList = document.getElementById('cartList');
      const cartTotal = document.getElementById('cartTotal');
      const checkoutButton = document.getElementById('checkoutButton');
      const modalOverlay = document.getElementById('modalOverlay');
      const modalClose = document.getElementById('modalClose');
      const discordInput = document.getElementById('discordInput');
      const robloxInput = document.getElementById('robloxInput');
      const submitPurchase = document.getElementById('submitPurchase');
      const successOverlay = document.getElementById('successOverlay');
      const successClose = document.getElementById('successClose');
      const successOk = document.getElementById('successOk');

      // Webhook URL (replace with your actual webhook)
      const webhookURL = 'https://discord.com/api/webhooks/yourwebhookurl';

      // Cart data: Array of objects { key, title, price, quantity }
      let cart = [];

      // Format price display helper
      function formatPrice(value) {
        return `$${value.toFixed(2)}`;
      }

      // Update Cart UI
      function updateCartUI() {
        if (cart.length === 0) {
          cartList.innerHTML = `<p style="color:#718096;text-align:center;">Your cart is empty.</p>`;
          cartTotal.textContent = formatPrice(0);
          checkoutButton.disabled = true;
          return;
        }

        let total = 0;
        cartList.innerHTML = '';

        cart.forEach(item => {
          const itemTotal = item.price * item.quantity;
          total += itemTotal;

          const itemElem = document.createElement('div');
          itemElem.classList.add('cart-item');
          itemElem.innerHTML = `
            <span>${item.title} x${item.quantity}</span>
            <span>${formatPrice(itemTotal)}</span>
          `;

          cartList.appendChild(itemElem);
        });

        cartTotal.textContent = formatPrice(total);
        checkoutButton.disabled = false;
      }

      // Add item to cart
      function addToCart(key, title, price) {
        const existingItem = cart.find(item => item.key === key);
        if (existingItem) {
          existingItem.quantity++;
        } else {
          cart.push({ key, title, price, quantity: 1 });
        }
        updateCartUI();
      }

      // Open modal for user details input
      function openModal() {
        modalOverlay.classList.add('active');
        discordInput.value = '';
        robloxInput.value = '';
        submitPurchase.disabled = false;
        discordInput.focus();
      }

      // Close modal
      function closeModal() {
        modalOverlay.classList.remove('active');
      }

      // Open success modal
      function openSuccessModal() {
        successOverlay.classList.add('active');
      }

      // Close success modal
      function closeSuccessModal() {
        successOverlay.classList.remove('active');
      }

      // Validate Discord username format: username#1234
      function isValidDiscordUsername(username) {
        return /^.{2,32}#[0-9]{4}$/.test(username);
      }

      // Validate Roblox username format (simple check)
      function isValidRobloxUsername(username) {
        return /^[a-zA-Z0-9_]{3,20}$/.test(username);
      }

      // Send purchase info to Discord webhook
      async function sendWebhook(payload) {
        try {
          const response = await fetch(webhookURL, {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body: JSON.stringify(payload),
          });
          return response.ok;
        } catch (error) {
          console.error('Webhook send error:', error);
          return false;
        }
      }

      // Handle purchase submission
      submitPurchase.addEventListener('click', async () => {
        const discordUsername = discordInput.value.trim();
        const robloxUsername = robloxInput.value.trim();

        if (!isValidDiscordUsername(discordUsername)) {
          alert('Discord username must be in the format username#1234');
          discordInput.focus();
          return;
        }
        if (!isValidRobloxUsername(robloxUsername)) {
          alert('Roblox username is invalid. Use 3-20 characters, letters, numbers, or underscores only.');
          robloxInput.focus();
          return;
        }
        if (cart.length === 0) {
          alert('Your cart is empty.');
          return;
        }

        submitPurchase.disabled = true;

        // Build description for Discord embed from cart items
        const cartDescription = cart.map(item => `**${item.title}** x${item.quantity} — $${(item.price * item.quantity).toFixed(2)}`).join('\n');

        const payload = {
          username: 'Key Shop Bot',
          embeds: [
            {
              title: 'New Purchase',
              color: 0x3b82f6,
              fields: [
                {
                  name: 'Discord Username',
                  value: discordUsername,
                  inline: true,
                },
                {
                  name: 'Roblox Username',
                  value: robloxUsername,
                  inline: true,
                },
                {
                  name: 'Items Purchased',
                  value: cartDescription,
                },
                {
                  name: 'Total Price',
                  value: `$${cart.reduce((sum, item) => sum + item.price * item.quantity, 0).toFixed(2)}`,
                },
              ],
              timestamp: new Date().toISOString(),
            },
          ],
        };

        const success = await sendWebhook(payload);

        if (success) {
          closeModal();
          openSuccessModal();
          cart = [];
          updateCartUI();
        } else {
          alert('Failed to send purchase info. Please try again later.');
          submitPurchase.disabled = false;
        }
      });

      // Close modal events
      modalClose.addEventListener('click', closeModal);
      successClose.addEventListener('click', closeSuccessModal);
      successOk.addEventListener('click', closeSuccessModal);

      // Close modals on overlay click (optional)
      modalOverlay.addEventListener('click', (e) => {
        if (e.target === modalOverlay) closeModal();
      });
      successOverlay.addEventListener('click', (e) => {
        if (e.target === successOverlay) closeSuccessModal();
      });

      // Add to cart buttons
      addCartButtons.forEach(button => {
        button.addEventListener('click', () => {
          const card = button.closest('.product-card');
          const key = card.dataset.key;
          const price = parseFloat(card.dataset.price);
          const title = card.querySelector('.product-title').textContent;
          addToCart(key, title, price);
        });
      });

      // Checkout button opens modal
      checkoutButton.addEventListener('click', () => {
        openModal();
      });

      // Initialize cart UI on page load
      updateCartUI();
    })();
  </script>
</body>
</html>
