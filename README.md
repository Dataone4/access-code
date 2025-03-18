<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Verification Page</title>
    <!-- Link to the external style.css file -->
    <link rel="stylesheet" href="style.css">
    <!-- Link to Google Fonts for Montserrat -->
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@700&display=swap" rel="stylesheet">
</head>
<body>
    <div class="container">
        <h1>This link is protected</h1>
        <h2>Please enter your email and a code will be sent to your email. Enter the code below.</h2>

        <div class="form-container">
            <!-- Email input form -->
            <form id="email-form">
                <input type="email" id="email" placeholder="Enter your email" required>
                <button type="submit">Request Code</button> <!-- Button to request the code -->
            </form>

            <!-- Code input form (hidden initially) -->
            <form id="code-form" style="display: none;">
                <input type="text" id="code" placeholder="Enter the code" required>
                <button type="submit">Verify Code</button> <!-- Button to verify the code -->
            </form>

            <!-- Final access button (hidden initially) -->
            <div id="access-button-container" style="display: none;">
                <button id="access-button">Get Access</button> <!-- Button to get access after code verification -->
            </div>
        </div>
    </div>

    <script>
        const emailForm = document.getElementById('email-form');
        const codeForm = document.getElementById('code-form');
        const accessButtonContainer = document.getElementById('access-button-container');
        const emailInput = document.getElementById('email');
        const codeInput = document.getElementById('code');

        // Handle email form submission
        emailForm.addEventListener('submit', async (e) => {
            e.preventDefault();

            const email = emailInput.value;
            if (!email) {
                alert('Please enter a valid email address');
                return;
            }

            try {
                // Send email to backend for code generation (using Resend API)
                const response = await fetch('/api/send-verification-email', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({ email })
                });

                if (response.ok) {
                    alert('Verification code sent! Please check your email.');
                    emailForm.style.display = 'none';
                    codeForm.style.display = 'block';
                } else {
                    alert('Failed to send verification code. Please try again.');
                }
            } catch (error) {
                console.error(error);
                alert('An error occurred. Please try again later.');
            }
        });

        // Handle code form submission
        codeForm.addEventListener('submit', async (e) => {
            e.preventDefault();

            const code = codeInput.value;
            if (!code) {
                alert('Please enter the code');
                return;
            }

            try {
                // Send the code for verification (you can add further backend verification logic here)
                const response = await fetch('/api/verify-code', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({ code })
                });

                if (response.ok) {
                    alert('Code verified successfully!');
                    codeForm.style.display = 'none';
                    accessButtonContainer.style.display = 'block'; // Show "Get Access" button
                } else {
                    alert('Invalid code. Please try again.');
                }
            } catch (error) {
                console.error(error);
                alert('An error occurred. Please try again later.');
            }
        });

        // Handle access button click
        document.getElementById('access-button').addEventListener('click', () => {
            alert('You now have access!');
            // Optionally, redirect to the desired page after gaining access
        });
    </script>
</body>
</html>
