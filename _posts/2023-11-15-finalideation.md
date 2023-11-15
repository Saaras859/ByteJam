---
toc: false
comments: false
layout: default
---


# Blackjack Game Rules

## Overview

- **Players**: 2 (Computer vs Human)
- **Objective**: Reach a card sum closest to 21 without exceeding it.

## Card Values

- **Number Cards**: Face value (2-10)
- **Face Cards** (Jack, Queen, King): 10
- **Ace**: 1 or 11 (player's choice)

## Gameplay

1. **Initial Deal**: Each player receives two random cards. Card values range from 1 to 11.
2. **Player's Turn**:
   - **Draw Option**: Player can draw additional cards to get closer to 21.
   - **Stand Option**: Player can choose to stop drawing cards.
   - **Bust**: If total sum exceeds 21, the player automatically loses.
3. **Dealer's (Computer's) Turn**:
   - **Mandatory Draw**: Dealer must draw cards until the total is 17 or more.
   - **Stand**: Dealer stands if the sum is 17 or more.
   - **Bust**: If dealer's total exceeds 21, the dealer automatically loses.
4. **Conclusion**:
   - **Player Wins**: If player's total is greater than the dealer's and ≤ 21.
   - **Dealer Wins**: If dealer's total is greater than the player's and ≤ 21.
   - **Bust Rule**: Player or dealer automatically loses if their total exceeds 21.

### Additional Notes:

- Ensure a fair random function for card drawing.
- Implement UI with two buttons: "Draw" for drawing cards, "Stand" to end turn.
- The game continues until either player stands or busts.
- The winner is determined by comparing the totals of the player and the dealer.
