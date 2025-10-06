# 🌐 สร้าง Nginx Docker Image Tutorial

## 📂 สร้าง Folder สำหรับเก็บไฟล์ nginx
```commandline
mkdir nginx-docker
cd nginx-docker
```

## 📝 สร้างไฟล์ index.html ที่สวยงาม
```html
<!DOCTYPE html>
<html>
<head>
    <title>Hayato360 Nginx Server</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            text-align: center; 
            margin: 0; 
            padding: 0;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); 
            color: white; 
            min-height: 100vh; 
            display: flex; 
            align-items: center; 
            justify-content: center; 
            flex-direction: column; 
        }
        .container { 
            background: rgba(255,255,255,0.1); 
            padding: 40px; 
            border-radius: 15px; 
            backdrop-filter: blur(10px); 
            box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
            border: 1px solid rgba(255, 255, 255, 0.18);
        }
        h1 { 
            color: #ffd700; 
            font-size: 3em; 
            margin-bottom: 20px; 
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        p { 
            color: #f0f0f0; 
            font-size: 1.2em; 
            margin: 10px 0;
        }
        .version { 
            background: rgba(255,255,255,0.2); 
            padding: 15px; 
            border-radius: 8px; 
            margin-top: 20px; 
            font-weight: bold;
            color: #ffd700;
        }
        .tech-stack {
            display: flex;
            gap: 10px;
            margin-top: 20px;
            justify-content: center;
            flex-wrap: wrap;
        }
        .tech-item {
            background: rgba(255, 255, 255, 0.3);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.9em;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🚀 Hayato360</h1>
        <p>This is a beautiful Nginx web server running inside a Docker container.</p>
        <p>Welcome to my personal web server!</p>
        <div class="tech-stack">
            <div class="tech-item">🐳 Docker</div>
            <div class="tech-item">🌐 Nginx</div>
            <div class="tech-item">🎨 HTML5</div>
            <div class="tech-item">💫 CSS3</div>
        </div>
        <div class="version">Version: uat-v0.0.1</div>
    </div>
</body>
</html>
```

## 🔄 ถอยกลับไปที่ root folder
```commandline
cd ..
```

## 🚀 รัน Container เพื่อคัดลอกไฟล์เข้าไป
```commandline
docker run -d --name nginx-web nginx
```

## 📁 คัดลอกไฟล์ HTML เข้าไปใน Container
```commandline
docker cp nginx-docker/index.html nginx-web:/usr/share/nginx/html/
```

> 💡 **สำคัญ**: `docker cp` จะคัดลอกไฟล์เข้าไปใน container จริงๆ ไม่ใช่แค่ mount

## ✅ ทดสอบว่าไฟล์ถูกคัดลอกแล้ว
```commandline
docker exec nginx-web cat /usr/share/nginx/html/index.html
```

## 🔄 สร้าง Image จาก Container ที่มีไฟล์จริง

### Commit Container เป็น Image ใหม่ก่อน
```commandline
docker commit nginx-web custom-nginx:uat-v0.0.1
```

> 💡 **สำคัญ**: สร้าง image จาก container ที่มีไฟล์ HTML แล้ว

## 🌐 ทดสอบ Image ที่สร้างแล้ว

### หยุดและลบ Container เก่า
```commandline
docker stop nginx-web
docker rm nginx-web
```

### รัน Container จาก Image ใหม่
```commandline
docker run -d -p 8080:80 --name nginx-web-test custom-nginx:uat-v0.0.1
```

### ทดสอบเว็บไซต์
```commandline
curl localhost:8080
```

> 📱 **ผลลัพธ์**: คุณจะเห็นหน้าเว็บที่สวยงามแสดงชื่อ Hayato360

### Tag Image สำหรับ Docker Hub
```commandline
docker tag custom-nginx:uat-v0.0.1 hayato360/nginx-web:uat-v0.0.1
```

### ตรวจสอบ Image ที่สร้าง
```commandline
docker images | findstr nginx-web
```

## 🐙 สร้าง Docker Hub Repository

### 🔑 Login เข้า Docker Hub
```commandline
docker login
```

### 📝 ตั้งชื่อ Repository 
สร้าง repository บน Docker Hub website ด้วยชื่อ:
```
nginx-web
```

## 📤 Push Image ขึ้น Docker Hub

**ไม่ต้อง tag อีกครั้ง** เพราะเราได้ commit ด้วยชื่อที่ถูกต้องแล้ว

```commandline
docker push hayato360/nginx-web:uat-v0.0.1
```

## ✅ ทดสอบ Pull และรันจาก Docker Hub

### หยุดและลบ Container เก่า
```commandline
docker stop nginx-web
docker rm nginx-web
```

### ลบ Image ในเครื่อง (เพื่อทดสอบ pull)
```commandline
docker rmi hayato360/nginx-web:uat-v0.0.1
```

### Pull จาก Docker Hub
```commandline
docker pull hayato360/nginx-web:uat-v0.0.1
```

### รันจาก Image ที่ Pull มา
```commandline
docker run -d -p 8080:80 --name nginx-test hayato360/nginx-web:uat-v0.0.1
```

### ทดสอบผลลัพธ์
เปิดเบราเซอร์ไปที่ http://localhost:8080

> 🎉 **ผลลัพธ์**: ตอนนี้คุณจะเห็นหน้าเว็บที่แก้ไขแล้วแน่นอน ไม่ใช่ default nginx page





