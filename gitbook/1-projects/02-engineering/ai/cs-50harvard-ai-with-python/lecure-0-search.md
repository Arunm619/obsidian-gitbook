examples
- Maze problem
- Map problem
- Games

agent 
- Entity that perceives its environment and acts upon that environment

state 
- a configuration of the agent in its environment

initial state 
- the state in which the agent begins

actions
- choices that can be made in a state
- `ACTIONS(s)` represent the set of actions that can be executed in state s.

transition model
- a description of what state results from performing any applicable action in any state
- `RESULT(s,a)` returns the state resulting from performing action a in state s.

state space 
- the set of all states reachable from the initial state by any sequence of actions
- representation as a graph - some sequences of nodes (states) and edges (actions).

goal test
- way to determine whether a given state is a goal state

path cost 
- numerical cost associated with a given path

optimal solution
 - solution that has the lowest path cost among all solutions


Search problems 
- initial state
- actions
- transition model
- goal test
- path cost function

Modelling the search problem in the program

node 
 a data structure that keeps track of 
 - a state 
 - a parent (node that generated this node)
 - an action (action applied to parent to get node)
 - a path cost (from initial state to node)

**approach** 
- start with a frontier that contains the initial state
- repeat: 
	- if the frontier is empty, then no solution.
	- remove a node from the frontier.
	- if node contains goal state, return the solution.
	- expand node, add resulting nodes to the frontier. 
what could go wrong?
circular dependency. Keep track of visited nodes.

**revised approach**
- start with a frontier that contains the initial state
- **start with an empty explored set.**
- repeat: 
	- if the frontier is empty, then no solution.
	- remove a node from the frontier.
	- if node contains goal state, return the solution.
	- **add the node to the explored set.**
	- expand node, add resulting nodes to the frontier **if they aren't already in the frontier or the explored set.** 

best data structure for frontier ?

**stack**
**last-in first-out data type

depth-first search 
search algorithm that always expands the deepest node in the frontier


queue 
first-in first-out data type

**breadth-first search** 
search algorithm that always expands the shallowest (closest) node in the frontier


```c++
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

class Node {
public:
    int x, y;
    int distance;
    Node(int x, int y, int distance = 0) : x(x), y(y), distance(distance) {}
};

bool isValid(vector<vector<int>>& map, vector<vector<bool>>& visited, int x, int y) {
    return (x >= 0) && (x < map.size()) && (y >= 0) && (y < map[0].size()) && map[x][y] && !visited[x][y];
}

int BFS(vector<vector<int>>& map, Node& start, Node& exit) {
    int rows = map.size();
    int cols = map[0].size();
    vector<vector<bool>> visited(rows, vector<bool>(cols, false));
    queue<Node> q;
    q.push(start);

    int row[] = {-1, 0, 0, 1};
    int col[] = {0, -1, 1, 0};

    while (!q.empty()) {
        Node node = q.front();
        q.pop();

        int x = node.x;
        int y = node.y;
        int dist = node.distance;

        if (x == exit.x && y == exit.y) {
            return dist;
        }

        visited[x][y] = true;

        for (int i = 0; i < 4; i++) {
            int newX = x + row[i], newY = y + col[i];

            if (isValid(map, visited, newX, newY)) {
                q.push(Node(newX, newY, dist + 1));
            }
        }
    }

    return -1;
}

int main() {
    vector<vector<int>> map = {
        {1, 1, 1, 1, 1},
        {1, 0, 0, 1, 0},
        {0, 1, 1, 1, 1},
        {1, 1, 0, 1, 1}
    };

    Node start(0, 0);
    Node exit(3, 4);

    int result = BFS(map, start, exit);

    if (result != -1) {
        cout << "Shortest path is " << result << endl;
    } else {
        cout << "Path doesn't exist." << endl;
    }

    return 0;
}
```



