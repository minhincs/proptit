# Stack

## 1. Khái niệm
- Là kiểu cấu trúc dữ liệu hoạt động theo nguyên tắc Last In First Out (LIFO) hoặc First In Last Out (FILO). Có nghĩa là phần tử đầu tiên được thêm vào Stack sẽ là phần tử cuối cùng được lấy ra và ngược lại, phần tử cuối cùng được thêm vào sẽ là phần tử đầu tiên được lấy ra.
- Có thể tưởng tượng Stack như 1 cái hộp chữ nhật như sau:

```
+--------
|A B      <- C (add 'C' to the stack)
+--------

+--------
|A B C ---->   (last in (C) first out (also C))
+--------
```

## 2. Khai báo Stack
```cpp
stack<data_type> stack_name;
```

## 3. Các thao tác trên Stack
- `push(X)`: Đẩy một phần tử vào stack
- `pop()`: Xóa phần tử trên cùng của stack
- `top`: Lấy phần tử trên cùng của stack
- `size`: Lấy độ dài của stack
- `empty`: Kiểm tra xem stack có rỗng không
