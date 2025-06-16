Purchase Keys Below!
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Custom Checkbox Form</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: #f7f9fc;
    margin: 0; padding: 40px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  form {
    background: white;
    padding: 30px 40px;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    width: 320px;
  }
  label {
    display: flex;
    align-items: center;
    gap: 12px;
    font-size: 18px;
    user-select: none;
  }
  input[type="checkbox"] {
    width: 22px;
    height: 22px;
  }
  button {
    margin-top: 24px;
    width: 100%;
    background-color: #1a73e8;
    color: white;
    border: none;
    border-radius: 6px;
    padding: 14px;
    font-size: 18px;
    cursor: pointer;
    font-weight: 700;
    transition: background-color 0.3s ease;
  }
  button:hover {
    background-color: #155bb5;
  }
  /* Notifications container */
  #notifications {
    position: fixed;
    bottom: 30px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
    z-index: 1000;
    max-width: 90vw;
  }
  .notification {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 14px 22px;
    border-radius: 8px;
    font-size: 16px;
    font-weight: 600;
    color: #333;
    background-color: #e0e0e0;
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    opacity: 1;
    animation: fadeInUp 0.4s ease forwards;
  }
  .notification.error {
    background-color: #fce8e6;
    color: #d93025;
  }
  .notification.success {
    background-color: #e8f0fe;
    color: #1a73e8;
  }
  .notification svg {
    flex-shrink: 0;
  }

  @keyframes fadeInUp {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
</style>
</head>
<body>

<form id="myForm">
  <label>
    <input type="checkbox" id="agreeCheckbox" />
    I agree to the terms and conditions
  </label>
  <button type="submit">Submit</button>
</form>

<div id="notifications"></div>

<script>
  const form = document.getElementById('myForm');
  const checkbox = document.getElementById('agreeCheckbox');
  const notifications = document.getElementById('notifications');

  // Icon HTML strings
  function createIcon(type) {
    if (type === 'error') {
      return `
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#d93025" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="18" y1="6" x2="6" y2="18" />
          <line x1="6" y1="6" x2="18" y2="18" />
        </svg>
      `;
    } else if (type === 'success') {
      return `
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#1a73e8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polyline points="20 6 9 17 4 12" />
        </svg>
      `;
    }
  }

  // Show notification
  function showNotification(type, message) {
    const notif = document.createElement('div');
    notif.classList.add('notification', type);
    notif.innerHTML = createIcon(type) + `<span>${message}</span>`;
    notifications.appendChild(notif);

    // Auto-remove after 4 seconds
    setTimeout(() => {
      notif.style.opacity = '0';
      notif.style.transform = 'translateY(20px)';
      setTimeout(() => notif.remove(), 400);
    }, 4000);
  }

  form.addEventListener('submit', e => {
    e.preventDefault();

    if (!checkbox.checked) {
      showNotification('error', '❌ Please check the box before submitting.');
      return;
    }

    // Simulated webhook call - replace this with your backend call
    fakeWebhookSubmit()
      .then(() => {
        showNotification('success', '✔️ Form submitted successfully!');
        checkbox.checked = false; // reset checkbox
      })
      .catch(() => {
        showNotification('error', '❌ Failed to submit. Please try again.');
      });
  });

  // Fake webhook function simulating async request (replace with real backend POST)
  function fakeWebhookSubmit() {
    return new Promise((resolve, reject) => {
      // Simulate network delay and random success/fail
      setTimeout(() => {
        // 90% chance success
        if (Math.random() < 0.9) resolve();
        else reject();
      }, 1200);
    });
  }
</script>

</body>
</html>
