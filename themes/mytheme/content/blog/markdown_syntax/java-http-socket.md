+++
date = '2025-09-30T20:30:00+07:00'
draft = false
title = 'Java HTTP Socket'
description = 'Hướng dẫn sử dụng Java Socket để gửi HTTP request và nhận HTTP response. Ví dụ minh họa client và server HTTP bằng Java.'
tags = ["Java", "Socket", "HTTP", "Network"]
categories = ["Java", "Networking"]
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 12px;">
  <img src="/images/java-http-socket.png" 
       alt="Java HTTP Socket" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">Java HTTP Socket</h2>
</div>

<div class="image-container" style="text-align: center; margin: 2rem auto; max-width: 800px;">
  <img src="/images/java-http-socket.png" 
       alt="Java HTTP Socket" 
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

# 🧠 I. Tổng quan về Socket và HTTP trong Java

## 🔹 1. Socket là gì?
Socket là điểm cuối của một kết nối hai chiều giữa hai chương trình chạy trên mạng.

Java cung cấp các lớp trong gói `java.net` để làm việc với socket:

- `Socket`: Dành cho client kết nối đến server.
- `ServerSocket`: Dành cho server lắng nghe kết nối từ client.
- `DatagramSocket`: Dùng cho giao thức UDP (không kết nối).

## 🔹 2. HTTP là gì?
HTTP (HyperText Transfer Protocol) là giao thức ứng dụng phổ biến nhất dùng để truyền dữ liệu qua web.

HTTP hoạt động trên nền TCP, nên bạn có thể xây dựng một HTTP server bằng cách sử dụng TCP socket.

---

# 🛠️ II. Xây dựng HTTP Server bằng Java Socket

## 🔸 1. Cấu trúc cơ bản của HTTP Request/Response

**Request từ client (trình duyệt):**
- GET / HTTP/1.1 
- Host: localhost:8080 
- User-Agent: Mozilla/5.0

**Response từ server:**
- HTTP/1.1 200 OK 
- Content-Type: text/html 
- Content-Length: 123
<html>...</html>


## 🔸 2. Ví dụ: HTTP Server đơn giản

```java
import java.io.*;
import java.net.*;

public class SimpleHttpServer {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(8080);
        System.out.println("Server đang chạy tại cổng 8080...");

        while (true) {
            Socket client = serverSocket.accept();
            new Thread(() -> handleClient(client)).start();
        }
    }

    private static void handleClient(Socket client) {
        try (
            BufferedReader in = new BufferedReader(new InputStreamReader(client.getInputStream()));
            PrintWriter out = new PrintWriter(client.getOutputStream())
        ) {
            String line;
            while (!(line = in.readLine()).isEmpty()) {
                System.out.println(line);
            }

            String response = "<html><body><h1>Hello from Java HTTP Server!</h1></body></html>";
            out.println("HTTP/1.1 200 OK");
            out.println("Content-Type: text/html");
            out.println("Content-Length: " + response.length());
            out.println();
            out.println(response);
            out.flush();
            client.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
---

# 🔄 III. Xây dựng HTTP Client bằng Java Socket

## 📌 Mục tiêu
Tạo một chương trình Java đóng vai trò là **HTTP Client** – tức là gửi yêu cầu HTTP đến một server (ví dụ: `example.com`) và nhận phản hồi.

## 🧰 Công cụ sử dụng
- `Socket`: để kết nối TCP đến server
- `PrintWriter`: để gửi dữ liệu (HTTP request)
- `BufferedReader`: để đọc dữ liệu (HTTP response)

## 💻 Mã nguồn ví dụ

```java
// KHỐI MÃ BẮT ĐẦU TỪ ĐÂY
import java.io.*;
import java.net.*;

public class SimpleHttpClient {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("example.com", 80);
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));

            out.println("GET / HTTP/1.1");
            out.println("Host: example.com");
            out.println("Connection: close");
            out.println();

            String line;
            while ((line = in.readLine()) != null) {
                System.out.println(line);
            }

            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
``` 
---

# 🚀 IV. Nâng cao: Xử lý đa luồng và nhiều client

Dùng ExecutorService để tạo thread pool:

```java
ExecutorService pool = Executors.newFixedThreadPool(10);
while (true) {
    Socket client = serverSocket.accept();
    pool.execute(() -> handleClient(client));
}
```
---
# 🔐 V. Bảo mật và tối ưu

| Kỹ thuật           | Mục đích                          |
|--------------------|-----------------------------------|
| **HTTPS (SSL/TLS)**| Mã hóa dữ liệu truyền tải         |
| **Keep-Alive**     | Giữ kết nối mở để tái sử dụng     |
| **Caching**        | Giảm tải server                   |
| **GZIP Compression**| Giảm dung lượng dữ liệu          |
| **Rate Limiting**  | Ngăn chặn DDoS                    |

---

# 📦 VI. Thư viện hỗ trợ nâng cao

| Thư viện            | Mô tả                                                                 |
|---------------------|----------------------------------------------------------------------|
| **Netty**           | Framework non-blocking I/O mạnh mẽ để xây dựng server hiệu suất cao |
| **Jetty**           | Web server nhẹ, dễ tích hợp vào ứng dụng Java                        |
| **Undertow**        | Web server non-blocking, hỗ trợ HTTP/2                               |
| **OkHttp**          | HTTP client hiện đại, hỗ trợ HTTP/2, WebSocket                       |
| **Apache HttpClient**| HTTP client phổ biến, hỗ trợ nhiều tính năng nâng cao              |

# 📚 VII. Tài liệu tham khảo

- [GeeksforGeeks: Socket Programming in Java](https://www.geeksforgeeks.org/java/socket-programming-in-java/)
- [W3Computing: Advanced Socket Programming](https://www.w3computing.com/articles/java-advanced-socket-programming-network-protocols/)
- [GitHub Workshop về Java Socket](https://github.com/Advanced-Programming-1403/Socket-Programming-Workshop)