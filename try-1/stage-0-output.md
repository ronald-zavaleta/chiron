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

## 1.1 Visually

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

## 1.2 Main Objects / Entities

| Entity | Definition | Purpose / Role | Key Attributes |
|--------|-------------|----------------|----------------|
| **Site** | Geospatial anchor for all infrastructure. | Houses structures and elements at a location. | id, name, coords(lat, lon), type(main/ghost) |
| **Structure** | Physical building / pole / manhole within a site. | Contains levels and substructures. | id, siteId, type(building, pole, manhole, ghost) |
| **Level** | Vertical partition of a structure. | Organizes substructures by height or depth. | id, structureId, index, elevation |
| **Substructure** | Localized space within a level (room, chamber). | Hosts containers and ODFs. | id, levelId, type(room, vault, chamber, pole-holder) |
| **Container** | Rack, cabinet, or mufa that houses ODFs. | Provides mounting and support. | id, substructureId, type(rack, cabinet, mufa) |
| **ODF (Optical Distribution Frame)** | Passive network element equivalent to active NE. | Hosts trays and ports for fiber termination. | id, containerId, type(reflex, splice reflex, splice), slots, trays, ports |
| **Network Element (Active)** | Powered equipment (router, switch). | Interfaces to ODF via ports. | id, containerId, powerStatus, ports |
| **Port** | Connection point for fiber or patch cord. | Enables link between components. | id, odfId, direction(client/line), status |
| **Cable** | Physical fiber bundle connecting ports or ODFs. | Carries fiber strands along paths. | id, fromPort, toPort, type(single-mode, multi-mode), fiberCount |
| **Fiber Strand** | Individual fiber within a cable. | Atomic connectivity unit. | id, cableId, strandNo, status, terminated(pigtail?) |
| **Pigtail** | Short fiber terminated with connector. | Used to terminate fiber strands in ODF. | id, connectorType, strandId |
| **Patch Event** | Connection between two terminated fibers. | Mutable connection event. | id, fromPort, toPort, timestamp, status |
| **Splice Event** | Fusion between two fiber strands. | Permanent connection event. | id, strandA, strandB, locationId |
| **FOLink (Physical Fiber Link)** | Abstraction of connection between two ODFs. | Represents end-to-end path. | id, fromODF, toODF, pathId |
| **Path** | Trace of fiber route over infrastructure. | Defines the route A ↔ B via segments. | id, spanId, segments[], infraType(trench/pole/mixed) |
| **Segment** | Line between two structures. | Basic element of path. | id, fromStructure, toStructure, type(trench/aerial), levels[], cables[] |
| **Section** | Link between two substructures. | Subdivision within segment. | id, fromSubstructure, toSubstructure |
| **Span** | Physical distance between sites A and B. | High-level envelope for paths. | id, siteA, siteB, length |
| **Trench / Subtrench / Duct / Subduct** | Infrastructure channels for cables. | Define nested containment for OSP. | id, parentId, depth, capacity |
| **Pole / Level** | Aerial support structure and its vertical positions. | Equivalent to trench + subtrench hierarchy. | id, siteId, height, levelNo |
| **Mufa** | Compact enclosure for aerial splice. | Hosts ODF and trays on poles. | id, poleId, levelId, odfId |

---

## 1.3 Relationships / Hierarchy

### Structural Containment
Site  
 └── Structure (Building / Manhole / Pole / Ghost)  
   ├── Level  
   │  └── Substructure (Room / Chamber / Pole-Holder)  
   │    └── Container (Rack / Cabinet / Mufa)  
   │      └── ODF (Passive Network Element)  
   │        └── Trays → Ports  
 └── Network Element (Active)

### Physical Connectivity
Active NE A → Port → ODF A → Patch Event → FOLink → Patch Event → ODF B → Port → Active NE B

### Infrastructure Linkage
Span (A ↔ B)  
 └── Path (Trace between Sites)  
   └── Segment (Line between Structures)  
     ├── Section (Between Substructures)  
     ├── Infrastructure Type → Trench / Aerial / Mixed  
     └── Containment → Trench > Subtrench > Duct > Subduct

### Equivalence Mappings
| Domain A | Domain B | Relationship |
|-----------|-----------|--------------|
| Trench | Invisible Trench (Aerial Span) | Functional equivalent |
| Subtrench | Level (Pole Structure) | Equivalent depth dimension |
| Manhole | Mufa | Containment equivalent |
| ODF in Manhole | ODF in Mufa | Functional equivalent |
| Splice Event | Patch Event | Permanent ↔ Mutable operations |

### Connection Rules
1. **ODF ↔ ODF** → via FOLink (abstracted path through OSP).  
2. **FOLink** = { Path + Segments + Infrastructure + Splice / Patch Events }.  
3. **Path** = collection of Segments; **Segment** = line between Structures.  
4. **Section** = link between Substructures (Mufa ↔ Chamber).  
5. **Manhole contains Container contains ODF**; equivalent for Aerial via Mufa.  
6. **Poles have Levels; Levels may host Mufas or cables.**  
7. **Cable hierarchy:** Cable → Strand → Pigtail → Port.
