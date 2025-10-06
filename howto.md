# สร้าง Directory สําหรับเริ่มต้นโปรเจค

```commandline
mkdir myproject
cd myproject
``` 

# สร้าง node project

```commandline
npm init -y
```


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


# ทดสอบรันโปรเจค

```commandline
node index.js
```

# สร้างไฟล์ Dockerfile สําหรับ build image

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

# รันคำสั่ง build image

```commandline
docker build -t nodejs-api:uat-v0.0.1 .
```

# รอให้ build image เสร็จ

# รัน container จาก image ที่ build ขึ้นมา

```commandline
docker run -p 3000:3000 -d nodejs-api:uat-v0.0.1
```

# ทดสอบเปิดเว็บเบราเซอร์

เปิดเว็บเบราเซอร์แล้วเข้าไปที่ http://localhost:3000

# หยุด container

```commandline
docker ps
docker stop <container_id>
``` 

# แก้ไขไฟล์ index.js ให้เป็น version 0.0.2

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


# รันคำสั่ง build image version 0.0.2

```commandline
docker build -t nodejs-api:uat-v0.0.2 .
```


# run image ใหม่ version 0.0.2

```commandline
docker run -p 3000:3000 -d nodejs-api:uat-v0.0.2
```

# สร้างไฟล์ .dockerignore

dockerignore ขึ้นมาเพื่อไม่ให้ copy node_modules เข้าไปใน image

```plaintext
node_modules
```

# สร้าง Docker hub repository

# login เข้า docker hub

```ตั้งชื่อ repository
nodejs-api
```

# ติด tag ให้กับ image

```commandline
docker tag nodejs-api:uat-v0.0.1 <<dockerhub-username>>/nodejs-api:uat-v0.0.1
```


# push image ขึ้น docker hub

```commandline
docker push <<dockerhub-username>>/nodejs-api:uat-v0.0.1
```

# ตรวจสอบ image ที่ push ขึ้น docker hub แล้ว

# tag image version 0.0.2

```commandline
docker tag nodejs-api:uat-v0.0.2 <<dockerhub-username>>/nodejs-api:uat-v0.0.2
```

# push image version 0.0.2 ขึ้น docker hub

```commandline
docker push <<dockerhub-username>>/nodejs-api:uat-v0.0.2
``` 

# ตรวจสอบ image ที่ push ขึ้น docker hub แล้ว