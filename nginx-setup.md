# สร้าง Folder สำหรับเก็บไฟล์ nginx
```commandline
mkdir nginx-docker
cd nginx-docker
```

# สร้างไฟล์  index.html
```html
<h1>Name</h1>
```

# ถอยกลับไปที่ root folder
```commandline
cd ..
```

# รันไฟล์แบบ map volume
```commandline
docker run -d -p 8080:80 --name nginx-web -v ${PWD}/nginx-docker:/usr/share/nginx/html nginx
```


# ตรวจสอบ Container ที่รันอยู่
```commandline
docker ps
```
# ทดสอบ curl
```commandline
curl localhost:8080
```

# ทําการ exec เข้าไปใน container
```commandline
docker exec -it nginx-web /bash
```

# หาตําแหน่งที่เราอยู่
```commandline
pwd
```

# เข้าไปที่โฟลเดอร์ html
```commandline
cd usr/share/nginx/html
```

# ดูไฟล์ index.html
```commandline
cat index.html
```

# ติดตั้ง vim
```commandline
apt update
apt install vim nano -y
```

# แก้ไขไฟล์ index.html
```commandline
vi index.html
```

# แก้ไขไฟล์ index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>"(Name)"</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin-top: 50px; }
        h1 { color: #333; }
        p { color: #666; }
    </style>
</head>
<body>
    <h1>Name</h1>
    <p>This is a simple Nginx web server running inside a Docker container.</p>
    <p>Enjoy your stay!</p>
</body>
</html>
```

# ออกมาจาก container
```commandline
exit
```


# สร้าง Docker hub repository

## login เข้า docker hub

### ตั้งชื่อ repository 
```commandline
nginx-web
```

# ติดแท๊ก image
```commandline
docker tag nginx-web:latest <your_dockerhub_username>/nginx-web:uat-v0.0.1
```

# push image ขึ้น docker hub
```commandline
docker push <your_dockerhub_username>/nginx-web:uat-v0.0.1
```

# ตรวจสอบ image ที่ push ขึ้น docker hub แล้ว
เข้าไปดู repository บน Docker Hub website เพื่อยืนยันว่า image ถูกอัปโหลดเรียบร้อย





