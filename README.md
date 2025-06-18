<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tính nhanh</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Roboto', sans-serif;
      background-color: #f0f4f8;
      color: #333;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 40px 20px;
    }

    h1 {
      color: #007acc;
      margin-bottom: 20px;
    }

    .container {
      background-color: #ffffff;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
      max-width: 500px;
      width: 100%;
    }

    label {
      display: block;
      margin-bottom: 8px;
      font-weight: bold;
    }

    input {
      width: 100%;
      padding: 10px;
      margin-bottom: 20px;
      border: 1px solid #ccc;
      border-radius: 5px;
      font-size: 16px;
    }

    button {
      background-color: #007acc;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    button:hover {
      background-color: #005f99;
    }

    .result {
      margin-top: 20px;
      font-size: 18px;
      font-weight: bold;
      color: #28a745;
    }
  </style>
</head>
<body>
  <h1>Tính phần trăm nhanh</h1>
  <div class="container">
    <label for="soGoc">Nhập số gốc:</label>
    <input type="number" id="soGoc" placeholder="Ví dụ: 16329">
    
    <label for="phanTram">Nhập % cần tính:</label>
    <input type="number" id="phanTram" placeholder="Ví dụ: 96">
    
    <button onclick="tinh()">Tính ngay</button>
    
    <div class="result" id="ketQua"></div>
  </div>

  <script>
    function tinh() {
      const soGoc = parseFloat(document.getElementById("soGoc").value);
      const phanTram = parseFloat(document.getElementById("phanTram").value);

      if (isNaN(soGoc) || isNaN(phanTram)) {
        document.getElementById("ketQua").innerText = "Vui lòng nhập đầy đủ!";
        return;
      }

      const ketQua = (soGoc * phanTram / 100).toFixed(2);
      document.getElementById("ketQua").innerText = ${phanTram}% của ${soGoc} là ${ketQua};
    }
  </script>
</body>
</html>

