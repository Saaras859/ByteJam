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
        flex-direction: row; /* Arrange items horizontally */
    }
    #game-container {
        flex: 1; /* Take up remaining space */
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: 50px;
    }
    #text-container {
        flex: 1; /* Take up remaining space */
        display: flex;
        flex-direction: column; /* Arrange items vertically */
        justify-content: center;
        align-items: center;
        padding: 0 20px; /* Add some padding */
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

    .turnbutton {
        background-color: #7d7d7d;
        border-color: #7d7d7d;
        width: 80px;
        height: 40px;
        border-radius: 10px;
        font-size: 20px;
        font-family: Verdana, sans-serif;
        cursor: pointer;
        margin-top: 10px;
    }

    .turnbutton:hover {
        background-color: #7d7d7d !important;
    }

    #score, #question, #answer {
        font-size: 24px; /* Increase font size */
        text-align: center; /* Center align text */
        margin-bottom: 10px; /* Add some space between elements */
    }

    input[type="text"] {
        font-size: 20px; /* Increase font size for input */
        padding: 5px; /* Adjust padding for input */
        margin-right: 5px; /* Add some space between input and button */
    }

    button {
        font-size: 20px; /* Increase font size for button */
        padding: 5px 10px; /* Adjust padding for button */
        cursor: pointer;
        background-color: #007bff;
        color: #fff;
        border: none;
        border-radius: 5px;
    }

    button:hover {
        background-color: #0056b3;
    }

    /* Styling for the dice roll result */
    #dice-roll {
        font-size: 24px;
        text-align: center;
        margin-top: 20px; /* Add space between the grid and dice roll */
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
<br><br>
</div>
    <div id="score">Player Money: $<span id="player-money">0</span> | AI Money: $<span id="ai-money">0</span></div>
    <div id="question">Question: <span id="current-question"></span></div>
    <div id="answer">Answer: <input type="text" id="user-answer"><button id="submit-answer" onclick="submitAnswer()">Submit Answer</button></div>
    <div id="position">Player Position: <span id="player-position">1</span> | AI Position: <span id="ai-position">1</span></div>
    <div id="steps">Player Steps: <span id="player-steps">0</span> | AI Steps: <span id="ai-steps">0</span></div>
</div>
    <div id="dice-roll"></div>
    <div class="ai" id="ai-dot"></div>

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


// Function to move the player (red box) to the center of the specified position
function movePlayerToPosition(position) {
    const boxes = document.querySelectorAll('.box');
    const box = boxes[position];
    const boxRect = box.getBoundingClientRect();
    const player = document.getElementById('player');
    const boxSize = 100; // Assuming box size is 100px
    const boxCenterX = boxRect.left + (boxSize / 2); // Calculate center X coordinate of the box
    const boxCenterY = boxRect.top + (boxSize / 2); // Calculate center Y coordinate of the box
    player.style.top = `${boxCenterY}px`; // Set the top position of the player
    player.style.left = `${boxCenterX}px`; // Set the left position of the player
}
function moveAIToPosition(position) {
    const boxes = document.querySelectorAll('.box');
    const box = boxes[position];
    const boxRect = box.getBoundingClientRect();
    const aiDot = document.getElementById('ai-dot');
    const dotSize = 40; // Assuming dot size is 40px
    const boxSize = 100; // Assuming box size is 100px
    const boxCenterX = boxRect.left + (boxSize / 2); // Calculate center X coordinate of the box
    const boxCenterY = boxRect.top + (boxSize / 2); // Calculate center Y coordinate of the box
    aiDot.style.top = `${boxCenterY - (dotSize / 2)}px`; // Set the top position of the dot to center it vertically
    aiDot.style.left = `${boxCenterX - (dotSize / 2)}px`; // Set the left position of the dot to center it horizontally
    aiDot.style.display = 'block'; // Show the dot
}

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

    // Retain additional functionality from the second function
    const diceRoll = Math.floor(Math.random() * 11) + 2; // Roll two dice
    document.getElementById('dice-roll').textContent = `Dice Roll: ${diceRoll}`;
    if (parseInt(answer) === correctAnswer) {
        movePlayerToPosition(playerPosition); // Move the player to the correct box position
    } else {
        moveAIToPosition(aiPosition); // Move the AI dot to the correct box position
    }
}
    // Initialize the game
    playerTurn();
    movePlayerToPosition(0);
    moveAIToPosition(0); // Move AI dot to box 1
</script>
</body>
</html>
