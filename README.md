# Meta Framework V3 — Structure Wizard

Generates complete Meta Framework Model project structures with 7 semantic layers, delivery sections, and bidirectional layer linkage. Output is a Claude Code prompt.

## What's inside

| File | Description |
|------|-------------|
| `struktura-wizard.html` | Browser-based wizard — fill in steps or import a template |

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

```
<ProjectName>/                          (Knowledge Layer)
├── 00_PROJECT_CONTROL/
│   ├── 01_BUSINESS/BUSINESS.md
│   ├── 02_KNOWLEDGE/
│   ├── 03_ARCHITECTURE/ADR/
│   ├── 04_ENGINEERING/
│   ├── 05_PLAN/PLAN.md
│   ├── 06_DATA/DATA.md
│   ├── 07_RESOURCE/prompty/
│   │               RESOURCE.md
│   └── 08_DEV/ExecutionLayer.lnk  -->  Execution Layer
├── 10_DELIVERY/                        (Standard+)
│   ├── 11_MEETINGS/
│   ├── 12_WORK_ITEMS/01-05/
│   ├── 13_MIGRATION/01-07/            (Full only)
│   ├── 14_INTEGRATION/01-04/          (Full only)
│   ├── 15_TESTING/01-06/              (Full only)
│   ├── 16_RELEASE_TRANSPORT/          (Full only)
│   └── 17_OPERATIONS/                 (Full only)
├── 20_SHARED_REFERENCE/                (Standard+)
│   ├── 21_TEMPLATES/
│   ├── 22_STANDARDS/TAGS.md
│   └── 23_NAMING_CONVENTIONS/README.md
├── 99_ARCHIVE/
├── CHANGELOG.md
├── EXECUTION_SNAPSHOT.md
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
