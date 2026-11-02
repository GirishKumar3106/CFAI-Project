::: {align="center"}
# Network Router

### Shortest Path Visualizer

A graph-based route-finding application built for the **Computational
Foundations of Artificial Intelligence (CFAI)** course.

Explore how **Dijkstra's, A\*, and IDA\*** search algorithms find routes
through a weighted network, and compare their theoretical
characteristics through an interactive visualization.

`<br>`{=html}

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-Web%20Framework-000000?style=for-the-badge&logo=flask&logoColor=white)
![Algorithms](https://img.shields.io/badge/Algorithms-Graph%20Search-16A34A?style=for-the-badge)
![Project](https://img.shields.io/badge/Course-CFAI-6D5CE7?style=for-the-badge)
:::Table of Contents
- Overview
- How It Works
- Algorithms
- Algorithm Comparison
- Features
- Technology Stack
- Project Structure
- Getting Started
- Using the Application
- Understanding the Results
- Limitations and Future
  Improvements
- Contributors
Overview
Network Router: Shortest Path Visualizer demonstrates how classical
graph-search algorithms can be applied to a network-routing problem.

The application models a social network as a weighted graph:
- Nodes represent people in the network.
- Edges represent connections between people.
- Edge weights represent the cost of moving between connected
  people.
A user selects a starting node and a destination, chooses a search
algorithm, and runs the route calculation. The application then displays
the resulting path and its total cost, with the selected route
highlighted in the graph.

The project combines algorithm implementation with a Flask-powered web
interface to make the search process easier to understand visually.
How It Works
The application follows a simple workflow:
1. Build the network --- represent people as nodes and their
   connections as weighted edges.
2. Choose the endpoints --- select the source and destination
   nodes.
3. Select an algorithm --- choose Dijkstra's, A*, or IDA*.
4. Find the route --- run the selected algorithm on the graph.
5. Visualize the result --- display the path, total cost, and
   highlighted route.
6. Compare algorithms --- review the algorithm characteristics
   presented by the application.
Algorithms
1. Dijkstra's Algorithm
Dijkstra's algorithm finds a minimum-cost path from a source node to
other reachable nodes in a graph with non-negative edge weights.

It repeatedly selects the unvisited node with the smallest known
distance and relaxes its neighbouring edges.

Key idea: Expand the currently cheapest known route.
2. A* Search
A* is an informed search algorithm. It combines the cost already spent
with a heuristic estimate of the remaining cost.

Its evaluation function is:

\(f(n) = g(n) + h(n)\)

Where:
- g(n) is the cost from the start node to the current node.
- h(n) is the estimated cost from the current node to the goal.
- f(n) is the estimated total cost of a solution path through that
  node.
Key idea: Use both the cost so far and an estimate of the distance
remaining to guide the search.
3. Iterative Deepening A* (IDA*)
IDA* combines the heuristic guidance of A* with the low memory usage
of iterative deepening depth-first search.

It performs depth-first searches using an increasing threshold based on
the evaluation function:

\(f(n) = g(n) + h(n)\)

Nodes whose evaluation exceeds the current threshold are not explored in
that iteration. The threshold is then increased and the search runs
again.

Key idea: Retain heuristic guidance while avoiding the large memory
requirements commonly associated with A*.
Algorithm Comparison
The following table gives the general theoretical characteristics of
these algorithms. Actual performance depends on the graph, heuristic,
data structures, and implementation.
  Algorithm         Search approach    Typical time         Typical space
complexity           complexity
  Dijkstra's        Uninformed,        O((V + E) log V)   O(V + E)
cost-based         with a binary heap   

  A*               Heuristic-guided   Exponential in the   O(b^d)
best-first search  worst case, often
expressed as
O(b^d)             
IDA*             Heuristic-guided   Exponential in the   O(bd)
iterative          worst case, often
deepening          expressed as
O(b^d)
Notation
- V --- number of vertices (nodes).
- E --- number of edges.
- b --- branching factor.
- d --- depth of the optimal solution.
Important: These are theoretical reference bounds, not benchmark
measurements from this application. A* and IDA* performance depends
heavily on the quality of the heuristic. The complexity shown for
Dijkstra assumes a binary-heap priority queue and an adjacency-list
graph representation.

Features
- Interactive graph-based representation of a network.
- Selection of source and destination nodes.
- Three route-finding algorithms: Dijkstra's, A*, and IDA*.
- Weighted connections between nodes.
- Route calculation with total path cost.
- Visual highlighting of the selected path.
- Algorithm information presented alongside the route result.
- Ability to add connections through the application interface.
Technology Stack
  Technology              Purpose
  Python                  Core programming language and algorithm logic
Flask                   Web application backend and routing
HTML, CSS, JavaScript   Browser interface and graph interaction
Graph representation    Models nodes, edges, and connection weights
Project Structure
CFAI-Project/
│
├── app.py             # Flask application and route logic
├── requirements.txt   # Python dependencies
└── README.md          # Project documentation
The repository's main application entry point is app.py. The browser
interface and graph visualization are served through the Flask
application.
Getting Started
Follow these steps to run the project locally.
Prerequisites
Make sure you have the following installed:
- Python 3
- pip (Python package installer)
- Git
1. Clone the repository
git clone https://github.com/GirishKumar3106/CFAI-Project.git
2. Open the project directory
cd CFAI-Project
3. Create a virtual environment
Windows:
python -m venv venv
venv\Scripts\activate
Linux / macOS:
python3 -m venv venv
source venv/bin/activate
4. Install dependencies
pip install -r requirements.txt
5. Run the application
python app.py
Open the local URL printed in your terminal by Flask. In a standard
Flask development setup, this is usually:
http://127.0.0.1:5000
Using the Application
1. Launch the Flask application.
2. Open it in your browser.
3. Select the starting node.
4. Select the destination node.
5. Choose Dijkstra's, A*, or IDA*.
6. Run the path-finding operation.
7. Inspect the calculated route and its total cost.
8. Observe the highlighted path in the graph.
9. Add connections where supported by the interface and try different
   routes.
Understanding the Results
The application is designed to help users understand the relationship
between graph structure and search strategy.

When a route is found, the result includes the selected path and its
total cost. The interface also presents algorithm characteristics such
as time-complexity information, completeness, and optimality.

Theoretical complexity and measured performance are different
things. Complexity describes how resource requirements grow as the
input grows. A true performance benchmark would additionally require
measuring execution time and memory usage over controlled test graphs.
Do not interpret the theoretical comparison as a measured benchmark.
Limitations and Future Improvements
Possible extensions to the project include:
- Add measured execution-time comparisons across identical test
  graphs.
- Track actual memory consumption for each algorithm.
- Display the number of expanded nodes and explored edges.
- Add graph-size controls to test algorithm behaviour on larger
  networks.
- Provide step-by-step animation of each algorithm's search process.
- Allow users to create custom graphs and edge weights.
- Add heuristic configuration and validation for A* and IDA*.
- Export route results and comparison reports.
Contributors
Project contributors
- Girish Kumar
- Wasim
Developed as part of the Computational Foundations of Artificial
Intelligence (CFAI) course.
::: {align="center"}
**Network Router --- Shortest Path Visualizer**

*Understanding graph search, one route at a time.*
:::
