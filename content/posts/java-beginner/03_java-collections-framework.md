---
title: "Bài 3: Java Collections Framework - List, Set, và Map"
date: "2025-10-15T09:00:00+07:00"
draft: false
summary: "Hiểu sâu về 3 interface cốt lõi của Java Collections Framework: List, Set, và Map, cùng các lớp triển khai phổ biến như ArrayList, HashSet, HashMap."
tags: ["Java", "Collections", "List", "Set", "Map", "Core Java"]
categories: ["Lập trình Java"]
series: ["Java Cho Người Mới Bắt Đầu"]
series_order: 3
featureAsset: "img/java-logo.png"
---

Khi làm việc với Java, bạn không thể tránh khỏi việc xử lý các tập hợp dữ liệu. Java Collections Framework (JCF) cung cấp một bộ công cụ mạnh mẽ để lưu trữ và thao tác với các nhóm đối tượng này.

Việc hiểu rõ và lựa chọn đúng cấu trúc dữ liệu cho từng bài toán là một kỹ năng quan trọng của lập trình viên Java. Bài viết này sẽ đi sâu vào ba giao diện (interface) cốt lõi của JCF: List, Set, và Map.

---

## 🧠 1. Tổng Quan Về JCF

JCF là một tập hợp các lớp và giao diện được thiết kế để:

- **Lưu trữ**: Cung cấp các cấu trúc dữ liệu như danh sách, tập hợp, hàng đợi, bản đồ.
- **Thao tác**: Cung cấp các thuật toán để tìm kiếm, sắp xếp, và quản lý dữ liệu.
- **Tối ưu hóa**: Các lớp triển khai được tối ưu hóa về hiệu suất cho các trường hợp sử dụng khác nhau.

### Cấu trúc phân cấp chính

- **Iterable (Interface)**: Giao diện gốc, cho phép duyệt qua các phần tử.
- **Collection (Interface)**: Kế thừa từ `Iterable`, là nền tảng cho `List`, `Set`, và `Queue`.
- **Map (Interface)**: Một cấu trúc riêng biệt, lưu trữ dữ liệu dưới dạng cặp `key-value`.

---

## 📚 2. List: Danh Sách Có Thứ Tự, Cho Phép Trùng Lặp

`List` là một tập hợp các phần tử được sắp xếp theo thứ tự và cho phép chứa các phần tử trùng lặp. Bạn có thể truy cập các phần tử thông qua chỉ số (index) của chúng, bắt đầu từ 0.

### Các lớp triển khai phổ biến

#### ArrayList

- **Cấu trúc**: Dựa trên mảng động (dynamic array).
- **Điểm mạnh**: Truy cập ngẫu nhiên phần tử theo chỉ số rất nhanh (độ phức tạp O(1)).
- **Điểm yếu**: Thêm hoặc xóa phần tử ở giữa danh sách chậm vì cần phải dịch chuyển các phần tử phía sau (độ phức tạp O(n)).
- **Khi nào dùng**: Khi bạn thường xuyên đọc dữ liệu theo chỉ số và ít khi thêm/xóa ở giữa.

```java
import java.util.ArrayList;
import java.util.List;

List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Apple"); // Cho phép trùng lặp

System.out.println(fruits.get(1)); // Output: Banana
```

#### LinkedList

- **Cấu trúc**: Dựa trên danh sách liên kết đôi (doubly-linked list).
- **Điểm mạnh**: Thêm hoặc xóa phần tử ở đầu/cuối danh sách rất nhanh (O(1)).
- **Điểm yếu**: Truy cập ngẫu nhiên phần tử theo chỉ số chậm vì phải duyệt từ đầu hoặc cuối (O(n)).
- **Khi nào dùng**: Khi bạn thường xuyên thêm/xóa phần tử ở đầu/cuối danh sách.

```java
import java.util.LinkedList;
import java.util.List;

List<String> animals = new LinkedList<>();
animals.add("Dog");
animals.add("Cat");

// Thêm vào đầu danh sách
((LinkedList<String>) animals).addFirst("Lion");
```

---

## 🌿 3. Set: Tập Hợp Không Thứ Tự, Không Cho Phép Trùng Lặp

`Set` là một tập hợp các phần tử **không chứa các phần tử trùng lặp**. Nó mô phỏng khái niệm tập hợp trong toán học và thường không đảm bảo về thứ tự.

### Các lớp triển khai phổ biến

#### HashSet

