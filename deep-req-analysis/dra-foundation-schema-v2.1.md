## Deep Requirements Analysis Results — Foundation Schema v2.1 (two-tier guidance system all sections)

---

### 1. What You Just Specified (in my own words) <!-- [SEC-1] -->

[NOTE. This section captures the essence of the raw requirement as described by the user. Future prompts should restate, in natural and explanatory language, the key functionality or concept that was just described in the source text. The tone should be descriptive but analytical, summarizing the intent rather than copying the wording. Each iteration may rephrase this section to ensure the evolving understanding remains coherent.]

>[SPECIFIC_INSTRUCTIONS.
>Re-express the Raw Requirements Text in your own words, keeping all the original intent but making it clearer, more organized, and easier to read.
>
>**How to write:**
>- Begin with a short introduction such as *“You basically described…”* or another equivalent opening phrase.
>- Then divide the explanation into thematic sub-blocks using clear headers or bullets:
>  - **Visually:** for any visual, geometric, or topological description.
>  - **Conceptually:** for logical, behavioral, or non-visual system concepts.
>  - **Functionally:** for processes or relationships between objects.
>
>**What to include:**
>- Identify and describe the main **objects/entities** mentioned (e.g., planes, nodes, spheres, screens, forms, etc.).
>- Describe how these entities **relate** (hierarchies, interactions, or dependencies).
>- Summarize the **behaviors/interactions** (user actions and system responses).
>- Summarize **data and settings** (what must be stored, configured, or persisted).
>
>**Formatting rules:**
>- Use concise bullets or short paragraphs.
>- Keep faithful to the user’s wording — clarify but do not invent.
>- Preserve the same tone and level of detail found in the RAW text.
>]

---

#### 1.1 Visually

[NOTE. This subsection should describe all **visual or geometric aspects** of the system or interface being designed. Include elements like shapes, spatial organization, perspective, axes, layers, or any graphic metaphors (e.g., planes, spheres, cubes). Future iterations may extend this section with new elements (e.g., icons, lighting, visual states), but must preserve the structural coherence of the visualization.]

>[SPECIFIC_INSTRUCTIONS.  
>**Purpose:**  
>Describe every **visual or geometric feature** of the system as derived from the Raw Requirements Text.  
>
>**Include:**
>  * The **geometric primitives** (planes, spheres, cubes, lines, layers, icons, etc.).  
>  * Their **spatial organization** — how they align, stack, or interconnect (e.g., top/middle/bottom planes, axes).  
>  * The **visual attributes** — colors, transparency, materials, textures, or lighting cues.  
>  * Any **reference coordinate system** or orientation (e.g., X/Y/Z axis markers, lat/lon mapping).  
>
>**Guidance:**  
>  * Keep language **descriptive but concise** — imagine explaining the visualization to a UI designer.  
>  * Avoid implementation terms (no CSS, shaders, or Three.js API references).  
>  * Use short bullet lists or paragraphs for readability.  
>
>**Iteration rules:**  
>  * New visual features introduced later (icons, animations, legends) should append here as new bullets.  
>  * Preserve the same visual hierarchy from earlier iterations.  
>]


---

#### 1.2 Main objects / entities

[NOTE. Here, enumerate and define each main entity identified in the requirements (e.g., planes, spheres, links). Each entity must include a definition, a short description of its purpose, and the key attributes that define it. Future prompts should add new entities as discovered in later iterations (e.g., Termination Points), maintaining consistent formatting and hierarchy.]

>[SPECIFIC_INSTRUCTIONS.  
>**Purpose:**  
>Identify and define every **main object or entity** mentioned in the Raw Requirements Text.  
>
>**Include for each entity:**
>  * **Name** — the canonical label (Plane, Sphere, Link, User, etc.).  
>  * **Definition** — a concise explanation of what it represents.  
>  * **Purpose** — why it exists or what role it plays in the system.  
>  * **Attributes** — essential properties (IDs, coordinates, colors, status, etc.).  
>  * **Optional metadata** — parameters or behaviors linked to that entity.  
>
>**Guidance:**  
>  * Write in a tabular or bullet-point format.  
>  * Keep definitions one or two sentences long — clear, neutral, factual.  
>  * Avoid redundancy with Relationships (that section handles hierarchy).  
>
>**Iteration rules:**  
>  * New entities discovered later should be appended here with consistent formatting.  
>  * If an entity becomes more complex (e.g., gaining subtypes), create sub-bullets under its name.  
>]