```cpp 
#include <iostream>
#include <stack>
#include <vector>

using namespace std;

class Node {
public:
    int x, y;
    int distance;
    Node(int x, int y, int distance = 0) : x(x), y(y), distance(distance) {}
};

bool isValid(vector<vector<int>>& map, vector<vector<bool>>& visited, int x, int y) {
    return (x >= 0) && (x < map.size()) && (y >= 0) && (y < map[0].size()) && map[x][y] && !visited[x][y];
}

int DFS(vector<vector<int>>& map, Node& start, Node& exit) {
    int rows = map.size();
    int cols = map[0].size();
    vector<vector<bool>> visited(rows, vector<bool>(cols, false));
    stack<Node> s;
    s.push(start);

    int rowDirection[] = {-1, 0, 0, 1};
    int colDirection[] = {0, -1, 1, 0};

    while (!s.empty()) {
        Node node = s.top();
        s.pop();

        int x = node.x;
        int y = node.y;
        int dist = node.distance;

        if (x == exit.x && y == exit.y) {
            return dist;
        }

        visited[x][y] = true;

        for (int i = 0; i < 4; i++) {
            int newX = x + rowDirection[i], newY = y + colDirection[i];

            if (isValid(map, visited, newX, newY)) {
                s.push(Node(newX, newY, dist + 1));
            }
        }
    }

    return -1;
}

int main() {
    vector<vector<int>> map = {
        {1, 1, 1, 1, 1},
        {1, 0, 0, 1, 0},
        {0, 1, 1, 1, 1},
        {1, 1, 0, 1, 1}
    };

    Node start(0, 0);
    Node exit(3, 4);

    int result = DFS(map, start, exit);

    if (result != -1) {
        cout << "Shortest path is " << result << endl;
    } else {
        cout << "Path doesn't exist." << endl;
    }

    return 0;
}
```


Let's analyze the time and space complexity of both the Breadth-First Search (BFS) and Depth-First Search (DFS) algorithms in the provided implementation.

1. **Breadth-First Search (BFS):**

   - **Time Complexity:** The time complexity of BFS is O(V + E), where V is the number of vertices and E is the number of edges in the graph. In the worst-case scenario, we might have to visit all the vertices and edges of the graph once. In the context of the provided implementation, where the graph is represented as a 2D grid (matrix), the time complexity is O(rows * cols) as each cell in the matrix is visited once.

   - **Space Complexity:** The space complexity of BFS is O(V), where V is the number of vertices. This is because in the worst-case scenario, all the vertices could end up in the queue at the same time. In the context of the provided implementation, the space complexity is O(rows * cols) as in the worst case, all cells might end up in the queue.

2. **Depth-First Search (DFS):**

   - **Time Complexity:** The time complexity of DFS is also O(V + E), where V is the number of vertices and E is the number of edges in the graph. Similar to BFS, in the worst-case scenario, we might have to visit all the vertices and edges of the graph once. In the context of the provided implementation, where the graph is represented as a 2D grid (matrix), the time complexity is O(rows * cols) as each cell in the matrix is visited once.

   - **Space Complexity:** The space complexity of DFS is O(V), where V is the number of vertices. This is because in the worst-case scenario, all the vertices could end up in the stack at the same time. In the context of the provided implementation, the space complexity is O(rows * cols) as in the worst case, all cells might end up in the stack.


```
shallow | ˈʃaləʊ | 
adjective 
1) of little depth: serve the noodles in a shallow bowl | being fairly shallow, the water was warm.
• situated at no great depth: the shallow bed of the North Sea.


2) not exhibiting, requiring, or capable of serious thought: a shallow analysis of contemporary society.
```

BFS is pretty good in finding optimal solution. 
But it depends on the size of the state space.
because it can exhaustively explore all the states.

**uninformed search** 
search strategy that uses no problem-specific knowledge

eg. DFS, BFS didn't care about the structure. No heuristics. 

**informed search**
search strategy that uses problem-specific knowledge to find solutions more efficiently

eg. greedy best-first search 

DFS - Deepest node first
BFS - Shallowest node first

greedy best-first search

