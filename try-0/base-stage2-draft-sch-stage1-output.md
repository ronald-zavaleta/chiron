### 1. What You Just Specified (in my own words) <!-- [SEC-1] -->

[NOTE. This section captures the essence of the raw requirement as described by the user. Future prompts should restate, in natural and explanatory language, the key functionality or concept that was just described in the source text. The tone should be descriptive but analytical, summarizing the intent rather than copying the wording. Each iteration may rephrase this section to ensure the evolving understanding remains coherent.]

You basically described a **3D interactive topology environment** composed of stacked geospatial planes, spheres, and links — with both a **macro view** (planes + spheres + links) and **micro views** (detailed sphere and link inspections). The system behaves like a visual network explorer with strong geometric grounding (LAT/LON), configurable colors, and persistent configuration.

At a high level:

- There is a **central vertical Z-axis** with three equidistant markers (*a*, *b*, *c*).

- Three **horizontal planes** (a1, b1, c1) are centered on these markers and share the same geospatial footprint (defined by 4 LAT/LON demarcation points).

- Each plane can host **spheres**, representing positional entities located via LAT/LON within that plane’s footprint.

- **Links** connect spheres within the same plane or across different planes, visually differentiated by line style.

- The user can **rotate the entire structure**, change colors of spheres and links, and manage data via **local storage + Settings tab** (JSON uploads for spheres and links, and coordinate inputs for plane demarcations).

- The main view is complemented by **pop-up based micro views**:

  - Plane pop-ups with tables (Spheres, Intra-plane Links, Inter-plane Links).

  - Sphere micro views that show a virus-like sphere with multiple **Termination Points (TPs)**.

  - Link micro views that show both endpoint spheres (with TPs) and the link using specific TP color logic.

- The system supports **search tools** (macro and micro) and allows **relocating spheres within their plane** and persisting the updated position in local storage.

Overall, the system combines **3D visualization**, **graph-like topology**, and **interactive drill-down views** driven by data stored and configured through the UI.

---

#### 1.1 Visually <!-- [SYS-VIS] -->

[NOTE. This subsection should describe all **visual or geometric aspects** of the system or interface being designed. Include elements like shapes, spatial organization, perspective, axes, layers, or any graphic metaphors (e.g., planes, spheres, cubes). Future iterations may extend this section with new elements (e.g., icons, lighting, visual states), but must preserve the structural coherence of the visualization.]

- **Central Z-axis (vertical line):**

  - A vertical **dashed gray line** representing the Z-axis of the 3D space.

  - It has **three equidistant markers**:

    - **a** at the top,

    - **b** in the middle,

    - **c** at the bottom.

- **Horizontal planes (a1, b1, c1):**

  - **b1 plane**:

    - A horizontal plane whose **center is pierced by the Z-axis** at marker **b** (middle).

    - Defined by **four demarcation points** (P1–P4) expressed as **LAT/LON decimal coordinates**.

    - Visually rendered as a **semi-transparent purple** surface.

  - **a1 plane**:

    - Centered at marker **a** (top).

    - Shares the **same LAT/LON footprint** as b1; conceptually, b1’s footprint is “lifted” upward to define a1.

    - Rendered as **semi-transparent turquoise**.

  - **c1 plane**:

    - Centered at marker **c** (bottom).

    - Shares the **same LAT/LON footprint** as b1; conceptually, b1’s footprint is “pushed down” to define c1.

    - Rendered as **semi-transparent blue**.

  - Together, these three planes form the visual impression of a **transparent cube-like volume**.

- **Spheres (macro visual):**

  - Positioned on each plane according to their **LAT/LON** coordinates within that plane’s demarcation polygon.

  - Each sphere is **bisected by its plane**:

    - Half of the sphere above the plane,

    - Half below the plane.

  - Default sphere color: **solid (non-transparent)** version of its parent plane’s color.

  - Sphere color can be overridden (e.g., red, orange, dark gray) via UI controls.

- **Links (macro visual):**

  - **Intra-plane links**:

    - Connect two spheres **within the same plane**.

    - Rendered as **solid green lines** by default.

  - **Inter-plane links**:

    - Connect spheres **across different planes**.

    - Rendered as **dashed green lines** by default.

  - Both link types have **visible labels** in the render area (e.g., link names or IDs).

