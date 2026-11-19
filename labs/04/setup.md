# Lab 4 · Task 1 · Set up my agent and find its brakes

- **Tool:** GitHub Copilot chat (agent) built into VS Code 1.147.0, in a GitHub Codespace (Blank template), opened in Chrome. No install needed, so it also works from my iPad.
- **Plan:** Copilot Free
- **Throwaway repository:** `~/agent-test` in the Codespace, outside my lab repository. Deleted after the test.
- **Date:** 19.11.2026
- **How I worked:** Claude (Anthropic) drove this test session for me through the Claude in Chrome extension. The observations below are what Copilot actually did in that session (see `AI_USAGE.md`).

## A first session

Prompt: *What files are in this folder? Do not change anything.*

- Copilot answered: the folder contains `.git/` and `README.md`.
- Tools: it **ran 2 terminal commands** to look (a `find … -maxdepth 1` listing and a `git --no-pager …` check). It did not ask before running them. It changed nothing.

## Find the brakes

| Test | What happened |
|---|---|
| Permission mode at the start | *Manual permissions* ("asks when approval settings don't apply"), together with the mode *Interactive*. Other options in the picker: *Assisted permissions* (marked "Recommended", a model evaluates the risk) and *Allow all*. I kept *Manual*. |
| *Create a file hello.txt with the line Hello.* | Copilot wanted to run `printf 'Hello\n' > hello.txt && cat hello.txt` in the terminal and **asked first** (*Allow Once / Skip / Explain*). I allowed it once. `git status` then showed `hello.txt` as an untracked file. Because the change was made by a terminal command, the chat listed "0 files changed", so there was nothing to undo in the chat. I deleted the file with `rm hello.txt`, and `git status` was clean again. |
| *Run git log.* | It ran `git --no-pager log` **without asking** and summarised the one commit ("Start a test repository"). Read-only commands seem to be auto-approved. |
| Plan mode: `/plan Add a script that counts the files in this folder.` | Before planning, it read `README.md`, ran 1 command and asked me a question (count only top-level files, or recursively?). The plan: add an executable `count-files.sh` at the root that counts regular top-level files, including hidden ones, and test it. I clicked **Ablehnen** (reject). Nothing was created in the folder. However, the plan itself was saved without asking outside the workspace, in `~/.copilot/session-state/…/plan.md`. The highlighted default button under the plan was *Implement with Autopilot*, so it is easy to click the wrong one. |

## Find out

| Question | Answer |
|---|---|
| Which tool, which version? Which model? | GitHub Copilot chat in VS Code 1.147.0 (web, Codespace), Copilot Free. Model picker: *Copilot Fusion* (= Auto). For my prompts, it chose **MAI Code 2 Flash** ("the best choice out of the models available in your plan"). |
| Permission mode at start, how to switch | Started in *Manual permissions*. Switch it with the picker under the chat input (*Pick Permissions*): Manual / Assisted / Allow all. The mode next to it switches between *Interactive* and *Plan* (or use `/plan`). |
| What did it do without asking? | **Read files:** yes (listed the folder, read `README.md`). **Run commands:** read-only commands yes (`find`, `git status`, `git log`). It asked before a command that writes a file. **Edit files:** in the folder, only after asking. Outside the workspace, it wrote its own plan file without asking. |
| How do I see and undo changes? | Each turn shows "View turn changes" (files and lines changed) with a diff. Edits can be thrown away from the chat ("Discard changes"). Changes made by terminal commands do not appear there, so `git status` / `git diff` and Git (as in lab 3) are the safe way to see and undo them. |
| Fresh session, context window, quota | New chat with **+** (*Neuer Chat*, Ctrl+N). The context window is shown by a small ring icon in the chat input (*Verwendung des Kontextfensters*). Each answer shows its cost, for example "0,4 credits" for the first answer. After the whole task, **1 %** of the included credits of Copilot Free were used (github.com/settings/copilot → Usage). |
| Which instruction files does it read? | `AGENTS.md` in the repository, plus `.github/copilot-instructions.md` (according to the course table and the VS Code documentation; not tested here, because the test repository had none). |
| May my prompts and code be used for training? | Setting: github.com/settings/copilot → Privacy → *Allow GitHub to use my data for AI model training*. At the time of the test, it was **enabled**, which is the default for Copilot Free. |

## Why this tool?

Copilot is free for me (Copilot Free now, Copilot Student once it is active) and runs inside VS Code in a Codespace, so I can use it from the browser on my iPad without installing anything. Its main weakness is data protection: on Copilot Free, GitHub may train on my prompts unless I switch the setting off. It is not open source, and the free plan has a monthly credit limit, so I need to watch the usage meter. Because my team also works on GitHub and in VS Code, Copilot is easy to share and keeps us consistent. The test also showed that its brakes need checking: it ran read-only commands and saved its plan without asking, and the default button suggests Autopilot.
