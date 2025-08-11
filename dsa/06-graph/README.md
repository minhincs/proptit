# Graph 
## 1. Các khái niệm cơ bản của đồ thị
### 1.1. Định nghĩa cơ bản của đồ thị
- Đồ thị (graph) là một kiểu cấu trúc dữ liệu gồm đỉnh (vertices) và cạn (edges) nối giữa các đỉnh đó
- Kí hiệu: $G = (V.E)$
	- $V$ là tập các đỉnh 
	- $E$ là tập các cạnh 

#### 1.1.1. Đơn đồ thị
- Không có khuyên (cạnh nối 1 đỉnh với chính nó)
- Không có cạnh song song (nhiều cạnh nối cùng 1 đỉnh)

>[!NOTE]
>```
>A --- B
>|     |
>C --- D
>```
>Các cạnh: $(A, B), (A, C), (B, D), (C, D)$

#### 1.1.2. Đa đồ thị
Có nhiều cạnh song song hoặc khuyên

>[!NOTE]
>```
>A == B (2 cạnh song song)
>A -- A (khuyên)
>```

#### 1.1.3. Đồ thị có hướng
- Mỗi cạnh được biểu diễn bởi một mũi tên 
- Thứ tự viết quan trọng: $(U, V) \neq (V, U)$ 

>[!NOTE]
>```
>A -> B -> C
>```

#### 1.1.4. Đồ thị vô hướng
- Các cạnh không có hướng
- $(U, V) = (V, U)$  

### 1.2. Các khái niệm cơ bản
- **Cạnh liên thuộc**: cạnh nối giữa hai đỉnh
- **Khuyên (loop)**: cạnh nối 1 đỉnh với chính nó
- **Đỉnh kề (adjacent vertices)**: hai đỉnh có chung 1 cạnh
- **Bậc (degree)**: số cạnh tương ứng với đỉnh đó 

>[!WARNING]
>Với đồ thị có hướng: 
>- **Bậc vào (in-degree)**: số cạnh đi vào đỉnh
>- **Bậc ra (out-degree)**: số cạnh đi ra từ đỉnh

### 1.3. Ví dụ thực tế
- Mạng xã hội: đỉnh là người dùng, cạnh là các mối quan hệ
- Bản đồ giao thông: đỉnh là các giao lộ, cạnh là đường 

## 2. Biểu diễn đồ thị trên máy tính
Có nhiều cách lưu trữ đồ thị, ba cách phổ biến nhất là:
- Ma trận kề (Adjacency Matrix)
- Danh sách kề (Adjacency List)
- Danh sách cạnh (Edge List)

### 2.1. Ma trận kề
- Dùng ma trận $n \times n$ với $n$ là số đỉnh
- Với mối truy vấn $[i][j]$ nhận 1 trong 2 giá trị:
	- `1`: nếu có cạnh từ đỉnh $i$ đến đỉnh $j$
	- `0`: nếu không có cạnh từ đỉnh $i$ đến đỉnh $j$
- Với đồ thị có hướng: ma trận không đối xứng
- Với đồ thị vô hướng: ma trận đối xứng

>[!NOTE]
>```
>[ 0 1 1 ]
>[ 1 0 1 ]
>[ 1 1 0 ]
>```

### 2.2. Danh sách kề
Mỗi đỉnh lưu lại danh sách các đỉnh kề với nó

>[!NOTE]
>```
>0: 1, 2
>1: 0, 2
>2: 0, 1
>```

### 2.3. Danh sách con
Lưu lại danh sách các cặp $(u, v)$ biểu diễn các cạnh 

>[!NOTE]
>```
>[(0, 1), (0, 2), (1, 2)]
>```

### 2.4. Ưu / Nhược điểm của các cách biểu diễn
| Cách biểu diễn | Ma trận kề                                                | Danh sách kề                                                         | Danh sách cạnh                     |
| -------------- | --------------------------------------------------------- | -------------------------------------------------------------------- | ---------------------------------- |
| **Ưu điểm**    | Truy vấn kiểm tra có cạnh giữa hai đỉnh rất nhanh: $O(1)$ | Tiết kiệm bộ nhớ với đồ thị thưa<br>Duyệt đỉnh kề nhanh              | Gọn, dễ duyệt toàn bộ cạnh         |
| **Nhược điểm** | Tốn bộ nhớ: $O(n^2)$                                      | Kiểm tra xem có cạnh giữa 2 đỉnh không tốn $O(k)$, $k$ là số đỉnh kề | Khó truy vấn hoặc tìm đỉnh liền kề |

## 3. Các thuật toán tìm kiếm trên đồ thị
### 3.1. Khái niệm cơ bản
- **Đường đi**: dãy các đỉnh nối liên tiếp bởi cạnh.
- **Chu trình**: đường đi mà đỉnh đầu trùng với đỉnh cuối.
- **Đường đi đơn**: đường đi không lặp lại đỉnh.
- **Chu trình đơn**: chu trình không lặp lại đỉnh (trừ đỉnh đầu/cuối).

