### STAGE-E: Deep Requirement Analysis Full Population

**Foundation:** Stage-2 structural skeleton (Sections 1–4 + Annex), derived directly from Stage-1 output.
**Objective:** Populate all sections with comprehensive analytical and descriptive content without altering any structure.

---

#### SECTION 2: System Architecture & Logic <!-- [SEC-2] -->

[NOTE. This section explains the underlying architecture that supports the behaviors and interactions described in Section 1. It connects UI elements, data persistence, and visualization logic into a coherent technical model.]

##### 2.1 Architectural Overview <!-- [ARCH-OVERVIEW] -->

The system operates as a **3D interactive visualization engine** built on a modular, browser-based architecture. It integrates the following components:

* **Three.js rendering core** — Handles the 3D geometry, lighting, and rotation of planes, spheres, and links.
* **UI control layer (HTML/CSS/JS)** — Provides the user interface for settings, pop-up windows, color controls, and search tools.
* **Data layer (LocalStorage + JSON)** — Stores and retrieves all user configurations: plane demarcations, sphere data, links, and TP states.
* **Event controller** — Manages click, drag, double-click, and search events; synchronizes all macro and micro-level actions.

The architecture is **event-driven** and **state-aware**, meaning that any user action triggers a cascade of updates:

* Updates to colors, coordinates, or JSON uploads trigger a refresh in both data and visualization layers.
* Synchronized highlighting between main 3D view and pop-ups ensures consistent entity state representation.

##### 2.2 Data Flow Logic <!-- [ARCH-DATAFLOW] -->

Data flows through four major stages:

1. **Initialization:**

   * Load stored demarcations, sphere, and link data from LocalStorage.
   * Parse JSON to instantiate Plane, Sphere, and Link objects.
   * Render the base geometry (Z-axis, planes, spheres, links).

2. **User Interaction:**

   * Interactions (click, drag, search, double-click) are intercepted by the Event Controller.
   * Event metadata (selected entity, action type) is propagated to listeners.

3. **Data Update:**

   * LocalStorage is modified upon confirmed changes (e.g., sphere relocation or color override).
   * Dependent components (links, TPs) are recalculated and re-rendered.

4. **Rendering Refresh:**

   * Visualization updates dynamically to reflect changes without full reload.
   * Rebuild logic ensures integrity of geometric relationships (links maintain continuity after relocation).

##### 2.3 Synchronization Rules <!-- [ARCH-SYNC] -->

Synchronization ensures **UI consistency** and **data integrity** across all system layers:

* Pop-up selections highlight corresponding entities in the 3D view.
* TP color changes propagate upward to parent link colors.
* Sphere relocation triggers link geometry updates in real time.
* Searches in any view yield synchronized highlights across all related views.

These rules are enforced by a global **Observer Pattern** implementation, where each entity (Plane, Sphere, Link, TP) can emit and listen to events of interest.

---

#### SECTION 3: UI & Interaction Schema <!-- [SEC-3] -->

[NOTE. This section details the interactive design logic, user interface zones, and behavior integration. It translates entities and behaviors into actionable UI/UX components.]

##### 3.1 Main Interface Layout <!-- [UI-LAYOUT] -->

The interface is divided into three major regions:

1. **3D Visualization Area:**

   * Displays the cube-like topology (planes, spheres, links).
   * Responds to mouse and keyboard events for rotation and selection.
   * Always visible.

2. **Control Panel:**

   * Contains color controls, search bar, and buttons to open Plane pop-ups.
   * Provides direct access to visual and data configuration.

3. **Settings Tab:**

   * Accessible via tab switch or gear icon.
   * Contains all upload and coordinate input fields.
   * Persists configuration changes to LocalStorage.

##### 3.2 Pop-up Interface Logic <!-- [UI-POPUP] -->

Each pop-up window follows a **standardized template** with the following regions:

* **Header:** Contextual label (Plane a1 / Sphere X / Link Y).
* **Main Body:** One or more tables or visualization panels.
* **Footer:** Search box and control buttons (color overrides, close, save).

All pop-ups are modal, draggable, and resizable. They are dynamically created when triggered, ensuring minimal memory footprint.

##### 3.3 Event Interaction Schema <!-- [UI-EVENTS] -->

| Event            | Origin     | Action             | Result                             |
| ---------------- | ---------- | ------------------ | ---------------------------------- |
| Click + Drag     | Plane      | Rotate cube        | Updates all planes and links       |
| Double Click     | Sphere     | Open Sphere Pop-up | Loads TP data and visualization    |
| Double Click     | Link       | Open Link Pop-up   | Loads link + endpoint spheres      |
| Select Table Row | Pop-up     | Highlight object   | Highlights entity in 3D view       |
| Search Query     | UI         | Filter + Highlight | Focus camera and highlight matches |
| Color Change     | UI Control | Apply new color    | Repaint sphere/link + persist      |
| Sphere Drag      | Main View  | Relocate           | Update coordinates + LocalStorage  |

