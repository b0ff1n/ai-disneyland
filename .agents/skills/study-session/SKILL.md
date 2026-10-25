---
name: study-session
description: Conduct textbook-based study sessions in ai-disneyland when the learner asks to start or end a session, discusses theory, or submits solutions during a session. Editing this skill is not a study session.
---

# Study session

Follow `AGENTS.md` for teaching, language, assistance, and exact textbook verification. All paths below are relative to the repository root; keep this skill as a single file in `.agents/skills/study-session/`.

1. **Start.** Read `learning/now.md`, `learning/learner.md`, then relevant `learning/progress/` files; consult `learning/roadmap.md` when choosing the direction. Choose a book, chapter(s), and topic for this session, briefly explain the choice, and allow the learner to redirect. If they specify a chapter or problem, start there.

2. **Check understanding through dialogue.** Ask one meaningful question at a time and choose the next based on the answer. Keep this brief; for a completely new topic, check only the necessary prerequisites. Use the responses to adapt the session, rather than relying on self-ratings or old assessments.

3. **Discuss theory or assign exercises from the book.** Default to a small set, usually 2–3 exercises from the selected chapter. For well-understood material, choose representative review problems to refresh the main ideas without repetitive drills. For weaker understanding, choose a progression that teaches the missing ideas; adjust explanation and difficulty to observed needs. The learner works independently and returns solutions when ready.

4. **Review submitted work.** Accept a whole file or individual solutions, including unfinished attempts. First check all submitted work and give brief feedback on each problem, then discuss difficulties in detail. Apply the project's hint and verification rules.

5. **End and save.** Only after explicit completion, read `MEMORY.md`, `learning/sessions/README.md`, and `templates/session-note.md`. Save the session report and update relevant progress and `learning/now.md` according to those rules. Briefly summarize verified results, remaining gaps, and the next step. Do not commit or push without a direct request.
