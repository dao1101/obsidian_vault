<!-- Written by TA Mohamad Ali -->
# COMP Casino

## Problem Statement

In this problem, you will complete a simplified Blackjack game written in Bash.

Most of the program has already been implemented for you. Your task is to complete the missing sections inside the `play_round()` function.

## Running the Program

Make the script executable:

```bash
chmod +x blackjack_student.sh
```

Run the program:

```bash
./blackjack_student.sh
```

---

## Game Rules

This is a simplified version of Blackjack.

### Card Values
All cards have values between `1` and `10`.

### Objective
Get as close to `21` as possible without going over.

### Busting
If your score exceeds `21`, you bust and automatically lose.

### Dealer Rules
The dealer (house):
- Must draw cards while their score is less than `17`.
- Must stop drawing cards once their score reaches `17` or higher.

### Betting
- Bets must be positive integers.
- You cannot bet more money than you currently have.
- If you win, your bet is added to your balance.
- If you lose, your bet is subtracted from your balance.
- If there is a tie, your balance does not change.

---

## Provided Variables

The following global variables have already been declared:

### Player Variables
- `PLAYER_NAME`: Stores the player's name.
- `PLAYER_BALANCE`: Stores the current balance.
- `PLAYER_BET`: Stores the active round's bet.
- `PLAYER_SCORE`: Stores the player's cumulative score.
- `PLAYER_HAND`: Array storing the player's card values (e.g., `PLAYER_HAND=(7 4 5)`).

### Dealer Variables
- `HOUSE_SCORE`: Stores the dealer's score.
- `HOUSE_HAND`: Array storing the dealer's card values.

### Result Variable
- `RESULT`: Outcome string (`"WIN"`, `"LOSE"`, or `"TIE"`).

---

## Provided Functions

The following functions are already implemented and can be referenced:

### `initialize_game()`
Prints the game rules, collects `PLAYER_NAME` and `PLAYER_BALANCE`, and validates the input.

### `reset_round()`
Resets round variables to initial states:
```bash
PLAYER_SCORE=0
HOUSE_SCORE=0
PLAYER_HAND=()
HOUSE_HAND=()
```

### `draw_card()`
Returns a pseudo-random integer between `1` and `10`.
```bash
card=$(draw_card)
```

### `deal_initial_cards()`
Deals two cards each to the player and dealer, illustrating array additions and arithmetic updates:
```bash
card=$(draw_card)
PLAYER_HAND+=("$card")
PLAYER_SCORE=$(( PLAYER_SCORE + card ))
```

---

## Your Task

Complete the missing sections inside `play_round()`:

1. **Part 1: Player Turn**
2. **Part 2: Dealer Turn**
3. **Part 3: Determine Winner**
4. **Part 4: Update Balance**

---

### Part 1: Player Turn

Prompt the player repeatedly while `PLAYER_SCORE <= 21`:

```text
(H)it or (S)tand?
```

- **If the player chooses Hit:**
  1. Draw a card: `card=$(draw_card)`
  2. Add it to the hand: `PLAYER_HAND+=("$card")`
  3. Update the score: `PLAYER_SCORE=$(( PLAYER_SCORE + card ))`
  4. Display cards: `echo "Your cards: ${PLAYER_HAND[*]}"`
  5. Display score: `echo "Your score: $PLAYER_SCORE"`

- **If the player chooses Stand:**
  End the player's turn (`break`).

---

### Part 2: Dealer Turn

If the player has not busted, the dealer draws cards while `HOUSE_SCORE < 17`:

```bash
card=$(draw_card)
HOUSE_HAND+=("$card")
HOUSE_SCORE=$(( HOUSE_SCORE + card ))
```

---

### Part 3: Determine Winner

Set `RESULT` according to the following order:

1. If `PLAYER_SCORE > 21`: `RESULT="LOSE"`
2. Else if `HOUSE_SCORE > 21`: `RESULT="WIN"`
3. Else if `PLAYER_SCORE > HOUSE_SCORE`: `RESULT="WIN"`
4. Else if `HOUSE_SCORE > PLAYER_SCORE`: `RESULT="LOSE"`
5. Otherwise: `RESULT="TIE"`

---

### Part 4: Update Balance

Update `PLAYER_BALANCE` based on `RESULT`:

- **WIN:** `PLAYER_BALANCE=$(( PLAYER_BALANCE + PLAYER_BET ))`
- **LOSE:** `PLAYER_BALANCE=$(( PLAYER_BALANCE - PLAYER_BET ))`
- **TIE:** No modification.

---

## Example Round

```text
Current balance: 100

Enter your bet: 20

Your cards: 8 5
Your score: 13

Dealer shows: 7

(H)it or (S)tand? H

You drew: 4

Your cards: 8 5 4
Your score: 17

(H)it or (S)tand? S

Dealer score: 18

Result: LOSE

Balance: 80
```

---

Only the contents of `play_round()` should be modified.