- **Micro “virus-like” sphere view (sphere detail visualization):**

  - When drilling into a single sphere, it can be displayed as a **virus-like 3D object**:

    - A central spherical body.

    - Multiple **protrusions** on the surface, each protrusion representing a **Termination Point (TP)**.

  - TPs have a **default color of green**, with possible overrides to **red, orange, or dark gray**.

  - The sphere must be **rotatable** in this micro view so the user can explore TP distribution across the surface.

- **Micro link detail view:**

  - When drilling into a link, the visualization shows:

    - The **link** itself.

    - The two **spheres** (each sphere contains one the **TP** that the **link** uses) shall be rendered in the **virus-like style** with visible TPs. Each **sphere** will show the **TP** that is in associated with the **link** only.

  - The link visually **attaches to one TP on each sphere**, emphasizing which TPs participate in that specific connection.

  - The **link’s color** is derived from the TP colors:

    - If both TPs are green → link appears green.

    - If any TP is red, orange, or dark gray → the link adopts that non-green color.

Overall, the UI visually communicates a **3D layered geospatial topology** at the macro level and **rich, TP-based detail** at the micro level, with color and line style used to distinguish types of objects and states.

---

#### 1.2 Main objects / entities <!-- [ENT] -->

[NOTE. Here, enumerate and define each main entity identified in the requirements (e.g., planes, spheres, links). Each entity must include a definition, a short description of its purpose, and the key attributes that define it. Future prompts should add new entities as discovered in later iterations (e.g., Termination Points), maintaining consistent formatting and hierarchy.]

- **Z-axis (Vertical Line)**

  - **Definition:** A vertical dashed gray line representing the central axis of the 3D scene.

  - **Purpose:** Provides reference for vertical positioning of the three planes and their markers (a, b, c).

  - **Key attributes:** Markers (a, b, c); visual style (dashed, gray).

- **Plane**

  - **Definition:** A horizontal geospatial layer (a1, b1, c1) defined by four LAT/LON demarcation points.

  - **Purpose:** Hosts spheres and intra-plane links; forms part of the stacked 3D volume.

  - **Key attributes:**

    - ID (e.g., a1, b1, c1).

    - Center position on Z-axis (aligned with marker a, b, or c).

    - LAT/LON corners: P1–P4.

    - Color (semi-transparent turquoise, purple, blue).

    - List of spheres belonging to the plane.

- **Sphere**

  - **Definition:** A 3D node positioned on a specific plane, representing a spatial or logical element.

  - **Purpose:** Serves as an endpoint for links and as a container for Termination Points (TPs) in micro views.

  - **Key attributes:**

    - Name/ID.

    - Associated plane (a1, b1, or c1).

    - LAT, LON within plane footprint.

    - Radius.

    - Default color (derived from plane) + optional color override (red, orange, dark gray).

    - Collection of Termination Points (in micro view).

- **Link**

  - **Definition:** A connection between two spheres, either within the same plane (intra-plane) or between different planes (inter-plane).

  - **Purpose:** Represents relationships or logical connectivity between spheres.

  - **Key attributes:**

    - ID / label (visible in main render).

    - From-sphere and to-sphere references.

    - Type: **intra-plane** or **inter-plane**.

    - Default color: green, with possible overrides (red, orange, dark gray).

    - Line style: solid (intra-plane) or dashed (inter-plane).

    - Associated TPs at each endpoint (used in micro link view).

- **Termination Point (TP)**

  - **Definition:** A “protrusion” on the surface of a sphere in the micro view, representing a specific termination endpoint for links.

  - **Purpose:** Provides a finer-grained representation of how links attach to spheres; each link uses two TPs (one on each sphere).

  - **Key attributes:**

    - ID/name or label.

    - Parent sphere reference.

    - Color/state: default green; overridable to red, orange, dark gray.

    - Spatial position on the sphere surface (for visualization).

    - Associated link(s) that terminate on this TP.

- **Plane Pop-up**

  - **Definition:** A pop-up window launched from the main UI, associated with a specific plane.

  - **Purpose:** Displays tabular data for all spheres and links on that plane and enables selection-based highlighting in the main view.

  - **Key attributes:**

    - Plane ID context.

    - Spheres Table (rows = spheres on that plane).

    - Intra-plane Links Table.

    - Inter-plane Links Table (links from this plane to others).

- **Sphere Micro View Pop-up**

  - **Definition:** A pop-up window that shows a single sphere in virus-like form with all its TPs.

  - **Purpose:** Allows detailed inspection and color management of TPs and visualization of how links attach.

  - **Key attributes:**

    - Sphere context (selected sphere).

    - Rotatable 3D virus-like sphere visualization.

    - List/visualization of TPs with their colors and labels.

    - TP color control (green, red, orange, dark gray).

    - Search/filter for TPs by name or label.

