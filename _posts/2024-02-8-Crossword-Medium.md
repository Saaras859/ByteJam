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
    .container {
        display: grid;
        grid-template-columns: repeat(7, 75px); /* Adjust box width */
        grid-template-rows: repeat(7, 75px); /* Adjust box height */
        gap: 5px; /* Smaller gap between boxes */
    }
    .whitebox {
        position: relative;
        background-color: white; /* Light gray */
        width: 75px; /* Adjust box width */
        height: 75px; /* Adjust box height */
        font-size: 24px; /* Make font size bigger */
        color: red; /* Set text color to light blue */
        font-weight: bold; /* Make text bold */
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: text; /* Set cursor to text */
    }
    .number {
        position: absolute;
        top: 0;
        left: 0;
        color: black; /* Set number color to black */
        font-size: 16px; /* Make font size smaller */
        padding: 5px; /* Add padding for spacing */
    }
    .letter {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        height: 100%;
        visibility: visible;
    }
    .blackbox {
        background-color: black; /* Light gray */
        width: 75px; /* Adjust box width */
        height: 75px; /* Adjust box height */
    }
    #game-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 20px; /* Adjust the top margin as needed */
    }
    .hint-box {
        background-color: black;
        color: white;
        border-radius: 10px;
        padding: 10px;
        font-size: 18px;
        width: 800px;
        height: 100px;
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
    }
    .input-box {
        padding: 10px;
        border-radius: 5px;
        border: 1px solid #ccc;
        font-size: 16px;
        width: 300px;
        margin-top: 10px;
    }
    .timer-box {
        position: fixed;
        top: 10%;
        left: 90%;
        transform: translate(-50%, -50%);
        background-color: black;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        font-size: 30px;
        font-family: Verdana, sans-serif;
        }
</style>
</head>
<body>
<div id="game-container">
    <div class="container">
        <!-- 81 white and black boxes -->
            <div class="whitebox" id="box1"><span class="number"></span></div>
            <div class="whitebox" id="box2"><span class="number"></span></div>
            <div class="whitebox" id="box3"><span class="number"></span></div>
            <div class="whitebox" id="box4"><span class="number"></span></div>
            <div class="whitebox" id="box5"><span class="number"></span></div>
            <div class="whitebox" id="box6"><span class="number"></span></div>
            <div class="whitebox" id="box7"><span class="number"></span></div>
            <div class="whitebox" id="box8"><span class="number"></span></div>
        <div class="blackbox"></div>
            <div class="whitebox" id="box9"><span class="number"></span></div>
        <div class="blackbox"></div>
            <div class="whitebox" id="box10"><span class="number"></span></div>
        <div class="blackbox"></div>
            <div class="whitebox" id="box11"><span class="number"></span></div>
            <div class="whitebox" id="box12"><span class="number"></span></div>
            <div class="whitebox" id="box13"><span class="number"></span></div>
            <div class="whitebox" id="box14"><span class="number"></span></div>
            <div class="whitebox" id="box15"><span class="number"></span></div>
            <div class="whitebox" id="box16"><span class="number"></span></div>
            <div class="whitebox" id="box17"><span class="number"></span></div>
            <div class="whitebox" id="box18"><span class="number"></span></div>
            <div class="whitebox" id="box19"><span class="number"></span></div>
        <div class="blackbox"></div>
            <div class="whitebox" id="box20"><span class="number"></span></div>
        <div class="blackbox"></div>
            <div class="whitebox" id="box21"><span class="number"></span></div>
        <div class="blackbox"></div>
            <div class="whitebox" id="box22"><span class="number"></span></div>
            <div class="whitebox" id="box23"><span class="number"></span></div>
            <div class="whitebox" id="box24"><span class="number"></span></div>
            <div class="whitebox" id="box25"><span class="number"></span></div>
            <div class="whitebox" id="box26"><span class="number"></span></div>
            <div class="whitebox" id="box27"><span class="number"></span></div>
            <div class="whitebox" id="box28"><span class="number"></span></div>
            <div class="whitebox" id="box29"><span class="number"></span></div>
            <div class="whitebox" id="box30"><span class="number"></span></div>
        <div class="blackbox"></div>
            <div class="whitebox" id="box31"><span class="number"></span></div>
        <div class="blackbox"></div>
            <div class="whitebox" id="box32"><span class="number"></span></div>
        <div class="blackbox"></div>
            <div class="whitebox" id="box33"><span class="number"></span></div>
            <div class="whitebox" id="box34"><span class="number"></span></div>
            <div class="whitebox" id="box35"><span class="number"></span></div>
            <div class="whitebox" id="box36"><span class="number"></span></div>
            <div class="whitebox" id="box37"><span class="number"></span></div>
            <div class="whitebox" id="box38"><span class="number"></span></div>
            <div class="whitebox" id="box39"><span class="number"></span></div>
            <div class="whitebox" id="box40"><span class="number"></span></div>  
    </div>
    <div class="hint-box">
    This is a hint box with some text.
</div>
    <div class="home-button">
        <a href="http://127.0.0.1:4100/ByteJam/2024/02/08/Main.html">Home</a>
    </div>
