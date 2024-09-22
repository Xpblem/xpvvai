<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>XPVVAI Confirmation</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            height: 100vh; /* Full height */
            margin: 0; /* Remove default margin */
            overflow: hidden; /* Prevent scrollbars */
            color: #00ff00; /* Green text color */
            background: linear-gradient(135deg, #000000, #1a1a1a); /* Gradient background */
            position: relative; /* Positioning for absolute elements */
            animation: backgroundAnimation 10s infinite alternate; /* Background animation */
        }

        @keyframes backgroundAnimation {
            0% { background: #000000; }
            100% { background: #1a1a1a; }
        }

        .falling {
            position: absolute;
            white-space: nowrap; /* Prevent line breaks */
            font-size: 20px; /* Font size */
            animation: fall linear infinite; /* Animation */
            cursor: pointer; /* Change cursor to pointer */
        }

        @keyframes fall {
            0% {
                transform: translateY(100vh); /* Start from the bottom of the screen */
            }
            100% {
                transform: translateY(-100%); /* Move to the top of the screen */
            }
        }

        .popup {
            position: absolute;
            top: 50%; /* Center vertically */
            left: 50%; /* Center horizontally */
            transform: translate(-50%, -50%) perspective(600px); /* 3D effect */
            background: rgba(0, 0, 0, 0.8); /* Semi-transparent background */
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
            text-align: center;
            z-index: 2; /* Ensure the popup is above the background */
            width: 80%; /* Responsive width */
            max-width: 400px; /* Maximum width for larger screens */
        }

        @keyframes pop {
            from {
                transform: scale(0);
            }
            to {
                transform: scale(1);
            }
        }

        .button {
            margin-top: 10px;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 18px; /* Increased font size for better visibility */
            position: relative;
            overflow: hidden; /* Hide overflow for the flip effect */
            transition: transform 0.5s; /* Smooth transition for flip */
        }

        .yes {
            background-color: #28a745; /* Green */
            box-shadow: 0 0 20px rgba(40, 167, 69, 0.7); /* RGB light effect */
        }

        .no {
            background-color: #dc3545; /* Red */
            box-shadow: 0 0 20px rgba(220, 53, 69, 0.7); /* RGB light effect */
        }

        .button:hover {
            transform: rotateY(180deg); /* Flip effect on hover */
        }

        /* Responsive adjustments */
        @media (max-width: 600px) {
            .popup {
                width: 90%; /* Use more width on smaller screens */
                padding: 15px; /* Less padding on smaller screens */
            }

            .button {
                font-size: 16px; /* Slightly smaller button text */
                padding: 8px 16px; /* Smaller padding */
            }
        }

        /* Footer styling */
        footer {
            position: absolute;
            bottom: 10px; /* Align to the bottom */
            right: 10px; /* Align to the right */
            color: white; /* Text color */
            font-size: 16px; /* Increased font size */
            background-color: rgba(0, 0, 0, 0.7); /* Semi-transparent background */
            padding: 5px 10px; /* Padding for better readability */
            border-radius: 5px; /* Rounded corners */
            z-index: 3; /* Ensure footer is above the background */
        }
    </style>
    <script>
        let passwordAttempts = 0; // Counter for password attempts

        function showPopup() {
            const popup = document.getElementById("popup");
            popup.style.display = "block";
        }

        function showPasswordPopup() {
            const passwordPopup = document.getElementById("passwordPopup");
            passwordPopup.style.display = "block";
        }

        function showConfirmationPopup() {
            const confirmPopup = document.getElementById("confirmPopup");
            confirmPopup.style.display = "block";
        }

        function showFinalPopup() {
            const finalPopup = document.getElementById("finalPopup");
            finalPopup.style.display = "block";
        }

        function showClosePopup() {
            const closePopup = document.getElementById("closePopup");
            closePopup.style.display = "block";
        }

        function handleResponse(response) {
            const popup = document.getElementById("popup");
            popup.style.display = "none";
            if (response === "yes") {
                showPasswordPopup(); // Show password popup
            } else {
                window.location.href = "https://www.google.com"; // Redirect to Google
            }
        }

        function checkPassword() {
            const passwordInput = document.getElementById("passwordInput").value;
            const passwordPopup = document.getElementById("passwordPopup");
            if (passwordInput === "xpblem2024") {
                passwordPopup.style.display = "none"; // Hide password popup
                showConfirmationPopup(); // Show confirmation popup
            } else {
                passwordAttempts++; // Increment password attempt counter
                if (passwordAttempts >= 5) {
                    alert("Too many incorrect attempts. Redirecting to Google.");
                    window.location.href = "https://www.google.com"; // Redirect to Google
                } else {
                    alert("Incorrect password. Please try again.");
                }
            }
        }

        function confirmRedirect() {
            window.location.href = "https://xpvvai.wordpress.com/content-finder/"; // Redirect to specified URL
        }

        function cancelRedirect() {
            const confirmPopup = document.getElementById("confirmPopup");
            confirmPopup.style.display = "none"; // Hide confirmation popup
            showFinalPopup(); // Show final message popup
        }

        function closeFinalPopup() {
            showClosePopup(); // Show the close warning popup
        }

        function closeWarningPopup() {
            const closePopup = document.getElementById("closePopup");
            closePopup.style.display = "none"; // Hide close warning popup
            window.close(); // Attempt to close the website
        }

        function createFallingText() {
            const container = document.body;
            const characters = '01';
            for (let i = 0; i < 150; i++) { // Create 150 falling elements
                const fallingText = document.createElement('div');
                fallingText.className = 'falling';
                fallingText.style.left = Math.random() * 100 + 'vw'; // Random horizontal position

                // Increase duration to decrease speed
                const duration = Math.random() * 0.5 + 0.5; // Random duration between 0.5s and 1s
                fallingText.style.animationDuration = duration + 's'; // Random duration

                fallingText.innerText = characters.charAt(Math.floor(Math.random() * characters.length));
                
                // Add click event for changing background color on "1"
                fallingText.addEventListener('click', function() {
                    if (fallingText.innerText === '1') {
                        document.body.style.backgroundColor = getRandomColor(); // Change background color
                    }
                });

                container.appendChild(fallingText);
            }
        }

        function getRandomColor() {
            const letters = '0123456789ABCDEF';
            let color = '#';
            for (let i = 0; i < 6; i++) {
                color += letters[Math.floor(Math.random() * 16)];
            }
            return color;
        }

        window.onload = function() {
            showPopup();
            createFallingText(); // Create falling text when the page loads
        };

        // Mouse movement effect
        document.addEventListener('mousemove', (event) => {
            const popup = document.getElementById("popup");
            const x = (event.clientX / window.innerWidth) * 2 - 1; // Normalize to -1 to 1
            const y = (event.clientY / window.innerHeight) * 2 - 1; // Normalize to -1 to 1

            // Apply 3D rotation effect based on mouse position
            popup.style.transform = `translate(-50%, -50%) perspective(600px) rotateY(${x * 10}deg) rotateX(${-y * 10}deg)`;
        });

        // Change text color to RGB light effect on hover
        function changeColorOnHover(element) {
            element.style.color = 'rgb(0, 255, 255)'; // Change to cyan as RGB effect
            element.style.textShadow = '0 0 5px rgb(0, 255, 255), 0 0 10px rgb(0, 0, 255)'; // RGB glow effect
        }

        function resetColor(element) {
            element.style.color = '#00ff00'; // Reset to original color
            element.style.textShadow = 'none'; // Reset glow effect
        }
    </script>
</head>
<body>

    <div id="popup" class="popup" style="display:none;">
        <h1 onmouseover="changeColorOnHover(this)" onmouseout="resetColor(this)">Welcome to the XPVVAI Website</h1>
        <p onmouseover="changeColorOnHover(this)" onmouseout="resetColor(this)">This website is managed by XPBLEM and is intended for personal use by XPBLEM, their friends, and family members.</p>
        <p onmouseover="changeColorOnHover(this)" onmouseout="resetColor(this)">Do you know XPBLEM?</p>
        <button class="button yes" onclick="handleResponse('yes')">Yes</button>
        <button class="button no" onclick="handleResponse('no')">No</button>
    </div>

    <div id="passwordPopup" class="popup" style="display:none;">
        <h2>Enter Password</h2>
        <input type="password" id="passwordInput" placeholder="Password" />
        <button class="button yes" onclick="checkPassword()">Submit</button>
        <button class="button no" onclick="document.getElementById('passwordPopup').style.display='none'">Cancel</button>
    </div>

    <div id="confirmPopup" class="popup" style="display:none;">
        <h2 onmouseover="changeColorOnHover(this)" onmouseout="resetColor(this)">You are directing to a simple UI</h2>
        <p onmouseover="changeColorOnHover(this)" onmouseout="resetColor(this)">Click OK to proceed.</p>
        <button class="button yes" onclick="confirmRedirect()">OK</button>
        <button class="button no" onclick="cancelRedirect()">Cancel</button>
    </div>

    <div id="finalPopup" class="popup" style="display:none;">
        <h2 style="font-weight: bold;">CHALA JA BSDK</h2>
        <button class="button yes" onclick="closeFinalPopup()">Close</button>
    </div>

    <div id="closePopup" class="popup" style="display:none;">
        <h2>SAALE ABHI BHI WEBSITE CLOSE NAHI KIYA. AB TO CHALA JA NAHI TO AMMA BEHEN PE AA JAUNGA</h2>
        <button class="button yes" onclick="closeWarningPopup()">Close</button>
    </div>

    <footer>
        Designed by Ranjan's Brothers
    </footer>

</body>
</html>
