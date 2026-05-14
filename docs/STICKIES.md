# Stickies — andrewchristison.com

## Active Stickies

### Sticky 1 — Session Start (Identity + Context Load)

```
This is andrewchristison.com — a Windows 95-inspired personal desktop environment.
Repo: ~/projects/andrewchristison.com
NOT Retencity. NOT Ask K. NOT DojoFlow. NOT Pondlog. NOT CropGraph.
Read CLAUDE.md. Read BRIEF.md. Read docs/SESSION_HANDOFF.md. Read docs/STICKIES.md.
Read ALL SKILL.md files in .agents/skills/ and .claude/skills/.
Confirm exact count of skills loaded (should be 56).
Check git log --oneline -5. Report current status and await instructions.
If CLAUDE.md describes any other product besides andrewchristison.com,
STOP and alert me — wrong file loaded.
```

### Sticky 2 — Plan Before Code

```
Before writing any code:
1. Read BRIEF.md and all relevant skills for the task
2. Present a full implementation plan including:
   - Files to modify and why
   - What windows/interactions are affected
   - How this looks at desktop AND mobile breakpoints
   - Edge cases (window stacking, drag boundaries, taskbar overflow)
3. Do NOT write any code until the plan is explicitly approved.
```

### Sticky 3 — End of Session

```
End of session:
1. Open index.html in browser — visually verify no regressions
2. Confirm all windows: open, close, minimize, recover, drag, z-index
3. git status — must be clean
4. Update docs:
   - docs/CHANGELOG.md (what shipped and why)
   - docs/SESSION_HANDOFF.md (current state, next priorities)
   - docs/PRODUCT_DECISIONS.md (if any design/architecture decisions were made)
   - docs/EASTER_EGGS.md (if any Easter eggs were added)
   - CLAUDE.md session notes
5. Commit with descriptive message
6. Report top 3 priorities for next session
```

### Sticky 4 — Scrub / Audit

```
Full site audit. Read ALL SKILL.md files. Check every window, every interaction,
every link, every Easter egg. Apply all relevant skills. Report:
- Broken interactions (drag, minimize, close, recover, z-index)
- Visual regressions (palette, typography, spacing, chrome)
- Content accuracy (links, text, photo references)
- Mobile behavior at 375px
- Sound behavior
- Easter egg inventory (do they all still work?)
- What should NOT be changed
Structure findings by severity: critical / high / medium / low / verified.
No code until I approve.
```

### Sticky 5 — Diagnosis Before Fix

```
No code. Diagnose the root cause before writing any fixes.
Trace the execution path through the window manager, event listeners,
and CSS. Report findings and await instructions.
```

### Sticky 6 — UI / Win95 Aesthetic Check

```
Before shipping any UI change:
1. Does it maintain the warm Win95 aesthetic? (See BRIEF.md for design tokens)
   - Warm palette, not cold Microsoft grey
   - Proper bevels (light top-left, dark bottom-right)
   - Monospace for system chrome, content font for window interiors
   - Tactile, satisfying interactions
2. Apply frontend-design skill
3. Apply superhuman-product-philosophy skill
4. Apply microinteractions skill
5. Check: does this spark "oooo, cool. what's this?"
6. Desktop check: do windows feel like windows?
7. Mobile check at 375px: does the adapted layout hold?
8. Sound check: are audio cues present and not annoying?
```

### Sticky 7 — Window Behavior Verification

```
After any change to the window system, verify ALL of the following:
- [ ] Every window opens from its desktop icon
- [ ] Every window opens from the start menu
- [ ] Every window can be dragged by title bar (stays in viewport)
- [ ] Every window can be minimized (disappears, shows in taskbar)
- [ ] Every minimized window can be restored from taskbar
- [ ] Every window can be closed (disappears from taskbar)
- [ ] Every closed window can be reopened (icon or start menu)
- [ ] Clicking a window brings it to front (z-index)
- [ ] Two open windows stack correctly
- [ ] Start menu opens and closes
- [ ] Taskbar clock updates
- [ ] Easter eggs are still accessible
Report any failures before commit.
```

### Sticky 8 — Deploy

```
This is a static site. Deployment is a file copy.
- Netlify: git push to main (if connected) or drag-drop the project folder
- Vercel: vercel --prod
- Manual: copy index.html + assets/ to any static host
Confirm: all photo paths resolve. All Google Font links load.
All external links (retencity.com, ask-k, pondlog, cropgraph, Instagram, LinkedIn) work.
```

### Sticky 9 — Sync Skills from gundry-agents

```
cp -r ~/projects/gundry-agents/.agents/skills/. ~/projects/andrewchristison.com/.agents/skills/
cp -r ~/projects/gundry-agents/.claude/skills/. ~/projects/andrewchristison.com/.claude/skills/
cd ~/projects/andrewchristison.com
git add .agents/skills/ .claude/skills/
git commit -m "chore: sync skills from gundry-agents"
After copying, review and remove any skills that don't apply
(e.g., ingestion pipeline, retrieval eval, Zendesk-specific skills).
```

### Sticky 10 — Easter Egg Inventory

```
When adding an Easter egg:
1. Describe what it is, where it lives, how it's triggered
2. Add it to docs/EASTER_EGGS.md
3. Verify it doesn't break any window or interaction
4. Verify it's discoverable but not obvious
5. Verify it sparks delight — would someone screenshot this and share it?
```

That's all 10. Stickies 6-12 from Ask K (ingestion, retrieval, Zendesk, system prompt) are not applicable to this project and have been replaced with project-appropriate rules for window behavior, aesthetics, and Easter eggs.

---

## Lessons Learned

_This section tracks real incidents that produced new rules. Each entry: date, what happened, what rule prevents recurrence._

_(None yet — this is a new project. First entries will come from the build.)_
