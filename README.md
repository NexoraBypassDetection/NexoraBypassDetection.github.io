<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Shop with Verification Modal</title>
<style>
  body {
    font-family: Arial, sans-serif;
    margin: 0; padding: 20px;
    background: #f5f5f5;
  }

  .product-list {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
  }

  .product {
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgb(0 0 0 / 0.1);
    padding: 15px;
    width: 150px;
    text-align: center;
  }

  .purchase-button {
    margin-top: 10px;
    padding: 10px;
    background-color: #22c55e;
    border: none;
    color: white;
    font-weight: bold;
    border-radius: 5px;
    cursor: pointer;
    width: 100%;
    transition: background-color 0.3s ease;
  }
  .purchase-button:hover:not(:disabled) {
    background-color: #16a34a;
  }
  .purchase-button:disabled {
    cursor: not-allowed;
    opacity: 0.6;
  }

  /* Cart Icon */
  #cartLogo {
    position: fixed;
    top: 20px;
    right: 20px;
    background: #22c55e;
    color: white;
    padding: 10px 15px;
    border-radius: 30px;
    font-weight: bold;
    cursor: pointer;
    user-select: none;
    z-index: 10000;
  }
  #cartLogo:focus {
    outline: 2px solid #16a34a;
  }

  /* Cart Modal */
  #cartModal {
    position: fixed;
    top: 70px;
    right: 20px;
    width: 300px;
    max-height: 400px;
    background: white;
    box-shadow: 0 4px 12px rgb(0 0 0 / 0.15);
    border-radius: 10px;
    overflow-y: auto;
    display: none;
    flex-direction: column;
    z-index: 9999;
  }
  #cartModal.active {
    display: flex;
  }
  #cartCloseBtn {
    align-self: flex-end;
    background: none;
    border: none;
    font-size: 20px;
    margin: 10px;
    cursor: pointer;
  }
  #cartItems {
    padding: 10px 20px 20px 20px;
    flex-grow: 1;
  }
  #cartItems p {
    margin: 8px 0;
  }

  /* Username Modal */
  #usernameModal {
    position: fixed;
    inset: 0;
    background: rgb(0 0 0 / 0.5);
    display: none;
    align-items: center;
    justify-content: center;
    z-index: 10001;
  }
  #usernameModal.active {
    display: flex;
  }
  .modal-content {
    background: white;
    border-radius: 10px;
    padding: 25px 30px;
    width: 320px;
    box-shadow: 0 4px 20px rgb(0 0 0 / 0.25);
    text-align: center;
  }
  .modal-content h2 {
    margin-top: 0;
  }
  .modal-content input[type="text"] {
    width: 100%;
    padding: 10px;
    font-size: 1rem;
    margin: 15px 0 20px 0;
    border-radius: 5px;
    border: 1px solid #ccc;
  }
  .modal-content button {
    background-color: #22c55e;
    border: none;
    color: white;
    font-weight: bold;
    padding: 10px 20px;
    border-radius: 6px;
    cursor: pointer;
    width: 100%;
    font-size: 1rem;
  }
  .modal-content button:disabled {
    background-color: #a5d6a7;
    cursor: not-allowed;
  }

  /* Notification */
  #notification {
    position: fixed;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%);
    background-color: #22c55e;
    color: white;
    padding: 12px 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgb(0 0 0 / 0.2);
    font-weight: 600;
    font-family: Arial, sans-serif;
    display: none;
    align-items: center;
    gap: 8px;
    z-index: 10002;
    user-select: none;
    cursor: default;
    animation: slideIn 0.3s ease forwards;
  }
  #notification .notification-icon {
    font-size: 1.3em;
  }
  @keyframes slideIn {
    from {
      opacity: 0;
      transform: translateX(-50%) translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateX(-50%) translateY(0);
    }
  }
</style>
</head>
<body>

<div id="cartLogo" tabindex="0" role="button" aria-label="Toggle Cart">Cart 🛒</div>

<div id="cartModal" role="dialog" aria-modal="true" aria-labelledby="cartTitle">
  <button id="cartCloseBtn" aria-label="Close Cart">&times;</button>
  <h3 id="cartTitle" style="padding: 0 20px;">Your Cart</h3>
  <div id="cartItems"><p>Your cart is empty.</p></div>
</div>

<div class="product-list">
  <div class="product">
    <h4>Item A</h4>
    <p>$10</p>
    <button class="purchase-button" data-name="Item A" data-price="10">Purchase</button>
  </div>
  <div class="product">
    <h4>Item B</h4>
    <p>$25</p>
    <button class="purchase-button" data-name="Item B" data-price="25">Purchase</button>
  </div>
  <div class="product">
    <h4>Item C</h4>
    <p>$50</p>
    <button class="purchase-button" data-name="Item C" data-price="50">Purchase</button>
  </div>