---

#### 1.3 Relationships / hierarchy

[NOTE. Describe how entities relate to one another. Specify parent-child hierarchies, associations, containment, and interaction rules between entities (e.g., Plane contains Spheres; Link connects Spheres). Use short diagrams or nested lists if needed. When future iterations introduce new entities, update this section to integrate their relational context without rewriting existing relationships unless those are superseded.]

>[SPECIFIC_INSTRUCTIONS.  
>**Purpose:**  
>Describe how all identified entities **relate, contain, or depend** on one another.  
>
>**Include:**
>  * Parent–child relationships (e.g., Plane → Sphere).  
>  * Peer or association links (e.g., Sphere ↔ Sphere via Link).  
>  * Containment or grouping structures (e.g., Scene contains all Planes).  
>  * Optional one-to-many or many-to-many mapping notes.  
>
>**Guidance:**  
>  * Use concise text, nested lists, or ASCII diagrams (Plane > Sphere > TP).  
>  * Keep language structural — avoid functional behavior here.  
>  * If unclear, prefer to describe in relational terms: “A connects to B” / “B belongs to C.”  
>
>**Iteration rules:**  
>  * Add new relationships only when new entities appear or hierarchy changes.  
>  * Keep earlier relationships intact unless explicitly replaced.  
>]


---

#### 1.4 Behavior & interactions

[NOTE. Explain how entities behave and interact from both the system and user perspectives. Include both general (system-wide) behaviors and view-specific (macro/micro) interactions. Each iteration may introduce new behaviors (like double-clicking to open pop-ups) — these should be added as sub-sections with the same naming style.]

>[SPECIFIC_INSTRUCTIONS.  
>**Purpose:**  
>Document **how users and system elements interact**, distinguishing general versus specific behaviors.  
>
>**Include:**  
>  * Interaction **categories** — generic, macro-level (main view), and micro-level (popup views).  
>  * Typical **actions** (click, drag, hover, double-click) and **responses** (highlight, open popup, rotate view).  
>  * If mentioned, any **feedback patterns** (color change, animation, status messages).  
>
>**Guidance:**  
>  * Keep verbs active and outcomes explicit (“Click → rotates cube,” “Select → opens popup”).  
>  * Do not duplicate detailed highlighting logic — that belongs to Section 3.4.  
>  * Avoid tool/framework names.  
>
>**Iteration rules:**  
>  * Add new behavior subsections (1.4.3, 1.4.4...) as the design grows.  
>  * Each new view or interaction context must define its scope and triggering mechanism.  
>]


##### 1.4.1 Generic (Applies to all Level Views)

[NOTE. Capture the universal interaction rules that apply across all interface levels (e.g., 3D rotation, hover highlights). Future additions should remain general — specific behaviors belong in later subsections.]

>[SPECIFIC_INSTRUCTIONS.  
>**Purpose:**  
>Capture behaviors that apply **universally** across the entire visualization or UI.  
>
>**Include:**  
>  * Navigation or camera controls (rotate, zoom, pan).  
>  * Common gestures or mouse actions.  
>  * Any consistent hover or focus effect shared across elements.  
>
>**Guidance:**  
>  * Keep this section brief — these are baseline rules, not exceptions.  
>  * Use simple, declarative sentences or bullet lists.  
>  * Example pattern: “Drag = rotate cube; Scroll = zoom; Hover = highlight.”  
>
>**Iteration rules:**  
>  * Add new global interactions only if they apply everywhere.  
>  * If a behavior becomes view-specific, move it to a dedicated subsection.  
>]


##### 1.4.2 Macro Level View (inside Main UI)

[NOTE. Describe user interactions that occur in the main visualization or cube view. Focus on actions like selection, dragging, highlighting, or zooming that affect the global scene.]

