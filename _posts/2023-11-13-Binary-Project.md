---
toc: false
comments: false
layout: default
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather</title>

<style>
  body {
  width: 100%; 
  height:100%;
  margin:0em 0%;
  background-color:#8ec1da;
  background-image: url("https://static.vecteezy.com/system/resources/previews/016/124/733/non_2x/poker-and-casino-playing-card-black-background-vector.jpg");
  background-position: center bottom;
  animation: animatedBackground 20s linear infinite;
  -webkit-animation: animatedBackground 20s linear infinite;
}

@keyframes animatedBackground {
  from { background-position: 0 100%; }
  to { background-position: 100% 100%; }
}
@-webkit-keyframes  animatedBackground {
  from { background-position: 0 100%; }
  to { background-position: 100% 100%; }
}

.title {
  position: fixed;
  top: 10%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 70px;
  font-family: Verdana, sans-serif;
}

.playercardsbox {
  position: fixed;
  top: 50%;
  left: 30%;
  transform: translate(-50%, -50%);
  background-color: rgba(128, 128, 128, 0.5); /* Transparent gray color */
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  font-size: 30px;
  font-family: Verdana, sans-serif;
}

.hitbutton {
  position: fixed;
  top: 70%;
  left: 30%;
  transform: translate(-50%, -50%);
  background-color: rgba(38, 152, 255, 0.5);
  border: none;
  width: 10%;
  height: 10%;
  border-radius: 10px;
  font-size: 30px;
  font-family: Verdana, sans-serif;
}
</style>
</head>

<body>
    <div>
      <h1 class="title">Binary Blackjack</h1>
    </div>
    <div class="playercardsbox">
      <p><strong>Cards:</strong><br><span id="playercard1"></span><br><span id="playercard2"></span><br><span id="playercard3"></span><br><span id="playercard4"></span><br><span id="playercard5"></span><br><span id="playercard6"></span></p>
    </div>
    <div>
      <button class="hitbutton" onclick="getplayercard()">Hit</button>
    </div>


<script>
  var cardcounter = 52
  function generatecards() {
    // Function that generates a deck of cards with the 52 standard cards but with their binary blackjack values
    var numbers = ["0010", "0011", "0100", "0101", "0110", "0111", "1000", "1001", "1010", "1010", "1010", "1010", "1011"] // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, J, Q, K, A] blackjack values in binary
    var suits = ["♠︎", "♥︎", "♦︎", "♣︎"]
    var cards = []
    for (let i = 0; i < numbers.length; i++) {
      for (let j = 0; j < suits.length; j++) {
        cards.push(numbers[i] + suits[j])
      }
    }
    return cards
    //console.log(cards)
    }

  var deck = generatecards()

  function playercards() {
    // Function to connect to the HTML and replace the text with the generated cards at the start of the game
    num1 = Math.floor(Math.random() * 52)
    num2 = Math.floor(Math.random() * 51)
    card1 = deck[num1]
    deck.splice(num1, 1)
    cardcounter -= 1
    card2 = deck[num2]
    cardcounter -= 1
    deck.splice(num2, 1)
    //console.log(card1, card2)
    card1Element = document.getElementById("playercard1")
    card2Element = document.getElementById("playercard2")
    card1Element.innerHTML = card1
    card2Element.innerHTML = card2
  }

playercards()

  function getplayercard() {
    tempnum = Math.floor(Math.random() * cardcounter)
    //console.log(tempnum)
    //console.log(deck)
    card = deck[tempnum]
    //console.log(deck[tempnum])
    cardcounter -= 1
    cardElement = document.getElementById("playercard" + (52 - cardcounter).toString())
    cardElement.innerHTML = card
  }

</script>
</body>
</html>