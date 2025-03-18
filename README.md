<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Access Code Verification</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 50px;
        }
        input, button {
            padding: 10px;
            margin: 10px;
        }
    </style>
</head>
<body>

    <h2>Enter Access Code</h2>
    <input type="text" id="accessCode" placeholder="Enter your code">
    <button onclick="checkAccess()">Submit</button>
    
    <p id="message"></p>

    <script>
        function checkAccess() {
            var code = document.getElementById("accessCode").value;
            var url = "https://script.google.com/macros/s/AKfycbwY9CNVOqHiFDXgHKoSof5MiOrFFEeIdA8o86tJw3mUZw3dVws1U3pk_72k8Cr6PdaF/exec
" + "?code=" + encodeURIComponent(code);

            fetch(url)
                .then(response => response.json())
                .then(data => {
                    if (data.valid) {
                        document.getElementById("message").innerHTML = "Access granted!";
                        // Redirect or load new content
                        window.location.href = "https://github.com/Dataone4/Offer-Calculator-.git"; 
                    } else {
                        document.getElementById("message").innerHTML = "Invalid code. Try again.";
                    }
                })
                .catch(error => console.error("Error:", error));
        }
    </script>

</body>
</html>
