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
    background-image: url('https://wallpapers.com/images/hd/plain-black-background-02fh7564l8qq4m6d.jpg');
    background-size: cover; /* Cover the entire background */
    background-position: center; /* Center the background image */
    display: flex;
    flex-direction: column; /* Change to column layout */
    justify-content: center; /* Center content vertically */
    align-items: center; /* Center content horizontally */
    margin-top: 5px;
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
        background-color: transparent; /* Light gray */
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
        width: 50px;
        height: 50px;
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
        justify-content: center; /* Center horizontally */
        margin-top: 20px;
    }
    #user-answer {
        font-size: 20px;
        padding: 20px;
        margin-right: 10px;
        background-color: rgba(0, 0, 0, 0.9); /* Lighter shade of black */
        color: white; /* White text */
        border-radius: 10px; /* Rounded corners */
        border: none; /* Remove border */
        outline: none; /* Remove outline */
        text-align: center; /* Center text horizontally */
        vertical-align: middle; /* Center text vertically */
        width: 100px; /* Adjust width as needed */
        height: 30px; /* Adjust height as needed */
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
    #game-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 20px; /* Adjust the top margin as needed */
    }
    #money-container {
        display: flex;
        justify-content: space-between;
        width: 100%; /* Ensure the container takes up full width */
        max-width: 600px; /* Adjust the maximum width as needed */
        margin-top: 20px; /* Adjust the top margin as needed */
    }
    #player-money, #ai-money {
        font-size: 20px;
    }
    .container {
        display: grid;
        grid-template-columns: repeat(5, 100px);
        grid-template-rows: repeat(5, 100px);
        gap: 10px; /* Gap between boxes */
    }
    /* Your existing styles for game board */
    .money-box {
        padding: 10px;
        margin-top: 10px;
        border-radius: 5px;
        color: white;
        font-size: 20px;
    }
    .player-money {
        background-color: red;
    }
    .ai-money {
        background-color: blue;
    }
    #turn-display {
    font-size: 24px; /* Increase font size */
    background-color: black; /* Black background */
    color: white; /* White text */
    padding: 10px; /* Add some padding */
    border-radius: 5px; /* Add rounded corners */
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
        <div class="box" id="box15">-30</div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="box" id="box5">140</div>
        <div class="box" id="box14">10</div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="box" id="box6">-60</div>
        <div class="box" id="box13">20</div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="emptybox"></div>
        <div class="box" id="box7">-50</div>
        <div class="box" id="box12">-5</div>
        <div class="box" id="box11">-10</div>
        <div class="box" id="box10">30</div>
        <div class="box" id="box9">-70</div>
        <div class="box" id="box8">5</div>
        <div class="player" id="player"></div>
        <div class="ai" id="ai-dot"></div>
    </div>
</div>

<div id="money-container">
    <div id="player-money" class="money-box player-money">Player Money: 0</div>
    <div id="turn-display" class="turn-display"></div>
    <div id="ai-money" class="money-box ai-money">AI Money: 0</div>
</div>
<br>
<div id="question">Question: <span id="current-question"></span></div>
<div id="answer"><input type="text" id="user-answer" onkeypress="checkEnter(event)"></div>

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
        5: 140,
        6: -60,
        7: -50,
        8: 5,
        9: -70,
        10: 30,
        11: -10,
        12: -5,
        13: 20,
        14: 10,
        15: -30
    };

    function generateQuestion() {
        const num1 = Math.floor(Math.random() * 10) + 1;
        const num2 = Math.floor(Math.random() * 10) + 1;
        const operator = Math.random() < 0.5 ? '+' : '-';
        return `${num1} ${operator} ${num2}`;
    }

function move(token, steps) {
    console.log(`Moving ${token} dot ${steps} steps.`);
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
        console.log(`Adding ${boxValue} to player sum.`);
        playerMoney += boxValue;
        document.getElementById('player-money').textContent = `Player Money: ${playerMoney}`;
    } else {
        console.log(`Adding ${boxValue} to AI sum.`);
        aiMoney += boxValue;
        document.getElementById('ai-money').textContent = `AI Money: ${aiMoney}`;
    }
    
    // Check if either player or AI reaches 500
    if (playerMoney >= 500) {
        alert("You wins! You reached 500 first.");
        resetGame();
    } else if (aiMoney >= 500) {
        alert("AI wins! AI reached 500 first.");
        resetGame();
    }
}

