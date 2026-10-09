# Lesson Plan Builder

A single-page tool for planning a class as a sequence of timed activities and then running that plan live in the classroom with a built-in lesson timer.

Everything lives in one file, [`index.html`](index.html). There is no build step, no back end and no account: plans are saved in your browser and can be exported as files.

---

## Contents

- [Running the app](#running-the-app)
- [Planning a lesson](#planning-a-lesson)
- [Running the lesson with the timer](#running-the-lesson-with-the-timer)
- [Saving, sharing and printing](#saving-sharing-and-printing)
- [Activity library](#activity-library)
- [Starting a new plan](#starting-a-new-plan)
- [Tips for teaching with it](#tips-for-teaching-with-it)
- [Customising the app](#customising-the-app)
- [Troubleshooting](#troubleshooting)

---

## Running the app

**Simplest:** double-click `index.html` to open it in a browser.

**With a local server (recommended).** Some browser features, such as desktop notifications, work more reliably over `http://localhost`:

```sh
cd lesson_plan_app
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Press `Ctrl+C` in the terminal to stop the server.

The page loads Tailwind CSS and Google Fonts from the internet, so it needs a connection to display properly.

---

## Planning a lesson

### 1. Fill in the header

| Field | What it's for |
| --- | --- |
| **Week** / **Class** | Week 1–52 and class 1–5. These appear in the title and in exported file names. |
| **Module code** | For example `DES101`. Shown in upper case. |
| **Session title** | A short name for this class. |
| **Class length** | 1, 1.5, 2 or 3 hours. Sets the time budget. |
| **Start time** | Used to work out the clock time for every activity. |
| **Learning outcomes** | What students should be able to do by the end of the class. |

### 2. Build the activity list

Each row in the table is one activity:

- **Timings:** start and end clock times, calculated automatically from the start time and the durations of the rows above. The coloured bar shows which *chunk* the activity belongs to (see [Activity library](#activity-library)).
- **Task:** choose an activity type and edit the description. Changing the type fills in a suggested description and resource.
- **Resource:** add one or more resources from the dropdown, which become removable chips. Choose **Other…** to type your own.
- **Duration:** 5–90 minutes.
- **Row actions:** ↑ / ↓ reorder, ⧉ duplicate, ✕ delete.

To add an activity, pick a type in the dropdown under the table and click **+ Add activity**.

### 3. Check the time budget

The **Time planned** bar compares the total of all durations with the class length:

- **Blue:** time still unallocated ("*n* min left")
- **Green:** exactly on time ✓
- **Red:** over-planned ("*n* min over")

Changes save automatically in your browser as you work.

---

## Running the lesson with the timer

The timer bar sticks to the top of the page while you scroll.

1. Click **▶ Start lesson** when the class begins.
2. The timer counts down the current activity and shows:
   - the activity name and its position (for example "2 of 11")
   - what's **next**
   - **drift**: whether you are *on schedule*, *n min behind* or *n min ahead*
   - the **projected finish** time for the whole lesson
3. Use the controls as the lesson goes:

| Button | Action |
| --- | --- |
| **Next ▶** | Finish this activity and move to the next one. The actual time taken is recorded. |
| **◀ Back** | Return to the previous activity and carry on from where it was left. |
| **Pause** | Pause or resume the countdown. |
| **+5 min** | Give the current activity an extra five minutes. |
| **■ Stop** | Clear the timer. You'll be asked to confirm if the lesson isn't finished. |

The current row is highlighted in the plan table and completed rows are faded out. The timer does **not** move on by itself; you choose when to click **Next**. When an activity runs over, the countdown pulses red and the overrun counts towards drift.

The timer state is saved too, so if you refresh or close the tab by accident it carries on where it was.

### Alerts

Open **🔔 Alerts** to configure:

- **Warn before the end:** 1, 2, 3 or 5 minutes (default 2). The timer turns amber.
- **Chime:** a short sound for the warning and for time's up.
- **Desktop notifications:** a system notification, which is useful when you are presenting slides in another window. The browser will ask for permission the first time.
- **Test alert:** checks that sound and notifications work. Try it before the class starts.

### Teach mode

**⛶ Teach mode** opens a full-screen view designed for a projector or a second screen. It shows a large countdown, the task description, resource chips and what's next. The background changes colour as time runs low.

Keyboard shortcuts in teach mode (these also work with most presentation clickers):

| Key | Action |
| --- | --- |
| `→` or `Page Down` | Next activity |
| `←` or `Page Up` | Previous activity |
| `Space` | Pause / resume (or start, if the timer is idle) |
| `Esc` | Exit teach mode |

---

## Saving, sharing and printing

| Toolbar option | Produces | Use it to |
| --- | --- | --- |
| **Save plan** | A `.json` file, for example `DES101-week12-class1.json` | Keep a copy of a plan, back it up or move it to another computer. |
| **Open plan** | Loads a saved `.json` file | Reopen a plan you saved earlier. |
| **Download HTML ▸ Editable page** | A full copy of the tool with this plan built in | Share a working, editable plan with a colleague. Each copy keeps its own saved state in the browser. |
| **Download HTML ▸ Static plan (read-only)** | A plain HTML table with no scripts | Embed the plan in a website or VLE (for example Moodle or Blackboard). |
| **Print / PDF** | A clean printout with toolbars and buttons removed | Print a paper copy, or choose *Save as PDF* in the print dialog. |
| **◐** | Switches between light and dark mode | Choose the theme you prefer. |

> **Note:** auto-save uses the browser's local storage. Your plan stays in that browser on that computer, and clearing site data deletes it. Use **Save plan** to keep a permanent copy. The browser holds one working plan at a time, so save each lesson to its own file before you start the next one.

---

## Activity library

Activities are grouped into colour-coded **chunks**, which helps you structure a class into short, varied segments:

| Chunk | Colour | Activities (default minutes) |
| --- | --- | --- |
| **Opening** | Grey | Welcome (5), Starter (10), Set-up (5), Recap (10) |
| **Input** | Blue | Mini-Lecture (15), Demo (10), Example (10) |
| **Practice** | Green | Guided practice (15), Independent task (20), Pair/group activity (20) |
| **Check** | Amber | Check for understanding (5), Feedback & Discussion (10), Share (10) |
| **Break** | Rose | Break (10) |
| **Close** | Violet | Recap (5), Summary (10), Next steps (5), Directed Learning (5) |
| **Other** | Light grey | Custom activity (10) |

Built-in resources: Figma, GitHub, GitHub Desktop, Graph paper, Miro, Mobile phone, Notes, OBS Studio, Pen & Paper, Quiz, Slides, SOL, Sticky notes, UX Lab, UX Lab computer, UX Lab webcams. Use **Other…** to add anything else.

---

## Starting a new plan

The app opens with a blank plan. To start the next lesson, click **New plan** in the toolbar. After you confirm, it:

- **keeps** the week, class number, class length and start time, which usually carry over to the next lesson
- **clears** the module code, session title, learning outcomes and all activities
- **resets** the lesson timer

Click **Save plan** first if you want to keep the current lesson, because the browser only holds one working plan at a time. To reuse a structure you like, save it as a `.json` file and open it again with **Open plan**. In effect, it becomes your own template.

---

## Tips for teaching with it

- **Chunk the lesson.** Alternate *Input* (blue) with *Practice* (green) and put a *Check* (amber) after each new idea. Avoid long blue stretches.
- **Keep input short.** Mini-lectures of 10–15 minutes followed by an activity hold attention better than one long talk.
- **Plan to the minute, then leave slack.** Aim for the budget bar to be green, but keep one flexible activity (such as Independent task) near the end that you can shorten if you're behind.
- **Watch the drift, not just the countdown.** If you're "5 min behind", trim a later activity rather than rushing the current one.
- **Write outcomes first.** Then check that every activity supports at least one of them.
- **Reuse plans.** A saved plan works as your own template. Save each week as a `.json` file, then open last year's file, change the week number and adjust.

---

## Customising the app

All configuration is in the `<script>` block of `index.html`:

| Constant | Controls |
| --- | --- |
| `ACTIVITIES` | Activity types: label, chunk, colour, default minutes, default task text and default resource |
| `RESOURCES` | Resources offered in the dropdown (sorted automatically) |
| `DURATIONS` | Duration options in minutes |
| `EXTEND_SECS` | How much time **+5 min** adds |

The class length options (`#sessionLength`) and the warning times (`#optWarn`) are set in the HTML markup above the script.

---

## Troubleshooting

| Problem | Fix |
| --- | --- |
| The page looks unstyled | Check your internet connection. Tailwind loads from a CDN. |
| No chime | Click anywhere on the page first (browsers block sound until you interact), make sure **Chime** is ticked, and check the system volume. |
| Notifications don't appear | Allow notifications for the site in the browser's settings and check your OS "Do Not Disturb" or Focus mode. Serve the page over `localhost` instead of opening the file directly. |
| "That file does not look like a saved lesson plan" | Only `.json` files created with **Save plan** can be opened. |
| My plan disappeared | It's stored per browser and per address. Opening the file directly and opening it from `localhost` count as different sites. Reopen it the way you used before, or load your saved `.json`. |
