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
    animation: animatedBackground 20s linear infinite;
    -webkit-animation: animatedBackground 20s linear infinite;
  }

  @keyframes animatedBackground {
    from { background-position: 0 100%; }
    to { background-position: 100% 100%; }
  }
  @-webkit-keyframes animatedBackground {
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

  .playercardsbox, .dealercardsbox {
    position: fixed;
    top: 50%;
    transform: translate(-50%, -50%);
    background-color: rgba(128, 128, 128, 0.5);
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    font-size: 30px;
    font-family: Verdana, sans-serif;
  }

  .playercardsbox {
    left: 30%; /* Adjusted to 30% width */
  }

  .dealercardsbox {
    left: 70%;
  }

  .hitbutton {
    position: fixed;
    top: 70%;
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
    <p><strong>Dealer Cards:</strong><br><span id="dealercard1"></span><br><span id="dealercard2"></span></p>
  </div>
  <div>
    <button class="hitbutton" onclick="getplayercard()">Hit</button>
  </div>

<script>
  var cardcounter = 52;
  var playercardcounter = 0;
  var dealercardcounter = 0;

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
    card1 = deck[num1];
    deck.splice(num1, 1);
    cardcounter -= 1;
    card2 = deck[num2];
    cardcounter -= 1;
    deck.splice(num2, 1);
    card1Element = document.getElementById("playercardsbox");
    card1Element.innerHTML += card1 + "<br>";
    card1Element.innerHTML += card2 + "<br>";
    playercardcounter = 2;
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
    dealercard1Element = document.getElementById("dealercard1");
    dealercard2Element = document.getElementById("dealercard2");
    dealercard1Element.innerHTML = dealercard1;
    dealercard2Element.innerHTML = dealercard2;
    dealercardcounter = 2;
  }

  playercards();
  dealercards();

  function getplayercard() {
    tempnum = Math.floor(Math.random() * cardcounter);
    card = deck[tempnum];
    cardcounter -= 1;
    cardElement = document.getElementById("playercardsbox");
    cardElement.innerHTML += card + "<br>";
    playercardcounter += 1;
  }

</script>
</body>
</html>
