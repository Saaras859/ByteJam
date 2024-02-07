---
toc: false
comments: false
layout: default
---
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gray Boxes</title>
<style>
    body {
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background-color: #f0f0f0; /* Light gray background */
    }
    .container {
        display: grid;
        grid-template-columns: repeat(5, 100px); 
        grid-template-rows: repeat(5, 100px); 
        gap: 10px; /* Gap between boxes */
    }
    .box {
        background-color: #cccccc; /* Light gray */
        width: 100px;
        height: 100px;
    }
    .empytbox {
        background-color: #000000; /* Light gray */
        width: 100px;
        height: 100px;
    }
    .player {
        background-color: #9c0000; /* Red */
        width: 20px;
        height: 20px;
        position: fixed;
        top: 22.5%;
        left: 35.65%;
        transform: translate(-50%, -50%);
        padding: 20px;
        border-radius: 10px;
    }
    .turnbutton {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: #7d7d7d;
        border-color: #7d7d7d;
        width: 10%;
        height: 10%;
        border-radius: 10px;
        font-size: 30px;
        font-family: Verdana, sans-serif;
        }
    .turnbutton:hover {
        background-color: #7d7d7d !important;
    }

</style>
</head>
<body>
<div class="container">
<!-- 16 light gray boxes -->
<div class="box" id="box1"></div>
<div class="box" id="box2"></div>
<div class="box" id="box3"></div>
<div class="box" id="box4"></div>
<div class="box" id="box5"></div>
<div class="box" id="box6"></div>
<div class="emptybox"></div>
<div class="emptybox"></div>
<div class="emptybox"></div>
<div class="box" id="box7"></div>
<div class="box" id="box8"></div>
<div class="emptybox"></div>
<div class="emptybox"></div>
<div class="emptybox"></div>
<div class="box" id="box9"></div>
<div class="box" id="box10"></div>
<div class="emptybox"></div>
<div class="emptybox"></div>
<div class="emptybox"></div>
<div class="box" id="box11"></div>
<div class="box" id="box12"></div>
<div class="box" id="box13"></div>
<div class="box" id="box14"></div>
<div class="box" id="box15"></div>
<div class="box" id="box16"></div>
<div class="player" id="player"></div>
<button class="turnbutton" id="turnbutton" onclick="playerturn()">GO</button>
</div>
<script>
    var playervalue = 1
    console.log(playervalue)
    function rollDice() {
        return Math.floor(Math.random() * 6) + 1;
    }
    function playerturn() {
        playervalue += rolldice()
        console.log(playervalue)
    }
</script>
</body>
</html>