##### 3.4 UX Behavior Summary <!-- [UI-UXSUMMARY] -->

The UX is designed to create a **seamless exploration** experience:

* Macro → Micro transitions are always reversible.
* Pop-ups retain focus context (linked to current selection).
* All color and position changes are reversible and persisted.
* Hover and label behaviors adapt by view depth (macro vs micro).

---

#### SECTION 4: Technical & Data Specifications <!-- [SEC-4] -->

[NOTE. This section formalizes the schema-level specifications: data formats, JSON object structures, and local storage keys.]

##### 4.1 JSON Schemas <!-- [DATA-SCHEMA] -->

**Plane JSON Example:**

```json
{
  "plane_id": "b1",
  "corners": {
    "P1": {"lat": -6.4891, "lon": -76.3641},
    "P2": {"lat": -6.4885, "lon": -76.3635},
    "P3": {"lat": -6.4890, "lon": -76.3628},
    "P4": {"lat": -6.4895, "lon": -76.3632}
  },
  "color": "purple"
}
```

**Sphere JSON Example:**

```json
{
  "sphere_id": "S01",
  "plane_id": "b1",
  "lat": -6.4892,
  "lon": -76.3634,
  "radius": 0.2,
  "color": "#800080",
  "state": "green"
}
```

**Link JSON Example:**

```json
{
  "link_id": "L1",
  "from_sphere": "S01",
  "to_sphere": "S03",
  "type": "intra",
  "color": "green",
  "from_tp": "TP1",
  "to_tp": "TP2"
}
```

**Termination Point JSON Example:**

```json
{
  "tp_id": "TP1",
  "sphere_id": "S01",
  "color": "green",
  "label": "TP_A"
}
```

##### 4.2 Local Storage Key Mapping <!-- [DATA-KEYMAP] -->

| Entity             | Key                   | Value Type             |
| ------------------ | --------------------- | ---------------------- |
| Plane Demarcations | `planes_demarcations` | JSON (P1-P4 per plane) |
| Spheres            | `spheres_[plane_id]`  | JSON array of spheres  |
| Links (intra)      | `links_intra`         | JSON array             |
| Links (inter)      | `links_inter`         | JSON array             |
| TP States          | `tps_states`          | JSON array             |
| Preferences        | `ui_prefs`            | JSON                   |

##### 4.3 Functional Constraints <!-- [DATA-CONSTRAINTS] -->

* LAT/LON values must fall within valid geographic bounds.
* Each sphere ID must be unique per plane.
* Each link must reference valid spheres and TPs.
* Color values must match predefined palette (green, red, orange, dark gray).
* Relocations update the same local storage key — overwriting prior state.

##### 4.4 Rendering Parameters <!-- [DATA-RENDER] -->

* Plane transparency: 30%
* Sphere radius: adjustable (default 0.2 units)
* Link thickness: constant (default 0.05 units)
* Label font: sans-serif, white text with black outline
* Frame rate target: 60 FPS
* Lighting: ambient + directional white light

---

#### ANNEX A: Tag Map & Cross-References <!-- [ANNEX-A] -->

| Tag                | Anchor    | Section | Description                     |
| ------------------ | --------- | ------- | ------------------------------- |
| [SEC-1]            | Section 1 | 1       | Raw Requirement Interpretation  |
| [SYS-VIS]          | 1.1       | 1       | Visual & Geometric Description  |
| [ENT]              | 1.2       | 1       | Entities & Definitions          |
| [REL]              | 1.3       | 1       | Relationships                   |
| [BEH]              | 1.4       | 1       | Behaviors & Interactions        |
| [DATASET]          | 1.5       | 1       | Data & Settings                 |
| [FUNC]             | 1.6       | 1       | Functional Integration          |
| [SEC-2]            | Section 2 | 2       | System Architecture & Logic     |
| [ARCH-OVERVIEW]    | 2.1       | 2       | Architectural Overview          |
| [ARCH-DATAFLOW]    | 2.2       | 2       | Data Flow Logic                 |
| [ARCH-SYNC]        | 2.3       | 2       | Synchronization Rules           |
| [SEC-3]            | Section 3 | 3       | UI & Interaction Schema         |
| [UI-LAYOUT]        | 3.1       | 3       | Main Interface Layout           |
| [UI-POPUP]         | 3.2       | 3       | Pop-up Interface Logic          |
| [UI-EVENTS]        | 3.3       | 3       | Event Interaction Schema        |
| [UI-UXSUMMARY]     | 3.4       | 3       | UX Behavior Summary             |
| [SEC-4]            | Section 4 | 4       | Technical & Data Specifications |
| [DATA-SCHEMA]      | 4.1       | 4       | JSON Schemas                    |
| [DATA-KEYMAP]      | 4.2       | 4       | Local Storage Key Mapping       |
| [DATA-CONSTRAINTS] | 4.3       | 4       | Functional Constraints          |
| [DATA-RENDER]      | 4.4       | 4       | Rendering Parameters            |
