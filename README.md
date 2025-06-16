<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Visit Counter (Local Only)</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin-top: 100px;
    }
    #visits {
      font-size: 2em;
      color: #3498db;
    }
  </style>
</head>
<body>
  <h1>Welcome to my site!</h1>
  <p>You have visited this site:</p>
  <div id="visits">Loading...</div>
  <p>times (on this device only).</p>

  <script>
    // Local tracking using browser storage
    let visits = localStorage.getItem("my-site-visits");
    if (!visits) {
      visits = 1;
    } else {
      visits = parseInt(visits) + 1;
    }
    localStorage.setItem("my-site-visits", visits);
    document.getElementById("visits").textContent = visits;
  </script>
</body>
</html>