>[SPECIFIC_INSTRUCTIONS.  
>**Purpose:**  
>Explain interactions occurring **within the main visualization or global interface**.  
>
>**Include:**  
>  * How users interact with large-scale entities (planes, global links).  
>  * Camera and orbit behaviors specific to main scene.  
>  * Global selection, deselection, and drag mechanics.  
>
>**Guidance:**  
>  * Use imperative tone (“User clicks plane → highlight all spheres”).  
>  * Describe visible outcomes, not internal code.  
>  * Keep hierarchy consistent: macro actions here, micro details later.  
>
>**Iteration rules:**  
>  * When new top-level views appear (e.g., overview maps, dashboards), create new Macro subsections.  
>]


##### 1.4.n Micro Level View (inside the pop-ups)

[NOTE. Explain the behavior and interactivity inside detailed or secondary views (e.g., pop-ups, modals). Future iterations should number new micro-views sequentially if multiple are introduced (e.g., 1.4.3, 1.4.4).]

>[SPECIFIC_INSTRUCTIONS.  
>**Purpose:**  
>Define behaviors **within detailed or secondary views** (pop-ups, modals, side panels).  
>
>**Include:**  
>  * How data is displayed or editable within the popup.  
>  * How selections affect other components (e.g., highlight in 3D view).  
>  * Available navigation controls or filters.  
>
>**Guidance:**  
>  * Keep descriptions paired: **trigger → reaction**.  
>  * Example: “Select row in table → highlight linked node.”  
>  * Maintain concise, hierarchical formatting.  
>
>**Iteration rules:**  
>  * For each new popup context, add a numbered subsection.  
>  * Never overwrite existing micro views — extend sequentially.  
>]


---

#### 1.5 Data & Settings

[NOTE. Document the data model and configuration parameters used by the system. This includes what data is persisted, how it is stored (e.g., localStorage, JSON), and what UI elements are used for configuration. Future prompts may extend this section with new parameters or persistence mechanisms (e.g., APIs, databases).]

>[SPECIFIC_INSTRUCTIONS.  
>**Purpose:**  
>Summarize all **data storage and configuration themes** introduced in the Raw Requirements Text.  
>
>**Include:**  
>  * Distinction between *data* (persistent model objects) and *settings* (user-defined preferences).  
>  * Overview of how data flows between UI, storage, and render layers.  
>
>**Guidance:**  
>  * Keep this section high-level — details go in 1.5.1 and 1.5.2.  
>  * Use diagrams or flow bullets if complex.  
>  * Example: “User edits coordinates → JSON updated → stored in localStorage.”  
>
>**Iteration rules:**  
>  * Append new persistence mechanisms (API sync, DB schema) when they appear.  
>  * Keep logical grouping intact.  
>]


##### 1.5.1 Data

[NOTE. Define what data categories are stored and their purpose. For example: plane definitions, sphere sets, link data, TP states. Future iterations should keep the grouping consistent and may add new fields reflecting added functionality.]

>[SPECIFIC_INSTRUCTIONS.
>**Purpose:**  
>Define *what data the system needs to store or manage*, at both runtime and persistence levels.
>
>**What to capture:**
>  * The major **data categories** (e.g., planes, spheres, links, TPs, configurations, logs, metrics).
>  * For each category, describe:
>    - **Purpose** — why the data exists and what function it serves.
>    - **Structure summary** — key fields or attributes (ID, name, type, status, coordinates, etc.).
>    - **Persistence mechanism** — where it lives (localStorage, file upload, database, API, memory).
>    - **Lifespan** — temporary (session-based) vs. persistent (saved/reloaded).
>    - **Update flow** — how and when it changes (manual edit, automatic sync, periodic refresh).
>
>**How to write it:**
>  * Present data logically grouped (e.g., “Core Data”, “User Data”, “Runtime State”).
>  * Use short bullets or lightweight tables — do **not** repeat JSON structures (those belong to Section 2.1).
>  * Keep the explanation conceptual, not technical — this is a “data purpose catalog”, not an API spec.
>
>**Iteration rules:**
>  * New data categories discovered in future requirements should be appended, maintaining the same descriptive format.
>  * If a dataset evolves (e.g., “sphere” gains new attributes), note that here and cross-reference Section 2.1.
>
>Goal: Give a complete picture of *what kinds of data exist, why they matter, and how they behave across the system lifecycle*.
>]



