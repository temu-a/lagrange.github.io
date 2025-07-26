<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>LAUSD</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      width: 100%;
      overflow: hidden;
      background-color: black;
      font-family: Arial, sans-serif;
      direction: rtl;
    }

    #container {
      position: relative;
      width: 100vw;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    #result {
      position: absolute;
      top: 20px;
      left: 50%;
      transform: translateX(-50%);
      background: #000;
      color: #0f0;
      padding: 10px 20px;
      border-radius: 8px;
      font-size: 1.5rem;
      z-index: 9999;
      box-shadow: 0 0 10px rgba(0,255,0,0.3);
    }

    #chart {
      width: 100%;
      height: 100%;
    }
  </style>
</head>
<body>

  <div id="container">
    <div id="result">...</div>
    <div id="chart"></div>
  </div>

  <script src="https://s3.tradingview.com/tv.js"></script>
  <script>
    const coinGeckoId = 'lagrange';
    const multiplier = 0.18319176;

    async function fetchPrice() {
      try {
        const response = await fetch(`https://api.coingecko.com/api/v3/simple/price?ids=${coinGeckoId}&vs_currencies=usd`);
        const data = await response.json();
        if (data[coinGeckoId] && data[coinGeckoId].usd) {
          return data[coinGeckoId].usd;
        }
        throw new Error('السعر غير متاح');
      } catch (error) {
        console.error(error);
        return null;
      }
    }

    async function updatePrice() {
      const price = await fetchPrice();
      const resultDiv = document.getElementById('result');
      if (price !== null) {
        const finalPrice = price * multiplier;
        resultDiv.textContent = finalPrice.toFixed(6) + ' USD';
      } else {
        resultDiv.textContent = 'تعذر جلب السعر.';
      }
    }

    updatePrice();
    setInterval(updatePrice, 60000);

    new TradingView.widget({
      autosize: true,
      symbol: "COINBASE:LAUSD",
      interval: "60",
      timezone: "Asia/Jerusalem",
      theme: "dark",
      style: "1",
      locale: "ar",
      toolbar_bg: "#000",
      enable_publishing: false,
      hide_side_toolbar: true,
      allow_symbol_change: false,
      container_id: "chart"
    });
  </script>

</body>
</html>
