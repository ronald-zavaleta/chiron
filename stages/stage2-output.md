## 1. What You Just Specified (in my own words) <!-- [SEC-1] -->

You basically described the logical and physical model of an **Outside Plant (OSP) fiber-optic infrastructure**, where both **active and passive network elements** coexist inside a multi-level spatial hierarchy inherited from the AppManager model.

### Conceptually
- The system models everything from a **site** to the smallest fiber **strand**.  
- **ODFs (Optical Distribution Frames)** are treated as **passive network elements**, structurally equivalent to active network elements (NEs). Both have **chassis / shelves**, **slots / trays**, and **ports**.  
- The distinction lies in **power dependency** – active NEs require power, ODFs do not.  
- **Physical connectivity** occurs through **patching events** and **splicing events**:  
  - *Patching Event* → connects two terminated cables (connector ↔ connector).  
  - *Splice Event* → fuses two fibers permanently (strand ↔ strand or strand ↔ pigtail).  
- The **FOLink** abstracts the physical fiber connection between two ODFs (A ↔ B) through the external plant (path, segments, infrastructure).  

### Functionally
- A fiber link starts at a port on an active NE (A), passes through ODF A (via patching), traverses the external plant via a FOLink composed of segments and paths, reaches ODF B (via patching again), and terminates on an active NE (B).  
- The external plant is built from **paths**, **segments**, and **spatial structures** (trenches, manholes, poles, levels).  
- The model distinguishes between **connection** (cable → port) and **patching** (cable → cable).  
- **Span** represents the distance between two sites (A ↔ B); **Path** represents the trace of the fiber along that span; **Segment** represents a single line between two structures (manhole–pole–pole).  

### Structurally
- **Site → Structure → Level → Substructure → Container → ODF.**  
- ODFs can reside in rooms or manholes depending on context.  
- **Manhole + Container + ODF** represents a trench implementation; **Mufa** (closure) is the equivalent for aerial implementation.  
- **Equivalences:**  
  - *Trench ↔ Subtrench ↔ Duct ↔ Subduct*  
  - *Aerial ↔ Pole ↔ Level ↔ Invisible Trench*  

### Terminology Recap
| Term | Meaning |
|------|----------|
| Patch Event | Connector-to-connector union (mutable) |
| Splice Event | Strand-to-strand fusion (permanent) |
| FOLink | Abstraction of the whole optical path between ODFs A & B |
| Span | Physical distance between sites |
| Path | Fiber trace along infrastructure |
| Segment | Line between structures |
| Level / Subtrench | Equivalent vertical sub-division |
| Mufa | Compact ODF inside a pole (aerial case) |
| Manhole | Chamber hosting ODF for trench case |

---

### 1.1 Visually <!-- [SEC-1.1] -->

- The system depicts a **spatially nested topology** linking sites and infrastructure elements in 3D or map view.  
- **Sites** are anchor points with geographic coordinates.  
- Each site contains **structures** (buildings, manholes, poles, ghost structures).  
- Structures are divided into **levels** (vertical or elevation planes).  
- **Substructures** (rooms, vaults, chambers) exist within levels.  
- **Containers** (racks, cabinets, mufas) host the functional components such as ODFs.  
- Inside each ODF: **chassis / shelves → trays → ports**.  
- **Ports** connect to cables and pigtails.  
- **Cables** follow **paths**, which are polyline-like routes on the map, formed by segments.  
- **Segments** appear as straight or slightly curved lines between structures (manhole ↔ pole).  
- **Trenches** and **subtrenches** can be visualized as nested horizontal channels; **poles and levels** as vertical stacks.  
- **Splice events** and **patch events** could be represented as icons or markers along the path.  
- **Manhole and Mufa equivalence:**  
  - Manhole → underground container with ODF and fusion trays.  
  - Mufa → aerial version attached to a pole level.  
- Visually, the entire model resembles a hierarchical network map linking physical spaces to fiber connections.

---

### 1.2 Main objects / entities <!-- [SEC-1.2] -->

