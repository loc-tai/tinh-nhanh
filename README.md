# tinh-nhanh<!DOCTYPE html>Add commentMore actions
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tính Giờ Làm Việc</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    label, input, select { margin: 10px; }
    .result { margin-top: 20px; font-weight: bold; }
    table { border-collapse: collapse; margin-top: 20px; }
    th, td { border: 1px solid #ccc; padding: 6px 12px; text-align: center; }
  </style>
</head>
<body>
  <h1>Tính Giờ Làm Việc</h1>
  <label>Giờ vào: <input type="time" id="start"></label>
  <label>Giờ ra: <input type="time" id="end"></label>
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
        <td><input type="number" id="output" value="0" min="0"></td>
        <td id="finalResult">--</td>
      </tr>
    </tbody>
  </table>

  <div class="result" id="result"></div>

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
        `Tổng giờ: ${totalHours.toFixed(2)} | Sản lượng: ${output} | Kết quả: ${final.toFixed(2)} (đã trừ ${breakMinutes} phút nghỉ).`;

      document.getElementById("finalResult").textContent = final.toFixed(2);
    }
  </script>
</body>
</html>
