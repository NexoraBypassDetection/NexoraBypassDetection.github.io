Buy keys below
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Custom Notification Form</title>
  <style>
    body {
      background: #0f172a;
      color: white;
      font-family: Arial, sans-serif;
      padding: 40px;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }

    form {
      background: #1e293b;
      padding: 24px 32px;
      border-radius: 8px;
      width: 320px;
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    label {
      display: flex;
      flex-direction: column;
      font-weight: bold;
      font-size: 14px;
    }

    input[type="text"] {
      margin-top: 6px;
      padding: 8px 10px;
      border-radius: 6px;
      border: none;
      font-size: 14px;
    }

    input[type="checkbox"] {
      margin-right: 8px;
      transform: scale(1.3);
      cursor: pointer;
    }

    .checkbox-label {
      display: flex;
      align-items: center;
      font-weight: normal;
      font-size: 13px;
      user-select: none;
    }

    button {
      background: #2563eb;
      color: white;
      padding: 10px 0;
      border: none;
      border-radius: 6px;
      font-weight: bold;
      font-size: 15px;
      cursor: pointer;
      transition: background 0.2s ease;
    }

    button:hover {
      background: #3b82f6;
    }

    /* Notification styles */
    .notification {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      background-color: #1e293b;
      color: white;
      border-radius: 6px;
      padding: 12px 20px;
      display: flex;
      align-items: center;
      gap: 12px;
      min-width: 280px;
      max-width: 90vw;
      box-shadow: 0 4px 12px rgba(0,0,0,0.4);
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.3s ease;
      font-family: Arial, sans-serif;
      font-size: 15px;
      z-index: 9999;
    }

    .notification.show {
      opacity: 1;
      pointer-events: auto;
    }

    .notification svg {
      flex-shrink: 0;
      stroke-width: 2;
    }

    .notification .close-notif {
      background: transparent;
      border: none;
      color: white;
      font-size: 20px;
      cursor: pointer;
      padding: 0;
      line-height: 1;
      transition: color 0.2s ease;
    }

    .notification .close-notif:hover {
      color: #60a5fa;
    }
  </style>
</head>
<body>

  <form id="purchaseForm" novalidate>
    <label>
      Discord Username:
      <input type="text" id="discordUsername" placeholder="Enter Discord username" autocomplete="off" />
    </label>

    <label class="checkbox-label">
      <input type="checkbox" id="agreeCheckbox" />
      I agree to the terms and conditions
    </label>

    <button type="submit">Submit Purchase</button>
  </form>

  <!-- Custom notification -->
  <div id="customNotification" role="alert" aria-live="assertive" aria-atomic="true" class="notification" hidden>
    <svg id="notifIcon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" width="24" height="24" aria-hidden="true"></svg>
    <span id="notifMessage">Message here</span>
    <button class="close-notif" aria-label="Close notification" onclick="hideNotification()">&times;</button>
  </div>

  <script>
    const form = document.getElementById('purchaseForm');
    const discordInput = document.getElementById('discordUsername');
    const checkbox = document.getElementById('agreeCheckbox');

    const notif = document.getElementById('customNotification');
    const notifMessage = document.getElementById('notifMessage');
    const notifIcon = document.getElementById('notifIcon');

    const icons = {
      redCross: `
        <line x1="18" y1="6" x2="6" y2="18" stroke="#ef4444" stroke-width="3"></line>
        <line x1="6" y1="6" x2="18" y2="18" stroke="#ef4444" stroke-width="3"></line>
      `,
      blueCheck: `
        <polyline points="20 6 9 17 4 12" stroke="#3b82f6" stroke-width="3" fill="none"></polyline>
      `
    };

    function showNotification(message, isError = false) {
      notifMessage.textContent = message;
      notifIcon.innerHTML = isError ? icons.redCross : icons.blueCheck;
      notif.hidden = false;
      notif.classList.add('show');

      clearTimeout(notif.hideTimeout);
      notif.hideTimeout = setTimeout(() => {
        hideNotification();
      }, 4000);
    }

    function hideNotification() {
      notif.classList.remove('show');
      setTimeout(() => {
        notif.hidden = true;
      }, 300);
    }

    form.addEventListener('submit', (e) => {
      e.preventDefault();

      const username = discordInput.value.trim();
      const isChecked = checkbox.checked;

      if (!username) {
        showNotification('❌ Please enter your Discord username', true);
        discordInput.focus();
        return;
      }

      if (!isChecked) {
        showNotification('❌ Please check the box to agree', true);
        return;
      }

      // If all valid, success notification
      showNotification('✅ Purchase submitted successfully!', false);

      // Reset form or any other logic here
      form.reset();
    });
  </script>

</body>
</html>
