LedgerMark v1.3
A Handwritten Markup Language for Engineering Notebooks
Write by hand → photograph → AI converts to Markdown → search everything
Version	1.3
Date	2026-10-23
Author	Mark Bender
Version History
Version	Changes
1.0	Core, context, knowledge, action and reference tokens
1.1	Deferred actions: [<] and WAKE:
1.2	Tables: TBL: and END
1.3	Formatting tags (Markdown-compatible), thread linking, prompt library renumbered
Contents
	1. Welcome to LedgerMark
	2. Quick Start
	3. Token Reference
	4. Writing Rules
	5. Worked Examples
	6. Threads: Scattered Conversations
	7. Workflows
	8. Core Prompts
	9. Prompt Library
	10. Search Guide
	11. FAQ
	• Appendix A: Quick Reference Card
	• Appendix B: Repository README
	• Appendix C: Converting This Manual to Word or PDF

1. Welcome to LedgerMark
What It Is
LedgerMark is a small set of short, uppercase tokens that you write in a paper notebook as you take notes. At the end of the day you photograph the pages, and an AI turns them into structured, searchable Markdown stored in GitHub.
You keep thinking on paper and can still find everything later.
Why LedgerMark
Problem	LedgerMark solution
Paper notes can't be searched	AI transcribes them into searchable Markdown
Actions get lost in meeting notes	Action tokens ([ ], !!, DUE:) are pulled out automatically
"Who said that? Was it verified?"	Facts (F:) are kept separate from claims (C:@person)
"Which computer is that file on?"	W> (work PC) and H> (home PC) file routing
Deferred items get forgotten	[<] with WAKE: brings them back on a chosen date
Sketches and tables are lost when digitized	FIG: labels sketches, and TBL: turns hand-drawn tables into real tables
Conversations are scattered across pages	Shared #Topic tags and SEE: links let the AI rebuild the thread
What Makes It Different
LedgerMark builds on proven ideas: Bullet Journal's rapid logging, the plain-text todo.txt format and the engineering lab notebook. It differs from them in three ways:
	1. It's analog first. You need no app and no special notebook, only a pen.
	2. It separates facts from claims. Every opinion is tied to the person who said it, so it can be verified later.
	3. It's designed for AI. The tokens are meant to be parsed by AI, not just read by people.
How It Works
Handwritten page  ->  Photo  ->  AI + Prompt A  ->  Markdown  ->  GitHub (CB03.md)
  (with tokens)                  (reads + structures)             (search anywhere)
Principle	Meaning
One notebook = one file	Notebook CB03 becomes CB03.md
Work and home in one file	Each entry is tagged [W] or [H]
W> / H>	Shows which PC holds a referenced file
The log stays in time order	Related entries are linked with tags and SEE:, never moved
Spec version	Each file header records spec: LedgerMark v1.3
Storage	A private GitHub repo named ledgermark

2. Quick Start
The 8 Tokens to Learn First
Token	Use it for	Example
==DATE DAY==	Start of each day	==2026-10-23 FRI==
T:	Start of each entry	T:0930
MTG:	Meeting name	MTG:FuseReview
PRJ:	Project number	PRJ:26-014
F:	A fact you learned	F: fuse clears in 4 msec
C:	Someone's claim	C:@JSmith fuse runs hot
[ ]	An action	[ ] update SFMEA
?Q	An open question	?Q temp rise measured?
Your First Page
==2026-10-23 FRI==            PG:CB01-001
T:0930 MTG:FuseReview PRJ:26-014
  F: fuse clears in 4 msec
  C:@JSmith fuse runs hot
  ?Q temp rise measured?
  [ ] update SFMEA
That's a complete LedgerMark entry.
One-Week Trial Plan
Day	Do this
1	Use only the 8 core tokens. Run Prompt A at the end of the day.
2	Add @ (people) and # (topics).
3	Add N:, !D (decisions) and W>/H> file references.
4	Add !!, DUE: and [<] with WAKE: to your actions.
5	Run P1 (open actions) and P6 (project notes). Notice what you can find now.
6–7	Try TBL: tables, FIG: sketches and formatting tags as you need them.
For the first two weeks, check every transcription closely. You'll quickly learn which handwritten tokens the AI misreads.
Setup Checklist
	• ☐ Pick a paper notebook and write its ID on the cover (e.g., CB01)
	• ☐ Copy the Quick Reference Card (Appendix A) inside the front cover
	• ☐ Create a private GitHub repo named ledgermark and add the README (Appendix B)
	• ☐ Run Prompt B to create CB01.md
	• ☐ Save Prompt A somewhere you can paste it quickly