- **Cấu trúc**: Dựa trên bảng băm (hash table).
- **Đặc điểm**: Không đảm bảo thứ tự các phần tử. Hiệu suất rất cao cho các thao tác thêm, xóa, kiểm tra sự tồn tại (trung bình là O(1)).
- **Khi nào dùng**: Khi bạn chỉ cần lưu trữ các phần tử duy nhất và không quan tâm đến thứ tự. Đây là lựa chọn phổ biến nhất cho `Set`.

```java
import java.util.HashSet;
import java.util.Set;

Set<Integer> numbers = new HashSet<>();
numbers.add(10);
numbers.add(20);
numbers.add(10); // Phần tử này sẽ không được thêm vào vì đã tồn tại

System.out.println(numbers); // Output: [20, 10] (thứ tự không đảm bảo)
```

#### TreeSet

- **Cấu trúc**: Dựa trên cây đỏ-đen (red-black tree).
- **Đặc điểm**: Các phần tử luôn được lưu trữ theo thứ tự tự nhiên (hoặc theo `Comparator` được cung cấp).
- **Khi nào dùng**: Khi bạn cần một tập hợp không trùng lặp và các phần tử phải được sắp xếp.

```java
import java.util.TreeSet;
import java.util.Set;

Set<String> sortedNames = new TreeSet<>();
sortedNames.add("Charlie");
sortedNames.add("Alice");
sortedNames.add("Bob");

System.out.println(sortedNames); // Output: [Alice, Bob, Charlie]
```

---

## 🗺️ 4. Map: Lưu Trữ Dưới Dạng Cặp Key-Value

`Map` là một cấu trúc dữ liệu lưu trữ các cặp **khóa-giá trị (key-value)**. Mỗi khóa (key) là duy nhất và được dùng để truy xuất giá trị (value) tương ứng. `Map` không kế thừa từ `Collection`.

### Các lớp triển khai phổ biến

#### HashMap

- **Cấu trúc**: Dựa trên bảng băm.
- **Đặc điểm**: Không đảm bảo thứ tự của các cặp key-value. Hiệu suất rất cao cho các thao tác thêm, lấy, xóa (trung bình là O(1)).
- **Khi nào dùng**: Khi bạn cần tra cứu dữ liệu nhanh chóng bằng một khóa duy nhất và không quan tâm đến thứ tự. Đây là lựa chọn mặc định cho `Map`.

```java
import java.util.HashMap;
import java.util.Map;

Map<String, String> capitals = new HashMap<>();
capitals.put("Vietnam", "Hanoi");
capitals.put("USA", "Washington D.C.");

System.out.println(capitals.get("Vietnam")); // Output: Hanoi
```

#### TreeMap

- **Cấu trúc**: Dựa trên cây đỏ-đen.
- **Đặc điểm**: Các cặp key-value được sắp xếp theo thứ tự tự nhiên của khóa.
- **Khi nào dùng**: Khi bạn cần một bản đồ mà các khóa luôn được sắp xếp.

```java
import java.util.TreeMap;
import java.util.Map;

Map<Integer, String> studentGrades = new TreeMap<>();
studentGrades.put(3, "Charlie");
studentGrades.put(1, "Alice");
studentGrades.put(2, "Bob");

System.out.println(studentGrades); // Output: {1=Alice, 2=Bob, 3=Charlie}
```

---

## 🎯 Tổng kết

Việc lựa chọn đúng collection cho bài toán là rất quan trọng:

- **📚 `List`**: Cần một danh sách **có thứ tự** và **cho phép trùng lặp**?
  - `ArrayList`: Ưu tiên truy cập nhanh theo chỉ số.
  - `LinkedList`: Ưu tiên thêm/xóa nhanh ở đầu/cuối.
- **🌿 `Set`**: Cần một tập hợp các phần tử **duy nhất**?
  - `HashSet`: Ưu tiên hiệu suất cao, không cần thứ tự.
  - `TreeSet`: Cần các phần tử được sắp xếp.
- **🗺️ `Map`**: Cần lưu trữ và tra cứu dữ liệu bằng một **khóa duy nhất**?
  - `HashMap`: Ưu tiên hiệu suất cao, không cần thứ tự khóa.
  - `TreeMap`: Cần các khóa được sắp xếp.

Hiểu rõ bản chất của các cấu trúc dữ liệu này sẽ giúp bạn viết mã Java hiệu quả và tối ưu hơn rất nhiều.
