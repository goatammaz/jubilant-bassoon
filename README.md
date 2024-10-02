<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Online Camera Test</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #f0f0f0;
        }
        h1 {
            margin-bottom: 20px;
        }
        video {
            border: 2px solid #28a745;
            border-radius: 10px;
            width: 90%;
            max-width: 600px;
            height: auto;
        }
        button {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 18px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>

<h1>Online Camera Test</h1>
<video id="video" autoplay playsinline></video>
<button id="startButton">Start Camera</button>
<button id="stopButton" style="display: none;">Stop Camera</button>

<script>
    const video = document.getElementById('video');
    const startButton = document.getElementById('startButton');
    const stopButton = document.getElementById('stopButton');
    let stream;

    startButton.addEventListener('click', async () => {
        try {
            stream = await navigator.mediaDevices.getUserMedia({ video: true });
            video.srcObject = stream;
            startButton.style.display = 'none';
            stopButton.style.display = 'inline';
        } catch (error) {
            console.error("Error accessing the camera: ", error);
        }
    });

    stopButton.addEventListener('click', () => {
        if (stream) {
            const tracks = stream.getTracks();
            tracks.forEach(track => track.stop());
            video.srcObject = null;
            startButton.style.display = 'inline';
            stopButton.style.display = 'none';
        }
    });
</script>

</body>
</html>