3. Token Reference
3.1 Structure Tokens: where and when
Token	Meaning	Example
==DATE DAY==	Day header	==2026-10-23 FRI==
PG:	Notebook and page	PG:CB03-045
T:	Time (24h). Starts a new entry	T:0930
>>	Continued on another page	>>PG:CB03-047
SEE:	Link to a related earlier page	SEE:PG:CB03-012
✅ T:1400 ❌ T:2pm ✅ PG:CB03-045 ❌ p.45
3.2 Context Tokens: what it's about
Token	Meaning	Example
MTG:	Meeting name (CamelCase, no spaces)	MTG:FuseReview
PRJ:	Project number only	PRJ:26-014
#	Topic or keyword	#FuseHeat
@	Person (first initial + last name)	@JSmith
[W] / [H]	Work or home entry (optional)	T:1900 #Investing [H]
T:0930 MTG:FuseReview PRJ:26-014 #FuseHeat
T:1100 MTG:DesignStandup PRJ:26-021
T:1500 @JSmith #FuseHeat
T:2030 #HouseRepairs #Furnace [H]
✅ PRJ:26-014 #FuseHeat ❌ PRJ:FuseHeat
3.3 Knowledge Tokens: what you learned
Token	Meaning	Example
N:	Note or context	N: fuse is in the L1 leg only
F:	Fact, always with units	F: fuse clears in 4 msec
C:	Claim, with the person	C:@JSmith fuse runs hot
SRC:	Source of a fact or table	SRC: manufacturer datasheet
*I	Your own idea	*I add L2 fault to template
FIG:	Sketch label	FIG: L1/L2 fuse path sketch
TBL:	Starts a table and names it	TBL: Fuse temp rise by load
END	Ends a table	END
F: max ambient 52 °C  SRC: spec rev C sec 3.2
F: inrush 18 A for 10 msec  SRC: scope capture
C:@MLee customer won't accept removal
N: 3 field returns discussed, no root cause yet
*I thermocouple on fuse clip during next run
FIG: thermal test setup with TC locations
Choosing a knowledge token
If it is…	Use
Measured, specified or documented	F:
Rows and columns of data	TBL: … END
Someone's unverified statement	C:@person
Background or context	N:
Your own thinking	*I
A drawing	FIG:
3.4 Action Tokens: what to do
Token	Meaning	Example
[ ]	Open action	[ ] send email @MLee
[X]	Done	[X] update SFMEA
[>]	Moved to another page or notebook	[>] write test plan >>PG:CB04-002
[-]	Cancelled	[-] order test fuses
[<]	Deferred until a wake date	[<] review UL 248 WAKE:2026-12-14
WAKE:	Date a deferred action reappears	WAKE:2026-12-14
DUE:	Deadline	DUE:2026-10-30
!!	High priority (written before the box)	!! [ ] get temp data
!D	Decision	!D keep F03 pending test
?Q	Open question	?Q who owns field data?
WAKE: vs. DUE:
	• WAKE: is the date the action comes back onto your list.
	• DUE: is the date it must be finished.
	• You can use both: [<] review UL 248 WAKE:2026-12-14 DUE:2026-12-18
The action lifecycle
[ ] open  ->  [X] done
          ->  [-] cancelled
          ->  [>] moved to another page or notebook
          ->  [<] deferred (sleeps until WAKE:, then counts as open again)
