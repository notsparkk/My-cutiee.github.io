<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Manya ❤️</title>
    <style>
        /* Immersive, romantic Google Fonts */
        @import url('https://fonts.googleapis.com/css2?family=Great+Vibes&family=Poppins:wght@300;400;600&display=swap');

        body {
            margin: 0;
            padding: 0;
            height: 100vh;
            width: 100vw;
            background-image: url('roses.jpg'); 
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            font-family: 'Poppins', sans-serif;
            overflow: hidden; 
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        /* Dark overlay to make the white butterflies pop */
        .overlay {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0, 0, 0, 0.65); 
            z-index: 1;
        }

        /* Center title and button */
        .main-container {
            position: relative;
            z-index: 20; 
            text-align: center;
            background: rgba(0, 0, 0, 0.3); 
            backdrop-filter: blur(8px);
            padding: 40px;
            border-radius: 20px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 15px 35px rgba(0,0,0,0.3);
        }

        h1 {
            font-family: 'Great Vibes', cursive;
            color: #ffffff;
            font-size: 4rem;
            margin: 0 0 20px 0;
            text-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
            letter-spacing: 2px;
        }

        button {
            background-color: transparent;
            color: #ffffff;
            border: 2px solid #ffffff;
            padding: 12px 35px;
            font-family: 'Poppins', sans-serif;
            font-size: 1.1rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-weight: 600;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.2);
        }

        button:hover {
            background-color: #ffffff;
            color: #1a1a1a;
            box-shadow: 0 0 25px rgba(255, 255, 255, 0.8);
            transform: scale(1.05);
        }

        /* Butterfly Garden (holds all the generated messages) */
        #butterfly-garden {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 10;
            pointer-events: none; /* Allows her to click the main button through the garden */
        }

        /* Individual Butterfly + Text Wrapper */
        .butterfly-message {
            position: absolute;
            display: flex;
            align-items: center;
            gap: 15px;
            max-width: 350px;
            opacity: 0;
            transform: translateY(20px);
            animation: floatIn 1s forwards ease-out;
        }

        @keyframes floatIn {
            to { 
                opacity: 1; 
                transform: translateY(0); 
            }
        }

        /* Pure CSS White Glowing Butterfly */
        .butterfly {
            position: relative;
            width: 24px;
            height: 24px;
            flex-shrink: 0;
            filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.9));
        }

        .butterfly::before, .butterfly::after {
            content: '';
            position: absolute;
            background: #ffffff;
            width: 12px;
            height: 24px;
            border-radius: 50% 50% 0 50%;
            animation: flapLeft 0.15s infinite alternate ease-in-out;
            transform-origin: right center;
        }

        .butterfly::after {
            left: 12px;
            border-radius: 50% 50% 50% 0;
            animation: flapRight 0.15s infinite alternate ease-in-out;
            transform-origin: left center;
        }

        @keyframes flapLeft {
            0% { transform: scaleX(1); }
            100% { transform: scaleX(0.2); }
        }

        @keyframes flapRight {
            0% { transform: scaleX(1); }
            100% { transform: scaleX(0.2); }
        }

        /* The message attached to the butterfly */
        .message-text {
            color: #ffffff;
            font-size: 1.1rem;
            font-weight: 300;
            font-style: italic;
            line-height: 1.5;
            text-shadow: 2px 2px 5px rgba(0,0,0,0.9), 0 0 8px rgba(255,255,255,0.3);
            background: rgba(0, 0, 0, 0.4);
            padding: 12px 18px;
            border-radius: 12px;
            border-left: 2px solid #ffffff;
            backdrop-filter: blur(4px);
        }
    </style>
</head>
<body>

    <div class="overlay"></div>

    <div id="butterfly-garden"></div>

    <div class="main-container">
        <h1>For Manya</h1>
        <button onclick="triggerButterfly()" id="action-btn">Tell me why</button>
    </div>

    <audio id="love-audio" loop>
        <source src="love-sound.mp3" type="audio/mpeg">
    </audio>

    <script>
        // Fill this array with all your beautiful, specific memories
        const reasons = [
            "I remember the exact moment I fell for you. It plays in my head like a movie.",
            "You have this way of looking at me that makes the world disappear.",
            "I never knew what true peace felt like until the first time I held you.",
            "Even when we are miles apart, you are the only thing on my mind.",
            "You aren't just my favorite person; you are my best friend.",
            "Every love song makes perfect sense now that I have you.",
            "Your laugh is my absolute favorite sound in the entire world.",
            "I love the way you light up when you talk about things you love."
        ];

        let audioStarted = false;
        let availableReasons = [...reasons]; // Copies the array so we can avoid repeating messages right away

        function triggerButterfly() {
            // 1. Play music on the very first click
            if (!audioStarted) {
                const audio = document.getElementById('love-audio');
                audio.volume = 0.5;
                audio.play().catch(e => console.log("Ensure 'love-sound.mp3' exists."));
                audioStarted = true;
                
                // Change button text after first click
                document.getElementById('action-btn').innerText = "Another Reason";
            }

            // 2. Wait exactly 1 second, then spawn the butterfly
            setTimeout(spawnButterflyWithMessage, 1000);
        }

        function spawnButterflyWithMessage() {
            const garden = document.getElementById('butterfly-garden');
            
            // Pick a random reason
            if (availableReasons.length === 0) {
                availableReasons = [...reasons]; // Reset if she clicks through all of them
            }
            const randomIndex = Math.floor(Math.random() * availableReasons.length);
            const selectedText = availableReasons[randomIndex];
            
            // Remove the used reason so it doesn't repeat immediately
            availableReasons.splice(randomIndex, 1);

            // Create the wrapper
            const wrapper = document.createElement('div');
            wrapper.className = 'butterfly-message';
            
            // Create the CSS butterfly
            const butterfly = document.createElement('div');
            butterfly.className = 'butterfly';

            // Create the text bubble
            const textBubble = document.createElement('div');
            textBubble.className = 'message-text';
            textBubble.innerText = selectedText;

            // Put them together
            wrapper.appendChild(butterfly);
            wrapper.appendChild(textBubble);

            // Calculate random positions (Keeps them mostly within the screen bounds)
            // 5 to 70 allows room for the text to stretch out without going off-screen
            const randomX = Math.floor(Math.random() * 65) + 5; 
            const randomY = Math.floor(Math.random() * 85) + 5; 

            wrapper.style.left = randomX + 'vw';
            wrapper.style.top = randomY + 'vh';

            // Random slight rotation for the whole message so it looks organic
            const randomRotate = (Math.random() * 10) - 5; // Rotates between -5 and 5 degrees
            wrapper.style.transform = `translateY(20px) rotate(${randomRotate}deg)`;

            // Add it to the page permanently
            garden.appendChild(wrapper);
        }
    </script>
</body>
</html>
