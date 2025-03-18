<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Secure Link Access</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>This Link is Protected</h1>
    <p>Please enter your email and a code will be sent to your email. Enter the code below.</p>
    
    <form id="accessForm">
      <input type="email" id="email" placeholder="Enter your email" required />
      <button type="submit">Access Link</button>
    </form>
    
    <div id="codeInput" style="display: none;">
      <input type="text" id="verificationCode" placeholder="Enter verification code" required />
      <button onclick="verifyCode()">Verify Code</button>
    </div>
    
    <div id="message"></div>
  </div>
  <script src="script.js"></script>
</body>
</html>
