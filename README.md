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
      position: relative;
    }

    .shop-container {
      max-width: 900px;
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
      max-height: 80vh;
      overflow-y: auto;
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

    /* Cart logo fixed on side */
    #cartLogo {
      position: fixed;
      top: 50%;
      right: 10px;
      transform: translateY(-50%);
      background: #3b82f6;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      cursor: pointer;
      box-shadow: 0 4px 10px rgba(59,130,246,0.6);
      display: flex;
      justify-content: center;
      align-items: center;
      user-select: none;
      z-index: 1100;
      transition: background-color 0.3s ease;
    }
    #cartLogo:hover {
      background: #2563eb;
      box-shadow: 0 6px 14px rgba(37,99,235,0.8);
    }
    #cartLogo svg {
      fill: white;
      width: 24px;
      height: 24px;
    }

    /* Cart modal styles */
    #cartModal {
      position: fixed;
      top: 50%;
      right: 70px;
      transform: translateY(-50%);
      background: #1e2a47;
      border-radius: 16px;
      width: 320px;
      max-height: 80vh;
      box-shadow: 0 12px 30px rgba(20,40,80,0.9);
      z-index: 1050;
      display: none;
      flex-direction: column;
      padding: 20px 24px;
      overflow-y: auto;
      user-select: none;
    }

    #cartModal.active {
      display: flex;
    }

    #cartModal h3 {
      margin: 0 0 16px 0;
      color: #cbd5e1;
      font-weight: 700;
      font-size: 1.4rem;
      text-align: center;
      position: relative;
    }

    #cartCloseBtn {
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
    #cartCloseBtn:hover {
      color: #cbd5e1;
    }

    #cartItems {
      flex-grow: 1;
      overflow-y: auto;
      margin-bottom: 20px;
    }

    .cart-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: #2a3b67;
      border-radius: 12px;
      padding: 10px 14px;
      margin-bottom: 12px;
      color: #cbd5e1;
      font-size: 1rem;
      user-select: text;
    }

    .cart-item-name {
      flex-grow: 1;
    }

    .remove-item-btn {
      background: transparent;
      border: none;
      color: #f87171;
      font-weight: 700;
      font-size: 1.2rem;
      cursor: pointer;
      padding: 0 6px;
      user-select: none;
    }
    .remove-item-btn:hover {
      color: #ef4444;
    }

  </style>
