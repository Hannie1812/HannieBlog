---
title: "Bài 4: Lập Trình Đa Luồng (Multithreading) Trong Java"
date: "2025-10-16T09:00:00+07:00"
draft: false
summary: "Tìm hiểu về lập trình đa luồng trong Java, từ Thread/Runnable cơ bản, ExecutorService, đến CompletableFuture hiện đại."
tags:
  [
    "Java",
    "Multithreading",
    "Concurrency",
    "CompletableFuture",
    "ExecutorService",
    "Core Java",
  ]
categories: ["Lập trình Java"]
series: ["Java Cho Người Mới Bắt Đầu"]
series_order: 4
featureAsset: "img/java-logo.png"
---

Trong thế giới hiện đại, các ứng dụng cần phải xử lý nhiều tác vụ cùng một lúc để mang lại trải nghiệm người dùng tốt nhất và tận dụng tối đa sức mạnh của CPU đa lõi. Đây là lúc lập trình đa luồng (multithreading) và bất đồng bộ (asynchronous programming) phát huy tác dụng. Java cung cấp một hệ sinh thái phong phú để làm việc với concurrency, từ các khái niệm cơ bản như Thread và Runnable cho đến các API cấp cao như ExecutorService và CompletableFuture.

Bài viết này sẽ dẫn dắt bạn qua hành trình phát triển của lập trình đa luồng trong Java.

---

## 🤔 1. Tại Sao Cần Đa Luồng?

Đa luồng giải quyết vấn đề này bằng cách cho phép bạn chạy các tác vụ tốn thời gian trên các luồng nền (background threads), giữ cho luồng chính luôn sẵn sàng phản hồi tương tác của người dùng.

---

## 🕰️ 2. Cách Cổ Điển: Thread và Runnable

Đây là cách tiếp cận cơ bản nhất để tạo luồng trong Java.

### implements Runnable (Ưu tiên)

Đây là cách được khuyến khích vì nó tách biệt tác vụ (task) khỏi cơ chế thực thi luồng (thread).

```java
class MyTask implements Runnable {
    @Override
    public void run() {
        System.out.println("Task is running in thread: " + Thread.currentThread().getName());
    }
}

// Sử dụng
Thread thread = new Thread(new MyTask());
thread.start();
```

### extends Thread

Cách này ít linh hoạt hơn vì Java không hỗ trợ đa kế thừa.

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Task is running in thread: " + Thread.currentThread().getName());
    }
}

// Sử dụng
MyThread myThread = new MyThread();
myThread.start();
```

**Vấn đề**: Việc quản lý thủ công các `Thread` (tạo mới, hủy bỏ) rất phức tạp, tốn kém tài nguyên và dễ gây ra lỗi.

---

## 🚀 3. Cách Tốt Hơn: Executor Framework

Ra đời từ Java 5, `Executor Framework` là một bước tiến lớn. Nó tách biệt việc định nghĩa tác vụ (`Runnable`, `Callable`) khỏi việc thực thi và quản lý luồng.

### Các thành phần chính

- **ExecutorService**: Giao diện quản lý việc thực thi các tác vụ bất đồng bộ.
- **Executors**: Lớp tiện ích để tạo các loại `ExecutorService` khác nhau.
- **ThreadPool**: `ExecutorService` thường quản lý một nhóm các luồng (thread pool) để tái sử dụng, giúp tiết kiệm tài nguyên.
- **Future**: Đại diện cho kết quả của một phép tính bất đồng bộ sẽ có trong tương lai.

### Ví dụ

```java
import java.util.concurrent.*;

public class ExecutorExample {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        // Tạo một thread pool với 2 luồng
        ExecutorService executor = Executors.newFixedThreadPool(2);

        // Gửi một tác vụ Runnable (không trả về kết quả)
        executor.submit(() -> {
            System.out.println("Runnable task is running in: " + Thread.currentThread().getName());
        });

        // Gửi một tác vụ Callable (trả về kết quả)
        Future<String> future = executor.submit(() -> {
            Thread.sleep(1000); // Giả lập một tác vụ tốn thời gian
            return "Result from Callable";
        });

