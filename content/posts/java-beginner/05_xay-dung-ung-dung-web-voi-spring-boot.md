---
title: "Bài 5: Xây Dựng Ứng Dụng Web Với Spring Boot"
date: "2025-10-17T09:00:00+07:00"
draft: false
summary: "Hướng dẫn xây dựng RESTful API đơn giản với Spring Boot, từ khởi tạo dự án, tạo Model, Repository, Controller đến kết nối cơ sở dữ liệu."
tags: ["Java", "Spring Boot", "REST API", "Web Development", "JPA"]
categories: ["Lập trình Java"]
series: ["Java Cho Người Mới Bắt Đầu"]
series_order: 5
featureAsset: "img/java-logo.png"
---

Spring Framework từ lâu đã là một thế lực trong thế giới Java để xây dựng các ứng dụng doanh nghiệp mạnh mẽ. Tuy nhiên, việc cấu hình Spring "truyền thống" có thể khá phức tạp và dài dòng. Spring Boot ra đời để giải quyết vấn đề này, mang đến một cách tiếp cận nhanh chóng và hiệu quả để tạo ra các ứng dụng Spring độc lập, sẵn sàng để chạy (production-ready).

Bài viết này sẽ hướng dẫn bạn các bước cơ bản để xây dựng một ứng dụng web RESTful API đơn giản bằng Spring Boot, từ việc khởi tạo dự án đến việc kết nối cơ sở dữ liệu.

---

## 🤔 1. Tại Sao Lại Là Spring Boot?

Spring Boot không phải là một framework mới thay thế Spring, mà là một dự án con của Spring giúp đơn giản hóa quá trình phát triển với những ưu điểm chính:

- **Tự động cấu hình (Auto-configuration)**: Tự động cấu hình ứng dụng dựa trên các thư viện bạn thêm vào. Ví dụ, có `spring-boot-starter-web` thì sẽ tự cấu hình Tomcat và Spring MVC.
- **"Opinionated" Defaults**: Đưa ra các cấu hình mặc định hợp lý, giúp bạn bắt đầu nhanh chóng theo triết lý "Convention over Configuration" (Ưu tiên quy ước hơn cấu hình).
- **Máy chủ nhúng (Embedded Server)**: Đi kèm các máy chủ nhúng như Tomcat, Jetty, không cần triển khai file WAR ra bên ngoài.
- **Hệ sinh thái Starter**: Cung cấp các `starter` dependencies để đơn giản hóa việc quản lý build. Ví dụ, chỉ cần `spring-boot-starter-data-jpa` là có đủ mọi thứ để làm việc với JPA và Hibernate.

---

## 🚀 2. Khởi Tạo Dự Án

Cách dễ nhất để tạo một dự án Spring Boot là sử dụng **Spring Initializr**.

1.  Truy cập <https://start.spring.io>.
2.  Chọn các thông số cho dự án của bạn:
    - **Project**: Maven
    - **Language**: Java
    - **Spring Boot**: Chọn phiên bản ổn định (không chọn SNAPSHOT).
    - **Project Metadata**: Điền `Group`, `Artifact` (tên dự án, ví dụ: `demo-api`).
    - **Packaging**: Jar
    - **Java**: Chọn phiên bản LTS (ví dụ: 17, 21).
3.  Trong phần **Dependencies**, nhấn "ADD DEPENDENCIES" và thêm:
    - **Spring Web**: Để xây dựng ứng dụng web và RESTful API.
    - **Spring Data JPA**: Để làm việc với cơ sở dữ liệu quan hệ.
    - **H2 Database**: Một cơ sở dữ liệu trong bộ nhớ (in-memory), rất tiện cho việc phát triển.
4.  Nhấn **GENERATE**. Một file `.zip` sẽ được tải về. Hãy giải nén và mở nó bằng IDE yêu thích của bạn.

---

## 🛠️ 3. Tạo REST API Đầu Tiên

Một REST API cho phép các hệ thống khác nhau giao tiếp với nhau qua giao thức HTTP. Chúng ta sẽ tạo một API đơn giản để quản lý danh sách `Product`.

### Bước 1: Tạo Model Product

Tạo một file `Product.java` để định nghĩa đối tượng của chúng ta.

```java
// src/main/java/com/example/demoapi/Product.java
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.Id;

@Entity // Đánh dấu đây là một JPA entity (tương ứng với một bảng trong CSDL)
public class Product {
    @Id // Đánh dấu đây là khóa chính
    @GeneratedValue // Tự động tạo giá trị cho khóa chính
    private Long id;
    private String name;
    private double price;

    // Constructors, Getters, Setters... (Có thể dùng Lombok để tự động tạo)
    // Constructor mặc định là bắt buộc đối với JPA
    public Product() {}

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    // ... getters and setters
    public Long getId() { return id; }
    public void setId(Long id) { this.id = id; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public double getPrice() { return price; }
    public void setPrice(double price) { this.price = price; }
}
```

