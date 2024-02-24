<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Spin the Wheel</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }
  .container {
    max-width: 600px;
    background-color: #f0f0f0;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    text-align: center;
  }
  #wheel {
    width: 300px;
    height: 300px;
    background-color: #f9c74f;
    border-radius: 50%;
    position: relative;
    margin: 20px auto;
    border: 10px solid #f4a261;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
    overflow: hidden;
  }
  #pointer {
    width: 0;
    height: 0;
    border-left: 15px solid transparent;
    border-right: 15px solid transparent;
    border-bottom: 20px solid #e63946;
    position: absolute;
    top: 30px;
    left: 50%;
    transform: translateX(-50%);
  }
  #spinBtn {
    margin-top: 20px;
    padding: 15px 30px;
    font-size: 20px;
    cursor: pointer;
    background-color: #a8dadc;
    border: none;
    color: #fff;
    border-radius: 5px;
    transition: background-color 0.3s;
  }
  #spinBtn:hover {
    background-color: #457b9d;
  }
  .confetti {
    width: 10px;
    height: 10px;
    position: absolute;
    top: 0;
    left: 0;
    animation: fall 3s ease-out infinite;
    opacity: 0;
  }
  @keyframes fall {
    0% { transform: translateY(-100px) rotate(0deg); opacity: 0; }
    20% { opacity: 1; }
    80% { opacity: 1; }
    100% { transform: translateY(500px) rotate(720deg); opacity: 0; }
  }
</style>
</head>
<body>

<div class="container">
  <h1 style="color: #2a9d8f;">Spin the Wheel</h1>
  <div id="wheel">
    <div id="pointer"></div>
    <div id="confettiContainer"></div>
  </div>
  <button id="spinBtn">Spin</button>
  <br>
  <label for="nameInput">Enter your name:</label>
  <input type="text" id="nameInput">
</div>

<script>
  const sectors = [
    { name: "50 Points", value: 50 },
    { name: "30 Points", value: 30 },
    { name: "20 Points", value: 20 },
    { name: "10 Points", value: 10 },
    { name: "5 Points", value: 5 },
    { name: "2 Points", value: 2 }
  ];

  const colors = ['#ffcc00', '#ff69b4', '#00bfff', '#ff4500', '#32cd32', '#9400d3'];

  const wheel = document.getElementById('wheel');
  const pointer = document.getElementById('pointer');
  const spinBtn = document.getElementById('spinBtn');
  const confettiContainer = document.getElementById('confettiContainer');
  const nameInput = document.getElementById('nameInput');

  const spinDuration = 5000; // in milliseconds
  let spinning = false;

  spinBtn.addEventListener('click', spinWheel);

  function spinWheel() {
    if (spinning) return;
    spinning = true;

    const randomDegree = Math.floor(Math.random() * 360);
    const rotation = 3600 + randomDegree;

    wheel.style.transition = `transform ${spinDuration / 1000}s ease-out`;
    wheel.style.transform = `rotate(${rotation}deg)`;

    setTimeout(() => {
      const deg = rotation % 360;
      let sectorIndex = Math.floor(deg / (360 / sectors.length));
      const result = sectors[sectorIndex];

      alert(`Congratulations, ${nameInput.value}! You won ${result.name}!`);

      // Store name locally
      localStorage.setItem('playerName', nameInput.value);

      // Create confetti
      for (let i = 0; i < 50; i++) {
        const confetti = document.createElement('div');
        confetti.classList.add('confetti');
        confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
        confetti.style.left = Math.random() * 100 + '%';
        confetti.style.animationDelay = Math.random() * 3 + 's';
        confettiContainer.appendChild(confetti);
      }

      // Stop confetti after 3 seconds
      setTimeout(() => {
        confettiContainer.innerHTML = '';
      }, 3000);

      spinning = false;
    }, spinDuration);
  }

  // Retrieve name from localStorage if available
  const storedName = localStorage.getItem('playerName');
  if (storedName) {
    nameInput.value = storedName;
  }
</script>

</body>
</html>
