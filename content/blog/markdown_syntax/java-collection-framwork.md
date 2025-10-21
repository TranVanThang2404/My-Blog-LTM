+++
title = "Java Collections Framework"
author = "Van Thang"
date = "2025-09-30T22:20:00+07:00"
draft = false
description = "Giới thiệu về Java Collections Framework và ví dụ minh họa"
tags = ["java", "collections", "framework"]
categories = ["programming", "java"]
icon = "/images/java-collection.jpg"
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 12px;">
  <img src="/images/java-collection.jpg" 
       alt="Java Collections Framework" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">Java Collections Framework</h2>
</div>


# 📚 Java Collections Framework

**Collections Framework** trong Java là tập hợp các **class** và **interface** giúp làm việc với dữ liệu động như danh sách, tập hợp, hàng đợi và ánh xạ. Nó cung cấp các cấu trúc dữ liệu mạnh mẽ hơn mảng (`array`) và nhiều phương thức tiện lợi để thao tác dữ liệu.

---

## 🔑 1.Các Interface chính

| Interface | Mô tả | Ví dụ triển khai |
|-----------|-------|------------------|
| `List`    | Danh sách có thứ tự, cho phép phần tử trùng lặp | `ArrayList`, `LinkedList` |
| `Set`     | Tập hợp không trùng lặp, không đảm bảo thứ tự | `HashSet`, `TreeSet` |
| `Queue`   | Hàng đợi theo nguyên tắc FIFO | `PriorityQueue`, `LinkedList` |
| `Map`     | Lưu trữ cặp key-value, key không trùng lặp | `HashMap`, `TreeMap` |

---

## 💻 2.Ví dụ minh họa

```java
import java.util.*;

public class CollectionsExample {
    public static void main(String[] args) {
        // List - Cho phép trùng lặp, có thứ tự
        List<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Python");
        list.add("Java");
        System.out.println("List: " + list); // [Java, Python, Java]

        // Set - Không cho phép trùng lặp
        Set<String> set = new HashSet<>(list);
        System.out.println("Set: " + set); // [Java, Python]

        // Queue - FIFO
        Queue<String> queue = new LinkedList<>();
        queue.offer("Task1");
        queue.offer("Task2");
        queue.offer("Task3");
        System.out.println("Queue poll: " + queue.poll()); // Task1
        System.out.println("Remaining: " + queue); // [Task2, Task3]

        // Map - Key-Value pairs
        Map<Integer, String> map = new HashMap<>();
        map.put(1, "One");
        map.put(2, "Two");
        map.put(3, "Three");
        System.out.println("Map: " + map); // {1=One, 2=Two, 3=Three}
        System.out.println("Get key 2: " + map.get(2)); // Two
    }
}

```

---

# ⚖️ 3.So sánh Array vs Collections

| Đặc điểm | Array | Collections |
|----------|-------|-------------|
| Kích thước | Cố định | Động (tự động mở rộng) |
| Kiểu dữ liệu | Primitive & Object | Chỉ Object (wrapper class) |
| Hiệu năng | Nhanh hơn | Linh hoạt hơn |
| Phương thức | Hạn chế | Nhiều (sort, search, v.v.) |

---

# 📌 4.Lưu ý khi sử dụng

- **ArrayList** phù hợp cho truy xuất ngẫu nhiên nhanh
- **LinkedList** tốt cho thêm/xóa phần tử thường xuyên
- **HashSet** cho tìm kiếm nhanh, không quan tâm thứ tự
- **TreeSet** cho dữ liệu đã sắp xếp
- **HashMap** cho tra cứu key-value nhanh
- **TreeMap** cho key-value đã sắp xếp theo key

---

# 📚 5.Tài liệu tham khảo

- [Java Collections Framework - Oracle Docs](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/overview.html)
- [Java Collection Tutorial - GeeksforGeeks](https://www.geeksforgeeks.org/collections-in-java-2/)