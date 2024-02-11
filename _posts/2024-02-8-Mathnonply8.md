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
<div id="question">Question: <span id="current-question"></span></div>
<div id="answer">Answer: <input type="text" id="user-answer"></div>
<div class="ai" id="ai-dot"></div>
<div id="player-money">Player Money: 0</div>
<div id="ai-money">AI Money: 0</div>

<script>
    let playerPosition = 0;
    let aiPosition = 0;
    let playerMoney = 0;
    let aiMoney = 0;

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
        15: 20,
        16: 5 
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
    console.log(`Moving ${token} dot ${steps} steps.`);
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
    }

    // After moving, get the value of the box at the final position
    const boxValue = boxValues[token === 'player' ? playerPosition : aiPosition];
    if (boxValue === undefined) {
        console.error(`Box value for position ${token === 'player' ? playerPosition : aiPosition} is undefined.`);
        return;
    }
    if (token === 'player') {
        console.log(`Adding ${boxValue} to player sum.`);
        playerMoney += boxValue;
    } else {
        console.log(`Adding ${boxValue} to AI sum.`);
        aiMoney += boxValue;
    }

    // Update the displayed sums
    document.getElementById('player-money').textContent = `Player Money: ${playerMoney}`;
    document.getElementById('ai-money').textContent = `AI Money: ${aiMoney}`;
}


    // Function to move the player (red box) to the center of the specified position
// Function to move the player dot to the correct box position
function movePlayerToPosition(position) {
    const playerBox = document.getElementById(`box${position + 1}`); // Box IDs start from 1
    const playerDot = document.getElementById('player');
    const boxRect = playerBox.getBoundingClientRect();
    const boxSize = 100; // Assuming box size is 100px
    const boxCenterX = boxRect.left + (boxSize / 2); // Calculate center X coordinate of the box
    const boxCenterY = boxRect.top + (boxSize / 2); // Calculate center Y coordinate of the box
    playerDot.style.top = `${boxCenterY}px`; // Set the top position of the player dot
    playerDot.style.left = `${boxCenterX}px`; // Set the left position of the player dot
    console.log(`Player dot moved to box ${position}.`);
}

// Function to move the AI dot to the correct box position
function moveAIToPosition(position) {
    const aiBox = document.getElementById(`box${position + 1}`); // Box IDs start from 1
    const aiDot = document.getElementById('ai-dot');
    const boxRect = aiBox.getBoundingClientRect();
    const dotSize = 40; // Assuming dot size is 40px
    const boxSize = 100; // Assuming box size is 100px
    const boxCenterX = boxRect.left + (boxSize / 2); // Calculate center X coordinate of the box
    const boxCenterY = boxRect.top + (boxSize / 2); // Calculate center Y coordinate of the box
    aiDot.style.top = `${boxCenterY - (dotSize / 2)}px`; // Set the top position of the AI dot
    aiDot.style.left = `${boxCenterX - (dotSize / 2)}px`; // Set the left position of the AI dot
    aiDot.style.display = 'block'; // Show the AI dot
    console.log(`AI dot moved to box ${position}.`);

}


    function submitAnswer() {
        const answer = document.getElementById('user-answer').value;
        const correctAnswer = eval(document.getElementById('current-question').textContent);
        if (parseInt(answer) === correctAnswer) {
            const steps = Math.floor(Math.random() * 11) + 2; // Roll two dice
            move('player', steps);
            document.getElementById('current-question').textContent = generateQuestion();
            movePlayerToPosition(playerPosition); // Move the player to the correct box position
        } else {
            const steps = Math.floor(Math.random() * 11) + 2; // Roll two dice
            move('ai', steps);
            document.getElementById('current-question').textContent = generateQuestion();
            moveAIToPosition(aiPosition); // Move the AI dot to the correct box position
        }
        document.getElementById('user-answer').value = '';
    }

    // Event listener for the Enter key to submit the answer
    document.getElementById('user-answer').addEventListener('keypress', function(event) {
        if (event.key === 'Enter') {
            submitAnswer();
        }
    });
// Initialize the game
document.getElementById('current-question').textContent = generateQuestion();
movePlayerToPosition(0);
moveAIToPosition(0); // Move AI dot to box 1

// Add event listeners to each box
const boxes = document.querySelectorAll('.box');
boxes.forEach(box => {
    box.addEventListener('boxVisited', function(event) {
        const { token } = event.detail;
        const boxValue = boxValues[token === 'player' ? playerPosition : aiPosition];
        if (boxValue === undefined) {
            console.error(`Box value for position ${token === 'player' ? playerPosition : aiPosition} is undefined.`);
            return;
        }
        if (token === 'player') {
            playerMoney += boxValue;
            document.getElementById('player-money').textContent = `Player Money: ${playerMoney}`;
        } else {
            aiMoney += boxValue;
            document.getElementById('ai-money').textContent = `AI Money: ${aiMoney}`;
        }
    });
});
</script>
</body>
</html>