# 🚀 Node.js Docker Wo# 💻 เปิดโปรเจ# 📦 ติดตั้ง E# 🔧 ทดสอบ Node.js Application

สร้างไฟล์ `index.js` แล้วใส่โค้ดนี้ลงไป เพื่อสร้าง web server อย่างง่าย

```javascript
const express = require('express');
condockerignore ขึ้นมาเพื่อไม่ให้ copy node_modules เข้าไปใน image

```plaintext
node_modules
```

> 🚫 **ประโยชน์ของ .dockerignore**: ช่วยลดขนาด image และเวลาใน build โดยไม่คัดลอก `node_modules` ที่ใหญ่

# 🐙 สร้าง Docker Hub Repository

## 🔑 Login เข้า Docker Hub

เข้าสู่ระบบ Docker Hub ผ่านคำสั่ง terminal

```commandline
docker login
```

> 🔐 **หมายเหตุ**: กรอก username และ password ของ Docker Hub account

## 📝 ตั้งชื่อ Repository

สร้าง repository บน Docker Hub website ด้วยชื่อ:

```
nodejs-api
```

> 💡 **เคล็ดลับ**: ชื่อ repository ควรเป็นภาษาอังกฤษและไม่มีช่องว่างess();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello <<username>> Version 0.0.1');
});

app.listen(port, () => {
    console.log(`Example app listening at http://localhost:${port}`);
});

```

> 📝 **อธิบายโค้ด**: 
> - สร้าง Express application
> - กำหนด route สำหรับ GET `/` ที่ส่งข้อความตอบกลับ
> - เริ่ม server ที่ port 3000
ติดตั้ง Express.js ซึ่งเป็น web framework ที่ได้รับความนิยมสำหรับ Node.js

```commandline
npm install express
```

> 🚀 **Express.js** เป็น framework ที่ช่วยให้การสร้าง web server ใน Node.js ง่ายและรวดเร็วขึ้น VS Code

เปิดโฟลเดอร์โปรเจคใน Visual Studio Code เพื่อเริ่มเขียนโค้ด

```commandline
code .
```

> ⚡ **เคล็ดลับ**: คำสั่งนี้จะเปิด VS Code และโหลดโฟลเดอร์ปัจจุบันเป็นโปรเจคp Tutorial

## 📂 สร้าง Directory สําหรับเริ่มต้นโปรเจค

สร้างโฟลเดอร์โปรเจคใหม่และเข้าไปในโฟลเดอร์นั้น เพื่อเป็นที่เก็บไฟล์โปรเจคของเรา

```commandline
mkdir myproject
cd myproject
``` 

# 📦 สร้าง Node.js Project

สร้างไฟล์ `package.json` สำหรับโปรเจค Node.js โดยใช้ flag `-y` เพื่อใช้ค่าเริ่มต้นทั้งหมด

```commandline
npm init -y
```

> 💡 **หมายเหตุ**: คำสั่งนี้จะสร้างไฟล์ `package.json` ที่มีข้อมูลพื้นฐานของโปรเจคเราอัตโนมัติ


# เปิดโปรเจคด้วย VS Code

```commandline
code .
```

# ติดตั้ง Express 

```commandline
npm install express
```

# ทดสอบ Node 

สร้างไฟล์ `index.js` แล้วใส่โค้ดนี้ลงไป

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello <<username>> Version 0.0.1');
});

app.listen(port, () => {
    console.log(`Example app listening at http://localhost:${port}`);
});

```


# 🏃‍♂️ ทดสอบรันโปรเจค

รันไฟล์ `index.js` เพื่อเริ่ม web server

```commandline
node index.js
```

> ✅ **ผลลัพธ์**: หากสำเร็จจะเห็นข้อความ "Example app listening at http://localhost:3000"

# 🐳 สร้างไฟล์ Dockerfile สําหรับ Build Image

สร้างไฟล์ `Dockerfile` เพื่อกำหนดวิธีการ build Docker image สำหรับแอปพลิเคชัน Node.js

```dockerfile

