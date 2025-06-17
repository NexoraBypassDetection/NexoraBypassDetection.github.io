
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Need Help?</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #0f172a, #1e293b);
      color: #e2e8f0;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 30px;
    }

    .container {
      position: relative;
      background: rgba(255, 255, 255, 0.05);
      border-radius: 24px;
      padding: 40px 30px;
      max-width: 480px;
      width: 100%;
      text-align: center;
      backdrop-filter: blur(15px);
      box-shadow: 0 10px 50px rgba(0, 0, 0, 0.5);
      overflow: hidden;
    }

    .corner-overlay {
      pointer-events: none;
      content: "";
      position: absolute;
      inset: 0;
      border-radius: 24px;
      border: 2px solid rgba(96, 165, 250, 0.5);
      box-shadow: 0 0 20px rgba(96, 165, 250, 0.5);
      opacity: 0;
      transition: opacity 1s ease;
      z-index: 0;
    }

    .corner-active .corner-overlay {
      opacity: 1;
      animation: cornerPulse 2s ease-in-out infinite;
    }

    @keyframes cornerPulse {
      0% {
        box-shadow: 0 0 10px rgba(96, 165, 250, 0.3);
      }
      50% {
        box-shadow: 0 0 20px rgba(96, 165, 250, 0.6);
      }
      100% {
        box-shadow: 0 0 10px rgba(96, 165, 250, 0.3);
      }
    }

    h1 {
      font-size: 1.8rem;
      color: #ef4444;
      margin-bottom: 16px;
      text-shadow: 0 0 8px rgba(255, 0, 0, 0.3);
      position: relative;
      z-index: 1;
    }

    h2, p, button {
      position: relative;
      z-index: 1;
    }

    h2 {
      font-size: 1.4rem;
      color: #60a5fa;
      margin-bottom: 6px;
    }

    p {
      font-size: 1rem;
      color: #94a3b8;
      margin-bottom: 24px;
    }

    button {
      background: linear-gradient(to right, #3b82f6, #60a5fa);
      color: white;
      border: none;
      padding: 14px 28px;
      font-size: 1rem;
      border-radius: 16px;
      cursor: pointer;
      transition: all 0.25s ease;
      box-shadow: 0 6px 24px rgba(96, 165, 250, 0.6);
    }

    button:hover {
      background: linear-gradient(to right, #60a5fa, #3b82f6);
      box-shadow:
        0 0 0 2px #3b82f6,
        0 0 20px 8px rgba(96, 165, 250, 0.8),
        0 10px 60px rgba(0, 0, 0, 0.55);
      transform: translateY(-2px);
    }

    .logo {
      margin-top: 32px;
      width: 100%;
      max-width: 360px;
      height: auto;
      border-radius: 16px;
      box-shadow:
        0 10px 30px rgba(30, 58, 138, 0.5),
        0 6px 16px rgba(0, 0, 0, 0.25);
      position: relative;
      z-index: 1;
    }

    @media (max-width: 500px) {
      .container {
        padding: 30px 20px;
      }

      .logo {
        max-width: 100%;
      }
    }
  </style>
</head>
<body>
  <div class="container" id="cornerBox">
    <div class="corner-overlay"></div>

    <h1>DO NOT TRY TO BYPASS THE KEY SYSTEM!</h1>
    <h2>Need assistance?</h2>
    <p>Join our verified Discord support server below</p>

    <button onclick="window.location.href='https://discord.gg/FepZCVDN'">
      Join Support Server
    </button>

    <img
      src="https://cdn.discordapp.com/attachments/1220824376123850752/1380312327806521415/NEXORA_SCRIPTS.png?ex=68436b87&is=68421a07&hm=75511ffd508259721d6878428d9e02059d0e3a937b29747089e999d58be8d8e4&"
      alt="NEXORA SCRIPTS Logo"
      class="logo"
    />
  </div>

  <script>
    const box = document.getElementById("cornerBox");
    let fadeTimeout;

    box.addEventListener("mouseenter", () => {
      clearTimeout(fadeTimeout);
      box.classList.add("corner-active");
    });

    box.addEventListener("mouseleave", () => {
      fadeTimeout = setTimeout(() => {
        box.classList.remove("corner-active");
      }, 1000); // 1s fade out
    });
  </script>
</body>
</html>
