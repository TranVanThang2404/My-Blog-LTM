+++
date = '2025-09-30T20:55:00+07:00'
draft = false
title = 'Java I/O & NIO'
description = 'Tìm hiểu Java I/O và Java NIO, sự khác biệt giữa Stream và Channel, minh họa đọc file bằng I/O và NIO trong Java.'
tags = ["Java", "I/O", "NIO", "File", "Programming"]
categories = ["Java", "Programming"]
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 12px;">
  <img src="/images/java-io-nio.jpg" 
       alt="Java IO NIO" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">Java IO NIO</h2>
</div>

<div class="image-container" style="text-align: center; margin: 2rem auto; max-width: 800px;">
  <img src="/images/java-io-nio.jpg" 
       alt="Java IO NIO" 
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

# 🔄 So sánh Java I/O và Java NIO

## 🧠 Giới thiệu

Trong Java, có hai cách chính để xử lý dữ liệu đầu vào/đầu ra (I/O):

- **Java I/O (java.io)**: API truyền thống, dễ dùng, phù hợp với xử lý file nhỏ hoặc đơn giản.
- **Java NIO (java.nio)**: API hiện đại, hỗ trợ non-blocking I/O, tối ưu cho hiệu suất cao và xử lý dữ liệu lớn.

---

## 1️⃣ Java I/O (Input/Output – `java.io`)

- Dựa trên mô hình **Stream** – dữ liệu được xử lý tuần tự theo từng byte hoặc ký tự.
- Blocking I/O: khi đọc/ghi dữ liệu, luồng chính sẽ bị chặn cho đến khi hoàn tất.
- Dễ sử dụng, phù hợp với các tác vụ đơn giản như đọc/ghi file văn bản hoặc nhị phân.

### 🔧 Một số class thường dùng:
- `FileReader`, `BufferedReader`: đọc file text.
- `FileWriter`, `BufferedWriter`: ghi file text.
- `FileInputStream`, `FileOutputStream`: xử lý dữ liệu nhị phân.

---

## 2️⃣ Java NIO (New I/O – `java.nio`)

- Xuất hiện từ **Java 1.4**, cải tiến hiệu năng và khả năng xử lý dữ liệu.
- Dựa trên mô hình **Channel + Buffer** thay vì Stream.
- Hỗ trợ **non-blocking I/O**: không chặn luồng chính khi đọc/ghi.
- Tối ưu cho ứng dụng mạng, server socket, hoặc xử lý file lớn.

### 🔧 Thành phần chính:
- `Buffer`: vùng nhớ trung gian để lưu dữ liệu.
- `Channel`: kênh kết nối giữa chương trình và nguồn dữ liệu (file, socket).
- `Selector`: quản lý nhiều channel cùng lúc (dùng trong server socket đa kết nối).

---

## 📊 So sánh nhanh

| Đặc điểm       | Java I/O                      | Java NIO                             |
|----------------|-------------------------------|--------------------------------------|
| Mô hình        | Stream                        | Channel + Buffer                     |
| Blocking       | Có (chặn luồng chính)         | Có thể non-blocking (không chặn)     |
| Hiệu năng      | Tốt cho file nhỏ              | Tối ưu cho dữ liệu lớn / mạng        |
| Độ phức tạp    | Dễ dùng, đơn giản             | Phức tạp hơn, mạnh mẽ hơn            |
| Quản lý nhiều kết nối | Không hiệu quả         | Có `Selector` để xử lý đa kết nối    |

---

## 💻 Mã nguồn minh họa

```java
import java.io.*;
import java.nio.*;
import java.nio.channels.FileChannel;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;

public class IOvsNIOExample {

    // Đọc file bằng I/O (java.io)
    public static void readFileUsingIO(String fileName) {
        System.out.println("=== Đọc file bằng I/O (java.io) ===");
        try (BufferedReader br = new BufferedReader(new FileReader(fileName))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // Đọc file bằng NIO (java.nio)
    public static void readFileUsingNIO(String fileName) {
        System.out.println("\n=== Đọc file bằng NIO (java.nio) ===");
        try (FileChannel fileChannel = FileChannel.open(Paths.get(fileName), StandardOpenOption.READ)) {
            ByteBuffer buffer = ByteBuffer.allocate(1024);
            while (fileChannel.read(buffer) > 0) {
                buffer.flip(); // chuyển sang chế độ đọc
                while (buffer.hasRemaining()) {
                    System.out.print((char) buffer.get());
                }
                buffer.clear(); // reset buffer để đọc tiếp
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // Chạy thử
    public static void main(String[] args) {
        String fileName = "example.txt";

        // Đọc file bằng I/O
        readFileUsingIO(fileName);

        // Đọc file bằng NIO
        readFileUsingNIO(fileName);
    }
}

```
---
# 📌 Gợi ý sử dụng

- Dùng Java I/O khi xử lý file nhỏ, đơn giản, không yêu cầu hiệu năng cao.
- Dùng Java NIO khi cần xử lý nhiều kết nối mạng, dữ liệu lớn, hoặc xây dựng server hiệu suất cao.
- Có thể kết hợp cả hai tùy theo bài toán cụ thể.

# 📚 Tài liệu tham khảo

- [Baeldung: Java NIO Tutorial](https://www.baeldung.com/java-nio)  
- [GeeksforGeeks: Java I/O vs NIO](https://www.geeksforgeeks.org/difference-between-java-io-and-java-nio/)  
- [Oracle Docs: java.nio package](https://docs.oracle.com/javase/8/docs/api/java/nio/package-summary.html)  