| Entity | Definition | Purpose / Role | Key Attributes |
|--------|-------------|----------------|----------------|
| **Site** | Geospatial anchor for all infrastructure. | Houses structures and elements at a location. | id, name, coords(lat, lon), type(main/ghost) |
| **Structure** | Physical building / pole / manhole within a site. | Contains levels and substructures. | id, siteId, type(building, pole, manhole, ghost) |
| **Level** | Vertical partition of a structure. | Organizes substructures by height or depth. | id, structureId, index, elevation |
| **Substructure** | Localized space within a level (room, chamber). | Hosts containers and ODFs. | id, levelId, type(room, vault, chamber, pole-holder) |
| **Container** | Rack, cabinet, or mufa that houses ODFs. | Provides mounting and support. | id, substructureId, type(rack, cabinet, mufa) |
| **ODF (Optical Distribution Frame)** | Passive network element equivalent to active NE. | Hosts trays and ports for fiber termination. | id, containerId, type(reflex, splice reflex, splice), slots, trays, ports |
| **Network Element (Active)** | Powered equipment (router, switch). | Interfaces to ODF via ports. | id, containerId, powerStatus, ports |
| **Port** | Connection point for fiber or patch cord. | Enables link between components. | id, odfId or neId, direction(client/line), status |
| **Cable** | Physical fiber bundle connecting ports or ODFs. | Carries fiber strands along paths. | id, fromPort, toPort, type(single-mode, multi-mode), fiberCount |
| **Fiber Strand** | Individual fiber within a cable. | Atomic connectivity unit. | id, cableId, strandNo, status, terminated(pigtail?) |
| **Pigtail** | Short fiber terminated with connector. | Used to terminate fiber strands in ODF. | id, connectorType, strandId |
| **Patch Event** | Connection between two terminated fibers. | Mutable connection event. | id, fromPort, toPort, timestamp, status |
| **Splice Event** | Fusion between two fiber strands. | Permanent connection event. | id, strandA, strandB, locationId |
| **FOLink (Physical Fiber Link)** | Abstraction of connection between two ODFs. | Represents end-to-end path. | id, fromODF, toODF, pathId |
| **Span** | Physical distance between sites A and B. | High-level envelope for paths. | id, siteA, siteB, length |
| **Path** | Trace of fiber route over infrastructure. | Defines the route A ↔ B via segments. | id, spanId, segments[], infraType(trench/pole/mixed) |
| **Segment** | Line between two structures. | Basic element of path. | id, fromStructure, toStructure, type(trench/aerial), levels[], cables[] |
| **Section** | Link between two substructures. | Subdivision within segment. | id, fromSubstructure, toSubstructure |
| **Trench / Subtrench / Duct / Subduct** | Infrastructure channels for cables. | Define nested containment for OSP. | id, parentId, depth, capacity |
| **Pole / Level** | Aerial support structure and its vertical positions. | Equivalent to trench + subtrench hierarchy. | id, siteId, height, levelNo |
| **Mufa** | Compact enclosure for aerial splice. | Hosts ODF and trays on poles. | id, poleId, levelId, odfId |

---

### 1.3 Relationships / hierarchy <!-- [SEC-1.3] -->

#### Structural Containment <!-- [REL-STRUCT] -->

Site  
 └── Structure (Building / Manhole / Pole / Ghost)  
   ├── Level  
   │  └── Substructure (Room / Chamber / Pole-Holder)  
   │    └── Container (Rack / Cabinet / Mufa)  
   │      └── ODF (Passive Network Element)  
   │        └── Trays → Ports  
 └── Network Element (Active)

#### Physical Connectivity <!-- [REL-CONNECT] -->

Active NE A → Port → ODF A → Patch Event → FOLink → Patch Event → ODF B → Port → Active NE B

#### Infrastructure Linkage <!-- [REL-INFRA] -->

Span (A ↔ B)  
 └── Path (Trace between Sites)  
   └── Segment (Line between Structures)  
     ├── Section (Between Substructures)  
     ├── Infrastructure Type → Trench / Aerial / Mixed  
     └── Containment → Trench > Subtrench > Duct > Subduct

#### Equivalence Mappings <!-- [REL-EQUIV] -->

| Domain A | Domain B | Relationship |
|-----------|-----------|--------------|
| Trench | Invisible Trench (Aerial Span) | Functional equivalent |
| Subtrench | Level (Pole Structure) | Equivalent depth dimension |
| Manhole | Mufa | Containment equivalent |
| ODF in Manhole | ODF in Mufa | Functional equivalent |
| Splice Event | Patch Event | Permanent ↔ Mutable operations |

#### Connection Rules <!-- [REL-RULES] -->

1. **ODF ↔ ODF** → via FOLink (abstracted path through OSP).  
2. **FOLink** = { Path + Segments + Infrastructure + Splice / Patch Events }.  
3. **Path** = collection of Segments; **Segment** = line between Structures.  
4. **Section** = link between Substructures (Mufa ↔ Chamber).  
5. **Manhole contains Container contains ODF**; equivalent for Aerial via Mufa.  
6. **Poles have Levels; Levels may host Mufas or cables.**  
7. **Cable hierarchy:** Cable → Strand → Pigtail → Port.

