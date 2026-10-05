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

* **Correct:** The AI said to save the hint in session state and show it outside the submit block. That fixed the hint button because toggling the checkbox reruns the page. I checked it by reading the diff and running the tests.
* **Not accepted as written:** The AI edited my code directly. I wanted to understand it first, so I had it undo the edits and explain them, then apply them.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?

A bug is fixed when its test passes. A guess of 60 against a secret of 50 should say "Too High" and "Go LOWER".

- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.

I ran `python -m pytest -q` and got 5 passed. I fixed the starter tests and added two for the hint text. I couldn't run the live game here, so the checkbox fix still needs a manual check.

- Did AI help you design or understand any tests? How?

Yes. Claude Code wrote the hint tests and explained why comparing strings gave wrong results.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
