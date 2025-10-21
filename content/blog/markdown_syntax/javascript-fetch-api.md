+++
date = '2025-09-30T21:10:00+07:00'
draft = false
title = 'JavaScript Fetch API'
description = 'Hướng dẫn JavaScript Fetch API: gửi HTTP request hiện đại, sử dụng Promise và async/await, ví dụ lấy dữ liệu từ JSONPlaceholder.'
tags = ["JavaScript", "Fetch API", "AJAX", "JSON", "Frontend"]
categories = ["JavaScript", "Frontend"]
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 12px;">
  <img src="/images/javascript-fetch-api.jpg" 
       alt="Javascript Fetch API" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">Javascript Fetch API</h2>
</div>

<div class="image-container" style="text-align: center; margin: 2rem auto; max-width: 800px;">
  <img src="/images/javascript-fetch-api.jpg" 
       alt="Java Fetch API" 
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