✅ !! [ ] task DUE:2026-10-30 ❌ [ ] task !! due Friday
3.5 Reference Tokens: where files live
Token	Meaning	Example
W>	File on the Work PC	W>SFMEA/Fuse_v3.xlsx
H>	File on the Home PC	H>Finance/Budget.xlsx
URL>	Web or SharePoint link (short label)	URL>TeamsCh-FuseIssue
✅ [ ] update W>SFMEA/Fuse_v3.xlsx ❌ [ ] update Fuse_v3.xlsx
3.6 Formatting Tags: how it looks
Write	Meaning	Markdown output
<H1> text	Heading, level 1	#### text
<H2> text	Heading, level 2	##### text
<H3> text	Heading, level 3	###### text
<B> text / `word	Bold (whole line / enclosed words)	**text**
<I> text / <I>word</I>	Italic	*text*
<Q> text	Quote or callout	> text
<LI> text	Bullet item	- text
<OL> text	Numbered item	1. text
<CODE> … </CODE>	Exact-text block	Fenced code block
<HR>	Divider line	---
Why <H1> becomes ####: the file already uses # for the notebook title, ## for days and ### for entries. Your handwritten headings sit inside an entry, so they start at ####. This keeps the structure that searches and prompts rely on.
Formatting tags change only how text looks. A fact is still F: and an action is still [ ].

4. Writing Rules
4.1 General Rules
	1. Write tokens in BLOCK CAPITALS.
	2. ID tokens take no space before the value: PRJ:26-014, T:0930, DUE:2026-10-30, WAKE:2026-12-14
	3. Text tokens take a space before the text: F: …, N: …, ?Q …, !D …
	4. C: is followed directly by @person: C:@JSmith …
	5. Write one item per line.
	6. Start every entry with T:, and indent the lines under it.
	7. A line without a token is treated as N:.
	8. Always include units on F: lines.
	9. Every file reference needs W> or H>.
	10. Use ASCII only: ->, not →, and -, not •.
	11. Start each day with ==DATE DAY== and PG:, and write PG: again on each new page.
	12. PRJ: takes the number only.
	13. Write !! before the checkbox.
	14. Write all dates (DUE:, WAKE:) as YYYY-MM-DD.
	15. Every [<] needs a WAKE: date. Pick a workday.
	16. Label every sketch with FIG:.
	17. Never erase actions. Change the box to [X], [>], [-] or [<].
	18. When you come back to a topic, reuse the same #Topic and add SEE: to its last entry.
	19. Leave a small gap after each token.
4.2 Table Rules
	1. Write TBL: and a short name on its own line. Add SRC: if you have one.
	2. The first row is the headers, with units in the headers: Load (A), Temp (°C).
	3. Draw a ruled grid, or separate the columns with |.
	4. Write - in empty cells. Don't leave them blank.
	5. Repeat values in full. No ditto marks.
	6. One value per cell, with no merged cells.
	7. Keep tables to 6 columns or fewer.
	8. Write END on its own line after the last row.
	9. If a table runs onto the next page, write >>PG: and continue it there.
4.3 Formatting Rules
	1. Write tags in CAPITALS inside < >.
	2. A tag at the start of a line applies to the whole line.
	3. To format only part of a line, use a closing tag: <B>4 msec</B>.
	4. Put the token first and the formatting after it: F: <B>fuse clears in 4 msec</B>.
	5. Draw and > with sharp angles.
4.4 Common Mistakes
Mistake	Problem	Fix
PRJ:FuseHeat	PRJ takes numbers only	PRJ:26-014 #FuseHeat
C: fuse runs hot	No person	C:@JSmith fuse runs hot
F: 4	No units	F: 4 msec
DUE:Fri	Ambiguous date	DUE:2026-10-30
[<] review spec	No wake date	[<] review spec WAKE:2026-12-14
Fuse_v3.xlsx	No domain	W>SFMEA/Fuse_v3.xlsx
T:2pm	Wrong format	T:1400
→ or •	OCR misreads it	-> or -
Erasing a done action	History is lost	Change to [X] or [-]
[ ] task !!	Priority in the wrong place	!! [ ] task
Unlabeled sketch	Can't be found	FIG: description
Table with no END	AI can't tell where it stops	Add END
Blank table cells	Columns shift	Use -
#FuseHeat then #FuseHot	Thread is split in two	Reuse the exact tag
4.5 Handwriting Traps
Written	Can be misread as	Prevention
F:	E:	Keep the lower bar of F short
C:	(:	Close the C clearly
[-]	[ ]	Make the dash bold
[<]	[c]	Draw a sharp, pointed 
!!	11	Make the dots clear
H>	#	Leave a gap between H and >
<B>	(B) or 8	Sharp angles, then a gap
0	O	Put a slash through zeros

5. Worked Examples
Example 1: Formal project meeting
Handwritten
==2026-10-23 FRI==            PG:CB03-045
T:0930 MTG:FuseReview PRJ:26-014 #FuseHeat
  @JSmith @MLee @KPatel
  F: fuse clears in 4 msec  SRC: datasheet
  C:@JSmith fuse runs hot under load
  C:@KPatel connector is the real issue
  N: F03 removal saves $0.60/unit
  ?Q is fuse temp rise measured?
  !D keep F03 pending temp test
  !! [ ] get temp rise data DUE:2026-10-30
  [ ] update SFMEA W>SFMEA/Fuse_v3.xlsx
AI output
## 2026-10-23 FRI | PG:CB03-045
### 09:30 | MTG: FuseReview | PRJ: 26-014 | #FuseHeat | [W]
- People: @JSmith @MLee @KPatel
- F: Fuse clears in 4 msec — SRC: datasheet
- C:@JSmith Fuse runs hot under load
- C:@KPatel Connector is the real issue
- N: F03 removal saves $0.60/unit
- ?Q Is fuse temp rise measured?
- !D Keep F03 pending temp test
- !! [ ] Get temp rise data DUE:2026-10-30
- [ ] Update SFMEA — `W>SFMEA/Fuse_v3.xlsx`

Example 2: Hallway conversation (no meeting)
T:1115 @JSmith #FuseHeat PRJ:26-014
  C:@JSmith saw discoloration on 2 returned units
  ?Q which serial numbers?
  [ ] ask @JSmith for return photos DUE:2026-10-24
You don't need MTG: here. The @person and the topic are enough.
Example 3: Desk analysis with a sketch
T:1330 PRJ:26-014 #FuseHeat #ThermalAnalysis
  N: reviewing thermal path from fuse to housing
  F: clip rated 105 °C  SRC: supplier catalog p.42
  FIG: thermal path fuse -> clip -> PCB -> housing
  *I add thermocouple at clip for next test
  SEE:PG:CB03-045
  W>Analysis/Thermal_26-014.xlsx
The AI writes the sketch line as FIG: … — [sketch on PG:CB03-046, see photo].
Example 4: Home entries
T:1900 #Investing [H]
  F: fund yield 4.2%  SRC: fund website
  *I rebalance portfolio in Jan
  [ ] update H>Finance/Budget.xlsx DUE:2026-11-01
T:2030 #HouseRepairs #Furnace [H]
  N: filter is 16x25x1
  [ ] order filters
  H>House/FurnaceManual.pdf
Example 5: Mixed work and home day
==2026-10-26 MON==            PG:CB03-048
T:0800 MTG:DesignStandup PRJ:26-021
  N: schedule slipped 1 week
  [ ] update Gantt W>Schedules/26-021.mpp
T:1230 #Personal [H]
  [ ] call dentist
T:1500 PRJ:26-014 #FuseHeat
  F: test chamber booked 2026-10-29
The AI tags these three entries [W], [H] and [W].
Example 6: Entry continued across pages
Bottom of page 045
  ?Q who has the field data?
  >>PG:CB03-046
Top of page 046
PG:CB03-046
  (cont. MTG:FuseReview)
  !D run thermal test next week
Photograph both pages together, and the AI merges them into one entry.
Example 7: Closing out an action later
On the original page, by hand:
!! [X] get temp rise data DUE:2026-10-30
On today's page:
==2026-10-30 FRI==            PG:CB03-055
T:1000 PRJ:26-014 #FuseHeat
  F: clip temp 78 °C at full load  SRC: thermal run 3
  SEE:PG:CB03-045
  W>TestData/Thermal/Run3.csv
In CB03.md, change the original line from [ ] to [X].
Example 8: Cancelled action
[-] order test fuses          (chamber test uses stock parts)
Keep the line. [-] shows you dropped it on purpose.
Example 9: Deferring an action
Writing a new deferred action
==2026-10-23 FRI==            PG:CB03-045
T:1600 PRJ:26-014 #FuseHeat
  [<] review UL 248 sec 14 WAKE:2026-12-14
  N: wait until thermal test report is released
Deferring an action you wrote earlier
	1. On paper, change [ ] to [<] and add WAKE:2026-12-14.
	2. Make the same change on that line in CB03.md.
	3. Optional: on today's page, write N: deferred UL 248 review to Dec SEE:PG:CB03-031.
What P1 (open actions) shows over time
Date	P1 shows
Before Dec 14	Under Deferred (sleeping) only
Dec 14	In the main list as WOKE TODAY
After Dec 14	Stays in the main list as WOKE 2026-12-14 until you close it
Example 10: Carrying actions into a new notebook
Old notebook, CB03
[>] write test plan >>PG:CB04-002
[>] review UL 248 WAKE:2026-12-14 >>PG:CB04-002
New notebook, CB04, page 002
==2026-12-01 TUE==            PG:CB04-002
T:0800 #CarriedForward
  [ ] write test plan  SEE:PG:CB03-061
  [<] review UL 248 WAKE:2026-12-14  SEE:PG:CB03-045
Example 11: Claim contradicted by a fact
(PG:CB03-045)  C:@KPatel connector is the real issue
(PG:CB03-058)  F: connector temp 41 °C, well below rating  SRC: thermal run 3
               SEE:PG:CB03-045
               N: connector theory not supported
Prompt P14 marks this claim as CONTRADICTED.
Example 12: Tables
Style 1: drawn grid
TBL: Fuse temp rise by load  SRC: thermal run 3
+----------+-----------+----------+
| Load (A) | Clip (°C) | Amb (°C) |
+----------+-----------+----------+
| 10       | 48        | 25       |
| 20       | 63        | 25       |
| 30       | 78        | 25       |
+----------+-----------+----------+
END
Style 2: pipe rows (faster to write)
TBL: Fuse options  PRJ:26-014
Part | Rating (A) | Cost ($) | Note
F03  | 30         | 0.60     | current
F05  | 25         | 0.45     | -
END
AI output (Style 1)
- TBL: Fuse temp rise by load — SRC: thermal run 3

| Load (A) | Clip (°C) | Amb (°C) |
|---|---|---|
| 10 | 48 | 25 |
| 20 | 63 | 25 |
| 30 | 78 | 25 |
Example 13: Formatted page
Handwritten
T:1400 PRJ:26-014 #FuseHeat
  <H1> Thermal Findings Summary
  <Q> Clip temperature is the limiting factor, not the fuse body
  <H2> Key results
  F: clip temp <B>78 °C</B> at full load  SRC: thermal run 3
  F: clip rated 105 °C  SRC: supplier catalog
  <H2> Next steps
  <OL> confirm with 2nd sample
  <OL> update SFMEA
  <HR>
  <I> draft - not reviewed yet
AI output
### 14:00 | PRJ: 26-014 | #FuseHeat | [W]
#### Thermal Findings Summary
> Clip temperature is the limiting factor, not the fuse body
##### Key results
- F: Clip temp **78 °C** at full load — SRC: thermal run 3
- F: Clip rated 105 °C — SRC: supplier catalog

##### Next steps
1. Confirm with 2nd sample
2. Update SFMEA
---
*Draft - not reviewed yet*

6. Threads: Scattered Conversations
The Situation
A conversation often starts in one place, gets interrupted by other work, and continues later, sometimes much later.
13:00      Hallway talk with Kim about fuse heating
13:15      Unrelated meeting (different project)
16:30      Back to Kim's topic
Next week  Test data arrives on the same topic
The Approach
Your notebook stays a time-ordered log, and you never rewrite it. When you need the whole conversation, the AI pulls the pieces together into a thread view (Prompt P12).
How well that works depends on the clues you leave. Each time you come back to a topic, write:
	1. The same #Topic you used the first time
	2. The same @person, if they're involved
	3. SEE:PG:<page> pointing to the most recent entry on that topic
Example
Page 045, 13:00: the conversation starts
T:1300 @KPatel #FuseHeat PRJ:26-014
  C:@KPatel fuse clip discolors on returns
  ?Q how many units affected?
Page 045, 13:15: an unrelated meeting
T:1315 MTG:DesignStandup PRJ:26-021
  N: schedule slipped 1 week
Page 046, 16:30: back to the topic
T:1630 #FuseHeat @KPatel SEE:PG:CB03-045
  F: 3 returns show discoloration  SRC: RMA log
  [ ] request photos from @KPatel DUE:2026-10-27
Page 052, a week later
T:1000 #FuseHeat PRJ:26-014 SEE:PG:CB03-046
  F: clip temp 78 °C at full load  SRC: thermal run 3
  !D add clip temp to SFMEA
The shared #FuseHeat tag and the chain of SEE: links tie all four pieces together.
Saving a Thread Summary (optional)
For long-running topics, save the P12 output as its own file:
ledgermark/
  CB03.md
  CB04.md
  threads/
    FuseHeat.md      <- P12 output, re-run when needed
A thread file is a view, and you can regenerate it whenever you like. Never edit notebook files to merge threads.
Tips
	• Give the topic a tag the first time it comes up, even if it's just a hallway chat.
	• Reuse tags exactly. #FuseHeat and #FuseHot count as two separate threads.
	• Point SEE: to the most recent entry, so the links form a chain.
	• Run P13 each week to find related entries you forgot to link.

7. Workflows
7.1 Daily Workflow (about 3 minutes)
Step	Action
1	Photograph the day's pages: flat, good light, whole page in frame
2	Open your AI assistant and attach the photos
3	Paste Prompt A
4	Check the output and fix any flags (see 7.2)
5	Paste the result at the end of the notebook file (e.g., CB03.md)
6	Update any earlier lines whose status changed ([X], [>], [-], [<])
7	Commit with a message like CB03 2026-10-23
Only ever add new entries at the end of the file. The one exception is changing an action's status on an earlier line.
7.2 Flags to Fix
Flag	Meaning	Fix
[??]	Word couldn't be read	Type the correct word
[W?] / [H?]	Work or home is unclear	Change to [W] or [H]
[WHO?]	Claim has no person	Add @Person
[NO DOMAIN]	File reference missing W> or H>	Add the prefix
DUE:[??] / WAKE:[??]	Date is unclear	Type it as YYYY-MM-DD
[TABLE CHECK]	Table columns are unclear	Compare with the page and fix
[FORMAT?]	Formatting tag is unclear	Fix the formatting by hand
7.3 Weekly Review (Fridays)
	1. Attach the current notebook file.
	2. Run P1 (all open actions) and P5 (what wakes up soon).
	3. Deal with OVERDUE, WOKE and !! items first.
	4. Run P14 (claim check) and plan how to verify the important claims.
	5. Run P13 (loose ends) and add SEE: links on today's page.
	6. On paper, mark items [X], [-] or [<] as needed.
7.4 Starting a New Notebook
	• ☐ Write the notebook ID on the cover (e.g., CB04)
	• ☐ Copy the Quick Reference Card inside the front cover
	• ☐ Run Prompt B to create CB04.md
	• ☐ Use page 001 or 002 for carried-forward items
7.5 Closing a Full Notebook
	• ☐ Run Prompt C and paste the index at the top of the old file
	• ☐ Update the YAML closed: and pages: fields
	• ☐ Mark the open [ ] items you're carrying over as [>], on paper and in the file
	• ☐ Carry forward every [<] item with its WAKE: date
	• ☐ Rewrite carried items in the new notebook with SEE:PG:<old page>
	• ☐ Carry over open ?Q items and important unverified C: items
	• ☐ Mark dropped items [-]
	• ☐ Commit with the message CB03 closed

8. Core Prompts
Copy the prompts as plain text into your AI assistant.
Prompt A: Daily Transcription (every day)
Transcribe the attached notebook page(s) from LedgerMark v1.3 handwritten notation to Markdown using these rules:
STRUCTURE
1. Output ONLY a section starting with: ## YYYY-MM-DD DAY | PG:<pages>. No YAML front matter.
2. Start a new ### heading at each T: line, formatted as:
   ### HH:MM | MTG: <name> | PRJ: <number> | #<topic> | [W] or [H]
   Omit any part not present.
3. End each ### heading with [W] (work) or [H] (home) based on content.
   PRJ: and MTG: = [W]. If unsure, write [W?] or [H?].
4. Put lines under each entry as bullets. List @people on one "- People:" line.
5. If an entry continues across pages (>>), merge it into one ### section and list all pages in the ## header.
TOKENS
6. Preserve all tokens exactly: ==DATE==, PG:, T:, MTG:, PRJ:, #, @, W>, H>, URL>, [ ], [X], [>], [-], [<], WAKE:, DUE:, !!, !D, ?Q, *I, N:, F:, C:, SRC:, SEE:, FIG:, TBL:, >>.
7. Any line without a token = note; prefix it with N:.
8. C: lines must keep the @person attribution, e.g. "C:@JSmith ...". If none is written, flag **[WHO?]**.
9. F: lines: keep numbers and units exactly as written. If a number or unit is unclear, mark [??]. Keep SRC: on the same bullet.
10. !! goes at the start of the bullet, before the checkbox, e.g. "- !! [ ] ...".
11. DUE: and WAKE: dates must be YYYY-MM-DD. If unclear, mark DUE:[??] or WAKE:[??].
12. [<] = deferred action and must have a WAKE: date; if missing, flag WAKE:[??].
13. SEE: lines: keep the page reference exactly, e.g. "SEE:PG:CB03-012".
FILES, SKETCHES, TABLES
14. Wrap file references in backticks, e.g. `W>SFMEA/Fuse_v3.xlsx`. Flag any file reference missing W> or H> with **[NO DOMAIN]**.
15. FIG: lines: keep the label and add "— [sketch on PG:<page>, see photo]". Do not invent details of the drawing.
16. TBL: starts a table, END ends it. Convert to a Markdown table: first row = headers, keep units in headers, keep every value exactly as written, "-" = empty cell. Put the TBL: name and any SRC: as a bullet above the table. Unreadable cell = [??]. Merge tables continued across pages. If the column count is unclear, flag **[TABLE CHECK]**.

FORMATTING
17. Convert <H1>, <H2>, <H3> to ####, #####, ###### (never #, ##, or ###). <B> = bold, <I> = italic: at line start they apply to the whole line; with a closing tag (</B>, </I>) only to the enclosed text. <Q> = blockquote (> ). <LI> = bullet (- ). <OL> = numbered item, numbered in sequence. <CODE>...</CODE> = fenced code block, text kept exactly. <HR> = ---. When a format tag and a token share a line, keep the token and format the text. Do not output the tags themselves. If a tag is unclear, flag **[FORMAT?]**.
ACCURACY
18. Mark unreadable words as [??]. Do not guess names, numbers, units, dates, or project codes.
19. Output in a single Markdown code block.
Prompt B: New Notebook File (once per notebook)
Create the YAML front matter for a new LedgerMark notebook file:
spec: LedgerMark v1.3
notebook: <CB04>
started: <YYYY-MM-DD>
closed: (blank)
pages: 001-
Then add a line: # LedgerMark Notebook <CB04>
Output in a single Markdown code block.
Prompt C: Notebook Close-Out Index (when a notebook is full)
From the attached LedgerMark notebook file, create an index to place at the top of the file:
1. Projects: each PRJ: with the dates and pages where it appears.
2. Topics: each #topic with dates and pages.
3. Meetings: each MTG: with date and page.
4. Decisions: every !D with date and page.
5. Facts: every F: with its SRC: (if any), date and page.
6. Tables: every TBL: name with SRC:, date and page.
7. Claims: every C: grouped by @person, with date and page.
8. Figures: every FIG: label with date and page.
9. Open items: every ?Q, every [ ], and every [<] (with WAKE:), including !! and DUE:, with date and page.
10. File references: list W> and H> references separately.
Also update the YAML: closed: <last entry date>, pages: 001-<last page>.
Output in a single Markdown code block.
Notebook File Template
---
spec: LedgerMark v1.3
notebook: CB03
started: 2026-10-01
closed:
pages: 001-
---
# LedgerMark Notebook CB03
## 2026-10-23 FRI | PG:CB03-045
### 09:30 | MTG: FuseReview | PRJ: 26-014 | #FuseHeat | [W]
- People: @JSmith @MLee
- F: Fuse clears in 4 msec — SRC: datasheet
- C:@JSmith Fuse runs hot under load
- !! [ ] Get temp rise data DUE:2026-10-30
- [<] Review UL 248 sec 14 WAKE:2026-12-14
- [ ] Update SFMEA — `W>SFMEA/Fuse_v3.xlsx`

### 19:00 | #Investing | [H]
- *I Rebalance portfolio in Jan — `H>Finance/Budget.xlsx`


9. Prompt Library
How to use: attach one or more notebook files, copy a prompt, replace anything in <angle brackets>, and run it.
	• Start date-sensitive prompts with "Today is …", because the AI needs today's date to work out what's overdue or woken.
	• To search across several notebooks, attach all of their files.
Quick Picker
I want…	Prompt
All open actions	P1
What's due this week	P2
Urgent items	P3
Actions involving one person	P4
What wakes up soon	P5
Everything on a project	P6
Project history	P7
What we decided	P8
Facts with sources	P9
Anything mentioning a word	P10
Topic summary before a review	P11
A whole scattered conversation	P12
Entries that should be linked	P13
Claims to check	P14
Unanswered questions	P15
My ideas	P16
Past meetings	P17
Prep for a meeting	P18
Prep for a 1:1	P19
Where a file is	P20
Where a sketch is	P21
All tables on a topic	P22
A table in Excel	P23
Day or week recap	P24
Status update	P25
"I wrote it somewhere…"	P26
Clean up errors	P27
9.1 Actions & Deadlines
P1: All Open Action Items
Today is <YYYY-MM-DD>.
From the attached LedgerMark notebook file(s), list every open action:
- [ ] items
- [<] items whose WAKE: date is today or earlier. Mark these **WOKE <date>**.
Exclude [X], [>], and [-].
Group by [W] and [H], then by PRJ:. List !! items first, then sort by DUE: date (no DUE: last).
Flag DUE: dates earlier than today as **OVERDUE**.
At the end, add a section "Deferred (sleeping)" listing [<] items with a WAKE: date after today, sorted by WAKE:.
Show date and PG: for each item.
Output as a Markdown checklist.
P2: Due This Week
Today is <YYYY-MM-DD>.
From the attached notebook file(s), list every open action ([ ] or woken [<]) with a DUE: date from <start> to <end>.
Also list any OVERDUE open actions.
Sort by DUE: date. Show PRJ:, date, and PG: for each.
Output as a Markdown checklist.
P3: High-Priority Items
Today is <YYYY-MM-DD>.
From the attached notebook file(s), list every open action marked !!.
Sort by DUE: date. Flag OVERDUE items.
Show PRJ:, date, and PG: for each.
Output as a Markdown checklist.
P4: Actions Involving One Person
From the attached notebook file(s), list every open action ([ ] or [<]) that mentions <@JSmith>,
including things I owe them and things they owe me.
Show date, PRJ:, DUE:, WAKE:, and PG: for each.
Output as a Markdown checklist.
P5: What Wakes Up Soon
Today is <YYYY-MM-DD>.
From the attached notebook file(s), list every deferred action ([<]) with a WAKE: date between today and <YYYY-MM-DD>.
Sort by WAKE: date. Show PRJ:, DUE:, original date, and PG: for each.
Flag any [<] item with no WAKE: date as **[NO WAKE DATE]**.
Output as a Markdown table.
9.2 Projects & Topics
P6: All Notes on a Project
From the attached notebook file(s), collect every entry with PRJ: <26-014>.
Present in date order. For each entry show the date, PG:, MTG: (if any), and all its lines exactly as written, including tables.
End with a short summary: key facts, decisions, open actions (including deferred), open questions.
Output as Markdown.
P7: Project Timeline
From the attached notebook file(s), build a timeline for PRJ: <26-014>.
One line per date: YYYY-MM-DD | PG: | one-sentence summary of what happened.
Highlight decisions (!D) and completed actions ([X]) in bold.Output as a Markdown table.
P8: Decision Log
From the attached notebook file(s), list every decision (!D) for PRJ: <26-014>.
For each: date, PG:, MTG:, the decision, and the people present.
Note any later decision that changes or reverses an earlier one.
Output as a Markdown table.
P9: Facts and Sources
From the attached notebook file(s), list every fact (F:) and table (TBL:) tagged <#Topic> or under PRJ: <26-014>.
Show value, units, SRC:, date, and PG:.
Flag any F: or TBL: with no SRC: as **[NO SOURCE]**. Flag any two facts that conflict.
Output as a Markdown table.
P10: Everything Mentioning a Word
From the attached notebook file(s), find every line that mentions <fuse> in any form
(tags, text, file names, meeting names, table contents).
Group by token type (F:, TBL:, C:, N:, !D, ?Q, [ ], [<], *I, FIG:, W>/H>).
Show date and PG: for each.
Output as Markdown.
P11: Topic Knowledge Summary (before a review)
From the attached notebook file(s), collect every entry tagged <#Topic> or PRJ: <26-014>.
Group into: Facts (F:, with SRC:), Tables (TBL:), Claims (C:, with who said it), Decisions (!D),
Open questions (?Q), Open actions ([ ] and [<], with !!, DUE:, WAKE:), Notes (N:), Ideas (*I), Figures (FIG:, with page).
Include date and PG: for each. Follow SEE: references and include those entries.
Flag any C: that contradicts an F:.
Output as Markdown.
9.3 Threads
P12: Thread Rollup
From the attached LedgerMark notebook file(s), reconstruct the full thread on <#FuseHeat>.
Include every entry that:
- has the tag <#FuseHeat>, OR
- is linked by SEE: to or from a thread entry, OR
- clearly discusses the same subject with <@KPatel>, even if untagged (mark these **[LIKELY]**).
Present in time order as one continuous story. For each entry show date, time, and PG:.
End with:
1. Current understanding (facts F: and tables TBL:, with SRC:)
2. Claims still unverified (C:)
3. Decisions (!D)
4. Open actions ([ ], [<]) and open questions (?Q)
Do not change or merge the original entries; this is a summary view only.
Output as Markdown.
P13: Find Loose Ends (weekly)
From the attached LedgerMark notebook file(s), find entries that seem to discuss the same subject
but are NOT connected by a shared #topic or SEE: link.
Also list near-duplicate tags that are probably the same topic (e.g., #FuseHeat and #FuseHot).
List each suggested group with date, time, PG:, and a proposed #topic.
Do not change the file.
Output as a Markdown table.
9.4 Claims, Questions & Ideas
P14: Claim Check
From the attached notebook file(s), list every claim (C:).
For each, check whether a later F:, TBL:, or SEE: link supports or contradicts it.
Mark each as **VERIFIED**, **CONTRADICTED**, or **UNVERIFIED**.
Group by @person. Show date and PG:.
Output as a Markdown table.
P15: Open Questions
From the attached notebook file(s), list every open question (?Q).
Mark any that appear to be answered by a later F:, TBL:, N:, or !D, and show where.
Group by PRJ:. Show date and PG:.
Output as Markdown.
P16: Idea Bank
From the attached notebook file(s), list every idea (*I).
Group by [W]/[H], then by PRJ: or #topic.
Show date and PG:. Mark any idea that later became an action.
Output as Markdown.
9.5 People & Meetings
P17: Meeting History
From the attached notebook file(s), collect every entry with MTG: <FuseReview>.
For each meeting: date, PG:, people, decisions (!D), actions, and open questions (?Q).
End with a list of actions still open from these meetings.
Output as Markdown.
P18: Prep for a Meeting
Today is <YYYY-MM-DD>. I have meeting <FuseReview> on PRJ: <26-014>.
From the attached notebook file(s), give me:
1. What was decided last time (!D)
2. Actions due from me and others ([ ] and woken [<], with @people)
3. Open questions (?Q) to raise
4. Unverified claims (C:) to challenge
5. Key facts (F:) and tables (TBL:) with sources
Keep it to one page. Output as Markdown.
P19: Person Summary (before a 1:1)
From the attached notebook file(s), collect every entry that mentions <@JSmith>.
Group into: Open actions involving them, Claims they made, Decisions in meetings they attended, Open questions.
Include date and PG: for each.
Output as Markdown.
9.6 Files, Sketches & Tables
P20: File References
From the attached notebook file(s), list every <W>> file reference (use H> for home).
Remove duplicates. For each file, show every date and PG: where it was mentioned and the PRJ: or #topic.
Sort by folder path. Output as a Markdown table.
P21: Sketch Index
From the attached notebook file(s), list every FIG: label with date, PG:, PRJ:, and #topic.
Output as a Markdown table.
P22: Pull Tables
From the attached notebook file(s), list every table (TBL:) for <PRJ: 26-014 or #Topic>.
For each: name, SRC:, date, PG:, then the table itself.
Output as Markdown.
P23: Table to Excel (CSV)
From the attached notebook file, find the table named <Fuse temp rise by load>.
Output it as CSV (comma-separated, headers in the first row, units kept in headers) in a single code block, ready to paste into Excel.
To use the CSV, paste it into Excel and choose Data > Text to Columns, with comma as the separator.
9.7 Summaries & Reports
P24: Day or Week Summary
From the attached notebook file(s), summarize entries from <start> to <end>.
Split into Work [W] and Home [H].
For each: what I worked on, decisions, facts learned, actions completed, opened, and deferred.
Keep it under 300 words. Output as Markdown.
P25: Status Report Draft
From the attached notebook file(s), draft a short status update on PRJ: <26-014> for <start> to <end>.
Sections: Progress, Decisions, Risks/Open questions, Next steps (with DUE: dates).
Use only information in the notes. Do not invent anything. Mark gaps as [NEEDS INPUT].
Professional tone, under 200 words.
P26: Find Something I Half-Remember
Search the attached notebook file(s) for anything about: <a fuse temperature number someone mentioned in October>.
Return the best matches with date, PG:, and the exact line.
If nothing matches, suggest the closest entries.
9.8 Housekeeping
P27: Quality Check
Check the attached LedgerMark notebook file for problems:
- Entries missing T:, [W]/[H], or PG:
- C: lines with no @person
- F: lines with no units or no SRC:
- File references missing W> or H>
- DUE: or WAKE: dates not in YYYY-MM-DD format
- [<] items with no WAKE: date
- TBL: tables with no END, uneven columns, or no SRC:
- Near-duplicate #tags (likely the same topic)
- Leftover [??], [W?], [WHO?], [NO DOMAIN], [TABLE CHECK], [FORMAT?] flags
- PRJ: values not in the agreed format
List each problem with date and PG:. Output as a Markdown checklist.

10. Search Guide
In VS Code, press Ctrl+Shift+F to search every notebook file at once.
Find	Search for
A project	PRJ: 26-014
A topic or thread	#FuseHeat
A meeting	MTG: FuseReview
A day	## 2026-10-23
A page	CB03-045
Work / home entries	[W] / [H]
Facts / sources	F: / SRC:
Tables	TBL:
Claims / one person's claims	C: / C:@JSmith
Notes / ideas / sketches	N: / *I / FIG:
Cross-references	SEE:
Decisions / questions	!D / ?Q
Open actions	[ ]
Deferred actions	[<]
Waking in a month	WAKE:2026-12
Due in a month	DUE:2026-11
High priority	!!
Moved / cancelled	[>] / [-]
A person	@JSmith
Work / home PC files	W> / H>
Search Examples
Question	Search
What did we decide about F03?	!D + F03
What's the fuse clearing time?	F: + clears
Where's the thermal data table?	TBL: + temp
Where's the thermal spreadsheet?	W> + Thermal
What did Jane say about heat?	C:@JSmith
What did I park for December?	WAKE:2026-12
Where's my wiring sketch?	FIG: + wiring

11. FAQ
Do I need [W]/[H] on every entry? No. The AI infers it, treating PRJ: and MTG: as work. Write the tag only when the entry is unclear.
What if I forget a token? The line is treated as N:, and you can fix it during review.
How does the AI "remember" a deferred action? It doesn't. Your notebook file holds it. The [<] … WAKE: line stays in the file, and P1 compares wake dates with today's date each time you run it.
What's the difference between [>] and [<]? [>] moves an action to another page. [<] moves it to another date.
Can the AI join a conversation scattered across pages? Yes, with P12. It works best when you reuse the #Topic and add SEE: links. Untagged entries it thinks are related get marked [LIKELY].
Can I write tables by hand? Yes. Start with TBL:, put the headers in the first row, and finish with END. Prompt A turns it into a Markdown table, and P23 exports it to Excel.
Can I use headings and bold text? Yes. Use the formatting tags (<H1>, <B>, <Q> and so on). Prompt A converts them to Markdown.
What if I photograph the pages late? That's fine. The date in ==DATE== is what counts.
Can a line have more than one token? Yes, for example !! [ ] update W>SFMEA/Fuse_v3.xlsx DUE:2026-10-30.
What about entries with no time? Use your best estimate. Every entry needs a T:.
Can I edit old entries in GitHub? Only to change an action's status or fix a transcription error.
Where do the sketches go? They stay on paper, and FIG: makes them searchable. You can also save page photos in the repo, for example img/CB03-045.jpg.
Should I also set calendar reminders? For critical deferred items, yes. LedgerMark only brings items back when you run P1, so an Outlook or Planner reminder is a useful backup.
Is work data safe in this repo? Keep the repo private, and confirm that your company's policy allows work notes in a personal GitHub account. If it doesn't, use your company's enterprise GitHub.

Appendix A: Quick Reference Card
Copy this inside the front cover of every notebook.
LEDGERMARK v1.3
STRUCTURE   ==YYYY-MM-DD DDD==   PG:CB03-045   T:0930   >>PG:   SEE:PG:
CONTEXT     MTG:Name   PRJ:26-014   #Topic   @JSmith   [W] [H]
KNOWLEDGE   N: note    F: fact+units   C:@who claim   SRC: source
            *I idea    FIG: sketch label
TABLES      TBL: name / header row with units / | between columns / - = empty / END
ACTIONS     [ ] open  [X] done  [>] moved  [-] cancelled  [<] deferred
            WAKE:YYYY-MM-DD  DUE:YYYY-MM-DD  !! priority  !D decision  ?Q question
FILES       W>work PC   H>home PC   URL>link
FORMAT      <H1> <H2> <H3> heading  <B> bold  <I> italic  <Q> quote
            <LI> bullet  <OL> numbered  <CODE>..</CODE>  <HR> divider
RULES       CAPS - one item per line - units on F: - W>/H> on every file
            every [<] needs WAKE: - reuse #Topic + SEE: when you return to a topic

Appendix B: Repository README
Paste this into README.md in the ledgermark repo.
# LedgerMark v1.3
A handwritten markup language for engineering notebooks.
Write by hand -> photograph -> AI converts to Markdown -> search in GitHub.
- One notebook = one file (CB03.md, CB04.md ...)
- Thread summaries: threads/<Topic>.md (generated views, never edited by hand)
- Token reference, rules, and prompts: see LedgerMark-Manual.md
- Daily transcription: Prompt A
- Open actions (including woken deferred items): P1

Appendix C: Converting This Manual to Word or PDF
Method	Steps
Word	Paste the manual into Word. Give the code boxes a "Code" style (Consolas 9 pt, light grey shading), then use File > Save As > PDF and turn on Create bookmarks using Headings.
VS Code	Install the Markdown PDF extension, open LedgerMark-Manual.md, then right-click and choose Markdown PDF: Export (pdf).
Pandoc	Run pandoc LedgerMark-Manual.md -o LedgerMark-Manual.docx --toc, then save the result as a PDF from Word.
Before you share it:
	• ☐ Make sure no real project details remain in the examples.
	• ☐ Confirm that you're allowed to share it inside your company.
	• ☐ Search the web and GitHub for "LedgerMark" to check the name isn't already taken.
	• ☐ Put the Quick Reference Card on its own page so people can print it.
