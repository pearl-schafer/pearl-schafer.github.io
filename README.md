# pearl-schafer.github.io

[WeAreLittleCreatures.html](https://github.com/user-attachments/files/25452705/WeAreLittleCreatures.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WE ARE LITTLE CREATURES</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: black;
            font-family: Arial, sans-serif;
            font-weight: bold;
            text-align: center;
        }

        #welcomeText {
            font-size: 2rem;
            line-height: 1.5;
            transition: color 0.3s ease;
            cursor: pointer;
            z-index: 3;
        }

        #welcomeText:hover {
            color: rgb(197, 0, 0);
        }

        img.abstractGif, img.animalGif {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            opacity: 0;
            transition: opacity 1s ease;
            cursor: pointer;
        }

        img.animalGif {
            z-index: 2;
        }
    </style>
</head>
<body>
    <div id="welcomeText">
        WE ARE LITTLE CREATURES
    </div>
    <img id="abstractGif1" class="abstractGif" alt="Abstract GIF">
    <img id="abstractGif2" class="abstractGif" alt="Abstract GIF">

    <script>
        const abstractsPath = 'Abstracts/';
        const animalsPath = 'Animals/';

        const abstractsGifs = ['1.gif', '2.gif', '3.gif', '4.gif', '5.gif', '6.gif', '7.gif', '8.gif'];
        const animalsGifs = Array.from({ length: 66 }, (_, i) => `${i + 1}.gif`);

        const abstractGifElement1 = document.getElementById('abstractGif1');
        const abstractGifElement2 = document.getElementById('abstractGif2');
        const welcomeTextElement = document.getElementById('welcomeText');

        let currentAbstractIndex = 0;
        let currentAbstractElement = abstractGifElement1;

        // Helper to get a random gif
        const getRandomGif = (gifs, path) => {
            const randomGif = gifs[Math.floor(Math.random() * gifs.length)];
            return `${path}${randomGif}`;
        };

        // Cycle Abstract GIFs with crossfade transition and overlap
        const cycleAbstractsGifs = () => {
            const nextAbstractIndex = (currentAbstractIndex + 1) % abstractsGifs.length;
            const nextAbstractGif = `${abstractsPath}${abstractsGifs[nextAbstractIndex]}`;

            // Get the next abstract GIF element to fade in
            const nextAbstractElement = currentAbstractElement === abstractGifElement1 ? abstractGifElement2 : abstractGifElement1;
            nextAbstractElement.src = nextAbstractGif;

            // Fade out current GIF element and fade in next GIF element
            currentAbstractElement.style.opacity = '0';
            nextAbstractElement.style.opacity = '1';

            // Update current abstract element and index
            currentAbstractElement = nextAbstractElement;
            currentAbstractIndex = nextAbstractIndex;

            // Ensure smooth, continuous cycling with no pause (5 seconds per GIF)
            setTimeout(cycleAbstractsGifs, 5000); // 5 seconds for each slide, no pause
        };

        // Display and fade-in a random Animal GIF
        const displayRandomAnimalGif = () => {
            const gif = getRandomGif(animalsGifs, animalsPath);
            const animalGifElement = document.createElement('img');
            animalGifElement.src = gif;
            animalGifElement.classList.add('animalGif');
            document.body.appendChild(animalGifElement);

            // Trigger fade-in
            requestAnimationFrame(() => {
                animalGifElement.style.opacity = '1';
            });

            // Fade-out and remove after display
            setTimeout(() => {
                animalGifElement.style.opacity = '0';
                animalGifElement.addEventListener('transitionend', () => {
                    animalGifElement.remove();
                });
            }, 5000); // Display duration (5 seconds)
        };

        // Start Abstract GIF cycling on first click
        welcomeTextElement.addEventListener('click', () => {
            welcomeTextElement.style.display = 'none';
            abstractGifElement1.style.display = 'block';
            abstractGifElement2.style.display = 'block';
            cycleAbstractsGifs();
        });

        // Show Animal GIF on body click (after welcome screen is hidden)
        document.body.addEventListener('click', (event) => {
            if (welcomeTextElement.style.display === 'none') {
                displayRandomAnimalGif();
            }
        });
    </script>
</body>
</html>
