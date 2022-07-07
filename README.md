# Lee-Algorithm

#include <iostream>
#include <queue>
#include <vector>
#include <climits>
#include <cstring>
using namespace std;
 
// A Queue Node
struct Node
{
    
    int x, y, dist;
};
 
int row[] = { -1, 0, 0, 1 };
int col[] = { 0, -1, 1, 0 };
 
bool isValid(vector<vector<int>> const &mat, vector<vector<bool>> &visited,
        int row, int col) {
    return (row >= 0 && row < mat.size()) && (col >= 0 && col < mat[0].size())
        && mat[row][col] && !visited[row][col];
}
 
int findShortestPathLength(vector<vector<int>> const &mat, pair<int, int> &src,
                    pair<int, int> &dest)
{
    if (mat.size() == 0 || mat[src.first][src.second] == 0 ||
            mat[dest.first][dest.second] == 0) {
        return -1;
    }
 
    int M = mat.size();
    int N = mat[0].size();
 
    vector<vector<bool>> visited;
    visited.resize(M, vector<bool>(N));
 
    queue<Node> q;
    
    int i = src.first;
    int j = src.second;
   
    visited[i][j] = true;
    q.push({i, j, 0});
 
    int min_dist = INT_MAX;
 
    while (!q.empty())
    {
        Node node = q.front();
        q.pop();
 
        int i = node.x, j = node.y, dist = node.dist;
 
        if (i == dest.first && j == dest.second)
        {
            min_dist = dist;
            break;
        }
 
        for (int k = 0; k < 4; k++)
        {
            if (isValid(mat, visited, i + row[k], j + col[k]))
            {
                visited[i + row[k]][j + col[k]] = true;
                q.push({ i + row[k], j + col[k], dist + 1 });
            }
        }
    }
 
    if (min_dist != INT_MAX) {
        return min_dist;
    }
 
    return -1;
}
 
int main()
{
    vector<vector<int>> mat =
    {
        { 1, 1, 1, 1, 1, 0, 0, 1, 1, 1 },
        { 0, 1, 1, 1, 1, 1, 0, 1, 0, 1 },
        { 0, 0, 1, 0, 1, 1, 1, 0, 0, 1 },
        { 1, 0, 1, 1, 1, 0, 1, 1, 0, 1 },
        { 0, 0, 0, 1, 0, 0, 0, 1, 0, 1 },
        { 1, 0, 1, 1, 1, 0, 0, 1, 1, 0 },
        { 0, 0, 0, 0, 1, 0, 0, 1, 0, 1 },
        { 0, 1, 1, 1, 1, 1, 1, 1, 0, 0 },
        { 1, 1, 1, 1, 1, 0, 0, 1, 1, 1 },
        { 0, 0, 1, 0, 0, 1, 1, 0, 0, 1 },
    };
 
    pair<int, int> src = make_pair(0, 0);
    pair<int, int> dest = make_pair(7, 5);
 
    int min_dist = findShortestPathLength(mat, src, dest);
    if (min_dist != -1)
    {
        cout << "The shortest path from source to destination "
                "has length " << min_dist;
    }
    else {
        cout << "Destination cannot be reached from a given source";
    }
 
    return 0;
}

#by python

mport sys
from collections import deque
 

row = [-1, 0, 0, 1]
col = [0, -1, 1, 0]
 
 

def isValid(mat, visited, row, col):
    return (row >= 0) and (row < len(mat)) and (col >= 0) and (col < len(mat[0])) \
           and mat[row][col] == 1 and not visited[row][col]
 
 

def findShortestPathLength(mat, src, dest):
 
  
    i, j = src
 
   
    x, y = dest
 
   
    if not mat or len(mat) == 0 or mat[i][j] == 0 or mat[x][y] == 0:
        return -1
 
  
    (M, N) = (len(mat), len(mat[0]))
 
   
    visited = [[False for x in range(N)] for y in range(M)]
 
    
    q = deque()
 
   
    visited[i][j] = True
 
  
    # minimum distance from the source
    q.append((i, j, 0))
 
  
    min_dist = sys.maxsize
 
    # loop till queue is empty
    while q:
 
        # dequeue front node and process it
        (i, j, dist) = q.popleft()
 
        # (i, j) represents a current cell, and `dist` stores its
        # minimum distance from the source
 
        # if the destination is found, update `min_dist` and stop
        if i == x and j == y:
            min_dist = dist
            break
 
      
        for k in range(4):
            # check if it is possible to go to position
            # (i + row[k], j + col[k]) from current position
            if isValid(mat, visited, i + row[k], j + col[k]):
                # mark next cell as visited and enqueue it
                visited[i + row[k]][j + col[k]] = True
                q.append((i + row[k], j + col[k], dist + 1))
 
    if min_dist != sys.maxsize:
        return min_dist
    else:
        return -1
 
 
if __name__ == '__main__':
 
    mat = [
        [1, 1, 1, 1, 1, 0, 0, 1, 1, 1],
        [0, 1, 1, 1, 1, 1, 0, 1, 0, 1],
        [0, 0, 1, 0, 1, 1, 1, 0, 0, 1],
        [1, 0, 1, 1, 1, 0, 1, 1, 0, 1],
        [0, 0, 0, 1, 0, 0, 0, 1, 0, 1],
        [1, 0, 1, 1, 1, 0, 0, 1, 1, 0],
        [0, 0, 0, 0, 1, 0, 0, 1, 0, 1],
        [0, 1, 1, 1, 1, 1, 1, 1, 0, 0],
        [1, 1, 1, 1, 1, 0, 0, 1, 1, 1],
        [0, 0, 1, 0, 0, 1, 1, 0, 0, 1]
    ]
 
    src = (0, 0)
    dest = (7, 5)
 
    min_dist = findShortestPathLength(mat, src, dest)
 
    if min_dist != -1:
        print("The shortest path from source to destination has length", min_dist)
    else:
        print("Destination cannot be reached from source")
