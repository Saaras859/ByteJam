---
toc: false
comments: false
layout: default
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Binary Blackjack</title>

<style>
  body {
    width: 100%; 
    height: 100%;
    margin: 0em 0%;
    background-color: #8ec1da;
    background-image: url("https://static.vecteezy.com/system/resources/previews/016/124/733/non_2x/poker-and-casino-playing-card-black-background-vector.jpg");
    background-position: center bottom;
  }

  .title {
    position: fixed;
    top: 10%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 70px;
    font-family: Verdana, sans-serif;
  }

  .playercardsbox, .dealercardsbox, .playerscorebox, .dealerscorebox {
    position: fixed;
    top: 50%;
    transform: translate(-50%, -50%);
    background-color: rgba(128, 128, 128, 0.5);
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    font-size: 30px;
    font-family: Verdana, sans-serif;
    overflow-y: auto; /* Enable vertical scroll if needed */
  }

  .playercardsbox, .playerscorebox {
    left: 30%;
    max-height: 100%; /* Allow it to grow to the full height of the viewport */
  }

  .dealercardsbox, .dealerscorebox {
    left: 70%;
    max-height: 100%;
  }

  .playerscorebox, .dealerscorebox {
    position: fixed;
    top: 78%;
    transform: translate(-50%, -50%);
    background-color: rgba(128, 128, 128, 0.5);
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    font-size: 30px;
    font-family: Verdana, sans-serif;
  }

  .result {
    position: fixed;
    top: 43%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 65px;
    font-family: Verdana, sans-serif;
    color: red;
    display: none;
  }

  .hitbutton, .standbutton, .resetbutton {
    position: fixed;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: rgba(38, 152, 255, 0.5);
    border: none;
    width: 10%;
    height: 10%;
    border-radius: 10px;
    font-size: 30px;
    font-family: Verdana, sans-serif;
  }

  .hitbutton:hover, .standbutton:hover, .resetbutton:hover {
    background-color: rgba(38, 152, 255, 0.3) !important;
}


  .standbutton {
    top: 72%
  }

  .hitbutton {
    top: 60%
  }
  .resetbutton {
    top: 84%;
    display: block
  }
</style>
</head>

<body>
  <div>
    <h1 class="title">Binary Blackjack</h1>
  </div>
  <div class="playercardsbox" id="playercardsbox">
    <p><strong>Player Cards:</strong></p>
  </div>
  <div class="dealercardsbox" id="dealercardsbox">
    <p><strong>Dealer Cards:</strong></p>
  </div>
  <div class="playerscorebox" id="playerscorebox">
    <p><strong>Player Score:</strong><br><span id="playerscore"></span></p>
  </div>
  <div class="dealerscorebox" id="dealerscorebox">
    <p><strong>Dealer Score:</strong><br><span id="dealerscore"></span></p>
  </div>
  <div class="result" id="result">Bust!</div>
  <div>
    <button class="hitbutton" onclick="getplayercard()">Hit</button>
    <button class="standbutton" onclick="stand()">Stand</button>
    <button class="resetbutton" onclick="resetGame()">Reset</button>
  </div>

