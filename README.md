<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Manya ❤️</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            /* A soft, romantic pink gradient background */
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 99%, #fecfef 100%);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            text-align: center;
            color: #333;
        }
        
        .container {
            background: white;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
            max-width: 80%;
            width: 400px;
        }

        h1 {
            margin-top: 0;
            color: #ff4d6d;
            font-size: 2rem;
        }

        #message-display {
            font-size: 1.2rem;
            min-height: 80px;
            margin: 20px 0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-style: italic;
            transition: opacity 0.3s ease-in-out;
        }

        button {
            background-color: #ff4d6d;
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 1.1rem;
            font-weight: bold;
            border-radius: 30px;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.1s;
            box-shadow: 0 4px 15px rgba(255, 77, 109, 0.4);
        }

        button:hover {
            background-color: #ff2a55;
        }

        button:active {
            transform: scale(0.95);
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Reasons I Love You</h1>
        <div id="message-display">Click the button to see why you're amazing!</div>
        <button onclick="generateReason()">Tell me why!</button>
    </div>

    <script>
        // STEP 2: Add all your personal reasons here! 
        // Make sure each phrase is wrapped in quotes and separated by a comma.
        const reasons = [
            "Your smile brightens up my entire day.",
            "The way you laugh at my terrible jokes.",
            "Because every moment with you feels special.",
            "You always know how to make me feel better.",
            "You are the most beautiful person I know, inside and out.",
            "I love our late-night conversations.",
            "You make me want to be a better person."
        ];

        function generateReason() {
            const display = document.getElementById("message-display");
            
            // Generate a random number based on how many reasons you have
            const randomIndex = Math.floor(Math.random() * reasons.length);
            
            // Fades the text out, changes it, and fades it back in smoothly
            display.style.opacity = 0;
            setTimeout(() => {
                display.innerText = reasons[randomIndex];
                display.style.opacity = 1;
            }, 300); 
        }
    </script>
</body>
</html>
