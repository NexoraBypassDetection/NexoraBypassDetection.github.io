<!-- Add this PayPal SDK script in your <head> or before </body> -->
<script src="https://www.paypal.com/sdk/js?client-id=YOUR_PAYPAL_CLIENT_ID&currency=USD"></script>

<script>
  const modal = document.getElementById('modal');
  const verificationModal = document.getElementById('verificationModal');
  const discordInput = document.getElementById('discordUsername');
  const robloxInput = document.getElementById('robloxUsername');
  const submitBtn = document.getElementById('submitBtn');
  let selectedKey = null;

  // Price mapping for keys
  const prices = {
    '1 Week Key': '1.00',
    '1 Month Key': '5.00',
    '1 Year Key': '50.00'
  };

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
    submitBtn.textContent = 'Processing Payment...';

    // PayPal payment process
    try {
      await createPaypalTransaction(prices[selectedKey], discordUsername, robloxUsername, selectedKey);
      closeModal();
      openVerificationModal();
    } catch (error) {
      console.error(error);
      alert('Payment failed or cancelled. Please try again.');
      submitBtn.disabled = false;
      submitBtn.textContent = 'Submit';
    }
  }

  // Create and handle PayPal payment flow
  function createPaypalTransaction(amount, discordUsername, robloxUsername, keyName) {
    return new Promise((resolve, reject) => {
      // Create a hidden PayPal button container
      let container = document.getElementById('paypal-button-container');
      if (!container) {
        container = document.createElement('div');
        container.id = 'paypal-button-container';
        container.style.display = 'none';
        document.body.appendChild(container);
      }
      container.innerHTML = '';

      paypal.Buttons({
        style: {
          layout: 'vertical',
          color:  'blue',
          shape:  'rect',
          label:  'pay',
        },
        createOrder: function(data, actions) {
          return actions.order.create({
            purchase_units: [{
              amount: {
                value: amount
              },
              description: keyName
            }]
          });
        },
        onApprove: function(data, actions) {
          return actions.order.capture().then(function(details) {
            // After payment approved, send webhook
            sendWebhook(discordUsername, robloxUsername, keyName)
              .then(() => resolve())
              .catch(err => reject(err));
          });
        },
        onCancel: function(data) {
          reject(new Error('Payment cancelled'));
        },
        onError: function(err) {
          reject(err);
        }
      }).render(container);

      // Programmatically click the hidden button (opens popup)
      container.querySelector('iframe')?.contentWindow.focus();
    });
  }

  // Send purchase info to Discord webhook
  async function sendWebhook(discordUsername, robloxUsername, keyName) {
    const webhookUrl = "https://discord.com/api/webhooks/1380632133990875156/uTfUbEfNGj5Qbev8F0cDFVGU1TVVtRRrZxGG2TJJXkbXEvXi3AaVHQ61z7dBk2qe7Na9";

    const payload = {
      embeds: [
        {
          title: "New Key Purchase",
          color: 0x3b82f6,
          fields: [
            { name: "Purchased Key", value: keyName, inline: true },
            { name: "Discord Username", value: discordUsername, inline: true },
            { name: "Roblox Username", value: robloxUsername, inline: true }
          ],
          timestamp: new Date().toISOString()
        }
      ]
    };

    const response = await fetch(webhookUrl, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(payload)
    });

    if (!response.ok) throw new Error(`Webhook error: ${response.status}`);
  }

  modal.addEventListener('click', e => {
    if (e.target === modal) closeModal();
  });

  verificationModal.addEventListener('click', e => {
    if (e.target === verificationModal) closeVerificationModal();
  });
</script>
