+++
title = "Java Multithreading"
date = "2025-09-30T22:55:00+07:00"
draft = false
description = "Giới thiệu về Java Multithreading với ví dụ minh họa"
tags = ["java", "multithreading", "threads"]
categories = ["programming", "java"]
icon = "/images/java-exception.jpg"
+++

<div style="display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; padding: 1rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 12px;">
  <img src="/images/java-exception.jpg" 
       alt="Java Multithreading Icon" 
       style="width: 80px; height: 80px; object-fit: cover; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); border: 3px solid white;"/>
  <h2 style="margin: 0; font-size: 2.5rem; color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">Java Multithreading</h2>
</div>

<div class="image-container" style="text-align: center; margin: 2rem auto; max-width: 800px;">
  <img src="/images/java-exception.jpg" 
       alt="Java Multithreading Diagram" 
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

# ⚙️ Multithreading trong Java

**Multithreading** cho phép chạy nhiều luồng (thread) đồng thời trong một chương trình, giúp tận dụng CPU tốt hơn. Trong Java, một luồng là đơn vị nhỏ nhất của tiến trình.

---

## 1️⃣ Cách tạo Thread

Có 2 cách chính để tạo thread trong Java:

1. **Kế thừa lớp `Thread`** – đơn giản nhưng hạn chế vì Java không hỗ trợ đa kế thừa.
2. **Triển khai interface `Runnable`** – linh hoạt hơn, được khuyến nghị sử dụng.

---

## 💻 2. Ví dụ minh họa

```java
// Cách 1: Kế thừa Thread
class MyThread extends Thread {
    private String threadName;

    MyThread(String name) {
        this.threadName = name;
    }

    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(threadName + " - Count: " + i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                System.out.println(threadName + " bị gián đoạn");
            }
        }
        System.out.println(threadName + " hoàn thành!");
    }
}

// Cách 2: Implement Runnable
class MyRunnable implements Runnable {
    private String threadName;

    MyRunnable(String name) {
        this.threadName = name;
    }

    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(threadName + " - Count: " + i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                System.out.println(threadName + " bị gián đoạn");
            }
        }
        System.out.println(threadName + " hoàn thành!");
    }
}

public class ThreadExample {
    public static void main(String[] args) {
        MyThread t1 = new MyThread("Thread-1");
        Thread t2 = new Thread(new MyRunnable("Thread-2"));

        t1.start();
        t2.start();

        for (int i = 1; i <= 5; i++) {
            System.out.println("Main Thread - Count: " + i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        System.out.println("Main Thread hoàn thành!");
    }
}
```

---

# 🔧 3.Các phương thức quan trọng của Thread

| Phương thức | Mô tả |
|-------------|-------|
| `start()` | Bắt đầu thread mới |
| `run()` | Chứa code thực thi của thread |
| `sleep(ms)` | Tạm dừng thread trong khoảng thời gian |
| `join()` | Đợi thread khác hoàn thành |
| `isAlive()` | Kiểm tra thread còn chạy không |
| `setPriority(int)` | Đặt độ ưu tiên (1-10) |
| `interrupt()` | Gián đoạn thread |

---

# 🎚️ 4.Thread Priority (Độ ưu tiên)

```java
Thread t1 = new Thread(new MyRunnable("Low Priority"));
Thread t2 = new Thread(new MyRunnable("High Priority"));

t1.setPriority(Thread.MIN_PRIORITY);    // 1
t2.setPriority(Thread.MAX_PRIORITY);     // 10

t1.start();
t2.start();
```

---

# ⏳ 5.Ví dụ với join()

```java
public class JoinExample {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            for (int i = 1; i <= 3; i++) {
                System.out.println("Thread 1: " + i);
                try { Thread.sleep(1000); } 
                catch (InterruptedException e) {}
            }
        });
        
        t1.start();
        
        try {
            t1.join(); // Main thread đợi t1 hoàn thành
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println("Main thread tiếp tục sau khi t1 hoàn thành");
    }
}
```

---

# 🔐 6.Synchronization (Đồng bộ hóa)

Khi nhiều thread truy cập cùng một tài nguyên, cần đồng bộ hóa để tránh xung đột:

```java
class Counter {
    private int count = 0;
    
    // Phương thức synchronized
    public synchronized void increment() {
        count++;
    }
    
    public int getCount() {
        return count;
    }
}

public class SyncExample {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();
        
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });
        
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });
        
        t1.start();
        t2.start();
        
        t1.join();
        t2.join();
        
        System.out.println("Final Count: " + counter.getCount());
        // Output: 2000 (nhờ synchronized)
    }
}
```

---

# 🔄 7.Thread States (Trạng thái của Thread)

```
NEW → RUNNABLE → RUNNING → TERMINATED
         ↓           ↓
      BLOCKED    WAITING/TIMED_WAITING
```

- **NEW**: Thread được tạo nhưng chưa start()
- **RUNNABLE**: Thread đã start() và sẵn sàng chạy
- **RUNNING**: Thread đang thực thi
- **BLOCKED**: Thread đang đợi lock
- **WAITING**: Thread đang đợi thread khác
- **TERMINATED**: Thread đã hoàn thành

---

# ⚠️ 8.Lưu ý quan trọng

- **Không gọi run() trực tiếp** - luôn dùng `start()` để tạo thread mới  
- **Sử dụng synchronized** khi nhiều thread truy cập shared resource  
- **Tránh deadlock** - cẩn thận khi lock nhiều object  
- **Ưu tiên Runnable** hơn extends Thread (linh hoạt hơn)  
- **Xử lý InterruptedException** đúng cách

---

# 📚 9.Tài liệu tham khảo

- [Java Concurrency - Oracle Docs](https://docs.oracle.com/javase/tutorial/essential/concurrency/)
- [Multithreading in Java - GeeksforGeeks](https://www.geeksforgeeks.org/multithreading-in-java/)
- [Java Thread Tutorial - Baeldung](https://www.baeldung.com/java-thread-lifecycle)