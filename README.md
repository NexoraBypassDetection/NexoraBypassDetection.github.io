Wont work 100%
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Keys Shop - Discord Username Input</title>
  <style>
    /* [All your existing CSS – unchanged] */
    /* ... (omitted here for brevity, same as your original) ... */
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
  <div class="modal-overlay" id="verificationModal">
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

    submitButton.addEventListener('click', () => {
      if (discordUsernameInput.value.trim() === '') return;

      const username = discordUsernameInput.value.trim();
      const webhookUrl = "https://discord.com/api/webhooks/YOUR_WEBHOOK_HERE";

      fetch(webhookUrl, {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          embeds: [{
            title: "New Key Purchase Submission",
            color: 5814783,
            fields: [
              { name: "Username", value: username },
              { name: "Product", value: selectedProduct }
            ],
            timestamp: new Date().toISOString()
          }]
        })
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
