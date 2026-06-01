# 🦷 Simulator

A high-fidelity, interactive 3D dental surgical simulation experience built entirely within a single dashboard. This simulator provides a procedure-based learning environment for dental professionals to practice surgical techniques like extractions, implants, and root canals in a controlled, risk-free virtual space.

![screenshot](https://raw.githubusercontent.com/mochiyaki/dentist/master/demo.gif)

## 🚀 Overview

The simulator presents a stylized, professional interface featuring a 3D viewport of a human dental arch. Users select from various surgical missions, each requiring a specific sequence of surgical steps. Success depends on selecting the correct surgical instrument and interacting with the precise target tooth at the right time.

## 🏗️ Architecture

The simulator follows a **data-driven, single-page application (SPA)** architecture.

### 1. Core Engine (Three.js)
The visual foundation is powered by **Three.js**. It handles:
- **Procedural Geometry Generation**: Teeth (crowns and roots) are generated programmatically based on anatomical parameters (molar, premolar, canine, etc.), ensuring high detail without heavy assets.
- **Scene Management**: Manuses the rendering of the upper and lower jaws, gums, palate, and tongue.
- **Lighting & Shading**: Implements a realistic surgical lighting setup using `SpotLight`, `DirectionalLight`, and `AmbientLight` with advanced material properties (roughness, metalness, translucency).
- **Physics-lite Interactions**: Handles raycasting for precise tooth selection and anatomical interaction.

### 2. Logic & State Management (JavaScript)
A centralized global state object (`gs`) tracks:
- **Session Progress**: Current mission, current step, score, and accuracy.
- **Anatomical State**: A mapping of tooth keys to their physical state (e.g., `healthy`, `diseased`, `extracted`, `treated`).
- **Engine State**: Camera orientation, view modes (Upper/Lower/Both), and visual toggles (X-Ray/Wireframe).

### 3. UI & Orchestration
The UI is built using standard DOM elements, styled with advanced **CSS Variables** for dynamic theme switching (Light/Dark).
- **Mission Control**: Manages mission selection and step-by-step progression logic.
- **Tool Palette**: Dynamically renders available surgical instruments.
- **HUD (Heads-Up Display)**: Provides real-time feedback on score, accuracy, and current surgical objectives.

## 🗺️ System Structure Diagram

```text
+-----------------------------------------------------------------------+
|                          TOPBAR (Stats & Controls)                    |
| [Brand] [Score] [Accuracy] [Status Pill] [View Controls] [Theme]      |
+-----------------------------------------------------------------------+
|                  |                                     |              |
|   TOOLS COLUMN   |           VIEWPORT COL              | MISSION COL  |
| (Instrument Set) |       (Three.js 3D Canvas)          | (Mission List|
|                  |                                     |  & Progress) |
| [Mirror]         |  [Toolbar: View/X-Ray/Wire]         |              |
| [Retractor]      |                                     | [Mission A]  |
| [...]            |  [3D Arch: Upper & Lower Jaws]      | [Mission B]  |
|                  |                                     | [Mission C]  |
|                  |  [HUD Overlay: Crosshair/Tooltip]   |              |
|                  |                                     |              |
+------------------+-------------------------------------+--------------+
|                       MISSION COMPLETE MODAL                          |
|            (Results, Score, Retry, and Next Mission Flows)            |
+-----------------------------------------------------------------------+
```

## ⚙️ Workflow

Successful completion of a surgical mission follows a precise loop:

1.  **Initiation**: User selects a mission from the **Mission Control** panel (e.g., "Tooth Extraction").
2.  **Diagnosis**: The viewport highlights the target tooth. The user inspects the area using the **Dental Mirror**.
3.  **Instrumentation**: The user selects the required tool from the **Surgical Tools** list (e.g., **Retractor**, then **Elevator**).
4.  **Execution**:
    - User clicks the target tooth with the active tool.
    - The system validates if the tool matches the current procedure step.
    - If correct, a 3D animation/visual effect (e.g., tooth luxation or extraction) is triggered.
5.  **Progression**: The "Procedure Steps" list updates. The user continues until all steps in the mission are completed.
6.  **Conclusion**: A **Mission Complete** modal appears, displaying final accuracy, earned points, and a summary of the procedure.

## ✨ Key Features

-   **Procedural Anatomy**: Anatomically accurate tooth crowns and root clusters generated via math-based geometry.
-   **Multi-Mode Visualization**:
    -   **X-Ray Mode**: Toggles transparency of soft tissues (gums, palate) to reveal bone and roots.
    -   **Wireframe Mode**: Provides structural visualization of dental anatomy.
    -   **View Switching**: Toggle between Full Arch, Upper Jaw, and Lower Jaw views.
-   **Dynamic Theming**: Seamless transition between a professional high-contrast **Dark Mode** and a clean **Light Mode**.
-   **Interactive HUD**: Real-time feedback through toasts, tooltips, and a crosshair for precise targeting.
-   **Advanced Missions**: Includes complex procedures like **Dental Implants**, **Root Canals**, and **Bone Grafting**.

## 🛠️ Technical Stack

-   **Language**: JavaScript (ES6+)
-   **Styling**: CSS3 (Modern Flexbox/Grid, CSS Variables)
-   **Deployment**: HTML (Zero dependencies required beyond CDN)

## 🤖 MCP (please refer to the content inside the folder)
- **📚 Medical Literature**:
  - `search-medical-literature`: Query PubMed for research articles.
  - `get-article-details`: Retrieve detailed abstracts and metadata via PMID.
  - `search-google-scholar`: Access academic research via Google Scholar.
  - `search-medical-journals`: Focused searches in high-impact journals (NEJM, JAMA, etc.).
- **🌍 Global Health & Pediatrics**:
  - `get-health-statistics`: Access WHO Global Health Observatory data.
  - `get-child-health-statistics`: WHO indicators specifically for pediatric populations.
  - `search-pediatric-guidelines`: Access AAP (Bright Futures) and policy statements.
- **🔍 Multi-Database Search**:
  - `search-medical-databases`: An aggregate tool searching PubMed, Scholar, Cochrane, and ClinicalTrials.gov simultaneously.
- **📊 System Monitoring**:
  - `get-cache-stats`: Monitor server performance (hit rates, memory usage).
- etc.
