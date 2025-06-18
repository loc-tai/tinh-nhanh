<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Tính nhanh phần trăm</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet"/>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      padding: 0;
      font-family: 'Roboto', sans-serif;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4, #fad0c4, #fbc2eb, #a6c1ee);
      background-size: 400% 400%;
      animation: gradientBG 15s ease infinite;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      min-height: 100vh;
      padding: 40px 20px;
    }

    @keyframes gradientBG {
      0% {background-position: 0% 50%;}
      50% {background-position: 100% 50%;}
      100% {background-position: 0% 50%;}
    }

    h1 {
      color: white;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
      margin-bottom: 20px;
    }

    .container {
      background-color: rgba(255, 255, 255, 0.95);
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.2);
      max-width: 500px;
      width: 100%;
    }

    label {
      display: block;
      margin-bottom: 8px;
      font-weight: bold;
      color: #333;
    }

    input {
      width: 100%;
      padding: 12px;
      margin-bottom: 20px;
      border: 2px solid #ccc;
      border-radius: 8px;
      font-size: 16px;
      transition: border-color 0.3s ease;
    }

    input:focus {
      border-color: #ff69b4;
      outline: none;
    }

    button {
      background: linear-gradient(45deg, #ff6ec4, #7873f5);
      color: white;
      padding: 12px 24px;
      font-size: 16px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
      width: 100%;
    }

    button:hover {
      transform: scale(1.03);
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }

    .result {
      margin-top: 20px;
      font-size: 20px;
      font-weight: bold;
      text-align: center;
      color: #28a745;
    }
  </style>
</head>
<body>
  <h1>✨ Tính phần trăm nhanh ✨</h1>
  <div class="container">
    <label for="soGoc">Nhập số gốc:</label>
    <input type="number" id="soGoc" placeholder="Ví dụ: 16329">

    <label for="phanTram">Nhập % cần tính:</label>
    <input type="number" id="phanTram" placeholder="Ví dụ: 96">

    <button onclick="tinh()">💡 Tính ngay</button>

    <div class="result" id="ketQua"></div>
  </div>

  <script>
    function tinh() {
      const soGoc = parseFloat(document.getElementById("soGoc").value);
      const phanTram = parseFloat(document.getElementById("phanTram").value);

      if (isNaN(soGoc) || isNaN(phanTram)) {
        document.getElementById("ketQua").innerText = "❗ Vui lòng nhập đầy đủ!";
        return;
      }

      const ketQua = (soGoc * phanTram / 100).toFixed(2);
      document.getElementById("ketQua").innerText = ✅ ${phanTram}% của ${soGoc} là ${ketQua};
    }
  </script>
</body>
</html>

