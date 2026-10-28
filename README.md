🌊 FloodPath UCC — Campus Route Lab

🧭 An Interactive Stack-Based Campus Route Simulation

FloodPath UCC is an interactive web application that demonstrates how the stack data structure and Depth-First Search (DFS) can be used to explore routes while avoiding simulated flood-blocked areas.

This project applies data structures and algorithms to a campus-inspired navigation scenario through an interactive, visual experience.

---

🚀 Live Demo

🌐 Live Application: "Open FloodPath UCC" (https://hafsatuburhan.github.io/FloodPath-UCC/)

Try the application to explore the campus grid, simulate blocked pathways, and observe how a stack supports route exploration.

---

📑 Table of Contents

- "📌 Project Overview" (#-project-overview)
- "❗ Problem Statement" (#-problem-statement)
- "🎯 Project Objectives" (#-project-objectives)
- "🌍 Real-World Applications of Stacks" (#-real-world-applications-of-stacks)
- "🧠 Why Stacks Are Necessary" (#-why-stacks-are-necessary)
- "⚙️ How the Application Works" (#-how-the-application-works)
- "✨ Key Features" (#-key-features)
- "💻 Technologies Used" (#-technologies-used)
- "🗺️ How to Use the Application" (#-how-to-use-the-application)
- "📁 Project Structure" (#-project-structure)
- "⚠️ Project Limitations" (#-project-limitations)
- "📚 Learning Outcomes" (#-learning-outcomes)
- "👩‍💻 Author" (#-author)
- "📄 License" (#-license)

---

📌 Project Overview

FloodPath UCC is an educational route-finding simulation built around an illustrative 8 × 8 grid. Users can select a starting location and destination, mark pathway tiles as flooded, and search for a possible route that avoids blocked tiles.

The simulation features campus-inspired locations, including:

- 🚪 UCC Main Gate
- 📚 UCC Library
- 🏢 Administration
- 🏫 Central Quad
- 🌿 Ayensu
- 🏘️ Amamoma

Note: The grid is illustrative and is not an official University of Cape Coast map. Flood areas are manually simulated; the application does not use live weather or flood data.

❗ Problem Statement

Flooding can block pathways and make movement between locations difficult. A route-finding system must explore available paths while avoiding areas marked as inaccessible.

FloodPath UCC demonstrates how a stack-based search algorithm can explore possible routes between two locations while avoiding simulated flood-blocked tiles.

🎯 Project Objectives

The objectives of this project are to:

1. Demonstrate the practical application of the stack data structure.
2. Explain the Last In, First Out (LIFO) principle.
3. Implement Depth-First Search for route exploration.
4. Demonstrate backtracking when a path cannot continue.
5. Show how blocked tiles affect route availability.
6. Develop an interactive web application using HTML, CSS, and JavaScript.

🌍 Real-World Applications of Stacks

Stacks are useful in many computing applications.

Application| How a Stack Is Used
🌐 Browser navigation| Helps manage previously visited pages for backward navigation.
↩️ Undo and redo| Stores actions that can be reversed or repeated.
📞 Function calls| Manages active function calls during program execution.
🧮 Expression evaluation| Helps process mathematical expressions and operators.
🧩 Syntax parsing| Supports processing nested structures in programming languages.
🧭 Depth-First Search| Stores locations awaiting exploration during graph traversal.

FloodPath UCC focuses on the use of a stack in route exploration while avoiding blocked tiles.

🧠 Why Stacks Are Necessary

A stack follows the Last In, First Out (LIFO) principle. This means the last item added is the first item removed.

In Depth-First Search, a stack helps the algorithm explore one path deeply before returning to consider another.

The main operations include:

- Push: Adds a location to the top of the stack.
- Pop: Removes the top location from the stack for exploration.
- Visited tracking: Prevents repeated exploration of the same locations.
- Backtracking: Allows the search to return to an earlier point when a path cannot continue.

Using a stack makes the search process systematic and demonstrates how a basic data structure supports graph traversal.

⚙️ How the Application Works

FloodPath UCC uses a grid in which each tile represents a location or pathway.

1. The user selects a starting location and destination.
2. The user can mark eligible pathway tiles as flooded.
3. The DFS algorithm begins exploring from the starting tile.
4. A stack manages locations awaiting exploration.
5. Flooded and previously visited tiles are skipped.
6. The search stops when the destination is found or no route is available.
7. The interface displays the discovered route, stack information, and activity log.

Movement rules: The algorithm uses four-directional movement: up, down, left, and right. Diagonal movement is not supported.

Algorithm note: DFS can find a valid route when one exists, but it does not guarantee the shortest route.

✨ Key Features

- 🗺️ Interactive campus grid: Explore an 8 × 8 grid.
- 📍 Location selection: Choose a starting point and destination.
- 🌊 Flood simulation: Add or remove simulated flood blocks.
- 🧭 DFS route search: Explore possible routes using a stack.
- 💠 Route visualization: View the discovered route highlighted on the grid.
- 📚 Stack explorer: View information about stack-based exploration.
- 📋 Activity log: Review recorded search and interaction events.
- 📊 Statistics: View route and exploration information.
- 🔄 Reset controls: Clear the route and reset simulated flood areas.
- 📱 Responsive interface: Use the application on mobile phones and desktop computers.

💻 Technologies Used

Technology| Purpose
🧱 HTML5| Structures the application interface.
🎨 CSS3| Styles the interface and creates the responsive layout.
⚡ JavaScript| Implements interactivity, stack operations, flood simulation, and DFS.
🐙 GitHub| Hosts the source code repository.
🚀 GitHub Pages| Publishes the application online.

🗺️ How to Use the Application

1. Open the "FloodPath UCC live application" (https://hafsatuburhan.github.io/FloodPath-UCC/).
2. Select a starting location and destination.
3. Enable flood-editing mode and mark eligible pathway tiles as flooded.
4. Select Find Route Using DFS to begin the search.
5. Observe the highlighted route, stack information, and activity log.
6. Try different locations and flood configurations.
7. Clear the route or reset the flood blocks to try another scenario.

📁 Project Structure

The project contains three main application files and its documentation.

FloodPath-UCC/
├── index.html   # Application structure
├── style.css    # Styling and responsive layout
├── script.js    # Stack operations and DFS logic
└── README.md    # Project documentation

- "index.html" — Defines the application structure.
- "style.css" — Controls the visual appearance and responsive layout.
- "script.js" — Implements stack operations, flood simulation, and DFS route search.
- "README.md" — Explains the project and how to use it.

⚠️ Project Limitations

Although FloodPath UCC demonstrates route exploration, it has several limitations:

- The grid is illustrative rather than an official geographical map.
- Flood blocks are manually configured.
- The application does not provide real-time flood detection or safety recommendations.
- DFS does not guarantee the shortest route.
- Movement is restricted to four directions.
- The application is intended for educational purposes rather than real-world navigation.

📚 Learning Outcomes

This project demonstrates how stacks can support a practical route-exploration problem. It reinforces understanding of:

- The LIFO principle and stack operations.
- Graph traversal using Depth-First Search.
- Tracking visited locations.
- Backtracking when a path cannot continue.
- Avoiding blocked locations during route exploration.
- Building interactive web applications with HTML, CSS, and JavaScript.
- Publishing a static website using GitHub Pages.

👩‍💻 Author

Burhandeen Hafsatu

💻 Passionate Web Developer

📄 License

No license has been selected for this project. Unless a license is added, the default copyright rules apply to the source code.