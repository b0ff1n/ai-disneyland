# External memory: Git is the database

The learner uses this repository on multiple machines. As explicitly requested on 2026-10-25, the agent's durable external memory is **the files tracked in Git and their history**, together with the Git LFS objects for large originals. Work needed by the next session must be available from the transferred repository.

## Where memory lives

| Location | Purpose |
| --- | --- |
| `AGENTS.md` | Shared tutoring rules, source verification, and rules for changing memory |
| `MEMORY.md` | This description of storage, portability, and persistence |
| `learning/now.md` | Short entry point: current priority, state, and next step |
| `learning/learner.md` | Current concise learner profile, preferences, and stated plans; distinguish these from tested knowledge |
| `learning/interview-2026-10-25.md` | Dated interview context and self-reports; not a lesson, diagnostic exam, or learning-statistics record |
| `learning/roadmap.md` | Study goals and priorities |
| `learning/progress/*.md` | Current textbook routes, exercise states, observed results, gaps, and progress toward goals; rules and book-to-file map in `learning/progress/README.md` |
| `learning/sessions/*.md` | Historical evidence for a future timeline, topic map, or chart: completed-session reports and explicit dated corrections; format in `learning/sessions/README.md` |
| `library/README.md` | Catalog of exact textbook sources and how to access them |
| `library/originals/` | Unchanged source PDFs, tracked through Git LFS |
| `library/indexes/` | Verified contents, edition evidence, and printed/PDF page maps |
| `library/extracted/` | Persistent full-text extraction, raw navigation data, structured contents, and provenance, tracked as ordinary Git files |
| `library/SHA256SUMS` | Identity checks for the original PDFs |
| `resources/` | Other study references and materials |
| `templates/` | Reusable structures for future records |

## Persistence rules

- Important data belongs in tracked repository files. This includes useful extracted text and OCR, page mappings, source metadata, decisions, and learning records. The ability to regenerate data does not make it disposable: retain extraction so another machine can use it without repeating the work.
- Never leave the only copy of important data in `/tmp`, an ignored directory, a tool's private workspace, app-specific memory, or chat history. Save it in the appropriate repository location before ending the task.
- `/tmp` and ignored `library/cache/` are for expendable intermediate files only, such as unannotated page previews that can be regenerated from a retained PDF. Preserve useful annotations, corrections, and conclusions in tracked files.
- Use repository-relative paths inside durable records. Avoid dependencies on a particular username, absolute checkout path, or temporary filename. Identify source-derived data by book ID and source SHA-256.
- Keep full-text extracts and JSON metadata in ordinary Git; large original PDFs use LFS. Preserve page boundaries and document extraction defects. The original PDF remains authoritative for exact mathematical statements.
- Verify that intended durable files are not ignored and are included in the requested commit. Creating a file inside the working directory alone does not make it part of Git history.
- Follow the commit and push authorization rules in `AGENTS.md`. A request to save a preference is not permanent permission to push. When a commit is outside the authorized scope, clearly report that the changes are still uncommitted.

## Continuing on another machine

Read `AGENTS.md`, then the relevant tracked state: `learning/now.md`, `learning/learner.md`, and the topic's progress file. For textbook work, read the library catalog and the book's index, search the saved extraction, and verify the relevant original PDF pages.

Ordinary Git history carries the learning state, documentation, indexes, and extraction. Source PDFs additionally require the LFS objects; follow [the library setup](library/README.md). Transfer them through an authorized Git/LFS push and pull, or copy a repository that includes the local LFS object store. A local commit is durable locally but is not automatically transferred to another machine.

Memory records evidence, not presumed mastery. Keep historical session records intact and record later corrections or new observations explicitly.

The session report is the single source of historical learning events; `learning/progress/` is the revisable current interpretation, linked to those reports. Use the versioned JSON block inside each Markdown report as specified in [the archive rules](learning/sessions/README.md). Reports and their metadata are ordinary Git files, not LFS objects. Future visualizations can be derived from them without a separate database or manually maintained aggregate. Unknown duration stays unknown, and session counts or time spent are not measures of mastery.

For requests such as "what did we cover this year?", follow the period-review instructions in [the archive rules](learning/sessions/README.md). Reconstruct topics, books and sections, exercises, verified results, assistance, and remaining gaps from dated reports and explicit corrections. `learning/roadmap.md` holds future plans; it is not a record of completed work.
