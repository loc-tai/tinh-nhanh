<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tính Giờ Làm Việc</title>
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      margin: 0;
      padding: 20px;
      background-image: url('https://em-content.zobj.net/source/joypixels/369/smiling-face_263a-fe0f.png');
      background-repeat: repeat;
      background-size: 60px 60px;
      background-color: #c2e9fb;
      color: #333;
    }
    h1 {
      text-align: center;
      margin-bottom: 30px;
      color: #2c3e50;
      text-shadow: 1px 1px 2px white;
    }
    .container {
      max-width: 500px;
      margin: 0 auto;
      background: white;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 8px 16px rgba(0,0,0,0.2);
    }
    label {
      display: block;
      margin-bottom: 10px;
      font-weight: bold;
      color: #34495e;
    }
    input[type="time"],
    input[type="number"] {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #ccc;
      border-radius: 8px;
      background-color: #f9f9f9;
    }
    button {
      width: 100%;
      padding: 12px;
      margin-top: 20px;
      background: linear-gradient(to right, #00c6ff, #0072ff);
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      transition: background 0.3s;
    }
    button:hover {
      background: linear-gradient(to right, #0072ff, #00c6ff);
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    th {
      background-color: #3498db;
      color: white;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 10px;
      text-align: center;
      background-color: #ecf0f1;
    }
    .result {
      margin-top: 20px;
      font-weight: bold;
      text-align: center;
      color: #2e86de;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Tính Giờ Làm Việc</h1>

    <label>Giờ vào:
      <input type="time" id="start">
    </label>

    <label>Giờ ra:
      <input type="time" id="end">
    </label>

    <label>Sản lượng:
      <input type="number" id="output" value="0" min="0">
    </label>

    <button onclick="calculateWorkTime()">Tính</button>

    <table>
      <thead>
        <tr>
          <th>Sản lượng</th>
          <th>Kết quả (giờ * sản lượng * 0.96)</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td id="outputDisplay">0</td>
          <td id="finalResult">--</td>
        </tr>
      </tbody>
    </table>

    <div class="result" id="result"></div>
  </div>

  <script>
    function parseTimeToMinutes(timeStr) {
      const [hours, minutes] = timeStr.split(":" ).map(Number);
      return hours * 60 + minutes;
    }

    function calculateBreakTime(startMinutes, endMinutes) {
      const breaks = [
        { start: 10 * 60, end: 10 * 60 + 10 },
        { start: 12 * 60, end: 12 * 60 + 45 },
        { start: 15 * 60, end: 15 * 60 + 10 },
        { start: 16 * 60 + 30, end: 17 * 60 },
      ];

      let totalBreak = 0;
      for (const b of breaks) {
        if (startMinutes < b.end && endMinutes > b.start) {
          const overlapStart = Math.max(startMinutes, b.start);
          const overlapEnd = Math.min(endMinutes, b.end);
          totalBreak += overlapEnd - overlapStart;
        }
      }
      return totalBreak;
    }

    function calculateWorkTime() {
      const start = document.getElementById("start").value;
      const end = document.getElementById("end").value;
      const output = parseFloat(document.getElementById("output").value);

      if (!start || !end || isNaN(output)) {
        document.getElementById("result").textContent = "Vui lòng nhập giờ vào, giờ ra và sản lượng.";
        document.getElementById("finalResult").textContent = "--";
        document.getElementById("outputDisplay").textContent = output || 0;
        return;
      }

      const startMinutes = parseTimeToMinutes(start);
      const endMinutes = parseTimeToMinutes(end);
      let workMinutes = endMinutes - startMinutes;
      const breakMinutes = calculateBreakTime(startMinutes, endMinutes);
      workMinutes -= breakMinutes;
      const totalHours = workMinutes / 60;

      const final = totalHours * output * 0.96;
      document.getElementById("result").textContent =
        `Tổng giờ: ${totalHours.toFixed(2)} | Sản lượng: ${output} | Kết quả: ${final.toFixed(2)} (đã trừ ${breakMinutes} phút nghỉ)`;

      document.getElementById("finalResult").textContent = final.toFixed(2);
      document.getElementById("outputDisplay").textContent = output;
    }
  </script>
</body>
</html>


