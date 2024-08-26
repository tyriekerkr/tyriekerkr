<!DOCTYPE html>  
    <html lang="en">  
    <head>  
        <meta charset="UTF-8">  
        <meta name="viewport" content="width=device-width, initial-scale=1.0">  
        <title>Xylophone</title>  
        <script src="https://cdn.tailwindcss.com"></script>  
        <style>  
            .key {  
                width: 60px;  
                height: 200px;  
                display: inline-block;  
                margin: 5px;  
                border-radius: 10px;  
                cursor: pointer;  
                transition: transform 0.1s;  
            }  
            .key:active {  
                transform: scale(0.95);  
            }  
        </style>  
    </head>  
    <body class="flex justify-center items-center h-screen bg-gray-100">  
        <div id="xylophone" class="flex">  
            <div class="key bg-red-500" data-frequency="261.63"></div>  
            <div class="key bg-orange-500" data-frequency="293.66"></div>  
            <div class="key bg-yellow-500" data-frequency="329.63"></div>  
            <div class="key bg-green-500" data-frequency="349.23"></div>  
            <div class="key bg-blue-500" data-frequency="392.00"></div>  
            <div class="key bg-indigo-500" data-frequency="440.00"></div>  
            <div class="key bg-purple-500" data-frequency="493.88"></div>  
        </div>  
        <div class="text-center mt-4">  
            <p class="text-lg">Click on the colorful keys to play sounds!</p>  
        </div>  
        <script>  
            const keys = document.querySelectorAll('.key');  

            keys.forEach(key => {  
                key.addEventListener('click', () => {  
                    const frequency = key.getAttribute('data-frequency');  
                    playSound(frequency);  
                });  
            });  

            function playSound(frequency) {  
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();  
                const oscillator = audioContext.createOscillator();  
                oscillator.type = 'sine';  
                oscillator.frequency.setValueAtTime(frequency, audioContext.currentTime);  
                oscillator.connect(audioContext.destination);  
                oscillator.start();  
                oscillator.stop(audioContext.currentTime + 0.5);  
            }  
        </script>  
    </body>  
    </html>  
