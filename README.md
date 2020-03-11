# Relay-Node-placement-for-Maximal-Connectedness
Relay Node Placement Problem with Minimum Number of Connected Components

The study of this problem is conducted in a scenario where a number of sensors
(nodes) have been placed in a deployment area and often the objective is to
place the fewest number of relay nodes in the deployment area such that the
resulting network comprising of sensor and relay nodes is connected.
Research paper used for reference:

*A. Mazumder, C. Zhou, A. Das and A. Sen, "Budget Constrained Relay
Node Placement Problem for Maximal \Connectedness"", MILCOM 2016.*

Analyze the Budget Constrained Relay node Place-
ment with Minimum Number of Connected Components(BCRP-MNCC) prob-
lem and implement the algorithm.
Analyze the Budget Constrained Relay node Placement for Maximizing the Largest Con-
nected Component(BCRP-MLCC) problem and implement the algorithm.

**PROBLEM FORMULATION**


Budget Constrained Relay Node Placement with Minimum Number of Connected Components (BCRP-MNCC)


Given the locations of n sensor nodes in the Euclidean plane,
P = {p1, p2, . . . , pn}, positive integers C, R as communication range of sensor nodes and relay nodes, and a budget B1 on the number of available relay nodes. Objective is to find a subset of Q = {q1, q2, . . . , q|B1|} points, in the same plane where relay nodes can be deployed, so that the number of connected components in the graph G0 = (V 0 , E0 ) corresponding to the point set P and Q is at most C.

Budget Constrained Relay Node Placement with Maximum size of Largest Connected Component (BCRP-MLCC)


Given the locations of n sensor nodes in the Euclidean plane P = {p1, p2, . . . , pn}, positive integer C, R as communication range of sensor nodes and relay nodes and a budget B2 on the number of available relay nodes. Objective is to find a subset of Q = {q1, q2, . . . , q|B2|} points in the same plane where relay nodes can be deployed, so that the size of the largest connected component in the graph G0 = (V 0 , E0 ) corresponding to the point set P and Q is at least C.

**PROBLEM SOLUTION**


(1) Solution for BCRP-MNCC


One way to find a graph with high level of connectedness is to create a complete graph for given terminal nodes. Using this graph, we construct a MST T’ and assign a weight to every edge based on the Euclidean distance between the two edges of the node. The weight of an edge represents the number of relay nodes required to connect two nodes of the edge. Using this information, we evaluate every edge and compare it with the range R of the nodes. If the length of the nodes is greater than R, we will have to assign a relay node for successful connection else we know that the nodes are connected. Very likely, the number of edges that require relay nodes may exceed the number of relay nodes available ‘B’. To deal with this shortage, we remove edges from the tree with maximum weights until the demand - supply is met. The resultant tree is the highly connected graph as per definition [1]
Prim’s algorithm for minimum spanning tree
Prim’s algorithm is a Greedy algorithm that starts with an empty tree and vertices are added one by one on finding the closest vertex. To start with, we select a vertex randomly and add it to MST. Then, at every step we create a candidate set of vertices that are connected to nodes in MST and select the one with minimum weight. The selected node is added to MST. We repeat this until all nodes of the graph are added to the tree.
The idea behind Minimum spanning tree is to connect two disjoint subsets using a parameter (weighted edge in our case).


Algorithm:


Step 1: For given terminal points, construct a Minimum Spanning Tree T’.


Step 2: For each edge E of T’ assign weight using: Weight = ceil (length(E)/R) - 1


Step 3: If sum of weight of all edges > Available relay nodes, (ie. budget is lesser than required nodes) goto step 4. Else goto step 5.


Step 4: Using greedy approach find edge with maximum weight in T’ and remove it. Goto Step 3.


Step 5: Return resulting T’


(2) Solution for BCRP-MLCC:


As the name suggests, BCRP-MLCC problem tries to maximise the largest connected component in the graph. To achieve this, we need to compute a minimum spanning tree for a subgraph that connects k vertices at the least (initially k= the number of terminal points). This is equivalent to the k-Minimum Spanning Tree problem. The weights of the edges in the resulting k-MST are calculated as: ceil(length(E)/R) - 1. The length of the edge between two terminal points (length(E)) is the measure of the number of relay nodes that are required to connect the two sensors at the end of this edge. If the number of relay nodes required for this k-MST comes out to be less than the budget, then we have found our solution for the problem. Otherwise, we decrement the value of k and compute another k-MST until we find our solution.


To compute k-MST:


It is known that finding the optimal solution for k-MST is NP-hard as its computational complexity is very high. As a workaround, we use an approximation algorithm to solve this problem. An approximation algorithm will provide a solution to the k-MST problem in polynomial time, but this solution will not necessarily be the optimal solution.


k-MST using Branch and Bound:


The Branch and bound algorithm considers all possible set of candidate solutions and discards them based on the lower and upper bound of the evaluation parameter. In our case, this parameter is evaluated using ceil(length(E)/R) – 1, and all candidates whose sum exceed the budget of relay nodes are discarded.


Algorithm:


Step 1: Set the value for k equal to n (the number of terminal points).


Step 2: For a subgraph G’ with k terminal points, construct an approximate k-Minimum Spanning Tree


Step 3: For each edge E of G’ assign weights to the edges using: Weight = ceil(length(E)/R) - 1


Step 4: If the sum of weight of all edges <= Available relay nodes, (ie. the required number of relay nodes are less than the budget) go 
to step 6. Else go to step 5.


Step 5: If k=2, go to step 7. Else, decrement k by 1 and go to step 2.


Step 6: Return this k-MST as the solution for the BCRP-MLCC problem and terminate.


Step 7: Return any random sensor point as solution.


INPUT FORMAT


Code expects file path as input.
Details on file content and input pattern is as below:


For BCRP-MNCC:


11        //Number of nodes in graph


300       //Value of R


4         //Value of B


0 1 1000  //node1 node2 length


0 2 1000  //node2 node5 length


0 3 1000


. .


. .       //nodei nodej length



For BCRP-MLCC
11        //Number of nodes in graph
300       //Value of R
4         //Value of B
0 1 1000  //node1 node2 length
0 2 1000  //node2 node5 length
0 3 1000
. .
. .       //nodei nodej length


CODE EXECUTION STEPS
Programming Language – Python
For BCRP-MNCC:
execute command:
python Algorithm4.py
enter the path for the input file provided
For BCRP-MLCC:
execute command:
python Algorithm5.py
enter the path for the input file provided

OUTPUT