<input type="text" class="input-box" placeholder="Guess the word :)" autocomplete="off">
</div>
        <div class="timer-box" id="timer">02:00</div>

<script>
    // Your existing JavaScript code here
    const boxLetterMapping = {
        box1: 'F',
        box2: 'A',
        box3: 'T',
        box4: 'L',
        box5: 'A',
        box6: 'D',
        box7: 'Y',
        box8: 'A',
        box9: 'R',
        box10: 'L',
        box11: 'I',
        box12: 'C',
        box13: 'H',
        box14: 'A',
        box15: 'R',
        box16: 'L',
        box17: 'I',
        box18: 'E',
        box19: 'I',
        box20: 'G',
        box21: 'E',
        box22: 'L',
        box23: 'A',
        box24: 'V',
        box25: 'E',
        box26: 'N',
        box27: 'G',
        box28: 'E',
        box29: 'D',
        box30: 'L',
        box31: 'D',
        box32: 'R',
        box33: 'E',
        box34: 'S',
        box35: 'E',
        box36: 'Y',
        box37: 'M',
        box38: 'O',
        box39: 'U',
        box40: 'R',
    };
    const wordHints = {
        Across: {
            1: "It's not over until you hear her singing!",
            5: "Third letter of the nato phoentic alphabet",
            6: "American heavy metal band - ______ Sevenfold",
            7: "Principle skinner's first name in the Simpsons"
        },
        Down: {
            1.1: "Beauty treatments for the face",
            2: "Type of Shakesphere play",
            3: "Musical word meaning 'at a brisk speed'",
            4: "Someone who surrenders"
        }
    };
    const hintBoxMapping = {
        1: ['box1', 'box2', 'box3', 'box4', 'box5', 'box6', 'box7'], 
        1.1: ['box1','box8', 'box12', 'box19', 'box23', 'box30', 'box34'],
        6: ['box23', 'box24', 'box25', 'box26', 'box27', 'box28', 'box29'], 
        5: ['box12', 'box13', 'box14', 'box15', 'box16', 'box17', 'box18'],
        2: ['box3', 'box9', 'box14', 'box20', 'box25', 'box31', 'box36'],
        4: ['box7', 'box11', 'box18', 'box22', 'box29', 'box33', 'box40'],
        7: ['box34', 'box35', 'box36', 'box37', 'box38', 'box39', 'box40'],
        3: ['box5', 'box10', 'box16', 'box21', 'box27', 'box32', 'box38' ],
    };
    Object.keys(wordHints).forEach(direction => {
        Object.keys(wordHints[direction]).forEach(hintNumber => {
            const letters = hintBoxMapping[hintNumber].map(box => boxLetterMapping[box]);
            const hint = wordHints[direction][hintNumber];
            console.log(`The word is ${letters.join('')} and its hint is: ${hint}`);
        });
    });
    // Function to check if the user input matches the correct word for the displayed hint