- **Link Micro View Pop-up**

  - **Definition:** A pop-up window that shows a specific link and its two endpoint spheres rendered with their TPs.

  - **Purpose:** Allows inspection of how a link attaches to specific TPs on each sphere and how TP state influences link color.

  - **Key attributes:**

    - Link context (selected link).

    - Two virus-like sphere visualizations (source and target).

    - Highlighted TPs used by that link.

    - Link color derived from TP colors.

    - Name/label display for spheres, TPs, and link.

- **Settings Tab**

  - **Definition:** A configuration area where the user defines or updates demarcation points, sphere data, and link data.

  - **Purpose:** Controls data input (via text fields and JSON uploads) and persistence of configuration in local storage.

  - **Key attributes:**

    - Inputs for P1–P4 (LAT/LON) demarcation points.

    - Upload controls for:

      - Sphere JSON per plane (a1, b1, c1).

      - Intra-plane link JSON.

      - Inter-plane link JSON.

    - Logic to read/write local storage.

- **Search Tool**

  - **Definition:** Search functionality available in both macro and micro contexts.

  - **Purpose:** Enables users to quickly locate spheres, links, or TPs by name or label.

  - **Key attributes:**

    - Search scope: macro topology view, plane pop-ups, sphere micro view, link micro view.

    - Query input (text).

    - Matching and highlighting behavior.

- **Local Storage Data Model**

  - **Definition:** The browser’s local storage used as a persistent store for plane demarcations, sphere positions, link definitions, and updated sphere positions.

  - **Purpose:** Retains user-provided or adjusted configuration between sessions.

  - **Key attributes:**

    - Keys for demarcation points (P1–P4).

    - Keys per plane for sphere JSON.

    - Keys for intra- and inter-plane link JSON.

    - Updated positions for relocated spheres.

---

#### 1.3 Relationships / hierarchy <!-- [REL] -->

[NOTE. Describe how entities relate to one another. Specify parent-child hierarchies, associations, containment, and interaction rules between entities (e.g., Plane contains Spheres; Link connects Spheres). Use short diagrams or nested lists if needed. When future iterations introduce new entities, update this section to integrate their relational context without rewriting existing relationships unless those are superseded.]

- **Z-axis & Planes**

  - The **Z-axis** has three key markers: a (top), b (middle), c (bottom).

  - Each marker is associated with **one plane**:

    - Marker **a** ↔ Plane **a1**.

    - Marker **b** ↔ Plane **b1**.

    - Marker **c** ↔ Plane **c1**.

  - All planes share the **same geospatial footprint** (same demarcation polygon P1–P4).

- **Planes & Spheres**

  - Each **Plane** contains **zero or more Spheres**.

  - Each **Sphere** belongs to **exactly one Plane** (a1, b1, or c1).

  - Sphere LAT/LON coordinates must lie **within** the Plane’s demarcation polygon.

- **Spheres & Termination Points (TPs)**

  - Each **Sphere** contains **zero or more TPs** (Termination Points).

  - Each **TP** belongs to **exactly one parent Sphere**.

  - In micro views, TPs are positioned on the surface of the Sphere visualization.

  - TP color/state is decoupled from the sphere color/state.

- **Spheres & Links**

  - A **Link** connects **two Spheres**:

    - Intra-plane: both spheres on the **same plane**.

    - Inter-plane: spheres on **different planes**.

  - A Link must reference two valid TP IDs and, by inheritance, the Link has reference to the Spheres IDs (parent of the TPs).

- **Termination Points (TPs) & Links**

  - At micro level, each **Link** is associated with **two TPs**:

    - One TP on the **source sphere**.

    - One TP on the **target sphere**.

  - A TP may be associated with:

    - No links (unconnected TP).

    - One or more links (multiple links share the same TP).

- **Plane Pop-ups**

  - Each **Plane Pop-up** is associated with **exactly one Plane**.

  - It **displays and references**:

    - All Spheres belonging to that Plane.

    - All intra-plane Links whose endpoints are both on that Plane.

    - All inter-plane Links where at least one endpoint is on that Plane.

- **Sphere Micro View Pop-up**

  - Each **Sphere Micro View Pop-up** is associated with **exactly one Sphere**.

  - It displays:

    - The Sphere (virus-like visualization).

    - All TPs belonging to that Sphere.

    - Any Links (if desired) that terminate on TPs of that Sphere.

