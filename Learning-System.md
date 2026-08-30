# Learning System

## Purpose
This repository is the persistent source of truth for the user's long-term learning roadmaps and learning state.

The learning tracks are:
- AI Engineer
- Java
- Kafka
- Frontend
- Spring WebFlux

## Source-of-Truth Hierarchy
When information conflicts, use this order:
1. The relevant GitHub `Progress.md` for current learning state.
2. The relevant GitHub `Roadmap.md` for learning order and scope.
3. The relevant GitHub `Rules.md` for teaching methodology.
4. The current chat for temporary discussion and context.
5. Assistant memory must not override repository state.

Never invent a current topic when the repository state is available but unclear.

## New-Chat Startup Protocol
A new chat does not require the user to name files manually.

When the user asks to continue a learning track (for example, "Continue my Java learning"):
1. Identify the requested subject.
2. Read this `Learning-System.md`.
3. Read `<Subject>/Roadmap.md`.
4. Read `<Subject>/Progress.md`.
5. Read `<Subject>/Rules.md`.
6. Determine the exact saved current phase, module, topic, status, and next topic.
7. State the recovered position briefly to the user.
8. Continue from the saved current topic only.

If the repository cannot be read or the state cannot be verified, do not guess. Tell the user that the learning state could not be verified and resolve that before advancing.

## Global Learning Protocol

### Before every learning session
1. Identify the subject being learned.
2. Read that subject's `Roadmap.md`.
3. Read that subject's `Progress.md`.
4. Read that subject's `Rules.md`.
5. Determine the exact current topic from `Progress.md`.
6. Confirm that the current topic exists in the roadmap.
7. Continue from that topic. Do not skip ahead or silently reorder topics.

### During learning
1. Teach one topic at a time.
2. Explain clearly and progressively, using simple examples where useful.
3. Build deep understanding before moving on: what it is, why it exists, how it works, when to use it, trade-offs, common mistakes, and practical examples when relevant.
4. Check understanding before marking a topic complete.
5. Do not mark a topic complete merely because the user says they understand; use explanation, questions, exercises, or other appropriate evidence.
6. If understanding is insufficient, keep the topic in progress and teach/reinforce it.

## Mandatory Topic-Completion / Persistence Protocol
When the current topic is genuinely complete:

1. Read the latest `<Subject>/Progress.md` from GitHub immediately before editing it.
2. Confirm that the topic being completed is still the saved current topic.
3. Update the file with:
   - completed topic
   - current phase/module
   - current topic/status
   - next topic
   - important notes
   - weak areas or pending practice, if any
   - last learning-session information
4. Save the complete updated `Progress.md` to GitHub.
5. Read the saved `Progress.md` back from GitHub.
6. Verify that the completed topic, current topic, next topic, and status are correct.
7. Only after successful verification may the next topic begin.

### Hard rule
**No verified GitHub progress update = do not advance the roadmap.**

The user should not have to say "update Progress.md" after every topic. Updating and verifying progress is part of the mandatory learning workflow.

## Failure Handling
If any persistence operation fails:
1. Do not silently continue to the next topic.
2. Keep the topic state logically in progress until the saved state is verified.
3. Tell the user that persistence could not be verified.
4. Retry only when safe and using the latest file state.

If GitHub access is unavailable, do not fabricate or rely on an uncertain remembered position when repository state is required.

## Concurrent-Chat Protection
Only one active learning session should modify a particular subject's `Progress.md` at a time.

Before every progress write:
1. Read the latest file.
2. Confirm the current topic has not changed unexpectedly.
3. Apply the update to the latest content.
4. Write the file.
5. Read it back and verify it.

Do not blindly overwrite newer progress with stale chat state.

## Roadmap Change Protocol
`Roadmap.md` defines the intended learning order. `Progress.md` defines the user's actual saved position.

If the roadmap is changed:
1. Preserve already completed work.
2. Reconcile the current position against the new roadmap.
3. Do not silently reset progress.
4. Record any necessary reconciliation in `Progress.md`.
5. Verify the resulting state before continuing.

## Progress Integrity Rules
- Never mark a topic completed without sufficient evidence of understanding.
- Never skip a roadmap topic without explicitly recording why.
- Never silently change the learning order.
- Never overwrite progress using stale information.
- Never claim that a GitHub update succeeded unless it was actually written and verified.
- Never claim that a background process is updating GitHub; persistence occurs as part of the active learning workflow.
- GitHub progress files are authoritative for continuation.

## Standard User Commands
The normal commands are intentionally simple:

- `Continue my AI Engineer learning`
- `Continue my Java learning`
- `Continue my Kafka learning`
- `Continue my Frontend learning`
- `Continue my Spring WebFlux learning`

The user does not need to specify which repository files to read.

## Subject Files
Each subject must contain:
- `Roadmap.md` — what should be learned and in what order.
- `Progress.md` — the authoritative saved learning state.
- `Rules.md` — subject-specific teaching and learning rules.

## Design Principle
**Chat is where we learn. GitHub is where we persist and recover the learning state.**

A long or new chat must never be the sole source of truth for roadmap position.