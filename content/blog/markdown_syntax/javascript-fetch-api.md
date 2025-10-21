+++
date = '2025-09-30T21:10:00+07:00'
draft = false
title = 'JavaScript Fetch API'
description = 'Hướng dẫn JavaScript Fetch API: gửi HTTP request hiện đại, sử dụng Promise và async/await, ví dụ lấy dữ liệu từ JSONPlaceholder.'
tags = ["JavaScript", "Fetch API", "AJAX", "JSON", "Frontend"]
categories = ["JavaScript", "Frontend"]
icon = "/images/javascript-fetch-api.jpg"
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 12px;">
  <img src="/images/javascript-fetch-api.jpg" 
       alt="Javascript Fetch API" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">Javascript Fetch API</h2>
</div>

# 🚀 JavaScript Fetch API – Gửi HTTP Request hiện đại

## 🧠 Giới thiệu

**Fetch API** là chuẩn hiện đại trong JavaScript để gửi HTTP request đến server. Nó thay thế `XMLHttpRequest` với cú pháp đơn giản hơn, hỗ trợ **Promise** và dễ dàng kết hợp với **async/await**.

---

## 🔍 Ưu điểm của Fetch API

- Cú pháp gọn gàng, dễ đọc.
- Hỗ trợ Promise và async/await.
- Dễ xử lý lỗi với `.catch()` hoặc `try...catch`.
- Hỗ trợ các phương thức HTTP: GET, POST, PUT, DELETE...
- Tương thích tốt với API RESTful và JSON.

---

## ⚙️ Cách hoạt động

1. JavaScript gọi `fetch()` để gửi request.
2. Server xử lý và trả về dữ liệu (thường là JSON).
3. JavaScript nhận response và cập nhật nội dung trang (DOM) mà không cần reload.

---

## 📦 Cấu trúc cú pháp cơ bản

```javascript
fetch(url, options)
  .then(response => {
    if (!response.ok) throw new Error("HTTP error " + response.status);
    return response.json(); // hoặc response.text()
  })
  .then(data => {
    // xử lý dữ liệu
  })
  .catch(error => {
    // xử lý lỗi
  });
```

### 💻 Ví dụ GET: Lấy dữ liệu từ JSONPlaceholder

```html
<button onclick="getPost()">Tải bài viết</button>
<div id="result"></div>

<script>
async function getPost() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
    if (!response.ok) throw new Error("Lỗi HTTP: " + response.status);
    const data = await response.json();
    document.getElementById("result").innerHTML = `
      <h3>${data.title}</h3>
      <p>${data.body}</p>
    `;
  } catch (error) {
    console.error("Lỗi khi fetch:", error);
    document.getElementById("result").innerText = "Không thể tải dữ liệu.";
  }
}
</script>
```

### 📝 Ví dụ POST: Gửi dữ liệu lên server

```javascript
async function createPost() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts", {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        title: "Tiêu đề mới",
        body: "Nội dung bài viết",
        userId: 1
      })
    });

    const result = await response.json();
    console.log("Server trả về:", result);
  } catch (error) {
    console.error("Lỗi khi gửi POST:", error);
  }
}
```

## 🔐 Xử lý lỗi nâng cao

- Kiểm tra response.ok để biết request có thành công không.
- Dùng try...catch để bắt lỗi mạng hoặc cú pháp.
- Có thể hiển thị thông báo lỗi cho người dùng.

## 🧪 So sánh Fetch API vs XMLHttpRequest

| Tiêu chí            | Fetch API                  | XMLHttpRequest               |
|---------------------|----------------------------|------------------------------|
| Cú pháp             | Gọn gàng, hiện đại         | Dài dòng, phức tạp           |
| Hỗ trợ Promise      | ✅ Có                      | ❌ Không                     |
| Hỗ trợ async/await  | ✅ Có                      | ❌ Không                     |
| Xử lý lỗi           | Dễ với `.catch()`          | Phải dùng callback phức tạp |
| Tính mở rộng        | Dễ tích hợp với API REST   | Khó mở rộng                 |

## 📚 Tài liệu tham khảo

- [MDN Web Docs: Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)  
- [W3Schools: AJAX Tutorial](https://www.w3schools.com/js/js_ajax_intro.asp)  
- [GeeksforGeeks: AJAX in JavaScript](https://www.geeksforgeeks.org/ajax-in-javascript/)  