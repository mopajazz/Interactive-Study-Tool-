# Interactive Study Tool Skill

Generate a deployable, three-panel interactive study reference as a standalone static site.

The skill creates a complete zero-build project with:

- `index.html`
- `style.css`
- `data.js`
- `app.js`
- `vercel.json`
- `README.md`

The generated site includes three learning modes:

1. **Reference** — searchable study reference
2. **Interactive** — hands-on practice surface
3. **Drill** — flashcard-style recall drill with scoring

This README explains how to use the skill. The full generation rules live in `SKILL.md`.

---

## Current Version

**Version:** `3.0`

Version 3.0 replaces the original fixed terminal-style interaction with a flexible **Interaction Model** system.

Instead of forcing every subject into a fake command-line simulator, the skill now chooses an interactive mechanic that fits the discipline.

---

## What This Skill Does

The Interactive Study Tool skill generates a complete static study site for a topic or discipline.

For example, you can ask it to generate study tools for:

- Graphic design principles
- SQL queries
- Medical case review
- Music theory ear training
- Chemistry lab identification
- Anatomy review
- Business scenarios
- History source analysis
- Math proofs
- Physics concepts
- Programming syntax

The output is a ready-to-deploy static web app.

---

## How to Use the Skill

Start by giving the skill a topic or discipline.

Example prompts:

```text
Create an interactive study tool for graphic design principles.
```

```text
Create a study tool for SQL joins and filtering.
```

```text
Build an interactive study reference for basic anatomy.
```

```text
Generate a study tool for music theory intervals.
```

```text
Create a deployable study tool for clinical decision-making basics.
```

The skill will first propose:

1. Three visual design directions
2. A recommended Interaction Model
3. A short explanation for why that model fits the discipline

You can accept the default recommendation or override the design direction and interaction model.

---

## Recommended Prompt Format

For best results, use this format:

```text
Create an interactive study tool for [topic].

Audience: [learner level]
Tone: [plain, academic, playful, clinical, professional, etc.]
Preferred visual direction: [optional]
Preferred interaction model: [optional]
Deployment target: Vercel
```

Example:

```text
Create an interactive study tool for graphic design layout principles.

Audience: first-year design students
Tone: clear, visual, and practical
Preferred visual direction: modern studio desk
Preferred interaction model: Parameter Lab
Deployment target: Vercel
```

---

## What the Skill Generates

Each generated project uses this structure:

```text
[topic-slug]-study-tool/
├── index.html
├── style.css
├── data.js
├── app.js
├── vercel.json
└── README.md
```

### File Responsibilities

| File | Purpose |
|---|---|
| `index.html` | Shell markup only. No inline style or script. |
| `style.css` | All visual styling, layout, tokens, and atmosphere. |
| `data.js` | Study content stored in `window.entries`. No DOM logic. |
| `app.js` | UI behavior, filtering, interaction logic, and drill logic. |
| `vercel.json` | Static routing and cache headers for Vercel deployment. |
| `README.md` | Deployment and usage instructions for the generated tool. |

---

## The Three Panels

Every generated study tool includes the same three-panel structure.

| Panel | Purpose | Discipline-specific? |
|---|---|---|
| Reference | Searchable sidebar and detail view for every entry | No |
| Interactive | Hands-on practice surface | Yes |
| Drill | Flashcard-style recall drill with scoring | No |

---

## Interaction Models

The **Interaction Model** controls the mechanic used in the Interactive panel.

This is not just a visual label. The selected model determines:

- The interactive interface
- The output behavior
- The required data field in `data.js`
- The related functions in `app.js`

| Interaction Model | Mechanic | Best For | Required Data Field |
|---|---|---|---|
| Command Sim | Type input and receive text output | CLI, SQL, programming | `simInputs` |
| Parameter Lab | Adjust variables and see consequences | Design, physics, math | `params` |
| Diagnostic Explorer | Click or inspect to identify parts | Chemistry, biology, anatomy | `hotspots` / `specimenNote` |
| Scenario Branch | Choose an action and see the outcome | Law, medicine, business, history | `scenario` |
| Ear Trainer | Listen and discriminate sounds | Music theory | `audioPrompt` |

---

## Mode Name Mappings

The **Mode Name** is the discipline-flavored label shown in the interface.

The **Interaction Model** is the underlying mechanic.

| Discipline | Mode Name | Interaction Model |
|---|---|---|
| CLI / OS / Networking | Terminal | Command Sim |
| SQL / Databases | Query Lab | Command Sim |
| Programming | REPL | Command Sim |
| Medical / Clinical | Case Sim | Scenario Branch |
| Law / LSAT | Mock Brief | Scenario Branch |
| Business / Marketing | Scenario | Scenario Branch |
| History | Primary Source | Scenario Branch |
| Chemistry | Lab Bench | Diagnostic Explorer |
| Biology / Anatomy | Specimen Lab | Diagnostic Explorer |
| Graphic Design | Layout Deck | Parameter Lab |
| Math | Proof Board | Parameter Lab |
| Physics | Observation Deck | Parameter Lab |
| Music Theory | Ear Lab | Ear Trainer |

If the discipline is not listed, the skill should choose a model based on the discipline’s core learner action:

