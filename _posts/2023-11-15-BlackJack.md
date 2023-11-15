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
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 20px;
        }
        #result {
            font-size: 24px;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>Binary Blackjack</h1>
    <button onclick="startGame()">Start Game</button>
    <p id="result"></p>

    <script>
        function startGame() {
            // Initialize deck
            let deck = initializeDeck();

            // Deal initial cards
            let playerHand = dealCard(deck);
            let dealerHand = dealCard(deck);

            // Display hands
            document.getElementById('result').innerHTML = `
                Player: ${binaryToHuman(playerHand)}<br>
                Dealer: ${binaryToHuman(dealerHand)}
            `;
        }

        function initializeDeck() {
            // Create a deck of cards represented in binary
            let deck = [];
            for (let i = 0; i < 4; i++) {
                for (let j = 1; j <= 13; j++) {
                    deck.push(decimalToBinary(j) + decimalToBinary(i));
                }
            }
            return deck;
        }

        function dealCard(deck) {
            // Randomly select a card from the deck
            let randomIndex = Math.floor(Math.random() * deck.length);
            let card = deck.splice(randomIndex, 1)[0];
            return card;
        }

        function binaryToHuman(card) {
            // Convert binary card representation to human-readable format
            let suit = binaryToSuit(card.slice(0, 4));
            let rank = binaryToRank(card.slice(4));
            return `${rank} of ${suit}`;
        }

        function binaryToSuit(binary) {
            // Convert binary suit representation to human-readable format
            let suits = ['Hearts', 'Diamonds', 'Clubs', 'Spades'];
            let index = parseInt(binary, 2);
            return suits[index];
        }

        function binaryToRank(binary) {
            // Convert binary rank representation to human-readable format
            let ranks = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'Jack', 'Queen', 'King', 'Ace'];
            let index = parseInt(binary, 2) - 1;
            return ranks[index];
        }

        function decimalToBinary(decimal) {
            // Convert decimal number to 4-bit binary representation
            return ('0000' + (decimal >>> 0).toString(2)).slice(-4);
        }
    </script>
</body>
</html>
