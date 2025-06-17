<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>1oz Display</title>
  <style>
    body {
      margin: 0;
      height: 100vh;
      background-color: #000; /* Black background */
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .text {
      font-size: 12rem;
      font-weight: 900;
      color: #001f4d; /* Dark blue text */
      -webkit-text-stroke: 2px #001f4d; /* Outline */
      text-shadow:
        0 0 10px #001f4d,
        0 0 20px #001f4d,
        0 0 30px #001f4d; /* Glow around edges only */
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
  </style>
</head>
<body>
  <div class="text">1oz</div>
</body>
</html>
