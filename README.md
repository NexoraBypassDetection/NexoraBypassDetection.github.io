<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Keys Shop</title>
  <style>
    /* Reset & basics */
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #f0f2f5;
      color: #333;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
      padding: 40px 20px;
    }

    .shop-container {
      max-width: 900px;
      width: 100%;
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(260px,1fr));
      gap: 30px;
    }

    .product-card {
      background: #fff;
      border-radius: 16px;
      box-shadow: 0 10px 20px rgba(0,0,0,0.08);
      padding: 24px 20px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }

    .product-card:hover {
      transform: translateY(-6px);
      box-shadow: 0 16px 30px rgba(0,0,0,0.12);
    }

    .product-title {
      font-size: 1.5rem;
      font-weight: 700;
      margin: 0 0 12px 0;
      color: #222;
      user-select: none;
    }

    .product-price {
      font-size: 1.125rem;
      margin-bottom: 24px;
      color: #555;
      user-select: none;
    }

    .purchase-button {
      background: #3b82f6; /* blue */
      border: none;
      border-radius: 12px;
      padding: 14px 0;
      color: white;
      font-weight: 600;
      font-size: 1rem;
      cursor: pointer;
      transition: background-color 0.25s ease;
      user-select: none;
      box-shadow: 0 4px 8px rgba(59,130,246,0.3);
    }

    .purchase-button:hover {
      background: #2563eb;
      box-shadow: 0 6px 14px rgba(37,99,235,0.4);
    }

    .purchase-button:active {
      background: #1e40af;
      box-shadow: 0 2px 6px rgba(30,64,175,0.5);
      transform: scale(0.97);
    }
  </style>
</head>
<body>
  <main class="shop-container">
    <div class="product-card">
      <h2 class="product-title">1 Week Key</h2>
      <p class="product-price">Price: $1</p>
      <button class="purchase-button" onclick="purchase('1 Week Key')">Purchase</button>
    </div>

    <div class="product-card">
      <h2 class="product-title">1 Month Key</h2>
      <p class="product-price">Price: $5</p>
      <button class="purchase-button" onclick="purchase('1 Month Key')">Purchase</button>
    </div>

    <div class="product-card">
      <h2 class="product-title">1 Year Key</h2>
      <p class="product-price">Price: $50</p>
      <button class="purchase-button" onclick="purchase('1 Year Key')">Purchase</button>
    </div>
  </main>

  <script>
    function purchase(keyName) {
      alert(`Thanks for purchasing the ${keyName}!`);
      // You can later replace this alert with real payment logic
    }
  </script>
</body>
</html>
