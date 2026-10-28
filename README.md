🌊 FloodPath UCC — Campus Route Lab

An Interactive Stack-Based Campus Route Simulation

FloodPath UCC is an interactive web application that demonstrates how the stack data structure can be used with Depth-First Search (DFS) to explore routes between locations while avoiding simulated flood-blocked areas.

The project applies fundamental data structure and algorithm concepts to a campus-inspired navigation scenario.

## 🚀 Live Demo

**Live Application:** [Open FloodPath UCC](https://hafsatuburhan.github.io/FloodPath-UCC/)

---

📑 Table of Contents

- "Project Overview" (#-project-overview)
- "Problem Statement" (#-problem-statement)
- "Objectives" (#-project-objectives)
- "Real-World Applications of Stacks" (#-real-world-applications-of-stacks)
- "Why Stacks Are Necessary" (#-why-stacks-are-necessary)
- "How the Application Works" (#-how-the-application-works)
- "Key Features" (#-key-features)
- "Technologies Used" (#-technologies-used)
- "How to Use the Application" (#-how-to-use-the-application)
- "Project Structure" (#-project-structure)
- "Limitations" (#-project-limitations)
- "Learning Outcomes" (#-learning-outcomes)
- "Author" (#-author)

---

📌 Project Overview

FloodPath UCC is an educational route-finding simulation built around an illustrative grid representing a campus environment. It includes campus-inspired locations such as the UCC Main Gate, UCC Library, Administration, Central Quad, Ayensu, and Amamoma.

Users can select a starting location and destination, mark pathway tiles as flooded, and run a search to find a possible route that avoids the blocked tiles.

The application demonstrates the relationship between stacks, graph traversal, and backtracking in a practical, interactive environment.

Important: The grid is illustrative and is not an official University of Cape Coast map. Flood areas are simulated manually, and the application does not use live weather, flood, or road-condition data.

🎯 Problem Statement

Flooding can block pathways and make movement between locations difficult. A route-finding system must explore available paths while avoiding areas that are marked as inaccessible.

FloodPath UCC models this problem using a grid. It applies Depth-First Search with an explicit stack to explore possible routes between a selected starting point and destination while skipping simulated flooded tiles.

🎯 Project Objectives

The objectives of this project are to:

1. Demonstrate the practical application of the stack data structure.
2. Explain the Last In, First Out (LIFO) principle through an interactive example.
3. Implement Depth-First Search for route exploration.
4. Demonstrate backtracking when a path cannot continue.
5. Show how blocked locations affect route availability.
6. Develop a responsive web application using HTML, CSS, and JavaScript.

🌍 Real-World Applications of Stacks

Stacks are used in many real-world computing applications.

Application| How a Stack Is Used
Browser navigation| Keeps track of previously visited pages for backward navigation.
Undo and redo| Stores actions so users can reverse or repeat operations.
Function calls| Manages active function calls during program execution.
Expression evaluation| Helps evaluate mathematical expressions and process operators.
Syntax parsing| Supports checking and processing nested structures in programming languages.
Depth-First Search| Stores locations or nodes waiting to be explored during graph traversal.

FloodPath UCC focuses on the last application: using a stack to explore a route through a grid while avoiding blocked tiles.

🧠 Why Stacks Are Necessary

A stack follows the Last In, First Out (LIFO) principle. This means that the last item added to the stack is the first item removed.

In Depth-First Search, a stack helps the algorithm explore one path deeply before returning to explore another option.

The main operations are:

- Push: Adds a location to the top of the stack.
- Pop: Removes the top location from the stack for exploration.
- Visited tracking: Prevents the algorithm from repeatedly exploring the same locations.
- Backtracking: Allows the search to return to an earlier point when a path cannot continue.

Using a stack makes this search process systematic and demonstrates how a basic data structure can support graph traversal.

⚙️ How the Application Works

FloodPath UCC uses a grid in which each tile represents a location or pathway.

1. The user chooses a starting location and destination.
2. The user may mark selected pathway tiles as flooded.
3. The DFS algorithm begins exploring from the starting tile.
4. A stack manages the locations awaiting exploration.
5. Flooded tiles and previously visited locations are excluded from further exploration.
6. The algorithm continues until it reaches the destination or determines that no route is available.
7. The interface displays the discovered route, stack information, and activity log.

The application uses four-directional movement: up, down, left, and right. Diagonal movement is not included.

Algorithm note: DFS can find a valid route if one exists, but it does not guarantee the shortest route.

✨ Key Features

- Interactive campus grid: Explore an 8 × 8 grid of pathway tiles.
- Location selection: Choose a starting point and destination.
- Flood simulation: Add or remove simulated flood blocks.
- DFS route search: Search for a route using an explicit stack.
- Route visualization: View the discovered route highlighted on the grid.
- Stack explorer: Observe information about the stack-based search.
- Activity log: Review recorded search and interaction events.
- Statistics: View route and exploration information.
- Reset controls: Clear the route and reset simulated flood areas.
- Responsive design: Use the application on mobile phones and desktop screens.

💻 Technologies Used

Technology| Purpose
HTML5| Structures the application interface.
CSS3| Provides the visual design, grid layout, and responsive styling.
JavaScript| Implements interactivity, flood simulation, stack operations, and DFS.
GitHub| Hosts the source code repository.
GitHub Pages| Publishes the application as a static website.

🧭 How to Use the Application

1. Open FloodPath UCC in your browser.
2. Select a starting location and destination.
3. Enable flood-editing mode to add or remove simulated flood blocks on eligible pathway tiles.
4. Select Find Route Using DFS to begin the search.
5. Observe the highlighted route and the stack and activity information.
6. Try different start and destination points or different flood configurations.
7. Use the reset controls to clear the route or restore the flood simulation.

📁 Project Structure

The project uses three main files:

FloodPath-UCC/
├── index.html   # Application structure
├── style.css    # Styling and responsive layout
├── script.js    # Stack operations and DFS logic
└── README.md    # Project documentation

⚠️ Project Limitations

FloodPath UCC is a learning and demonstration tool. It has the following limitations:

- The campus grid is illustrative rather than an official geographical map.
- Flood blocks are manually configured and do not represent real flood conditions.
- The application does not provide live navigation or safety recommendations.
- DFS does not guarantee the shortest available route.
- The grid uses four-directional movement only.

📚 Learning Outcomes

This project demonstrates how a stack can be applied to a route-exploration problem. It reinforces understanding of LIFO operations, graph traversal, visited tracking, backtracking, and the handling of blocked locations.

It also provides practical experience in building an interactive web application using HTML, CSS, and JavaScript and publishing it through GitHub Pages.

👩‍💻 Author

Burhandeen Hafsatu

Passionate Web Developer

---

📄 License

No license has been selected for this project yet. Unless a license is added, the default copyright rules apply to the source code.
