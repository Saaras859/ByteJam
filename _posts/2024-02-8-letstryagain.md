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
        color: black;
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
            <div class="box">80</div>
            <div class="box">30</div>
            <div class="box">200</div>
            <div class="box">-10</div>
        </div>
        <div class="row">
            <div class="box">90</div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box">40</div>
        </div>
        <div class="row">
            <div class="box">-50</div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box">70</div>
        </div>
        <div class="row">
            <div class="box">120</div>
            <div class="box">110</div>
            <div class="box">130</div>
            <div class="box">40</div>
        </div>
    </div>
    <div id="score">Player Money: $<span id="player-money">0</span> | AI Money: $<span id="ai-money">0</span></div>
    <div id="question">Question: <span id="current-question"></span></div>
    <div id="answer">Answer: <input type="text" id="user-answer"><button id="submit-answer" onclick="submitAnswer()">Submit Answer</button></div>
    <div id="position">Player Position: <span id="player-position">1</span> | AI Position: <span id="ai-position">1</span></div>
    <div id="steps">Player Steps: <span id="player-steps">0</span> | AI Steps: <span id="ai-steps">0</span></div>
</div>

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
        1: 80,
        2: 30,
        3: 200,
        4: -10,
        5: 40,
        6: 70,
        7: 40,
        8: 130 ,
        9: 110,
        10: 120,
        11: -50,
        12: 90  
        // Add more mappings as needed for other dice roll numbers
    };

    // Function to generate a random math question
    function generateQuestion() {
        const num1 = Math.floor(Math.random() * 10) + 1;
        const num2 = Math.floor(Math.random() * 10) + 1;
        const operator = Math.random() < 0.5 ? '+' : '-';
        return `${num1} ${operator} ${num2}`;
    }

    // Function to move player or AI
    // Function to move player or AI
    function move(token, steps) {
        for (let i = 0; i < steps; i++) {
            token === 'player' ? playerPosition++ : aiPosition++;
            const totalBoxes = Object.keys(boxValues).length;
            // Loop back to 1 if position exceeds the total number of boxes
            if (playerPosition > totalBoxes) {
                playerPosition %= totalBoxes;
            }
            if (aiPosition > totalBoxes) {
                aiPosition %= totalBoxes;
            }
            const boxValue = boxValues[token === 'player' ? playerPosition : aiPosition];
            token === 'player' ? totalPlayerMoney += boxValue : totalAiMoney += boxValue;
            document.getElementById(`${token}-money`).textContent = token === 'player' ? totalPlayerMoney : totalAiMoney;
            document.getElementById(`${token}-position`).textContent = token === 'player' ? playerPosition : aiPosition; // Update position display
        }
        token === 'player' ? playerSteps = steps : aiSteps = steps; // Update steps
        document.getElementById(`${token}-steps`).textContent = steps; // Update steps display
    }


    // Function to handle player's turn
    function playerTurn() {
        playerMoney = 0;
        playerSteps = 0; // Reset playerSteps
        document.getElementById('current-question').textContent = generateQuestion();
    }

    // Function to handle AI's turn
    function aiTurn() {
        aiSteps = 0; // Reset aiSteps
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
