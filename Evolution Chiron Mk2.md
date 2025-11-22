# 🔥 Chiron Mk2 — Database Integration

## Chiron Evolution - Long Term Storage
Key elements:
- The adoption of a database engine to support the PRIMAL Datamodel coming from Palas Framework.
- It must handle existing and new entities, evolve over time, and support regeneration of documents using the Master Prompts and Foundation Schemas.

The exploration goes towards:
- A layered guidance system
- Diagram generation engine for conceptual architecture
- Exporting all analysis output into a structured report (canvas-supported)
- Using MongoDB, for PRIMAL Datamodel storage and a structured repository for prompts, schemas, and derived documents
- ChatGPT API integration

Chiron Mk2 became the meta-architecture for document generation + requirement analysis + schema evolution.
Chiron Mk2 will evolve as the backbone for future project automation

---

## ✅ What the PRIMAL Datamodel refers to in the long-term context
### ✅ Future AI-driven code generation
1. **Persistent Core Model**
A centralized definition of all entities (relationships, behaviors, and attributes), Master Prompt and Foundation Schema architecture. The PRIMAL datamodel is the foundational conceptual model used to:
- Handle existing entities or those entities derived from RAW input analysis
- Support deep requirement analysis
- Track both existing and new entities across evolving projects
- Serve as the single source of truth for:
  - Master Prompts
  - Foundation Schemas
  - Document regeneration
  - Cross-project consistency

This is the “primal” layer because all other schemas derive from it. The usage of MongoDB (expansion stage) as long term repository enables:
- Storage of Metadata
- Traceability to prompts
- Versioning

---

2. **Integration with ChatGPT API**
A core future objective:
- ChatGPT API acts as the derivation engine
- PRIMAL specifies all rules
- Master Prompts + Foundation Schemas are generated, validated, refined through API interactions

Project regeneration becomes automatic and reproducible

## ✅ Relationship to Chiron

The PRIMAL datamodel is, in fact, one of the two inputs for Chiron Mk2 meta-engine, so that:
- PRIMAL = The datamodel that exists at the begining of the analysys or the datamodel resulting after the analysis.
- Chiron = orchestration, diagrams, and document generation

Think of PRIMAL as the ontology, and Chiron as the processor + UI.
