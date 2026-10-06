# AI Coding Agent Context & Guidelines

This file provides system instructions and context for AI coding assistants (like Copilot, Cursor, Gemini, etc.) working within this repository. 

**Project Identity:**
* **Name:** JFLAT
* **Purpose:** A Java Swing desktop application for drawing, editing, and simulating Finite State Automata, Turing Machines, and Languages.
* **Primary Namespace:** `uk.co.jamesgaskin.jflat`
* **Build System:** Maven
* **Target JDK:** Java 25

**Core Architectural Rules (STRICT):**
1. **Model-View-Controller (MVC):** 
   * `model/`: Contains pure Java objects representing Automata, States, Transitions, and Simulation engines. NO Swing imports (`javax.swing.*` or `java.awt.*`) are allowed in this package.
   * `view/`: Contains Swing components (`JFrame`, `JPanel`, custom `JComponent` for the canvas). This package handles drawing ONLY. It must not contain graph traversal algorithms or automata logic.
   * `controller/`: Acts as the bridge, listening to View events and updating the Model, then triggering View repaints.
2. **Testing:**
   * Framework: JUnit 5 (Jupiter).
   * Focus tests heavily on the `model` and `io` packages.
   * Do not write tests that attempt to instantiate `JFrame` or visible UI components unless explicitly mocked, to ensure headless CI builds (`mvn verify`) do not crash.

## Conventions
- **Commits**: Conventional Commits (`feat:`, `fix:`, `chore:`, etc.). Breaking changes are marked using `<type>!:` (e.g. `fix!:`)
- **Versioning**: Semantic Versioning — see `CHANGELOG.md`
- **Branching**: feature branches (`feat/your-feature`), open an issue before PRing

## Code Style
- **Interfaces**: prefix with `I` — e.g. `IState`, `ITransition`, `IAutomaton`
- **Classes**: PascalCase — e.g. `TuringMachineState`, `FiniteStateAutomaton`,,
- **Methods / variables**: camelCase (standard Java)
- **Tests**: JUnit 5 via Spring Boot Test; one test class per service class (e.g. `EventServiceTest` for `EventService`)
- **Style enforcement**: code must conform to the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html), enforced by the `maven-checkstyle-plugin` (Checkstyle 10.17.0, `google_checks.xml`) during `mvn verify`

## Current State
in progress.