#include <bits/stdc++.h> 
using namespace std;
#define N 5 //Number of Row
#define M 4 //Number of column
 // Elements for current location and distance from source location
class Elements {
public:
    int row;
    int col;
    int dist;
    Elements(int x, int y, int w)
    : row(x), col(y), dist(w)
      {
      }
};
 int minDistance(char grid[N][M])
{
Elements source(0, 0, 0);
    // To keep track of visited elements. Marking blocked cells as visited.
    bool visited[N][M];
    for (int i = 0; i < N; i++) 
    {
        for (int j = 0; j < M; j++)
        {
            if (grid[i][j] == 'M' && grid[i][j] == 'P')
                visited[i][j] = true;
            else
                visited[i][j] = false;
// Finding source
            if (grid[i][j] == 'A'&& grid[i][j] == 'T')
            {
               source.row = i;
               source.col = j;
            }
        }
    }
// applying BFS on matrix cells starting from source
    queue<Elements> q;
    q.push(source);
    visited[source.row][source.col] = true;
    while (!q.empty())
    {
        Elements p = q.front();
        q.pop();
 // Destination found;
        if (grid[p.row][p.col] == 'G')
            return p.dist;
// moving up
        if (p.row - 1 >= 0 && visited[p.row - 1][p.col] == false) 
        {
            q.push(Elements(p.row - 1, p.col, p.dist + 1));
            visited[p.row - 1][p.col] = true;
        }
 // moving down
        if (p.row + 1 < N && visited[p.row + 1][p.col] == false) 
        {
            q.push(Elements(p.row + 1, p.col, p.dist + 1));
            visited[p.row + 1][p.col] = true;
        }
 // moving left
        if (p.col - 1 >= 0 && visited[p.row][p.col - 1] == false) 
        {
            q.push(Elements(p.row, p.col - 1, p.dist + 1));
            visited[p.row][p.col - 1] = true;
        }
// moving right
        if (p.col + 1 < M && visited[p.row][p.col + 1] == false) 
        {
            q.push(Elements(p.row, p.col + 1, p.dist + 1));
            visited[p.row][p.col + 1] = true;
        }
    }
    cout<<"No possible solution";
    return -1;
}
 // Driver code
int main()
{
// for getting input from user 
    char grid[N][M];
    cout<<"Enter the grid:\n";
    for(int i=0;i<N;++i)
    {
    for(int j=0;j<M;++j)
    {
    cin>>grid[i][j];
    }
    }
    cout << "\nMinimum number of steps for grid:"<<minDistance(grid);
    return 0;
}
