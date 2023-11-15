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
</style>
</head>

<body>
    <div>
      <h1 class="title">Binary Blackjack</h1>
    </div>
    <div class="playercardsbox">
      <p><strong>Cards:</strong><br><span id="playercards"></span></p>
    </div>


<script>
  function generatecards() {
    var numbers = ["0001", "0010", "0011", "0100", "0101", "0110", "0111", "1000", "1001", "1010", "1010", "1010", "1010", "1010"] // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, J, Q, K, A] blackjack values in binary
    var suits = ["♠︎", "♥︎", "♦︎", "♣︎"]
    var cards = []
    for (let i = 0; i < numbers.length; i++) {
      for (let j = 0; j < suits.length; j++) {
        cards.push(numbers[i] + suits[j])
      }
    }
    //console.log(cards)
    }
    cards1 = cards
    num1 = Math.floor(Math.random() * 52) + 1
    console.log(cards1[num1])
    console.log(cards1)
    cards1.splice(num1, 1)
    console.log(cards1)
    

</script>
</body>
</html>