<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Fast Phasing with Flash Effect</title>
  <style>
    body {
      background-color: black;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      overflow: hidden;
      font-family: 'Creepster', cursive; /* Creepy font */
    }

    /* Welcome Text */
    .welcome-text {
      color: white;
      font-size: 60px;
      letter-spacing: 5px;
      text-transform: uppercase;
      text-align: center;
      z-index: 10;
      display: none;
    }

    /* Input Form Styling */
    .name-form {
      position: absolute;
      text-align: center;
      color: white;
      font-size: 30px;
    }

    input {
      font-size: 20px;
      padding: 10px;
      margin: 20px;
      width: 200px;
      border: none;
      border-radius: 5px;
      outline: none;
    }

    button {
      font-size: 20px;
      padding: 10px 20px;
      background-color: #333;
      color: white;
      border: none;
      cursor: pointer;
      border-radius: 5px;
    }

    button:hover {
      background-color: #555;
    }

    .image-container {
      position: relative;
      width: 60%;
      height: 80%;
      display: none; /* Hidden initially */
    }

    .image {
      position: absolute;
      width: 100%;
      height: 100%;
      object-fit: cover;
      opacity: 0;
      transition: opacity 0.5s ease;
    }

    /* Flash animation for background */
    @keyframes flash {
      0% {
        background-color: black;
      }
      50% {
        background-color: white;
      }
      100% {
        background-color: black;
      }
    }

    /* Spooky sound */
    #sound {
      display: none;
    }
  </style>
  <link href="https://fonts.googleapis.com/css2?family=Creepster&display=swap" rel="stylesheet"> <!-- Creepy font -->
</head>
<body>

  <!-- Name Input Form -->
  <div class="name-form">
    <p>Enter your name:</p>
    <input type="text" id="nameInput" placeholder="Your name here" />
    <button onclick="startGame()">Submit</button>
  </div>

  <!-- Welcome message -->
  <div class="welcome-text" id="welcomeText">WELCOME TO THE GAME</div>

  <div class="image-container" id="imageContainer">
    <img src="https://rukminim2.flixcart.com/image/720/864/xif0q/mask/h/9/l/free-size-realistic-ghost-horror-face-mask-full-head-party-mask-original-imaghctknhpcpj8y.jpeg?q=60&crop=false" class="image" id="img1">
    <img src="https://ae01.alicdn.com/kf/Sdfb1a4bc5586446ba80529a97a8152706.jpg_640x640q90.jpg" class="image" id="img2">
    <img src="https://i.redd.it/cd9zpvayqdfb1.jpg" class="image" id="img3">
    <img src="https://pics.craiyon.com/2023-07-09/db76187d2772440d8b6362aad3d98fe1.webp" class="image" id="img4">
  </div>

  <!-- Spooky sound -->
  <audio id="sound" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" preload="auto"></audio>

  <script>
    // Start game when the user submits their name
    function startGame() {
      const name = document.getElementById('nameInput').value;
      if (name.trim() === "") {
        alert("Please enter a name.");
        return;
      }
      
      // Hide the name input form
      document.querySelector('.name-form').style.display = 'none';
      
      // Show the welcome text
      const welcomeText = document.getElementById('welcomeText');
      welcomeText.style.display = 'block';

      // Play spooky sound
      const sound = document.getElementById('sound');
      sound.play();

      // Display images after a slight delay
      setTimeout(() => {
        document.getElementById('imageContainer').style.display = 'block';
        startImagePhase();
      }, 1000); // Show images after 1 second delay

      // Start flashing effect
      document.body.style.animation = 'flash 0.3s infinite';
    }

    // Phasing images function
    const images = document.querySelectorAll('.image');
    let currentImageIndex = 0;

    function startImagePhase() {
      // Make the current image fade out
      images[currentImageIndex].style.opacity = '0';

      // Get the next image to show
      currentImageIndex = (currentImageIndex + 1) % images.length;

      // Make the next image fade in
      images[currentImageIndex].style.opacity = '1';
      
      // Repeat phasing images every 500ms
      setInterval(() => {
        images[currentImageIndex].style.opacity = '0';
        currentImageIndex = (currentImageIndex + 1) % images.length;
        images[currentImageIndex].style.opacity = '1';
      }, 500);
    }
  </script>

</body>
</html>
