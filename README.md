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