##### 1.5.2 Settings

[NOTE. Specify what settings or configuration controls the user has. This includes fields, upload buttons, or UI options related to data definition. Future iterations may extend this list but should maintain the same layout and level of detail.]

>[SPECIFIC_INSTRUCTIONS.
>**Purpose:**  
>Describe the *logical configuration parameters* of the system — what can be configured conceptually, independent of any specific UI layout or control implementation.
>
>**What to capture:**
>  * The list of **settings domains** (e.g., plane demarcations, sphere appearance defaults, link color rules, TP severity thresholds, search behaviors).
>  * For each setting:
>    - **Name / label** (human-readable).
>    - **Scope** (per user, per session, per project, global).
>    - **Type** (boolean, numeric, enum, string, JSON blob, etc.).
>    - **Default value** and whether it is required or optional.
>    - **Effect on the system** (what changes when this setting changes).
>  * Any **grouping** of settings (e.g., “Visualization Settings”, “Data Input Settings”, “Behavioral Settings”).
>
>**How to write it:**
>  * Use bullets or small tables to keep things clear.
>  * Stay at the *requirements / conceptual* level — do **not** describe specific UI controls here (those belong to section 3.2 Settings / Configuration Tab).
>  * Whenever the RAW Requirements Text hints at “configurable”, “customizable”, “uploadable”, or “switchable” behavior, translate that into a well-defined setting in this section.
>
>**Iteration rules:**
>  * When future iterations introduce new tunable parameters (e.g., TP color mapping rules, filtering options, layout presets), add them to this list with the same structure.
>  * If a setting is deprecated or superseded, keep it in the list but mark it clearly as replaced, and reference the new setting.
>
>Goal: By reading this section alone, someone should understand *what can be configured in the system, what each option means, and how it conceptually affects behavior*, without needing UI details.
>]


---

#### 1.6 Functionally

[NOTE. Describe system functions that integrate multiple entities or data flows (e.g., pop-up generation, highlighting, event propagation). This section bridges the gap between interaction design and data architecture. Future iterations should refine or expand the functions as features evolve.]

>[SPECIFIC_INSTRUCTIONS.  
>**Purpose:**  
>Describe **cross-entity or systemic functions** that combine logic, data, and user interaction.  
>
>**Include:**  
>  * Processes triggered by events (e.g., clicking → open popup).  
>  * Computations or sync logic that coordinate multiple components.  
>  * Data propagation or visual update mechanisms.  
>
>**Guidance:**  
>  * Use concise verb-driven phrasing (detects, updates, refreshes).  
>  * Avoid duplication with algorithms (those belong to Section 2.2).  
>  * If a function spans multiple layers (UI ↔ data), illustrate sequence briefly.  
>
>**Iteration rules:**  
>  * Add new functions only when distinct new integration logic appears.  
>]


---

### 2. Internal Architecture Plan (independent of framework)

[NOTE. This section defines the conceptual data and algorithmic structure independent of any specific technology. It serves as the abstract model of the system. Each iteration may enrich it with new data entities, relations, or algorithmic processes, but should preserve modularity and readability.]

### 2.1 Data Shapes (Conceptual JSON per Entity) <!-- [DATA-SHAPES] -->

[NOTE. Present canonical JSON structures describing how data for each entity is organized. Each subsection corresponds to an entity defined in Section 1.2. When new entities emerge, future iterations should add matching JSON templates here.]