<script>
  var cardcounter = 52;
  var playercardcounter = 0;
  var dealercardcounter = 0;
  var playerBusted = false;

  function generatecards() {
    var numbers = ["2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A"];
    var suits = ["♠︎", "♥︎", "♦︎", "♣︎"];
    var cards = [];
    for (let i = 0; i < numbers.length; i++) {
      for (let j = 0; j < suits.length; j++) {
        cards.push(numbers[i] + suits[j]);
      }
    }
    return cards;
  }

  var deck = generatecards();

  function playercards() {
    num1 = Math.floor(Math.random() * 52);
    num2 = Math.floor(Math.random() * 51);
    card1 = deck[num1]//tobinary(deck[num1]);
    deck.splice(num1, 1);
    cardcounter -= 1;
    card2 = deck[num2]//tobinary(deck[num2]);
    cardcounter -= 1;
    deck.splice(num2, 1);
    card1Element = document.getElementById("playercardsbox");
    card1Element.innerHTML += card1 + "<br>";
    card1Element.innerHTML += card2 + "<br>";
    playercardcounter = 2;
    calculatePlayerScore()
  }

  function dealercards() {
    num1 = Math.floor(Math.random() * 50);
    num2 = Math.floor(Math.random() * 49);
    dealercard1 = deck[num1];
    deck.splice(num1, 1);
    cardcounter -= 1;
    dealercard2 = deck[num2];
    cardcounter -= 1;
    deck.splice(num2, 1);
    dealercard1Element = document.getElementById("dealercardsbox");
    dealercard1Element.innerHTML += dealercard1 + "<br>";
    dealercard1Element.innerHTML += dealercard2 + "<br>";
    dealercardcounter = 2;
    calculateDealerScore()
  }

  function calculatePlayerScore() {
    var playerCards = document.getElementById("playercardsbox").textContent;
    var cardValues = playerCards.match(/\d+|A|J|Q|K/g);
    var sum = 0;

    if (cardValues) {
      for (var i = 0; i < cardValues.length; i++) {
        var value = 0;
        if (cardValues[i] === "A") {
          value = 11;
        } else if (["J", "Q", "K"].includes(cardValues[i])) {
          value = 10;
        } else {
          value = parseInt(cardValues[i]);
        }
        sum += value;
      }
    }

    // Reassign value of Ace if needed
    for (var i = 0; i < cardValues.length; i++) {
      if (cardValues[i] === "A" && sum > 21) {
        sum -= 10; // Reassign Ace value to 1
      }
    }

    document.getElementById("playerscore").innerText = sum;
    return sum;
  }

  function calculateDealerScore() {
    var dealerCards = document.getElementById("dealercardsbox").textContent;
    var cardValues = dealerCards.match(/\d+|A|J|Q|K/g);
    var sum = 0;

    if (cardValues) {
      for (var i = 0; i < cardValues.length; i++) {
        var value = 0;
        if (cardValues[i] === "A") {
          value = 11;
        } else if (["J", "Q", "K"].includes(cardValues[i])) {
          value = 10;
        } else {
          value = parseInt(cardValues[i]);
        }
        sum += value;
      }
    }
    // Reassign value of Ace if needed
    for (var i = 0; i < cardValues.length; i++) {
      if (cardValues[i] === "A" && sum > 21) {
        sum -= 10; // Reassign Ace value to 1
      }
    }
    document.getElementById("dealerscore").innerText = sum;
    return sum;
  }

  function getplayercard() {
    if (!playerBusted) {
      tempnum = Math.floor(Math.random() * cardcounter);
      temp = deck[tempnum];
      card = temp//tobinary(temp)
      cardcounter -= 1;
      cardElement = document.getElementById("playercardsbox");
      cardElement.innerHTML += card + "<br>";
      playercardcounter += 1;

      var playerScore = calculatePlayerScore();
      if (playerScore > 21) {
        handlePlayerBust();
      }
    }
  }

  function handlePlayerBust() {
    playerBusted = true;
    document.getElementById("result").innerText = "Bust!";
    document.getElementById("result").style.display = "block";
  }

  function stand() {
    // Execute dealer logic
    if (!playerBusted) {
      if (calculateDealerScore() > calculatePlayerScore()) {
      compareScores()
      }
      while (calculateDealerScore() < 17) {
        getdealercard();
      }
    }

    // Compare scores and determine the winner
    compareScores();
  }

  function getdealercard() {
    tempnum = Math.floor(Math.random() * cardcounter);
    card = deck[tempnum];
    cardcounter -= 1;
    cardElement = document.getElementById("dealercardsbox");
    cardElement.innerHTML += card + "<br>";

    calculateDealerScore();
  }

  function compareScores() {
    var playerScore = calculatePlayerScore();
    var dealerScore = calculateDealerScore();

    if (playerScore > 21) {
      handlePlayerBust();
    } else if (dealerScore > 21 || playerScore > dealerScore) {
      document.getElementById("result").innerText = "You Win!";
      document.getElementById("result").style.display = "block";
    } else if (playerScore === dealerScore) {
      document.getElementById("result").innerText = "It's a Tie!";
      document.getElementById("result").style.display = "block";
    } else {
      document.getElementById("result").innerText = "You Lose!";
      document.getElementById("result").style.display = "block";
    }
  }
  function resetGame() {
    // Reset card counters
    cardcounter = 52;
    playercardcounter = 0;
    dealercardcounter = 0;
    // Clear player and dealer cards
    document.getElementById("playercardsbox").innerHTML = "<p><strong>Player Cards:</strong></p>";
    document.getElementById("dealercardsbox").innerHTML = "<p><strong>Dealer Cards:</strong></p>";
    // Reset scores
    document.getElementById("playerscore").innerText = "";
    document.getElementById("dealerscore").innerText = "";
    // Hide result message
    document.getElementById("result").style.display = "none";
    // Reset bust
    playerBusted = false
    // Generate a new deck of cards
    deck = generatecards();
    // Deal new cards
    playercards();
    dealercards();
  }

  function cardtobinary(decimalnum) {
    value = decimalnum
    if (decimalnum[0] === "A") {
      value = 11;
    } 
    else if (["J", "Q", "K", "10"].includes(decimalnum[0])) {
      value = 10;
    }
    console.log(decimalnum)
    if (decimalnum[1] == 0) {
      suit = decimalnum[2]
    }
    else {
      suit = decimalnum[1]
    }
    decimalNumber = parseInt(value)
    decimaltemp = parseInt(value)
    // Convert decimal to binary using bitwise operations
    let binaryResult = "";
    while (decimalNumber > 0) {
        // Get the remainder when dividing by 2 (0 or 1)
        let remainder = decimalNumber % 2;
        // Add the remainder to the front of the result string
        binaryResult = remainder + binaryResult;
        // Update decimal number by integer division
        decimalNumber = Math.floor(decimalNumber / 2);
    }
    if (decimaltemp == 0) {
        binaryResult = "0";
    }
    //console.log(suit)
    var output = String(binaryResult) + suit
    while (output.length != 5) {
    output = "0" + output
    }
    //console.log(output)
    return output
  }
  
  function tobinary(decimalnum) {
    decimalNumber = parseInt(value)
    decimaltemp = parseInt(value)
    let binaryResult = "";
    while (decimalNumber > 0) {
        // Get the remainder when dividing by 2 (0 or 1)
        let remainder = decimalNumber % 2;
        // Add the remainder to the front of the result string
        binaryResult = remainder + binaryResult;
        // Update decimal number by integer division
        decimalNumber = Math.floor(decimalNumber / 2);
    }
    if (decimaltemp == 0) {
        binaryResult = "0";
    }
    //console.log(binaryResult)
    return binaryResult
  }

  function cardtodecimal(binarynum) {

  }

  function todecimal(binarynum) {
    // Convert binary to decimal using the parseInt function
    var decimalResult = parseInt(binarynum, 2);
    return String(decimalResult);
  }

playercards();
dealercards();
calculatePlayerScore();
calculateDealerScore();
</script>
</body>
</html>
