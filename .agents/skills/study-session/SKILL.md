---
name: study-session
description: Conduct sequential textbook-based study sessions in ai-disneyland when the learner asks to start, continue, or end a session, discusses theory, or submits solutions during a session. Editing this skill is not a study session.
---

# Study session

Follow `AGENTS.md` for teaching, language, assistance, and exact textbook verification. All paths below are relative to the repository root; keep this skill as a single file in `.agents/skills/study-session/`.

1. **Start or resume a continuous route.** Read `learning/now.md`, `learning/learner.md`, then relevant `learning/progress/` files; consult `learning/roadmap.md` when choosing the direction. By default, resume the active book and unfinished chapter at the saved stopping point, including pending exercises or checks. Do not choose a new book or chapter afresh each session. Briefly state the book, chapter/section, where the learner stopped, and today's small next step. If they specify a chapter or problem, follow that request.

   - If no route is saved yet, propose one book from the recorded priorities and a starting chapter using `library/README.md` and that book's index. Normally begin at the beginning of the book's instructional sequence; use an existing reading position or a later entry point only with an explicit reason grounded in the learner's goals and a brief check of the necessary earlier ideas. Self-reported reading is not verified mastery. Let the learner redirect without requiring them to design the route.
   - Work through the selected chapter across as many sessions as needed, following its section order: discuss new ideas, work examples, and select exercises that cover the main ideas. A small exercise set is a step within the chapter, not automatic completion of it. Familiar material may move faster after a check; solving every exercise is not required.
   - Move to the next chapter in the book's order after covering the current chapter's main ideas and checking representative work independently. Identify remaining gaps and distinguish a decision to move on from verified mastery. Explain any proposed skip or change of book and agree it with the learner instead of silently jumping. Learner-requested detours remain welcome; preserve the main route's return point. If several books are in use, keep a separate stopping point for each.

2. **Check understanding through dialogue.** Ask one meaningful question at a time and choose the next based on the answer. Keep this brief; for a completely new topic, check only the necessary prerequisites. Use the responses to adapt the session, rather than relying on self-ratings or old assessments.

3. **Discuss theory or assign exercises from the book.** Default to a small set, usually 2–3 exercises from the selected chapter. For well-understood material, choose representative review problems to refresh the main ideas without repetitive drills. For weaker understanding, choose a progression that teaches the missing ideas; adjust explanation and difficulty to observed needs. The learner works independently and returns solutions when ready.

4. **Review submitted work.** Accept a whole file or individual solutions, including unfinished attempts. First check all submitted work and give brief feedback on each problem, then discuss difficulties in detail. Apply the project's hint and verification rules.

5. **End and save.** Only after explicit completion, read `MEMORY.md`, `learning/sessions/README.md`, and `templates/session-note.md`. Save the session report and update relevant progress and `learning/now.md` according to those rules. In the subject's progress file, retain the book ID/edition, current chapter/section and exact stopping point with verified printed/PDF page locators, pending exercises or checks, and the next step within the chapter (or the reason for moving on). Link to the session report as evidence; keep only the active route and a concise next step in `learning/now.md`. Preserve other books' stopping points and any return point after a detour. Briefly summarize verified results, remaining gaps, and the next step. Do not commit or push without a direct request.