### 3.2. DFS - Depth First Search
- Tìm kiếm theo chiều sâu 
- Bắt đầu từ 1 đỉnh, đi càng sâu càng tốt theo 1 nhánh, khi không thể đi nữa thì quay lại đỉnh phía trước và tiếp tục như thế
- Ứng dụng: tìm thành phần liên thông, kiểm tra chu trình, giải bài toán mê cung, tìm đường đi,...
- Độ phức tạp: $O(V + E)$

#### 3.2.1. Cài đặt DFS theo đệ quy
```cpp
void dfs_rec(int u, const vector<vector<int>>& adj, vector<char>& vis) {
    vis[u] = 1;
    cout << u << " ";
    for (int v : adj[u]) {
        if (!vis[v]) dfs_rec(v, adj, vis);
    }
}
```

#### 3.2.2. Cài đặt DFS không đệ quy (stack)
```cpp
void dfs_iter(int start, const vector<vector<int>>& adj) {
    int n = adj.size();
    vector<char> vis(n, 0);
    vector<int> st;
    st.push_back(start);
    while (!st.empty()) {
        int u = st.back(); st.pop_back();
        if (vis[u]) continue;
        vis[u] = 1;
        cout << u << " ";
        // để giữ thứ tự tương tự đệ quy, ta push theo reversed order
        for (auto it = adj[u].rbegin(); it != adj[u].rend(); ++it) {
            if (!vis[*it]) st.push_back(*it);
        }
    }
}
```

### 3.3. BFS - Breadth First Search
- Tìm kiếm theo chiều rộng
- Bắt đầu từ 1 đỉnh, duyệt tất cả các đỉnh kề trước khi sang lớp tiếp theo
- Ứng dụng: tìm đường đi ngắn nhất trong đồ thị không trọng số, tìm thành phần liên thông, thuật toán "loang",...
- Độ phức tạp: $O(V + E)$ 

#### 3.3.1. Thuật toán "loang" - flood fill
- Là một biến thể của DFS/BFS dùng để "lan truyền" từ một ô ban đầu sang các ô kế tiếp theo một điều kiện nào đó
- Ví dụ: công cụ **Bucket** trong các phần mềm vẽ, thiết kế
- Nguyên tắc hoạt động:
	1. Chọn 1 ô bắt đầu 
	2. Nếu ô đó có giá trị thỏa mãn điều kiện (VD: cùng màu với ô ban đầu) thì thực hiện loang, đổi giá trị cũ sang giá trị mới
	3. Lan ra các ô kề, lặp lại cho đến khi kết thúc

