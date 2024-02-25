---
toc: false
comments: false
layout: default
---

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
      const token = localStorage.getItem('jwtToken');
      if (!token) {
          console.error('JWT token not found.');
          return;
      }
      try {
          var base64Url = token.split('.')[1];
          var base64 = base64Url.replace(/-/g, '+').replace(/_/g, '/');
          var jsonPayload = decodeURIComponent(window.atob(base64).split('').map(function(c) {
              return '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2);
          }).join(''));
          const decodedToken = JSON.parse(jsonPayload);
          const userId = decodedToken.user_id;
          // Send POST request to backend
          const data = {
              userId: userId,
              points: result.value
          };
          fetch('http://127.0.0.1:5000/leaderboard', {
              method: 'POST',
              headers: {
                  'Content-Type': 'application/json'
              },
              body: JSON.stringify(data)
          })
          .then(response => {
              if (!response.ok) {
                  throw new Error('Network response was not ok');
              }
              return response.json();
          })
          .then(data => {
              console.log('POST request successful:', data);
          })
          .catch(error => {
              console.error('Error making POST request:', error);
          });
      } catch (error) {
          console.error('Error decoding JWT token:', error);
      }
      alert(`You won ${result.name}!`);
      spinning = false;
    }, spinDuration);
  }
</script>
</body>
</html>