</head>
<body>
  <main class="shop-container">
    <div class="product-card">
      <h2 class="product-title">1 Week Key</h2>
      <p class="product-price">Price: $1</p>
      <button class="purchase-button" onclick="handleProductButton(this, '1 Week Key', 1)">Purchase</button>
    </div>

    <div class="product-card">
      <h2 class="product-title">1 Month Key</h2>
      <p class="product-price">Price: $5</p>
      <button class="purchase-button" onclick="handleProductButton(this, '1 Month Key', 5)">Purchase</button>
    </div>

    <div class="product-card">
      <h2 class="product-title">1 Year Key</h2>
      <p class="product-price">Price: $50</p>
      <button class="purchase-button" onclick="handleProductButton(this, '1 Year Key', 50)">Purchase</button>
    </div>
  </main>

  <!-- Username Input Modal -->
  <div id="usernameModal" class="modal-overlay">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="usernameModalTitle">
      <button class="close-button" aria-label="Close" onclick="closeModal('usernameModal')">×</button>
      <h3 id="usernameModalTitle">Enter Your Username</h3>
      <p>Please enter your Discord or Roblox username to proceed.</p>
      <input type="text" id="usernameInput" placeholder="Discord or Roblox username" />
      <button class="submit-button" id="submitUsernameBtn" disabled>Submit</button>
    </div>
  </div>

  <!-- Cart Logo -->
  <div id="cartLogo" title="Toggle Cart" aria-label="Toggle Cart" role="button" tabindex="0">
    <!-- Shopping Cart SVG Icon -->
    <svg viewBox="0 0 24 24" aria-hidden="true" focusable="false">
      <path d="M7 18c-1.1 0-1.99.9-1.99 2S5.9 22 7 22s2-.9 2-2-.9-2-2-2zm10-2H8.42l-.72-3h9.72l-1.14 3zm-3-9h-6l-1 4h8l-1-4zm3.16 7l.74 3H7.99l.74-3H17.16zM21 6h-2l-3 9H8l-3-9H3V4h3.6l3.59 7.59L14.17 6H21v2z"/>
    </svg>
  </div>

  <!-- Cart Modal -->
  <div id="cartModal" role="dialog" aria-modal="true" aria-labelledby="cartModalTitle" aria-describedby="cartModalDesc">
    <h3 id="cartModalTitle">Your Cart
      <button id="cartCloseBtn" aria-label="Close Cart">×</button>
    </h3>
    <div id="cartItems" aria-live="polite" aria-relevant="additions removals"></div>
    <p id="cartModalDesc" style="color:#94a3b8; font-size:0.9rem; text-align:center;">
      Add products by clicking "Add to Cart" buttons.
    </p>
  </div>

  <script>
    // State variables
    let cartMode = false;
    let cart = [];

    // Cache DOM elements
    const cartLogo = document.getElementById('cartLogo');
    const cartModal = document.getElementById('cartModal');
    const cartCloseBtn = document.getElementById('cartCloseBtn');
    const cartItemsContainer = document.getElementById('cartItems');
    const purchaseButtons = document.querySelectorAll('.purchase-button');

    // Toggle cart mode when clicking the cart logo
    cartLogo.addEventListener('click', () => {
      cartMode = !cartMode;
      updateButtons();
      if (cartMode) {
        openCart();
      } else {
        closeCart();
      }
    });

    // Allow keyboard toggle for accessibility
    cartLogo.addEventListener('keydown', (e) => {
      if (e.key === 'Enter' || e.key === ' ') {
        e.preventDefault();
        cartLogo.click();
      }
    });

    // Close cart modal when clicking close button
    cartCloseBtn.addEventListener('click', () => {
      cartMode = false;
      updateButtons();
      closeCart();
    });

    // Update all buttons based on cart mode
    function updateButtons() {
      purchaseButtons.forEach(btn => {
        if (cartMode) {
          btn.textContent = 'Add to Cart';
          btn.title = 'Add this product to your cart';
        } else {
          btn.textContent = 'Purchase';
          btn.title = 'Purchase this product now';
        }
      });
    }

    // Open the cart modal and render contents
    function openCart() {
      renderCartItems();
      cartModal.classList.add('active');
    }

    // Close the cart modal
    function closeCart() {
      cartModal.classList.remove('active');
    }

    // Render cart items inside the cart modal
    function renderCartItems() {
      cartItemsContainer.innerHTML = '';

      if (cart.length === 0) {
        cartItemsContainer.innerHTML = '<p style="text-align:center; color:#94a3b8;">Your cart is empty.</p>';
        return;
      }

      cart.forEach((item, index) => {
        const itemDiv = document.createElement('div');
        itemDiv.classList.add('cart-item');

        const nameSpan = document.createElement('span');
        nameSpan.classList.add('cart-item-name');
        nameSpan.textContent = `${item.name} - $${item.price}`;

        const removeBtn = document.createElement('button');
        removeBtn.classList.add('remove-item-btn');
        removeBtn.setAttribute('aria-label', `Remove ${item.name} from cart`);
        removeBtn.textContent = '×';

        removeBtn.addEventListener('click', () => {
          removeFromCart(index);
        });

        itemDiv.appendChild(nameSpan);
        itemDiv.appendChild(removeBtn);
        cartItemsContainer.appendChild(itemDiv);
      });
    }

    // Remove item from cart by index and re-render
    function removeFromCart(index) {
      cart.splice(index, 1);
      renderCartItems();
    }

    // Handle product button clicks
    function handleProductButton(button, productName, productPrice) {
      if (cartMode) {
        // Add to cart
        cart.push({ name: productName, price: productPrice });
        alert(`Added "${productName}" to your cart.`);
        renderCartItems();
      } else {
        // Purchase flow: open username modal
        openUsernameModal(productName);
      }
    }

    // Username modal references
    const usernameModal = document.getElementById('usernameModal');
    const usernameInput = document.getElementById('usernameInput');
    const submitUsernameBtn = document.getElementById('submitUsernameBtn');
    let currentProductName = '';

    // Open username modal with product info
    function openUsernameModal(productName) {
      currentProductName = productName;
      usernameInput.value = '';
      submitUsernameBtn.disabled = true;
      usernameModal.classList.add('active');
      usernameInput.focus();
    }

    // Close username modal
    function closeModal(modalId) {
      const modal = document.getElementById(modalId);
      modal.classList.remove('active');
    }

    // Enable submit button if input is not empty
    usernameInput.addEventListener('input', () => {
      submitUsernameBtn.disabled = usernameInput.value.trim() === '';
    });

    // Handle username submit
    submitUsernameBtn.addEventListener('click', () => {
      const username = usernameInput.value.trim();
      if (!username) return;

      alert(`Thank you, ${username}! You purchased "${currentProductName}".`);

      // Here you can add actual purchase processing logic

      closeModal('usernameModal');
    });

    // Close username modal on outside click or ESC
    usernameModal.addEventListener('click', (e) => {
      if (e.target === usernameModal) {
        closeModal('usernameModal');
      }
    });
    window.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') {
        closeModal('usernameModal');
      }
    });
  </script>
</body>
</html>
