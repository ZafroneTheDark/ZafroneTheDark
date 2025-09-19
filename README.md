<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Dashboard Bisnis Bersama</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      background: #0a0f2c;
      color: white;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
    }
    h1, h2 { margin: 0 0 10px; }
    .container { display: flex; gap: 20px; flex-wrap: wrap; }
    .card {
      background: #151b3c;
      border-radius: 12px;
      padding: 20px;
      box-shadow: 0 0 10px rgba(0,0,0,0.5);
      flex: 1;
      min-width: 300px;
    }
    input, button {
      padding: 10px;
      margin: 5px 0;
      border-radius: 6px;
      border: none;
    }
    button {
      background: #28a745;
      color: white;
      cursor: pointer;
    }
    ul { padding-left: 20px; }
    canvas { width: 100% !important; height: 200px !important; }
    footer {
      margin-top: 30px;
      padding: 15px;
      text-align: center;
      background: #111633;
      border-radius: 12px;
      font-size: 14px;
      color: #ccc;
    }
    footer span {
      display: block;
      margin: 4px 0;
    }
    footer a {
      color: #25D366;
      text-decoration: none;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <h1>📊 Dashboard Bisnis Bersama</h1>

  <!-- Form Pendaftaran -->
  <div class="card">
    <h2>Form Pendaftaran</h2>
    <input type="text" id="nama" placeholder="Masukkan nama">
    <button onclick="daftarUser()">Daftar</button>
    <h3>Daftar Peserta:</h3>
    <ul id="listUser"></ul>
  </div>

  <!-- Bagian Dashboard -->
  <div class="container">
    <div class="card">
      <h2>Cash in Bank</h2>
      <div id="cashValue" class="big">$616.5K</div>
      <canvas id="cashChart"></canvas>
    </div>

    <div class="card">
      <h2>Expenses</h2>
      <canvas id="expensesChart"></canvas>
    </div>
  </div>

  <div class="container">
    <div class="card">
      <h2>Debtors</h2>
      <div class="big">$345K</div>
      <canvas id="debtorsChart"></canvas>
    </div>
    <div class="card">
      <h2>Income vs Outgoing</h2>
      <canvas id="incomeChart"></canvas>
    </div>
  </div>

  <!-- Footer -->
  <footer>
    <span>📞 Info lanjut bisa hubungi: 
      <a href="https://wa.me/6285722244875" target="_blank">
        +62 857-2224-4875
      </a>
    </span>
    <span>✍️ By: <strong>fijayM.Y</strong></span>
  </footer>

  <script>
    let users = [];

    function daftarUser() {
      let nama = document.getElementById("nama").value;
      if (nama.trim() !== "") {
        users.push(nama);
        updateUserList();
        document.getElementById("nama").value = "";
      }
    }

    function updateUserList() {
      let list = document.getElementById("listUser");
      list.innerHTML = "";
      users.forEach(u => {
        let li = document.createElement("li");
        li.textContent = u;
        list.appendChild(li);
      });
    }

    // Chart Cash
    new Chart(document.getElementById('cashChart'), {
      type: 'bar',
      data: {
        labels: ['Jan','Feb','Mar','Apr','May','Jun'],
        datasets: [{
          label: 'Cash',
          data: [1000000,950000,800000,750000,700000,650000],
          backgroundColor: 'rgba(54,162,235,0.7)'
        }]
      }
    });

    // Chart Expenses
    new Chart(document.getElementById('expensesChart'), {
      type: 'line',
      data: {
        labels: ['Jan','Feb','Mar','Apr','May','Jun'],
        datasets: [
          { label: 'Salary', data: [200000,210000,220000,230000,240000,250000], borderColor: 'cyan', fill: false },
          { label: 'Fixed Cost', data: [100000,150000,120000,90000,110000,130000], borderColor: 'magenta', fill: false }
        ]
      }
    });

    // Chart Debtors
    new Chart(document.getElementById('debtorsChart'), {
      type: 'bar',
      data: {
        labels: ['Jan','Feb','Mar','Apr','May','Jun'],
        datasets: [{
          label: 'Debtors',
          data: [200000,210000,220000,250000,300000,350000],
          backgroundColor: 'lime'
        }]
      }
    });

    // Chart Income vs Outgoing
    new Chart(document.getElementById('incomeChart'), {
      type: 'bar',
      data: {
        labels: ['Jan','Feb','Mar','Apr','May','Jun'],
        datasets: [
          { label: 'Income', data: [250000,300000,400000,300000,350000,380000], backgroundColor: 'gold' },
          { label: 'Outgoing', data: [200000,250000,300000,250000,280000,320000], backgroundColor: 'orange' }
        ]
      }
    });
  </script>
</body>
</html>