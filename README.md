# LedgerMark v1.4

## A Handwritten Markup Language for Searchable Engineering and Commonplace Notebooks

**Write by hand -> photograph -> AI converts to Markdown -> search, summarize, and retrieve.**

| Field | Value |
|---|---|
| Version | 1.4 |
| Status | Trial specification |
| Primary format | Handwritten notes converted to Markdown |
| Suggested storage | Private GitHub repository |
| Author | Mark Bender |

> **Important:** LedgerMark is a personal note-organization method, not a security control. Before storing workplace information in GitHub, confirm that the repository, account, device access, and content comply with your organization's data-handling policies.

---

## Version History

| Version | Changes |
|---|---|
| 1.0 | Core structure, context, knowledge, action, and file-reference tokens |
| 1.1 | Deferred actions using `[<]` and `WAKE:` |
| 1.2 | Handwritten tables using `TBL:` and `END` |
| 1.3 | Markdown-compatible formatting tags and thread reconstruction |
| 1.4 | Consolidated prompt library with a **When to run** reference |

---

## Contents

1. [What LedgerMark Is](#1-what-ledgermark-is)
2. [Quick Start](#2-quick-start)
3. [Notebook and Repository Structure](#3-notebook-and-repository-structure)
4. [Token Reference](#4-token-reference)
5. [Writing Rules](#5-writing-rules)
6. [Worked Examples](#6-worked-examples)
7. [Threads and Scattered Conversations](#7-threads-and-scattered-conversations)
8. [Daily, Weekly, and Notebook Workflows](#8-daily-weekly-and-notebook-workflows)
9. [Core AI Prompts](#9-core-ai-prompts)
10. [Prompt Library](#10-prompt-library)
11. [Prompt Run Schedule](#11-prompt-run-schedule)
12. [Search Guide](#12-search-guide)
13. [Quality and Troubleshooting](#13-quality-and-troubleshooting)
14. [Frequently Asked Questions](#14-frequently-asked-questions)
15. [Appendix A: Front-Cover Quick Reference](#appendix-a-front-cover-quick-reference)
16. [Appendix B: Repository README](#appendix-b-repository-readme)

---

# 1. What LedgerMark Is

LedgerMark is a compact handwritten markup language for people who prefer to think and take notes on paper but need their notes to become searchable, reviewable, and reusable later.

You write ordinary notes with short tokens such as:

- `F:` for a verified fact
- `C:@Person` for a claim made by a person
- `[ ]` for an open action
- `[<] ... WAKE:` for an action deferred until a future date
- `PRJ:` for a project identifier
- `#Topic` for a reusable subject tag
- `W>` and `H>` for files stored on mutually exclusive work and home systems

At the end of the day, you photograph the notebook pages and give the images to an AI with the daily transcription prompt. The AI converts the handwritten page into structured Markdown. You then append that Markdown to the GitHub file for the physical notebook.

```text
Handwritten notebook -> page photo -> AI transcription -> Markdown -> GitHub search
```

## 1.1 Core Principles

1. **One physical notebook equals one Markdown file.**  
   Example: notebook `CB03` becomes `CB03.md`.

2. **The digital file remains chronological.**  
   Do not reorganize the original notebook file by subject. Use prompts to create project, topic, person, meeting, and thread views.

3. **Work and home notes may share the same Markdown file.**  
   Use `[W]` and `[H]` to classify entries, and use `W>` and `H>` to identify where referenced files actually reside.

4. **Facts and claims are different.**  
   `F:` means documented, measured, or verified. `C:@Person` means someone stated it, but it may still need verification.

5. **The file remembers, not the AI.**  
   Open, deferred, completed, moved, and cancelled actions remain encoded in the notebook file. Each prompt reads the file again.

6. **Original notes remain auditable.**  
   New content is appended. Earlier content is edited only to correct transcription errors or update an action status.

---

# 2. Quick Start

## 2.1 Eight Tokens to Learn First

| Token | Purpose | Example |
|---|---|---|
| `==DATE DAY==` | Start a day | `==2026-10-28 WED==` |
| `PG:` | Identify notebook and page | `PG:CB03-045` |
| `T:` | Start a timed entry | `T:1300` |
| `PRJ:` | Identify a project | `PRJ:26-014` |
| `#` | Identify a topic | `#FuseHeat` |
| `F:` | Record a fact | `F: fuse clears in 4 msec` |
| `C:` | Record an attributed claim | `C:@RButcher fuse gets hot` |
| `[ ]` | Record an open action | `[ ] request thermal data` |

## 2.2 First LedgerMark Entry

```text
==2026-10-28 WED==            PG:CB01-001
T:1300 @RButcher PRJ:26-014 #FuseHeat
  C:@RButcher fuse gets hot during operation
  ?Q is temperature rise measured?
  [ ] request thermal data from @RButcher
```

## 2.3 One-Week Trial

| Day | Practice |
|---|---|
| 1 | Use the eight core tokens and run Prompt A at the end of the day |
| 2 | Add `@Person`, `MTG:`, and consistent `#Topic` tags |
| 3 | Add `N:`, `F:`, `C:`, `SRC:`, `!D`, and `?Q` |
| 4 | Add `[X]`, `[>]`, `[-]`, `[<]`, `DUE:`, and `WAKE:` |
| 5 | Run P1 for action items and P6 for project notes |
| 6 | Try a `TBL:` table and a `FIG:` sketch reference |
| 7 | Run P12 to reconstruct a scattered topic thread |

---

# 3. Notebook and Repository Structure

## 3.1 Suggested Repository

```text
ledgermark/
├── README.md
├── LedgerMark-Manual.md
├── CB01.md
├── CB02.md
├── CB03.md
├── threads/
│   └── FuseHeat.md
└── images/
    └── CB03-045.jpg
```

The `threads/` and `images/` directories are optional. Notebook files are the authoritative chronological record. Thread files are generated views.

## 3.2 Notebook File Header

```yaml
---
spec: LedgerMark v1.4
notebook: CB03
started: 2026-10-01
closed:
pages: 001-
---
# LedgerMark Notebook CB03
```

## 3.3 Daily Markdown Structure

```markdown
## 2026-10-28 WED | PG:CB03-045

### 13:00 | PRJ: 26-014 | #FuseHeat | [W]
- People: @RButcher
- C:@RButcher Fuse gets hot during operation
- ?Q Is temperature rise measured?
- [ ] Request thermal data from @RButcher
```

---

# 4. Token Reference

## 4.1 Structure Tokens

| Token | Meaning | Example |
|---|---|---|
| `==DATE DAY==` | Day header | `==2026-10-28 WED==` |
| `PG:` | Notebook and page | `PG:CB03-045` |
| `T:` | Time in 24-hour format | `T:1300` |
| `>>` | Continues on another page | `>>PG:CB03-046` |
| `SEE:` | Related earlier or later page | `SEE:PG:CB03-045` |

## 4.2 Context Tokens

| Token | Meaning | Example |
|---|---|---|
| `MTG:` | Meeting name | `MTG:FuseReview` |
| `PRJ:` | Project identifier | `PRJ:26-014` |
| `#Topic` | Reusable topic tag | `#FuseHeat` |
| `@Person` | Person identifier | `@RButcher` |
| `[W]` | Work context | `T:1300 #FuseHeat [W]` |
| `[H]` | Home context | `T:1900 #HouseRepair [H]` |

Use consistent person and topic forms. For example, choose `@RButcher` and do not alternate among `@Ron`, `@RonButcher`, and `@RButcher`.

## 4.3 Knowledge Tokens

| Token | Meaning | Example |
|---|---|---|
| `N:` | General note or context | `N: fuse is installed in L1 only` |
| `F:` | Verified or documented fact | `F: clearing time is 4 msec` |
| `C:` | Attributed but unverified claim | `C:@RButcher fuse gets hot` |
| `SRC:` | Source of a fact or table | `SRC: supplier datasheet rev C` |
| `*I` | Your idea or insight | `*I add a thermocouple to the clip` |
| `FIG:` | Searchable label for a sketch | `FIG: fuse thermal path` |
| `TBL:` | Start and name a table | `TBL: Fuse temperature by load` |
| `END` | End a table | `END` |

### Choosing Between `F:`, `C:`, `N:`, and `*I`

| Information type | Use |
|---|---|
| Measured, specified, calculated, or documented | `F:` |
| Something another person said that is not yet verified | `C:@Person` |
| Background, context, or neutral description | `N:` |
| Your proposed explanation or improvement | `*I` |

## 4.4 Action Tokens

| Token | Meaning | Example |
|---|---|---|
| `[ ]` | Open action | `[ ] request return photos` |
| `[X]` | Completed action | `[X] request return photos` |
| `[>]` | Moved to another page or notebook | `[>] review report >>PG:CB04-002` |
| `[-]` | Cancelled or no longer required | `[-] order test fuses` |
| `[<]` | Deferred until a future date | `[<] review report WAKE:2026-12-14` |
| `WAKE:` | Date a deferred action returns | `WAKE:2026-12-14` |
| `DUE:` | Completion deadline | `DUE:2026-12-18` |
| `!!` | High priority | `!! [ ] send customer response` |
| `!D` | Decision | `!D keep F03 pending test` |
| `?Q` | Open question | `?Q is the clip temperature measured?` |

### Wake Date Versus Due Date

```text
[<] review UL 248 WAKE:2026-12-14 DUE:2026-12-18
```

- `WAKE:` means do not place the item on the active list before that date.
- `DUE:` means the item must be completed by that date.
- Once the wake date arrives, the action remains active until marked `[X]`, `[>]`, `[-]`, or deferred again.

## 4.5 Reference Tokens

| Token | Meaning | Example |
|---|---|---|
| `W>` | File accessible from the work PC | `W>SFMEA/Fuse_v3.xlsx` |
| `H>` | File accessible from the home PC | `H>Finance/Budget.xlsx` |
| `URL>` | Named web, SharePoint, or Teams reference | `URL>TeamsCh-FuseIssue` |

Every local file reference should use `W>` or `H>`.

## 4.6 Table Tokens

A table begins with `TBL:` and ends with `END`.

```text
TBL: Fuse temperature by load  SRC: thermal run 3
Load (A) | Clip (deg C) | Ambient (deg C)
10       | 48           | 25
20       | 63           | 25
30       | 78           | 25
END
```

Use `-` for an empty cell. Keep units in column headers.

## 4.7 Formatting Tags

Formatting tags let handwritten notes request Markdown formatting without using Markdown symbols that conflict with LedgerMark tokens.

| Handwritten tag | Markdown result |
|---|---|
| `<H1> Heading` | `#### Heading` |
| `<H2> Heading` | `##### Heading` |
| `<H3> Heading` | `###### Heading` |
| `<B> text` | Bold line |
| `<B>text</B>` | Bold selected text |
| `<I> text` | Italic line |
| `<I>text</I>` | Italic selected text |
| `<Q> text` | Blockquote |
| `<LI> text` | Bullet item |
| `<OL> text` | Numbered item |
| `<CODE>` ... `</CODE>` | Fenced code block |
| `<HR>` | Horizontal rule |

`<H1>` becomes a fourth-level Markdown heading because the notebook title uses `#`, the day uses `##`, and each timed entry uses `###`.

---

# 5. Writing Rules

## 5.1 General Rules

1. Write LedgerMark tokens in block capitals.
2. Use no space inside identifier tokens: `T:1300`, `PRJ:26-014`, `DUE:2026-12-18`.
3. Put a space after text tokens: `F: text`, `N: text`, `!D text`.
4. Write claims as `C:@Person claim`.
5. Put one item on each line.
6. Start every entry with `T:`.
7. A line without a token is treated as `N:`.
8. Include units in facts: `4 msec`, `30 A`, `78 deg C`.
9. Prefix every file with `W>` or `H>`.
10. Use ASCII where possible. Write `->` instead of a drawn arrow.
11. Write dates as `YYYY-MM-DD`.
12. Every `[<]` action must include `WAKE:`.
13. Write `!!` before the action box.
14. Do not erase an action. Change its state.
15. Reuse the same `#Topic` every time you return to a subject.
16. Add `SEE:` when returning to a conversation or analysis from an earlier page.

## 5.2 Table Rules

1. Name the table with `TBL:`.
2. Put the header row first.
3. Put units in headers.
4. Use six columns or fewer when possible.
5. Use `-` for empty cells.
6. Do not merge cells.
7. Do not use ditto marks.
8. Write `END` after the last row.
9. Use `>>PG:` if the table continues to another page.

## 5.3 Formatting Rules

1. Use capitalized tags such as `<B>` and `<H1>`.
2. A tag at the start of a line applies to the whole line.
3. Use closing tags when only part of a line is formatted.
4. Keep the LedgerMark semantic token first: `F: <B>78 deg C</B>`.
5. Formatting changes presentation, not meaning.

---

# 6. Worked Examples

## 6.1 Hallway Conversation Followed by a Meeting

```text
==2026-10-28 WED==            PG:CB03-045
T:1300 @RButcher PRJ:26-014 #FuseHeat
  C:@RButcher fuse gets hot during operation
  ?Q how many returned units show discoloration?

T:1315 MTG:DesignStandup PRJ:26-021 #Schedule
  N: prototype build moved one week
  [ ] update W>Schedules/26-021.mpp
```

## 6.2 Returning to the Hallway Topic Later

```text
T:1630 @RButcher PRJ:26-014 #FuseHeat SEE:PG:CB03-045
  F: 3 returns show clip discoloration  SRC: RMA log
  [ ] request photos from @RButcher DUE:2026-10-30
```

## 6.3 Fact, Claim, and Source

```text
F: fuse clearing time is 4 msec  SRC: supplier datasheet rev C
C:@RButcher fuse temperature is causing the discoloration
?Q is there a measured clip temperature?
```

## 6.4 Decision and High-Priority Action

```text
!D keep F03 until thermal testing is complete
!! [ ] obtain clip temperature data DUE:2026-11-06
```

## 6.5 Deferred Action

```text
[<] review final thermal report WAKE:2026-12-14 DUE:2026-12-18
```

Before December 14, P1 places it under **Deferred (sleeping)**. On or after December 14, P1 returns it to the active list.

## 6.6 Completing, Moving, and Cancelling

```text
[X] obtain clip temperature data DUE:2026-11-06
[>] update test plan >>PG:CB04-002
[-] order additional sample fuses
```

## 6.7 Handwritten Table

```text
TBL: Fuse options  PRJ:26-014  SRC: supplier quotes
Part | Rating (A) | Cost ($) | Note
F03  | 30         | 0.60     | current
F05  | 25         | 0.45     | alternate
END
```

Expected Markdown:

```markdown
- TBL: Fuse options — PRJ:26-014 — SRC: supplier quotes

| Part | Rating (A) | Cost ($) | Note |
|---|---:|---:|---|
| F03 | 30 | 0.60 | current |
| F05 | 25 | 0.45 | alternate |
```

## 6.8 Formatting Example

```text
T:1400 PRJ:26-014 #FuseHeat
  <H1> Thermal Findings
  <Q> Clip temperature is the limiting factor
  F: clip temperature is <B>78 deg C</B>  SRC: thermal run 3
  <H2> Next steps
  <OL> repeat on second sample
  <OL> update SFMEA
```

Expected Markdown:

```markdown
### 14:00 | PRJ: 26-014 | #FuseHeat | [W]
#### Thermal Findings
> Clip temperature is the limiting factor

- F: Clip temperature is **78 deg C** — SRC: thermal run 3

##### Next steps
1. Repeat on second sample
2. Update SFMEA
```

---

# 7. Threads and Scattered Conversations

LedgerMark keeps the notebook chronological. The AI creates a consolidated thread later.

## 7.1 Thread Linking Habit

When returning to a subject:

1. Reuse the exact `#Topic`.
2. Include the involved `@Person` when useful.
3. Add `SEE:` to the most recent related page.

Example thread:

```text
PG:CB03-045  T:1300 @RButcher #FuseHeat
PG:CB03-046  T:1630 @RButcher #FuseHeat SEE:PG:CB03-045
PG:CB03-052  T:1000 PRJ:26-014 #FuseHeat SEE:PG:CB03-046
```

P12 reconstructs the thread in date and time order. It may include untagged but likely related entries, but it must label those entries `[LIKELY]` so a person can verify them.

## 7.2 Generated Thread Files

For major topics, save the P12 result as a generated view:

```text
threads/FuseHeat.md
```

Do not move original entries out of the notebook file.

---

# 8. Daily, Weekly, and Notebook Workflows

## 8.1 Daily Workflow

1. Photograph the day's pages with the page flat and fully visible.
2. Attach the photos to the AI assistant.
3. Run **Prompt A: Daily Transcription**.
4. Compare the output with the paper and correct flags.
5. Append the output to the notebook's Markdown file.
6. Update earlier action statuses when needed.
7. Commit the change to GitHub with a message such as `CB03 2026-10-28`.

## 8.2 Weekly Review

Run these prompts each week:

1. **P1: All Open Action Items**
2. **P5: What Wakes Up Soon**
3. **P14: Claim Check**
4. **P13: Find Loose Ends**
5. **P27: Quality Check**

Then update paper and Markdown action states.

## 8.3 Starting a Notebook

- Assign the notebook ID.
- Copy the quick-reference card into the front cover.
- Run Prompt B to create the Markdown header.
- Number pages consistently.
- Carry forward active, deferred, and unresolved items.

## 8.4 Closing a Notebook

1. Run Prompt C.
2. Add the generated index near the top of the file.
3. Complete `closed:` and the final `pages:` range.
4. Mark transferred open actions `[>]` in the old notebook.
5. Rewrite them in the new notebook as `[ ]` or `[<]`.
6. Preserve `WAKE:`, `DUE:`, `!!`, project, topic, and `SEE:` information.
7. Commit with a message such as `CB03 closed`.

---

# 9. Core AI Prompts

## Prompt A: Daily Transcription

**When to run:** At the end of each writing day, or whenever a group of handwritten pages is ready for transcription.

```text
Transcribe the attached notebook page(s) from LedgerMark v1.4 handwritten notation to Markdown using these rules:

STRUCTURE
1. Output ONLY a section starting with: ## YYYY-MM-DD DAY | PG:<pages>. Do not add YAML front matter.
2. Start a new ### heading at each T: line, formatted as:
   ### HH:MM | MTG: <name> | PRJ: <number> | #<topic> | [W] or [H]
   Omit parts that are not present.
3. End each ### heading with [W] or [H]. Treat PRJ: and MTG: as work unless the page indicates otherwise. If unsure, write [W?] or [H?].
4. Put entry content below the heading. List standalone @people on one "- People:" line.
5. If an entry continues across pages using >>, merge the pages into one entry and list all pages in the day heading.

TOKENS
6. Preserve the meaning of these tokens: ==DATE==, PG:, T:, MTG:, PRJ:, #, @, W>, H>, URL>, [ ], [X], [>], [-], [<], WAKE:, DUE:, !!, !D, ?Q, *I, N:, F:, C:, SRC:, SEE:, FIG:, TBL:, END, and >>.
7. Treat any unmarked prose line as N:.
8. Keep C:@Person attribution. If a claim has no person, add [WHO?].
9. Keep facts, numbers, units, and sources exactly as written. If unclear, write [??].
10. Put !! before the action box.
11. DUE: and WAKE: dates must be YYYY-MM-DD. If unclear, write DUE:[??] or WAKE:[??].
12. Every [<] action must have WAKE:. If missing, add WAKE:[??].
13. Preserve SEE: page references exactly.

FILES, SKETCHES, AND TABLES
14. Wrap W>, H>, and URL> references in backticks. If a local file has no W> or H> prefix, mark [NO DOMAIN].
15. For FIG:, keep the label and add: [sketch on PG:<page>, see photo]. Do not invent details.
16. TBL: starts a table and END ends it. Convert it to a Markdown table. The first row is the header. Keep units in headers. Treat - as an empty cell. Keep all values exactly as written. Merge tables continued across pages. If columns are unclear, add [TABLE CHECK].

FORMATTING
17. Convert <H1>, <H2>, and <H3> to ####, #####, and ######. Never use #, ##, or ### for handwritten subheadings.
18. Convert <B> to bold, <I> to italic, <Q> to blockquote, <LI> to a bullet, <OL> to a numbered item, <CODE>...</CODE> to a fenced code block, and <HR> to a horizontal rule.
19. If a format tag and a LedgerMark token share a line, retain the semantic token and apply formatting to the text. Do not output the format tags.
20. If formatting is unclear, add [FORMAT?].

ACCURACY
21. Do not guess names, numbers, units, dates, project codes, or table values.
22. Output the result in one Markdown code block.
```

## Prompt B: New Notebook File

**When to run:** Once, when a new physical notebook is started.

```text
Create the YAML front matter for a new LedgerMark notebook file:
spec: LedgerMark v1.4
notebook: <CB04>
started: <YYYY-MM-DD>
closed: (blank)
pages: 001-
Then add: # LedgerMark Notebook <CB04>
Output in one Markdown code block.
```

## Prompt C: Notebook Close-Out Index

**When to run:** When the physical notebook is full or formally retired.

```text
From the attached LedgerMark notebook file, create a close-out index to place after the YAML header:
1. Projects: each PRJ: with dates and pages.
2. Topics: each #topic with dates and pages.
3. Meetings: each MTG: with dates and pages.
4. Decisions: each !D with date and page.
5. Facts: each F: with SRC:, date, and page.
6. Tables: each TBL: with SRC:, date, and page.
7. Claims: each C: grouped by @person, with date and page.
8. Figures: each FIG: with date and page.
9. Open items: each ?Q, [ ], and [<], including !!, DUE:, and WAKE:, with date and page.
10. File references: list W> and H> separately.
Also provide updated YAML values for closed: and pages:.
Output in one Markdown code block.
```

---

# 10. Prompt Library

Replace placeholder values in angle brackets before running a prompt.

## P1: All Open Action Items

**When to run:** Daily, at the start of work; weekly during review; anytime you ask, "What do I still owe?"

```text
Today is <YYYY-MM-DD>.
From the attached LedgerMark notebook file(s), list every active action:
- Include [ ] items.
- Include [<] items whose WAKE: date is today or earlier and label them WOKE <date>.
- Exclude [X], [>], and [-].
Group by [W] and [H], then by PRJ:.
List !! items first, then sort by DUE: date, with items having no DUE: last.
Mark DUE: dates earlier than today as OVERDUE.
Add a final section called "Deferred (sleeping)" containing [<] items whose WAKE: date is after today, sorted by WAKE:.
Show the original date and PG: for every item.
Output as a Markdown checklist.
```

## P2: Due This Week

**When to run:** Monday morning, before a planning meeting, or whenever the weekly workload changes.

```text
Today is <YYYY-MM-DD>.
From the attached LedgerMark notebook file(s), list active actions due from <START-DATE> through <END-DATE>.
Include [ ] items and [<] items whose WAKE: date is today or earlier.
Also list overdue actions.
Sort by DUE: date and show PRJ:, original date, and PG:.
Output as a Markdown checklist.
```

## P3: High-Priority Actions

**When to run:** At the beginning of a busy day, before escalation meetings, or when time is limited.

```text
Today is <YYYY-MM-DD>.
From the attached LedgerMark notebook file(s), list every active action marked !!.
Include woken [<] items and exclude sleeping [<], [X], [>], and [-].
Sort by DUE: date, mark overdue items, and show PRJ:, original date, and PG:.
Output as a Markdown checklist.
```

## P4: Actions Involving a Person

**When to run:** Before a one-on-one, follow-up conversation, email, or meeting with that person.

```text
Today is <YYYY-MM-DD>.
From the attached LedgerMark notebook file(s), list active and sleeping actions that mention <@RButcher>.
Separate:
1. Actions I owe the person.
2. Actions the person appears to owe me.
3. Deferred actions and their WAKE: dates.
Show PRJ:, DUE:, WAKE:, original date, and PG:.
Output as a Markdown checklist.
```

## P5: What Wakes Up Soon

**When to run:** Weekly, at month-end, or before planning the next month.

```text
Today is <YYYY-MM-DD>.
From the attached LedgerMark notebook file(s), list deferred actions [<] with WAKE: dates from today through <END-DATE>.
Sort by WAKE: date.
Show PRJ:, DUE:, original date, and PG:.
Flag any deferred action missing WAKE: as [NO WAKE DATE].
Output as a Markdown table.
```

## P6: All Notes on a Project

**When to run:** Before a project review, when re-entering a project after time away, or when asked for all background on a project.

```text
From the attached LedgerMark notebook file(s), collect every entry containing PRJ:<PROJECT-ID>.
Present entries in date and time order.
For each entry show date, time, PG:, MTG:, #topics, people, and all content, including tables.
End with a concise summary of facts, claims, decisions, open actions, deferred actions, questions, files, and figures.
Output as Markdown.
```

## P7: Project Timeline

**When to run:** For milestone reviews, postmortems, onboarding, or reconstructing how a decision developed.

```text
From the attached LedgerMark notebook file(s), build a timeline for PRJ:<PROJECT-ID>.
Use one row per meaningful event with columns for date, PG:, event, decision, and resulting action.
Bold decisions and completed actions.
Output as a Markdown table.
```

## P8: Decision Log

**When to run:** Before design reviews, change-control discussions, audits, or when someone asks, "Why did we do this?"

```text
From the attached LedgerMark notebook file(s), list every !D for PRJ:<PROJECT-ID>.
For each decision show date, PG:, MTG:, people present, the decision, supporting facts or sources, and any later decision that modified or reversed it.
Output as a Markdown table.
```

## P9: Facts and Sources

**When to run:** Before technical reviews, calculations, specifications, reports, or whenever source traceability matters.

```text
From the attached LedgerMark notebook file(s), list every F: and TBL: associated with PRJ:<PROJECT-ID> or <#TOPIC>.
Show fact or table name, value, units, SRC:, date, and PG:.
Mark missing sources [NO SOURCE].
Identify conflicting values without choosing one unless the notes establish which is authoritative.
Output as Markdown tables.
```

## P10: Everything Mentioning a Word or Phrase

**When to run:** When you remember a term but not the project, date, person, or page.

```text
From the attached LedgerMark notebook file(s), find every mention of <SEARCH-TERM>, including tags, prose, meeting names, file names, table cells, and figure labels.
Group results by F:, TBL:, C:, N:, !D, ?Q, actions, *I, FIG:, and file references.
Show date, time, and PG: for each result.
Output as Markdown.
```

## P11: Topic Knowledge Summary

**When to run:** Before a subject-matter review, troubleshooting session, or technical discussion.

```text
From the attached LedgerMark notebook file(s), collect entries tagged <#TOPIC> or associated with PRJ:<PROJECT-ID>.
Group into facts, tables, claims, decisions, questions, active actions, deferred actions, notes, ideas, figures, and files.
Include date and PG: for every item.
Follow SEE: references.
Flag claims that conflict with facts or tables.
Output as Markdown.
```

## P12: Thread Rollup

**When to run:** When a conversation or analysis is scattered across many pages, meetings, or notebooks.

```text
From the attached LedgerMark notebook file(s), reconstruct the full thread for <#TOPIC>.
Include entries that:
- use <#TOPIC>;
- are connected through SEE: links; or
- clearly concern the same subject and person <@PERSON>, even if untagged. Mark inferred matches [LIKELY].
Present the thread in date and time order with PG: references.
End with current facts and sources, unverified claims, decisions, open questions, active actions, deferred actions, and unresolved contradictions.
Do not rewrite the source files. This is a generated view.
Output as Markdown.
```

## P13: Find Loose Ends and Duplicate Topics

**When to run:** Weekly or after transcribing a large batch of pages.

```text
From the attached LedgerMark notebook file(s), find entries that appear related but do not share a #topic or SEE: link.
Also find near-duplicate topic tags, such as #FuseHeat and #FuseHot.
For each proposed group, show date, time, PG:, current tags, suggested canonical #topic, and the reason for the match.
Do not change the files.
Output as a Markdown table.
```

## P14: Claim Check

**When to run:** Before making a decision based on meeting statements, during weekly review, or before publishing a technical conclusion.

```text
From the attached LedgerMark notebook file(s), list every C: claim.
For each claim, search later F:, TBL:, !D, and SEE:-linked entries for support or contradiction.
Classify the claim as VERIFIED, CONTRADICTED, PARTIALLY SUPPORTED, or UNVERIFIED.
Group by @person and show claim date, PG:, evidence date, and evidence PG:.
Do not infer verification without evidence in the notes.
Output as a Markdown table.
```

## P15: Open Questions

**When to run:** Before a meeting, troubleshooting session, experiment, or project handoff.

```text
From the attached LedgerMark notebook file(s), list every ?Q.
For each question, determine whether a later F:, TBL:, N:, or !D appears to answer it.
Group by PRJ: and #topic.
Mark each OPEN, POSSIBLY ANSWERED, or ANSWERED, and show the supporting date and PG: when applicable.
Output as Markdown.
```

## P16: Idea Bank

**When to run:** During planning, brainstorming, continuous-improvement reviews, or when looking for unused ideas.

```text
From the attached LedgerMark notebook file(s), list every *I idea.
Group by [W] and [H], then by PRJ: or #topic.
Show date and PG:.
Indicate whether the idea later became an action, decision, fact, or was never revisited.
Output as Markdown.
```

## P17: Meeting History

**When to run:** Before the next occurrence of a recurring meeting or when reviewing recurring commitments.

```text
From the attached LedgerMark notebook file(s), collect every entry with MTG:<MEETING-NAME>.
For each occurrence show date, PG:, attendees, facts, claims, decisions, open questions, active actions, deferred actions, and completed actions.
End with actions still open from the meeting series.
Output as Markdown.
```

## P18: Meeting Preparation

**When to run:** Immediately before a meeting.

```text
Today is <YYYY-MM-DD>.
I am preparing for MTG:<MEETING-NAME> concerning PRJ:<PROJECT-ID> or <#TOPIC>.
Using the attached LedgerMark notebook file(s), provide:
1. Decisions from the previous meeting.
2. Active and woken actions assigned to me or others.
3. Deferred actions that wake within the next 30 days.
4. Open questions to raise.
5. Unverified or contradicted claims.
6. Key facts and tables with sources.
7. Files and figures I may need.
Keep the result concise and suitable as a one-page meeting brief.
Output as Markdown.
```

## P19: Person Summary

**When to run:** Before a one-on-one, performance conversation, stakeholder update, or follow-up call.

```text
From the attached LedgerMark notebook file(s), collect entries mentioning <@PERSON>.
Group into meetings attended, claims made, decisions involving the person, actions I owe, actions they appear to owe, open questions, and recent facts or files relevant to the relationship.
Include date and PG: for every item.
Output as Markdown.
```

## P20: File Reference Index

**When to run:** When locating a file, during project close-out, or when checking whether references are properly routed.

```text
From the attached LedgerMark notebook file(s), list every <W>> file reference. Replace <W>> with H> when searching the home system.
Remove exact duplicates but retain every date and PG: where the file was mentioned.
Show path, PRJ:, #topic, first mention, most recent mention, and all pages.
Sort by path.
Output as a Markdown table.
```

## P21: Figure and Sketch Index

**When to run:** When finding diagrams, preparing a review, or closing a notebook.

```text
From the attached LedgerMark notebook file(s), list every FIG: label.
Show description, date, PG:, PRJ:, #topic, and any SEE: references.
Output as a Markdown table.
```

## P22: Pull Project or Topic Tables

**When to run:** Before technical analysis, reporting, comparison, or data transfer.

```text
From the attached LedgerMark notebook file(s), list every TBL: associated with PRJ:<PROJECT-ID> or <#TOPIC>.
For each table show name, SRC:, date, PG:, and the complete Markdown table.
Flag inconsistent headers, units, or column counts.
Output as Markdown.
```

## P23: Convert a Table to CSV

**When to run:** When transferring a handwritten table into Excel, Power BI, MATLAB, Python, or another analysis tool.

```text
From the attached LedgerMark notebook file(s), find the table named <TABLE-NAME>.
Output only valid CSV in one code block.
Use the first table row as headers and preserve units in the headers.
Preserve empty cells as empty CSV fields.
Do not add commentary inside the code block.
```

## P24: Daily or Weekly Summary

**When to run:** End of day, end of week, for a work journal review, or to prepare a concise personal recap.

```text
From the attached LedgerMark notebook file(s), summarize entries from <START-DATE> through <END-DATE>.
Separate Work [W] and Home [H].
For each section include work performed, facts learned, decisions made, actions opened, actions completed, actions deferred, overdue items, and unresolved questions.
Use only information in the notes.
Output as Markdown in fewer than 400 words.
```

## P25: Project Status Report

**When to run:** Before a manager update, engineering review, steering meeting, or weekly project report.

```text
From the attached LedgerMark notebook file(s), draft a status update for PRJ:<PROJECT-ID> covering <START-DATE> through <END-DATE>.
Use these sections:
- Progress
- Key facts and evidence
- Decisions
- Risks and open questions
- Completed actions
- Next steps with DUE: dates
- Deferred items with WAKE: dates
Use only the notes. Mark missing information [NEEDS INPUT].
Use a professional tone and keep the report under <WORD-LIMIT> words.
```

## P26: Find Something Half-Remembered

**When to run:** Whenever you remember only part of a fact, phrase, person, time period, file, or discussion.

```text
Search the attached LedgerMark notebook file(s) for information matching this memory:
<MEMORY-DESCRIPTION>
Return the strongest matches first.
For each match show date, time, PG:, exact relevant line, and why it matches.
Mark inferred matches [LIKELY].
If there is no exact match, return the closest related entries rather than inventing an answer.
Output as Markdown.
```

## P27: Quality Check

**When to run:** Weekly, before closing a notebook, after bulk transcription, or before sharing notes.

```text
Check the attached LedgerMark notebook file(s) for:
- entries missing date, time, or PG:;
- entries missing [W] or [H] where the context is ambiguous;
- C: lines missing @person;
- F: lines missing units or SRC:;
- local file references missing W> or H>;
- invalid DUE: or WAKE: dates;
- [<] items missing WAKE:;
- TBL: blocks missing END or having uneven columns;
- near-duplicate #topic tags;
- unresolved [??], [W?], [H?], [WHO?], [NO DOMAIN], [TABLE CHECK], or [FORMAT?] flags;
- inconsistent person names;
- inconsistent project identifiers.
List every issue with date and PG: and provide the recommended correction.
Output as a Markdown checklist.
```

---

# 11. Prompt Run Schedule

## 11.1 Routine Schedule

| Frequency or event | Prompts to run | Purpose |
|---|---|---|
| End of each writing day | Prompt A | Convert handwritten pages to Markdown |
| Start of day | P1, optionally P3 | Review active and urgent actions |
| Monday or weekly planning | P2, P5 | Review deadlines and waking deferred items |
| Friday weekly review | P1, P5, P13, P14, P27 | Actions, deferred work, loose threads, claims, quality |
| Before a meeting | P18 | Create a one-page meeting brief |
| Before a one-on-one | P4, P19 | Review commitments and person-related context |
| Before a project review | P6, P8, P9, P11 | Project notes, decisions, facts, topic knowledge |
| When a subject is scattered | P12 | Reconstruct a thread |
| When locating a file or sketch | P20 or P21 | Build a reference index |
| When moving handwritten data to Excel | P22, then P23 | Find and export tables |
| End of day or week | P24 | Create a recap |
| Before a status update | P25 | Draft a project report |
| When memory is incomplete | P26 | Search by partial recollection |
| When notebook is full | Prompt C, P27 | Index and validate before close-out |

## 11.2 Quick Decision Guide

| Question | Run |
|---|---|
| What do I need to do? | P1 |
| What is urgent? | P3 |
| What is due this week? | P2 |
| What is sleeping but coming back soon? | P5 |
| What do I know about project 123? | P6 |
| What happened over time? | P7 |
| What did we decide and why? | P8 |
| Which facts are sourced? | P9 |
| Where did I mention this word? | P10 |
| What is the current state of this topic? | P11 |
| Can you combine this scattered conversation? | P12 |
| Did I use inconsistent topic tags? | P13 |
| Was that statement ever verified? | P14 |
| What questions remain open? | P15 |
| What ideas have I not used? | P16 |
| What happened in this recurring meeting? | P17 |
| What should I bring up at the next meeting? | P18 |
| What do I need to discuss with this person? | P19 |
| Where is that file? | P20 |
| Where is that sketch? | P21 |
| Show me all tables for this project | P22 |
| Put this handwritten table into Excel | P23 |
| Summarize my day or week | P24 |
| Draft my project status update | P25 |
| I remember writing something about... | P26 |
| Is my notebook file clean and consistent? | P27 |

---

# 12. Search Guide

Use GitHub search or VS Code's repository search.

| Find | Search text |
|---|---|
| Project | `PRJ:26-014` |
| Topic | `#FuseHeat` |
| Meeting | `MTG:FuseReview` |
| Person | `@RButcher` |
| Date | `## 2026-10-28` |
| Page | `CB03-045` |
| Facts | `F:` |
| Claims | `C:` |
| Claims by one person | `C:@RButcher` |
| Sources | `SRC:` |
| Decisions | `!D` |
| Questions | `?Q` |
| Open actions | `[ ]` |
| Completed actions | `[X]` |
| Deferred actions | `[<]` |
| Wake dates in a month | `WAKE:2026-12` |
| Due dates in a month | `DUE:2026-11` |
| Priority actions | `!!` |
| Moved actions | `[>]` |
| Cancelled actions | `[-]` |
| Tables | `TBL:` |
| Figures | `FIG:` |
| Work files | `W>` |
| Home files | `H>` |
| Cross-references | `SEE:` |

---

# 13. Quality and Troubleshooting

## 13.1 AI Flags

| Flag | Meaning | Correction |
|---|---|---|
| `[??]` | Handwriting was unreadable | Enter the correct text |
| `[W?]` or `[H?]` | Domain was unclear | Choose `[W]` or `[H]` |
| `[WHO?]` | Claim lacks attribution | Add `@Person` |
| `[NO DOMAIN]` | File lacks W> or H> | Add the correct file domain |
| `DUE:[??]` | Due date unclear | Enter `YYYY-MM-DD` |
| `WAKE:[??]` | Wake date unclear or missing | Enter `YYYY-MM-DD` |
| `[TABLE CHECK]` | Table structure unclear | Compare with the original page |
| `[FORMAT?]` | Formatting tag unclear | Correct the Markdown formatting |
| `[LIKELY]` | AI inferred a relationship | Verify before relying on it |

## 13.2 Common Errors

| Error | Better form |
|---|---|
| `PRJ:FuseHeat` | `PRJ:26-014 #FuseHeat` |
| `C: fuse gets hot` | `C:@RButcher fuse gets hot` |
| `F: 4` | `F: 4 msec` |
| `DUE:Friday` | `DUE:2026-10-30` |
| `[<] review report` | `[<] review report WAKE:2026-12-14` |
| `Fuse_v3.xlsx` | `W>SFMEA/Fuse_v3.xlsx` |
| `T:1pm` | `T:1300` |
| `#FuseHeat` and later `#FuseHot` | Pick one canonical topic tag |
| Table without `END` | Add `END` |

## 13.3 Handwriting Tips

- Print tokens rather than using cursive.
- Leave a visible space after a token.
- Make `[<]` pointed so it is not read as `[c]`.
- Make the dots on `!!` visible so it is not read as `11`.
- Keep `H>` distinct from `#`.
- Use a consistent crossed or slashed zero if `0` and `O` are confused.

---

# 14. Frequently Asked Questions

## Does the AI remember my notes?

No. The Markdown files remember the notes. Each prompt reads the attached files and reconstructs the desired view.

## Can an action wake up automatically?

It becomes active when a date-aware prompt such as P1 is run on or after the `WAKE:` date. LedgerMark does not create a push notification by itself. For critical items, also use Outlook, Microsoft To Do, Planner, or another reminder system.

## Can scattered notes be combined later?

Yes. Reuse the same `#Topic`, add `SEE:` links, and run P12. The original notebook remains chronological.

## Can I edit older Markdown entries?

Yes, but only to correct transcription errors or change an action state. Avoid rewriting historical content.

## Can I use LedgerMark without GitHub?

Yes. Any searchable Markdown storage works, including a local folder, SharePoint-synchronized folder, or another version-controlled repository. GitHub is useful because it provides search and history.

## Can I save notebook photos in the repository?

Yes, if policy and storage limits allow it. A predictable name such as `images/CB03-045.jpg` lets `FIG:` entries point back to the exact page.

## Can tables be moved into Excel?

Yes. Run P22 to retrieve the table and P23 to produce CSV.

## Why not use raw Markdown while handwriting?

Several Markdown symbols conflict with LedgerMark tokens. Angle-bracket formatting tags are more explicit and easier for OCR to distinguish.

---

# Appendix A: Front-Cover Quick Reference

```text
LEDGERMARK v1.4

STRUCTURE
==YYYY-MM-DD DDD==   PG:CB03-045   T:1300   >>PG:   SEE:PG:

CONTEXT
MTG:Name   PRJ:26-014   #Topic   @Person   [W] [H]

KNOWLEDGE
N: note   F: fact+units   C:@Person claim   SRC: source
*I idea   FIG: sketch label

TABLES
TBL: name   header row with units   | between columns   - empty   END

ACTIONS
[ ] open   [X] done   [>] moved   [-] cancelled   [<] deferred
WAKE:YYYY-MM-DD   DUE:YYYY-MM-DD   !! priority   !D decision   ?Q question

FILES
W>work PC   H>home PC   URL>named link

FORMAT
<H1> <H2> <H3> heading   <B> bold   <I> italic   <Q> quote
<LI> bullet   <OL> numbered   <CODE>...</CODE>   <HR>

RULES
One item per line. Units on F:. Every local file gets W> or H>.
Every [<] gets WAKE:. Reuse #Topic and SEE: when returning to a subject.
```

---

# Appendix B: Repository README

```markdown
# LedgerMark

LedgerMark is a handwritten markup language for converting paper notebooks into searchable Markdown.

## Workflow

1. Write handwritten notes with LedgerMark tokens.
2. Photograph the notebook pages.
3. Run Prompt A from `LedgerMark-Manual.md`.
4. Append the generated Markdown to the matching notebook file.
5. Commit the update.

## Repository Structure

- `LedgerMark-Manual.md` — specification, prompts, and examples
- `CB01.md`, `CB02.md`, etc. — chronological notebook files
- `threads/` — optional generated topic views
- `images/` — optional notebook page photographs

## Important Prompts

- Prompt A — daily transcription
- P1 — all open and woken actions
- P6 — all notes on a project
- P12 — reconstruct a scattered topic thread
- P18 — prepare for a meeting
- P25 — draft a project status update
- P27 — quality check

## Data Handling

Keep repositories private and follow organizational data-classification, intellectual-property, export-control, retention, and acceptable-use requirements.
```
