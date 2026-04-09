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
            transition: background 1s ease-in-out; /* Smooth background disappearance if needed */
        }

        /* Initial dark overlay to make text readable, which can fade later */
        .overlay {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0, 0, 0, 0.4); /* Adjust opacity here (0.4 = 40%) */
            z-index: 1;
            transition: opacity 1s ease-in-out; /* Smooth disappearance */
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
            transition: opacity 0.5s ease-in-out, visibility 0.5s ease-in-out; /* Smooth disappearance of initial content */
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
            position: relative; /* Ensure it stays above disappearing elements */
            z-index: 20; /* Keep it interactive on top of everything */
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
        .butterfly-container {
            position: fixed;
            z-index: 15; /* Above initial background and disappearing elements, below button */
            width: 40px; /* Adjust butterfly size here */
            height: 40px;
            filter: drop-shadow(0 0 5px rgba(255,255,255,0.5));
            opacity: 0; /* Starts hidden for fade in */
            animation: fadeInButterfly 1s forwards ease-out, flutter 0.2s infinite alternate;
        }

        /* Internal butterfly shape */
        .butterfly {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: #f5f5f0; /* Pure off-white color */
            /* Simple butterfly shape using clip-path */
            clip-path: polygon(50% 100%, 0% 50%, 50% 0%, 100% 50%);
        }

        /* Message text directly on the butterfly wings */
        .butterfly-message {
            position: absolute;
            top: 15%; left: 0; width: 100%; text-align: center;
            font-family: 'Great Vibes', cursive;
            color: #333; /* Dark legible color */
            font-size: 0.8rem; /* Small font size for butterfly messages */
            font-weight: 400;
            line-height: 1.2;
            word-break: break-all; /* Break long words on small space */
            padding: 0 3px;
        }

        @keyframes fadeInButterfly {
            to { opacity: 0.9; } /* Keep them slightly translucent */
        }

        /* Subtle fluttering motion */
        @keyframes flutter {
            0% { transform: rotate3d(0, 1, 0, 0deg) scale(1); }
            100% { transform: rotate3d(0, 1, 0, 70deg) scale(0.95); }
        }

        /* Hide the main container and background overlay if needed on click */
        .content-hidden {
            opacity: 0;
            visibility: hidden;
        }
    </style>
</head>
<body>

    <div class="overlay" id="background-overlay"></div>

    <div id="butterfly-garden"></div>

    <div class="main-container" id="initial-content">
        <h1>For Manya</h1>
        <div id="message-display">
            Tap the button, my love...
            <span class="cursor">&nbsp;</span>
        </div>
    </div>

    <button onclick="revealLove()" id="action-btn">Tell me why</button>

    <audio id="love-audio" loop>
        <source src="love-sound.mp3" type="audio/mpeg">
    </audio>

    <script>
        // Update these with short, distinct memories and feelings for each butterfly
        // Since user wants to write the code later, these are placeholders for now.
        const messages = [
            "You're my sunshine",
            "I love your laugh",
            "Thinking of you makes me smile",
            "You're beautiful!",
            "Every day is better with you",
            "Your kindness inspires me!",
            "Can't wait for our next adventure"
        ];
        let currentMessageIndex = 0; // Keep track of the message to use

        let audioStarted = false;
        let isTyping = false;

        function revealLove() {
            if (isTyping) return; // Prevent clicking during typing of main message

            // 1. Play "lovely sound" (the romantic song) on first click
            if (!audioStarted) {
                const audio = document.getElementById('love-audio');
                audio.volume = 0.5; // Set volume to 50%
                audio.play().catch(error => {
                    console.log("Audio playback failed. Ensure 'love-sound.mp3' exists and browser allows it.");
                });
                audioStarted = true;
                
                // 2. Make everything *except* the button disappear smoothly on first click
                document.getElementById('initial-content').classList.add('content-hidden');
                document.getElementById('background-overlay').classList.add('content-hidden');
                // The main rose background image stays
            }

            // 3. Immediately queue the new off-white butterfly to appear randomly after 1 second
            // and never disappear, containing the current message.
            setTimeout(createButterfly, 1000);
            
            // 4. Temporarily show current message in central area (or you could just update button text)
            // But user only asked for elements to *disappear* and butterflies to *appear with message*.
            // So, let's just make the central main message area fade away *after* the initial text disappears on first click,
            // or just make the text vanish, and the butterflies become the focus.
            // Let's go with just butterflies for subsequent clicks.
            // But user also requested "butterfly appears with text, but never dissappears... new butterfly appears with text".
            // So, for now, the subsequent clicks *only* add a butterfly with the *next* message.
            currentMessageIndex = (currentMessageIndex + 1) % messages.length; // Loop through messages
        }

        // Previous typewriter function is removed for subsequent clicks to follow the "only butterflies" requirement
        
        function createButterfly() {
            const garden = document.getElementById('butterfly-garden');
            const butterflyContainer = document.createElement('div');
            butterflyContainer.className = 'butterfly-container';
            
            // Random positioning over the whole screen (using viewport units)
            const randomX = Math.random() * 95; // Keep 5vw away from edge
            const randomY = Math.random() * 95; // Keep 5vh away from edge
            
            butterflyContainer.style.left = randomX + 'vw';
            butterflyContainer.style.top = randomY + 'vh';
            
            // Random slight rotation so they don't all look the same
            const randomRotate = Math.random() * 360;
            butterflyContainer.style.transform = `rotate(${randomRotate}deg)`;

            // Internal butterfly structure
            const butterflyShape = document.createElement('div');
            butterflyShape.className = 'butterfly';
            butterflyContainer.appendChild(butterflyShape);

            // Message text element
            const butterflyMessage = document.createElement('div');
            butterflyMessage.className = 'butterfly-message';
            // User specified short messages on each, likely to fit this design.
            // Placeholders used from messages array. User to edit later.
            butterflyMessage.innerText = messages[currentMessageIndex]; 
            butterflyContainer.appendChild(butterflyMessage);

            // Add to the screen - it will not remove itself
            garden.appendChild(butterflyContainer);
        }
    </script>
</body>
</html>
