---
name: loop-breaker
description: Detects and escapes failure loops, repeated errors, and stuck states. Use whenever a command, test, build, or fix fails twice; the same error reappears; progress stalls; you are about to retry unchanged; or you have made 3 or more attempts at one problem. Triggers include “still failing,” “same error again,” “tried that already,” “going in circles,” “flaky,” and “timeout.”
---

# Loop Breaker

Repeating a failed action and hoping is an expensive mistake. Use this procedure to turn repeated failures into evidence, change the approach, and stop before burning time on a loop.

## Track attempts

For each attempt on the same problem, record briefly:

| Attempt | What I did | What happened (exact error/result) | What this tells me |
|---|---|---|---|

Keep the log in working notes or the task context. Before each new attempt, review it. Never repeat an identical action expecting a different result. A retry must change the input, approach, or understanding, and the change must be based on evidence.

## Enforce the limits

- **Two-strike reset:** After two failed attempts at the same operation or approach, stop and perform the reset below before trying again. Do not keep making small parameter changes that preserve the failed approach.
- **Four-attempt hard cap:** Count all attempts to solve one problem, including attempts made before the reset. After four unsuccessful attempts, stop troubleshooting. Report the failure honestly and ask for only the information or decision needed to proceed.
- **Stalled work:** If progress has stalled, the same error has returned, or you have made three or more attempts, activate this skill immediately—even if the attempts used different commands. Review the log before acting.

## Reset after strike two

1. **Read the complete failure literally.** Inspect the full output, not only the first line. Identify the earliest causal error and distinguish it from downstream symptoms.
2. **State one testable hypothesis.** Use: “I think it fails because X.” Mark it as a hypothesis, not a fact.
3. **Design a falsifiable test.** Choose the smallest diagnostic that could disprove the hypothesis. Gather evidence—such as verbose output, a log, a printed value, or a minimal reproduction—before editing blindly.
4. **Shrink the problem.** Isolate the smallest failing test, file, function, command, or input.
5. **Check assumptions.** Verify the working directory, target file, command and version, environment variables, stale build/cache state, and whether the edited file is actually the one being run. Consider whether the error predates the change.
6. **Change the approach.** If patching fails, choose a different strategy, library, or decomposition. Consider returning to the last known-good state and reapplying changes one at a time.
7. **Log the evidence and next action.** Before trying again, confirm it is materially different from earlier attempts and still within the four-attempt cap.

## Avoid common loop traps

- Fixing symptoms in different places while the root cause remains.
- Adding retries, sleeps, or broad exception handling to silence an error you do not understand.
- Reinstalling dependencies or clearing caches repeatedly without evidence that they are the cause.
- Ping-ponging between two fixes that break each other.
- Editing a file that is not the one the command or build actually uses.
- Treating a changed flag or input as a genuinely new approach when the failed assumption is unchanged.

## Stop and report when stuck

At the four-attempt cap—or sooner when required access or a user decision is missing—stop rather than spin. Give a concise, honest status containing:

- **Goal and failure:** What you were trying to do and the exact error, trimmed only enough to be readable.
- **Attempts:** What you tried and what each result ruled out.
- **Best current hypothesis:** Clearly label it as unverified if it has not been proven.
- **Next step:** What you would test or change next.
- **What you need:** The specific access, decision, log, or alternative approach needed from the user.

Stopping with a clear diagnosis is a good outcome. Do not hide a product or infrastructure defect behind another retry.