search algorithm that expands the node that is closest to the goal, as estimated by a heuristic function h(n)

heuristic 
- estimating whether or not we are closer to the goal.
- attempt to try to approximate

**Manhattan distance** is a distance measure that is calculated by taking the sum of distances between the _x_ and _y_ coordinates.

The Manhattan distance is also known as _Manhattan length_. In other words, it is the distance between two points measured along axes at right angles.

Manhattan distance works very well for high-dimensional datasets. As it does not take any squares, it does not amplify the differences between any of the features. It also does not ignore any features.


greedy - maximise at local decision points, not at global 

A* search
search algorithm that expands node with lowest value of g(n) + h(n)

g(n) = cost to reach node
h(n) = estimated cost to goal

A* search
optimal if 
- h(n) is admissible (never overestimates the true cost), and
- h(n) is consistent (for every node n and successor n' with step cost c, h(n) <= h(n') + c)

---

Adversarial search 

Now there are two agents. 
Eg. TicTacToe with AI
There is adversary that tries to win and oppose me.

Minimax 
- deterministic two-player game
- -1 (O wins), 0 (draw), 1 (X wins)
- MAX(X) aims to maximise score
- MIN(O) aims to minimise score

Game
- S0 - Initial state
- PLAYER(S) = returns which player to move in state S
- ACTIONS(S) = returns legal moves in state s
- RESULT(S, a) = returns state after action a taken in state S
- TERMINAL(S) = checks if state S is a terminal state
- UTILITY(S) - final numerical value for a terminal state S

Minimax
- Given a state S
	- MAX picks action a in ACTION(S) that produces highest value of MIN-VALUE(RESULT(S,a)) 
	- MIN picks action a in ACTION(S) that produces lowest value of MAX-VALUE(RESULT(S,a)) 

```
function MAX-VALUE(state)
	 if TERMINAL(state):
		return UTILITY(state)
	 v = -INF
	 for action in ACTIONS(state):
		v = MAX(v, MIN-VALUE(RESULT(state, action)))
	return v

function MIN-VALUE(state)
	if TERMINAL(state):
	   return UTILITY(state)
	v = INF
	for action in ACTIONS(state):
		v = MIN(v, MAX-VALUE(RESULT(state, action)))
	return v

```

Optimizations
- use less space and time?
- Thinking many levels deep and choosing is how the algo works
- The min and the max players play intelligently, so we need to be in their shoes and make decisions and then optimize from their to get our max benefit.
- This is very computation heavy!!!!

![[alpha beta pruning 2.png]]
- the algo works as usual but we make smart decisions (book keeping scores)
- if there is a 4 I can get from first choice, and while going thru the second choices' opponents choices as soon as I encounter a number <= 3 then I can quit early.
- first choice guarantees a score of 4 and the second choice can only give <=3 (3 for sure or even worse smaller than that) then we can quit that choice and move on.

![[alpha beta pruning-1.png]]

- and the third choice while looking at 2, we can say for sure our intelligent enemy would obviously optimise for their win choosing 2 or even worse anything lesser than that. So we can quit early. and return 4.
![[alpha beta pruning.png]]

This is called **Alpha-Beta pruning**
Alpha - score for booking keeping max
Beta - score for book keeping min
Pruning means removing nodes from the tree to optimize my search
Saves time!

Total possible tictactoe games
2,55,168 

Total possible chess games after four moves each
288,000,000,000 (288 billion)

Total possible chess games
10^29000 (lower bound)

Depth-Limited Minimax

Minimax is depth unlimited by default
after certain number of steps (depth), I am going to stop and not consider additional moves
Computationally untractable to cover every steps

Even after those many depth if we don't have a game over, then what do we do? One additional feature is needed.

Evaluation function
function that estimates the expected utility of the game from a given state

Evaluation function directly determines the impact of the AI game
Eg in Chess - determine the number of pieces captured and assigning a score for that.

Classical search problems 
- Google Maps
- Chess / TicTacToe


