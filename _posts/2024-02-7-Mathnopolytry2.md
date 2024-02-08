---
toc: false
comments: false
layout: default
---

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mathnopoly</title>
<style>
    body {
        margin: 0;
        padding: 0;
        font-family: Arial, sans-serif;
    }
    #container {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    #board {
        width: 500px;
        height: 500px;
        border: 2px solid #000;
        position: relative;
        display: flex;
        flex-wrap: wrap;
    }
    .box {
        width: calc(100% / 4);
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 20px;
        border: 1px solid #000;
        box-sizing: border-box;
    }
    .row {
        width: 100%;
        height: 25%; /* Set height to 25% of #board height */
        display: flex;
    }
    .row .box {
        flex: 1;
    }
    #player, #ai {
        position: absolute;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        background-color: red;
        top: 0;
        left: 0;
    }
    #ai {
        background-color: blue;
    }
    #score {
        background-color: #fff;
        border: 1px solid #000;
        padding: 5px 10px;
        margin-top: 10px;
    }
    #question {
        font-size: 18px;
        margin-top: 10px;
    }
    #answer {
        margin-top: 10px;
        display: flex;
        align-items: center;
    }
    #user-answer {
        width: 100px;
        padding: 5px;
        box-sizing: border-box;
    }
    #submit-answer {
        margin-left: 10px;
        padding: 5px 10px;
        cursor: pointer;
        background-color: #007bff;
        color: #fff;
        border: none;
        border-radius: 5px;
    }
    #submit-answer:hover {
        background-color: #0056b3;
    }
</style>

</head>
<body>
<div id="container">
    <div id="board">
        <div class="row">
            <div class="box">200</div>
            <div class="box">-300</div>
            <div class="box">500</div>
            <div class="box">100</div>
        </div>
        <div class="row">
            <div class="box">200</div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box">100</div>
        </div>
        <div class="row">
            <div class="box">200</div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box">100</div>
        </div>
        <div class="row">
            <div class="box">200</div>
            <div class="box">-300</div>
            <div class="box">500</div>
            <div class="box">100</div>
        </div>
        <!-- Add more rows and boxes here -->
    </div>
    <div id="score">Player Money: $<span id="player-money">0</span> | AI Money: $<span id="ai-money">0</span></div>
    <div id="question">Question: <span id="current-question"></span></div>
    <div id="answer">Answer: <input type="text" id="user-answer"><button id="submit-answer" onclick="submitAnswer()">Submit Answer</button></div>
</div>


<script>
    let playerPosition = 0;
    let aiPosition = 0;
    let playerMoney = 0;
    let aiMoney = 0;

    // Function to generate a random math question
    function generateQuestion() {
        const num1 = Math.floor(Math.random() * 10) + 1;
        const num2 = Math.floor(Math.random() * 10) + 1;
        const operator = Math.random() < 0.5 ? '+' : '-';
        return `${num1} ${operator} ${num2}`;
    }

    // Function to move player or AI
    function move(token, steps) {
        token === 'player' ? playerPosition += steps : aiPosition += steps;
        const currentPosition = token === 'player' ? playerPosition : aiPosition;
        const boxValue = parseInt(document.querySelectorAll('.box')[currentPosition].textContent);
        token === 'player' ? playerMoney += boxValue : aiMoney += boxValue;
        document.getElementById(`${token}-money`).textContent = token === 'player' ? playerMoney : aiMoney;
    }

    // Function to handle player's turn
    function playerTurn() {
        document.getElementById('current-question').textContent = generateQuestion();
    }

    // Function to handle AI's turn
    function aiTurn() {
        document.getElementById('current-question').textContent = generateQuestion();
    }

    // Function to submit answer
    function submitAnswer() {
        const answer = document.getElementById('user-answer').value;
        const correctAnswer = eval(document.getElementById('current-question').textContent);
        if (parseInt(answer) === correctAnswer) {
            const steps = Math.floor(Math.random() * 11) + 2; // Roll two dice
            move('player', steps);
            playerTurn();
        } else {
            const steps = Math.floor(Math.random() * 11) + 2; // Roll two dice
            move('ai', steps);
            aiTurn();
        }
        document.getElementById('user-answer').value = '';
    }

    // Initialize the game
    playerTurn();
</script>
</body>
</html>
