BUYYY
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Custom Notification Form</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #0f172a;
    color: white;
    margin: 0; padding: 20px;
  }

  form {
    max-width: 400px;
    margin: 50px auto;
    background-color: #1e293b;
    padding: 20px;
    border-radius: 8px;
  }

  label {
    display: block;
    margin-bottom: 8px;
    font-weight: bold;
  }

  input[type="text"] {
    width: 100%;
    padding: 8px 10px;
    margin-bottom: 15px;
    border: none;
    border-radius: 5px;
    font-size: 16px;
  }

  input[type="checkbox"] {
    margin-right: 8px;
  }

  button {
    background-color: #3b82f6;
    color: white;
    border: none;
    padding: 12px 20px;
    border-radius: 6px;
    font-size: 16px;
    cursor: pointer;
    width: 100%;
  }

  button:hover {
    background-color: #2563eb;
  }

  /* Notification styling */
  #notification {
    position: fixed;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%);
    background-color: #1e293b;
    color: white;
    padding: 12px 20px;
    border-radius: 6px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.4);
    display: flex;
    align-items: center;
    font-size: 15px;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s ease;
    z-index: 1000;
  }

  #notification.show {
    opacity: 1;
    pointer-events: auto;
  }

  #notification svg {
    margin-right: 10px;
  }
</style>
</head>
<body>

<form id="purchaseForm">
  <label for="discordUsername">Discord Username:</label>
  <input type="text" id="discordUsername" name="discordUsername" placeholder="Enter your Discord username" />

  <label><input type="checkbox" id="agreeCheckbox" /> I agree to the terms and conditions</label>

  <button type="submit">Submit Purchase</button>
</form>

<div id="notification"></div>

<script>
  const form = document.getElementById('purchaseForm');
  const notification = document.getElementById('notification');

  function showNotification(message, type) {
    // Clear previous content
    notification.innerHTML = '';

    // Create icon span
    const iconSpan = document.createElement('span');
    iconSpan.style.display = 'inline-flex';
    iconSpan.style.alignItems = 'center';

    if (type === 'error') {
      // Red cross icon
      iconSpan.innerHTML = `
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#ef4444" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
          <line x1="18" y1="6" x2="6" y2="18"></line>
          <line x1="6" y1="6" x2="18" y2="18"></line>
        </svg>`;
    } else if (type === 'success') {
      // Blue checkmark icon
      iconSpan.innerHTML = `
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#3b82f6" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
          <polyline points="20 6 9 17 4 12"></polyline>
        </svg>`;
    }

    notification.appendChild(iconSpan);
    notification.appendChild(document.createTextNode(message));

    // Show notification
    notification.classList.add('show');

    // Hide after 4 seconds
    clearTimeout(notification.timeout);
    notification.timeout = setTimeout(() => {
      notification.classList.remove('show');
    }, 4000);
  }

  form.addEventListener('submit', (e) => {
    e.preventDefault();

    const username = form.discordUsername.value.trim();
    const isChecked = form.agreeCheckbox.checked;

    if (!username) {
      showNotification('RedCross Please enter your Discord username', 'error');
      return;
    }

    if (!isChecked) {
      showNotification('RedCross Please checkout the box', 'error');
      return;
    }

    // If all good:
    showNotification('BlueCheck Purchase submitted successfully!', 'success');

    // Here you can put your form submission code or API call...

    // Optionally clear the form
    // form.reset();
  });
</script>

</body>
</html>
