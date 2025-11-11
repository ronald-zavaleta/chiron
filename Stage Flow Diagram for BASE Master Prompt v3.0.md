## Compact Visual Stage Flow Diagram

### 🧭 Horizontal Flow (Markdown Diagram)

```markdown
RAW Requirements Text
        ⬇️
┌────────────────────────┐
│  STAGE‑0  │ Layered Extraction & Section Population │
│  - Parse RAW text layer‑by‑layer                    │
│  - Populate Section 1 structure (1.1–1.6)          │
└────────────────────────┘
        ⬇️
┌────────────────────────┐
│  STAGE‑1  │ Interactive Review of Section 1         │
│  - Present subsections as chunks                   │
│  - User approves/edits each                        │
│  - Section 1 validated + locked                    │
└────────────────────────┘
        ⬇️
┌────────────────────────┐
│  STAGE‑2  │ Schema Expansion & Validation           │
│  - Enumerate subsections & anchors                 │
│  - Insert placeholders for missing content         │
│  - Cross‑verify entities/relationships             │
└────────────────────────┘
        ⬇️
┌────────────────────────┐
│  STAGE‑3  │ Content Population & Completion         │
│  - Populate enumerated schema with content         │
│  - Inject data, logic, UI, and behaviors           │
│  - Validate cross‑references + Tag Map entries     │
└────────────────────────┘
        ⬇️
┌────────────────────────┐
│  STAGE‑n  │ Finalization & Meta‑Assembly            │
│  - Add anchors, Change Log, Annex‑A                │
│  - Validate structure + metadata                   │
│  - Output publication‑ready document               │
└────────────────────────┘
        ⬇️
✅ FINAL OUTPUT → Complete Deep Requirements Analysis Document
```

---

### 🧱 Vertical Annotated Flow (Process with Roles & Checkpoints)

```plaintext
┌──────────────────────────────────────────────────────────────────┐
│ INPUT: RAW Requirements Text                                     │
│ ROLE: Analyst / Engineer                                         │
│ ACTION: Submit initial freeform system or feature description    │
└──────────────────────────────────────────────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────────────────────────────┐
│ STAGE‑0 — Layered Extraction & Section Population                │
│ ROLE: Sage (Analyst AI)                                          │
│ ACTION: Parse RAW → Populate Section 1 with all [NOTE.] blocks   │
│ OUTPUT: Draft Section 1 (1.1–1.6) ready for review               │
└──────────────────────────────────────────────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────────────────────────────┐
│ STAGE‑1 — Interactive Review of Section 1                        │
│ ROLE: User + Sage (Collaborative Editing)                        │
│ ACTION: Approve, edit, or refine Section 1 chunks                │
│ OUTPUT: Locked Section 1 baseline (entities, relationships, etc.)│
└──────────────────────────────────────────────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────────────────────────────┐
│ STAGE‑2 — Schema Expansion & Validation                          │
│ ROLE: Sage (Automated Structuring)                               │
│ ACTION: Enumerate all subsections/sub‑subsections, anchors       │
│ OUTPUT: Full enumerated schema skeleton (with placeholders)      │
└──────────────────────────────────────────────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────────────────────────────┐
│ STAGE‑3 — Content Population & Completion                        │
│ ROLE: Sage (Content Architect)                                   │
│ ACTION: Populate schema using validated data + behaviors          │
│ OUTPUT: Fully populated Deep Requirements Analysis Document       │
└──────────────────────────────────────────────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────────────────────────────┐
│ STAGE‑n — Finalization & Meta‑Assembly                           │
│ ROLE: Sage (Integrator / Publisher)                              │
│ ACTION: Add anchors, Change Log, Annex‑A, metadata, validations  │
│ OUTPUT: Publication‑ready Markdown file                          │
└──────────────────────────────────────────────────────────────────┘
               │
               ▼
✅ FINAL STATE — Stable Deep Requirements Analysis Document
   (Traceable • Anchored • Validated • Publishable)
```
