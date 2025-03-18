<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Email Verification</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #271b0c; /* brown color */
      --primary-hover: #b02125; /* dark brown hover */
      --background: #f0f0f0; /* light grey background */
      --card-bg: #ffffff; /* white background for card */
      --text: #271b0c; /* brown text */
      --border-radius: 12px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Montserrat', sans-serif;
      background: var(--background);
      color: var(--text);
      padding: 20px;
      line-height: 1.6;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .verification-container {
      width: 100%;
      max-width: 500px;
      background: var(--card-bg);
      padding: 30px;
      border-radius: var(--border-radius);
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }

    h2 {
      margin-bottom: 20px;
      color: var(--primary);
      text-align: center;
    }

    .input-group {
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-bottom: 8px;
      font-weight: 500;
    }

    input[type="email"], input[type="text"] {
      width: 100%;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 6px;
      font-family: inherit;
      margin-bottom: 15px;
    }

    .button {
      display: block;
      width: 100%;
      padding: 12px 20px;
      background-color: var(--primary);
      color: #fff;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      font-family: inherit;
      font-weight: 600;
      font-size: 16px;
      margin: 20px 0;
    }

    .button:hover {
      background-color: var(--primary-hover);
    }

    .result {
      background-color: #f5f5f5;
      padding: 15px;
      border-radius: 8px;
      margin-top: 20px;
      display: none;
    }

    .result.active {
      display: block;
    }

    .result-value {
      font-size: 24px;
      font-weight: 600;
      color: var(--primary);
      margin: 10px 0;
    }

    @media (max-width: 600px) {
      .verification-container {
        padding: 20px;
      }
    }
  </style>
</head>
<body>
  <div class="verification-container">
    <h2>Email Verification</h2>
    
    <div class="input-group">
      <label for="email">Enter your email:</label>
      <input 
        type="email" 
        id="email" 
        placeholder="Enter your email"
      >
    </div>

    <button class="button" id="requestCodeBtn">Request Code</button>

    <div class="input-group">
      <label for="code">Enter the code:</label>
      <input 
        type="text" 
        id="code" 
        placeholder="Enter verification code"
      >
    </div>

    <button class="button" id="verifyCodeBtn">Verify Code</button>

    <div class="result" id="resultContainer">
      <h3>Verification Status</h3>
      <div class="result-value" id="resultMessage"></div>
    </div>
  </div>

  <script>
    const emailInput = document.getElementById('email');
    const codeInput = document.getElementById('code');
    const requestCodeBtn = document.getElementById('requestCodeBtn');
    const verifyCodeBtn = document.getElementById('verifyCodeBtn');
    const resultContainer = document.getElementById('resultContainer');
    const resultMessage = document.getElementById('resultMessage');

    requestCodeBtn.addEventListener('click', () => {
      const email = emailInput.value;
      if (!email) {
        alert("Please enter a valid email.");
        return;
      }
      
      fetch('/api/send-verification-email', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ email: email })
      })
      .then(response => response.json())
      .then(data => {
        if (data.success) {
          alert('Verification code sent to your email.');
        } else {
          alert('Failed to send verification code. Please try again.');
        }
      });
    });

    verifyCodeBtn.addEventListener('click', () => {
      const email = emailInput.value;
      const code = codeInput.value;

      if (!email || !code) {
        alert("Please enter both email and code.");
        return;
      }

      fetch('/api/verify-code', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ email: email, code: code })
      })
      .then(response => response.json())
      .then(data => {
        if (data.success) {
          resultMessage.textContent = "Verification successful!";
          resultContainer.classList.add('active');
        } else {
          resultMessage.textContent = "Invalid code. Please try again.";
          resultContainer.classList.add('active');
        }
      });
    });
  </script>
</body>
</html>
