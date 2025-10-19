+++
title = "Bài 3: JavaScript Bất đồng bộ (Async) - Từ Callbacks, Promises đến Async/Await"
date = "2025-10-13T10:00:00+07:00"
draft = false
summary = "Tìm hiểu về cách JavaScript xử lý các tác vụ bất đồng bộ, từ callbacks truyền thống đến promises và cú pháp hiện đại async/await."
tags = ["JavaScript", "Async", "Promises", "Callbacks"]
categories = ["Lập trình JavaScript"]
series = ["JavaScript Cho Người Mới Bắt Đầu"]
series_order = 3
featureAsset = "img/javascript-logo.png"
+++

## 🧠 Giới thiệu về Bất đồng bộ

JavaScript về cơ bản là đơn luồng (single-threaded). Điều này có nghĩa là nó chỉ có thể làm một việc tại một thời điểm. Hãy tưởng tượng một nhân viên pha chế tại quán cà phê chỉ có thể phục vụ từng người một.

---

## 😱 Vấn đề của Đồng bộ (Synchronous)

```javascript
console.log("1. Bắt đầu đặt hàng");

// Giả sử đây là một tác vụ nặng, mất 5 giây
syncTask(5000);

console.log("3. Nhận được cà phê");
```

Trong mô hình đồng bộ, toàn bộ ứng dụng sẽ bị "đơ" (blocked) trong 5 giây đó.

---

## 🔄 Event Loop - Giải pháp Bất đồng bộ

### Quy trình xử lý:

1. Nhận tác vụ (đơn hàng)
2. Giao cho Web API (máy pha cà phê)
3. Tiếp tục công việc khác
4. Nhận kết quả từ Callback Queue
5. Event Loop điều phối

---

## 📞 Callbacks - Cấp độ 1

### Ví dụ cơ bản:

```javascript
console.log("1. Bắt đầu đặt hàng");

setTimeout(() => {
  console.log("3. Nhận được cà phê");
}, 2000);

console.log("2. Nhận hóa đơn và chờ");
```

### Callback Hell:

```javascript
step1(data, (result1) => {
  step2(result1, (result2) => {
    step3(result2, (result3) => {
      // Code lồng nhau sâu 😱
    });
  });
});
```

---

## 🤝 Promises - Cấp độ 2

### Ba trạng thái:

- **pending**: Đang chờ
- **fulfilled**: Thành công
- **rejected**: Thất bại

### Ví dụ Promise:

```javascript
fetch("https://api.example.com/user/1")
  .then((response) => response.json())
  .then((userData) => {
    console.log("Dữ liệu:", userData);
  })
  .catch((error) => {
    console.error("Lỗi:", error);
  });
```

---

## ⭐ Async/Await - Cấp độ 3

### Quy tắc sử dụng:

- Đánh dấu hàm với `async`
- Dùng `await` với Promises
- Xử lý lỗi bằng try/catch

### Ví dụ Async/Await:

```javascript
async function fetchUserData() {
  try {
    const response = await fetch("https://api.example.com/user/1");
    const userData = await response.json();
    console.log("Dữ liệu:", userData);
  } catch (error) {
    console.error("Lỗi:", error);
  }
}
```

---

## 🎯 Tổng kết

- **Đồng bộ**: Blocking, đơn giản nhưng không hiệu quả
- **Callbacks**: Cách truyền thống, dễ rơi vào callback hell
- **Promises**: Chuỗi .then() rõ ràng, xử lý lỗi tập trung
- **Async/Await**: Cú pháp hiện đại, dễ đọc và maintain
