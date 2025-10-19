+++
title = "Bài 5: 10 Tính năng ES6+ \"Thay đổi cuộc chơi\" Bạn Phải Biết"
date = "2025-10-13T11:00:00+07:00"
draft = false
summary = "Khám phá 10 tính năng quan trọng nhất của ES6+ đã thay đổi cách chúng ta viết JavaScript hiện đại."
tags = ["JavaScript", "ES6", "Modern JavaScript"]
categories = ["Lập trình JavaScript"]
series = ["JavaScript Cho Người Mới Bắt Đầu"]
series_order = 5
featureAsset = "img/javascript-logo.png"
+++

## 🚀 Giới thiệu

ES6 (hay ECMAScript 2015) là bản cập nhật quan trọng nhất trong lịch sử JavaScript. Nó không chỉ thêm tính năng mới, mà còn thay đổi hoàn toàn cách chúng ta viết code.

---

## 1️⃣ let và const

(Đã phân tích chi tiết ở Bài 2)

- Block Scope thay vì Function Scope
- Giải quyết vấn đề hoisting
- Ngăn chặn rò rỉ biến

---

## 2️⃣ Arrow Functions (=>)

### Cú pháp ngắn gọn:

```javascript
// Kiểu cũ
function add(a, b) {
  return a + b;
}

// Kiểu mới (Arrow Function)
const add = (a, b) => a + b;
```

### Xử lý this:

```javascript
function Timer() {
  this.seconds = 0;

  setInterval(() => {
    this.seconds++; // 'this' là Timer
    console.log(this.seconds);
  }, 1000);
}
```

---

## 3️⃣ Template Literals (``)

### Ưu điểm:

- Nhúng biến với ${...}
- Hỗ trợ nhiều dòng

```javascript
const user = "Alice";
const score = 95;

// Kiểu mới
const greeting = `Xin chào ${user},
Điểm của bạn là ${score}.`;
```

---

## 4️⃣ Destructuring

### Với Objects:

```javascript
const user = { firstName: "John", lastName: "Doe", age: 30 };

// Destructuring object
const { firstName, age } = user;
const { lastName: ho } = user; // Đổi tên
```

### Với Arrays:

```javascript
const colors = ["Đỏ", "Xanh", "Vàng"];
const [firstColor, secondColor] = colors;
```

---

## 5️⃣ Spread Operator (...)

```javascript
// Nối mảng
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2];

// Shallow copy
const original = ["a", "b"];
const copy = [...original];

// Với objects
const user = { name: "Bot", version: 1 };
const updatedUser = { ...user, version: 2 };
```

---

## 6️⃣ Rest Parameters

```javascript
function sum(first, second, ...allOtherNumbers) {
  let total = first + second;
  allOtherNumbers.forEach((num) => (total += num));
  return total;
}

sum(1, 2, 3, 4, 5); // 15
```

---

## 7️⃣ Default Parameters

```javascript
// Kiểu mới
function greet(name = "Guest") {
  console.log(`Hello, ${name}`);
}

greet(); // Hello, Guest
```

---

## 8️⃣ ES Modules

```javascript
// math.js
export const PI = 3.14;
export function add(a, b) {
  return a + b;
}

// app.js
import { PI, add } from "./math.js";
```

---

## 9️⃣ Promises

(Đã phân tích ở Bài 3)

## 🔟 async/await

(Đã phân tích ở Bài 3)

---

## 🎯 Tổng kết

- **let/const**: Block scope, thay thế var
- **Arrow Functions**: Cú pháp ngắn gọn, xử lý this
- **Template Literals**: String interpolation đơn giản
- **Destructuring**: Trích xuất dữ liệu dễ dàng
- **Spread/Rest**: Thao tác với arrays/objects linh hoạt
- **Modules**: Code organization chuẩn mực
- **Promises & async/await**: Xử lý bất đồng bộ hiện đại
