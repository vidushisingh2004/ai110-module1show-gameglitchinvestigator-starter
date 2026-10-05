# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
* It showed a guessing game, where the user had to guess the number between 0 and 100. 
* The user could choose the level of difficulty 
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
1) The hints were backwards
2) The new game button doesn't work
3) The 'easy' diffculty level  had less tries 'normal' diffculty level.
4) The hint button did not work after I reclicked it
5) The final score was incorrect (not sure how the score was calculated, got a negative number)
6) Displayed final score eventhough I had one attempt left

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
|Pressed reset button | Rest Game | No action | No ouput | 
|Pressed the hint button | Show hints | No Hint |  No ouput |
|Guess of 30 | To low | To high | No output|

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
* I used claude code

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).

* I used it to fix the reset button. AI gave me the code and I asked it to explain the logic behind it and it make sense so I implemented it and it worked, the reset button was fixed.

- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.

* **Correct suggestion:** The AI found that the hint button problem had two causes. The hint was only drawn inside `if submit:`, so toggling the checkbox (which reruns the script with `submit = False`) erased it. Also, `app.py` turned the secret into a string on every even attempt, which made `check_guess` compare strings. It suggested saving the hint in `st.session_state.last_hint` and drawing it outside the submit block, and always passing the integer secret. This was correct because it matches how Streamlit reruns work. I checked it by reading the diff and by new pytest cases for the hint text.
* **Suggestion I did not accept as written:** The AI edited `app.py` directly to fix the bugs. I wanted to understand the fixes first, so I had it undo them and explain each one with the code. I then asked for the fixes to be applied once I understood them. The AI also left the string-comparison `except TypeError` fallback in `check_guess` at first. That was a poor fit once the secret was always an int, so we removed it when moving the function into `logic_utils.py`.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?

I decided a bug was fixed when a test that failed before the change passed after it, and when the behavior matched what the code now says. For the high/low bug, a guess of 60 against a secret of 50 must return "Too High" with a "Go LOWER" message.

- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.

I ran `python -m pytest -q` and got 5 passed. The starter tests compared the whole return value to a string, but `check_guess` returns an `(outcome, message)` tuple. I changed them to check the outcome, and added two regression tests that check the hint text ("LOWER" for a too-high guess, "HIGHER" for a too-low guess). I could not run `streamlit run app.py` here because the local Streamlit install is broken (a pyarrow/protobuf mismatch), so the toggle fix still needs a manual check in the live game.

- Did AI help you design or understand any tests? How?

Yes. Claude Code noticed that the starter tests did not match the function's return type, and it wrote the regression tests. It also explained why the string comparison on even attempts gave wrong results (for example, `"9" > "10"` is `True`).

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
