---
toc: false
comments: false
layout: default
---

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tic Tac Toe</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">

<style>
  body {
    font-family: 'Poppins', sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
  }
  .container {
    max-width: 800px;
    margin: 50px auto;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }
  .box {
    width: 45%;
    background-color: #fff;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .box h2 {
    margin-top: 0;
    margin-bottom: 10px;
  }
  .box a {
    display: block;
    text-decoration: none;
    color: #333;
    font-weight: bold;
    text-align: center;
    width: 100%;
    padding: 10px 0;
    border: 2px solid #333;
    border-radius: 5px;
    transition: background-color 0.3s ease;
  }
  .box a:hover {
    background-color: #333;
    color: #fff;
  }
  .box img {
    width: 100%; /* Make all images fill the container */
    height: auto;
    max-height: 200px; /* Set a maximum height for the images */
    object-fit: cover; /* Ensure images maintain aspect ratio */
    border-radius: 8px;
  }
  .welcome-heading {
    text-align: center;
    font-size: 36px;
    color: white;
    margin-bottom: 30px;
    font-weight: 600;
  }
  .home-button {
    position: fixed;
    top: 20px;
    left: 20px;
    z-index: 9999;
  }
  .home-button a {
    text-decoration: none;
    color: white;
    background-color: #007bff;
    padding: 10px 20px;
    border-radius: 5px;
  }
  .home-button a:hover {
    background-color: #0056b3;
  }
</style>
</head>
<body>
<h1 class="welcome-heading">Gamble In a Casino!!</h1>

<div class="container">
  <div class="box">
    <img src="https://images.prismic.io/desplaines-rushstreetgaming/1c8e0aa3-6b2d-4f01-a49e-15b556dc0882_03253_March-Blackjack-Blowout-Email_Image_1200x650_v1_210223.jpg?auto=compress,format" alt="Blackjack">
    <h2>Play some Blackjack</h2>
    <a href="http://127.0.0.1:4100/ByteJam/2024/02/08/Binary-Project.html"><center>Blackjack</center></a>
  </div>
  <div class="box">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/82/Las_Vegas_slot_machines.jpg/640px-Las_Vegas_slot_machines.jpg" alt="Slot">
    <h2>Play some slot!!</h2>
    <a href="http://127.0.0.1:4100/ByteJam/2024/02/15/Slot-Machine.html"><center>Slot Machine</center></a>
  </div>
    <div class="box">
    <img src="https://crescent.edu/uploads/editor/images/blog/The_History_of_Baccarat.jpg" alt="Bakkarat">
    <h2>PLay some Bakkarat!</h2>
    <a href="http://127.0.0.1:4100/ByteJam/2024/02/15/baccarat.html"><center>Baccarat</center></a>
  </div>
    <div class="box">
    <img src="https://c8.alamy.com/comp/D83FDG/spinning-casino-roulette-wheel-gambling-and-casino-concept-D83FDG.jpg" alt="Spin the wheel!">
    <h2>Spin the Wheel!</h2>
    <a href="http://127.0.0.1:4100/ByteJam/2024/02/23/SPINTHEWHEEL.html">Spin the Wheel!</a>
  </div>
</div>

<div class="home-button">
  <a href="http://127.0.0.1:4100/ByteJam/2024/02/08/Main.html">Home</a>
</div>

</body>
</html>



