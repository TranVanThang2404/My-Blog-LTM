+++
date = '2025-09-30T21:50:00+07:00'
draft = false
title = 'OOP trong JavaScript'
description = 'Tìm hiểu OOP trong JavaScript: class, encapsulation, inheritance, polymorphism, abstraction với ví dụ minh họa.'
tags = ["JavaScript", "OOP", "Programming", "ES6"]
categories = ["JavaScript", "Programming"]
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 12px;">
  <img src="/images/java-oop.jpg" 
       alt="Java OOP" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">Java OOP</h2>
</div>

<div class="image-container" style="text-align: center; margin: 2rem auto; max-width: 800px;">
  <img src="/images/java-oop.jpg" 
       alt="Java OOP" 
       class="zoomable-image"
       style="width: 100%; height: auto; object-fit: contain; cursor: zoom-in; border-radius: 12px; box-shadow: 0 8px 16px rgba(0,0,0,0.2); transition: transform 0.3s ease, box-shadow 0.3s ease;"
       onmouseover="this.style.transform='scale(1.02)'; this.style.boxShadow='0 12px 24px rgba(0,0,0,0.3)'"
       onmouseout="this.style.transform='scale(1)'; this.style.boxShadow='0 8px 16px rgba(0,0,0,0.2)'"
       onclick="openImageModal(this.src, this.alt)"/>
  <p style="font-size: 0.9em; color: #888; margin-top: 1rem; font-style: italic;">💡 Click vào ảnh để xem phóng to</p>
</div>

<div id="imageModal" class="image-modal" onclick="closeImageModal()" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.95); cursor: zoom-out;">
  <img id="modalImage" style="margin: auto; display: block; max-width: 95%; max-height: 95%; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); border-radius: 8px;"/>
  <span style="position: absolute; top: 20px; right: 35px; color: #f1f1f1; font-size: 40px; font-weight: bold; cursor: pointer;" onclick="closeImageModal()">&times;</span>
</div>

<script>
function openImageModal(src, alt) {
  const modal = document.getElementById('imageModal');
  const modalImg = document.getElementById('modalImage');
  modal.style.display = 'block';
  modalImg.src = src;
  modalImg.alt = alt;
  document.body.style.overflow = 'hidden';
}

function closeImageModal() {
  document.getElementById('imageModal').style.display = 'none';
  document.body.style.overflow = 'auto';
}

document.addEventListener('keydown', function(event) {
  if (event.key === 'Escape') {
    closeImageModal();
  }
});
</script>

# 🧠 Tổng quan về Lập trình Hướng đối tượng (OOP) trong Java

Java là ngôn ngữ lập trình hướng đối tượng hoàn toàn, nghĩa là mọi chương trình đều được xây dựng dựa trên các khái niệm như class, object, kế thừa, đa hình, đóng gói và trừu tượng hóa.

---

## 🔑 4 Tính chất cốt lõi của OOP

| Tính chất       | Mô tả |
|----------------|------|
| **Encapsulation** | Đóng gói dữ liệu và phương thức liên quan vào một class. Giúp bảo vệ dữ liệu khỏi truy cập trái phép. |
| **Inheritance**   | Cho phép một class kế thừa thuộc tính và hành vi từ class khác. |
| **Polymorphism**  | Cho phép đối tượng có nhiều hình thức: ghi đè (overriding) và nạp chồng (overloading). |
| **Abstraction**   | Ẩn chi tiết triển khai, chỉ hiển thị hành vi cần thiết thông qua interface hoặc abstract class. |

---

## 🧱 1. Class và Object

```java
class Person {
    String name;
    int age;

    void sayHello() {
        System.out.println("Xin chào, tôi là " + name);
    }
}

public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        p.name = "Trần";
        p.age = 25;
        p.sayHello(); // Output: Xin chào, tôi là Trần
    }
}
```
# 🔐 2. Encapsulation (Đóng gói)

```java
class Account {
    private double balance;

    public void deposit(double amount) {
        if (amount > 0) balance += amount;
    }

    public double getBalance() {
        return balance;
    }
}
```

# 🧬 3. Inheritance (Kế thừa)

```java
class Animal {
    void eat() {
        System.out.println("Đang ăn...");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Gâu gâu!");
    }
}
```

# 🔁 4. Polymorphism (Đa hình)

## 🔸 Overriding (Ghi đè)

```java
class Animal {
    void sound() {
        System.out.println("Âm thanh...");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Meo meo!");
    }
}
```
## 🔸 Overloading (Nạp chồng)

```java 
class MathUtil {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```
# 🧩 5. Abstraction (Trừu tượng)

## 🔸 Abstract Class

```java
abstract class Shape {
    abstract double area();
}

class Circle extends Shape {
    double radius;

    Circle(double r) {
        radius = r;
    }

    double area() {
        return Math.PI * radius * radius;
    }
}
```

## 🔸 Interface

```java
interface Drawable {
    void draw();
}

class Square implements Drawable {
    public void draw() {
        System.out.println("Vẽ hình vuông");
    }
}
```

# 🧠 6.Các tính năng nâng cao

| Tính năng     | Mô tả                                           |
|---------------|--------------------------------------------------|
| `final`       | Ngăn ghi đè phương thức hoặc kế thừa class       |
| `static`      | Thuộc về class thay vì instance cụ thể           |
| `this`        | Tham chiếu đến đối tượng hiện tại                |
| `super`       | Gọi constructor hoặc phương thức từ class cha    |
| `instanceof`  | Kiểm tra kiểu đối tượng tại runtime              |
| `constructor` | Hàm khởi tạo khi tạo object mới từ class         |

# 📚 7.Tài liệu tham khảo

- [GeeksforGeeks: Java OOP Concepts](https://www.geeksforgeeks.org/java/object-oriented-programming-oops-concept-in-java/)  
- [W3Schools: Java OOP Tutorial](https://www.w3schools.com/java/java_oop.asp)  
- [FreeCodeCamp: Beginner’s Guide to Java OOP](https://www.freecodecamp.org/news/object-oriented-programming-concepts-java/)  
