<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic Animations from Kitale</title>
    <style>
        body {
            font-family: sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 20px;
            padding: 20px;
            background-color: #f4f4f4;
        }

        .animated-button {
            background-color: #4CAF50; /* Green like the lush fields around Kitale */
            color: white;
            padding: 15px 32px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease-in-out, transform 0.2s ease-in-out;
        }

        .animated-button:hover {
            background-color: #45a049;
            transform: scale(1.05);
        }

        .animated-image-container {
            width: 200px;
            height: 200px;
            overflow: hidden;
        }

        .animated-image {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease-in-out;
        }

        .animated-image.zoomed {
            transform: scale(1.2);
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        .pulsing-element {
            width: 100px;
            height: 100px;
            background-color: orange; /* Bright like the Kitale sun */
            border-radius: 50%;
            animation: pulse 1s infinite alternate;
        }
    </style>
</head>
<body>
    <h1>Dynamic Animations from Kitale</h1>

    <button id="myButton" class="animated-button">Click Me to Animate</button>

    <div class="animated-image-container">
        <img id="myImage" class="animated-image" src="https://via.placeholder.com/200/87CEEB/FFFFFF?Text=Kitale%20View" alt="A view of Kitale">
    </div>
    <button id="zoomButton" class="animated-button">Zoom Image</button>

    <div class="pulsing-element"></div>

    <script>
        function storePreference(key, value) {
            try {
                localStorage.setItem(key, JSON.stringify(value));
                console.log(`Preference stored: ${key} - ${value}`);
            } catch (error) {
                console.error("Error storing preference:", error);
            }
        }

        function getPreference(key) {
            try {
                const storedValue = localStorage.getItem(key);
                return storedValue ? JSON.parse(storedValue) : null;
            } catch (error) {
                console.error("Error retrieving preference:", error);
                return null;
            }
        }

        function triggerButtonAnimation() {
            const button = document.getElementById('myButton');
            button.classList.add('animated-button-click');
            setTimeout(() => {
                button.classList.remove('animated-button-click');
            }, 300); // Duration of the "click" effect

            // Store user's interaction preference
            storePreference('lastButtonClicked', new Date().toISOString());
        }

        function triggerImageZoom() {
            const image = document.getElementById('myImage');
            image.classList.toggle('zoomed');

            // Store user's zoom preference
            const isZoomed = image.classList.contains('zoomed');
            storePreference('imageZoomed', isZoomed);
        }

        // Apply stored image zoom preference on load
        document.addEventListener('DOMContentLoaded', () => {
            const zoomedPreference = getPreference('imageZoomed');
            const image = document.getElementById('myImage');
            if (zoomedPreference) {
                image.classList.add('zoomed');
            }
            console.log("Last button click:", getPreference('lastButtonClicked'));
        });

        // Event listeners to trigger animations
        document.getElementById('myButton').addEventListener('click', triggerButtonAnimation);
        document.getElementById('zoomButton').addEventListener('click', triggerImageZoom);

        // CSS for the dynamic button click animation
        const style = document.createElement('style');
        style.textContent = `
            .animated-button-click {
                animation: buttonClick 0.3s ease-in-out;
            }

            @keyframes buttonClick {
                0% { transform: scale(1); }
                50% { transform: scale(0.9); }
                100% { transform: scale(1); }
            }
        `;
        document.head.appendChild(style);
    </script>
</body>
</html>
