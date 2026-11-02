# Sola Payments — private homepage cloning trial

Prepared November 2, 2026. This is a prompt for a future execution run; preparing this file did not clone or deploy Sola's website.

[Workflow and compatibility guide](../REUSE-GUIDE.md).

## Where to use it

Paste the complete prompt below into Claude Code, Codex, a ChatGPT Work environment that can run the required tools, or the existing Agent Zero runtime. Each environment must verify its own capabilities. The prompt is intentionally normal language, so it does not assume support for Claude's slash commands.

For Claude Code, an optional opening is:

```text
/goal Complete the Sola Payments task below until Remake's actual report passes and the specified manual checks pass, or stop after 100 turns with a saved checkpoint.
```

Paste the full task immediately after that opening. In another agent, omit the slash-command opening and use the task alone.

## Ready-to-paste task

```text
Create a private, high-fidelity reference copy of the complete Sola Payments homepage, using my Remake engine fork.

TARGET
- Public website: https://solapayments.com/ (the site also requested as www.solapayments.com).
- Engine source: https://github.com/avromy/remake
- Website project name: sola-payments-reference
- Intended website repository: avromy/sola-payments-reference, PRIVATE.
- Scope for this first trial: the entire homepage, from header to footer, at desktop and phone sizes. Include its observed menus and visual interactions. Do not automatically expand into a whole-site crawl.

1. USE THE CORRECT ENGINE
Read the repository's AGENTS.md, docs/REUSE-GUIDE.md, plugins/remake/skills/remake/SKILL.md, and relevant reference files.
The inherited setup instructions point to rubenhassid1/remake. Adapt that setup to use avromy/remake instead. Before reusing an engine installation, verify its remote and revision. Use a separate checkout if necessary, and invoke that checkout's engine/bin/remake.mjs directly to avoid accidentally running another installation.
Keep the website project separate from the engine repository. If the named website project already exists, inspect and resume it without overwriting unrelated work.

2. VERIFY THE EXECUTION ENVIRONMENT
Check Node 20+, dependencies, runnable Playwright Chromium, filesystem access, network access, and the ability to inspect screenshots and run a local preview.
For deployment, separately verify GitHub CLI and Vercel CLI authentication and the intended account. Do not assume connected apps or a browser login authenticate these CLIs.
Use the existing runtime and its allowed tools. In Agent Zero, verify its own browser/runtime; do not assume it can access a ChatGPT browser session.
Continue any useful local work if only deployment access is missing. Request only the specific authorization or access genuinely needed to unblock the remaining step.

3. INSPECT AND REPRODUCE THE REFERENCE
Verify the reference URL at run time. Inspect the full homepage on desktop and phone before making design decisions.
Capture and reproduce the actual layout, typography, spacing, colors, image proportions, backgrounds, header, navigation, footer, and observable animations/interactions. Match the reference rather than inventing a replacement design.
Use the current live page as the authority. The research snapshot includes the hero, customer-logo section, platform and merchant sections, support content, company section, product spotlight, customer story, resources, final call to action, and footer; verify the current order and content rather than assuming this list is unchanged.
Use the engine's one-page scope. Do not replace sections with screenshots or embed the live site as the finished result.

4. KEEP THE TRIAL LIMITED TO PUBLIC MARKETING
Exclude merchant portals, sign-in/account pages, sandbox registration, checkout, payment entry, and transaction APIs. Preserve any relevant menu appearance, but keep excluded destinations inactive in the copy and explain that they are outside scope.
Keep contact/newsletter forms and other outbound submissions inactive. Do not send information to Sola or its partners.
If access is blocked, report the exact blocker and preserve progress; do not bypass access controls or silently change the reference source.

5. COMPARE, REPAIR, AND VERIFY
Run the documented capture, score, repair, slots, and board workflow. Use its normal desktop and phone measurements and motion checks. Inspect the actual difference images, fix the largest problems, and re-run the relevant checks after meaningful changes.
Keep the original measurement thresholds and reference files intact. Disclose any accepted exception with the remaining difference and reason.
Separately check menu opening/closing, responsive layout, scrolling, hover states, image loading, and layout overflow. Clearly identify any interaction outside scope. Do not equate a visual score with working backend functionality.

6. DELIVER A PRIVATE PREVIEW
Using my existing authorized accounts, save the website in its separate private repository and deploy a passcode-protected Vercel preview with indexing disabled. Do not attach a public custom domain or remove the passcode. Do not incur new paid services without approval.
Verify the deployed page at desktop and phone widths and verify access is blocked without the passcode and works with it. Keep credentials/passcodes out of committed files; deliver the preview passcode privately.
Provide the real Remake report, the comparison page, and the replacement board. Do not label the task complete unless the report and the manual checks actually support that result. If deployment remains blocked, report local progress and the outstanding deployment gate explicitly.

7. FINISH WITH A REUSABLE CHECKPOINT
Return the repository and commit, engine revision, private preview, comparison and replacement-board links, actual measured results, manually checked interactions, remaining differences, and any required owner action.
Save a concise README with setup/reproduction steps and a precise resume checkpoint. Continue through ordinary repairs; stop only on verified completion, a genuine blocker, or the 100-turn limit. At a blocker or limit, preserve completed work and identify the exact next action. Do not claim background continuation that the host does not provide.
The first deliverable is this private reference copy. Business rebranding, asset replacement, and a React/Next.js rebuild are later stages.
```

## Optional expansion after the homepage passes

To test additional public pages, use this follow-up after reviewing the first result:

```text
Continue the existing sola-payments-reference project from its verified checkpoint. Preserve the completed homepage. Propose and then implement a bounded expansion to up to five additional public marketing pages from the site's current primary navigation, choosing the most relevant platform and merchant pages. Treat ordinary page selection as your implementation decision; do not ask me to approve each page. Keep sign-in, merchant portals, sandbox registration, checkout, payment APIs, and outbound submissions excluded. Capture, compare, repair, and report each added page. Retain the private repository, passcode protection, and the same evidence requirements.
```

## Evidence and scope notes

The [public homepage](https://solapayments.com/) was retrieved for its current content and navigation. Its navigation includes platforms, merchants, developers, company, resources, and sign-in destinations. The site exposes real merchant/partner account links; the trial excludes those services. Desktop/mobile animation and timing were not established by text retrieval, so the prompt requires fresh visual inspection during execution.

The homepage-only scope is a deliberate first-test boundary. A request for a prompt is not a record that the clone, deployment, or Agent Zero integration has already been executed.

Technical instructions were checked against Remake baseline `895744f0fb00d7151540a29d4f680c2e269fe644`. See the [guide's primary sources](../REUSE-GUIDE.md#sources).
