<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Visit Counter</title>
</head>
<body>
  <h1>Welcome to my site!</h1>
  <p>This site has been visited <span id="visits">...</span> times.</p>

  <script>
    // Replace these with your custom namespace and key
    const namespace = "your-username"; // can be anything unique
    const key = "visit-counter"; // specific counter name

    fetch(`https://api.countapi.xyz/hit/${namespace}/${key}`)
      .then(res => res.json())
      .then(data => {
        document.getElementById("visits").textContent = data.value;
      });
  </script>
</body>
</html>
