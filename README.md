<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Manya ❤️</title>
    <style>
        /* Immersive, romantic Google Font */
        @import url('https://fonts.googleapis.com/css2?family=Great+Vibes&family=Poppins:wght@300;400;600&display=swap');

        body {
            margin: 0;
            padding: 0;
            height: 100vh;
            width: 100vw;
            /* STEP A: Your Pink Rose Background */
            /* You need a file named roses.jpg in the same folder */
            background-image: url('roses.jpg'); 
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            font-family: 'Poppins', sans-serif;
            overflow: hidden; /* Keeps scrollbars away as butterflies build up */
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* Dark overlay to make text readable against the busy rose background */
        .overlay {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0, 0, 0, 0.5); /* Adjust opacity here (0.5 = 50%) */
            z-index: 1;
        }

        .main-container {
            position: relative;
            z-index: 10; /* Above the overlay and butterflies */
            text-align: center;
            background: rgba(255, 255, 255, 0.1); /* Glassmorphism effect */
            backdrop-filter: blur(10px);
            padding: 50px;
            border-radius: 20px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            max-width: 600px;
            width: 80%;
        }

        h1 {
            font-family: 'Great Vibes', cursive;
            color: #ffb7c5; /* Soft pink */
            font-size: 3.5rem;
            margin-top: 0;
            text-shadow: 0 0 15px rgba(255, 183, 197, 0.7);
        }

        #message-display {
            font-size: 1.3rem;
            color: #fdfcfc; /* Off-white text */
            min-height: 100px;
            margin: 30px 0;
            line-height: 1.6;
            font-weight: 300;
        }

        /* The cursor for typewriter effect */
        .cursor {
            display: inline-block;
            width: 2px;
            background-color: #ffb7c5;
            margin-left: 2px;
            animation: blink 1s infinite;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }

        button {
            background-color: transparent;
            color: #ffb7c5;
            border: 2px solid #ffb7c5;
            padding: 12px 30px;
            font-family: 'Poppins', sans-serif;
            font-size: 1rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-weight: 600;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 20px;
        }

        button:hover {
            background-color: #ffb7c5;
            color: #333;
            box-shadow: 0 0 20px rgba(255, 183, 197, 0.6);
        }

        button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        /* Butterfly styling */
        .butterfly {
            position: fixed;
            z-index: 5; /* Above overlay, below main content */
            width: 40px;
            height: 40px;
            /* Pure off-white color */
            background-color: #f5f5f0; 
            /* Simple butterfly shape using clip-path */
            clip-path: polygon(50% 100%, 0% 50%, 50% 0%, 100% 50%);
            opacity: 0; /* Starts hidden for fade in */
            filter: drop-shadow(0 0 5px rgba(255,255,255,0.5));
            animation: fadeInButterfly 1s forwards ease-out, flutter 0.2s infinite alternate;
        }

        @keyframes fadeInButterfly {
            to { opacity: 0.8; } /* Keep them slightly translucent */
        }

        /* Subtle fluttering motion */
        @keyframes flutter {
            0% { transform: rotate3d(0, 1, 0, 0deg) scale(1); }
            100% { transform: rotate3d(0, 1, 0, 70deg) scale(0.95); }
        }
    </style>
</head>
<body>

    <div class="overlay"></div>

    <div id="butterfly-garden"></div>

    <div class="main-container">
        <h1>For Manya</h1>
        <div id="message-display">
            Tap the button, my love...
            <span class="cursor">&nbsp;</span>
        </div>
        <button onclick="revealLove()" id="action-btn">Tell me why</button>
    </div>

    <audio id="love-audio" loop>
        <source src="love-sound.mp3" type="audio/mpeg">
    </audio>

    <script>
        // Update these with deep, specific memories and feelings for goosebumps
        const reasons = [
            "I remember the exact moment I fell for you. It still plays in my head like a movie.",
            "You have this way of looking at me that makes the rest of the world completely disappear.",
            "I never knew what peace felt like until the first time I held you.",
            "Even when we are miles apart, you are the only thing on my mind.",
            "You aren't just my favorite person; you are my best friend and my greatest adventure.",
            "Every love song makes perfect sense now that I have you."
        ];

        let audioStarted = false;
        let isTyping = false;

        function revealLove() {
            if (isTyping) return; // Prevent clicking during typing

            // 1. Play "lovely sound" on first click
            if (!audioStarted) {
                const audio = document.getElementById('love-audio');
                audio.volume = 0.5; // Set volume to 50%
                audio.play().catch(error => {
                    console.log("Audio playback failed. Ensure 'love-sound.mp3' exists.");
                });
                audioStarted = true;
            }

            // 2. Start Typewriter effect immediately
            typeWriterEffect();

            // 3. Queue the off-white butterfly to appear after 1 second
            setTimeout(createButterfly, 1000);
        }

        function typeWriterEffect() {
            isTyping = true;
            const display = document.getElementById("message-display");
            const btn = document.getElementById("action-btn");
            
            // Clear existing text but keep the cursor
            display.innerHTML = '<span class="cursor">&nbsp;</span>';
            
            const randomIndex = Math.floor(Math.random() * reasons.length);
            const textToType = reasons[randomIndex];
            let i = 0;

            function type() {
                if (i < textToType.length) {
                    // Insert character before the cursor
                    const char = textToType.charAt(i);
                    display.innerHTML = textToType.substring(0, i + 1) + '<span class="cursor">&nbsp;</span>';
                    i++;
                    
                    // Variable speed for human-like typing effect (tension building)
                    const speed = Math.floor(Math.random() * 50) + 40; 
                    setTimeout(type, speed);
                } else {
                    isTyping = false;
                }
            }
            type();
        }

        function createButterfly() {
            const garden = document.getElementById('butterfly-garden');
            const butterfly = document.createElement('div');
            butterfly.className = 'butterfly';
            
            // Random positioning over the whole screen (using viewport units)
            const randomX = Math.random() * 95; // Keep 5vw away from edge
            const randomY = Math.random() * 95; // Keep 5vh away from edge
            
            butterfly.style.left = randomX + 'vw';
            butterfly.style.top = randomY + 'vh';
            
            // Random slight rotation so they don't all look the same
            const randomRotate = Math.random() * 360;
            butterfly.style.transform = `rotate(${randomRotate}deg)`;

            // Add to the screen - it will not remove itself
            garden.appendChild(butterfly);
        }
    </script>
</body>
</html>
