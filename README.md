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
  <h1>Welcome to MYYYYY GitHub Page!</h1>
  <p>This page has been visited:</p>
  <div id="visits">Loading...</div>
  <p>times.</p>

  <script>
    const COUNTER_SLUG = "VisitCounter"; // your counter slug
    const API_KEY = "ut_e4nlNx1iPMqnRfK8gNKDSqY1Q6HZ6nQ3UswW1U4K"; // your API key

    fetch(`https://counterapi.dev/api/v1/counter/${COUNTER_SLUG}/hit`, {
      method: "POST",
      headers: {
        "Authorization": `Bearer ${API_KEY}`,
        "Content-Type": "application/json"
      }
    })
    .then(res => {
      if (!res.ok) throw new Error(`HTTP error! status: ${res.status}`);
      return res.json();
    })
    .then(data => {
      document.getElementById("visits").textContent = data.count;
    })
    .catch(err => {
      document.getElementById("visits").textContent = "Error";
      console.error("CounterAPI error:", err);
    });
  </script>
</body>
</html>
