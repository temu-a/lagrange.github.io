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
