# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 Project Overview

Game Glitch Investigator is a Python number-guessing game built with Streamlit. The player selects a difficulty level, guesses a secret number, and receives hints to help find the correct answer before running out of attempts.

The original AI-generated game contained several bugs affecting the hints, input validation, scoring, and game state. My goal was to investigate these problems, use AI as a coding teammate, repair the application, and verify the fixes through automated and manual testing.

## 🛠️ Setup

1. Install dependencies:

   `pip install -r requirements.txt`

2. Start the Streamlit application:

   `python -m streamlit run app.py`

3. Open the local URL displayed in the terminal.

4. Select a difficulty level and start guessing.

## 🎯 Game Features

The repaired game includes three difficulty levels:

| Difficulty | Number Range | Maximum Attempts |
|---|---|---|
| Easy | 1–20 | 6 |
| Normal | 1–100 | 8 |
| Hard | 1–50 | 5 |

The game provides higher/lower hints, tracks attempts and scores, rejects invalid inputs, and allows players to start a new game.

## 📝 Document Your Experience

### Game Purpose

The purpose of the game is to guess a randomly generated secret number within a limited number of attempts. Players use the hints after each guess to narrow down the possible answer.

### Bugs Identified

- **Incorrect hints:** The game sometimes instructed players to guess higher when their guess was already above the secret number.
- **Invalid input handling:** Numbers outside the selected difficulty's range were accepted and recorded.
- **Incorrect attempt counter:** The game started with one attempt already counted.
- **Difficulty switching:** Changing difficulty did not always reset the secret number and previous game progress.
- **New Game reset:** Starting another game did not consistently clear the score, history, and game status.
- **Scoring inconsistency:** Some incorrect high guesses increased the score instead of decreasing it.
- **Delayed status updates:** The displayed attempts remaining could lag behind the actual game state.

### Fixes Applied

I used Claude in VS Code to investigate and propose fixes, while ChatGPT helped me understand the code and debugging process.

- Corrected the comparison logic so the game displays the appropriate higher/lower hints.
- Refactored reusable game logic into `logic_utils.py`.
- Improved `parse_guess()` to reject invalid or out-of-range inputs before updating game state.
- Corrected the attempt counter to start at zero.
- Added consistent game resets when changing difficulty or selecting New Game.
- Fixed the scoring logic so incorrect guesses subtract five points.
- Updated the Streamlit status display so information refreshes correctly.
- Added automated tests using pytest and Streamlit AppTest.

I reviewed and manually tested the fixes rather than relying only on AI-generated solutions.

## 📸 Demo Walkthrough

The following example illustrates how the repaired game works.

1. The player opens the application and selects **Easy**, which uses numbers from 1 to 20 and allows six attempts.
2. Suppose the secret number is **12**. The player enters **5**, and the game responds with **"Go HIGHER!"** The attempt counter increases to 1, and the score becomes -5.
3. The player enters **18**, and the game responds with **"Go LOWER!"** The attempt counter increases to 2, and the score becomes -10.
4. The player enters **25**, which is outside the Easy difficulty range. The game rejects the input without increasing the attempt counter or changing the score.
5. The player enters **12**, and the game recognizes the correct guess, displays a winning result, and updates the score.
6. The player clicks **New Game**, and the application generates another secret number within the selected difficulty's range. Attempts, score, and guess history reset.

## 🧪 Test Results

I used pytest and Streamlit AppTest to verify the repaired game logic and interactions.

```text
107 passed
0 failed
```

Of the 107 automated tests, 15 were Streamlit AppTest tests.

I also manually verified input validation, difficulty switching, game resets, directional hints, and scoring behavior in the browser.

## 🤖 AI Collaboration

I used Claude to investigate bugs, suggest code changes, refactor functions, and generate tests. I used ChatGPT to help explain Python logic, Streamlit session state, and testing concepts.

I reviewed AI suggestions before applying them and verified the results through automated tests and manual gameplay.

For additional details, see `reflection.md` and `ai_interactions.md`.

## 🚀 Stretch Features

- **SF7: Test Generation:** Used AI to generate and improve automated tests.
- **SF8: Agent Workflow:** Used Claude to assist with multi-file code changes and debugging.
