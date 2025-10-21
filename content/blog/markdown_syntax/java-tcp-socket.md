+++
date = '2025-09-30T19:54:12+07:00'
draft = false
title = 'Java TCP Socket'
description = 'Hướng dẫn sử dụng Java TCP Socket: ServerSocket, Socket, InputStream/OutputStream, với ví dụ client-server đơn giản.'
tags = ["Java", "TCP", "Socket", "Networking", "Programming"]
categories = ["Java", "Networking"]
icon = "/images/java-tcp-socket.jpg"
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 12px;">
  <img src="/images/java-tcp-socket.jpg" 
       alt="Java TCP Socket" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">Java TCP Socket</h2>
</div>

<div class="image-container" style="text-align: center; margin: 2rem auto; max-width: 800px;">
  <img src="/images/java-tcp-socket.jpg" 
       alt="Java TCP Socket" 
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
# 🔌 Giới thiệu về TCP Socket trong Java

**Socket** là điểm cuối của một kết nối mạng. Với **TCP Socket**, dữ liệu được truyền **tin cậy** và **có thứ tự**, đảm bảo tính toàn vẹn khi giao tiếp giữa client và server.

---

## 🧰 Các thành phần chính

- `ServerSocket`: dùng để lắng nghe kết nối từ client.
- `Socket`: dùng để kết nối và trao đổi dữ liệu giữa hai bên.
- `InputStream` / `OutputStream`: dùng để đọc và ghi dữ liệu qua socket.

---

## 🔄 Luồng hoạt động TCP Socket

1. **Server** tạo `ServerSocket` và gọi `accept()` để chờ kết nối.
2. **Client** tạo `Socket` và kết nối đến địa chỉ server.
3. Hai bên trao đổi dữ liệu thông qua stream (`BufferedReader`, `PrintWriter`, v.v.).
4. Đóng kết nối khi hoàn tất.

---

## 💻 Ví dụ minh họa

### 🖥️ Server

```java
import java.io.*;
import java.net.*;

public class TCPServer {
    public static void main(String[] args) throws Exception {
        ServerSocket server = new ServerSocket(1234);
        System.out.println("Server đang chạy...");

        Socket socket = server.accept();
        BufferedReader in = new BufferedReader(
            new InputStreamReader(socket.getInputStream()));
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

        String msg = in.readLine();
        System.out.println("Client: " + msg);
        out.println("Server nhận: " + msg);

        socket.close();
        server.close();
    }
}
```

### 💻 Client
```java
import java.io.*;
import java.net.*;

public class TCPClient {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("localhost", 1234);
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
        BufferedReader in = new BufferedReader(
            new InputStreamReader(socket.getInputStream()));

        out.println("Xin chào Server!");
        System.out.println(in.readLine());

        socket.close();
    }
}
```

### 🔁 Xử lý nhiều client bằng luồng (Thread)

```java
import java.io.*;
import java.net.*;

public class MultiClientServer {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(1234);
        System.out.println("Server đang chạy...");

        while (true) {
            Socket clientSocket = serverSocket.accept();
            new Thread(() -> handleClient(clientSocket)).start();
        }
    }

    private static void handleClient(Socket socket) {
        try (
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream()));
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true)
        ) {
            String msg = in.readLine();
            System.out.println("Client: " + msg);
            out.println("Server nhận: " + msg);
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
# 📌 Lưu ý khi triển khai thực tế

- Nên dùng ExecutorService thay vì tạo Thread thủ công để quản lý tài nguyên tốt hơn.
- Cần xử lý timeout, exception, và đóng kết nối đúng cách để tránh rò rỉ tài nguyên.
- Có thể dùng BufferedReader, DataInputStream, hoặc ObjectInputStream tùy kiểu dữ liệu.
- Với ứng dụng lớn, nên dùng thư viện như Netty, Spring WebSocket, hoặc gRPC.

# 📚 Tài liệu tham khảo

- [GeeksforGeeks: Java Socket Programming](https://www.geeksforgeeks.org/java/socket-programming-in-java/)  
- [Baeldung: Java TCP Server](https://www.baeldung.com/a-guide-to-java-sockets)  
- [Oracle Docs: java.net package](https://docs.oracle.com/javase/8/docs/api/java/net/package-summary.html)  
