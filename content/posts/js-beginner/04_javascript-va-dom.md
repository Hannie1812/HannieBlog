+++
title = "Bài 4: DOM là gì? \"Quyền năng\" Thay đổi Trang Web với JavaScript"
date = "2025-10-13T10:30:00+07:00"
draft = false
summary = "Tìm hiểu về DOM (Document Object Model) và cách JavaScript tương tác với trang web thông qua DOM API để tạo ra các trang web động."
tags = ["JavaScript", "DOM", "Web Development"]
categories = ["Lập trình JavaScript"]
series = ["JavaScript Cho Người Mới Bắt Đầu"]
series_order = 4
featureAsset = "img/javascript-logo.png"
+++

## 🌳 DOM là gì?

DOM (Document Object Model) là một API cho phép JavaScript tương tác với HTML. Khi trình duyệt tải trang web, nó tạo ra một "cây đối tượng" từ HTML của bạn.

### Ví dụ HTML:

```html
<html>
  <head>
    <title>Trang của tôi</title>
  </head>
  <body>
    <h1>Chào bạn</h1>
    <p id="greeting">Đây là một trang web.</p>
  </body>
</html>
```

---

## 🔍 Bước 1: Truy vấn (Query)

### Các phương thức truy vấn:

- **Theo ID** (Nhanh nhất):

```javascript
const element = document.getElementById("greeting");
```

- **Theo CSS Selector** (Linh hoạt nhất):

```javascript
const heading = document.querySelector("h1");
const firstParagraph = document.querySelector(".my-class");
const allParagraphs = document.querySelectorAll("p");
```

---

## ✨ Bước 2: Thao tác (Manipulation)

### Thay đổi nội dung:

```javascript
// Thay đổi text
element.textContent = "Nội dung mới!";

// Thay đổi HTML (cẩn thận XSS)
element.innerHTML = "<strong>Nội dung</strong> mới!";
```

### Thay đổi thuộc tính:

```javascript
const img = document.querySelector("img");
img.src = "new-image.jpg";
img.setAttribute("alt", "Mô tả mới");
```

### Thao tác với classes:

```javascript
element.classList.add("active");
element.classList.remove("inactive");
element.classList.toggle("visible");
```

---

## 👂 Bước 3: Lắng nghe (Listen)

### Xử lý sự kiện:

```javascript
const button = document.querySelector("#myButton");

button.addEventListener("click", function (event) {
  // Ngăn hành vi mặc định
  event.preventDefault();

  // Thực hiện thao tác
  const greeting = document.getElementById("greeting");
  greeting.textContent = "Bạn đã click!";
});
```

---

## 🎯 Tổng kết

- **DOM**: Cây đối tượng biểu diễn HTML
- **Query**: `getElementById`, `querySelector` để tìm phần tử
- **Manipulate**: Thay đổi nội dung, thuộc tính, style
- **Listen**: `addEventListener` để phản hồi tương tác
