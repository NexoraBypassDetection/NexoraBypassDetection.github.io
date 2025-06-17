<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Keys Shop - Discord Username Input</title>
<style>
  /* Your original CSS unchanged here for brevity */
  * {box-sizing: border-box;}
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
</style>
</head>
<body>
<main class="shop-container">
  <div class="product-card">
    <h2 class="product-title">1 Week Key</h2>
    <p class="product-price">Price: $1</p>
    <button class="purchase-button" onclick="window.openModal('1 Week Key')">Purchase</button>
  </div>
  <div class="product-card">
    <h2 class="product-title">1 Month Key</h2>
    <p class="product-price">Price: $5</p>
    <button class="purchase-button" onclick="window.openModal('1 Month Key')">Purchase</button>
  </div>
  <div class="product-card">
    <h2 class="product-title">1 Year Key</h2>
    <p class="product-price">Price: $50</p>
    <button class="purchase-button" onclick="window.openModal('1 Year Key')">Purchase</button>
  </div>
</main>

<script>
(function(){
  // Encoded modal HTML string (base64)
  const modalHTML = atob('PGRpdiBjbGFzcz0ibW9kYWwtb3ZlcmxheSIgaWQ9Im1vZGFsIiBhcmlhLWhpZGRlbj0idHJ1ZSI+CiAgPGRpdiBjbGFzcz0ibW9kYWwiIHJvbGU9ImRpYWxvZyIgYXJpYS1tb2RhbD0idHJ1ZSIgYXJpYS1sYWJlbGxlZD0ibW9kYWxUaXRsZSI+CiAgICA8YnV0dG9uIGNsYXNzPSJjbG9zZS1idXR0b24iIGFyaWEtbGFiZWw9IkNsb3NlIG1vZGFsIiBvbmNsaWNrPSJ3aW5kb3cubG9jYXRpb25IYW5kbGVyKCkiPiZ0aW1lczs8L2J1dHRvbj4KICAgIDxoMyBpZD0ibW9kYWxUaXRsZSI+SW5wdXQgeW91ciBEaXNjb3JkIHVzZXJuYW1lPC9oMz4KICAgIDxwPldlIG5lZWQgeW91ciBEaXNjb3JkIHVzZXJuYW1lIHRvIGNvbnRhY3QgeW91ITwvcD4KICAgIDxpbnB1dCB0eXBlPSJ0ZXh0IiBpZD0iZGlzY29yZFVzZXJuYW1lIiBwbGFjZWhvbGRlcj0iRGlzY29yZCNcMTIzNCIgYXV0b2NvbXBsZXRlPSJvZmYiIC8+CiAgICA8bGFiZWw+CiAgICAgIDxpbnB1dCB0eXBlPSJjaGVja2JveCIgaWQ9ImNvbmZpcm1DaGVja2JveCIgLz4KICAgICAgSSBjb25maXJtIHRoZSBpbmZvcm1hdGlvbiBpcyBjb3JyZWN0LgogICAgPC9sYWJlbD4KCiAgICA8YnV0dG9uIGNsYXNzPSJzdWJtaXQtYnV0dG9uIiBpZD0ic3VibWl0QnV0dG9uIiBkaXNhYmxlZD5TdWJtaXQ8L2J1dHRvbj4KICA8L2Rpdj4KPC9kaXY+Cg==');

  // Insert modal HTML into body
  document.body.insertAdjacentHTML('beforeend', modalHTML);

  // Variables
  let selectedProduct = null;
  const modal = document.getElementById('modal');
  const discordUsernameInput = document.getElementById('discordUsername');
  const confirmCheckbox = document.getElementById('confirmCheckbox');
  const submitButton = document.getElementById('submitButton');

  // Functions
  function openModal(product) {
    selectedProduct = product;
    modal.style.display = 'flex';
    discordUsernameInput.value = '';
    confirmCheckbox.checked = false;
    submitButton.disabled = true;
    discordUsernameInput.focus();
  }
  function closeModal() {
    modal.style.display = 'none';
  }
  function validateForm() {
    submitButton.disabled = !(confirmCheckbox.checked && discordUsernameInput.value.trim() !== '');
  }
  // Event listeners
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
    alert('Thanks, we will contact you as soon as possible!');
  });

  // Export openModal globally so buttons can use it
  window.openModal = openModal;
  window.closeModal = closeModal;
})();
</script>

</body>
</html>
