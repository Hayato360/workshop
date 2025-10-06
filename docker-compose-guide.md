# 🐙 Workshop Container - Docker Compose Setup

## 📋 **ข้อมูล Workshop**
- **Node.js API v1**: `<<username>>/nodejs-api:uat-v0.0.1` (Port 3000)
- **Node.js API v2**: `<<username>>/nodejs-api:uat-v0.0.2` (Port 3001)  
- **Nginx Web**: `<<username>>/nginx:uat-v0.0.1` (Port 8080)

## 🚀 **ขั้นตอนการรัน Docker Compose**

### 1. 📥 Pull Images จาก Docker Hub

ดาวน์โหลด images ทั้งหมดจาก Docker Hub ก่อนรัน compose

```commandline
docker pull <<username>>/nodejs-api:uat-v0.0.1
docker pull <<username>>/nodejs-api:uat-v0.0.2
docker pull <<username>>/nginx:uat-v0.0.1
```

### 2. 🔧 แก้ไข docker-compose.yml

เปลี่ยน `<<username>>` เป็น Docker Hub username จริงของคุณใน `docker-compose.yml`

```yaml
# ตัวอย่าง: ถ้า username คือ "john"
services:
  nodejs-api-v1:
    image: john/nodejs-api:uat-v0.0.1
    # ... ส่วนอื่นๆ
```

### 3. ⬆️ รัน Docker Compose

รัน containers ทั้งหมดด้วยคำสั่งเดียว

```commandline
docker-compose up -d
```

> 🔧 **คำอธิบาย**:
> - `up`: สร้างและรัน containers ตาม config
> - `-d`: รันในโหมด detached (background)

### 4. 📊 ตรวจสอบสถานะ Services

```commandline
docker-compose ps
```

### 5. 🌐 ทดสอบการทำงาน

เปิดเบราเซอร์และทดสอบ URLs ดังนี้:

- **Node.js API v1**: http://localhost:3000
  - ผลลัพธ์: "Hello <<username>> Version 0.0.1"
  
- **Node.js API v2**: http://localhost:3001  
  - ผลลัพธ์: "Hello <<username>> version 2"
  
- **Nginx Website**: http://localhost:8080
  - ผลลัพธ์: หน้าเว็บที่แสดงชื่อของคุณ

### 6. 📋 ดู Logs

```commandline
# ดู logs ทั้งหมด
docker-compose logs

# ดู logs ของ service เฉพาะ
docker-compose logs nodejs-api-v1
docker-compose logs nodejs-api-v2
docker-compose logs nginx-web

# ดู logs แบบ real-time
docker-compose logs -f
```

## 🔧 **การจัดการ Services**

### 🔄 Restart Services

```commandline
# Restart service เฉพาะ
docker-compose restart nodejs-api-v1

# Restart ทั้งหมด
docker-compose restart
```

### ⏹️ หยุด Services

```commandline
# หยุด services ทั้งหมด (แต่ไม่ลบ containers)
docker-compose stop

# หยุดและลบ containers
docker-compose down

# หยุด ลบ containers และ networks
docker-compose down --networks
```

### 📈 ตรวจสอบ Resources

```commandline
# ดู resource usage
docker stats

# ดู network information
docker network ls
docker network inspect workshop-network
```

## 🚨 **Troubleshooting**

### ❌ **ถ้า Pull Image ไม่ได้**
```commandline
# ตรวจสอบว่า login Docker Hub แล้วหรือยัง
docker login

# ลอง pull แต่ละ image เพื่อดู error message
docker pull <<username>>/nodejs-api:uat-v0.0.1
```

### ❌ **ถ้า Port ขัดแย้ง**
```commandline
# ตรวจสอบ port ที่ใช้งานอยู่
netstat -an | findstr "3000"
netstat -an | findstr "3001"  
netstat -an | findstr "8080"

# หยุด containers ที่อาจจะรันอยู่
docker stop $(docker ps -q)
```

### ❌ **ถ้า Network มีปัญหา**
```commandline
# ลบ network เก่า
docker network rm workshop-network

# รัน compose ใหม่
docker-compose up -d
```

## 🎯 **คำสั่งที่ใช้บ่อย**

```commandline
# ดู containers ทั้งหมด
docker ps -a

# ดู images
docker images

# ทำความสะอาด containers ที่หยุดแล้ว
docker container prune

# ทำความสะอาด networks ที่ไม่ใช้
docker network prune

# ทำความสะอาดทั้งระบบ
docker system prune -a
```

## ✅ **สรุป Architecture**

```
┌─────────────────────┐
│   Docker Compose    │
└─────────────────────┘
           │
    ┌──────┴──────┐
    │   Network   │
    │ workshop-   │
    │  network    │
    └──────┬──────┘
           │
    ┌──────┼──────┐
    │      │      │
┌───▼───┐ ▼ ┌────▼────┐
│Node.js│   │ Nginx   │
│API v1 │   │   Web   │
│:3000  │   │  :8080  │
└───────┘   └─────────┘
│Node.js│
│API v2 │
│:3001  │
└───────┘
```

> 🎉 **สำเร็จแล้ว!** ตอนนี้คุณมี multi-container application ที่ใช้ Docker Compose จัดการ 3 services พร้อมกัน โดยดึง images จาก Docker Hub repository ของคุณเอง!