### Bước 2: Tạo Repository

Repository là một interface chịu trách nhiệm giao tiếp với cơ sở dữ liệu. Spring Data JPA sẽ tự động tạo ra các phương thức CRUD (Create, Read, Update, Delete) cho chúng ta.

Tạo một interface `ProductRepository.java`.

```java
// src/main/java/com/example/demoapi/ProductRepository.java
import org.springframework.data.jpa.repository.JpaRepository;

public interface ProductRepository extends JpaRepository<Product, Long> {
    // JpaRepository<Kiểu_Entity, Kiểu_Khóa_Chính>
    // Spring Data JPA sẽ tự động cung cấp các phương thức như save(), findById(), findAll()...
}
```

Thật vậy, chỉ cần định nghĩa interface như vậy là đủ!

### Bước 3: Tạo Controller

Controller là nơi xử lý các request HTTP từ client và trả về response.

Tạo file `ProductController.java`.

```java
// src/main/java/com/example/demoapi/ProductController.java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;
import java.util.List;

@RestController // Đánh dấu đây là một REST controller, các phương thức sẽ trả về JSON
@RequestMapping("/api/products") // Tất cả các endpoint trong class này sẽ có tiền tố /api/products
public class ProductController {

    @Autowired // Spring sẽ tự động inject (tiêm) một instance của ProductRepository vào đây
    private ProductRepository productRepository;

    // GET /api/products -> Lấy tất cả sản phẩm
    @GetMapping
    public List<Product> getAllProducts() {
        return productRepository.findAll();
    }

    // POST /api/products -> Tạo một sản phẩm mới
    @PostMapping
    public Product createProduct(@RequestBody Product product) {
        // @RequestBody sẽ chuyển đổi JSON từ request body thành đối tượng Product
        return productRepository.save(product);
    }
}
```

**Dependency Injection (`@Autowired`)**: Thay vì tự tạo `new ProductRepository()`, chúng ta để Spring IoC container quản lý và "tiêm" nó vào khi cần. Đây là một khái niệm cốt lõi của Spring.

---

## 🏃 4. Chạy Và Kiểm Tra Ứng Dụng

Bây giờ, hãy mở file `DemoApiApplication.java` và nhấn nút "Run". Spring Boot sẽ khởi động máy chủ Tomcat nhúng trên cổng `8080`.

Bạn có thể dùng các công cụ như `curl` hoặc Postman để kiểm tra API:

#### Tạo một sản phẩm mới (POST)

- **URL**: `POST http://localhost:8080/api/products`
- **Body** (JSON):

```json
{
  "name": "Laptop Pro",
  "price": 1200.5
}
```

Bạn sẽ nhận lại đối tượng vừa tạo, có kèm theo `id`.

#### Lấy tất cả sản phẩm (GET)

- **URL**: `GET http://localhost:8080/api/products`

Bạn sẽ nhận lại một mảng JSON chứa tất cả sản phẩm có trong cơ sở dữ liệu H2.

---

## 🎯 Tổng kết

Chỉ với vài bước đơn giản, bạn đã xây dựng được một REST API hoàn chỉnh. Đây chính là sức mạnh của Spring Boot: giúp bạn tập trung vào logic nghiệp vụ thay vì sa đà vào việc cấu hình.

- **🚀 Khởi tạo**: Dùng **Spring Initializr** để tạo dự án nhanh chóng với các `starter` cần thiết (`Web`, `JPA`).
- **🛠️ Xây dựng**:
  - **Model (`@Entity`)**: Định nghĩa đối tượng dữ liệu.
  - **Repository (`JpaRepository`)**: Giao tiếp với cơ sở dữ liệu mà không cần viết code SQL.
  - **Controller (`@RestController`)**: Xử lý request HTTP và định nghĩa các API endpoint (`@GetMapping`, `@PostMapping`).
- **🏃 Chạy**: Spring Boot tự khởi động máy chủ nhúng, sẵn sàng để kiểm thử.

Từ nền tảng này, bạn có thể tiếp tục khám phá các khía cạnh khác của hệ sinh thái Spring như Spring Security (bảo mật), validation, exception handling, và nhiều hơn nữa. Chúc mừng bạn đã bắt đầu hành trình với một trong những framework Java mạnh mẽ nhất hiện nay!
