<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Key Shop with PayPal.me Links</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: #222;
    color: #eee;
    text-align: center;
    padding: 2rem;
  }
  .key-card {
    background: #333;
    border-radius: 10px;
    margin: 1rem auto;
    padding: 1.5rem;
    width: 300px;
  }
  button.purchase-button {
    background: #ff9900;
    border: none;
    color: #222;
    padding: 10px 20px;
    margin-top: 1rem;
    cursor: pointer;
    border-radius: 5px;
    font-weight: bold;
  }
  #modal {
    display: none;
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(0,0,0,0.8);
    justify-content: center;
    align-items: center;
  }
  #modal.active {
    display: flex;
  }
  #modal-content {
    background: #444;
    padding: 2rem;
    border-radius: 10px;
    width: 350px;
    text-align: left;
  }
  #modal-content label,
  #modal-content input {
    display: block;
    width: 100%;
    margin-bottom: 1rem;
  }
  #modal-content input {
    padding: 8px;
    border-radius: 5px;
    border: none;
    font-size: 1rem;
  }
  #modal-close {
    float: right;
    cursor: pointer;
    color: #f00;
    font-weight: bold;
  }
  #paypal-link {
    display: inline-block;
    background: #0070ba;
    color: white;
    padding: 10px 15px;
    border-radius: 6px;
    text-decoration: none;
    margin-bottom: 1rem;
    font-weight: bold;
  }
  #submit-username {
    background: #28a745;
    border: none;
    color: white;
    padding: 10px 0;
    width: 100%;
    cursor: pointer;
    border-radius: 5px;
    font-weight: bold;
  }
  #submit-username:disabled {
    background: #555;
    cursor: not-allowed;
  }
  #message {
    margin-top: 1rem;
    font-weight: bold;
  }
</style>
</head>
<body>

<h1>Key Shop</h1>

<div class="key-card">
  <h2>1 Week Key</h2>
  <p>Price: $1.00</p>
  <button class="purchase-button" data-key="1 Week Key">Purchase</button>
</div>

<div class="key-card">
  <h2>1 Month Key</h2>
  <p>Price: $5.00</p>
  <button class="purchase-button" data-key="1 Month Key">Purchase</button>
</div>

<div class="key-card">
  <h2>1 Year Key</h2>
  <p>Price: $50.00</p>
  <button class="purchase-button" data-key="1 Year Key">Purchase</button>
</div>

<!-- Modal for Discord username & PayPal -->
<div id="modal">
  <div id="modal-content">
    <span id="modal-close">&times;</span>
    <h2 id="modal-title">Purchase</h2>
    <a href="#" target="_blank" id="paypal-link">Pay with PayPal</a>
    <label for="discord-username">Enter your Discord username (with #):</label>
    <input type="text" id="discord-username" placeholder="Example: User#1234" />
    <button id="submit-username" disabled>Submit</button>
    <div id="message"></div>
  </div>
</div>

<script>
  const webhookUrl = "YOUR_DISCORD_WEBHOOK_URL";

  let selectedKey = null;
  let paypalUrl = null;

  const modal = document.getElementById("modal");
  const modalTitle = document.getElementById("modal-title");
  const discordInput = document.getElementById("discord-username");
  const submitBtn = document.getElementById("submit-username");
  const messageDiv = document.getElementById("message");
  const paypalLink = document.getElementById("paypal-link");
  const modalClose = document.getElementById("modal-close");

  // Map keys to PayPal.me URLs
  function getPaypalUrl(key) {
    let url = "";
    switch (key) {
      case "1 Week Key":
        url = "https://www.paypal.com/paypalme/kevsterlive/1"; // Replace yourusername and amount
        break;
      case "1 Month Key":
        url = "https://www.paypal.com/paypalme/kevsterlive/5";
        break;
      case "1 Year Key":
        url = "https://www.paypal.com/paypalme/kevsterlive/50";
        break;
      default:
        url = "https://www.paypal.com/paypalme/kevsterlive/1";
    }
    return url;
  }

  // Open modal when purchase button clicked
  document.querySelectorAll(".purchase-button").forEach(btn => {
    btn.addEventListener("click", () => {
      selectedKey = btn.dataset.key;
      paypalUrl = getPaypalUrl(selectedKey);

      modalTitle.textContent = `Purchase ${selectedKey}`;
      discordInput.value = "";
      messageDiv.textContent = "";
      submitBtn.disabled = true;

      paypalLink.href = paypalUrl;

      modal.classList.add("active");
    });
  });

  // Close modal
  modalClose.addEventListener("click", () => {
    modal.classList.remove("active");
  });

  // Enable submit button only if input has value
  discordInput.addEventListener("input", () => {
    submitBtn.disabled = discordInput.value.trim().length === 0;
  });

  // Submit Discord username and key info to webhook
  submitBtn.addEventListener("click", () => {
    const discordUsername = discordInput.value.trim();

    if (!discordUsername) {
      alert("Please enter your Discord username.");
      return;
    }

    // Send data to Discord webhook
    fetch(webhookUrl, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        content: null,
        embeds: [{
          title: "New Key Purchase",
          color: 0x00ff00,
          fields: [
            { name: "Key Type", value: selectedKey, inline: true },
            { name: "Discord Username", value: discordUsername, inline: true },
            { name: "PayPal Link", value: paypalUrl, inline: false }
          ],
          timestamp: new Date().toISOString()
        }]
      })
    })
    .then(response => {
      if (response.ok) {
        messageDiv.style.color = "lightgreen";
        messageDiv.textContent = "Thank you! Your information was sent successfully.";
        submitBtn.disabled = true;
      } else {
        throw new Error("Failed to send data");
      }
    })
    .catch(error => {
      messageDiv.style.color = "red";
      messageDiv.textContent = "Error sending information. Please try again.";
      console.error(error);
    });
  });
</script>

</body>
</html>
