+++
title = "Bài 2: Hiểu Sâu về var, let, và const - Scope và Hoisting"
date = "2025-10-13T09:30:00+07:00"
draft = false
summary = "Tìm hiểu sự khác biệt giữa var, let và const trong JavaScript, cách hoạt động của scope và hoisting, và khi nào nên dùng mỗi loại."
tags = ["JavaScript", "Variables", "Scope", "Hoisting"]
categories = ["Lập trình JavaScript"]
series = ["JavaScript Cho Người Mới Bắt Đầu"]
series_order = 2

featureAsset = "img/javascript-logo.png"
+++

## 🔍 Giới thiệu

Trong JavaScript, bạn dùng `var`, `let`, và `const` để khai báo biến—những chiếc hộp có nhãn để lưu trữ dữ liệu. Trong hơn 20 năm, chúng ta chỉ có `var`. Kể từ ES6 (2015), chúng ta có thêm `let` và `const`.

Sự khác biệt cốt lõi nằm ở hai khái niệm: **Scope** (Phạm vi) và **Hoisting** (Kéo cờ).

---

## 😱 Vấn đề với var và Function Scope

### Function Scope là gì?

- `var` tuân theo function scope
- Biến chỉ "thuộc về" hàm chứa nó
- Nếu không trong hàm nào, trở thành biến toàn cục

### Ví dụ về rò rỉ biến:

```javascript
function runLoop() {
  for (var i = 0; i < 5; i++) {
    console.log(i); // 0, 1, 2, 3, 4
  }
  console.log("Giá trị cuối:", i); // 5 - biến i rò rỉ!
}
runLoop();
```

---

## 🤔 Hoisting với var

### Hoisting là gì?

- JavaScript "kéo" khai báo lên đầu scope
- Biến `var` được khởi tạo là `undefined`

### Ví dụ hoisting:

```javascript
console.log(myVar); // undefined, không lỗi!
var myVar = "Hello";
console.log(myVar); // "Hello"

// Thực tế JS thực thi như sau:
var myVar; // Hoisted
console.log(myVar);
myVar = "Hello";
console.log(myVar);
```

---

## 🎯 let và const: Giải pháp Modern

### Block Scope

- Biến chỉ tồn tại trong khối `{}`
- Không rò rỉ ra ngoài

```javascript
function runLoopFixed() {
  for (let i = 0; i < 5; i++) {
    console.log(i);
  }
  // console.log(i); // Lỗi: i is not defined
}
```

### Temporal Dead Zone (TDZ)

```javascript
console.log(myLetVar); // Lỗi: Cannot access before initialization
let myLetVar = "Hello";
```

---

## 💡 Khi nào dùng let vs const?

### let - cho biến có thể thay đổi

```javascript
let score = 0;
score += 10; // OK
```

### const - cho tham chiếu không đổi

```javascript
const PI = 3.14;
// PI = 3.14159; // Lỗi!

const user = { name: "Alice" };
user.name = "Bob"; // OK - thay đổi thuộc tính
// user = {};        // Lỗi - không thể gán lại
```

---

## 🎯 Tổng kết

- `var`: function scope, hoisting với `undefined`
- `let`/`const`: block scope, TDZ bảo vệ
- Dùng `const` mặc định, `let` khi cần thay đổi giá trị
- Tránh dùng `var` trong code hiện đại
