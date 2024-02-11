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
        height: 100vh;
        background-color: #f0f0f0; /* Light gray background */
        display: flex;
        flex-direction: column; /* Change to column layout */
        justify-content: center; /* Center content vertically */
        align-items: center; /* Center content horizontally */
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
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 24px; /* Make font size bigger */
        color: black; /* Set text color to black */
    }

    .emptybox {
        background-color: #000000; /* Light gray */
        width: 100px;
        height: 100px;
    }

    .player {
        background-color: rgba(156, 0, 0, 0.5); /* Red with 50% opacity */
        width: 50px;
        height: 50px;
        position: absolute;
        transform: translate(-50%, -50%); /* Center the dot */
        border-radius: 50%; /* Make it round */
    }
    .ai {
        background-color: rgba(0, 0, 156, 0.5); /* Blue with 50% opacity */
        width: 40px;
        height: 40px;
        position: fixed;
        border-radius: 50%; /* Makes the dot round */
        display: none; /* Initially hidden */
    }

    #question {
        font-size: 24px; /* Increase font size */
        text-align: center; /* Center align text */
        margin-bottom: 10px; /* Add some space between elements */
    }

    #answer {
        display: flex;
        align-items: center;
    }

    #user-answer {
        font-size: 20px; /* Increase font size for input */
        padding: 5px; /* Adjust padding for input */
        margin-right: 10px; /* Add some space between input and button */
    }

    /* Styling for the dice roll result */
    #dice-roll {
        font-size: 24px;
        text-align: center;
        margin-top: 20px; /* Add space between the grid and dice roll */
    }

    #player-money, #ai-money {
        font-size: 20px;
        margin-top: 10px;
    }
</style>
</head>
<body>

<div id="game-container">
    <div class="container">
        <!-- 16 light gray boxes -->
        <!-- Box IDs start from 0 -->
        <div class="box" id="box0"></div>
        <div class="box" id="box1">100</div>
        <div class="box" id="box2">150</div>
        <div class="box" id="box3">-20</div>
        <div class="box" id="box4">200</div>
        <div class="box" id="box5">-30</div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="box" id="box6">140</div>
        <div class="box" id="box7">10</div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="box" id="box8">-60</div>
        <div class="box" id="box9">20</div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="box" id="box10">-50</div>
        <div class="box" id="box11">-5</div>
        <div class="box" id="box12">-10</div>
        <div class="box" id="box13">30</div>
        <div class="box" id="box14">-70</div>
        <div class="box" id="box15">5</div>
        <div class="player" id="player"></div>
        <div class="ai" id="ai-dot"></div>
    </div>
</div>

<br><br>
<div id="question">Question: <span id="current-question"></span></div>
<div id="answer">Answer: <input type="text" id="user-answer" onkeypress="checkEnter(event)"></div>
<div id="player-money">Player Money: 0</div>
<div id="ai-money">AI Money: 0</div>


<script>
    let playerPosition = 0; // Start from 0
    let aiPosition = 0; // Start from 0
    let playerMoney = 0;
    let aiMoney = 0;

    const boxValues = {
        0: 0,
        1: 100,
        2: 150,
        3: -20,
        4: 200,
        5: -30,
        6: 140,
        7: 10,
        8: -60,
        9: 20,
        10: -50,
        11: -5,
        12: -10,
        13: 30,
        14: -70,
        15: 5 
    };

    function generateQuestion() {
        const num1 = Math.floor(Math.random() * 10) + 1;
        const num2 = Math.floor(Math.random() * 10) + 1;
        const operator = Math.random() < 0.5 ? '+' : '-';
        return `${num1} ${operator} ${num2}`;
    }

    function move(token, steps) {
        const totalBoxes = Object.keys(boxValues).length;
        for (let i = 0; i < steps; i++) {
            if (token === 'player') {
                playerPosition = (playerPosition + 1) % totalBoxes;
            } else {
                aiPosition = (aiPosition + 1) % totalBoxes;
            }
        }
        const boxValue = boxValues[token === 'player' ? playerPosition : aiPosition];
        if (token === 'player') {
            playerMoney += boxValue;
            document.getElementById('player-money').textContent = `Player Money: ${playerMoney}`;
        } else {
            aiMoney += boxValue;
            document.getElementById('ai-money').textContent = `AI Money: ${aiMoney}`;
        }
    }

    function movePlayerToPosition(position) {
        const playerBox = document.getElementById(`box${position}`);
        const playerDot = document.getElementById('player');
        const boxRect = playerBox.getBoundingClientRect();
        const boxSize = 100; 
        const boxCenterX = boxRect.left + (boxSize / 2);
        const boxCenterY = boxRect.top + (boxSize / 2);
        playerDot.style.top = `${boxCenterY}px`;
        playerDot.style.left = `${boxCenterX}px`;
    }

    function moveAIToPosition(position) {
        const aiBox = document.getElementById(`box${position}`);
        const aiDot = document.getElementById('ai-dot');
        const boxRect = aiBox.getBoundingClientRect();
        const dotSize = 40;
        const boxSize = 100;
        const boxCenterX = boxRect.left + (boxSize / 2);
        const boxCenterY = boxRect.top + (boxSize / 2);
        aiDot.style.top = `${boxCenterY - (dotSize / 2)}px`;
        aiDot.style.left = `${boxCenterX - (dotSize / 2)}px`;
        aiDot.style.display = 'block';
    }

    function submitAnswer() {
        const answer = document.getElementById('user-answer').value;
        const correctAnswer = eval(document.getElementById('current-question').textContent);
        if (parseInt(answer) === correctAnswer) {
            const steps = Math.floor(Math.random() * 11) + 2;
            move('player', steps);
            document.getElementById('current-question').textContent = generateQuestion();
            movePlayerToPosition(playerPosition);
        } else {
            const steps = Math.floor(Math.random() * 11) + 2;
            move('ai', steps);
            document.getElementById('current-question').textContent = generateQuestion();
            moveAIToPosition(aiPosition);
        }
        document.getElementById('user-answer').value = '';
    }

    document.getElementById('current-question').textContent = generateQuestion();
    movePlayerToPosition(playerPosition);
    moveAIToPosition(aiPosition);

function checkEnter(event) {
    if (event.key === "Enter") {
        submitAnswer();
    }
}

</script>
</body>
</html>
