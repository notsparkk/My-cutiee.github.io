<!DOCTYPE html>
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
            align-items: flex-end; /* Push button to bottom */
            justify-content: center;
            position: relative;
        }

        /* Ambient dark overlay to make text readable against the busy rose background */
        .overlay {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0, 0, 0, 0.4); /* Adjust opacity here */
            z-index: 1;
        }

        /* Fixed Title at the top */
        .page-title {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 10;
            text-align: center;
            width: 100%;
        }

        h1 {
            font-family: 'Great Vibes', cursive;
            color: #ffb7c5; /* Soft pink */
            font-size: 3.5rem;
            margin: 0;
            text-shadow: 0 0 15px rgba(255, 183, 197, 0.7);
        }

        /* Button styling - anchored at the bottom */
        button {
            background-color: transparent;
            color: #ffb7c5;
            border: 2px solid #ffb7c5;
            padding: 15px 40px;
            font-family: 'Poppins', sans-serif;
            font-size: 1.1rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-weight: 600;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 30px; /* Space from bottom edge */
            position: relative;
            z-index: 20; /* Keep it interactive on top of everything */
            backdrop-filter: blur(5px);
            background: rgba(0, 0, 0, 0.2);
        }

        button:hover {
            background-color: #ffb7c5;
            color: #333;
            box-shadow: 0 0 20px rgba(255, 183, 197, 0.6);
            transform: scale(1.05);
        }

        /* Butterfly Container for positioning and fluttering */
        .butterfly-container {
            position: fixed;
            z-index: 5; /* Below the title and button, above overlay */
            /* Set a safe, readable size relative to the screen */
            width: 300px; /* Butterfly width */
            height: 200px; /* Butterfly height */
            transform-origin: center;
            filter: drop-shadow(0 0 10px rgba(255,255,255,0.7));
            opacity: 0; /* Starts hidden for fade in */
            animation: fadeInButterfly 1s forwards ease-out, flutter 0.2s infinite alternate;
        }

        /* The actual SVG Butterfly Shape - Pure off-white color */
        .butterfly-shape {
            width: 100%;
            height: 100%;
            fill: #fdfcfc; /* Off-white color */
        }

        /* Message text area centered within the butterfly body */
        .butterfly-text-area {
            position: absolute;
            top: 25%; /* Adjust vertically within the butterfly body */
            left: 20%; /* Adjust horizontally within the butterfly body */
            width: 60%; /* Limit text width */
            height: 50%; /* Limit text height */
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            z-index: 6; /* On top of the shape */
        }

        .butterfly-message {
            font-family: 'Poppins', sans-serif; /* Clean font for full sentences */
            color: #333; /* Dark legible color */
            font-size: 1rem;
            font-weight: 400;
            line-height: 1.4;
            margin: 0;
            padding: 10px;
            word-wrap: break-word; /* Ensure full sentences break correctly */
        }

        @keyframes fadeInButterfly {
            to { opacity: 0.95; } /* Make them clear and distinct */
        }

        /* Subtle fluttering motion */
        @keyframes flutter {
            0% { transform: rotate3d(0, 1, 0, 0deg) scale(1) translateY(0px); }
            100% { transform: rotate3d(0, 1, 0, 50deg) scale(0.98) translateY(-5px); }
        }
    </style>
</head>
<body>

    <div class="overlay"></div>

    <div id="butterfly-garden"></div>

    <div class="page-title">
        <h1>For Manya ❤️</h1>
    </div>

    <button onclick="addButterfly()" id="action-btn">Tell me why</button>

    <audio id="love-audio" loop>
        <source src="love-sound.mp3" type="audio/mpeg">
    </audio>

    <script>
        // STEP C: Edit these messages later!
        // These are full romantic reasons that will appear inside the butterflies.
        const messages = [
            "Your smile is the most beautiful thing I have ever seen.",
            "I love the way you laugh; it sounds like my favorite song.",
            "You make every single day feel like a dream come true.",
            "You aren't just my partner; you are my best friend.",
            "I fall more in love with you every time you look at me.",
            "You have shown me what unconditional love truly looks like.",
            "My favorite place in the world is right by your side.",
            "You are the strongest and most inspiring person I know.",
            "Every love song makes perfect sense now that I have you."
        ];
        
        let messageIndex = 0; // Keep track of the message to use
        let audioStarted = false;

        function addButterfly() {
            // 1. Play "lovely sound" (the romantic song) on first click
            if (!audioStarted) {
                const audio = document.getElementById('love-audio');
                audio.volume = 0.5; // Set volume to 50%
                audio.play().catch(error => {
                    console.log("Audio playback failed. Ensure 'love-sound.mp3' exists in the folder.");
                });
                audioStarted = true;
            }

            // 2. Create the unique butterfly with the message
            createButterflyWithMessage(messages[messageIndex]);
            
            // 3. Increment the message index and loop if we run out
            messageIndex = (messageIndex + 1) % messages.length;
        }

        function createButterflyWithMessage(messageContent) {
            const garden = document.getElementById('butterfly-garden');
            const butterflyContainer = document.createElement('div');
            butterflyContainer.className = 'butterfly-container';
            
            // Random positioning over the whole screen (using viewport units)
            // Ensure they don't appear over the title or button.
            const randomX = Math.random() * 70 + 5; // Horizontal safe zone (5vw to 75vw)
            const randomY = Math.random() * 60 + 10; // Vertical safe zone (10vh to 70vh)
            
            butterflyContainer.style.left = randomX + 'vw';
            butterflyContainer.style.top = randomY + 'vh';
            
            // Random slight rotation for an organic feel
            const randomRotate = (Math.random() * 40) - 20; // Rotate between -20 and +20 degrees
            
            // Base transform includes rotation. The animation adds the flutter on top.
            butterflyContainer.style.transform = `rotate(${randomRotate}deg)`;

            // --- Constructing the Butterfly with SVG ---
            // Simple butterfly SVG (two wings and a body)
            const butterflySVG = `
                <svg viewBox="0 0 100 80" class="butterfly-shape">
                    <path d="M 50 40 Q 10 10, 10 40 Q 10 70, 50 40 Z"/>
                    <path d="M 50 40 Q 90 10, 90 40 Q 90 70, 50 40 Z"/>
                    <ellipse cx="50" cy="40" rx="3" ry="10" fill="#333"/>
                    <circle cx="50" cy="28" r="3" fill="#333"/>
                </svg>
            `;
            butterflyContainer.innerHTML = butterflySVG;

            // --- Adding the Message Text ---
            const textArea = document.createElement('div');
            textArea.className = 'butterfly-text-area';
            
            const messageElement = document.createElement('p');
            messageElement.className = 'butterfly-message';
            messageElement.innerText = messageContent; 
            textArea.appendChild(messageElement);

            butterflyContainer.appendChild(textArea);

            // Add to the screen - it will not remove itself
            garden.appendChild(butterflyContainer);
        }
    </script>
</body>
</html>
