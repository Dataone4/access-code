<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Email Verification</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="style.css"> <!-- Link to your CSS file -->
</head>
<body>
  <div class="verification-container">
    <h2>Email Verification</h2>

    <div class="input-group">
      <label for="email">Enter your email</label>
      <input type="email" id="email" placeholder="Enter your email" />
    </div>

    <button id="sendCodeBtn">Send Code</button>

    <div class="input-group" id="codeInputGroup" style="display: none;">
      <label for="code">Enter verification code</label>
      <input type="text" id="code" placeholder="Enter the code sent to your email" />
    </div>

    <button id="verifyCodeBtn" style="display: none;">Verify Code</button>

    <div class="result" id="resultContainer">
      <p>Verification successful!</p>
    </div>
  </div>

  <script>
    const sendCodeBtn = document.getElementById('sendCodeBtn');
    const verifyCodeBtn = document.getElementById('verifyCodeBtn');
    const emailInput = document.getElementById('email');
    const codeInput = document.getElementById('code');
    const codeInputGroup = document.getElementById('codeInputGroup');
    const resultContainer = document.getElementById('resultContainer');

    sendCodeBtn.addEventListener('click', function() {
      const email = emailInput.value;
      if (email) {
        // Here you would call the backend to send the code
        alert('Verification code sent to ' + email); // Simulate sending the code

        // Show the code input and verify button
        codeInputGroup.style.display = 'block';
        verifyCodeBtn.style.display = 'block';
      } else {
        alert('Please enter a valid email.');
      }
    });

    verifyCodeBtn.addEventListener('click', function() {
      const code = codeInput.value;
      if (code === '123456') {  // Example code, replace with real logic
        resultContainer.style.display = 'block';
      } else {
        alert('Invalid code. Please try again.');
      }
    });
  </script>
</body>
</html>