function resetGame() {
    // Reset player and AI positions
    playerPosition = 0;
    aiPosition = 0;
    
    // Reset player and AI money
    playerMoney = 0;
    aiMoney = 0;
    
    // Update displayed money
    document.getElementById('player-money').textContent = `Player Money: ${playerMoney}`;
    document.getElementById('ai-money').textContent = `AI Money: ${aiMoney}`;
    
    // Generate new initial question
    document.getElementById('current-question').textContent = generateQuestion();
    
    // Move player and AI dots to initial positions
    movePlayerToPosition(playerPosition);
    moveAIToPosition(aiPosition);
}
    function movePlayerToPosition(position) {
        const playerBox = document.getElementById(`box${position}`);
        const playerDot = document.getElementById('player');
        const boxRect = playerBox.getBoundingClientRect();
        const boxSize = 100; 
        const boxCenterX = boxRect.left + (boxSize / 2);
        const boxCenterY = boxRect.top + (boxSize / 2);
        console.log(`Player dot is currently positioned in box ${position} at (${boxCenterX}, ${boxCenterY}).`);
        playerDot.style.top = `${boxCenterY}px`;
        playerDot.style.left = `${boxCenterX}px`;
        console.log(`Player dot moved to box ${position}.`);
    }

    function moveAIToPosition(position) {
        const aiBox = document.getElementById(`box${position}`);
        const aiDot = document.getElementById('ai-dot');
        const boxRect = aiBox.getBoundingClientRect();
        const dotSize = 50;
        const boxSize = 100;
        const boxCenterX = boxRect.left + (boxSize / 2);
        const boxCenterY = boxRect.top + (boxSize / 2);
        console.log(`AI dot moved to box ${position}.`);
        aiDot.style.top = `${boxCenterY - (dotSize / 2)}px`;
        aiDot.style.left = `${boxCenterX - (dotSize / 2)}px`;
        aiDot.style.display = 'block';
    }

function submitAnswer() {
    const answer = document.getElementById('user-answer').value;
    const correctAnswer = eval(document.getElementById('current-question').textContent);
    const turnDisplay = document.getElementById('turn-display');

    // Indicate AI's turn by default
    turnDisplay.textContent = "AI's Turn";

    if (parseInt(answer) === correctAnswer) {
        const playerSteps = Math.floor(Math.random() * 6) + 1;
        console.log(`Player answered correctly. Moving player.`);
        move('player', playerSteps);
        movePlayerToPosition(playerPosition);
        // Hide the alert after 2 seconds
        setTimeout(() => {
            // Delay AI's turn
            const aiSteps = Math.floor(Math.random() * 6) + 1;
            console.log(`AI's turn. Moving AI.`);
            move('ai', aiSteps);
            moveAIToPosition(aiPosition);

            // Set the question for the player after AI's move
            document.getElementById('current-question').textContent = generateQuestion();

            // Indicate player's turn
            turnDisplay.textContent = "Your Turn";
        }, 4000); // 2 second delay
    } else {
        const playerSteps = Math.floor(Math.random() * 6) + 1;
        console.log(`Player answered incorrectly. Moving AI.`);
        move('ai', playerSteps);
        document.getElementById('current-question').textContent = generateQuestion();
        moveAIToPosition(aiPosition);

        // Indicate AI's turn
        alert("Mhmm incorrect, AI is making its move now...");

        // Delay AI's turn
        setTimeout(() => {
            // Set the question for the player after AI's move
            document.getElementById('current-question').textContent = generateQuestion();
            // Indicate player's turn
            turnDisplay.textContent = "Your Turn";
        }, 3000); // 3 second delay
    }

    // Clear user's answer after submitting
    document.getElementById('user-answer').value = '';

    // Focus on user answer input for convenience
    document.getElementById('user-answer').focus();
}
    console.log(`Generating initial question.`);
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