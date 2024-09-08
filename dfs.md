- dfs can be in two types of data traversal
    -- either for tree, or for graphs
        -- what is the difference for trees & graphs? -> graphs can contain cycles, whereas trees cannot
            -- graphs can be disconnected, whether trees are always connected

-- dfs (Graphs case)
    - as graphs can contain cycles, a node can be visited multiple times, so to remove that we have to denote a visited or non-visited list for the nodes. Also a graph can have more than one dfs traversal.


0--------1
| \
|  \
|   2
|  /  \
| /    \
3       4

algorithm steps -
1. visit a node put it into the visited list
2. put the visited nodes adjacent nodes to a stack
3. pop node from top of stack and repeat the process from step 1.


c++ code
```
#include<bits/stdc++.h>
using namespace std;

void addEdges(vector<vector<int>> &graphList, int firstVertex, int secondVertex){
    graphList[firstVertex].push_back(secondVertex);
    graphList[secondVertex].push_back(firstVextex);
}

void dfsCall(vector<vector<int>> &graphList, vector<bool> &visitedList, int source){
    visitedList[source] = true;
    cout << source << " "<< endl;

    for(auto item: graphList[source]){
        if(visitedList[item] == false)
            dfsCall(graphList, visitedList, item);
    }
}

void dfsAlgo(vector<vector<int>> &graphList, int source){
    vector<bool> visitedList(graphList.size(), false);

    dfsCall(graphList, visitedList, source);
}

int main()
{
    int numOfVertices = 5;

    vector<vector<int>> graphList(numOfVertices);

    vector<vector<int>> graphEdges = {{0, 1}, {0, 2}, {0, 3}, {2, 3}, {2, 4}};

    for(auto &edge: graphEdges)
        addEdges(graphList, edge[0], edge[1]);

    int sourceVertex = 0;

    cout << "DFS source: " << sourceVertex << endl;

    dfsAlgo(graphList, sourceVertex);
}

```