FROM node

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

COPY package.json /usr/src/app/

RUN npm install

COPY . /usr/src/app/

EXPOSE 3000

CMD ["node", "index.js"]

```

> 🔍 **อธิบาย Dockerfile**:
> - `FROM node`: ใช้ base image ของ Node.js
> - `WORKDIR`: กำหนด working directory
> - `COPY package.json`: คัดลอกไฟล์ dependencies ก่อน
> - `RUN npm install`: ติดตั้ง dependencies
> - `COPY .`: คัดลอกไฟล์โปรเจคทั้งหมด
> - `EXPOSE 3000`: เปิดพอร์ต 3000
> - `CMD`: คำสั่งที่จะรันเมื่อ container เริ่มทำงาน

# 🔨 รันคำสั่ง Build Image

```commandline
docker build -t nodejs-api:uat-v0.0.1 .
```

> ⏳ **รอให้ build image เสร็จ** - กระบวนการ build อาจใช้เวลาสักครู่ในครั้งแรก

# 🚢 รัน Container จาก Image ที่ Build ขึ้นมา

รัน Docker container จาก image ที่เพิ่งสร้างขึ้น โดย map port 3000 จาก container ไปยัง host

```commandline
docker run -p 3000:3000 -d nodejs-api:uat-v0.0.1
```

> 🔧 **อธิบายคำสั่ง**:
> - `-p 3000:3000`: map port 3000 ของ container ไปยัง port 3000 ของ host
> - `-d`: รัน container ในโหมด detached (background)
> - `nodejs-api:uat-v0.0.1`: ชื่อ image และ tag ที่จะใช้รัน

# 🌐 ทดสอบเปิดเว็บเบราเซอร์

เปิดเว็บเบราเซอร์แล้วเข้าไปที่ http://localhost:3000

> 📱 **ผลลัพธ์**: คุณจะเห็นข้อความ "Hello <<username>> Version 0.0.1" แสดงบนหน้าเว็บ

# ⏹️ หยุด Container

```commandline
docker ps
docker stop <container_id>
```

> 💡 **วิธีการหยุด Container**: ใช้ `docker ps` เพื่อดู container ID แล้วใช้ `docker stop <container_id>` เพื่อหยุด

# 🔄 แก้ไขไฟล์ index.js ให้เป็น Version 0.0.2

แก้ไขไฟล์ `index.js` เพื่ออัพเดท version และข้อความตอบกลับ

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello <<username>> version 2');
});

app.listen(port, () => {
    console.log(`Example app listening at http://localhost:${port}`);
});
```


# 🔨 รันคำสั่ง Build Image Version 0.0.2

สร้าง Docker image ใหม่ด้วย version 0.0.2 ที่มีการเปลี่ยนแปลงโค้ด

```commandline
docker build -t nodejs-api:uat-v0.0.2 .
```

> 🔄 **การ Update Version**: การสร้าง image ใหม่จะรวมการเปลี่ยนแปลงที่เราทำไว้


# 🚀 รัน Image ใหม่ Version 0.0.2

รัน container จาก image version ใหม่ที่เพิ่งสร้างเสร็จ

```commandline
docker run -p 3000:3000 -d nodejs-api:uat-v0.0.2
```

> 🔄 **ทดสอบ**: ลองเปิดเบราเซอร์ไปที่ http://localhost:3000 เพื่อดูผลลัพธ์ใหม่

# 📂 สร้างไฟล์ .dockerignore

สร้างไฟล์ `.dockerignore` เพื่อไม่ให้ Docker คัดลอกไฟล์ที่ไม่จำเป็นเข้าไปใน image

dockerignore ขึ้นมาเพื่อไม่ให้ copy node_modules เข้าไปใน image

```plaintext
node_modules
```

# สร้าง Docker hub repository

## login เข้า docker hub

### ตั้งชื่อ repository 
nodejs-api


# 🏷️ ติด Tag ให้กับ Image

เพิ่ม tag ที่มี Docker Hub username เพื่อเตรียม push ขึ้น Docker Hub

```commandline
docker tag nodejs-api:uat-v0.0.1 <<username>>/nodejs-api:uat-v0.0.1
```

> 🎯 **การ Tag Image**: จำเป็นต้องมี username ใน tag เพื่อให้ push ขึ้น Docker Hub ได้

# 📤 Push Image ขึ้น Docker Hub

อัปโหลด image ที่เราสร้างไว้ขึ้นสู่ Docker Hub repository

```commandline
docker push <<username>>/nodejs-api:uat-v0.0.1
```

> ⬆️ **กระบวนการ Push**: Docker จะอัปโหลด layers ต่างๆ ของ image ไปยัง Docker Hub

# ✅ ตรวจสอบ Image ที่ Push ขึ้น Docker Hub แล้ว

เข้าไปดู repository บน Docker Hub website เพื่อยืนยันว่า image ถูกอัปโหลดเรียบร้อย

# 🏷️ Tag Image Version 0.0.2

เพิ่ม tag สำหรับ version 0.0.2 เพื่อเตรียม push ขึ้น Docker Hub

```commandline
docker tag nodejs-api:uat-v0.0.2 <<username>>/nodejs-api:uat-v0.0.2
```

> 📋 **Version Management**: การใช้ tag ที่แตกต่างกันจะช่วยในการจัดการ version ต่างๆ

# 📤 Push Image Version 0.0.2 ขึ้น Docker Hub

อัปโหลด image version ใหม่ขึ้นสู่ Docker Hub repository

```commandline
docker push <<username>>/nodejs-api:uat-v0.0.2
``` 

> 🆕 **การ Push Version ใหม่**: Image version ใหม่จะถูกอัปโหลดและเก็บไว้ใน repository เดียวกัน

# 🔍 ตรวจสอบ Image ที่ Push ขึ้น Docker Hub แล้ว

เข้าไปตรวจสอบบน Docker Hub website ว่ามี image ทั้งสอง version (0.0.1 และ 0.0.2) แล้ว

# 📥 ดาวน์โหลด Image จาก Docker Hub (Docker Pull)

## 📥 Pull Image Version 0.0.1

ดาวน์โหลด image version 0.0.1 จาก Docker Hub มายังเครื่องของเรา

```commandline
docker pull <<username>>/nodejs-api:uat-v0.0.1
```

> 📦 **การ Pull Image**: คำสั่งนี้จะดาวน์โหลด image จาก Docker Hub repository มาเก็บไว้ในเครื่องเรา

## 📥 Pull Image Version 0.0.2

ดาวน์โหลด image version 0.0.2 จาก Docker Hub มายังเครื่องของเรา

```commandline
docker pull <<username>>/nodejs-api:uat-v0.0.2
```

> 🔄 **การ Pull Version ใหม่**: สามารถดาวน์โหลด version ต่างๆ ได้ตามต้องการ

## 🚀 รัน Container จาก Image ที่ Pull มา

### รัน Version 0.0.1
```commandline
docker run -p 3000:3000 -d --name <<username>>-nodejs-api-v1 <<username>>/nodejs-api:uat-v0.0.1
```

### รัน Version 0.0.2
```commandline
docker run -p 3001:3000 -d --name <<username>>-nodejs-api-v2 <<username>>/nodejs-api:uat-v0.0.2
```

> 💡 **เคล็ดลับ**: ใช้ port ต่างกันเพื่อรัน version ต่างๆ พร้อมกัน (port 3000 และ 3001)

## 🌐 ทดสอบ Image ที่ดาวน์โหลดมา

- Version 0.0.1: เปิด http://localhost:3000
- Version 0.0.2: เปิด http://localhost:3001

> 🎉 **สำเร็จแล้ว!**: ตอนนี้คุณมี Node.js application ที่ containerized และสามารถ deploy หรือ pull จาก Docker Hub ได้เรียบร้อย