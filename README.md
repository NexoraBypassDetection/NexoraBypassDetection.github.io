<!DOCTYPE html>
<html>
<head>
  <title>Global Visit Counter</title>
</head>
<body>
  <h1>Welcome to my GitHub Page!</h1>
  <p>This page has been visited <span id="counter">loading...</span> times.</p>

  <script>
    const apiUrl = 'https://script.google.com/macros/s/AKfycbxOKM3RVI72IPKF6cHmbvVuajN8cxGtbFuVOUsSCIrYlXYhD38t74ENYCEfF2E_26kErQ/exec';

    fetch(apiUrl)
      .then(response => response.text())
      .then(count => {
        document.getElementById('counter').textContent = count;
      })
      .catch(() => {
        document.getElementById('counter').textContent = 'Error';
      });
  </script>
</body>
</html>
