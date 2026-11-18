# Finals Review Quizzes

Free, self-contained practice quizzes for finals review. No sign-up, no install, no server: open a quiz in your browser and start practicing.

**Live site:** https://charloaf.github.io/BAIT/

## The quizzes

| Quiz | Covers | Format |
|---|---|---|
| [Networking](networking-quiz.html) | Modules 4–10: physical layer through basic router configuration | Multiple choice, plus typed binary / decimal / hex conversions (scrap paper only, no calculator) |
| [Hardware](hardware-quiz.html) | CompTIA A+ Core 1 (220-1101), Modules 1–8 | Multiple choice |
| [PowerShell & CLI](powershell-quiz.html) | CP3126, Modules 1–17: Command Prompt first, then PowerShell | Multiple choice, plus a terminal-practice mode |
| [Math](math-quiz.html) | Math 1521, Units 1–4: number systems, set theory, Boolean algebra, normal distribution | Multiple choice |

The landing page ([index.html](index.html)) links to all of them, so one link is all you need to share.

## Features

Every quiz works the same way, so once you've used one you've used them all.

**Building a quiz**
- **Pick your modules.** Tick any combination of modules. Shift+click selects a range, and there are Select all and Clear buttons.
- **Choose how many questions.** The quiz remembers your last number. Questions are drawn at random from what you haven't done yet.
- **Shuffle answer choices** and **hide each question's module until you've answered** are both optional.

**Taking a quiz**
- Keyboard shortcuts: press `1`–`4` to answer and `Enter` for the next question.
- Hints are available on many questions.
- You get an explanation after every answer, whether you were right or wrong.
- A timer and running score are shown at the top.

**After a quiz**
- Your score is broken down by module, so you can see which areas need work.
- Every question you missed is listed with your answer, the correct answer and the explanation.
- **Retry missed questions** starts a new quiz with only the ones you got wrong.

**Progress that sticks**
- Questions you've already answered are left out of future quizzes, so you keep seeing new material. A counter shows how many you've completed, and each module shows how many are left.
- **Reset completed questions** starts you over (click twice to confirm).
- **Bad question** removes a question you think is wrong from your quizzes, and lists removed questions so you can report them.
- Light and dark mode.

**Quiz-specific extras**
- **Networking:** typed conversion questions (binary, decimal, hex, dotted-decimal IPs) are freshly generated every time. Answers are checked forgivingly, so spacing, case, `0x` prefixes and missing leading zeros are all fine.
- **PowerShell:** **Test 1** and **Test 2** buttons next to Select all and Clear tick exactly the modules each test covers (Test 1: modules 1–12, Test 2: modules 11–13). A **Terminal practice** mode with step-by-step scenarios. You type commands into a practice terminal, and wrong commands get a realistic error and a hint. Nothing you type is ever run; answers are checked against a built-in answer key.
- **Math:** four modules, one per unit of the course (Number Systems, Set Theory, Boolean Algebra, Normal Distribution and Statistics). Answers to the number-system, set, Venn and normal-table questions were computed by script, and the explanations show the working.
- Networking, Hardware and PowerShell each have a few hidden joke questions that very occasionally replace a normal one. They never change how many questions you asked for. The Math quiz has none.

## Privacy

Everything runs in your browser. There are no accounts, no tracking and no server storing anything. Your progress (completed questions, removed questions, theme, last question count) is saved in your own browser's local storage, which means:

- It stays on the device and browser you used. A different phone or browser starts fresh.
- Clearing your browser's site data also clears your progress.
- Private/incognito windows won't remember anything between visits.

## How the project works

Each quiz is **one standalone HTML file** containing its own styles, question bank and quiz engine. There is no build step and no dependencies.

```
index.html             landing page that links to each quiz
networking-quiz.html   quizzes (one self-contained file each)
hardware-quiz.html
powershell-quiz.html
math-quiz.html
```

You can open any of these files directly in a browser to try changes locally.

### Anatomy of a quiz file

Inside each quiz file's `<script>`:

- `COURSE`: the title, subtitle, module names, and (for quizzes with generated typed questions) the generator settings.
- `BANK`: the questions, in this shape:
  ```js
  { "m": 3, "q": "Question text?", "o": ["A", "B", "C", "D"], "a": 2, "e": "Explanation shown after answering.", "h": "Optional hint" }
  ```
  `m` is the module number and `a` is the 0-based index of the correct option.
- `EGG`: the hidden joke questions (empty in the Math quiz).
- The quiz engine, which is shared code. All the quizzes should keep using the same version of it.

### Things to know when editing

- Saved progress is keyed by each quiz's **title** (`COURSE.title`) and by each question's **exact text**. Renaming a quiz or rewording a question means people's saved progress no longer matches it.
- Module numbers in `BANK` must exist in `COURSE.modules`, or they'll show up unlabeled.

### Adding a new quiz

1. Copy the quiz file into the repo root.
2. Add a card for it in `index.html`.
3. Commit and push.

## Deployment

The site is served by GitHub Pages straight from the `main` branch. Every push to `main` is published automatically, usually within a minute or two, so there is no separate deploy step.
