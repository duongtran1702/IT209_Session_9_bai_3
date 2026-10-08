# Bài 3: Đóng gói trang Web HTML tĩnh với Dockerfile

## 1. Mục tiêu
Viết tệp Dockerfile ngắn gọn để đóng gói một trang HTML tĩnh vào Docker Image sử dụng web server Nginx (phiên bản Alpine Linux tối ưu dung lượng).

---

## 2. Cấu trúc thư mục
```text
bai_3/
├── Dockerfile
├── index.html
└── README.md
```

---

## 3. Nội dung các tệp tin

### `index.html`
```html
<h1>Hello Docker Session 09!</h1>
```

### `Dockerfile`
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

**Giải thích:**
- `FROM nginx:alpine`: Sử dụng base image Nginx chạy trên nền Alpine Linux cực nhẹ (~20-40MB).
- `COPY index.html /usr/share/nginx/html/index.html`: Sao chép file `index.html` từ máy host vào thư mục root chứa nội dung web mặc định của Nginx trong container.

---

## 4. Hướng dẫn chạy và kiểm tra

### Bước 1: Build Docker Image
Chạy lệnh tại thư mục `bai_3`:
```bash
docker build -t my-html-app:v1 .
```

### Bước 2: Khởi chạy container
Khởi chạy container ở chế độ chạy ngầm (`-d`), ánh xạ cổng host 8081 vào cổng 80 của container:
```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

### Bước 3: Kiểm tra kết quả
Sử dụng `curl`:
```bash
curl http://localhost:8081
```
Hoặc truy cập trực tiếp trên trình duyệt: [http://localhost:8081](http://localhost:8081)

**Kết quả mong đợi:**
```html
<h1>Hello Docker Session 09!</h1>
```

---

## 5. Dọn dẹp tài nguyên (Khi cần)
Để dừng và xoá container sau khi kiểm tra xong:
```bash
docker stop html-app
docker rm html-app
```
Xoá image nếu không dùng nữa:
```bash
docker rmi my-html-app:v1
```
