+++
date = '2025-10-21T14:30:00+07:00'
draft = false
title = 'JavaScript Loops'
description = 'Tổng hợp các loại vòng lặp trong JavaScript: for, while, do...while, for...in, for...of, forEach. Giải thích chi tiết, ví dụ minh họa, bảng so sánh và lưu ý khi sử dụng.'
tags = ["JavaScript", "Loop", "for", "while", "forEach"]
categories = ["JavaScript", "Cơ bản"]
icon = "/images/js-loops.jpg"
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #f7971e 0%, #ffd200 100%); border-radius: 12px;">
  <img src="/images/js-loops.jpg" 
       alt="JavaScript Loop" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">JavaScript Loops</h2>
</div>

# 🔁 I. Tổng quan về vòng lặp

Vòng lặp giúp bạn thực thi một đoạn mã nhiều lần mà không cần viết lại. Đây là công cụ quan trọng trong xử lý dữ liệu, duyệt mảng, và tự động hóa tác vụ.

---

# 🧠 II. Các loại vòng lặp phổ biến

## 🔸 1. `for` loop – vòng lặp xác định số lần

```javascript
for (let i = 0; i < 5; i++) {
  console.log("Lần thứ", i);
}
```

## 🔸 2. while loop – lặp khi điều kiện đúng

```javascript
let i = 0;
while (i < 5) {
  console.log("Lần thứ", i);
  i++;
}
```

## 🔸 3. do...while loop – luôn chạy ít nhất một lần

```javascript
let i = 0;
do {
  console.log("Lần thứ", i);
  i++;
} while (i < 5);
```

## 🔸 4. for...in – duyệt key trong object

```javascript
const person = { name: "Trần", age: 25 };
for (let key in person) {
  console.log(key, ":", person[key]);
}
```

## 🔸 5. for...of – duyệt giá trị trong iterable

```javascript
const fruits = ["Táo", "Chuối", "Xoài"];
for (let fruit of fruits) {
  console.log(fruit);
}
```

## 🔸 6. forEach() – duyệt mảng hiện đại

```javascript
const numbers = [1, 2, 3];
numbers.forEach((num, index) => {
  console.log(`Phần tử thứ ${index}: ${num}`);
});
```

# 📊 III. So sánh các loại vòng lặp

| **Vòng lặp**   | **Duyệt gì?**         | **Có thể break?** | **Ưu điểm chính**                              |
|----------------|------------------------|--------------------|------------------------------------------------|
| `for`          | Số lần cụ thể          | ✅                 | Linh hoạt, kiểm soát tốt                       |
| `while`        | Điều kiện động         | ✅                 | Dễ dùng khi không biết số lần lặp              |
| `do...while`   | Điều kiện động         | ✅                 | Luôn chạy ít nhất một lần                      |
| `for...in`     | Object (key)           | ✅                 | Duyệt thuộc tính object                        |
| `for...of`     | Iterable (value)       | ✅                 | Duyệt giá trị trong mảng, string, Set          |
| `forEach()`    | Mảng                   | ❌                 | Ngắn gọn, hiện đại, không break được           |


# ⚠️ IV. Lưu ý khi sử dụng

- Tránh vòng lặp vô hạn (while(true)) nếu không có break.
- Dùng continue để bỏ qua vòng lặp hiện tại.
- Không dùng for...in để duyệt mảng (có thể duyệt cả prototype).
- forEach() không hỗ trợ break hoặc return.

# 📚 V. Tài liệu tham khảo

- [MDN Web Docs – Loops and iteration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)  
- [JavaScript.info – Loops](https://javascript.info/while-for)  
- [W3Schools – JavaScript Loops](https://www.w3schools.com/js/js_loop_for.asp)  