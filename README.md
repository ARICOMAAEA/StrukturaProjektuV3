# Meta Framework V3 — Structure Wizard

Generates complete Meta Framework Model project structures with 7 semantic layers, delivery sections, and bidirectional layer linkage. Output is a Claude Code prompt.

## What's inside

| File | Description |
|------|-------------|
| `struktura-wizard.html` | Browser-based wizard — fill in steps or import a template |
| `diagrams/architecture-overview.html` | One-page visual overview of the whole tool — input, engine, output, two-layer structure, automation, lifecycle |

## Architecture diagram

For a one-page visual explanation of how the wizard, generated structure, automation (skills/agents/hooks), and lifecycle rules fit together, open:

```
diagrams/architecture-overview.html
```

It is a single self-contained HTML file (dark theme, inline SVG, no build step). Open it directly in a browser via `file://`. Use it for onboarding new users, presentations, or as a refresher before working with the framework.

## Requirements

- **Browser** (for HTML wizard)
- **Claude Code** (for executing the generated prompt)

## Usage

1. Open `struktura-wizard.html` in a browser
2. Choose workflow:
   - **Quick import:** Download blank template ("Stahnout sablonu"), fill it in an editor, drag & drop back
   - **Step by step:** Fill the 10-step wizard directly
3. On the output step, copy the **Claude Code Prompt** and paste it into Claude Code

## Generated structure

> Every structural folder also gets a **folder-description `README.md`** (Účel / Co sem patří / Co sem nepatří / Kdo smí měnit) following the KOFOLA pattern — see `README.md` markers below.

```
<ProjectName>/                          (Knowledge Layer)
├── 00_PROJECT_CONTROL/README.md
│   ├── 01_BUSINESS/BUSINESS.md + README.md
│   ├── 02_KNOWLEDGE/README.md
│   ├── 03_ARCHITECTURE/ADR/ + README.md
│   ├── 04_ENGINEERING/README.md
│   ├── 05_PLAN/PLAN.md + README.md
│   ├── 06_DATA/DATA.md + README.md
│   ├── 07_RESOURCE/prompty/
│   │               RESOURCE.md + README.md
│   └── 08_DEV/ExecutionLayer.lnk + README.md  -->  Execution Layer
├── 10_DELIVERY/README.md               (Standard+)
│   ├── 11_MEETINGS/README.md
│   ├── 12_WORK_ITEMS/01-05/ + README.md
│   ├── 13_MIGRATION/01-07/            (Full only)
│   ├── 14_INTEGRATION/01-04/          (Full only)
│   ├── 15_TESTING/01-06/              (Full only)
│   ├── 16_RELEASE_TRANSPORT/          (Full only)
│   └── 17_OPERATIONS/                 (Full only)
├── 20_SHARED_REFERENCE/README.md       (Standard+)
│   ├── 21_TEMPLATES/README.md
│   ├── 22_STANDARDS/TAGS.md + README.md
│   └── 23_NAMING_CONVENTIONS/README.md
├── 99_ARCHIVE/
├── GLOSSARY.md                         (Standard+)
├── ID_REGISTRY.md                      (Standard+)
├── PROJECT_HISTORY.md
├── PROJECT_STATUS.md
├── README.md
├── STALE.md                            (Standard+)
├── TOPIC_MAP.md                        (Standard+)
├── Todo.md
└── souhrnGPT.md

<ProjectName>/                          (Execution Layer)
├── .claude/skills/
├── apps/
└── CONTEXT  -->  Knowledge Layer       (NTFS junction)
```

## Delivery presets

| Preset | Sections |
|--------|----------|
| **Minimal** | Core layers (01-07) + 99_ARCHIVE only |
| **Standard** | + 11_MEETINGS, 12_WORK_ITEMS, 20_SHARED_REFERENCE, Discovery Layer |
| **Full** | + 13_MIGRATION, 14_INTEGRATION, 15_TESTING, 16_RELEASE_TRANSPORT, 17_OPERATIONS |

