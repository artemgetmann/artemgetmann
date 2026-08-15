# Selected Technical Evidence

This page is a compact index of work I can support with public experiments, reports, or pull requests. It separates measured results from interpretation and distinguishes the Jarvis consumer product from the upstream OpenClaw codebase used as its technical foundation.

## Cortex: Persistent Agent Memory

### Architecture trade-offs depend on task difficulty

- **Problem:** A multi-role learning architecture may add complexity without improving results.
- **Hypothesis:** Separate execution, evaluation, and lesson-generation roles should help most on unfamiliar or remapped tasks.
- **Experiment:** Compared full and simplified architectures over 10 runs per arm on an easier in-domain task and a harder holdout task.
- **Result:** Simplified won 90% to 80% on the easier task; full won 100% to 60% on the holdout task.
- **Lesson:** There was no universal winner. The extra architecture earned its cost on the harder transfer problem, not on every task.
- **Proof:** [Architecture A/B findings](https://github.com/artemgetmann/Cortex/blob/main/docs/archive/memory-v2-history/AB-FINDINGS.md)

### Memory improved one constrained transfer test

- **Problem:** A small model repeatedly failed a difficult Git transfer task under a six-step limit.
- **Hypothesis:** Retrieving lessons from earlier failures would improve completion without changing the model or step budget.
- **Experiment:** Ran learning ON and OFF for 10 sessions per arm with the same task, model, evaluator, and limits.
- **Result:** ON passed 5/10 versus 2/10 for OFF; mean errors fell from 5.5 to 3.7.
- **Lesson:** The learning mechanism showed a useful signal in this setup, but one small experiment is not proof of general improvement.
- **Proof:** [Shell hotfix ON/OFF report](https://github.com/artemgetmann/Cortex/blob/main/tracks/cli_sqlite/reports/2026-03-09_shell_hotfix_hard_onoff_step6_10run.md)

### Memory also made another test worse

- **Problem:** Positive results can hide sensitivity to model, budget, retrieval, or task setup.
- **Hypothesis:** The same learning approach should also help under a tighter three-step limit with a different model.
- **Experiment:** Ran a second 10-versus-10 ON/OFF comparison.
- **Result:** ON passed 50%; OFF passed 70%. Lesson activation was low, so the intended mechanism rarely engaged.
- **Lesson:** Treat retrieval activation as part of the causal test. Do not claim that adding memory automatically improves an agent.
- **Proof:** [Negative ON/OFF result](https://github.com/artemgetmann/Cortex/blob/main/tracks/cli_sqlite/reports/hard_shell_git_transfer_hotfix_step3_onoff_10run.md)

### Similar failures had three different causes

- **Problem:** Repeated failure could come from insufficient steps, ineffective retries, or a model capability limit.
- **Hypothesis:** Controlled changes to one factor at a time would separate the causes.
- **Experiment:** Varied the step budget, compared one long attempt with several short retries, and compared `gpt-5-nano` with `gpt-5-mini`.
- **Result:** Nano moved from 0/2 passes at 6 and 12 steps to 2/2 at 20; retries did not help when memory activation stayed at zero; mini passed 3/3 versus nano at 1/3.
- **Lesson:** Step budget, retry design, memory activation, and model capability are different engineering problems.
- **Proof:** [Three-part diagnosis](https://github.com/artemgetmann/Cortex/blob/main/tracks/cli_sqlite/reports/diag_three_part_openai_nano_2026-03-02.md)

## Jarvis: Production Agent Engineering

Jarvis is my current local-first consumer product for bringing coding-agent capabilities to everyday Mac users. Its repository began as a fork of [OpenClaw](https://github.com/openclaw/openclaw), and the engine and substantial upstream code remain inherited. The examples below link to specific changes I authored and product decisions I made rather than claiming the full repository as my work.

### Durable goals need independent completion checks

- **Problem:** An agent that grades its own work can mark a long-running goal complete without sufficient evidence.
- **Hypothesis:** A fresh evaluator with no tools, hooks, or owner authority should judge a structured evidence packet after each work attempt.
- **Change:** Added durable goal claims, an isolated evaluator, bounded automatic revision, stable-blocker handling, and fail-closed behavior for unsupported providers.
- **Result:** The exact source head passed focused tests, full required CI, and independent review. Installed-runtime behavior remained a separate proof layer.
- **Lesson:** Persistence is not enough. Long-running agents need independent evidence checks and explicit stop states.
- **Proof:** [PR #1334: independent evaluator loop](https://github.com/artemgetmann/openclaw/pull/1334)

### Delegation must preserve only the authority it needs

- **Problem:** Jarvis delegated monitor creation to a child agent, but the child lost the already-verified owner permission and could not use the monitor tool.
- **Hypothesis:** Carrying one core-written owner marker across the spawn boundary could restore the requested capability without exposing unrelated privileged tools.
- **Change:** Preserved verified owner context for delegated monitoring and added negative tests proving other privileged tools remained unavailable.
- **Result:** Five focused test files and 87 tests passed, alongside required CI and independent review.
- **Lesson:** Agent delegation needs narrow capability propagation, not blanket inheritance.
- **Proof:** [PR #1372: delegated monitor access](https://github.com/artemgetmann/openclaw/pull/1372)

### Reliability claims require separate proof layers

- **Problem:** Jarvis had repeated gateway crashes, but a source fix alone could not prove that an installed application would remain healthy.
- **Hypothesis:** Logs and crash reports could identify a specific source-level cause while keeping deployment and long-term runtime claims separate.
- **Change:** Connected 21 heap-limit aborts to missing adaptive heap configuration and added sizing logic with focused regression coverage.
- **Result:** Seventy-six focused tests plus type, format, and lint checks passed. The pull request explicitly did not claim lower live restart frequency before installation and observation.
- **Lesson:** Source, package, installed runtime, public release, and user-visible behavior are different receipts.
- **Proof:** [PR #1429: adaptive gateway heap sizing](https://github.com/artemgetmann/openclaw/pull/1429)

## Attribution And Limits

- Cortex is a research prototype with controlled experiments, not proof of solved continual learning or AGI.
- Jarvis is a distinct consumer product whose repository began as an OpenClaw fork. It is not OpenClaw renamed, and it is not a from-scratch claim over the inherited codebase.
- Test and source evidence do not automatically prove packaged, installed, or real-user behavior.
- Negative results stay visible because understanding where a system fails is part of the work.
