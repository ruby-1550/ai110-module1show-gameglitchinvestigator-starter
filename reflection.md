# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- Bug 1: On Normal, there was no correct answer even after trying all possibilities. I expected one of the guesses in the Normal range to eventually win, but none of the numbers I tried ever produced a correct result.
- Bug 2: On Easy, the hint told me to guess higher than the maximum described value (100). I expected hints to stay within the stated range, but it told me to go above 100 even though the description capped the range at 100.
- Bug 3: The New Game button didn’t work as expected and blocked guessing. I expected it to reset the game and let me keep playing, but after pressing it I couldn’t enter guesses in any game.
- Bug 4: The Show hint toggle didn’t appear to work. I expected hints to appear when toggled.

---

## 2. How did you use AI as a teammate?

- I used ChatGPT and Copilot in VS Code, using `#file:app.py` and `#file:logic_utils.py` so the AI could see how the UI and logic connect.
- Correct suggestion: The AI suggested that the “Too High/Too Low” hints were reversed in the comparison logic. That was correct. I verified it by updating `check_guess` and running `python3 -m pytest -q`, which passed and showed the hint message matched the expected direction.
- Incorrect/misleading suggestion: The AI suggested that the “Normal mode has no correct answer” bug was caused by the difficulty range alone, but the code review showed the range was fine and the issue was likely elsewhere. I verified this by checking `get_range_for_difficulty` and then running the game to see that the range displayed correctly even though the glitch still appeared.
- Step 3: Ask AI for Help. I opened Copilot, highlighted the Normal-difficulty logic, and used Inline Chat to ask: “Explain this logic step-by-step. On Normal, there was no correct answer even after trying all possibilities—what in the code could cause that?”

---

## 3. Debugging and testing your fixes

- I decided a bug was fixed only after the behavior matched the expected hint and the tests passed.
- I ran `python3 -m pytest -q` and saw all tests pass, including a new test asserting that a guess of 60 vs a secret of 50 returns “Too High” with the “Go LOWER!” hint.
- I also launched the app with Streamlit and manually checked that the hint text now aligned with the guess direction.
- AI helped by suggesting a focused test case that checks both the outcome and the hint message.

---

## 4. What did you learn about Streamlit and state?

- Streamlit reruns your script from top to bottom on every interaction, so any non‑state variables reset unless you store them.
- Session state is like a small memory dictionary that survives those reruns, which is how values like the secret number persist.
- If you don’t put game data into `st.session_state`, it will look like the app is “forgetting” or changing things randomly.
- I would explain it as “Streamlit refreshes the page logic every click, and session state is the safe place for anything you want to keep.”

---

## 5. Looking ahead: your developer habits

- I want to keep the habit of writing a focused test right after each fix, because it made it easy to confirm the bug was truly resolved.
- Next time, I will challenge AI suggestions sooner by checking the actual code paths before I assume the diagnosis is correct.
- This project reminded me that AI can be very helpful for brainstorming and refactoring, but it can still miss the real root cause without careful validation.
- I now treat AI output as a starting point that I must verify with tests and manual runs.