</div>

<!-- Username Verification Modal -->
<div id="usernameModal" role="dialog" aria-modal="true" aria-labelledby="usernameTitle">
  <div class="modal-content">
    <h2 id="usernameTitle">Enter Your Username</h2>
    <input type="text" id="usernameInput" placeholder="Discord or Roblox username" autocomplete="off" />
    <button id="submitUsernameBtn" disabled>Submit</button>
  </div>
</div>

<!-- Notification -->
<div id="notification">
  <span class="notification-icon">✔️</span>
  <span id="notification-text"></span>
</div>

<script>
  let cartMode = false;
  let cart = [];
  let currentPurchase = null;

  const cartLogo = document.getElementById('cartLogo');
  const cartModal = document.getElementById('cartModal');
  const cartCloseBtn = document.getElementById('cartCloseBtn');
  const cartItemsContainer = document.getElementById('cartItems');
  const purchaseButtons = document.querySelectorAll('.purchase-button');
  const usernameModal = document.getElementById('usernameModal');
  const usernameInput = document.getElementById('usernameInput');
  const submitUsernameBtn = document.getElementById('submitUsernameBtn');
  const notification = document.getElementById('notification');
  const notificationText = document.getElementById('notification-text');

  // Toggle cart modal
  cartLogo.addEventListener('click', () => {
    cartMode = !cartMode;
    updateButtons();
    if (cartMode) openCart();
    else closeCart();
  });

  cartLogo.addEventListener('keydown', (e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault();
      cartLogo.click();
    }
  });

  cartCloseBtn.addEventListener('click', () => {
    cartMode = false;
    updateButtons();
    closeCart();
  });

  // Update purchase buttons state
  function updateButtons() {
    const disable = cartMode || usernameModal.classList.contains('active');
    purchaseButtons.forEach(btn => {
      btn.disabled = disable;
      btn.style.cursor = disable ? 'not-allowed' : 'pointer';
      btn.style.opacity = disable ? '0.6' : '1';
    });
  }

  function openCart() {
    cartModal.classList.add('active');
    renderCartItems();
  }

  function closeCart() {
    cartModal.classList.remove('active');
  }

  function renderCartItems() {
    if (cart.length === 0) {
      cartItemsContainer.innerHTML = '<p>Your cart is empty.</p>';
      return;
    }
    cartItemsContainer.innerHTML = '';
    cart.forEach((item, index) => {
      const p = document.createElement('p');
      p.textContent = `${item.productName} - $${item.price}`;
      cartItemsContainer.appendChild(p);
    });
  }

  function openUsernameModal() {
    usernameModal.classList.add('active');
    usernameInput.value = '';
    submitUsernameBtn.disabled = true;
    usernameInput.focus();
    updateButtons();
  }

  function closeUsernameModal() {
    usernameModal.classList.remove('active');
    currentPurchase = null;
    updateButtons();
  }

  usernameInput.addEventListener('input', () => {
    submitUsernameBtn.disabled = usernameInput.value.trim().length === 0;
  });

  submitUsernameBtn.addEventListener('click', () => {
    const username = usernameInput.value.trim();
    if (!username) return;

    // Simulate purchase completion and verification
    addToCart(currentPurchase);
    closeUsernameModal();
    showNotification(`${currentPurchase.productName} was added to your cart! (User: ${username})`);
  });

  // Add product to cart
  function addToCart(product) {
    cart.push(product);
    renderCartItems();
  }

  // Purchase buttons handler
  purchaseButtons.forEach(btn => {
    btn.addEventListener('click', () => {
      if (cartMode || usernameModal.classList.contains('active')) return;
      const productName = btn.getAttribute('data-name');
      const price = btn.getAttribute('data-price');
      currentPurchase = { productName, price };
      openUsernameModal();
    });
  });

  // Notification
  function showNotification(message) {
    notificationText.textContent = message;
    notification.style.display = 'flex';

    clearTimeout(notification.hideTimeout);
    notification.hideTimeout = setTimeout(() => {
      notification.style.display = 'none';
    }, 3000);
  }

  // Close modals on ESC key
  document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') {
      if (usernameModal.classList.contains('active')) closeUsernameModal();
      if (cartModal.classList.contains('active')) {
        cartMode = false;
        updateButtons();
        closeCart();
      }
    }
  });
</script>
</body>
</html>
