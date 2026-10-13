# Report: how to scope products with non-technical users, for the discovery assistant

**Access limits.** The GitHub API was blocked for non-session repos, and the proxy blocked basecamp.com, openai.com, momtestbook.com, producttalk.org and amazon.com. So:
- **Read directly:** raw GitHub files, GitHub repo pages (via WebFetch) and anthropic.com.
- **Confirmed only through search results:** the other sources. Their URLs are confirmed that way; the wording of the Mom Test and JTBD summaries comes from my own knowledge of these well-known public works.
- **Not fabricated:** I found no public scoping questionnaire from Anthropic, OpenAI or Meta, and I did not invent one.

## Top 10 sources, ranked

1. **mattpocock/skills, the `grilling` skill.** https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md
   - MIT licence. The repo page showed about 288.8k stars (the figure looks inflated, so check it).
   - **What to steal:**
     - Treat the open decisions as a "design tree".
     - Ask in rounds: each round asks every question that can be answered now ("the frontier").
     - Give a recommended answer, worded so that "yes" accepts it.
     - "Finding facts is your job, never the user's", while "decisions are the user's".
     - The session ends only when the frontier is empty and the user confirms you share an understanding.
   - **Also useful:** `to-questionnaire` (an async questionnaire for someone else to fill in, built around what they know that you don't) and `to-spec` (a template whose sections end with Out of Scope).
2. **deanpeters/Product-Manager-Skills.** https://github.com/deanpeters/Product-Manager-Skills
   - About 7.3k stars. **Licence: CC BY-NC-SA 4.0, so it can't be copied into a commercial product. Use it for patterns only.**
   - **What to steal:** the `workshop-facilitation` protocol:
     - one question per turn, in plain language;
     - progress labels such as "Context Q3/8";
     - three entry modes: Guided, Context dump, or Best guess (assumptions labelled);
     - a meta question ("how many left?") gets answered, then the pending question is restated;
     - "stop" pauses immediately;
     - the session ends with an "Assumptions to Validate" list.
   - **Also useful:** `discovery-interview-prep` (Mom Test based), `problem-framing-canvas`, `press-release` (Amazon Working Backwards) and `opportunity-solution-tree`.
3. **anthropics/knowledge-work-plugins, product-management plugin.** https://github.com/anthropics/knowledge-work-plugins
   - Apache-2.0, about 29.4k stars.
   - **What to steal from `write-spec`:**
     - "Be conversational — do not dump all questions at once."
     - Non-goals, each with a reason: "Non-goals prevent scope creep."
     - Priorities split P0, P1 and P2.
     - Goals written as outcomes, not outputs.
     - Open questions tagged with who must answer them.
   - **Also useful:** `product-brainstorming` asks "who has this problem / what are they doing about it today?" first, keeps asking why until it reaches a root cause, and names the riskiest assumption.
4. **Basecamp Shape Up, chapter 1.5 "Write the Pitch".** https://basecamp.com/shapeup/1.5-chapter-06
   - Free to read online.
   - **What to steal:** the five parts of a pitch: Problem, Appetite, Solution, Rabbit holes, No-gos.
   - Appetite works as the reverse of an estimate: fix the time, then fit the scope to it.
5. **The Mom Test (Rob Fitzpatrick).** https://www.momtestbook.com/
   - **What to steal:**
     - Talk about their life, not your idea.
     - Ask about specific things that already happened, not opinions or guesses about the future.
     - Talk less, listen more.
     - Never ask "would you use / pay for…?".
     - Compliments and "I'd definitely…" carry no information. Push for commitments and for what they actually did.
6. **Teresa Torres, story-based interviewing.**
   - https://www.producttalk.org/best-customer-interview-questions/ and https://www.producttalk.org/opportunity-solution-trees/
   - **What to steal:**
     - "Tell me about the last time you…"
     - Collect stories, not general claims.
     - Let the outcome set how broad the question is.
     - Use an opportunity solution tree (outcome → opportunities → solutions → experiments) as the assistant's internal map of the conversation.
7. **Anthropic, "Building effective agents".** https://www.anthropic.com/engineering/building-effective-agents
   - **What to steal for setting AI expectations:**
     - "finding the simplest solution possible, and only increasing complexity when needed"
     - Workflows suit "well-defined tasks"; agents trade "latency and cost for better task performance", with "potential for compounding errors".
8. **OpenAI, "A practical guide to building agents" (April 2025).** https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf
   - **What to steal:** an agent fits complex judgement calls, rules too messy to maintain, and unstructured data. Plain generation needs only one model call. This helps sort "the request really needs AI" from "the request is just a form plus a rule".
9. **phuryn/pm-skills.** https://github.com/phuryn/pm-skills
   - MIT, about 26.9k stars. The most reusable of these under its licence.
   - **What to steal:** `interview-script` (JTBD probing questions), `summarize-interview` (turns a transcript into jobs, satisfaction signals and actions), `opportunity-solution-tree`, `job-stories` ("When… I want to… so I can…"), and `prioritization-frameworks` (MoSCoW, Kano and others).
10. **Amazon Working Backwards (PR/FAQ).**
    - **Questions to steal:** Who is the customer? What is their problem or opportunity? What is the most important benefit? How do you know? What does the experience look like?
    - Write the press release and FAQ before building anything.
    - **Wording varies between sources; I found no single official text.** The best public reference is the book *Working Backwards* (Bryar and Carr).
    - URLs: https://productmindset.substack.com/p/product-framework-working-backward, https://amer.resources.awscloud.com/vidyard-all-players-2/working-backwards

**Also checked:**
- **deanpeters/Product-Manager-Prompts:** https://github.com/deanpeters/Product-Manager-Prompts. About 1.2k stars, CC BY-NC-SA (it was MIT before v2.3.0). Best item: `incoming-request-breakdown`, which works out what an inbound request really wants.
- **dend/awesome-product-management:** https://github.com/dend/awesome-product-management. CC0, about 1.3k stars. Only a list of links; stale since April 2024.

**Public material vs folklore:**
- **Intercom JTBD:** the job story format is public, from the free Intercom book and https://jtbd.info.
- **Meta "product sense":** the steps goal → users → pain points → solutions → prioritise → metrics come from interview-prep material (Exponent, CIRCLES). It is not a published internal Meta process.
- **Stripe and Linear:** "write it down first" cultures, known only from blog posts and talks. Neither has a public questionnaire.
- **Anthropic and OpenAI scoping:** the only public items are the two agent guides above, plus Anthropic's https://www.anthropic.com/news/how-anthropic-teams-use-claude-code. Their PM podcast talks (e.g. Lenny's Podcast) are about evals and fast prototyping, not intake questionnaires.

