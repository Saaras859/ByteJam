<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Spin the Wheel</title>
<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
  }
  #wheel {
    width: 300px;
    height: 300px;
    background-color: #f2f2f2;
    border-radius: 50%;
    position: relative;
    margin: 20px auto;
  }
  #pointer {
    width: 0;
    height: 0;
    border-left: 15px solid transparent;
    border-right: 15px solid transparent;
    border-bottom: 20px solid red;
    position: absolute;
    top: 40px;
    left: 50%;
    transform: translateX(-50%);
  }
  #spinBtn {
    margin-top: 20px;
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
  }
</style>
</head>
<body>

<div id="wheel">
  <div id="pointer"></div>
</div>
<button id="spinBtn">Spin</button>

<script>
  const sectors = [
    { name: "50 Points", value: 50 },
    { name: "30 Points", value: 30 },
    { name: "20 Points", value: 20 },
    { name: "10 Points", value: 10 },
    { name: "5 Points", value: 5 },
    { name: "2 Points", value: 2 }
  ];

  const wheel = document.getElementById('wheel');
  const pointer = document.getElementById('pointer');
  const spinBtn = document.getElementById('spinBtn');

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

      alert(`You won ${result.name}!`);
      spinning = false;
    }, spinDuration);
  }
</script>

</body>
</html>
