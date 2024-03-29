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
<h1 class="welcome-heading">Relax with some Tic Tac Toe!</h1>

<div class="container">
  <div class="box">
    <img src="https://as1.ftcdn.net/v2/jpg/00/42/79/76/1000_F_42797620_sNsiHXxAcuWJnTr5GyywQ8oWTQH0gfvP.jpg" alt="Tic Tac Toe Easy">
    <h2>Easy</h2>
    <a href="http://127.0.0.1:4100/ByteJam/2024/02/08/Tick_Tac_Toe_Easy.html"><center>Easy Mode</center></a>
  </div>
  <div class="box">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/32/Tic_tac_toe.svg/1200px-Tic_tac_toe.svg.png" alt="Tic Tac Toe Hard">
    <h2>Hard</h2>
    <a href="http://127.0.0.1:4100/ByteJam/2024/02/08/Tick_Tac_Toe_Hard.html"><center>Hard Mode</center></a>
  </div>
</div>

<div class="home-button">
  <a href="http://127.0.0.1:4100/ByteJam/2024/02/08/Main.html">Home</a>
</div>

</body>
</html>