##### 3.3.1.1. Cài đặt thuật toán loang bằng DFS
(Code tham khảo từ [geeksforgeeks](https://www.geeksforgeeks.org/dsa/flood-fill-algorithm/))
```cpp
#include <iostream>
#include <vector>
using namespace std;

// Helper function for Depth-First Search (DFS)
void dfs(vector<vector<int>>& image, int x, 
         int y, int oldColor, int newColor) {
    
    // Base case: check boundary conditions and color mismatch
    if (x < 0 || x >= image.size() || 
        y < 0 || y >= image[0].size() || 
        image[x][y] != oldColor) {
    // Backtrack if pixel is out of bounds or color doesn't match
        return; 
    }

    // Update the color of the current pixel
    image[x][y] = newColor;

    // Recursively visit all 4 connected neighbors
    dfs(image, x + 1, y, oldColor, newColor); 
    dfs(image, x - 1, y, oldColor, newColor); 
    dfs(image, x, y + 1, oldColor, newColor); 
    dfs(image, x, y - 1, oldColor, newColor); 
}

// Main flood fill function
vector<vector<int>> floodFill(
    vector<vector<int>>& image, int sr, 
    int sc, int newColor) {

    // If the starting pixel already has the new color,
    // no changes are needed
    if (image[sr][sc] == newColor) {
        return image;
    }

    // Call DFS to start filling from the source pixel
    int oldColor = image[sr][sc]; // Store original color
    dfs(image, sr, sc, oldColor, newColor);

    return image; // Return the updated image
}

// Driver code to test the flood fill function
int main() {
    // Input image (2D grid)
    vector<vector<int>> image = {
        {1, 1, 1, 0},
        {0, 1, 1, 1},
        {1, 0, 1, 1}
    };
    
    // Starting pixel (row, col)
    int sr = 1, sc = 2;
    
    // New color to apply
    int newColor = 2;        

    // Perform flood fill and get the result
    vector<vector<int>> result = floodFill(image, sr, sc, newColor);

    // Print the updated image
    for (auto& row : result) {
        for (auto& pixel : row) {
            cout << pixel << " ";
        }
        cout << "\n";
    }
    return 0;
}
```
- Độ phức tạp: $O(m.n)$

##### 3.3.1.2. Cài đặt thuật toán loang bằng BFS
(Code tham khảo từ [geeksforgeeks](https://www.geeksforgeeks.org/dsa/flood-fill-algorithm/))
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

vector<vector<int>> floodFill(
    vector<vector<int>>& image, int sr, 
    int sc, int newColor) {

    // If the starting pixel already has the new color
    if (image[sr][sc] == newColor) {
        return image;
    }

    // Direction vectors for traversing 4 directions
    vector<pair<int, int>> directions = {
        {1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    
    // Initialize the queue for BFS
    queue<pair<int, int>> q;
    int oldColor = image[sr][sc];
    q.push({sr, sc});
    
    // Change the color of the starting pixel
    image[sr][sc] = newColor;

    // Perform BFS
    while (!q.empty()) {
        pair<int, int> front = q.front();
        int x = front.first, y = front.second;
        q.pop();
        
        // Traverse all 4 directions
        for (const pair<int, int>& direction : directions) {
            int nx = x + direction.first;
            int ny = y + direction.second;
            
            // Check boundary conditions and color match
            if (nx >= 0 && nx < image.size() && 
                ny >= 0 && ny < image[0].size() && 
                image[nx][ny] == oldColor) {
                
                // Change the color and enqueue
                image[nx][ny] = newColor;
                q.push({nx, ny});
            }
        }
    }

    return image;
}

int main() {
    
    // Define the input 2D image (grid of pixel colors)
    vector<vector<int>> image = {
        {1, 1, 1, 0},
        {0, 1, 1, 1},
        {1, 0, 1, 1}
    };

    // Starting pixel coordinates (row = 1, column = 2)
    int sr = 1, sc = 2;

    // New color to apply to the connected region
    int newColor = 2;

    // Call the floodFill function to perform DFS/BFS fill from the
    // starting pixel
    vector<vector<int>> result = floodFill(image, sr, sc, newColor);

    // Print the updated image after flood fill
    for (auto& row : result) {
        for (auto& pixel : row) {
            
            // Print each pixel with a space
            cout << pixel << " ";  
        }
        
        // Move to the next line after printing each row
        cout << "\n";  
    }
    
    return 0; 
}
```
- Độ phức tạp: $O(m.n)$

#### 3.3.2. Cài đặt BFS bằng queue
```cpp
vector<int> bfs(vector<vector<int>>& adj)  {
    int V = adj.size();
    int s = 0; 

    vector<int> res;
    queue<int> q;  
    vector<bool> visited(V, false);

    visited[s] = true;
    q.push(s);

    while (!q.empty()) {
        int curr = q.front();
        q.pop();
        res.push_back(curr);

        for (int x : adj[curr]) {
            if (!visited[x]) {
                visited[x] = true;
                q.push(x);
            }
        }
    }
    return res;
}
```

## 4. Tính liên thông của đồ thị
### 4.1. Các định nghĩa trong đồ thị vô hướng
#### 4.1.1. Liên thông
- Một đồ thị vô hướng liên thông nếu giữa mọi cặp đỉnh đều tồn tại đường đi.
- Nếu đồ thị không liên thông, nó sẽ được chia thành nhiều thành phần liên thông.

#### 4.1.2. Thành phần liên thông
- Thành phần liên thông là một tập con các đỉnh sao cho:
    1. Bất kỳ hai đỉnh nào trong tập đều liên thông với nhau.
    2. Không thể thêm đỉnh nào từ ngoài vào mà vẫn giữ tính liên thông.

#### 4.1.3. Cạnh cầu
- Cạnh cầu là một cạnh mà khi bỏ nó đi, số thành phần liên thông của đồ thị tăng lên.
- Nói cách khác, nó là cạnh “quan trọng” để giữ các phần của đồ thị kết nối với nhau.

#### 4.1.4. Khớp (đỉnh trụ)
- Khớp là một đỉnh mà khi bỏ nó (cùng các cạnh kề), số thành phần liên thông của đồ thị tăng lên.
- Đỉnh này giống như một “nút cổ chai” trong mạng.

### 4.2. Các định nghĩa trong đồ thị có hướng
#### 4.2.1. Liên thông mạnh
Đồ thị có hướng là liên thông mạnh nếu với mọi cặp đỉnh $(u, v)$ đều tồn tại đường đi có hướng từ $u$ đến $v$ và ngược lại.

#### 4.2.2. Liên thông yếu
- Nếu bỏ hướng của tất cả các cạnh, đồ thị trở thành vô hướng liên thông → gọi là liên thông yếu.
- Nghĩa là có thể đi giữa mọi cặp đỉnh nếu không quan tâm đến hướng đi.
