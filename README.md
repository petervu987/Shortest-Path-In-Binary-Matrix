# Shortest-Path-In-Binary-Matrix

class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        int n = grid.size();

        if (grid[0][0] == 1 || grid[n-1][n-1] == 1) {
            return -1;
        }

        vector<pair<int,int>> ds = {
            {1,0}, {-1,0}, {0,1}, {0,-1},
            {1,1}, {1,-1}, {-1,1}, {-1,-1}
        };
        
        queue<pair<int,int>> q;
        q.push({0, 0});
        grid[0][0] = 1;

        while (!q.empty()) {
            auto [r, c] = q.front();
            q.pop();
            int dt = grid[r][c];

            if (r == n-1 && c == n-1)
                return dt;

            for (auto& d : ds) {
                int nr = r + d.first;
                int nc = c + d.second;

                if (nr >= 0 && nc >= 0 && nr < n && nc < n && grid[nr][nc] == 0) {
                    grid[nr][nc] = dt + 1;
                    q.push({nr, nc});
                }
            }
        }

        return -1;  
    }
};
