---
title: "Bài 1: Nhập Môn Java - Hướng Dẫn Toàn Diện"
date: "2025-10-13T09:00:00+07:00"
draft: false
summary: "Hướng dẫn toàn diện về Java cho người mới bắt đầu, từ khái niệm, cài đặt môi trường đến viết chương trình Hello World đầu tiên."
tags: ["Java", "Giới Thiệu", "Cơ Bản", "Hello World"]
categories: ["Lập trình Java"]
series: ["Java Cho Người Mới Bắt Đầu"]
series_order: 1
featureAsset: "img/java-logo.png"
---

Java là một trong những ngôn ngữ lập trình phổ biến và có sức ảnh hưởng nhất trên thế giới. Từ các ứng dụng Android, hệ thống ngân hàng, cho đến các dịch vụ web khổng lồ, Java luôn có mặt ở khắp mọi nơi. Nếu bạn đang muốn bắt đầu hành trình lập trình của mình, Java chính là một lựa chọn tuyệt vời.

Bài viết này sẽ cung cấp cho bạn một lộ trình chi tiết, từ việc hiểu Java là gì cho đến việc viết chương trình đầu tiên của bạn.

---

## 🤔 1. Java Là Gì và Tại Sao Nên Học?

Java là một ngôn ngữ lập trình hướng đối tượng, đa nền tảng được phát triển bởi Sun Microsystems (nay thuộc sở hữu của Oracle). Triết lý cốt lõi của nó là **"Viết một lần, chạy mọi nơi"** (Write Once, Run Anywhere - WORA).

### Những lý do bạn nên học Java

- **Đa nền tảng**: Mã Java được biên dịch thành "bytecode", có thể chạy trên bất kỳ máy nào có cài đặt Máy ảo Java (JVM).
- **Lập trình hướng đối tượng (OOP)**: Giúp tổ chức mã nguồn một cách logic, dễ quản lý, tái sử dụng và mở rộng.
- **Hệ sinh thái và cộng đồng lớn**: Có một cộng đồng phát triển khổng lồ cùng với hàng triệu thư viện và framework (như Spring, Hibernate).
- **Nhu cầu tuyển dụng cao**: Java liên tục nằm trong top các ngôn ngữ lập trình được yêu cầu nhiều nhất trên thị trường việc làm.

---

## 🛠️ 2. Chuẩn Bị Môi Trường Phát Triển

Để bắt đầu lập trình Java, bạn cần hai thứ chính:

- **JDK (Java Development Kit)**: Bộ công cụ dành cho nhà phát triển, bao gồm Trình biên dịch (Compiler) và Máy ảo Java (JVM). Bạn có thể tải JDK từ trang web của Oracle hoặc các bản OpenJDK như Adoptium.
- **IDE (Integrated Development Environment)**: Một trình soạn thảo code thông minh giúp bạn viết, biên dịch và chạy chương trình dễ dàng hơn.
  - **IntelliJ IDEA (Community Edition)**: Rất mạnh mẽ và thông minh.
  - **Visual Studio Code (với Java Extension Pack)**: Nhẹ nhàng và linh hoạt.
  - **Eclipse**: Một IDE kỳ cựu và vẫn rất phổ biến.

---

## 🚀 3. Chương Trình "Hello, World!" Đầu Tiên

Sau khi cài đặt xong, hãy cùng viết chương trình Java đầu tiên. Mở IDE của bạn và tạo một tệp mới tên là `HelloWorld.java`.

```java
// Tên class phải trùng với tên tệp
public class HelloWorld {
    // Đây là phương thức chính, nơi chương trình bắt đầu chạy
    public static void main(String[] args) {
        // In dòng chữ "Hello, World!" ra màn hình console
        System.out.println("Hello, World!");
    }
}
```

### Giải thích

- `public class HelloWorld`: Khai báo một lớp (class) có tên là `HelloWorld`. Trong Java, mọi thứ đều nằm trong các lớp.
- `public static void main(String[] args)`: Đây là phương thức `main`, điểm khởi đầu của mọi chương trình Java.
- `System.out.println("Hello, World!");`: Lệnh này dùng để in một chuỗi ký tự ra console.

Bây giờ, hãy nhấn nút "Run" trong IDE của bạn. Bạn sẽ thấy dòng chữ `Hello, World!` xuất hiện. Chúc mừng, bạn đã viết thành công chương trình Java đầu tiên!

---

## 🧠 4. Các Khái Niệm Cú Pháp Cơ Bản

### Biến (Variables)

Dùng để lưu trữ dữ liệu. Mỗi biến phải có một kiểu dữ liệu xác định.

```java
String name = "Alice"; // Chuỗi ký tự
int age = 30;         // Số nguyên
double score = 9.5;   // Số thực
boolean isStudent = true; // Giá trị đúng/sai
```

### Toán tử (Operators)

Dùng để thực hiện các phép toán.

```java
int a = 10;
int b = 5;
int sum = a + b; // Phép cộng
int product = a * b; // Phép nhân
```

### Cấu trúc điều khiển (Control Flow)

Dùng để quyết định luồng chạy của chương trình.

**if-else (Rẽ nhánh):**

```java
int a = 10;
if (a > 5) {
    System.out.println("a lớn hơn 5");
} else {
    System.out.println("a không lớn hơn 5");
}
```

**for (Vòng lặp):**

```java
// In các số từ 0 đến 4
for (int i = 0; i < 5; i++) {
    System.out.println("Số hiện tại là: " + i);
}
```

---

## 🎯 Tổng kết

Bạn đã đi qua những bước đầu tiên quan trọng nhất trên con đường chinh phục Java.

- **🤔 Hiểu khái niệm**: Java là ngôn ngữ đa nền tảng, hướng đối tượng.
- **🛠️ Cài đặt môi trường**: Cài đặt **JDK** và một **IDE** (như IntelliJ hoặc VS Code).
- **🚀 Viết code đầu tiên**: Tạo lớp, viết phương thức `main` và dùng `System.out.println()` để in ra console.
- **🧠 Nắm cú pháp cơ bản**: Làm quen với biến, toán tử và cấu trúc điều khiển như `if-else`, `for`.

Nền tảng vững chắc hôm nay sẽ là bàn đạp để bạn tiến xa hơn với các chủ đề thú vị như OOP, Collections, và Spring Boot. Hãy kiên trì luyện tập nhé!
