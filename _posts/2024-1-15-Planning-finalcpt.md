---
toc: false
comments: false
layout: default
---

# Planning for Final CPT Project

Feature 1: Face ID Login page (Backend)
Lead: Eric
Description: A Face ID Login page utilizing the face recognition package in python. Will redirect to the main home page when face and username are accepted. Will have a login system for individual users to sign up.

Feature 2: Home page (Frontend)
Lead: All
Description: Where the face ID login redirects to. Should have different sections for different features, and clickable links to each section.

Feature 4: Leaderboard (Backend)
Lead: Saaras
Description: A global leaderboard that records score throughout the whole project. Each following feature will contribute to this leaderboard, and users can log into their individual accounts to keep trying to improve their score through the different games. Utilizes backend tables to store values for each user.

Feature 3: Mathnopoly (Frontend)
Lead: Cayden
Description: A math question gets displayed each round. The User answers the math question by submitting the answer in the answer box. If the user answers the question correctly, two dice are rolled, and the user moves forward on a board based on that roll. The board has different boxes/steps with different values set to each box. The user plays against the AI, who always rolls after the users turn. Each step/box the user lands on gives or takes differing set amounts of money. The player who gets to 500$ first wins.

Feature 4: Crossword Puzzles + Tic Tac Toe (Frontend)
Lead: Sri
Description: The crossword puzzles are four-fold: easy, medium, hard, extra hard. Each has its own unique words and has a timer in the top right. The player should be displayed one clue at a time, and should have a button to refresh the clue for a new one, which makes them lose a certain amount of time on the timer. Players can earn different amounts of money for beating the crosswords, but will lose some when they lose the crossword. Tic Tac Toe is will just be a classical Tic Tac Toe game, with two bots: easy and hard. The hard bot will very rarely lose, and will mostly play the best move in the position. The easy bot will be lighter, lets the user win almost two thirds of the time, but isn't fully stupid. Tic Tac Toe will likely not link with the leaderboard, as it is too easy to win for most.

Feature 5: The Casino (Frontend)
Lead: Austin
Description: A series of games that is an online 'casino' with fake money. The user can pick between blackjack, baccarat, slot machine, or poker to play, and can bet their virtual money on the outcome of the game. In all the games, the player plays against a virtual banker, or another player in poker, and all of the logic is in javascript. The logic for poker will be simpler than in real life, there will be no betting/folding during the game, just one bet at the start of the game by the player which will double or be lost when winning, and will be connected to the leaderboard. The player should also be able to fold when first seeing their cards, but not after that. This game connects with the global leaderboard through betting systems and randomized cards/spins.