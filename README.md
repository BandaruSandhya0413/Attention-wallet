# Attention-wallet
<!DOCTYPE html>
<html>
<head>
  <title>Attention Wallet</title>
  <style>
    body {
      font-family: Arial;
      background: #f4f6f8;
      padding: 20px;
    }
    h1 { color: #2c3e50; }
    .card {
      background: white;
      padding: 15px;
      margin-bottom: 15px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    button {
      margin: 5px;
      padding: 8px 12px;
      cursor: pointer;
    }
    input, select {
      padding: 6px;
      margin: 5px;
    }
  </style>
</head>
<body>

<h1>🧠 Attention Wallet</h1>

<div class="card">
  <h3>💰 Token Balance: <span id="balance">0</span></h3>
</div>

<div class="card">
  <h3>🏃 Earn Tokens</h3>
  <button onclick="earn(10)">Reading</button>
  <button onclick="earn(8)">Exercise</button>
  <button onclick="earn(12)">Homework</button>
  <button onclick="earn(6)">Family Time</button>
</div>

<div class="card">
  <h3>📱 Spend Tokens</h3>
  <select id="app">
    <option value="YouTube">YouTube / Reels</option>
    <option value="Instagram">Instagram</option>
    <option value="Games">Games</option>
    <option value="Learning">Learning Apps</option>
  </select>
  <input type="number" id="minutes" placeholder="Minutes used">
  <button onclick="spend()">Use App</button>
</div>

<div class="card">
  <h3>📊 Attention Dashboard</h3>
  <p id="report">No data yet</p>
</div>

<script>
  let balance = 0;
  let usage = {
    YouTube: 0,
    Instagram: 0,
    Games: 0,
    Learning: 0
  };

  const cost = {
    YouTube: 5,
    Instagram: 4,
    Games: 3,
    Learning: 1
  };

  function earn(tokens) {
    balance += tokens;
    update();
  }

  function spend() {
    const app = document.getElementById("app").value;
    const minutes = Number(document.getElementById("minutes").value);

    if (minutes <= 0) return alert("Enter valid minutes");

    const spent = minutes * cost[app];

    if (spent > balance) {
      alert("Not enough tokens!");
      return;
    }

    balance -= spent;
    usage[app] += spent;
    update();
  }

  function update() {
    document.getElementById("balance").innerText = balance;

    let maxApp = "";
    let maxValue = 0;

    for (let app in usage) {
      if (usage[app] > maxValue) {
        maxValue = usage[app];
        maxApp = app;
      }
    }

    document.getElementById("report").innerHTML =
      `Most attention stolen by: <b>${maxApp || "None"}</b><br>
       Tokens spent: ${maxValue}`;
  }
</script>

</body>
</html>Your attention is your money