---

### 1.4 Behavior & interactions <!-- [SEC-1.4] -->

> Not required yet.  
> (RAW Requirements Text does not define explicit UI interaction behaviors for this domain at this stage.)

#### 1.4.1 Generic (Applies to all Level Views) <!-- [BEH-GEN] -->

Not required yet.

#### 1.4.2 Macro Level View (inside Main UI) <!-- [BEH-MACRO] -->

Not required yet.

#### 1.4.3 Micro Level View – OSP Detail pop-ups <!-- [BEH-MICRO-OSP] -->

Not required yet.

---

### 1.5 Data & Settings <!-- [SEC-1.5] -->

High-level description of data models and configuration settings has not been specified in the current RAW Requirements Text.  
This section is reserved for future description of:

- Core data domains (sites, structures, ODFs, cables, paths, events).  
- Configurable parameters (naming conventions, capacity thresholds, visualization preferences).  

#### 1.5.1 Data <!-- [DATA] -->

Not required yet.

#### 1.5.2 Settings <!-- [SETTINGS] -->

Not required yet.

---

### 1.6 Functionally <!-- [SEC-1.6] -->

Cross-entity processes and functional workflows (e.g., end-to-end provisioning, rerouting, impact analysis) are not explicitly defined in the current RAW Requirements Text.  

This section is reserved for:

- Sequenced workflows combining ODFs, cables, FOLinks, paths, and events.  
- System-level behaviors such as validation, conflict detection, and consistency checks.

For now:

> Not required yet.

---

## 2. Internal Architecture Plan (independent of framework) <!-- [SEC-2] -->

### 2.1 Data Shapes (Conceptual JSON per Entity) <!-- [DATA-SHAPES] -->

This section will define canonical JSON-like structures for the main entities introduced in **1.2 Main objects / entities**.  
At this stage, only the entity list and relationships are defined; detailed data shapes will be filled in later.

> For now, all subsections are structural placeholders.

#### 2.1.1 Sites <!-- [DATA-SITE] -->

Not required yet.

#### 2.1.2 Structures & Levels <!-- [DATA-STRUCT] -->

Not required yet.

#### 2.1.3 Substructures & Containers <!-- [DATA-SUBSTRUCT] -->

Not required yet.

#### 2.1.4 ODFs & Network Elements <!-- [DATA-ODF-NE] -->

Not required yet.

#### 2.1.5 Cables & Fiber Strands <!-- [DATA-CABLE] -->

Not required yet.

#### 2.1.6 Spans, Paths, Segments & Sections <!-- [DATA-PATH] -->

Not required yet.

#### 2.1.7 Events (Patch, Splice, FOLink) <!-- [DATA-EVENT] -->

Not required yet.

---

### 2.2 Mapping Logic / Core algorithms <!-- [SEC-2.2] -->

The RAW Requirements Text conceptually distinguishes between:

- **Span / Path / Segment / Section** levels.  
- **Trench vs. Aerial** infrastructure.  
- **Splice vs. Patch** events.  

However, it does not yet define explicit computational or geometric algorithms.

The following subsections are reserved for future formalization of those mappings.

#### 2.2.1 Topology mapping for Span / Path / Segment / Section <!-- [ALG-TOPO] -->

Not required yet.

#### 2.2.2 ODF / Port / Event resolution algorithms <!-- [ALG-PORT] -->

Not required yet.

#### 2.2.3 Capacity & Level allocation rules <!-- [ALG-CAPACITY] -->

Not required yet.

---

## 3. Interaction & UI Plan <!-- [SEC-3] -->

The RAW Requirements Text focuses on conceptual and physical modeling of OSP and does not yet describe UI components or interaction flows.  
This section defines the structural placeholders for a future UI specification.

### 3.1 Render View / Main View <!-- [UI-MAIN] -->

Not required yet.

### 3.2 Settings / Configuration Tab <!-- [UI-SETTINGS] -->

Not required yet.

---

### 3.3 Popups / Detail Panels <!-- [UI-POPUPS] -->

The following popup types are anticipated but not yet formally defined in the RAW Requirements Text:

#### 3.3.1 ODF Detail pop-up <!-- [POP-ODF] -->

Not required yet.

