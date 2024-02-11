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
        background-color: #f0f0f0;
        display: flex;
        flex-direction: row;
    }
    #game-container {
        flex: 1;
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: 50px;
    }
    .container {
        display: grid;
        grid-template-columns: repeat(5, 100px);
        grid-template-rows: repeat(5, 100px);
        gap: 10px;
    }
    .box {
        background-color: #cccccc;
        width: 100px;
        height: 100px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 24px;
        color: black;
    }
    .emptybox {
        background-color: #000000;
        width: 100px;
        height: 100px;
    }
    .player {
        background-color: rgba(156, 0, 0, 0.5);
        width: 50px;
        height: 50px;
        position: absolute;
        transform: translate(-50%, -50%);
        border-radius: 50%;
    }
    .ai {
        background-color: rgba(0, 0, 156, 0.5);
        width: 40px;
        height: 40px;
        position: fixed;
        border-radius: 50%;
        display: none;
    }
    #score, #question, #answer {
        font-size: 24px;
        text-align: center;
        margin-bottom: 10px;
    }
    input[type="text"] {
        font-size: 20px;
        padding: 5px;
        margin-right: 5px;
    }
    button {
        font-size: 20px;
        padding: 5px 10px;
        cursor: pointer;
        background-color: #007bff;
        color: #fff;
        border: none;
        border-radius: 5px;
    }
    button:hover {
        background-color: #0056b3;
    }
    #dice-roll {
        font-size: 24px;
        text-align: center;
        margin-top: 20px;
    }
</style>
</head>
<body>

<div id="game-container">
    <div class="container">
        <!-- 16 light gray boxes -->
        <div class="box" id="box1"></div>
        <div class="box" id="box2">100</div>
        <div class="box" id="box3">150</div>
        <div class="box" id="box4">-20</div>
        <div class="box" id="box5">10</div>
        <div class="box" id="box6">5</div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="box" id="box7">-30</div>
        <div class="box" id="box8">-70</div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="box" id="box9">140</div>
        <div class="box" id="box10">30</div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="box" id="box11">10</div>
        <div class="box" id="box12">-10</div>
        <div class="box" id="box13">-5</div>
        <div class="box" id="box14">-50</div>
        <div class="box" id="box15">20</div>
        <div class="box" id="box16">-20</div>
        <div class="player" id="player"></div>
    </div>
</div>

<div id="score">Player Money: $<span id="player-money">0</span> | AI Money: $<span id="ai-money">0</span></div>
<div id="question">Question: <span id="current-question"></span></div>
<div id="answer">Answer: <input type="text" id="user-answer"><button id="submit-answer" onclick="submitAnswer()">Submit Answer</button></div>
<div id="position">Player Position: <span id="player-position">1</span> | AI Position: <span id="ai-position">1</span></div>
<div id="steps">Player Steps: <span id="player-steps">0</span> | AI Steps: <span id="ai-steps">0</span></div>
<div id="dice-roll"></div>
<div class="ai" id="ai-dot"></div>

