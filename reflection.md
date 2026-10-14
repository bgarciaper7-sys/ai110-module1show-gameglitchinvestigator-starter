# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

While investigating the AI-generated guessing game, I identified several problems involving game state, comparison logic, and input validation.

**Bug 1: Incorrect high/low hints**

The game gives directions that contradict the comparison result. For example, when the secret is 6 and the guess is 50, the game says to go higher instead of lower. In `app.py`, the `check_guess()` function returns incorrect directional messages.

**Bug 2: Invalid guesses are accepted**

The game advertises a range of 1–100, but values such as 0 and 102 appear in the guess history. The `parse_guess()` function converts input into integers without checking whether the result is within the allowed range.

**Bug 3: Attempts start at the wrong value**

The initial session state sets `attempts` to 1 instead of 0. On Normal difficulty, this can cause the game to display seven attempts remaining before the player has submitted a guess.

### Bug Reproduction Logs

| Input Used / Trigger | Expected Behavior | Actual Behavior | Console Error / Output | Suspected Code Location |
|---|---|---|---|---|
| Secret 6, guess 50 | Display "Go LOWER!" | Displays "Go HIGHER!" | No console error observed | `app.py`, `check_guess()`, lines 37–40 |
| Guess 102 | Reject a number outside the range | Guess is recorded in history | No console error observed | `app.py`, `parse_guess()`, lines 14–29 |
| Initial game load on Normal | Show 8 attempts remaining | Shows 7 attempts remaining | No console error observed | `app.py`, lines 95–96 |

Additional issues identified during code inspection include inconsistent number types during comparisons, incomplete New Game resets, and attempts being counted before input validation.

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