| Learner Action | Recommended Model |
|---|---|
| Typing exact syntax | Command Sim |
| Adjusting a variable | Parameter Lab |
| Inspecting a structure | Diagnostic Explorer |
| Applying a rule to a situation | Scenario Branch |
| Discriminating sounds | Ear Trainer |

If the best model is unclear, the skill should ask before generating code.

---

## Content Requirements

Each generated tool should include:

- 15–25 fully written entries
- 4–6 categories
- Complete instructional content
- No placeholders
- No stubs
- No empty demo data

Every entry must include these fields:

```js
id
name
category
tag
tagline
description
syntax
switches
examples
answer
drillQ
drillE
```

Each entry must also include one field specific to the selected Interaction Model:

| Interaction Model | Required Field |
|---|---|
| Command Sim | `simInputs` |
| Parameter Lab | `params` |
| Diagnostic Explorer | `hotspots` or `specimenNote` |
| Scenario Branch | `scenario` |
| Ear Trainer | `audioPrompt` |

---

## Design System

The skill chooses a design system that matches the discipline.

Each generated tool should include:

- Discipline-appropriate font pairing
- Matching color palette
- One atmospheric effect
- Consistent spacing and layout
- CSS tokens under `:root`
- No hardcoded hex colors outside `:root`

Atmosphere families include:

| Atmosphere Family | Best For |
|---|---|
| Light / Paper | Humanities, writing, general study |
| Dark / Terminal | CLI, networking, programming |
| Clinical / Scientific | Medicine, anatomy, chemistry, biology |
| Astronomical / Space | Physics, systems, abstract concepts |

---

## Example Workflow

A typical workflow looks like this:

1. User requests a study tool for a topic.
2. Skill proposes three visual design directions.
3. Skill recommends an Interaction Model.
4. User accepts or modifies the direction.
5. Skill generates all six project files in one pass.
6. User downloads or copies the project.
7. User deploys the static site to Vercel.

---

## Example Prompt and Response Flow

### User Prompt

```text
Create an interactive study tool for graphic design layout principles.
```

### Skill Should Propose

```text
Recommended Interaction Model: Parameter Lab

Why: Layout design is best learned by adjusting spacing, scale, alignment, and contrast, then seeing the visual consequence immediately.

Design directions:
1. Modern Studio Desk
2. Swiss Grid Lab
3. Editorial Layout Board
```

### User Response

```text
Use Swiss Grid Lab and keep Parameter Lab.
```

### Skill Output

The skill generates:

```text
graphic-design-layout-study-tool/
├── index.html
├── style.css
├── data.js
├── app.js
├── vercel.json
└── README.md
```

---

## Deployment

Generated projects are designed for Vercel.

### Option 1: Drag-and-Drop Deploy

1. Generate the project files.
2. Put all files in one folder.
3. Go to Vercel.
4. Drag the folder into the Vercel dashboard.
5. Deploy.

### Option 2: CLI Deploy

Install the Vercel CLI:

```bash
npm i -g vercel
```

From the generated project folder, run:

```bash
vercel
```

For production:

```bash
vercel --prod
```

---

## GitHub Pages Note

The generated project is a static site, so it can also be hosted on GitHub Pages.

However, the included `vercel.json` is only used by Vercel. GitHub Pages will ignore it.

---

## Extending the Skill

### Add a New Discipline Using an Existing Model

No file changes are required.

Use the closest existing Interaction Model based on the learner action.

Example:

| New Discipline | Likely Model |
|---|---|
| Economics | Scenario Branch or Parameter Lab |
| Color theory | Parameter Lab |
| Microbiology | Diagnostic Explorer |
| Cybersecurity commands | Command Sim |

---

### Add a New Discipline Mapping

To create an explicit mapping, add a row to the Mode Name / Interaction Model table in `SKILL.md`.

Example:

```markdown
- Economics → Market Simulator → Parameter Lab
```

---

### Rename a Mode Name

Mode names are presentation labels.

Renaming a mode does not change the underlying interaction logic.

Example:

```markdown
Graphic Design → Layout Deck → Parameter Lab
```

Could become:

```markdown
Graphic Design → Composition Lab → Parameter Lab
```

The model remains `Parameter Lab`.

---

### Add a New Interaction Model

Only add a new model if none of the existing five models fit.

A new model should define:

1. Input mechanic
2. Output surface
3. Required `data.js` field
4. Minimum content requirements
5. Required `app.js` functions
6. Example entries
7. Disciplines where the model should be used

---

## Version History

### v3.0

Added the Interaction Model branching system:

- Command Sim
- Parameter Lab
- Diagnostic Explorer
- Scenario Branch
- Ear Trainer

The Interactive panel no longer defaults to a terminal for non-CLI subjects.

### v2.0

Original CompTIA-derived specification:

- Fixed three-panel layout
- Terminal-only interactive panel
- Theme library
- Terminology adaptation table

---

## Important Notes

- The generated site should be complete in one pass.
- Do not generate placeholders.
- Do not leave TODO comments.
- Do not include inline CSS or JavaScript in `index.html`.
- Keep content in `data.js`.
- Keep UI behavior in `app.js`.
- Keep all CSS color values under `:root`.
- Confirm the Interaction Model before generating code.
- Use Q&A-style drill content that reinforces the Reference and Interactive panels.

---

## License

Choose a license that matches your use case.

Common options:

- MIT License for open educational reuse
- GPL if derivative tools should remain open
- Private/internal license for institutional use only