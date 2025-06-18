<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tính Giờ Làm Việc</title>
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      background-color: #f4f4f4;
      color: #333;
    }
    h1 {
      text-align: center;
      margin-bottom: 30px;
    }
    .container {
      max-width: 500px;
      margin: 0 auto;
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }
    label {
      display: block;
      margin-bottom: 10px;
    }
    input[type="time"],
    input[type="number"] {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      width: 100%;
      padding: 10px;
      margin-top: 20px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 10px;
      text-align: center;
    }
    .result {
      margin-top: 20px;
      font-weight: bold;
      text-align: center;
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


