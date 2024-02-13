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
<style>
    body {
        margin: 0;
        padding: 0;
        height: 100vh;
        background-image: url('https://wallpapers.com/images/hd/plain-black-background-02fh7564l8qq4m6d.jpg');
        background-size: cover;
        background-position: center;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    
    .container {
        display: grid;
        grid-template-columns: repeat(3, 150px);
        grid-template-rows: repeat(3, 150px);
        gap: 15px;
    }
    
    .box {
        background-color: white;
        width: 150px;
        height: 150px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 48px;
        color: black;
        cursor: pointer;
    }
    
    .emptybox {
        background-color: white;
        width: 150px;
        height: 150px;
    }
    
    .cross::after {
        content: 'X';
    }
    
    .circle::after {
        content: 'O';
    }
    
    .money-container {
        display: flex;
        justify-content: space-between;
        width: 500px; /* Adjust as needed */
        margin-top: 20px;
    }
    
    .money-box {
        padding: 10px;
        border-radius: 5px;
        color: white;
        font-size: 20px;
    }
    
    .player-money {
        background-color: red;
    }
    
    .ai-money {
        background-color: blue;
        margin-left: 20px; /* Adjust margin-left as needed */

    }
</style>
</head>
<body>

<div id="game-container">
    <div class="container">
        <!-- Boxes for the tic-tac-toe game -->
        <div class="box emptybox" id="box0"></div>
        <div class="box emptybox" id="box1"></div>
        <div class="box emptybox" id="box2"></div>
        <div class="box emptybox" id="box3"></div>
        <div class="box emptybox" id="box4"></div>
        <div class="box emptybox" id="box5"></div>
        <div class="box emptybox" id="box6"></div>
        <div class="box emptybox" id="box7"></div>
        <div class="box emptybox" id="box8"></div>
    </div>
</div>

<div class="money-container">
    <div id="player-money" class="money-box player-money">Player Money: 0</div>
    <div id="ai-money" class="money-box ai-money">AI Money: 0</div>
</div>

</body>
</html>
