# Reusing Remake with Claude Code, ChatGPT/Codex, or Agent Zero

Reviewed: November 2, 2026. Engine baseline: [`895744f0fb00d7151540a29d4f680c2e269fe644`](https://github.com/avromy/remake/commit/895744f0fb00d7151540a29d4f680c2e269fe644).

**Start here:** [Sola Payments trial prompt](prompts/SOLA-PAYMENTS.md).

This guide documents a repeatable workflow based on the public tutorial, the repository's actual code, and official product documentation. The embedded tutorial video was not directly reviewed. The compatibility conclusions are a source review, not a completed cloning test in Claude Code, Codex, ChatGPT Work, or Agent Zero.

## 1. What has been copied, and what happens next?

There are three different operations:

| Operation | Result |
| --- | --- |
| Fork the Remake repository | A copy of the cloning tool on GitHub. This is already available as `avromy/remake`. |
| Clone the repository locally | A working copy of the tool in a computer or agent workspace. |
| Use Remake on a website | A separate project containing the captured website, comparison evidence, and replacement checklist. |

The engine repository is [avromy/remake](https://github.com/avromy/remake). Its upstream is [rubenhassid1/remake](https://github.com/rubenhassid1/remake). Keep generated website projects separate from the engine repository. In particular, do not put a captured company's website into this public fork.

### How to repeat the GitHub fork operation for another tool

1. Open the source repository on GitHub.
2. Choose **Fork**.
3. Select the intended owner and repository name.
4. Clear **Copy the main branch only** when all branches are wanted.
5. Create the fork, then verify the owner, upstream relationship, files, and branch status.

Do not repeat this operation for Remake: this fork already exists. Future website experiments reuse the engine and create their own project folders/repositories.

## 2. Does it require Claude?

**The core engine does not require Claude.** `package.json` defines a Node.js command-line program with `parse5`, `playwright`, and `pngjs` dependencies, and requires Node 20 or newer. The capture/scoring commands do not invoke an Anthropic SDK or Claude executable. Claude-specific integration lives in the plugin, command instructions, reviewer instructions, and `/goal` workflow. [Sources: package, CLI, plugin.](#sources)

| Environment | Practical answer | What needs adapting or verifying |
| --- | --- | --- |
| Claude Code | The intended integration and the closest match to the author's tutorial. | Install the engine, supply the reference URL, and follow its repair/report workflow. Verify the fork source during setup. |
| Codex | The same CLI can in principle be driven by Codex. | Provide a runnable terminal, dependencies, network access, screenshots, and a writable workspace. Translate Claude-specific instructions into ordinary task instructions. |
| ChatGPT with suitable Work/coding tools | Possible when that actual environment can run Node, launch Chromium, write files, and reach the reference site. | Inspect the capabilities of the current session. A GitHub connection alone does not establish an execution environment. |
| ChatGPT conversation without those execution tools | Useful for planning, writing prompts, and reviewing results. | Execute the engine in a separately equipped environment. |
| Agent Zero | The engine can in principle be operated through its command-execution tools. | Verify dependencies, browser launch, network access, persistent project storage, screenshot review, and deployment authentication in the existing runtime. |

OpenAI documents command execution and local development tools in Codex CLI; Work capabilities depend on its environment and permissions. Agent Zero documents a Docker workspace and its own browser. These establish relevant platform capabilities, not a tested Remake integration. [Sources: OpenAI CLI, Work, Agent Zero.](#sources)

The `/goal` instruction belongs to Claude Code's orchestration. It is not a Remake CLI command. Anthropic documents it as continuing work until a condition or turn cap is reached. In Codex/ChatGPT or Agent Zero, express the same repair-and-check loop in normal language. A prompt does not by itself create a background service or guarantee that a host session will keep running indefinitely.

## 3. Important fork setup detail

The inherited `plugins/remake/skills/remake/SKILL.md` still tells an agent to clone Ruben's upstream into `~/.remake`. Merely linking to this fork in a prompt does not ensure that the installed engine comes from the fork.

For this fork, explicitly instruct the executing agent to:

- Use `https://github.com/avromy/remake` as the engine source.
- Inspect an existing engine checkout's remote and revision before reusing it.
- Use a separate checkout if the existing one belongs to another project or source.
- Run the CLI by its absolute path when necessary, so an old globally installed `remake` command cannot silently take precedence.
- Retain the author's attribution and license.

The supplied Sola prompt includes this correction. This documentation change does not rewrite the inherited engine or plugin instructions.

## 4. What the execution environment needs

### For capture, comparison, and repair

- Node.js 20 or newer and the package dependencies.
- Playwright Chromium plus the operating-system libraries needed to launch it.
- Network access to the reference page and its public resources.
- A writable project folder and permission to start subprocesses and a local server.
- An agent able to inspect comparison images, edit the project, and re-run checks.

Remake launches its own Playwright browser. For a public marketing page, this does not inherently require access to ChatGPT's signed-in browser or a personal browser profile. Its preview server listens on `127.0.0.1`; a remote viewer needs an approved route to that runtime's preview. [Sources: browser and serve code.](#sources)

### For the repository's deployment workflow

The `ship` command additionally needs git and authenticated GitHub and Vercel CLIs. A connected GitHub plugin in one product is not evidence that `gh` is signed in inside another machine or container. Verify the target account before creating the website repository. [Source: ship code.](#sources)

`doctor` checks deployment credentials as well as local dependencies. Read its individual findings: missing deployment authentication need not stop useful local capture and comparison. [Source: doctor code.](#sources)

The existing shell instructions are written in a Unix style. Linux/container/WSL or macOS is a clearer starting point; native Windows execution was not tested in this review. This is an inference from the setup and process-launch code, not a finding that Windows cannot work.

## 5. Repeatable workflow for a new website

### Step 1 — Specify the experiment

Record the reference URL, pages in scope, project name, intended output, and the point at which the task should stop. For a first test, start with the complete homepage at desktop and phone sizes. Broader page coverage can follow after the first result is verified.

Decide whether the immediate goal is a private visual reference, a rebranded marketing site, or an editable application. Treat each as a distinct stage.

### Step 2 — Verify and prepare the runtime

Use the engine source described above. Check Node, browser launch, filesystem access, and network access. Identify deployment authentication separately. Preserve any existing project with the chosen name and inspect it before resuming.

### Step 3 — Inspect and capture

Inspect the reference at desktop and phone widths. Record the page structure and interactions that will be assessed. Capture the agreed public pages and their resources using the engine's documented process.

### Step 4 — Compare and repair

Run scoring, examine the actual difference images, and repair the largest problems. Recheck after meaningful changes. Keep a record of failures and fixes. Do not substitute screenshots or an iframe of the live reference for working page markup, and do not change the measurements to manufacture a pass. [Source: Remake skill instructions.](#sources)

### Step 5 — Review interactions separately

Check navigation menus, responsive layout, scrolling, hover states, and visible controls. Confirm whether each control is functional, intentionally inactive, or outside scope. A visual comparison cannot prove that a form sends email or that a backend service exists.

### Step 6 — Produce the private preview and evidence

When deployment is within scope and account access is available, use a separate private website repository and a passcode-protected preview. Verify the actual deployed result. Keep credentials and passcodes out of committed documentation.

If deployment is blocked, finish the available local work and state exactly what remains. Do not change the engine's report to disguise an incomplete deployment.

### Step 7 — Adapt the result to the intended business

Use the replacement board to track copy, images, video, logos, fonts, colors, links, and form destinations. Replace these deliberately, then review the final layout. Keep reference material private while it remains a reference copy. [Source: swap guidance.](#sources)

### Step 8 — Preserve a usable checkpoint

Record the engine revision, project location, repository/commit, preview location, latest evidence, completed checks, outstanding issues, and exact next action. A successor should be able to resume without repeating completed capture or repair work.

## 6. Understanding the completion evidence

The documented visual defaults use desktop `1440 × 900` and phone `390 × 844`, with a 98% threshold for stable screenshot pixels, 95% for sampled motion frames, and page-height tolerance of 4 pixels. Unstable pixels are masked, and color comparisons use a tolerance. These numbers describe the measurement, not full functional equivalence. [Sources: project defaults and scoring documentation.](#sources)

| Status | Meaning |
| --- | --- |
| Local capture completed | Files were captured and the local page can be examined. |
| Visual checks passed | The measured views meet their thresholds, subject to any disclosed exceptions. |
| Engine report complete | All report gates pass, including its deployment requirement. Read the entire report. |
| Branded result reviewed | The current customized pages have been visually and functionally examined. This needs separate evidence. |

Two details deserve attention:

1. The normal report includes a live/private deployment gate. A local-only exercise cannot truthfully claim the standard complete status.
2. After content swaps, the report can reuse the last pre-swap score. Review the final customized appearance afresh. The preserved score describes the earlier reference match. [Source: report code.](#sources)

The documented acceptance mechanism permits certain recorded exceptions. Do not quietly treat an accepted difference as an exact match. If deployment evidence shows a hosting checkpoint rather than a fully verified preview, resolve that check before presenting the preview as verified.

## 7. Command reference for the executing agent

These are instructions for a future run; they were not executed against Sola while preparing this guide. The examples assume a Unix-style shell and an empty engine destination. Inspect existing folders first.

```bash
git clone https://github.com/avromy/remake.git ./remake-engine
cd ./remake-engine
npm ci
npx playwright install chromium
REMAKE_ENGINE_DIR="$PWD"
node "$REMAKE_ENGINE_DIR/engine/bin/remake.mjs" doctor
```

Resolve missing operating-system dependencies through the runtime's supported installation process. Read `doctor` findings individually; authentication is required for deployment but is not used by capture/scoring itself.

The following block assumes the same shell session. If an agent starts a new shell for each command, re-establish `REMAKE_ENGINE_DIR` and `REMAKE_PROJECT_DIR` as absolute paths in every call; variables from an earlier call may not survive.

```bash
REMAKE_TARGET_URL="https://example.com/"
REMAKE_PROJECT_DIR="$HOME/remakes/example-reference"
node "$REMAKE_ENGINE_DIR/engine/bin/remake.mjs" init "$REMAKE_TARGET_URL" --pages 1 --dir "$REMAKE_PROJECT_DIR"
node "$REMAKE_ENGINE_DIR/engine/bin/remake.mjs" capture --dir "$REMAKE_PROJECT_DIR"
node "$REMAKE_ENGINE_DIR/engine/bin/remake.mjs" score --dir "$REMAKE_PROJECT_DIR"
node "$REMAKE_ENGINE_DIR/engine/bin/remake.mjs" slots --dir "$REMAKE_PROJECT_DIR"
node "$REMAKE_ENGINE_DIR/engine/bin/remake.mjs" board --dir "$REMAKE_PROJECT_DIR"
node "$REMAKE_ENGINE_DIR/engine/bin/remake.mjs" report --dir "$REMAKE_PROJECT_DIR"
```

Scoring is followed by image inspection and repairs, not simply by ignoring a nonzero exit code. To view the project, run `serve --dir "$REMAKE_PROJECT_DIR"` through the same CLI path in a suitable background session. The process remains running until stopped. Use `ship` only for the agreed destination after checking account access and project identity. Check the current CLI help before changing options. [Source: CLI implementation.](#sources)

## 8. Optional features and common misunderstandings

### Image generation

The Codex image adapter is optional. Its code looks for a Codex executable and local Codex authentication, then runs an image task. A ChatGPT subscription or browser login alone does not establish that this path will work. Other image sources are supported, and new image generation can wait until the branding stage. [Source: images code.](#sources)

### Editable applications

The default clone preserves captured HTML, CSS, and JavaScript. The separate rebuild guidance converts it to React or Next.js incrementally, retaining a reference and checking changes section by section. This is additional work; it is not an automatic property of the initial capture. [Source: rebuild guidance.](#sources)

### Backend functionality

A page populated with captured API responses is not a recreated database, payment system, authentication service, or email backend. Specify and implement needed business functions separately. For a payment-company marketing reference, keep merchant portals and transaction flows outside the cloning scope. [Sources: README and runtime code.](#sources)

### Keeping the fork current

Review upstream changes before syncing them. This fork now has its own documentation, so preserve those files when updating. Record the engine revision used for each successful run; future changes can alter behavior.

## 9. Starting future work

For Sola, use the [complete trial prompt](prompts/SOLA-PAYMENTS.md). It includes the source correction, scope, evidence, private output, and resume requirements.

For another website, replace the target URL, project/repository name, and page-specific observations. Keep the runtime checks, source identity, comparison evidence, and truthful completion reporting. In Claude Code, the file includes a `/goal` wrapper. For Codex, ChatGPT Work, or Agent Zero, paste the full normal-language prompt.

## Sources

All repository links below pin the reviewed engine baseline; they do not imply a runtime integration test.

- [Original written tutorial](https://ruben.substack.com/p/claude-jacking).
- [Package and dependencies](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/package.json).
- [CLI implementation](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/engine/bin/remake.mjs).
- [Claude plugin definition](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/.claude-plugin/marketplace.json).
- [Remake skill and inherited setup](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/plugins/remake/skills/remake/SKILL.md).
- [Browser launch](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/engine/lib/browser.mjs), [local preview server](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/engine/lib/serve.mjs), and [doctor](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/engine/lib/doctor.mjs).
- [Deployment](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/engine/lib/ship.mjs) and [completion report](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/engine/lib/report.mjs).
- [Project defaults](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/engine/lib/project.mjs) and [scoring documentation](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/docs/HOW-IT-WORKS.md).
- [Image adapters](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/engine/lib/images.mjs).
- [Content replacement](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/plugins/remake/skills/remake/references/swap.md) and [editable rebuild](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/plugins/remake/skills/remake/references/rebuild.md).
- [README limitations](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/README.md) and [captured-response runtime](https://github.com/avromy/remake/blob/895744f0fb00d7151540a29d4f680c2e269fe644/engine/templates/runtime.js).
- [Official OpenAI: Codex CLI](https://learn.chatgpt.com/docs/cli) and [ChatGPT Work environments and permissions](https://learn.chatgpt.com/docs/enterprise/chatgpt-work-overview).
- [Official Anthropic: goal-based loops](https://claude.com/resources/articles/getting-started-with-loops).
- [Official Agent Zero: installation and workspace](https://www.agent-zero.ai/p/docs/installation/) and [browser guide](https://github.com/agent0ai/agent-zero/blob/main/docs/guides/browser.md).
