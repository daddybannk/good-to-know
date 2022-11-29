# Good-To-Know
เรื่องบางเรื่องยิ่งรู้ยิ่งดี

## 🔑 SSH 

### ประกอบด้วย 
* Public Key `id_rsa.pub`
* Private Key `id_rsa`

### ตำแหน่งไฟล์ที่จัดเก็บ
* Windows `~/.ssh/`

### สร้างยังไง
* คำสั่ง `ssh-keygen` (ปัจจุบันเลือกวิธีนี้)
  1. พิมพ์คำสั่ง
    ```console
    $ ssh-keygen
    ```
  2. (แนะนำ) ตั้งชื่อคีย์ SSH เช่น `id_rsa` หรือไม่ตั้งก็ได้
  3. ตั้งรหัสผ่าน และยืนยันรหัสอีกครั้ง
  4. จะได้ไฟล์ `id_rsa` และ `id_rsa.pub`
* PuTTYGen
  1. กดปุ่ม Generate
  2. ขยับเมาส์ไปมาในหน้าต่างโปรแกรม ได้เนื้อหาคีย์ที่สร้าง
  3. ตั้งรหัสผ่านในช่อง `Key passphase` และ `Confirm passphase`
  4. (แนะนำ) เขียนคำอธิบายใน `Key comment` เช่น account หรือ website ที่ต้องการผูก
  5. กดปุ่ม `Save private key` ตั้งชื่อเป็น `id_{อะไรก็ได้}.ppk`
  6. กดปุ่ม `Save public key` ตั้งชื่อเป็น `id_{อะไรก็ได้}.pub`

### เพิ่ม SSH Public Key ใน Github ยังไง
1. เปิดไฟล์ที่เป็น Public Key และคัดลอกเนื้อหาข้างใน เช่น
  ```
  ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAlU5fI1dpnYtLo5HRnOSw9I/BTihd1wEE9U9ZqOpt8qY02H1zOrLauK+uDaTRyf2/ALIVtSx8vLyWlsxsSEvsS7M2eHtQUz2Q/aaTUoBb7YTb00Lu8Rg0ODTcLSbuhxhYkQ1FeaqCp3ddVKdqdSV8WHNzz9eP63aexswwqIBzXKcARW8+NzKLVyUS/6PxAyHBUHaFMkEdny5eTafPMzZ+TYKDMzC8++YPHpn+/pfzyBjdymEKUJ8kYTUAldP78mgrm297g2q7mUD5k7dhgC0QRru0//HFLBN4Ii9X++BUMBgOHHnzJmPMQbCh4eEXZ2JdL3OVq44HOpxrbRtIHdd/9Q== rsa-key-20221129
  ```
2. นำไปวางที่ช่อง Key หน้า Add key และกดปุ่มบันทึก
  ```
  https://github.com/settings/ssh/new
  ```

### ผูก SSH Private Key กับคอมพิวเตอร์ยังไง
```console
$ ssh-add ~/.ssh/id_rsa
Identity added: {Path ของ Key} {(Comment ถ้ามี)}
```

### ทดสอบการเชื่อมต่อ Github ผ่าน SSH
```console
$ ssh -T git@ssh.github.com
Hi {ชื่อ Github เรา}! You've successfully authenticated, but GitHub does not provide shell access.
```

### 🐛 กรณีขึ้นข้อความ `ssh: connect to host ssh.github.com port 22: Connection timed out`
แสดงว่า Port 22 อาจปิดอยู่ทดลองย้ายไปใช้ Port 443 (https) แทนด้วยคำสั่ง
```console
$ ssh -T -p 443 git@ssh.github.com
```

### การโคลนโปรเจค
```console
$ git clone ssh://git@ssh.github.com:443/YOUR-USERNAME/YOUR-REPOSITORY.git
```
