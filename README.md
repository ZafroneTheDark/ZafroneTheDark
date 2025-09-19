<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>FijayM.Y Business</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: #f5f6fa;
    }
    header {
      background: linear-gradient(135deg, #2c3e50, #34495e);
      color: white;
      text-align: center;
      padding: 20px;
    }
    h1 {
      margin: 0;
    }
    .container {
      padding: 20px;
      max-width: 900px;
      margin: auto;
      background: white;
      border-radius: 12px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      margin-bottom: 20px;
    }
    .form-section, .dashboard, .transaksi {
      margin-bottom: 30px;
    }
    input, button {
      padding: 12px;
      margin: 8px 0;
      width: 100%;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 16px;
    }
    button {
      background: #27ae60;
      color: white;
      cursor: pointer;
      font-weight: bold;
    }
    button:hover {
      background: #219150;
    }
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      background: #ecf0f1;
      padding: 10px;
      border-radius: 5px;
      margin-bottom: 5px;
    }
    .total {
      font-weight: bold;
      color: #2c3e50;
      margin-top: 10px;
    }
    footer {
      margin-top: 30px;
      padding: 20px;
      text-align: center;
      background: #111633;
      border-radius: 12px 12px 0 0;
      font-size: 14px;
      color: #ccc;
    }
    .wa-btn {
      display: inline-block;
      margin: 10px 0;
      padding: 12px 20px;
      background: #25D366;
      color: white;
      font-weight: bold;
      border-radius: 8px;
      text-decoration: none;
      transition: 0.3s;
    }
    .wa-btn:hover {
      background: #1ebe5d;
    }
  </style>
</head>
<body>
  <header>
    <h1>🚀 FijayM.Y Business</h1>
    <p>Tempat bergabung & transaksi bisnis</p>
  </header>

  <div class="container form-section">
    <h2>📌 Pendaftaran</h2>
    <form id="registerForm">
      <input type="text" id="name" placeholder="Nama Lengkap" required>
      <input type="email" id="email" placeholder="Email" required>
      <input type="number" id="amount" placeholder="Nominal Investasi (Rp)" required>
      <button type="submit">Daftar & Bergabung</button>
    </form>
    <p id="msg"></p>
  </div>

  <div class="container dashboard">
    <h2>📊 Dashboard Bisnis</h2>
    <ul id="userList"></ul>
  </div>

  <div class="container transaksi">
    <h2>💰 Transaksi Bisnis</h2>
    <p>Klik untuk menambah transaksi:</p>
    <button onclick="tambahTransaksi(50000)">+ Rp50.000</button>
    <button onclick="tambahTransaksi(100000)">+ Rp100.000</button>
    <button onclick="tambahTransaksi(200000)">+ Rp200.000</button>
    <p class="total">Total Transaksi: <span id="total">Rp0</span></p>
  </div>

  <footer>
    <p>📞 Info lanjut bisa hubungi:</p>
    <a href="https://wa.me/6285722244875" target="_blank" class="wa-btn">💬 Chat via WhatsApp</a>
    <p>By: <b>FijayM.Y</b></p>
  </footer>

  <script>
    const form = document.getElementById('registerForm');
    const userList = document.getElementById('userList');
    const msg = document.getElementById('msg');
    const totalEl = document.getElementById('total');

    let users = JSON.parse(localStorage.getItem('users')) || [];
    let totalTransaksi = parseInt(localStorage.getItem('totalTransaksi')) || 0;

    // tampilkan data awal
    users.forEach(user => {
      let li = document.createElement('li');
      li.textContent = `${user.name} (${user.email}) - Rp${user.amount}`;
      userList.appendChild(li);
    });
    totalEl.textContent = "Rp" + totalTransaksi.toLocaleString();

    form.addEventListener('submit', (e) => {
      e.preventDefault();
      const name = document.getElementById('name').value;
      const email = document.getElementById('email').value;
      const amount = document.getElementById('amount').value;

      let user = { name, email, amount };
      users.push(user);
      localStorage.setItem('users', JSON.stringify(users));

      let li = document.createElement('li');
      li.textContent = `${name} (${email}) - Rp${amount}`;
      userList.appendChild(li);

      msg.textContent = "✅ Pendaftaran berhasil!";
      form.reset();
    });

    function tambahTransaksi(nominal) {
      totalTransaksi += nominal;
      localStorage.setItem('totalTransaksi', totalTransaksi);
      totalEl.textContent = "Rp" + totalTransaksi.toLocaleString();
    }
  </script>
</body>
</html>