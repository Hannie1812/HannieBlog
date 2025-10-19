---
title: "Bài 2: Lập Trình Hướng Đối Tượng (OOP) Trong Java"
date: "2025-10-14T09:00:00+07:00"
draft: false
summary: "Tìm hiểu sâu về 4 trụ cột của OOP trong Java: Tính đóng gói, Kế thừa, Đa hình và Trừu tượng, với các ví dụ thực tế."
tags: ["Java", "OOP", "Lập Trình Hướng Đối Tượng", "Core Java"]
categories: ["Lập trình Java"]
series: ["Java Cho Người Mới Bắt Đầu"]
series_order: 2
featureAsset: "img/java-logo.png"
---

## 🤔 OOP là gì?

Lập Trình Hướng Đối Tượng (OOP) Trong Java: Từ Lý Thuyết Đến Thực Tiễn

Lập trình hướng đối tượng (Object-Oriented Programming - OOP) không chỉ là một tính năng của Java, mà nó chính là triết lý, là xương sống của ngôn ngữ này. Hiểu rõ và vận dụng thành thạo các nguyên tắc OOP sẽ giúp bạn viết mã nguồn có cấu trúc, dễ bảo trì, dễ mở rộng và có khả năng tái sử dụng cao.

Bài viết này sẽ đi sâu vào bốn trụ cột của OOP trong Java: Tính đóng gói (Encapsulation), Tính kế thừa (Inheritance), Tính đa hình (Polymorphism), và Tính trừu tượng (Abstraction).

---

## 📦 1. Tính Đóng Gói (Encapsulation)

### Khái niệm

Tính đóng gói là kỹ thuật **che giấu thông tin** (data hiding) và các chi tiết triển khai của một đối tượng, chỉ cho phép tương tác với nó thông qua các phương thức công khai (public methods).

Hãy tưởng tượng một chiếc xe hơi. Bạn không cần biết động cơ, hộp số hoạt động chi tiết như thế nào. Bạn chỉ cần sử dụng vô lăng, chân ga, chân phanh – đó chính là các "giao diện" công khai.

Trong Java, chúng ta thực hiện đóng gói bằng cách:

- Khai báo các thuộc tính (biến) là `private`.
- Cung cấp các phương thức `public` để truy cập và thay đổi các thuộc tính đó (thường gọi là getters và setters).

### Ví dụ

```java
public class Student {
    // Thuộc tính được che giấu, không thể truy cập trực tiếp từ bên ngoài
    private String name;
    private int age;

    // Getter: Phương thức public để lấy giá trị của 'name'
    public String getName() {
        return this.name;
    }

    // Setter: Phương thức public để thiết lập giá trị cho 'name'
    // Có thể thêm logic kiểm tra dữ liệu ở đây
    public void setName(String name) {
        if (name != null && !name.trim().isEmpty()) {
            this.name = name;
        }
    }

    // Tương tự cho age
    public int getAge() {
        return this.age;
    }

    public void setAge(int age) {
        if (age > 0) {
            this.age = age;
        }
    }
}
```

### Lợi ích

- **Bảo vệ dữ liệu**: Ngăn chặn việc thay đổi dữ liệu một cách tùy tiện.
- **Tăng tính linh hoạt**: Bạn có thể thay đổi cách triển khai bên trong một lớp mà không ảnh hưởng đến các lớp khác đang sử dụng nó.
- **Dễ kiểm soát**: Logic kiểm tra dữ liệu có thể được đặt trong các phương thức setter.

---

## 👨‍👩‍👧‍👦 2. Tính Kế Thừa (Inheritance)

### Khái niệm

Tính kế thừa cho phép một lớp (gọi là **lớp con** - subclass) thừa hưởng lại các thuộc tính và phương thức của một lớp khác (gọi là **lớp cha** - superclass).

Kế thừa tạo ra mối quan hệ **"is-a"** (là một). Ví dụ, một `Dog` (Chó) "là một" `Animal` (Động vật). `Dog` sẽ có những đặc điểm chung của `Animal` (như ăn, ngủ) và có những đặc điểm riêng (như sủa).

Trong Java, chúng ta sử dụng từ khóa `extends` để thực hiện kế thừa.

### Ví dụ

```java
// Lớp cha (Superclass)
public class Animal {
    private String name;

    public Animal(String name) {
        this.name = name;
    }

    public void eat() {
        System.out.println(name + " is eating.");
    }

    public String getName() {
        return name;
    }
}

// Lớp con (Subclass) kế thừa từ Animal
public class Dog extends Animal {
    // Gọi constructor của lớp cha
    public Dog(String name) {
        super(name); // 'super' dùng để tham chiếu đến lớp cha
    }

    // Phương thức riêng của Dog
    public void bark() {
        // getName() được kế thừa từ Animal
        System.out.println(getName() + " is barking: Woof! Woof!");
    }
}
```

