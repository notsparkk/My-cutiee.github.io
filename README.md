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
            /* Your Pink Rose Background */
            background-image: url('roses.jpg'); 
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            font-family: 'Poppins', sans-serif;
            overflow: hidden; 
            display: flex;
            align-items: flex-end; /* Push button to bottom */
            justify-content: center;
            position: relative;
        }

        /* Ambient dark overlay to make text readable */
        .overlay {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0, 0, 0, 0.5); /* Slightly darker for better contrast with white butterflies */
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
            color: #ffb7c5; 
            font-size: 3.5rem;
            margin: 0;
            text-shadow: 0 0 15px rgba(255, 183, 197, 0.7);
        }

        /* Button styling */
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
            transition: all 0.4s ease;
            margin-bottom: 30px; 
            position: relative;
            z-index: 20; 
            backdrop-filter: blur(5px);
            background: rgba(0, 0, 0, 0.2);
            box-shadow: 0 0 15px rgba(255, 183, 197, 0.3);
        }

        button:hover {
            background-color: #ffb7c5;
            color: #222;
            box-shadow: 0 0 25px rgba(255, 183, 197, 0.8);
            transform: scale(1.05);
        }

        /* Butterfly Container */
        .butterfly-container {
            position: fixed;
            z-index: 5; 
            width: 380px; /* Larger, more magnificent size */
            height: 280px; 
            transform-origin: center;
            filter: drop-shadow(0 10px 20px rgba(0,0,0,0.5)); /* Deep shadow for 3D effect */
            opacity: 0; 
            /* Only fading in, perfectly stationary */
            animation: fadeInButterfly 1.5s forwards ease-out;
            transition: transform 0.3s ease;
        }

        /* A subtle hover effect so they feel interactive but stationary */
        .butterfly-container:hover {
            transform: scale(1.02) !important; /* Overrides the inline inline transform slightly */
            z-index: 15; /* Brings hovered butterfly to the front */
        }

        .butterfly-shape {
            width: 100%;
            height: 100%;
        }

        /* Message text area inside the upper/middle wings */
        .butterfly-text-area {
            position: absolute;
            top: 15%; 
            left: 15%; 
            width: 70%; 
            height: 50%; 
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            z-index: 6; 
        }

        .butterfly-message {
            font-family: 'Poppins', sans-serif; 
            color: #1a1a1a; /* Very dark grey for beautiful contrast */
            font-size: 1.05rem;
            font-weight: 500;
            line-height: 1.5;
            margin: 0;
            padding: 10px;
            word-wrap: break-word; 
            text-shadow: 0 0 5px rgba(255, 255, 255, 0.8); /* Helps legibility over the wing details */
        }

        @keyframes fadeInButterfly {
            0% { opacity: 0; transform: scale(0.8) translateY(20px); }
            100% { opacity: 1; transform: scale(1) translateY(0); }
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
        
        let messageIndex = 0; 
        let audioStarted = false;

        function addButterfly() {
            if (!audioStarted) {
                const audio = document.getElementById('love-audio');
                audio.volume = 0.5; 
                audio.play().catch(error => console.log("Audio playback failed."));
                audioStarted = true;
            }

            createButterflyWithMessage(messages[messageIndex]);
            messageIndex = (messageIndex + 1) % messages.length;
        }

        function createButterflyWithMessage(messageContent) {
            const garden = document.getElementById('butterfly-garden');
            const butterflyContainer = document.createElement('div');
            butterflyContainer.className = 'butterfly-container';
            
            // Random positioning 
            const randomX = Math.random() * 65 + 5; 
            const randomY = Math.random() * 55 + 10; 
            
            butterflyContainer.style.left = randomX + 'vw';
            butterflyContainer.style.top = randomY + 'vh';
            
            // Set an initial rotation. We use a CSS variable to keep it stationary but rotated.
            const randomRotate = (Math.random() * 30) - 15; 
            butterflyContainer.style.transform = `rotate(${randomRotate}deg)`;

            // --- Magnificent Layered SVG Butterfly ---
            const butterflySVG = `
                <svg viewBox="0 0 200 150" class="butterfly-shape">
                    <defs>
                        <filter id="glow" x="-20%" y="-20%" width="140%" height="140%">
                            <feGaussianBlur stdDeviation="3" result="blur" />
                            <feComposite in="SourceGraphic" in2="blur" operator="over" />
                        </filter>
                    </defs>
                    
                    <path d="M 100 20 C 60 -20, 0 10, 15 60 C 25 90, 40 110, 45 140 C 55 120, 70 100, 100 80 Z" fill="#fdfcfc" opacity="0.95" filter="url(#glow)"/>
                    <path d="M 100 20 C 70 0, 20 20, 30 60 C 40 90, 55 105, 60 120 C 70 105, 80 90, 100 80 Z" fill="#ffffff" opacity="0.7"/>
                    
                    <path d="M 100 20 C 140 -20, 200 10, 185 60 C 175 90, 160 110, 155 140 C 145 120, 130 100, 100 80 Z" fill="#fdfcfc" opacity="0.95" filter="url(#glow)"/>
                    <path d="M 100 20 C 130 0, 180 20, 170 60 C 160 90, 145 105, 140 120 C 130 105, 120 90, 100 80 Z" fill="#ffffff" opacity="0.7"/>
                    
                    <ellipse cx="100" cy="50" rx="2.5" ry="18" fill="#222"/>
                    <circle cx="100" cy="28" r="3.5" fill="#222"/>
                    
                    <path d="M 98 28 Q 85 10 90 5" stroke="#222" stroke-width="1.5" fill="none"/>
                    <path d="M 102 28 Q 115 10 110 5" stroke="#222" stroke-width="1.5" fill="none"/>
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

            // Add to the screen 
            garden.appendChild(butterflyContainer);
        }
    </script>
</body>
</html>