- **Link Micro View Pop-up**

  - Each **Link Micro View Pop-up** is associated with **exactly one Link**.

  - It displays:

    - The Link itself.

    - The two endpoint Spheres.

    - The specific TPs used by the link on each sphere.

- **Settings Tab & Local Storage**

  - The **Settings Tab** is the UI owner of:

    - Plane demarcation definitions (P1–P4).

    - Sphere JSON definitions per plane.

    - Link JSON definitions for intra- and inter-plane links.

  - The **Local Storage** stores:

    - Plane demarcations.

    - Sphere sets per plane (including updated positions after relocation).

    - Link definitions (intra- and inter-plane).

  - Settings Tab reads from and writes to Local Storage, which is then used by the main render view.

- **Search Tools**

  - **Macro search** relates to:

    - Spheres and Links in the main topology view.

  - **Micro search** relates to:

    - Spheres/Links rows in Plane pop-ups.

    - TPs (and possibly spheres/links) in Sphere/Link micro views.

  - Search results are tied back to the corresponding entity instances for highlighting and focusing.

---

#### 1.4 Behavior & interactions <!-- [BEH] -->

[NOTE. Explain how entities behave and interact from both the system and user perspectives. Include both general (system-wide) behaviors and view-specific (macro/micro) interactions. Each iteration may introduce new behaviors (like double-clicking to open pop-ups) — these should be added as sub-sections with the same naming style.]

##### 1.4.1 Generic (Applies to all Level Views) <!-- [BEH-GEN] -->

[NOTE. Capture the universal interaction rules that apply across all interface levels (e.g., 3D rotation, hover highlights). Future additions should remain general — specific behaviors belong in later subsections.]

- **Click-and-drag rotation:**

  - User can click and drag on **any plane area**.

  - The entire cube-like structure (all three planes, spheres, links, axis) rotates together around one or more axes.

- **Selection & highlighting (conceptual):**

  - Selecting an entity in any view (macro or micro or table) causes the corresponding visual element(s) to be **highlighted**.

- **Consistent labeling:**

  - Names and labels for spheres, links, and TPs are always available in micro views, and generally appear or can be revealed in macro views by hovering on top of the entity or by selecting (click) on the entity.

##### 1.4.2 Macro Level View (inside Main UI) <!-- [BEH-MACRO] -->

[NOTE. Describe user interactions that occur in the main visualization or cube view. Focus on actions like selection, dragging, highlighting, or zooming that affect the global scene.]

- **Rotation via planes:**

  - User clicks on any of the three planes and drags:

    - The **entire 3D scene rotates** as if it were a single solid object (cube-like behavior).

- **Sphere behavior:**

  - Spheres are visible on their respective planes, showing their color and name/label (macro labeling may use hover or always-on labels depending on design).

  - **Double-click on a sphere**:

    - Opens the **Sphere Micro View Pop-up**, showing the virus-like sphere with all its TPs.

- **Link behavior:**

  - Links between spheres are visible as:

    - Solid lines (intra-plane).

    - Dashed lines (inter-plane).

  - **Double-click on a link**:

    - Opens the **Link Micro View Pop-up**, showing the link and both endpoint spheres with their TPs.

- **Color override controls:**

  - In the main render UI, the user can:

    - Change the **default sphere colors** from “plane-derived” to specific overrides (red, orange, dark gray).

    - Change the **default link colors** from green to specific overrides (red, orange, dark gray).

  - Color changes should be immediately reflected in the visualization.

- **Search behavior (macro view):**

  - User can search by **sphere name** or **link label**.

  - Search results cause:

    - Matching sphere(s) or link(s) to be highlighted.

    - Optionally, the view to center or zoom toward the selected entity.

- **Sphere relocation:**

  - User can **relocate a sphere** within its plane in the main view.

  - Once relocated:

    - The **new coordinates are persisted** in local storage.

    - Links attached to that sphere update visually to the new position.

##### 1.4.n Micro Level View (inside the pop-ups) <!-- [BEH-MICRO] -->

[NOTE. Explain the behavior and interactivity inside detailed or secondary views (e.g., pop-ups, modals). Future iterations should number new micro-views sequentially if multiple are introduced (e.g., 1.4.3, 1.4.4).]

