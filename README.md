<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Keys Shop - Discord & Roblox Username Input</title>
  <style>
    /* Your full CSS styles go here — already included above */
    /* ... (unchanged from your input) ... */
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

  <!-- Input Modal -->
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

  <!-- Thank You Modal -->
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
