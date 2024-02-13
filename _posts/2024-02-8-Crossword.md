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
        top: 5px;
        left: 5px;
        color: black; /* Set number color to black */
        font-size: 16px; /* Make font size smaller */
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
    .hint-bsox {
        background-color: black;
        color: white;
        border-radius: 10px;
        padding: 10px;
        font-size: 18px;
        width: 400px;
        height: 400px;
        top: 20%;
        left: 10%;
        text-align: center;
    }
    .hint-box-across {
        position: fixed;
        top: 50%;
        left: 18%;
        transform: translate(-50%, -50%);
        background-color: rgba(38, 152, 255, 0.3) !important;
        padding: 20px;
        width: 300px;
        height: 600px;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        font-size: 15px;
        font-family: Verdana, sans-serif;
        text-align: center;
        overflow-y: auto; /*Enable vertical scroll if needed */
    }
    .input-box {
        padding: 10px;
        border-radius: 5px;
        border: 1px solid #ccc;
        font-size: 16px;
        width: 300px;
        margin-top: 10px;
    }
</style>
</head>
<body>
<div id="game-container">
    <div class="container">
        <!-- 81 white and black boxes -->
        <div class="whitebox" id="box1"><span class="number">1</span></div>
        <div class="whitebox" id="box2"><span class="number"></span></div>
        <div class="whitebox" id="box3"><span class="number">2</span></div>
        <div class="whitebox" id="box4"><span class="number"></span></div>
        <div class="whitebox" id="box5"><span class="number">3</span></div>
        <div class="blackbox"></div>
        <div class="whitebox" id="box6"><span class="number">4</span></div>
        <div class="whitebox" id="box7"><span class="number"></span></div>
        <div class="blackbox"></div>
        <div class="whitebox" id="box8"><span class="number"></span></div>
        <div class="blackbox"></div>
        <div class="whitebox" id="box9"><span class="number">5</span></div>
        <div class="whitebox" id="box10"><span class="number"></span></div>
        <div class="whitebox" id="box11"><span class="number"></span></div>
       <div class="whitebox" id="box12"><span class="number">6</span></div>
       <div class="whitebox" id="box13"><span class="number"></span></div>
       <div class="whitebox" id="box14"><span class="number"></span></div>
        <div class="whitebox" id="box15"><span class="number">7</span></div>
        <div class="whitebox" id="box16"><span class="number"></span></div>
        <div class="blackbox"></div>
        <div class="whitebox" id="box17"><span class="number"></span></div>
        <div class="whitebox" id="box18"><span class="number"></span></div>
        <div class="blackbox"></div>
        <div class="blackbox"></div>
        <div class="whitebox" id="box19"><span class="number"></span></div>
        <div class="blackbox"></div>
        <div class="blackbox"></div>
        <div class="whitebox" id="box20"><span class="number"></span></div>
        <div class="whitebox" id="box21"><span class="number"></span></div>
        <div class="blackbox"></div>
       <div class="whitebox" id="box22"><span class="number"></span></div>
       <div class="whitebox" id="box23"><span class="number">8</span></div>
        <div class="whitebox" id="box24"><span class="number"></span></div>
        <div class="whitebox" id="box25"><span class="number">9</span></div>
        <div class="whitebox" id="box26"><span class="number"></span></div>
        <div class="whitebox" id="box27"><span class="number"></span></div>
        <div class="whitebox" id="box28"><span class="number">10</span></div>
        <div class="whitebox" id="box29"><span class="number"></span></div>
        <div class="blackbox"></div>
        <div class="whitebox" id="box30"><span class="number"></span></div>
        <div class="blackbox"></div>
        <div class="whitebox" id="box31"><span class="number"></span></div>
        <div class="whitebox" id="box32"><span class="number"></span></div>
        <div class="blackbox"></div>
        <div class="whitebox" id="box33"><span class="number"></span></div>
        <div class="whitebox" id="box34"><span class="number">11</span></div>
        <div class="whitebox" id="box35"><span class="number"></span></div>
        <div class="whitebox" id="box36"><span class="number"></span></div>
        <div class="whitebox" id="box37"><span class="number"></span></div>
    </div>
    <div class="hint-box-across">
    <h2>ACROSS</h2> <br><br>
    1: Provides security, or a sense of feeling more secured <br><br>
    6: Entertain and bring joy<br><br>
    8: European country famous for its cuisine and culture (Beside Portugal)<br><br>
    10: Lower briefly into a liquid, also a type of sauce<br><br>
    11: Give way or surrender<br><br>
    5: Not new; ancient or aged
    </div>
<input type="text" class="input-box" placeholder="Guess the word :)" autocomplete="off">
</div>
<script>
    // Your existing JavaScript code here
    const boxLetterMapping = {
        box1: 'S',
        box2: 'A',
        box3: 'F',
        box4: 'E',
        box5: 'R',
        box6: 'A',
        box7: 'E',
        box8: 'L',
        box9: 'O',
        box10: 'L',
        box11: 'D',
        box12: 'A',
        box13: 'M',
        box14: 'U',
        box15: 'S',
        box16: 'E',
        box17: 'O',
        box18: 'S',
        box19: 'I',
        box20: 'R',
        box21: 'I',
        box22: 'S',
        box23: 'P',
        box24: 'A',
        box25: 'I',
        box26: 'N',
        box27: 'D',
        box28: 'I',
        box29: 'P',
        box30: 'L',
        box31: 'E',
        box32: 'E',
        box33: 'Y',
        box34: 'I',
        box35: 'E',
        box36: 'L',
        box37: 'D',
    };
    const wordHints = {
        Across: {
            1: "Provides security, or a sense of feeling more secured",
            6: "Entertain and bring joy",
            8: "European country famous for its cuisine and culture (Beside Portugal)",
            10: "Lower briefly into a liquid, also a type of sauce",
            11: "Give way or surrender",
            5: "Not new; ancient or aged"
        },
        Down: {
            1.1: "Coastal area where the land meets the sea",
            2: "Seasonal illness caused by viruses",
            4: "Decorated or embellished",
            7: "Drink slowly in small quantities through a straw",
            9: "Type of alcoholic beverage brewed from malt and hops"
        }
    };
    const hintBoxMapping = {
        1: ['box1', 'box2', 'box3', 'box4', 'box5'], 
        1.1: ['box1','box7', 'box12', 'box18', 'box21', 'box27', 'box32'],
        6: ['box12', 'box13', 'box14', 'box15', 'box16'], 
        8: ['box22', 'box23', 'box24', 'box25', 'box26'], 
        10: ['box27', 'box28', 'box29'], 
        11: ['box33', 'box34', 'box35', 'box36', 'box37'], 
        5: ['box9', 'box10', 'box11'],
        2: ['box3', 'box8', 'box14'],
        4: ['box6', 'box11', 'box17', 'box20', 'box26', 'box31', 'box37'],
        7: ['box15', 'box19', 'box23'],
        9: ['box24', 'box30', 'box35']
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
// function populateHintBox() {
//     const hint = hintIndex % 2 === 1 ? wordHints['Across'][hintIndex] : wordHints['Down'][Math.ceil(hintIndex / 2)];
//     if (hint) {
//         document.querySelector('.hint-box').innerText = hint;
//         document.querySelector('.hint-box').setAttribute('data-hint', hintIndex);
//     } else {
//         console.log("No hint provided for the specified hint number.");
//     }
//     hintIndex++;
// }

</script>
</body>
</html>