>[SPECIFIC_INSTRUCTIONS.
>* Extract all **data-related definitions** from the RAW Requirements Text.
>* Identify each **entity type** (e.g., planes, nodes, links, transactions, users, etc.) and provide a representative JSON or key–value schema.
>* Include realistic sample values that illustrate structure, not exact data.
>
>**For each entity:**
>- Declare an array or object named after the entity (e.g., `"planes"`, `"spheres"`, `"links"`).
>- Include:
>  - `"id"` — unique identifier.
>  - `"name"` / `"label"` — display name.
>  - `"type"` — subtype or classification if applicable.
>  - References to other entities (e.g., `"planeId"`, `"fromNode"`, `"toNode"`).
>  - Domain-specific attributes (coordinates, color, radius, status, amount, etc.).
>  - Optional overrides or metadata (e.g., `"colorOverride"`, `"flags"`).
>
>**Example pattern (adapt to context):**
>```json
>{
>  "entities": [
>    {
>      "id": "entity-1",
>      "type": "ExampleType",
>      "name": "Example Name",
>      "metadata": { "key": "value" },
>      "relationships": [ "other-entity-1", "other-entity-2" ]
>    }
>  ]
>}
>
>``````
>Ensure JSON is well-formatted, minimal, and syntactically valid.
>]

---

##### 2.1.1 Planes

[NOTE. Define the JSON structure representing planes, including IDs, colors, z-levels, and coordinates. Keep attributes aligned with actual geometric logic (e.g., corners, lat/lon).]

##### 2.1.2 Spheres

[NOTE. Define the JSON schema for spheres, including identifiers, coordinates, visual properties, and linkage to planes. Add new fields as entities gain more complexity (e.g., embedded TPs).]

##### 2.1.3 Links

[NOTE. Define the JSON schema for links, referencing their connected spheres (and later, TPs). Indicate type (intra/inter-plane), label, and optional visual overrides. Update as link logic evolves.]

---

#### 2.2 Mapping Logic / Core algorithms

[NOTE. Explain the algorithms that map logical or geographic data into visual or spatial form. For example: LAT/LON normalization, color propagation, or state synchronization. Future iterations should add new algorithmic rules as separate numbered subsections (e.g., 2.2.2, 2.2.3), always preserving chronological order of introduction.]

>[SPECIFIC_INSTRUCTIONS.
>If coordinates or transformations are involved (e.g., LAT/LON → X/Y, logical → visual, raw → normalized):
>  * Explain the **mapping logic step by step**.
>  * Use concise pseudo-formulas (like the `u, v` normalization pattern) to illustrate how raw data becomes spatial data.
>
>If no geometry is involved, use this subsection to describe:
>  * Core **computational logic** or evaluation processes.
>  * **Normalization rules** or conversions between internal and external values.
>  * **Validation** or filtering criteria.
>  * **Matching / lookup logic** between entities or states.
>
>Keep this section **implementation-agnostic** — no framework-specific syntax or language features.
>Focus on conceptual algorithms, mathematical logic, or procedural flow that would remain valid regardless of platform or technology.
>]

##### 2.2.1 Planes positioning and coordinates

[NOTE. Describe how plane coordinates are normalized and mapped into the 3D scene. This subsection should show formulas and parameter definitions. If later logic depends on this (e.g., distance normalization, link curvature), new subsections should reference this baseline.]

---

### 3. Interaction & UI Plan

[NOTE. Provide an architectural overview of all user-facing interface components. Each subsection should describe a distinct UI context (main view, settings tab, detail pop-ups) and explain its function, controls, and relation to the underlying data model. Future iterations should append new subsections for any new UI layers.]

#### 3.1 Render View / Main View <!-- [UI-MAIN] -->

[NOTE. Describe what the user sees in the main 3D environment: objects, visual states, controls, and interaction behavior. Include camera or rotation logic if relevant.]

>[SPECIFIC_INSTRUCTIONS.
>* Summarize all **visual and interactive components** in the main scene or interface view.
>* Describe what is rendered (planes, spheres, links, etc.), their color/shape logic, and how users interact with them.
>* Use concise bullet points for readability.
>
>**Include:**
>- Layout overview (e.g., “Central 3D canvas with three translucent planes”).
>- Object behavior (hover, click, drag, double-click).
>- Control elements (color pickers, toggle buttons, upload fields).
>- Camera and rotation behavior (e.g., drag to orbit, zoom level, reset view).
>
>**Output must include:**
>- Clear visual hierarchy of components.
>- Interaction summary using verbs (selects, highlights, rotates, opens pop-up, etc.).
>- References to stored/persistent states when relevant.
>
>Maintain a tone that’s instructive and technical; this section should read like part of a UI specification document.
>]

#### 3.2 Settings / Configuration Tab

[NOTE. Explain how users input or adjust data. List all available configuration options and their persistence model. If new configuration domains arise (e.g., TP color settings), they should be added here.]

>[SPECIFIC_INSTRUCTIONS.
>**Purpose:**  
>Define all *user-configurable parameters* and *system persistence methods* that affect how the visualization or data behaves.  
>
>**Include:**
>  * What can be configured (e.g., coordinates, thresholds, colors, JSON uploads, parameters, preferences).
>  * How each item is stored or remembered:
>     - localStorage keys  
>     - IndexedDB or browser memory  
>     - backend APIs or configuration files  
>  * The UI elements that enable configuration (textboxes, file inputs, dropdowns, toggles, sliders, color pickers, reset buttons).
>
>**Behavioral details:**
>  * Specify what happens on change (e.g., data reloaded, colors refreshed, validation triggered).
>  * Include default values and whether they are user-editable.
>  * Clarify any *linkage* between controls (e.g., changing plane coordinates updates dependent spheres).
>
>**Iteration rules:**
>  * If later iterations introduce new configuration topics (e.g., TP color persistence, link severity filters),  
>    add them here as additional bullet groups under the same structure.
>
>Keep this section focused on *data input, storage, and persistence flow* — not on visual layout or rendering.
>]

#### 3.3 Popups / Detail Panels

[NOTE. Describe secondary UI layers (pop-ups, modals) that present detailed data views. Each pop-up type should be defined in its own sub-subsection. Future iterations introducing new pop-up types should follow a numbered naming convention (e.g., 4.3.3, 4.3.4).]

>[SPECIFIC_INSTRUCTIONS.
>**Purpose:**  
>Define the *interactive secondary views* (pop-ups, modals, drawers, or floating panels) that display detailed data about specific entities or relationships.  
>
>**Include for each popup:**
>  * **Scope / Trigger:** What event opens it (e.g., double-click on sphere, link, or table row).  
>  * **Contents:** Which data tables or 3D visualizations appear (e.g., Spheres Table, Links Table, TP view).  
>  * **Controls:** Buttons, color selectors, search boxes, or filters present inside the popup.  
>  * **Behavior:** What happens when a row or element is selected — e.g., highlight corresponding object, center camera, show tooltips.  
>  * **Persistence:** Whether modifications made here (like color change) are stored and propagated to the main view.
>
>**Automatic Subsection Generation Logic:**  
>  * When the RAW Requirements Text describes **multiple pop-up types** (e.g., “one popup per plane,” “sphere detail,” “link detail”),  
>    generate one numbered subsection per popup following the pattern:
>    - `##### 3.3.1 [Popup Type Name] Detail pop-up`  
>    - `##### 3.3.2 [Popup Type Name] Detail pop-up`, etc.
>  * Use natural, meaningful names drawn from context (e.g., “Plane Detail pop-up,” “Sphere Detail pop-up,” “Link Detail pop-up”).
>  * Maintain sequential numbering and consistent structure inside each (scope, contents, controls, behavior).
>
>**Iteration rules:**
>  * Future iterations adding new popups must extend numbering (3.3.3, 3.3.4...) rather than overwrite existing ones.
>  * If a popup evolves into a more complex view (e.g., multi-scene modal), reference its original entry but describe the expanded behavior.
>
>**Stylistic guideline:**  
>  Keep explanations concise and hierarchical — bullets for structure, short paragraphs for behavior.
>]

