# JFLAT Software Architecture

This document outlines the core architectural design of the JFLAT application. 

JFLAT strictly adheres to the **Model-View-Controller (MVC)** design pattern. To maintain a clean, maintainable, and testable codebase, it is critical that the boundaries between these packages are respected. 

**Golden Rule:** The `model` and `io` packages must *never* contain any UI-related imports (e.g., `javax.swing.*` or `java.awt.*`).

---

## Package Breakdown

All code resides under the base namespace: `uk.co.jamesgaskin.jflat`

### 1. `model` (The Business Logic)
This package contains the pure mathematical representation of the automata. It has no knowledge of how it is being drawn on the screen.
*   **`State` / `Node`:** Represents a single state in a machine (e.g., `q0`). Stores logical properties like `isAcceptState`, `isStartState`, and its abstract X/Y coordinates for the canvas.
*   **`Transition`:** Represents the directed edge between two states. Contains the rules (e.g., read symbol, write symbol, tape direction).
*   **`Automaton` / `Machine`:** The aggregate root. Holds the collections of `States` and `Transitions`.
*   **`Simulator`:** The execution engine. Takes an `Automaton` and an input string/tape, processes the rules step-by-step, and outputs a final accepted/rejected result.

### 2. `view` (The User Interface)
This package handles everything the user sees. It uses Java Swing and Java2D (`java.awt.Graphics`). It reads data from the `model` but does not mutate the model directly.
*   **`MainFrame` (`JFrame`):** The primary application window, containing the menus, toolbars, and layout managers.
*   **`EditorCanvas` (`JPanel`):** The core visual component. Overrides `paintComponent(Graphics g)` to physically draw the circles and arrows based on the current `Automaton` state.
*   **`PropertiesPanel` (`JPanel`):** A contextual sidebar that displays (and allows editing of) the properties of the currently selected `State` or `Transition`.

### 3. `controller` (The Glue)
Controllers handle user input, update the Model, and instruct the View to refresh.
*   **`CanvasMouseHandler`:** Listens for clicks, drags, and releases on the `EditorCanvas`. Translates a "click on empty space" into a command to create a new `State` in the model. Translates a "drag between states" into a new `Transition`.
*   **`SimulationController`:** Manages the "Play / Step / Stop" actions. Instructs the `Simulator` to advance one step, and then tells the `EditorCanvas` to highlight the active state.

### 4. `io` (Data Persistence)
This package is responsible for saving workspaces to disk and loading them back into memory.
*   **`ProjectSerializer`:** Converts the `Automaton` model into the custom `.jflat` JSON format.
*   **`ProjectDeserializer`:** Parses a `.jflat` JSON file and reconstructs the `Automaton` object hierarchy.

---

## Data Flow (The Event Loop)
1. **User Action:** The user clicks on the `EditorCanvas` (View).
2. **Handling:** The `CanvasMouseHandler` (Controller) detects the click coordinates.
3. **Mutation:** The Controller calculates what should happen and calls methods on the `Automaton` (Model) to update the data (e.g., `automaton.addState(x, y)`).
4. **Update:** The Controller then calls `canvas.repaint()` on the View.
5. **Render:** The View loops through the updated Model and redraws the screen with the new state.