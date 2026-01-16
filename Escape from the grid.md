[Escape from grid | Practice Problems](https://www.hackerearth.com/practice/algorithms/graphs/breadth-first-search/practice-problems/algorithm/escape-from-grid-google-ff752cb1/)

## Problem Statement

Assume that you are given a two-dimensional grid $G$ that contains $N$ rows and $M$ columns. The grid $G$ consists of only three integers: 0, 1, and 2.

- **0** denotes an empty cell
- **1** denotes that a cell contains a plant
- **2** denotes a cell where you are standing initially12
    

You can move into an adjacent cell if that adjacent cell is empty. Two cells are adjacent if they share a side. In other words, if a cell is empty, then you can move in one of the four3 directions: **Up, Down, Left, and Rig4ht**. You cannot move out of the grid $G$.

Your task is to find the length of the shortest path to reach one of the **boundary edges** of the grid without stepping on a plant. The length of a path is equal to the number of moves you make.56

**Note:** It is guaranteed that there is only one cell with value 2 (you are standing in only one cell initiall7y).8

---

### Input Format9

- First line: Two space-separated integers, $N$ and $M$, denoting the number of rows and columns in the grid $G$ respectively.
    
- Next $N$ lines: $M$ space-separated integers denoting the rows of the grid $G$.
    

### Output Format

Print the length of the shortest path to reach one of the boundary edges of the grid without stepping on a plant. If it is not possible to reach the edge of the grid, then print **-1**.

---

### Constraints

- $1 \le N, M \le 100$
    
- $0 \le G_{i,j} \le 2$ where $G_{i,j}$ denotes a cell of the $G$ grid
    

---

### Sample Input & Output

| **Sample Input**                                                  | **Sample Output** |
| ----------------------------------------------------------------- | ----------------- |
| `4 5`<br>`1 1 1 0 1`<br>`1 0 2 0 1`<br>`0 0 1 0 1`<br>`1 0 1 1 0` | `2`               |

---

### Explanation10

There are 4 rows and 5 columns in the grid.11

```
1 1 1 0 1
1 0 2 0 1
0 0 1 0 1
1 0 1 1 0
```

Initially, you are standing at cell 12$(2, 3)$ (second row and third column) denoted by 2. There are three ways t13o reach a boundary edge of the grid without stepping on a plant:141516

- Move to cell 171819$(2, 2)$ (Left), then move to cell 202122$(3, 2)$ (Down) and then move to cell 232425$(4, 2)$ (Down) (**3 steps**).262728
    
- Move to cell 293031$(2, 2)$ (Left), then move to cell 323334$(3, 2)$ (Down) and then move to cell 353637$(3, 1)$ (Left) 38(**3 steps**).3940
    
- Move to cell 4142$(2, 4)$ (Right) and then move to cell 4344$(1, 4)$ (Up) (45**2 steps**).46
    
In t47he third case, we took only **2 steps** to reach the edge of the grid, which is the shortest path.


```c++
#include <iostream>
#include <queue>

using namespace std;
const int MAX = 1e3 + 5;
int grid[MAX][MAX], dist[MAX][MAX], n, m;
bool vis[MAX][MAX];
int dr[] = {0, 0, -1, 1};
int dc[] = {-1, 1, 0, 0};

int bfs(int fromX, int fromY)
{
    queue <pair<int, int> > q;
    pair <int, int> p;
    dist[fromX][fromY] = 0;
    q.push({fromX, fromY});
    while(!q.empty())
    {
        p = q.front();
        q.pop();
        fromX = p.first;
        fromY = p.second;
        if(fromX == 0 or fromX == n-1 or fromY == 0 or fromY == m-1)
            return dist[fromX][fromY];
        for(int i = 0;i < 4;++i)
        {
            int x = fromX + dr[i];
            int y = fromY + dc[i];
            if(x >= 0 and x < n and y >= 0 and y < m and grid[x][y] != 1 and vis[x][y] == false)
            {
                vis[x][y] = true;
                dist[x][y] = dist[fromX][fromY] + 1;
                q.push({x, y});
            }
        }
    }
    return -1;

}

int main()
{
    int ans, x, y;
    cin >> n >> m;
    for(int i = 0;i < n;++i) for(int j = 0;j < m;++j)
    {
        cin >> grid[i][j];
        vis[i][j] = false;
        dist[i][j] = 0;
        if(grid[i][j] == 2)
            x = i, y = j;
    }
    ans = bfs(x, y);
    cout << ans << endl;
    return 0;
}
```

