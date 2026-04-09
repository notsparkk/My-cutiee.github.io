<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For You ❤️</title>
    <style>
        /* Imports an elegant, cinematic font from Google Fonts */
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&display=swap');

        body {
            margin: 0;
            height: 100vh;
            background-color: #050505; /* Deep, dark background */
            color: #eaeaea;
            font-family: 'Playfair Display', serif;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            overflow: hidden; 
        }

        /* Ambient glowing background effect */
        .glow {
            position: absolute;
            width: 400px;
            height: 400px;
            background: radial-gradient(circle, rgba(139,0,0,0.3) 0%, rgba(0,0,0,0) 70%);
            border-radius: 50%;
            z-index: -1;
            animation: pulse-glow 5s infinite alternate ease-in-out;
        }

        @keyframes pulse-glow {
            0% { transform: scale(0.8); opacity: 0.5; }
            100% { transform: scale(1.3); opacity: 1; }
        }

        .container {
            z-index: 10;
            padding: 40px;
            max-width: 600px;
            width: 90%;
        }

        h1 {
            color: #ff3366;
            font-size: 2.5rem;
            font-weight: 400;
            letter-spacing: 3px;
            margin-bottom: 40px;
            text-shadow: 0 0 15px rgba(255, 51, 102, 0.4);
            opacity: 0;
            animation: fade-in 3s forwards 1s; /* Slow fade in on load */
        }

        @keyframes fade-in {
            to { opacity: 1; }
        }

        #message-display {
            font-size: 1.8rem;
            min-height: 150px;
            margin: 30px 0;
            line-height: 1.6;
            font-style: italic;
            border-right: 2px solid #ff3366; /* Typewriter cursor */
            white-space: pre-wrap;
            display: inline-block;
            animation: blink-cursor 0.8s step-end infinite;
        }

        @keyframes blink-cursor {
            from, to { border-color: transparent; }
            50% { border-color: #ff3366; }
        }

        button {
            background: transparent;
            color: #ff3366;
            border: 1px solid #ff3366;
            padding: 15px 40px;
            font-size: 1.1rem;
            font-family: 'Playfair Display', serif;
            letter-spacing: 2px;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.4s ease;
            text-transform: uppercase;
            box-shadow: 0 0 15px rgba(255, 51, 102, 0.2);
            opacity: 0;
            animation: fade-in 3s forwards 2s, heartbeat 2.5s infinite 5s; /* Fades in, then starts beating */
        }

        @keyframes heartbeat {
            0% { transform: scale(1); }
            10% { transform: scale(1.03); }
            20% { transform: scale(1); }
            30% { transform: scale(1.03); }
            40% { transform: scale(1); }
            100% { transform: scale(1); }
        }

        button:hover {
            background: #ff3366;
            color: #050505;
            box-shadow: 0 0 30px rgba(255, 51, 102, 0.6);
            animation: none; 
            transform: scale(1.05);
        }
    </style>
</head>
<body>

    <div class="glow"></div>

    <div class="container">
        <h1>For Manya</h1>
        <div><span id="message-display"></span></div>
        <br>
        <button onclick="triggerMessage()" id="action-btn">Remind Me</button>
    </div>

    <audio id="bg-music" loop>
        <source src="song.mp3" type="audio/mpeg">
    </audio>

    <script>
        // Update these with deep, specific memories and feelings
        const reasons = [
            "I remember the exact moment I fell for you. It still plays in my head like a movie.",
            "You have this way of looking at me that makes the rest of the world completely disappear.",
            "I never knew what peace felt like until the first time I held you.",
            "Even when we are miles apart, you are the only thing on my mind.",
            "You aren't just my favorite person; you are my best friend and my greatest adventure."
        ];

        let isTyping = false;
        let musicStarted = false;

        function triggerMessage() {
            if (isTyping) return; // Prevents her from clicking again while it's still typing
            
            // Start music on the first click
            if (!musicStarted) {
                const audio = document.getElementById("bg-music");
                audio.volume = 0.4; // Keeps the music soft and ambient
                audio.play().catch(e => console.log("Add 'song.mp3' to the folder to enable music."));
                musicStarted = true;
            }

            isTyping = true;
            const display = document.getElementById("message-display");
            const btn = document.getElementById("action-btn");
            
            btn.innerText = "Tell me more";
            display.innerText = ""; 
            
            const randomIndex = Math.floor(Math.random() * reasons.length);
            const textToType = reasons[randomIndex];
            let i = 0;

            // The Typewriter Effect Function
            function typeWriter() {
                if (i < textToType.length) {
                    display.innerHTML += textToType.charAt(i);
                    i++;
                    
                    // Randomizes the typing speed slightly so it feels like a human is typing it to her in real-time
                    const speed = Math.floor(Math.random() * 60) + 40;
                    setTimeout(typeWriter, speed);
                } else {
                    isTyping = false; 
                }
            }

            typeWriter();
        }
    </script>
</body>
</html>
