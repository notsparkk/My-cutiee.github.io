<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Manya ❤️</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Great+Vibes&family=Poppins:wght@300;400;600&display=swap');

        body {
            margin: 0;
            padding: 0;
            height: 100vh;
            width: 100vw;
            /* Background Image */
            background-image: url('roses.jpg'); 
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            font-family: 'Poppins', sans-serif;
            overflow: hidden; 
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .overlay {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0, 0, 0, 0.6); /* Slightly darker to make white pop */
            z-index: 1;
        }

        .main-container {
            position: relative;
            z-index: 10; 
            text-align: center;
            background: rgba(255, 255, 255, 0.1); 
            backdrop-filter: blur(10px);
            padding: 50px;
            border-radius: 20px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 15px 35px rgba(0,0,0,0.3);
            max-width: 600px;
            width: 80%;
        }

        h1 {
            font-family: 'Great Vibes', cursive;
            color: #ffb7c5; 
            font-size: 3.5rem;
            margin-top: 0;
            text-shadow: 0 0 15px rgba(255, 183, 197, 0.7);
        }

        #message-display {
            font-size: 1.3rem;
            color: #fdfcfc; 
            min-height: 100px;
            margin: 30px 0;
            line-height: 1.6;
            font-weight: 300;
        }

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

        /* --- NEW BUTTERFLY STYLES --- */
        .butterfly-wrapper {
            position: absolute;
            z-index: 5; 
            display: flex;
            flex-direction: column;
            align-items: center;
            opacity: 0;
            pointer-events: none; /* So they don't block clicks on the button */
            animation: fadeInWrapper 1s forwards ease-out, floatAround 4s infinite alternate ease-in-out;
        }

        .butterfly-icon {
            /* Gives the wings a flapping effect */
            animation: flutter 0.15s infinite alternate linear;
            filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.8));
        }

        .butterfly-text {
            color: #ffffff;
            font-family: 'Poppins', sans-serif;
            font-size: 0.85rem;
            font-weight: 600;
            text-align: center;
            margin-top: 8px;
            max-width: 140px;
            /* Dark text shadow makes it readable over any part of the rose background */
            text-shadow: 0 2px 4px rgba(0,0,0,0.9), 0 0 10px rgba(0,0,0,0.7);
        }

        @keyframes fadeInWrapper {
            to { opacity: 1; } 
        }

        @keyframes flutter {
            0% { transform: scaleX(1); }
            100% { transform: scaleX(0.3); } /* Compresses width to look like flapping */
        }

        @keyframes floatAround {
            0% { transform: translateY(0px) rotate(0deg); }
            100% { transform: translateY(-20px) rotate(5deg); }
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
        // --- CENTRAL MESSAGES ---
        // These type out in the center of the screen
        const mainReasons = [
            "I remember the exact moment I fell for you. It still plays in my head like a movie.",
            "You have this way of looking at me that makes the rest of the world completely disappear.",
            "I never knew what peace felt like until the first time I held you.",
            "Even when we are miles apart, you are the only thing on my mind.",
            "You aren't just my favorite person; you are my best friend and my greatest adventure."
        ];

        // --- BUTTERFLY MESSAGES ---
        // ADD YOUR MESSAGES HERE. A random one will be picked for each new butterfly.
        const butterflyMessages = [
            "Your smile is my favorite.",
            "You are stunning.",
            "My beautiful Manya.",
            "I love your laugh.",
            "Forever and always.",
            "You are my peace.",
            "I adore you."
        ];

        let audioStarted = false;
        let isTyping = false;

        function revealLove() {
            if (isTyping) return; 

            // Play "A Thousand Years" on first click
            if (!audioStarted) {
                const audio = document.getElementById('love-audio');
                audio.volume = 0.5; 
                audio.play().catch(e => console.log("Ensure 'love-sound.mp3' is in the folder."));
                audioStarted = true;
            }

            // Start Typewriter effect for the main text
            typeWriterEffect();

            // Spawn the white butterfly and text 1 second (1000ms) later
            setTimeout(createButterflyWithText, 1000);
        }

        function typeWriterEffect() {
            isTyping = true;
            const display = document.getElementById("message-display");
            display.innerHTML = '<span class="cursor">&nbsp;</span>';
            
            const randomIndex = Math.floor(Math.random() * mainReasons.length);
            const textToType = mainReasons[randomIndex];
            let i = 0;

            function type() {
                if (i < textToType.length) {
                    display.innerHTML = textToType.substring(0, i + 1) + '<span class="cursor">&nbsp;</span>';
                    i++;
                    const speed = Math.floor(Math.random() * 50) + 40; 
                    setTimeout(type, speed);
                } else {
                    isTyping = false;
                }
            }
            type();
        }

        function createButterflyWithText() {
            const garden = document.getElementById('butterfly-garden');
            const wrapper = document.createElement('div');
            wrapper.className = 'butterfly-wrapper';
            
            // Random positioning over the screen (keeping it slightly away from the extreme edges)
            const randomX = Math.random() * 85 + 5; // 5vw to 90vw
            const randomY = Math.random() * 85 + 5; // 5vh to 90vh
            
            wrapper.style.left = randomX + 'vw';
            wrapper.style.top = randomY + 'vh';

            // Pick a random message for this butterfly
            const randomMsgIndex = Math.floor(Math.random() * butterflyMessages.length);
            const messageText = butterflyMessages[randomMsgIndex];
            
            // Create the Pure White SVG Butterfly and append the text below it
            wrapper.innerHTML = `
                <div class="butterfly-icon">
                    <svg fill="#ffffff" viewBox="0 0 64 64" width="40px" height="40px">
                       <path d="M62.2,23.1c-1.3-3.6-5.4-5-8.9-3.2c-5.8,2.9-14.1,8.3-21.3,14.9V14.1c0-4.4-3.6-8-8-8s-8,3.6-8,8v20.7c-7.2-6.5-15.5-12-21.3-14.9c-3.5-1.8-7.6-0.3-8.9,3.2c-1.3,3.5-0.1,7.6,2.8,10l12,9.8c-4.4,2.8-8,5.4-8.8,5.9c-3.1,2.4-4.2,6.7-2.6,10.2c1.6,3.6,5.8,5.3,9.7,3.9c0.9-0.3,4.7-1.7,9.6-3.8v7.2c0,4.4,3.6,8,8,8s8-3.6,8-8v-7.2c4.9,2.1,8.7,3.5,9.6,3.8c3.9,1.4,8.1-0.3,9.7-3.9c1.6-3.6,0.5-7.9-2.6-10.2c-0.8-0.6-4.3-3.1-8.8-5.9l12-9.8C62.3,30.7,63.4,26.6,62.2,23.1z"/>
                    </svg>
                </div>
                <div class="butterfly-text">${messageText}</div>
            `;

            // Add the new butterfly to the screen (it will never be removed)
            garden.appendChild(wrapper);
        }
    </script>
</body>
</html>