## Master question set (plain language)

**Problem / pain**
1. What made you want to talk about this now?
2. Tell me about the last time this went wrong. What happened?
3. How often does that happen?
4. What does it cost you when it does: time, money, stress, a customer?
5. If nothing changed for a year, what would happen?

**Today's workaround (the spreadsheet)**
6. Walk me through how you do it today, step by step.
7. Can you show me the spreadsheet? What does each column mean to you?
8. Where does the data come from? Who types it in?
9. Which part do you dread, or do twice?
10. What have you already tried to fix it? Why did you stop?
11. What do you copy and paste, and where to?

**Outcome / success**
12. Picture it working perfectly three months from now. What's different on a Monday morning?
13. How would you know it worked? What number would move?
14. What's the one thing that, if it worked, would make this worth it?

**Users**
15. Who touches this today? Who would use the new thing?
16. Who has to approve it or sign off?
17. Who gets the result at the end?
18. How comfortable are they with new tools?

**Stories / examples**
19. Give me a real example from last week, with real names and numbers.
20. What's the strangest case you've had to handle?
21. What happens when something is missing or wrong?

**Constraints / appetite**
22. If this took two weeks versus three months, would it still be worth it?
23. Is there a date that really matters? What happens if we miss it?
24. Which systems must it work with (email, accounting software, etc.)?
25. Are there rules we must follow (privacy, audit, approvals)?
26. If we could only do one part first, which part?

**Risks / no-gos**
27. What would make you stop using it?
28. What must it never do?
29. What should we deliberately leave out of version one?
30. Who might push back on this, and why?