let totalQuestionsAnswered = 0;
let currentWordHints;
let acrossWordsCompleted = false; // Initialize acrossWordsCompleted
let downWordsCompleted = false;
let correctAnswerCounter = 0;
let hintIndex = 1;
// Function to check if the user input matches the correct word for the displayed hint
function checkAnswer() {
    const userInput = document.querySelector('.input-box').value.trim().toUpperCase();
    const displayedHint = document.querySelector('.hint-box').innerText.trim();
    const hintNumber = parseInt(document.querySelector('.hint-box').getAttribute('data-hint'));
    if (!hintNumber) {
        console.log("No hint provided.");
        return;
    }
    if (!currentWordHints) {
        currentWordHints = wordHints['Across'];
        currentWordDirection = 'Across';
    }
    if (acrossWordsCompleted && !downWordsCompleted && currentWordDirection !== 'Down') {
        currentWordHints = wordHints['Down'];
        currentWordDirection = 'Down';
    }
    currentWordKey = Object.keys(currentWordHints).find(key => currentWordHints[key] === displayedHint);
    const correctLetters = hintBoxMapping[currentWordKey].map(box => boxLetterMapping[box]).join('');
    console.log("User Input:", userInput);
    console.log("Correct Word:", correctLetters);
    if (userInput === correctLetters) {
        correctAnswerCounter++;
        // If the answer is correct, display the word on the crossword
        hintBoxMapping[currentWordKey].forEach(boxId => {
            document.getElementById(boxId).innerText = boxLetterMapping[boxId];
        });
        console.log("Congratulations! You got it right!");
        // Clear the input box
        document.querySelector('.input-box').value = '';
        // Move to the next hint if available, or move to the next word
        const nextHintNumber = hintNumber + 1;
        const nextHint = currentWordHints[nextHintNumber];
        if (nextHint) {
            document.querySelector('.hint-box').innerText = nextHint;
            document.querySelector('.hint-box').setAttribute('data-hint', nextHintNumber);
        } else {
            totalQuestionsAnswered++;
            // If there are no more hints for this direction, mark the word as completed
            if (currentWordDirection === 'Across') {
                const nextWordKeys = Object.keys(currentWordHints);
                const nextWordIndex = nextWordKeys.indexOf(currentWordKey) + 1;
                const nextWordKey = nextWordKeys[nextWordIndex];
                // Check if all words have been completed
                if (acrossWordsCompleted && downWordsCompleted) {
                    console.log("All words completed.");
                    console.log("Well done! All words guessed correctly!");
                    // Change hint box background color to black
                    document.querySelector('.hint-box').style.backgroundColor = 'black';
                    // Display "Well done! All words guessed correctly!" in the console
                    console.log("Well done! All words guessed correctly!");
                    return;
                }
                if (nextWordKey) {
                    const nextWordHint = currentWordHints[nextWordKey];
                    document.querySelector('.hint-box').innerText = nextWordHint;
                    document.querySelector('.hint-box').setAttribute('data-hint', nextWordKey);
                    // Clear the input box and perform any other actions for the next word
                    document.querySelector('.input-box').value = '';
                    console.log("Moving to the next word.");
                } else {
                    console.log("All across words completed.");
                    acrossWordsCompleted = true;
                    if (!downWordsCompleted) {
                        currentWordHints = wordHints['Down'];
                        currentWordDirection = 'Down';
                        const firstDownHint = currentWordHints[Object.keys(currentWordHints)[0]];
                        const firstDownHintNumber = Object.keys(currentWordHints)[0];
                        document.querySelector('.hint-box').innerText = firstDownHint;
                        document.querySelector('.hint-box').setAttribute('data-hint', firstDownHintNumber);
                        // Clear the input box and perform any other actions for the next word
                        document.querySelector('.input-box').value = '';
                        console.log("Moving to the down words.");
                    } else {
                        console.log("All words completed.");
                        console.log("Well done! All words guessed correctly!");
                        // Change hint box background color to black
                        document.querySelector('.hint-box').style.backgroundColor = 'black';
                        // Display "Well done! All words guessed correctly!" in the console
                        console.log("Well done! All words guessed correctly!");
                        // Perform any necessary actions if all words are completed
                    }
                }
            } else if (currentWordDirection === 'Down') {
                const nextWordKeys = Object.keys(currentWordHints);
                const nextWordIndex = nextWordKeys.indexOf(currentWordKey) + 1;
                const nextWordKey = nextWordKeys[nextWordIndex];
                if (nextWordKey) {
                    const nextWordHint = currentWordHints[nextWordKey];
                    document.querySelector('.hint-box').innerText = nextWordHint;
                    document.querySelector('.hint-box').setAttribute('data-hint', nextWordKey);
                    // Clear the input box and perform any other actions for the next word
                    document.querySelector('.input-box').value = '';
                    console.log("Moving to the next word.");
                } else {
                    console.log("All down words completed.");
                    downWordsCompleted = true;
                    if (acrossWordsCompleted) {
                        console.log("All words completed.");
                        console.log("Well done! All words guessed correctly!");
                        // Change hint box background color to black
                        document.querySelector('.hint-box').style.backgroundColor = 'black';
                        // Display "Well done! All words guessed correctly!" in the console
                        console.log("Well done! All words guessed correctly!");
                        // Perform any necessary actions if all words are completed
                    }
                }
            }
        }
        if (totalQuestionsAnswered === 11) {
            console.log("You've answered 11 questions. Game Over.");
            // Perform any additional actions or cleanup here
            return;
        }
    } else {
        console.log("Sorry, that's not correct. Please try again.");
        alert('Incorrect word, try again');
    }
}
// Populate hint box with the first hint
populateHintBox(1);
// Listen for user input in the answer box
document.querySelector('.input-box').addEventListener('keyup', function(event) {
    if (event.key === 'Enter') {
        // If the user presses Enter, check the answer
        checkAnswer();
    }
});
function populateHintBox() {
    const hint = hintIndex % 2 === 1 ? wordHints['Across'][hintIndex] : wordHints['Down'][Math.ceil(hintIndex / 2)];
    if (hint) {
        document.querySelector('.hint-box').innerText = hint;
        document.querySelector('.hint-box').setAttribute('data-hint', hintIndex);
    } else {
        console.log("No hint provided for the specified hint number.");
    }
    hintIndex++;
}
  const timerDuration = 2 * 60; // in seconds
        let timeRemaining = timerDuration;

        // Function to start the timer
        function startTimer() {
            const timerElement = document.getElementById('timer');

            const timerInterval = setInterval(function() {
                // Calculate minutes and seconds
                const minutes = Math.floor(timeRemaining / 60);
                const seconds = timeRemaining % 60;

                // Update the timer display
                timerElement.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;

                // Decrement time remaining
                timeRemaining--;

                // If time runs out, stop the timer
                if (timeRemaining < 0) {
                    clearInterval(timerInterval);
                    // Alert the user that time is up
                    alert("Time's up!");
                    // Refresh the page
                    location.reload();
                }
            }, 1000); // Update every second
        }

        // Start the timer when the page loads
        startTimer();
</script>
</body>
</html>