## Discovery layer (Standard+)

Generated automatically for non-Minimal presets. Provides metadata and indexes for faster project navigation:

| File | Purpose |
|------|---------|
| `ID_REGISTRY.md` | Lookup table for all project IDs (BR, SP, FS, TS, DEV, CR, TC) |
| `TOPIC_MAP.md` | Cross-cutting topics with canonical sources |
| `GLOSSARY.md` | Terms, abbreviations, custom objects, roles |
| `STALE.md` | Tracking dead links in indexes |
| `22_STANDARDS/TAGS.md` | Controlled vocabulary for frontmatter tags |
| `23_NAMING_CONVENTIONS/README.md` | File and folder naming patterns |

Also adds **Search protocol** and **Don't-read list** sections to CLAUDE.md.

## Recent updates

- **2026-06-16** — Folder-description READMEs (v1.8.0): the wizard now generates a folder-description `README.md` (Účel / Co sem patří / Co sem nepatří / Kdo smí měnit) for **every structural folder** — `00_PROJECT_CONTROL` + layers `01_BUSINESS`–`08_DEV`, `10_DELIVERY` + `11_MEETINGS`/`12_WORK_ITEMS`, `20_SHARED_REFERENCE` + `21_TEMPLATES`/`22_STANDARDS`. Mirrors the KOFOLA Časová okna pattern. Implemented in all three outputs: PowerShell init script (`Write-FolderReadme` helper + content), Claude Code prompt (folder-description directive + template), and tree preview. Generated READMEs carry the mandatory YAML origin header.
- **2026-05-03** — Wizard A-patch (v1.7.0): `struktura-wizard.html` now generates everything back-ported in v1.6.x. New checkboxes in Step 4 (Engineering: `zvl_knowledge-builder`, `zvl_new-meeting`, `zvl_meeting-from-transcript`, `session-guard.ps1`) and Step 8 (Delivery: 4 new templates, 2 SAP standards, 2 governance META files). Tree preview + Claude Code prompt + PowerShell init script all updated. Wizard grew 111 KB → 118 KB.
- **2026-05-03** — Generalization pass (v1.6.2): rewrote 11 root governance META files (`README.md`, `START_HERE.md`, `STALE.md`, `souhrnGPT.md`, `TOPIC_MAP.md`, `ID_REGISTRY.md`, `DIAGRAMS_INDEX.md`, `GLOSSARY.md`, `ContextQuick.md`, plus the two sub-folder ContextQuicks) into project-agnostic schemas with `{{PLACEHOLDER}}` slots. KOFOLA-content quarantine (`_NEEDS_GENERALIZATION_FROM_KOFOLA/`) deleted. Knowledge layer is now fully template-clean — zero customer references in any of the 15 root .md files.
- **2026-05-03** — Logic-only back-port from WIKOV (v1.6.1): added skill `zvl_meeting-from-transcript`, templates `meetings-overview-template.md` + `br-all-template.md`, and layer schema `10_DELIVERY/11_MEETINGS/README.md`. The skill propagates `(BR)`-flagged points from meeting transcripts into `BR-ALL.md` and keeps `MEETINGS_OVERVIEW.md` in sync (`PENDING/REVIEWED` workflow). Wizard checkboxes still pending.
- **2026-05-01** — Added `diagrams/architecture-overview.html` — single-page visual overview (6 zones: Input / Engine / Output / Generated structure / Automation / Lifecycle). Generated via the `architecture-diagram` skill.
- **2026-05-01** — Template back-port v1.6.0: imported 5 skills, 4 agents, 1 hook, 7 delivery templates, 5 standards, 9 layer-schema READMEs from KOFOLA. 12 governance META files quarantined in `_NEEDS_GENERALIZATION_FROM_KOFOLA/` for manual generalization. Wizard checkboxes pending.
