
Network Router: Shortest Path Visualizer
A graph-based shortest-path visualizer built as a Computational Foundations of Artificial Intelligence (CFAI) course project. It models a social network as a weighted graph and uses search algorithms to find a route between two people.

The application combines a Python Flask backend with an interactive browser-based graph. Instead of viewing an algorithm only as code, users can select two nodes, choose a search algorithm, calculate a route, and see the result highlighted on the network.

Repository: GirishKumar3106/CFAI-Project

What the project does
The application represents people as nodes and their connections as weighted edges. The edge weight represents the cost of moving from one person to another.

After selecting a starting person and a target person, the user can run one of the available algorithms. The application returns the route and its total cost, then highlights the selected route in the graph.

The project currently includes three algorithms:

Dijkstra's Algorithm - finds a minimum-cost path in a graph with non-negative edge weights.
A Search* - uses the cost already travelled and a heuristic estimate of the remaining cost to guide the search.
Iterative Deepening A (IDA)** - uses repeated depth-first searches with an increasing cost threshold, reducing the memory required by a typical A* search.
Dijkstra's Algorithm is included as a baseline so that heuristic search approaches can be compared against it.

Features
Interactive weighted graph with nodes and labelled edges.
Selection of a starting node and destination node.
Three pathfinding choices: Dijkstra, A*, and IDA*.
Automatic calculation of the total path cost.
Step-by-step visual highlighting of the resulting route.
Ability to add a connection between two people and assign an edge weight.
Algorithm information displayed after a search, including the configured time-complexity label, completeness, and optimality.
Flask endpoints that provide graph data and handle pathfinding requests.
How the algorithms work
1. Dijkstra's Algorithm
Dijkstra's Algorithm explores the graph in increasing order of the known path cost from the starting node. It is suitable when edge weights are non-negative and does not require a heuristic.

Purpose: Establishes a shortest-path baseline.
Typical time complexity: O((V + E) log V) with an adjacency-list graph and a binary heap implementation.
Typical auxiliary space: O(V) for the priority queue and distance/visited information, in addition to the graph representation.
2. A* Search
A* evaluates a node using:

f(n) = g(n) + h(n)
Where:

g(n) is the actual cost from the start node to the current node.
h(n) is the estimated cost from the current node to the goal.
f(n) is the estimated total cost of a path through that node.
In this project, the heuristic is based on the Euclidean distance between predefined node coordinates. A priority queue is used to select the next candidate.

Purpose: Guide the search towards the destination using a heuristic.
Typical worst-case time complexity: Exponential in the search depth; commonly expressed as O(b^d) for an uninformed worst-case search-tree bound.
Typical auxiliary space: Exponential in the search depth because candidate nodes are retained in memory.
3. Iterative Deepening A* (IDA*)
IDA* combines heuristic cost evaluation with iterative deepening. It performs depth-first searches while enforcing a threshold on f(n) = g(n) + h(n). When the threshold is exceeded, the algorithm records the next smallest value to use as the threshold for another iteration.

Purpose: Find an optimal route while using less search memory than a typical A* implementation.
Typical worst-case time complexity: Exponential, commonly expressed as O(b^d).
Typical auxiliary space: O(bd) for a search tree with branching factor b and solution depth d, excluding the graph representation and implementation-specific overhead.
Here, V is the number of vertices, E is the number of edges, b is the branching factor, and d is the depth of the solution.

Complexity note: These are general theoretical characteristics, not benchmark results. Actual performance depends on the graph, edge weights, heuristic quality, and implementation. The current application displays configured time-complexity labels and the completeness/optimality properties; it does not yet measure execution time or display space complexity as live metrics.

Technology stack
Part	Technology
Backend	Python, Flask
Frontend	HTML, CSS, JavaScript
Graph visualization	vis-network
Search data structures	Python heapq
Heuristic calculation	Python math module
Communication	JSON over Flask HTTP routes
The vis-network JavaScript library is loaded from a CDN in the HTML template, so the browser needs internet access to load that script.

Project structure
CFAI-Project/
├── app.py                 # Flask application, graph data, and search algorithms
├── requirements.txt        # Python dependencies
└── templates/
    └── index.html          # User interface and interactive graph visualization
Getting started
Prerequisites
Python 3.8 or later
pip
A modern web browser
Internet access in the browser to load the vis-network CDN script
1. Clone the repository
git clone https://github.com/GirishKumar3106/CFAI-Project.git
cd CFAI-Project
2. Create a virtual environment (recommended)
Windows PowerShell:

python -m venv .venv
.venv\Scripts\Activate.ps1
Linux / macOS:

python3 -m venv .venv
source .venv/bin/activate
3. Install dependencies
pip install -r requirements.txt
4. Run the application
python app.py
Open the following address in your browser:

http://127.0.0.1:5000
The Flask application is configured to listen on port 5000.

Using the application
Open the application in your browser.
Choose a Start Person and a Target Person from the dropdowns.
Select Dijkstra Search, A Search, or IDA Search.
Click Calculate Path.
Review the total path cost and the algorithm properties shown below the graph.
Watch the route nodes and edges highlight in sequence.
To extend the network, enter two person names, specify a positive connection weight, and click Add Connection.
The initial graph is a sample weighted social network containing the people Alice, Bob, Charlie, Diana, Eve, Frank, Grace, Harry, Ivy, and Jack.

Flask routes
Method	Route	Purpose
GET	/	Renders the main page and supplies the node list to the template.
GET	/get_graph	Returns the current weighted graph as JSON.
POST	/add_connection	Adds or updates a weighted, undirected connection.
POST	/find_path	Runs the selected algorithm and returns the path, total cost, and algorithm properties.
Example: find a path
POST /find_path

{
  "start": "Alice",
  "end": "Ivy",
  "algorithm": "astar"
}
Supported algorithm values:

dijkstra
astar
idastar
The response contains the path, its total cost, and the configured algorithm properties.

Example: add a connection
POST /add_connection

{
  "person1": "Alice",
  "person2": "Ivy",
  "weight": 3
}
The connection is added in both directions, so the graph is treated as undirected.

Current implementation notes
The graph is stored in the Flask application's Python memory. Connections added through the interface are not saved to a database or file, so they are reset when the application process restarts.
A* and IDA* use predefined coordinates for the original sample nodes. Newly added nodes do not receive custom coordinates automatically; the heuristic function falls back to (0, 0) for nodes without coordinates.
The interface reports theoretical/configured algorithm properties. It does not currently run a controlled benchmark, record elapsed execution time, or show measured memory consumption.
The graph uses positive weights in the provided sample and the interface's weight input is intended for positive values.
Possible future improvements
Add measured execution-time comparisons across the algorithms.
Display theoretical and measured space usage separately.
Assign coordinates or another meaningful heuristic to newly created nodes.
Persist graph changes using SQLite or another database.
Add input validation and clearer handling for invalid or disconnected paths.