- **Plane Pop-up behavior:**

  - Trigger: clicking a button in the main UI for a specific plane (e.g., “Open Plane a1 Details”).

  - Contents:

    - **Spheres Table** (rows = spheres on that plane).

    - **Links Table** (rows = intra-plane links).

    - **Inter-Layer Links Table** (rows = links that connect this plane to other planes).

  - Interactions:

    - Selecting a **Sphere row**:

      - Highlights the corresponding sphere in the main 3D view.

      - Optionally centers or emphasizes the sphere in the macro scene.

    - Selecting a **Link row**:

      - Highlights the corresponding link (and its endpoint spheres) in the main view.

  - Search:

    - Each table has its own **search/filter tool** to locate rows by name/label.

- **Sphere Micro View Pop-up behavior:**

  - Trigger: **double-clicking on a sphere** in the main UI.

  - Contents:

    - A **rotatable virus-like sphere** visualization.

    - All **TPs** represented as protrusions (with names/labels).

    - A **color control** for TPs (green, red, orange, dark gray).

    - A **search tool** to quickly locate TPs by name or label.

  - Interactions:

    - User can **rotate the sphere** to inspect TPs all around the surface.

    - Changing a TP’s color:

      - Updates the TP’s visual state.

      - Influences any link that terminates on that TP (via the link color logic).

    - Names/labels of sphere and TPs are **always visible** in this micro view (no hover-only behavior).

   - Color override controls:

    - In the Micro View render UI, the user can:

      - Change the **default sphere colors** from “plane-derived” to specific overrides (red, orange, dark gray).

      - Change the **default TP colors** from green to specific overrides (red, orange, dark gray).

    - Color changes should be immediately reflected in the Micro View render UI and main render UI visualization.

- **Link Micro View Pop-up behavior:**

  - Trigger: **double-clicking on a link** in the main UI.

  - Contents:

    - The **link** itself.

    - Two **virus-like spheres** (the link’s endpoints).

    - The **two TPs** used by the link (one TP on each sphere) clearly highlighted.

    - A **search tool** to look up names/labels related to this link (sphere names, TP names, link label).

  - Interactions:

    - TP color logic:

      - If both associated TPs are green → the link is rendered green.

      - If one or more of the associated TPs is red, orange, or dark gray → the link takes that color instead of green.

    - Names and labels for spheres, TPs, and the link are **always visible** in this micro view.

---

#### 1.5 Data & Settings <!-- [DATASET] -->

[NOTE. Document the data model and configuration parameters used by the system. This includes what data is persisted, how it is stored (e.g., localStorage, JSON), and what UI elements are used for configuration. Future prompts may extend this section with new parameters or persistence mechanisms (e.g., APIs, databases).]

- The system uses **browser local storage** to persist:

  - Plane demarcation points (P1–P4, as LAT/LON).

  - Spheres per plane (including their coordinates, radius, and colors).

  - Intra-plane and inter-plane link definitions.

  - Updated sphere positions when spheres are relocated in the UI.

- A dedicated **Settings tab** is responsible for:

  - Inputting plane demarcation points.

  - Uploading JSON definitions for spheres and links.

  - Triggering persistence updates to local storage.

  - Setting the transparency of **Z-axis (Vertical Line)**. Default transparency is set to 30%.

##### 1.5.1 Data <!-- [DATA] -->

[NOTE. Define what data categories are stored and their purpose. For example: plane definitions, sphere sets, link data, TP states. Future iterations should keep the grouping consistent and may add new fields reflecting added functionality.]

- **Plane demarcation data**

  - Purpose: defines the shared geospatial footprint of all planes (a1, b1, c1).

  - Contents: four corner points **P1–P4**, each with LAT and LON.

  - Persistence: stored in local storage as structured data (e.g., JSON).

- **Sphere data per plane**

  - Purpose: defines all spheres on each plane.

  - Contents:

    - Sphere ID/name.

    - Plane ID (a1, b1, c1).

    - LAT, LON coordinates.

    - Radius.

    - Color or color override.

  - Persistence:

    - Read from uploaded JSON per plane.

    - Written back to local storage (including updated positions after sphere relocation).

    - The sphere state, is set by default (state/color set to green) or the sphere state can be user defined (via controls in Sphere Micro View). The requirements imply that the sphere state should be restorable i.e. after web page reload). Then, the sphere state must be stored in local storage.

- **Link data (intra-plane and inter-plane)**

  - Purpose: defines connectivity between spheres.

  - Contents:

    - Link ID/label.

    - From-sphere ID.

    - To-sphere ID.

    - Link type (intra or inter).

    - Optional color override.

  - Persistence:

    - Read from uploaded JSON for intra-plane links and inter-plane links.

    - Saved into local storage for reuse.

    - The Link state is derived from its TPs color/state from session state. The system must store the User defined Link color/state. For Link rendering purposes, the User defined Link color/state, takes precedence over session defined Link color/state derived from its TPs color/state.