**AI expectations**
31. What do you imagine the AI doing, in one sentence?
32. If it's right 9 times out of 10, is that great or a disaster?
33. Who checks its work before it matters?
34. What decisions should always stay with a person?
35. Is it OK if it sometimes says "I'm not sure"?
36. Is it OK if it takes a minute, or costs a few cents per use?

## Scope-creep and digression heuristics, with redirect lines

1. **A new feature appears mid-session.** "Good idea. I've put it in the parking lot so we don't lose it. Can we finish X first?"
2. **"It would be nice if…" (no pain behind it).** "When did you last actually need that? If you can't recall a time, let's mark it 'later'."
3. **A solution comes before the problem.** "Before we design that, what's the problem it fixes for you?"
4. **New users or departments get added.** "That widens who it's for. Should version one serve just [core group] well first?"
5. **Talk of the future** ("eventually we'll…"). "Let's keep that as a someday note. What do you need in the first month?"
6. **The total exceeds the appetite.** "We agreed about [X weeks]. This would double it. What should we drop to make room, or should it wait?"
7. **Edge-case spiral, or the same topic three or more times.** "That's a rabbit hole. Let's decide the rule for the normal case and handle exceptions manually for now."
8. **"Also could it…" plus integration requests.** "Every connection adds risk. Can a person do that step by hand in version one?"
9. **Expecting the AI to be magic or perfect.** "AI is like a fast new hire: great at drafts, and sometimes wrong. Who reviews its work?"
10. **Off-topic venting or company history.** "That's useful background. I've noted it. To keep us moving: [restate the pending question]."

**Change-request triage:** for each new item, ask:
- Does it serve the agreed outcome?
- Does it fit the appetite?
- Is it a must, or a nice-to-have?

Then put it in one of four places: now, swap for something else, parking lot, or no-go. Show the parking lot back to the user at the end of every session.

## Exact grill-me text (fetched from main)

`skills/productivity/grill-me/SKILL.md` is now only a wrapper:
```
---
name: grill-me
description: A relentless interview to sharpen a plan or design.
disable-model-invocation: true
---

Call the Skill tool with "grilling".
```
`skills/productivity/grilling/SKILL.md`:
```
---
name: grilling
description: Grill the user relentlessly about a plan, decision, or idea. Use when the user wants to stress-test their thinking, or uses any 'grill' trigger phrases.
---

Interview the user relentlessly until you reach a shared understanding. Map this as a **design tree**: every decision branches into the decisions that hang off it.

Work the tree in **rounds**. The **frontier** is every decision whose prerequisites are already settled: the questions you can ask _now_ without guessing at answers you haven't heard yet. Ask the whole frontier in one round: number each question and give your recommended answer. Then wait for the user's answers before the next round.

Format a round like so:

❓ **Q1** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

➡️ <your recommended answer>

---

❓ **Q2** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

➡️ <your recommended answer>

Word each question so "yes" accepts your recommended answer.

Each round the user answers reshapes the tree: settled decisions push the frontier outward and unblock questions that depended on them. Recompute the frontier and ask the next round. A question whose answer depends on another question still open in this round belongs to a _later_ round, not this one.

Finding _facts_ is your job, never the user's. When a frontier question needs a fact from the environment (filesystem, tools, etc.), dispatch a sub-agent to find it; don't ask the user for anything you could look up yourself. Don't block on it: a running exploration is an unsettled prerequisite, so only the questions downstream of it wait for the sub-agent to report; ask the rest of the frontier now. The _decisions_ are the user's: put each to them and wait.

The session is done when the frontier is empty: every branch of the design tree visited, nothing left silently assumed. Do not act on it until the user confirms you have reached a shared understanding.
```
In the original block, the format example sits inside a code fence.

**Earlier version (not verified):** older versions, per mirrors such as https://skills.sh/mattpocock/skills/grilling, asked one question at a time and explored the codebase when that could answer a question.

**Adaptation note for non-technical users:** asking a whole frontier per round will likely overwhelm Excel-level users. Combine grilling's tree, recommended answers and "facts are my job" with deanpeters' rule of one question per turn plus progress labels.

No files were written to the repo.