<script>
    let playerPosition = 1;
    let aiPosition = 1;
    let playerMoney = 0;
    let aiMoney = 0;
    let playerSteps = 0;
    let aiSteps = 0;
    let totalPlayerMoney = 0;
    let totalAiMoney = 0;

    const boxValues = {
        1: 0,
        2: 100,
        3: 150,
        4: -20,
        5: 10,
        6: -30,
        7: 140,
        8: 10,
        9: -20 ,
        10: 20,
        11: -50,
        12: -5,
        13: -10,
        14: 30,
        16: 5 
    };

    const cardFunctions = [
        () => { playerMoney += 50; alert("You gained $50!"); },
        () => { playerMoney -= 50; alert("You lost $50!"); },
        () => { playerMoney += 100; alert("You gained $100!"); },
        () => { playerMoney -= 100; alert("You lost $100!"); }
    ];

    const cardIndices = [1, 2, 3, 4]; // Indices corresponding to card functions

    // Modify boxValues to include card indices at random positions
    for (let i = 0; i < cardIndices.length; i++) {
        const randomIndex = Math.floor(Math.random() * Object.keys(boxValues).length) + 1;
        boxValues[randomIndex] = cardIndices[i];
    }

    function activateCard(position) {
        const cardIndex = boxValues[position];
        if (cardIndex !== undefined) {
            const cardFunction = cardFunctions[cardIndex - 1];
            cardFunction();
            document.getElementById('player-money').textContent = playerMoney;
        }
    }

    function move(token, steps) {
        for (let i = 0; i < steps; i++) {
            token === 'player' ? playerPosition++ : aiPosition++;
            const totalBoxes = Object.keys(boxValues).length;
            if (playerPosition > totalBoxes) {
                playerPosition %= totalBoxes;
            }
            if (aiPosition > totalBoxes) {
                aiPosition %= totalBoxes;
            }
            activateCard(token === 'player' ? playerPosition : aiPosition);
            const boxValue = boxValues[token === 'player' ? playerPosition - 1 : aiPosition - 1];
            token === 'player' ? (totalPlayerMoney += boxValue) : (totalAiMoney += boxValue);
            document.getElementById(`${token}-money`).textContent = token === 'player' ? totalPlayerMoney : totalAiMoney;
            document.getElementById(`${token}-position`).textContent = token === 'player' ? playerPosition : aiPosition;
        }
        token === 'player' ? (playerSteps = steps) : (aiSteps = steps);
        document.getElementById(`${token}-steps`).textContent = steps;
    }

    function submitAnswer() {
        const answer = document.getElementById('user-answer').value;
        const correctAnswer = eval(document.getElementById('current-question').textContent);
        if (parseInt(answer) === correctAnswer) {
            const steps = Math.floor(Math.random() * 11) + 2;
            move('player', steps);
            playerTurn();
        } else {
            const steps = Math.floor(Math.random() * 11) + 2;
            move('ai', steps);
            aiTurn();
        }
        document.getElementById('user-answer').value = '';
        const diceRoll = Math.floor(Math.random() * 11) + 2;
        document.getElementById('dice-roll').textContent = `Dice Roll: ${diceRoll}`;
        movePlayerToPosition(playerPosition);
        moveAIToPosition(aiPosition);
    }

    function playerTurn() {
        playerMoney = 0;
        playerSteps = 0;
        document.getElementById('current-question').textContent = generateQuestion();
    }

    function aiTurn() {
        aiSteps = 0;
        document.getElementById('current-question').textContent = generateQuestion();
    }

    function generateQuestion() {
        const num1 = Math.floor(Math.random() * 10) + 1;
        const num2 = Math.floor(Math.random() * 10) + 1;
        const operator = Math.random() < 0.5 ? '+' : '-';
        return `${num1} ${operator} ${num2}`;
    }

    function movePlayerToPosition(position) {
        const boxes = document.querySelectorAll('.box');
        const box = boxes[position - 1];
        const boxRect = box.getBoundingClientRect();
        const player = document.getElementById('player');
        const boxSize = 100;
        const boxCenterX = boxRect.left + (boxSize / 2);
        const boxCenterY = boxRect.top + (boxSize / 2);
        player.style.top = `${boxCenterY}px`;
        player.style.left = `${boxCenterX}px`;
    }

    function moveAIToPosition(position) {
        const boxes = document.querySelectorAll('.box');
        const box = boxes[position - 1];
        const boxRect = box.getBoundingClientRect();
        const aiDot = document.getElementById('ai-dot');
        const dotSize = 40;
        const boxSize = 100;
        const boxCenterX = boxRect.left + (boxSize / 2);
        const boxCenterY = boxRect.top + (boxSize / 2);
        aiDot.style.top = `${boxCenterY - (dotSize / 2)}px`;
        aiDot.style.left = `${boxCenterX - (dotSize / 2)}px`;
        aiDot.style.display = 'block';
    }

    playerTurn();
    movePlayerToPosition(1);
    moveAIToPosition(1);

</script>
</body>
</html>