- **Termination Point (TP) state (conceptual)**

  - Purpose: represents the color/state of each TP used in micro views and in link color resolution.

  - Contents:

    - TP ID/name.

    - Parent sphere ID.

    - TP color (green, red, orange, dark gray).

  - Persistence:

    - The TP state, is set by default (state/color set to green) or the TP state can be user defined (via controls in Sphere Micro View). The requirements imply that the TP state should be restorable i.e. after web page reload). Then, the TP state must be stored in local storage.

- **UI and interaction preferences (conceptual)**

  - Purpose: optional parameters influencing search behavior, default colors, or view settings (if made persistent).

  - Contents:

    - Potentially search defaults, last-used colors, or view preferences.

  - Persistence:

    - Not explicitly defined, but local storage is the natural place if these become requirements later.

##### 1.5.2 Settings <!-- [SET] -->

[NOTE. Specify what settings or configuration controls the user has. This includes fields, upload buttons, or UI options related to data definition. Future iterations may extend this list but should maintain the same layout and level of detail.]

- **Plane demarcation settings**

  - 4 textboxes in the Settings tab:

    - **P1**, **P2**, **P3**, **P4** — each accepting LAT/LON decimal coordinates.

  - User can input or modify corner coordinates and then save them to local storage.

- **Sphere configuration per plane**

  - 3 upload controls in the Settings tab:

    - One **JSON upload button** for each plane: a1, b1, c1.

  - Each uploaded JSON defines the set of spheres on that plane (IDs, positions, radii, colors).

- **Link configuration**

  - 1 upload control for **intra-plane links JSON**.

  - 1 upload control for **inter-plane links JSON**.

  - These JSONs define link endpoints and types and are persisted in local storage.

- **Color control settings (conceptual)**

  - Controls in the main UI and micro views allow:

    - Changing sphere colors (overriding plane-based defaults).

    - Changing link colors (overriding default green).

    - Changing TP colors (in micro views: green, red, orange, dark gray).

  - These settings influence **visual state**, and may optionally be persisted (exact persistence behavior can be defined later).

- **Search configuration (conceptual)**

  - Search tools exist:

    - In the macro topology view (for spheres and links).

    - In plane pop-ups (per table).

    - In micro sphere and link pop-ups (for TPs/spheres/links).

  - Each search control defines a **search scope** and matching logic (by name/label), even if not deeply configurable by the user yet.

---

#### 1.6 Functionally <!-- [FUNC] -->

[NOTE. Describe system functions that integrate multiple entities or data flows (e.g., pop-up generation, highlighting, event propagation). This section bridges the gap between interaction design and data architecture. Future iterations should refine or expand the functions as features evolve.]

- **Main 3D topology rendering**

  - Loads plane demarcation data, sphere sets per plane, and link definitions from local storage (or uploaded JSON).

  - Constructs the 3D scene:

    - Places the three planes (a1, b1, c1) at their respective Z-axis markers.

    - Positions spheres on each plane based on LAT/LON mapping.

    - Draws intra-plane and inter-plane links between sphere positions with appropriate line styles and labels.

- **Interactive rotation and exploration**

  - Interprets mouse drag on any plane as a rotation input.

  - Applies rotation to the entire 3D structure, maintaining relative positions of planes, spheres, and links.

- **Color override and propagation**

  - Applies UI-driven color overrides for spheres and links in the main view.

  - In micro views:

    - TP color changes propagate to any link using that TP.

    - Link color is recomputed based on its endpoint TP colors (green if both TPs green; otherwise adopts the non-green severity color).

- **Pop-up management**

  - Plane pop-up:

    - Creates and populates plane-specific tables (Spheres, Links, Inter-Layer Links) based on underlying data model.

    - Synchronizes row selections with highlight states in the main 3D view.

  - Sphere micro view:

    - On double-click of a sphere, loads that sphere’s TP set and constructs the virus-like 3D view.

    - Manages rotation, TP color changes, and label display.

  - Link micro view:

    - On double-click of a link, loads link details and its two endpoint spheres + specific TPs.

    - Renders both spheres and the link and applies TP-driven color logic.

