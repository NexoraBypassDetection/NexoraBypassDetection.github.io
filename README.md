<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Keys Shop - Dark Blue Theme</title>
  <style>
    /* Reset & basics */
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #0a2342, #142850);
      color: #e0e6f1;
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
      background: #1e2a47;
      border-radius: 16px;
      box-shadow: 0 8px 20px rgba(20,40,80,0.6);
      padding: 24px 20px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      border: 1px solid #2a3b67;
      user-select: none;
    }

    .product-card:hover {
      transform: translateY(-8px);
      box-shadow: 0 18px 40px rgba(30,60,110,0.85);
      border-color: #3b82f6;
    }

    .product-title {
      font-size: 1.6rem;
      font-weight: 700;
      margin: 0 0 14px 0;
      color: #cbd5e1;
    }

    .product-price {
      font-size: 1.2rem;
      margin-bottom: 28px;
      color: #94a3b8;
    }

    .purchase-button {
      background: #3b82f6; /* bright blue */
      border: none;
      border-radius: 14px;
      padding: 16px 0;
      color: white;
      font-weight: 700;
      font-size: 1.1rem;
      cursor: pointer;
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
      box-shadow: 0 6px 12px rgba(59,130,246,0.5);
      user-select: none;
    }

    .purchase-button:hover {
      background: #2563eb;
      box-shadow: 0 10px 24px rgba(37,99,235,0.7);
    }

    .purchase-button:active {
      background: #1e40af;
      box-shadow: 0 4px 10px rgba(30,64,175,0.8);
      transform: scale(0.96);
    }

    /* Responsive text scaling */
    @media (max-width: 400px) {
      .product-title {
        font-size: 1.3rem;
      }
      .product-price {
        font-size: 1rem;
      }
      .purchase-button {
        font-size: 1rem;
        padding: 14px 0;
      }
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
    }
  </script>
</body>
</html>