#### 3.3.2 Path / FOLink Detail pop-up <!-- [POP-FOLINK] -->

Not required yet.

#### 3.3.3 Segment / Infrastructure Detail pop-up <!-- [POP-SEGMENT] -->

Not required yet.

### 3.4 Highlighting & Feedback <!-- [UI-HIGHLIGHT] -->

Visual feedback behaviors (hover/selection, error states, capacity warnings) are not specified in the RAW Requirements Text.

> Not required yet.

---

## 4. Proposed Battle Roadmap (step-by-step) <!-- [SEC-4] -->

Roadmap phases are not explicitly defined in the RAW Requirements Text.  
The following phases are suggested placeholders aligned with the OSP modeling context:

#### Phase 1 – Basic OSP Entity Model <!-- [PHASE-1] -->

Not required yet.

#### Phase 2 – Path / Segment / Section Modeling <!-- [PHASE-2] -->

Not required yet.

#### Phase 3 – Event Modeling (Patch / Splice / FOLink) <!-- [PHASE-3] -->

Not required yet.

#### Phase 4 – Data Shapes & Persistence <!-- [PHASE-4] -->

Not required yet.

#### Phase 5 – UI & Visualization Layer <!-- [PHASE-5] -->

Not required yet.

#### Phase 6 – Validation, QA & Optimization <!-- [PHASE-6] -->

Not required yet.

---

## Annex-1. [Title] <!-- [ANN-1] -->

This annex is reserved for out-of-structure or deferred requirements that do not yet fit into the main sections.

Not required yet.

---

## Annex-A. Tag Map Table <!-- [ANN-A] -->

> Stage-2 draft: minimal Tag Map capturing the primary anchors defined so far.  
> This table can be extended as more subsections and anchors are populated in STAGE-3.

| Tag ID          | Section Title                        | Purpose / Description                                  | Merge Category   |
|-----------------|--------------------------------------|--------------------------------------------------------|------------------|
| [SEC-1]         | What You Just Specified              | High-level narrative of OSP model                      | Introductory     |
| [SEC-1.1]       | Visually                             | Visual / geometric description of OSP topology         | Visual           |
| [SEC-1.2]       | Main objects / entities              | Canonical list of entities                             | Structural       |
| [SEC-1.3]       | Relationships / hierarchy            | Containment and connectivity hierarchy                 | Structural       |
| [REL-STRUCT]    | Structural Containment               | Site → Structure → Level → Substructure → Container   | Structural       |
| [REL-CONNECT]   | Physical Connectivity                | Active NE ↔ ODF ↔ FOLink chain                         | Connectivity     |
| [REL-INFRA]     | Infrastructure Linkage               | Span / Path / Segment / Section relationships          | Structural       |
| [REL-EQUIV]     | Equivalence Mappings                 | Trench ↔ Aerial, Manhole ↔ Mufa mappings               | Conceptual       |
| [REL-RULES]     | Connection Rules                     | Rules governing FOLink construction                    | Behavioral       |
| [SEC-1.4]       | Behavior & interactions              | Placeholder for global and view-level behaviors        | Behavioral       |
| [SEC-1.5]       | Data & Settings                      | Placeholder for data and configuration description     | Data             |
| [SEC-1.6]       | Functionally                         | Placeholder for cross-entity functional flows          | Functional       |
| [SEC-2]         | Internal Architecture Plan           | High-level data and algorithm architecture             | Architectural    |
| [DATA-SHAPES]   | Data Shapes                          | Placeholder for conceptual JSON per entity             | Data             |
| [SEC-2.2]       | Mapping Logic / Core algorithms      | Placeholder for computational logic                     | Algorithmic      |
| [SEC-3]         | Interaction & UI Plan                | Placeholder for UI interactions                        | UI               |
| [UI-MAIN]       | Render View / Main View              | Placeholder for main visualization behaviors           | UI               |
| [UI-SETTINGS]   | Settings / Configuration Tab         | Placeholder for configuration interactions             | UI               |
| [UI-POPUPS]     | Popups / Detail Panels               | Placeholder for detailed views                         | UI               |
| [UI-HIGHLIGHT]  | Highlighting & Feedback              | Placeholder for visual feedback rules                  | UI               |
| [SEC-4]         | Proposed Battle Roadmap              | Placeholder for phased implementation plan             | Planning         |
| [ANN-1]         | Annex-1                              | Placeholder for extra / deferred requirements          | Annex            |
| [ANN-A]         | Annex-A Tag Map Table                | This table – anchor registry                           | Meta             |