##### 3.3.1 "1st Required" Detail pop-up

[NOTE. Placeholder for the first detailed pop-up definition. Future prompts should specify its purpose, layout, and content mapping.]

##### 3.3.2 "2nd Required" Detail pop-up

[NOTE. Placeholder for the second pop-up type. Use when the system introduces multiple, distinct detailed views.]

##### 3.3.n "n-th Required" Detail pop-up

[NOTE. This general form acts as a template for all future pop-ups. Each should define its data scope, triggering action, and interactive controls.]

#### 3.4 Highlighting & Feedback

[NOTE. Document the visual feedback and highlighting logic for user interaction. Include color, glow, or line width changes, and specify their meaning. Future iterations can add new feedback patterns or link states but should remain consistent with overall visual language.]

>[SPECIFIC_INSTRUCTIONS.
>**Purpose:**  
>Describe how the system communicates *state, focus, or selection* visually to the user.
>
>**Include:**
>  * How selection or focus is reflected (e.g., thicker lines, bold labels, enlarged nodes, opacity shifts, glow effects).  
>  * How system-level or user-triggered events appear (e.g., mouse hover, double-click, update confirmation).  
>  * Optional enhancements (e.g., “center on object”, “flash on selection”, “fade non-selected elements”).  
>  * Visual meaning of colors, transparency, or glow (e.g., red = error, orange = warning, green = normal).
>
>**Guidance:**  
>Keep the style *concrete and actionable*, but do **not invent new requirements** not implied by the Raw Requirements Text.  
>If multiple layers of feedback exist (hover vs. active selection vs. linked object highlight), describe them hierarchically.
>
>**Iteration rules:**  
>  * When future iterations introduce new feedback mechanisms (like focus transitions, animations, or contextual legends), append them to this section without deleting prior ones.  
>  * Maintain visual consistency with previously defined cues.
>]

