<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Visit Counter</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      margin-top: 100px;
    }
    #visits {
      font-size: 2em;
      color: #2ecc71;
    }
  </style>
</head>
<body>
  <h1>Welcome to my site!</h1>
  <p>This page has been visited:</p>
  <div id="visits">Loading...</div>
  <p>times.</p>

  <script>
    const namespace = "NexoraBypassDetection"; // change to your unique ID
    const key = "ut_e4nlNx1iPMqnRfK8gNKDSqY1Q6HZ6nQ3UswW1U4K"; // change to anything (page name, etc.)

    fetch(`https://api.countapi.xyz/hit/${namespace}/${key}`)
      .then(res => res.json())
      .then(data => {
        document.getElementById("visits").textContent = data.value;
      })
      .catch(err => {
        document.getElementById("visits").textContent = "Error";
        console.error("CountAPI error:", err);
      });
  </script>
</body>
</html>
