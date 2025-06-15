<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Keys Shop</title>
<style>
  /* Base & reset */
  * {
    box-sizing: border-box;
  }
  body {
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #0a192f;
    color: #cbd5e1;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    min-height: 100vh;
    padding: 40px 20px;
  }

  h1 {
    width: 100%;
    text-align: center;
    color: #3b82f6;
    margin-bottom: 40px;
    user-select: none;
  }

  /* Shop container */
  .shop-container {
    display: flex;
    gap: 25px;
    max-width: 900px;
    width: 100%;
    flex-wrap: wrap;
    justify-content: center;
  }

  /* Product card */
  .product-card {
    background: #112240;
    border-radius: 14px;
    padding: 20px;
    width: 260px;
    box-shadow: 0 8px 20px rgba(59, 130, 246, 0.25);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    user-select: none;
    transition: transform 0.25s ease, box-shadow 0.25s ease;
  }
  .product-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 14px 32px rgba(59, 130, 246, 0.45);
  }

  .product-name {
    font-size: 1.3rem;
    font-weight: 700;
    margin-bottom: 12px;
    color: #7aa2f7;
  }

  .product-price {
    font-size: 1.1rem;
    margin-bottom: 22px;
    color: #a3bffa;
  }

  .purchase-btn {
    background: #3b82f6;
    border: none;
    border-radius: 12px;
    color: white;
    padding: 14px 0;
    font-size: 1.05rem;
    cursor: pointer;
    box-shadow: 0 6px 18px rgba(59, 130, 246, 0.7);
    transition: background-color 0.3s ease;
    user-select: none;
  }
  .purchase-btn:disabled {
    background: #2563eb88;
    cursor: not-allowed;
    box-shadow: none;
  }
  .purchase-btn:hover:not(:disabled) {
    background: #2563eb;
  }

  /* Modal base */
  .modal {
    position: fixed;
    inset: 0;
    background: rgba(10, 25, 47, 0.85);
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s ease;
    z-index: 999;
  }
  .modal.active {
    opacity: 1;
    pointer-events: all;
  }

  /* Modal content */
  .modal-content {
    background: #112240;
    border-radius: 16px;
    padding: 32px 28px;
    width: 340px;
    box-shadow: 0 18px 48px rgba(59, 130, 246, 0.45);
    text-align: center;
    color: #cbd5e1;
    user-select: none;
    display: flex;
    flex-direction: column;
    gap: 22px;
  }

  .modal-content h2 {
    color: #7aa2f7;
    margin: 0 0 8px 0;
    font-weight: 700;
  }

  .modal-content label {
    font-size: 0.9rem;
    text-align: left;
    color: #90a4ae;
    margin-bottom: 6px;
    user-select: text;
  }

  .modal-content input {
    padding: 11px 14px;
    border-radius: 12px;
    border: none;
    font-size: 1rem;
    outline: none;
    width: 100%;
    color: #0a192f;
    font-weight: 600;
  }
  .modal-content input::placeholder {
    color: #7b8a9e;
  }

  /* Modal button */
  .modal-button {
    background: #3b82f6;
    border: none;
    padding: 14px 0;
    border-radius: 14px;
    font-size: 1.05rem;
    color: white;
    cursor: pointer;
    box-shadow: 0 8px 24px rgba(59, 130, 246, 0.75);
    user-select: none;
    transition: background-color 0.3s ease;
  }
  .modal-button:hover {
    background: #2563eb;
  }
  .modal-button:disabled {
    background: #2563eb88;
    cursor: not-allowed;
    box-shadow: none;
  }
</style>
</head>
<body>

  <h1>Keys Shop</h1>
  <div class="shop-container">
    <div class="product-card">
      <div class="product-name">1 Week Key</div>
      <div class="product-price">Price: $1</div>
      <button class="purchase-btn" onclick="openModal('1 Week Key')">Purchase</button>
    </div>
    <div class="product-card">
      <div class="product-name">1 Month Key</div>
      <div class="product-price">Price: $5</div>
      <button class="purchase-btn" onclick="openModal('1 Month Key')">Purchase</button>
    </div>
    <div class="product-card">
      <div class="product-name">1 Year Key</div>
      <div class="product-price">Price: $50</div>
      <button class="purchase-btn" onclick="openModal('1 Year Key')">Purchase</button>
    </div>
  </div>

  <!-- Purchase Modal -->
  <div class="modal" id="modal" role="dialog" aria-modal="true" aria-labelledby="purchaseTitle">
    <div class="modal-content">
      <h2 id="purchaseTitle">Input Your Info</h2>
      <label for="discordUsername">Discord Username</label>
      <input id="discordUsername" type="text" placeholder="e.g. User#1234" autocomplete="off" />
      <label for="robloxUsername">Roblox Username</label>
      <input id="robloxUsername" type="text" placeholder="e.g. RobloxUser" autocomplete="off" />
      <button id="submitBtn" class="modal-button" onclick="submitPurchase()">Submit</button>
    </div>
  </div>

  <!-- Verification Modal -->
  <div class="modal" id="verificationModal" role="dialog" aria-modal="true" aria-labelledby="verificationTitle" aria-describedby="verificationDesc">
    <div class="modal-content">
      <h2 id="verificationTitle">Thank You!</h2>
      <p id="verificationDesc">Thanks, we will contact you as soon as possible!</p>
      <button class="modal-button" onclick="closeVerificationModal()">Ok</button>
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

  function getPrice(keyName) {
    switch (keyName) {
      case "1 Week Key": return "$1";
      case "1 Month Key": return "$5";
      case "1 Year Key": return "$50";
      default: return "Unknown";
    }
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

    const webhookUrl = "https://discord.com/api/webhooks/1380632133990875156/uTfUbEfNGjSJIkLgY6p34xaR5S1lMXuHmjdhFKoYAXjTd3GXBvNgPtRU9z2M4RIPjSu6";

    const embed = {
      title: "New Key Purchase",
      color: 0x3b82f6, // Blue color
      fields: [
        { name: "Key Type", value: selectedKey, inline: true },
        { name: "Price", value: getPrice(selectedKey), inline: true },
        { name: "Discord Username", value: discordUsername, inline: false },
        { name: "Roblox Username", value: robloxUsername, inline: false },
      ],
      timestamp: new Date().toISOString(),
      footer: { text: "Keys Shop" }
    };

    const payload = {
      username: "KeyShop Bot",
      embeds: [embed],
    };

    try {
      const response = await fetch(webhookUrl, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload),
      });

      if (response.ok) {
        closeModal();
        openVerificationModal();
      } else {
        alert("Failed to submit your purchase. Please try again later.");
        submitBtn.disabled = false;
        submitBtn.textContent = 'Submit';
      }
    } catch (err) {
      alert("Error submitting purchase: " + err.message);
      submitBtn.disabled = false;
      submitBtn.textContent = 'Submit';
    }
  }

  // Close modal if clicked outside content area
  modal.addEventListener('click', e => {
    if (e.target === modal) {
      closeModal();
    }
  });
  verificationModal.addEventListener('click', e => {
    if (e.target === verificationModal) {
      closeVerificationModal();
    }
  });
</script>

</body>
</html>
