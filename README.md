<!DOCTYPE html>
<html>
<head>
  <title>Local Visit Counter</title>
</head>
<body>
  <h1>Welcome to my GitHub Page!</h1>
  <p>You have visited this page <span id="count">0</span> times on this browser.</p>

  <script>
    let visits = localStorage.getItem('visitCount') || 0;
    visits = Number(visits) + 1;
    localStorage.setItem('visitCount', visits);
    document.getElementById('count').textContent = visits;
  </script>
</body>
</html>