- **Search and focus functions**

  - Macro search:

    - Accepts a query and finds matching spheres or links by name/label.

    - Highlights found entities and may center the camera on them.

  - Plane pop-up search:

    - Filters rows in Spheres, Links, and Inter-Layer Links tables for that plane.

    - Highlights selected row’s entity in the main 3D view.

  - Micro search:

    - In the sphere micro view, locates specific TPs by name/label and visually emphasizes them.

    - In the link micro view, may locate TP or sphere references related to that link.

- **Sphere relocation and persistence**

  - Allows user to move a sphere within its parent plane in the main 3D visualization.

  - Updates in real time:

    - Sphere’s visual position.

    - Connected links’ geometry.

  - Persists new sphere coordinates back to local storage so that future sessions or reloads reflect the updated topology.

- **Data refresh/update pipeline**

  - When settings are updated (e.g., new JSON uploaded, new demarcation points):

    - The system reads new data.

    - Updates local storage.

    - Rebuilds or refreshes the main 3D scene and associated pop-up data views to remain consistent.

Overall, these functions tie together **UI actions**, **data models**, and **3D visualization**, ensuring that changes in one area (e.g., TP colors, sphere positions, JSON uploads) are propagated consistently across all views and levels of detail.

---

---

### 2. Internal Architecture Plan (independent of framework) <!-- [ARCH] -->

[NOTE. As defined in Foundation Schema.]

#### 2.1 Data Shapes (Conceptual JSON per Entity) <!-- [DATA-SHAPES] -->

[NOTE. As defined in Foundation Schema.]

##### 2.1.1 Planes <!-- [ENT-PLN] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### 2.1.2 Spheres <!-- [ENT-SPH] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### 2.1.3 Links <!-- [ENT-LNK] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### 2.1.4 Termination Points (TPs) <!-- [ENT-TP] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### 2.1.5 Pop-ups & Detail Views <!-- [ENT-POP] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### 2.1.6 Settings & Storage Model <!-- [ENT-SET-STOR] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

#### 2.2 Mapping Logic / Core Algorithms <!-- [ALG] -->

[NOTE. As defined in Foundation Schema.]

##### 2.2.1 Planes Positioning and Coordinates <!-- [ALG-COORD] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### 2.2.2 Sphere Positioning from LAT/LON <!-- [ALG-SPH] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### 2.2.3 Link Geometry & Type Mapping <!-- [ALG-LNK] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### 2.2.4 TP & Link Color Resolution Logic <!-- [ALG-TP-LNK-COLOR] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

---

### 3. Interaction & UI Plan <!-- [UI] -->

[NOTE. As defined in Foundation Schema.]

#### 3.1 Render View / Main View <!-- [UI-MAIN] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

#### 3.2 Settings / Configuration Tab <!-- [UI-SET] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

#### 3.3 Popups / Detail Panels <!-- [UI-POP] -->

[NOTE. As defined in Foundation Schema.]

##### 3.3.1 Plane Detail Pop-up <!-- [POP-PLANE] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### 3.3.2 Sphere Detail Pop-up <!-- [POP-SPHERE] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### 3.3.3 Link Detail Pop-up <!-- [POP-LINK] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

#### 3.4 Highlighting & Feedback <!-- [UI-HL] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

---

### 4. Proposed Battle Roadmap (step-by-step) <!-- [ROAD] -->

[NOTE. As defined in Foundation Schema.]

##### Phase 1 – Skeleton 3D Scene <!-- [ROAD-1] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### Phase 2 – Spheres <!-- [ROAD-2] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### Phase 3 – Links <!-- [ROAD-3] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### Phase 4 – Settings & Persistence <!-- [ROAD-4] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### Phase 5 – Popups & Highlighting <!-- [ROAD-5] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

##### Phase 6 – Color Controls & Polish <!-- [ROAD-6] -->

[NOTE. As defined in Foundation Schema.]

Not required yet.

---

### 5. Annex-A Tag Map Table <!-- [ANN-A] -->

