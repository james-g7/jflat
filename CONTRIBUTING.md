# Contributing to JFLAT

Firstly, thank you for considering contributing to JFLAT!

## Development Workflow

We follow a standard Milestone-based branching model and release process.
Please **do not** push directly to the `main` branch.

1. **Ensure your local branch is up to date:**
   ```bash
   git checkout `the-branch-name-here`
   git pull origin main
   ```
2. **Create a new branch for your feature or bugfix:**
   Use descriptive prefixes like `feat/`, `fix/`, `docs/`, or `refactor/`.
   ```bash
   git checkout -b feat/add-json-parser
   ```
3. **Commit your changes:**
   Write clear, concise commit messages. We recommend Conventional Commits (e.g., `feat: implement canvas grid drawing`).
4. **Push and open a Pull Request (PR):**
   Push your branch to GitHub and open a PR against the specific milestones branch. 
5. **CI/CD Checks:**
   Ensure all GitHub Actions workflows (compilation and unit tests) pass. PRs will not be merged if the build is failing.

## Coding Standards
* **Architecture:** Stick to the Model-View-Controller (MVC) pattern. Do not put business logic (like Turing machine evaluation) inside UI event listeners.
* **UI Framework:** We use standard Java Swing.
* **Testing:** All core logic (the `model` and `io` packages) must be covered by JUnit 5 tests. UI tests are not strictly required but UI code should be kept as "dumb" as possible to minimize bugs.
* **Namespacing:** All new classes should be placed under `uk.co.jamesgaskin.jflat`.

## Code Style
- **Interfaces**: prefix with `I` — e.g. `IState`, `ITransition`, `IAutomaton`
- **Classes**: PascalCase — e.g. `TuringMachineState`, `FiniteStateAutomaton`,,
- **Methods / variables**: camelCase (standard Java)
- **Tests**: JUnit 5 via Spring Boot Test; one test class per service class (e.g. `EventServiceTest` for `EventService`)
- **Style enforcement**: code must conform to the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html), enforced by the `maven-checkstyle-plugin` (Checkstyle 10.17.0, `google_checks.xml`) during `mvn verify`

## Reporting Bugs
If you find a bug, please open an Issue on GitHub. Include:
* Steps to reproduce the bug.
* Expected behavior vs. actual behavior.
* Your operating system and Java version.