---

### 4. Proposed Battle Roadmap (step-by-step)

[NOTE. Define the phased implementation plan. Each phase describes a clear milestone with goals and deliverables. When future iterations introduce new features or UI layers, they should append new phases rather than modify existing ones, preserving historical progression.]

>[SPECIFIC_INSTRUCTIONS.
>**Purpose:**  
>Outline a *logical sequence of progressive implementation stages* derived from the analyzed requirements.  
>This is not a full project plan but a conceptual evolution map — a guide for how the system might be realized in code once requirements are mature.
>
>**Include for each Phase:**
>  * A short **goal statement** (1–2 sentences) describing what is achieved.  
>  * A list of **key elements** or features to build or verify.  
>  * Optional remarks on dependencies or transition to next phase.
>
>**Guidance:**  
>Keep phases small, incremental, and logically ordered (e.g., geometry → data → interactivity → persistence → polish).  
>Use the same style for all phases to facilitate traceability.
>
>**Strategic note:**  
>This section becomes more relevant **after core requirements stabilization**.  
>During early requirement analysis, you may generate placeholder phases (e.g., “Phase 0 – Requirement Validation”) or keep the roadmap minimal.  
>Once the system moves into design or prototyping, expand the roadmap to reflect buildable milestones.
>
>**Iteration rules:**  
>New phases are appended sequentially; existing ones are never rewritten — they represent historical design intentions.
>]

##### Phase 1 – Skeleton 3D Scene

[NOTE. Establish the base rendering and spatial setup. Future prompts should keep this as the foundational milestone.]

##### Phase 2 – Spheres

[NOTE. Add spheres to planes, define core visual attributes. Keep alignment with earlier geometry rules.]

##### Phase 3 – Links

[NOTE. Implement link rendering logic, types (intra/inter-plane), and visual cues.]

##### Phase 4 – Settings & Persistence

[NOTE. Introduce data upload, save, and local persistence logic.]

##### Phase 5 – Popups & Highlighting

[NOTE. Implement pop-up interaction and selection-based highlighting.]

##### Phase 6 – Color Controls & Polish

[NOTE. Add final visual adjustments, color controls, and refinement steps.]

---

### Annex-1. [Title]

[NOTE. Use this annex for any out-of-structure or deferred requirements. When a requirement doesn’t fit existing sections, document it here temporarily before deciding on its structural placement in a future iteration.]

---

**End of Deep Requirement Analysis Results — Foundation Schema v1.6 (Enhanced Notes Edition)**