### Lợi ích

- **Tái sử dụng mã**: Không cần phải viết lại các thuộc tính và phương thức đã có ở lớp cha.
- **Tổ chức mã nguồn**: Tạo ra một hệ thống phân cấp logic, dễ hiểu.

---

## 🎭 3. Tính Đa Hình (Polymorphism)

### Khái niệm

Đa hình có nghĩa là "nhiều hình thái". Trong OOP, nó cho phép một đối tượng có thể được thể hiện dưới nhiều dạng khác nhau. Hành vi của một phương thức có thể thay đổi tùy thuộc vào đối tượng gọi nó.

Tính đa hình trong Java thường được thể hiện qua **ghi đè phương thức (Method Overriding)**.

### Ví dụ

Hãy mở rộng ví dụ về `Animal`. Cả `Dog` và `Cat` đều là `Animal` và đều có thể phát ra âm thanh, nhưng cách chúng phát ra âm thanh thì khác nhau.

```java
public class Animal {
    public void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

public class Dog extends Animal {
    @Override // Chú thích cho biết đây là phương thức ghi đè
    public void makeSound() {
        System.out.println("Dog barks: Woof! Woof!");
    }
}

public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Cat meows: Meow! Meow!");
    }
}

// Sử dụng tính đa hình
public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal();
        Animal myDog = new Dog(); // Một đối tượng Dog cũng là một Animal
        Animal myCat = new Cat(); // Một đối tượng Cat cũng là một Animal

        myAnimal.makeSound(); // Output: Animal makes a sound
        myDog.makeSound();    // Output: Dog barks: Woof! Woof!
        myCat.makeSound();    // Output: Cat meows: Meow! Meow!
    }
}
```

Cùng một lời gọi phương thức makeSound() nhưng kết quả lại khác nhau tùy thuộc vào đối tượng thực sự là gì (Dog hay Cat).

---

## 🎨 4. Tính Trừu Tượng (Abstraction)

### Khái niệm

Tính trừu tượng là quá trình **che giấu các chi tiết triển khai phức tạp** và chỉ hiển thị những thông tin cần thiết ra bên ngoài. Kế thừa cho thấy mối quan hệ "is-a", còn trừu tượng định nghĩa ra một "bản thiết kế" chung.

Trong Java, chúng ta đạt được tính trừu tượng thông qua **lớp trừu tượng (abstract class)** và **giao diện (interface)**.

### Abstract Class vs Interface

- **Abstract Class**: Là một lớp không thể khởi tạo đối tượng, nó hoạt động như một khuôn mẫu cho các lớp con. Nó có thể chứa cả phương thức trừu tượng (không có thân hàm) và phương thức thông thường.
- **Interface**: Là một bản thiết kế hoàn toàn trừu tượng. Nó chỉ chứa các phương thức trừu tượng và các hằng số. Một lớp có thể `implements` (triển khai) nhiều interface.

### Ví dụ với Interface

```java
// Interface định nghĩa hành vi "có thể bay"
interface Flyable {
    void fly(); // Mặc định là public abstract
}

// Lớp Airplane cũng triển khai interface Flyable
class Airplane implements Flyable {
    @Override
    public void fly() {
        System.out.println("Airplane is flying with engines.");
    }
}

// Lớp Bird triển khai interface Flyable
class Bird implements Flyable {
    @Override
    public void fly() {
        System.out.println("Bird is flying with wings.");
    }
}
```

### Khi nào dùng?

- Dùng **abstract class** khi bạn muốn chia sẻ mã nguồn chung giữa các lớp con có liên quan chặt chẽ.
- Dùng **interface** khi bạn muốn định nghĩa một "hợp đồng" về hành vi mà các lớp không liên quan có thể cùng triển khai.

---

## 🎯 Tổng kết

Để trở thành một lập trình viên Java giỏi, việc nắm vững 4 nguyên tắc OOP là điều bắt buộc.

- **📦 Tính Đóng Gói**: Che giấu dữ liệu, bảo vệ trạng thái của đối tượng.
- **👨‍👩‍👧‍👦 Tính Kế Thừa**: Tái sử dụng code và tạo ra hệ thống phân cấp logic.
- **🎭 Tính Đa Hình**: Cho phép hành vi của phương thức thay đổi tùy theo đối tượng.
- **🎨 Tính Trừu Tượng**: Che giấu sự phức tạp, tập trung vào "cái gì" thay vì "như thế nào".
