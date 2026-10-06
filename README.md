# JFLAT

JFLAT is a Java Swing-based desktop application designed for building, simulating, and visualising finite state automata, Turing machines, and Langauges. Built with a clean Model-View-Controller (MVC) architecture, JFLAT provides an intuitive graphical canvas for constructing state machines and testing input strings.

[![Version](https://img.shields.io/badge/version-0.5.1-blue.svg)](CHANGELOG.md)
[![Versioning](https://img.shields.io/badge/versioning-semantic-brightgreen.svg)](https://semver.org)
[![Code Style](https://img.shields.io/badge/code%20style-Google%20Java-blue.svg)](https://google.github.io/styleguide/javaguide.html)
[![Java](https://img.shields.io/badge/java-25+-orange.svg)](https://openjdk.org)


## Features (Planned)
* **Visual Editor:** Drag-and-drop interface for creating states and transitions.
* **Automata Simulation:** Step-by-step execution for Deterministic Finite Automata (DFA), Non-Deterministic Finite Automata (NFA), and Turing Machines.
* **Modern Serialization:** Save and load your workspaces using a robust, JSON-based `.jflat` file format.

## Prerequisites
* **Java Development Kit (JDK) 25 or higher**
* **Maven 4.0.0+**

## Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/jflat.git
   cd jflat
   ```

2. **Build the project:**
   ```bash
   mvn clean verify
   ```

3. **Run the application:**
   ```bash
   mvn exec:java -Dexec.mainClass="uk.co.jamesgaskin.jflat.Main"
   ```
   *(Alternatively, you can run the compiled `.jar` file found in the `/target` directory).*

## Documentation
* See `docs/architecture.md` for an overview of the codebase and MVC pattern.

## Contributing
Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on the code of conduct and the process for submitting pull requests.