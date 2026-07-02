# Interactive Study Tool — Skill README

Generates a deployable, three-panel interactive study reference (Reference / Interactive / Drill) as a standalone static site: `index.html` + `style.css` + `data.js` + `app.js` + `vercel.json` + `README.md`. Zero-build, no frameworks, drag-and-drop or CLI deploy to Vercel.

Full generation rules live in `SKILL.md`. This file is a map of that spec, not a replacement for reading it.

## Current version: 3.0

v3.0 replaced the original CompTIA-derived terminal panel with a branching **Interaction Model** system, so the interactive panel actually fits the discipline instead of forcing every subject into a fake command line.

## How it works, at a glance

1. User gives a topic/discipline.
2. Skill proposes 3 named visual design directions **and** a default Interaction Model for the interactive panel, with one sentence on why that model fits. User can accept or override either.
3. Skill generates all six project files in one pass — fully populated, no placeholders, no stubs.

## The three panels

| Panel | Purpose | Varies by discipline? |
|---|---|---|
| Reference | Searchable sidebar + detail view for every entry | No — fixed structure |
| Interactive | Hands-on practice surface | **Yes — this is what Interaction Models control** |
| Drill | Flashcard-style recall drill with scoring | No — fixed structure |

## Interaction Models

The mechanic underneath the Interactive panel. Chosen per-discipline, confirmed with the user before any code is generated.

| Model | Mechanic | Fits | Data field |
|---|---|---|---|
| Command Sim | type → text output | CLI, SQL, programming | `simInputs` |
| Parameter Lab | adjust → visible consequence | design, physics, math | `params` |
| Diagnostic Explorer | click → identify | chemistry, biology, anatomy | `hotspots` / `specimenNote` |
| Scenario Branch | choose → outcome | law, medicine, business, history | `scenario` |
| Ear Trainer | listen → discriminate | music theory | `audioPrompt` |

Each model has its own input surface, output surface, and `app.js` functions — see the `INTERACTION MODELS` section in `SKILL.md` for full specs. Picking a model isn't cosmetic: it determines which field gets added to every entry in `data.js`.

### Known Mode Name mappings

Mode Name is the discipline-flavored label shown on the tab; Interaction Model is the mechanic underneath.

- CLI/OS/Networking → Terminal → Command Sim
- SQL/Databases → Query Lab → Command Sim
- Programming → REPL → Command Sim
- Medical/Clinical → Case Sim → Scenario Branch
- Law/LSAT → Mock Brief → Scenario Branch
- Business/Marketing → Scenario → Scenario Branch
- History → Primary Source → Scenario Branch
- Chemistry → Lab Bench → Diagnostic Explorer
- Biology / Anatomy → Specimen Lab → Diagnostic Explorer
- **Graphic Design → Layout Deck → Parameter Lab**
- Math → Proof Board → Parameter Lab
- Physics → Observation Deck → Parameter Lab
- Music Theory → Ear Lab → Ear Trainer

If a discipline isn't listed, the skill picks a model by matching the discipline's core verb (typing exact syntax, adjusting a variable, inspecting a structure, applying a rule, discriminating sounds) — and should ask rather than defaulting to Command Sim.

## Generated project structure

\```
[topic-slug]-study-tool/
├── index.html    — shell markup only, no inline style/script
├── style.css     — all CSS, tokens under :root, no hardcoded hex outside :root
├── data.js       — window.entries array, content only, no DOM code
├── app.js        — all UI logic, no content data
├── vercel.json   — static routing + cache headers
└── README.md     — deploy instructions for the generated tool (not this file)
\```

15–25 fully-written entries, 4–6 categories, minimum required fields per entry (`id`, `name`, `category`, `tag`, `tagline`, `description`, `syntax`, `switches`, `examples`, `answer`, `drillQ`, `drillE`) plus one Interaction-Model-specific field.

## Design system

- Discipline-matched font pairing + palette + one atmospheric effect, chosen from 4 atmosphere families: Light/Paper, Dark/Terminal, Clinical/Scientific, Astronomical/Space
- Full theme library with pre-built directions across STEM, Medicine, Humanities, Music/Performing Arts, Tech, Business/Law — in `SKILL.md` under `THEME LIBRARY`
- Terminology auto-adapts per discipline ("commands" → "terms/cases/theorems/reagents" etc.) — see `TERMINOLOGY ADAPTATION TABLE`

## Extending this skill

- **New discipline, existing model fits:** just use it — no file changes needed, the skill infers from the discipline table or the core-verb heuristic.
- **New discipline, no model fits well:** add a row to the Mode Name / Interaction Model table in `SKILL.md`, or define a 6th model following the pattern in `INTERACTION MODELS` (input mechanic, output surface, data field, minimum content count).
- **Renaming a Mode Name** (like Layout Deck): edit the table row directly — it's presentation only, doesn't touch the underlying model logic.

## Version history

- **v3.0** — Added the Interaction Model branching system (Command Sim / Parameter Lab / Diagnostic Explorer / Scenario Branch / Ear Trainer). Interactive panel no longer defaults to a terminal for non-CLI disciplines.
- **v2.0** — Original CompTIA-derived spec: fixed three-panel layout, terminal-only interactive panel, theme library, terminology adaptation table.