        System.out.println("Main thread continues to run...");

        // Lấy kết quả từ Future, luồng chính sẽ bị block ở đây cho đến khi có kết quả
        String result = future.get();
        System.out.println("Received result: " + result);

        // Rất quan trọng: phải đóng executor service khi không dùng nữa
        executor.shutdown();
    }
}
```

**Vấn đề với `Future`**: Mặc dù tốt hơn, `Future` vẫn còn hạn chế. Rất khó để kết hợp nhiều `Future` với nhau hoặc xử lý kết quả một cách bất đồng bộ mà không block luồng chính.

---

## ✨ 4. Cách Hiện Đại: CompletableFuture

`CompletableFuture`, được giới thiệu trong Java 8, là câu trả lời cho những hạn chế của `Future`. Nó là một bước đột phá trong lập trình bất đồng bộ của Java.

### Các đặc điểm nổi bật

- **Non-blocking**: Xử lý kết quả ngay khi nó có sẵn mà không cần gọi `get()` và block luồng hiện tại.
- **Khả năng kết hợp (Composable)**: Dễ dàng xâu chuỗi các tác vụ bất đồng bộ với nhau.
- **Xử lý lỗi linh hoạt**: Cung cấp các phương thức để xử lý ngoại lệ một cách mượt mà.

### Ví dụ

Hãy tưởng tượng chúng ta cần thực hiện một chuỗi tác vụ:

1.  Lấy thông tin người dùng (bất đồng bộ).
2.  Dựa trên thông tin đó, lấy danh sách đơn hàng của họ (bất đồng bộ).
3.  Đếm số lượng đơn hàng.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

public class CompletableFutureExample {

    public static CompletableFuture<String> getUserInfo() {
        return CompletableFuture.supplyAsync(() -> {
            System.out.println("Getting user info...");
            sleep(1);
            return "User123"; // Giả lập kết quả
        });
    }

    public static CompletableFuture<Integer> getOrderCount(String userId) {
        return CompletableFuture.supplyAsync(() -> {
            System.out.println("Getting order count for " + userId);
            sleep(1);
            return 15; // Giả lập kết quả
        });
    }

    public static void main(String[] args) {
        System.out.println("Main thread starts.");

        getUserInfo()
            .thenCompose(userId -> getOrderCount(userId)) // thenCompose để xâu chuỗi các CompletableFuture
            .thenAccept(count -> { // thenAccept để xử lý kết quả cuối cùng
                System.out.println("Final result: User has " + count + " orders.");
            })
            .exceptionally(ex -> { // Xử lý lỗi
                System.err.println("An error occurred: " + ex.getMessage());
                return null;
            });

        System.out.println("Main thread continues without blocking.");

        // Chờ để chương trình không kết thúc sớm
        sleep(3);
        System.out.println("Main thread ends.");
    }

    private static void sleep(int seconds) {
        try {
            TimeUnit.SECONDS.sleep(seconds);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
```

Trong ví dụ trên, luồng `main` không hề bị block. Các tác vụ được thực thi trên một thread pool và kết quả được xử lý thông qua các callback (`thenCompose`, `thenAccept`).

---

## 🎯 Tổng kết

Lập trình đa luồng trong Java đã có một chặng đường phát triển dài:

- **🕰️ Cấp 1 (Cổ điển - `Thread`/`Runnable`)**: Nền tảng cơ bản nhưng quản lý thủ công, phức tạp và dễ lỗi.
- **🚀 Cấp 2 (Tốt hơn - `ExecutorService`)**: Tách biệt tác vụ và thực thi, quản lý luồng qua `ThreadPool`, nhưng `Future` còn hạn chế trong việc kết hợp.
- **✨ Cấp 3 (Hiện đại - `CompletableFuture`)**: Mạnh mẽ, linh hoạt, cho phép lập trình bất đồng bộ non-blocking và kết hợp các tác vụ một cách dễ dàng.

Việc nắm vững các công cụ này sẽ giúp bạn xây dựng được những ứng dụng hiệu năng cao và có khả năng phản hồi tốt.
