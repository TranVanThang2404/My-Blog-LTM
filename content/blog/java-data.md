+++
title = "Java Data Types & Variables"
date = "2025-09-30T22:05:00+07:00"
draft = false
description = "Giới thiệu các kiểu dữ liệu và biến trong Java với ví dụ minh họa"
tags = ["java", "data types", "variables"]
categories = ["programming", "java"]
icon = "/images/java-data.jpg"
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 12px;">
  <img src="/images/java-data.jpg" 
       alt="Java Data Types Icon" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">Java Data Types & Variables</h2>
</div>

# 🧠 Biến và Kiểu Dữ Liệu trong Java

Trong Java, **biến (variable)** là vùng nhớ để lưu trữ dữ liệu, và **kiểu dữ liệu (data type)** xác định loại giá trị mà biến có thể lưu trữ. Java có hai nhóm kiểu dữ liệu chính:

- **Primitive Types** (kiểu nguyên thủy)
- **Reference Types** (kiểu tham chiếu)

---

## 1️⃣ Kiểu dữ liệu nguyên thủy (Primitive Types)

Java có 8 kiểu dữ liệu nguyên thủy:

| Kiểu      | Kích thước | Phạm vi                  | Mặc định | Mô tả                    |
|-----------|------------|--------------------------|----------|--------------------------|
| `byte`    | 8-bit      | -128 đến 127             | `0`      | Số nguyên nhỏ            |
| `short`   | 16-bit     | -32,768 đến 32,767       | `0`      | Số nguyên trung bình     |
| `int`     | 32-bit     | -2³¹ đến 2³¹-1           | `0`      | Số nguyên phổ biến nhất  |
| `long`    | 64-bit     | -2⁶³ đến 2⁶³-1           | `0L`     | Số nguyên lớn            |
| `float`   | 32-bit     | ~±3.4E+38                | `0.0f`   | Số thực độ chính xác đơn|
| `double`  | 64-bit     | ~±1.7E+308               | `0.0d`   | Số thực độ chính xác kép|
| `char`    | 16-bit     | 0 đến 65,535             | `'\u0000'`| Ký tự Unicode           |
| `boolean` | 1-bit      | `true` / `false`         | `false`  | Giá trị logic            |

---

## 2️⃣ Kiểu tham chiếu (Reference Types)

Lưu trữ **địa chỉ** của đối tượng trong bộ nhớ heap:

- `String` – Chuỗi ký tự
- `Array` – Mảng
- `Class` – Lớp
- `Interface` – Giao diện
- `Enum` – Kiểu liệt kê

📌 **Khác biệt:**
- `Primitive`: lưu giá trị trực tiếp trong stack
- `Reference`: lưu địa chỉ tham chiếu đến object trong heap

---

## 3️⃣ Khai báo và khởi tạo biến

```java
int age;
age = 21;

double salary = 5000.50;

int x = 10, y = 20, z = 30;

final double PI = 3.14159;
final int MAX_USERS = 100;
        
        System.out.println("Age: " + age);
        System.out.println("Salary: " + salary);
        System.out.println("PI: " + PI);
    }
}
```

---

# 4️⃣ Ví dụ chi tiết với tất cả kiểu dữ liệu

```java
byte smallNumber = 100;
short mediumNumber = 30000;
int age = 25;
long population = 8000000000L;

float price = 99.99f;
double pi = 3.141592653589793;

char grade = 'A';
char unicode = '\u0041';

boolean isJavaFun = true;

String name = "Nguyễn Văn A";
int[] numbers = {1, 2, 3};
String[] fruits = {"Táo", "Cam", "Chuối"};

```
---

# 5️⃣ Type Casting (Ép kiểu)

## 🔸 Widening (tự động)
```java
int myInt = 9;
double myDouble = myInt; // 9.0
```
## 🔸 Narrowing (thủ công)
```java
double myDouble = 9.78;
int myInt = (int) myDouble; // 9
```

---

# 6️⃣ Wrapper Classes

Mỗi primitive type đều có wrapper class tương ứng:

| Primitive | Wrapper Class |
|-----------|---------------|
| byte | Byte |
| short | Short |
| int | **Integer** |
| long | Long |
| float | Float |
| double | Double |
| char | **Character** |
| boolean | Boolean |

**Ví dụ:**
```java
Integer wrapperInt = 10; // Autoboxing
int primitiveInt = wrapperInt; // Unboxing
```

---

# 7️⃣ Phạm vi biến (Variable Scope)

- Local: trong method
- Instance: thuộc về object
- Static: thuộc về class

```java
class Example {
    int instanceVar = 10;
    static int staticVar = 20;

    void method() {
        int localVar = 30;
    }
}
```

---

# 8️⃣ Quy tắc đặt tên biến

## ✅ **Được phép:**
- Bắt đầu bằng chữ cái, `_`, hoặc `$`
- Chứa chữ cái, số, `_`, `$`
- Phân biệt hoa thường (`age` ≠ `Age`)

## ❌ **Không được phép:**
- Bắt đầu bằng số: `1age` ❌
- Chứa khoảng trắng: `my age` ❌
- Sử dụng từ khóa: `int`, `class`, `public` ❌

**Convention (Quy ước):**

- camelCase cho biến & method
- PascalCase cho class
- UPPER_SNAKE_CASE cho hằng số

---

# 9️⃣ So sánh Primitive vs Reference

```java
int a = 5;
int b = 5;
System.out.println(a == b); // true

String s1 = new String("Hello");
String s2 = new String("Hello");
System.out.println(s1 == s2); // false
System.out.println(s1.equals(s2)); // true

```

---

# 🔟 Lưu ý quan trọng

- Integer overflow: vượt giới hạn → quay vòng

- Float precision: không chính xác tuyệt đối

- Default values: chỉ áp dụng cho biến instance

---

# 📚 Tài liệu tham khảo

- [Java Data Types - Oracle Docs](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html)
- [Java Variables - W3Schools](https://www.w3schools.com/java/java_variables.asp)
- [Primitive Data Types - GeeksforGeeks](https://www.geeksforgeeks.org/data-types-in-java/)