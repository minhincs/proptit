# Queue, Deque, Priority Queue

## 1. Queue
- Hoạt động theo quy tắc FIFO - First In First Out, tức là phần tử được thêm vào đầu tiên sẽ là phần tử được lấy ra đầu tiên

### 1a. Khai báo queue
Khai báo queue rỗng:
```cpp
queue<data_type> queue_name;
```

Khai báo queue dựa trên queue có sẵn:
```cpp
queue<int> q1; // Queue cho trước

// Khai báo q2 dựa trên q1
queue<int> q2(q1);
```

### 1b. Thao tác trên Queue
- `front()`: Truy cập vào phần tử được thêm sớm nhất trong queue
- `back()`: Truy cập vào phần tử được thêm muộn nhất trong queue
- `empty()`: Kiểm tra xem queue có rỗng hay không
- `size()`: Lấy số phần tử có trong queue
- `push(X)`: Thêm vào queue 1 phần tử 
- `pop()`: Xóa phần tử (theo quy tắc FIFO) của queue 
- `swap(q1, q2)`: Swap 2 queue

> [!NOTE] 
> Các thao tác trên đều có độ phức tạp $O(1)$ trừ thao tác `swap` là $O(n)$

## 2. Deque
- Deque là viết tắt của Double Ended Queue
- Cho phép người dùng có thể thực hiện thêm/bớt phần tử trên cả 2 đầu của queue 

### 2a. Khai báo Deque
- Khởi tạo một Deque rỗng
```cpp
deque<data_type> deque_name;
```
- Khởi tạo một dequa có số phần tử cho trước và giá trị mặc định của các phần tử đó
```cpp
deque<date_type> deque_name(n, p);
// Deque có n phần tử giá trị p
```
- Khởi tạo một Deque với các phần tử được định nghĩa sẵn
```cpp
deque<int> dq = {1, 2, 3, 4, 5};
```

### 2b. Thao tác trên Deque
- `front()`: Truy cập phần tử đầu queue
- `back()`: Truy cập phần tử cuối queue
- `begin()`: Trả về Iterator chỉ vào phần tử đầu tiên
- `end()`: Trả về Iterator chỉ vào phần tử cuối cùng 
- `push_front(X)`: đẩy 1 phần tử vào đầu queue
- `push_back(X)`: đẩy 1 phần tử vào cuối queue
- `pop_front()`: Xóa phần tử đầu queue
- `pop_back()`: Xóa phần tử cuối queue
- `size()`: Trả về số lượng phần tử trong queue
- `empty()`: Kiểm tra xem queue có rỗng không
- `at(i)`: Trả về giá trị phần tử tại vị trí `i`
- `insert(it, X)`: Chèn 1 phần tử vào vị trí xác định
- `erase(it)`: Xóa phần tử tại vị trí xác định
- `clear()`: Xóa toàn bộ queue

> [!NOTE] 
> Các thao tác trên 2 đầu của queue thường sẽ có độ phức tạp $O(1)$. Trong khi đó các thao tác tại phần tử bất kì trong queue thưởng có độ phức tạo $O(n)$

## 3. Priority Queue
- Là queue mà mỗi phần tử đều có một độ ưu tiên nhất định
- Các phần tử sẽ được lấy ra dựa vào độ ưu tiên đó
- Mặc định, giá trị của phần tử sẽ là độ ưu tiên của nó, tức là phần tử có giá trị càng cao thì độ ưu tiên càng cao. Nhưng có thể cài đặt để thay đổi cách sắp xếp độ ưu tiên

### 3a. Khai báo Priority Queue
```cpp
priority_queue<data_type, container, comp> queue_name
```
**Giải thích**:
- `container`: là cấu trúc dữ liệu dùng để lưu các phần tử của queue. Mặc định priority queue dùng vector đảm nhiệm vai trò này
- `comp`: hàm so sánh, để quyết định cách các phần tử được gán độ ưu tiên (priority)

> [!NOTE] 
> priority_queue là một lớp bọc (wrapper) xung quanh 1 containter (mặc định là vector). Thông thường nó sử dụng binary heap để duy trì các đặc tính của priority queue 

**Ví dụ**: khởi tạo một priority queue nhưng giá trị lớn hơn có độ ưu tiên thấp hơn
```cpp
priority_queue<int, vector<int>, greater<int>> pq;
```

### 3b. Thao tác trên priority queue
- `empty()`: Kiểm tra xem queue có rỗng không
- `size()`: Trả về số phần tử có trong queue
- `top()`: Trả về giá trị của phần tử có độ ưu tiên cao nhất 
- `push(X)`: Đẩy vào queue 1 phần tử
- `pop()`: Xóa phần tử có priority lớn nhất trong queue
- `swap()`: Swap 2 queue

> [!NOTE] 
> Thêm bớt phần tử trong priority queue có độ phức tạp $O(\log n)$. Còn truy cập vào phần tử "top" có độ phức tạp $O(1)$