| Tag ID             | Section Title                     | Purpose / Description                                       | Merge Category    |
| ------------------ | --------------------------------- | ----------------------------------------------------------- | ----------------- |
| [SEC-1]            | What You Just Specified           | Root narrative for system concept and requirements context. | Introductory      |
| [SYS-VIS]          | Visually                          | Defines geometric and visual primitives.                    | System Definition |
| [ENT]              | Main Objects / Entities           | Lists all conceptual entities in the model.                 | Structural        |
| [REL]              | Relationships / Hierarchy         | Describes entity containment and connectivity.              | Relational        |
| [BEH]              | Behavior & Interactions           | Defines how entities behave and respond to user actions.    | Behavioral        |
| [BEH-GEN]          | Generic Behavior                  | Global interactions that apply across all views.            | Behavioral        |
| [BEH-MACRO]        | Macro Level View                  | Interactions in the main 3D topology view.                  | Behavioral        |
| [BEH-MICRO]        | Micro Level View                  | Interactions inside detailed pop-ups and micro views.       | Behavioral        |
| [DATASET]          | Data & Settings                   | High-level overview of data and configuration themes.       | Data Definition   |
| [DATA]             | Data                              | Catalog of stored data categories and their purpose.        | Data Definition   |
| [SET]              | Settings                          | Conceptual configuration parameters and their effects.      | Data Definition   |
| [FUNC]             | Functionally                      | Cross-entity/system functions tying UI, data, and behavior. | Functional        |
| [ARCH]             | Internal Architecture Plan        | Conceptual, tech-agnostic model of data and algorithms.     | Architectural     |
| [DATA-SHAPES]      | Data Shapes                       | Canonical JSON / schema per entity type.                    | Data Definition   |
| [ENT-PLN]          | Planes Data Shape                 | JSON/schema representation of planes.                       | Data Definition   |
| [ENT-SPH]          | Spheres Data Shape                | JSON/schema representation of spheres.                      | Data Definition   |
| [ENT-LNK]          | Links Data Shape                  | JSON/schema representation of links.                        | Data Definition   |
| [ENT-TP]           | TPs Data Shape                    | JSON/schema representation of Termination Points.           | Data Definition   |
| [ENT-POP]          | Pop-ups & Detail Views            | Data shapes for plane/sphere/link pop-ups.                  | UI / UX           |
| [ENT-SET-STOR]     | Settings & Storage Model          | Data shapes for configuration and persistence.              | Data Definition   |
| [ALG]              | Mapping Logic / Core Algorithms   | High-level description of computational and mapping logic.  | Architectural     |
| [ALG-COORD]        | Planes Positioning & Coordinates  | Normalization and placement of planes in 3D space.          | Architectural     |
| [ALG-SPH]          | Sphere Positioning from LAT/LON   | Mapping LAT/LON to local plane/sphere coordinates.          | Architectural     |
| [ALG-LNK]          | Link Geometry & Type Mapping      | Logic for intra/inter-plane link geometry and styling.      | Architectural     |
| [ALG-TP-LNK-COLOR] | TP & Link Color Resolution        | Rules for deriving link colors from TP states.              | Behavioral        |
| [UI]               | Interaction & UI Plan             | Overall UI structure and interaction overview.              | UI / UX           |
| [UI-MAIN]          | Render View / Main View           | Main 3D topology visualization and controls.                | UI / UX           |
| [UI-SET]           | Settings / Configuration Tab      | UI for configuring data and persistence.                    | UI / UX           |
| [UI-POP]           | Popups / Detail Panels            | UI containers for detailed views.                           | UI / UX           |
| [POP-PLANE]        | Plane Detail Pop-up               | Detailed per-plane tabular view.                            | UI / UX           |
| [POP-SPHERE]       | Sphere Detail Pop-up              | Detailed virus-like sphere + TP view.                       | UI / UX           |
| [POP-LINK]         | Link Detail Pop-up                | Detailed link + endpoint spheres + TPs view.                | UI / UX           |
| [UI-HL]            | Highlighting & Feedback           | Visual feedback rules for selection and focus.              | UI / UX           |
| [ROAD]             | Proposed Battle Roadmap           | Implementation sequence and evolution.                      | Roadmap           |
| [ROAD-1]           | Phase 1 – Skeleton 3D Scene       | Establish base rendering and spatial setup.                 | Roadmap           |
| [ROAD-2]           | Phase 2 – Spheres                 | Implement sphere placement and rendering.                   | Roadmap           |
| [ROAD-3]           | Phase 3 – Links                   | Implement link rendering and differentiation.               | Roadmap           |
| [ROAD-4]           | Phase 4 – Settings & Persistence  | Implement data upload, configuration, and storage.          | Roadmap           |
| [ROAD-5]           | Phase 5 – Popups & Highlighting   | Implement detailed pop-ups and selection feedback.          | Roadmap           |
| [ROAD-6]           | Phase 6 – Color Controls & Polish | Final visual refinements and controls.                      | Roadmap           |

---

### Annex-1. [Title] <!-- [ANN-1] -->

[NOTE. Use this annex for any out-of-structure or deferred requirements.]
