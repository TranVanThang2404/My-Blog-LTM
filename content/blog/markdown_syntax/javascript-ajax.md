+++
date = '2025-09-30T20:45:00+07:00'
draft = false
title = 'JavaScript AJAX'
description = 'Tìm hiểu JavaScript AJAX: gửi và nhận dữ liệu từ server mà không tải lại trang, ví dụ minh họa bằng Fetch API.'
tags = ["JavaScript", "AJAX", "Fetch API", "JSON", "Frontend"]
categories = ["JavaScript", "Frontend"]
icon = "/images/javascript-ajax.jpg"
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 12px;">
  <img src="/images/javascript-ajax.jpg" 
       alt="Javascript Ajax" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">Javascript Ajax</h2>
</div>

# 🔄 AJAX trong JavaScript

## 🧠 AJAX là gì?

**AJAX** (Asynchronous JavaScript and XML) là kỹ thuật cho phép **gửi và nhận dữ liệu từ server mà không cần tải lại toàn bộ trang web**. Mặc dù tên gọi là XML, ngày nay AJAX thường sử dụng **JSON** vì tính nhẹ và dễ xử lý hơn.

---

## ⚙️ Cách hoạt động của AJAX

1. **JavaScript** tạo request đến server (qua `XMLHttpRequest` hoặc `fetch`).
2. **Server** xử lý yêu cầu và trả về dữ liệu (thường là JSON hoặc text).
3. **JavaScript** nhận response và cập nhật nội dung trang (DOM) một cách động.

---

## 📦 Công cụ AJAX phổ biến

| Công cụ           | Mô tả |
|-------------------|------|
| `XMLHttpRequest`  | API truyền thống để gửi request bất đồng bộ |
| `fetch()`         | API hiện đại, dễ dùng, hỗ trợ Promise |
| `axios`           | Thư viện bên ngoài, hỗ trợ nhiều tính năng nâng cao |

---

## 💻 Ví dụ sử dụng Fetch API

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>AJAX với Fetch</title>
</head>
<body>
  <h2>Ví dụ AJAX với Fetch API</h2>
  <button onclick="loadData()">Tải dữ liệu</button>
  <div id="result" style="margin-top: 1rem; padding: 1rem; border: 1px solid #ccc;"></div>

  <script>
    function loadData() {
      fetch("data.txt")
        .then(response => {
          if (!response.ok) {
            throw new Error("Lỗi khi tải dữ liệu");
          }
          return response.text();
        })
        .then(data => {
          document.getElementById("result").innerHTML = data;
        })
        .catch(error => {
          console.error("Error:", error);
          document.getElementById("result").innerHTML = "Không thể tải dữ liệu.";
        });
    }
  </script>
</body>
</html>
```
# 📌 Ghi chú

- File data.txt có thể chứa nội dung văn bản hoặc HTML đơn giản.
- Nếu dùng JSON, bạn có thể thay response.text() bằng response.json() và xử lý dữ liệu như object.
- Fetch API hỗ trợ Promise nên dễ kết hợp với async/await.

# 📚 Tài liệu tham khảo

- [MDN Web Docs: Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)  
- [W3Schools: AJAX Tutorial](https://www.w3schools.com/js/js_ajax_intro.asp)  
- [GeeksforGeeks: AJAX in JavaScript](https://www.geeksforgeeks.org/ajax-in-javascript/)  