# Staff engineer review — final staged Staff Designer candidate

**Verdict: APPROVE the exact v3 snapshot for activation.** The three conflicts in my first review are resolved in the loaded guidance. I found no remaining blocker in this scoped patch. Approval is tied to the source hashes below; the tests support no observed regression on three synthetic cases, not general superiority or guaranteed future behavior.

## Findings

**None requiring revision.** The full critique template now asks whether depth treatments clarify grouping and layer order ([`critique.md:202`](/Users/alan/Desktop/apps/staff-designer/skills/staff-designer/critique.md:202)), consistent with its method at line 105. The checklist now requires an observed hierarchy, usability or approved-brief failure before assigning severity to visual choices ([`checklists.md:190`](/Users/alan/Desktop/apps/staff-designer/skills/staff-designer/references/checklists.md:190)); its white-card and font rows at lines 196 and 217 are conditional. The typography reference retains its user-visibility rule without calling Staff Designer a scored critique ([`typography.md:27`](/Users/alan/Desktop/apps/staff-designer/skills/staff-designer/references/typography.md:27)). A search of the loaded package found no surviving one-depth, four-level, automatic-warning or numeric Staff Designer scoring instruction. The separate `/typeset` score-table reference in unchanged `SKILL.md` remains correctly scoped to Typeset.

## Evidence

- I re-read the raw `git diff` against `06d9563f8a1181ffa77dcbc687a3af20352256b8`, including the untracked `tests/scoped-review/` evidence. The source scope remains `critique.md`, three loaded references and the matching repository README. `SKILL.md`, Typeset and installation wiring are unchanged. The vault README's two source-location corrections were checked in the first pass. The candidate archive `tests/scoped-review/candidate-v3.tar.gz` contains the five loaded skill files, and I compared every archived file byte-for-byte with the staged checkout and the v3 blind package. All five match. `git diff --check` passes.
- I read the three fresh v3 raw critiques and their exact isolated prompts, then compared them with the retained v1/v2 reviews, frozen fixtures, source and measurements. The corrected clean control received grounded preview-context and mobile-placement suggestions without a palette, mixed-depth, system-font or hierarchy-count blocker. The flawed case still exposed mobile overflow, the non-keyboard request action, disappearing owner and low-contrast active Export label; it also identified the incomplete preview. The plan review found the draft-persistence contradiction, premature Assigned status and duplicate-submission risk, and separated unbuilt visual questions from observed defects. None of the nine valid runs emitted a numeric Design Score or an unrelated product pivot. The first baseline control found real incomplete fixture behavior and is properly retained outside the valid comparison.
- The v3 archive closes the prior replay gap for the candidate package. Prompts, fixtures, screenshots, measurements, baseline archive, earlier v2 archive, raw outputs and hash manifests are retained. The source hash manifest and the v3 blind package agree with the current staged files. The installed package and host links remain at the original baseline; this review did not activate them. Accessibility, motion and mobile checklist sections were not removed; the v3 flawed review still detected keyboard and contrast failures.

## Verification limits

These are one fresh generative review per candidate version and case, using synthetic designs and a plan. Their outputs establish coverage on those cases only. The prompts and preserved files document the inputs; the prose outputs alone do not authenticate the reported model, concurrency or isolation. The reviewers inspected supplied images/source and did not independently operate the browser or assistive technology. All-palette behavior, portfolio and print critiques, actual CSV delivery, and Alan's real project corpus remain untested. The candidate is still on an unpublished branch, so an installer targeting GitHub main would receive the old version until the exact reviewed source is landed or another versioned activation path is used. Recheck hashes if any source changes before activation.

## Reviewed SHA-256 snapshot

| Source | SHA-256 |
|---|---|
| `skills/staff-designer/SKILL.md` | `4525c3daa38760e454aa7aa9e8f5918112f6137c0d38ea01ffd8072b126fd887` |
| `skills/staff-designer/critique.md` | `477f8e5d18c3a9868d6b8749e8db3c8138ec471bdf282469f1f3225f1ec6bab8` |
| `skills/staff-designer/references/checklists.md` | `4f7a34a547388260ebebe2be83d73c510a2a23e46dea63b59eebae54a06dedde` |
| `skills/staff-designer/references/interaction.md` | `7a8ad9e0212953dfa484a51f68208a99dd632ecc21d91f136ddc06ee28afb06f` |
| `skills/staff-designer/references/typography.md` | `8896799a3a471e13721c533caad7c6343d705ef30edb3ee50d3b8739bd2a88a5` |
| `README.md` | `1b37836e8deaab62f7818da85c8b334deba083d8c5d53f61d6dc83a84b9b853b` |

The reviewed v3 archive SHA-256 is `c1f6df80d120750315963882f0eb86cde22e1152c35bab563a29edba5b9855fc`.
