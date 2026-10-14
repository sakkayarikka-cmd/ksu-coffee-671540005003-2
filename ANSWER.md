# ANSWER — นายศักยริกข์ กาญจันดา 671540005003-2

- Platform: Render
- Production URL: https://ksu-coffee-671540005003-2.onrender.com

## คำตอบ

1. เลือกแพลตฟอร์ม Render ซึ่งรันโค้ดด้วยโมเดล Container (Web Service แบบ Long-running process) บน production ไฟล์ server.js ถูกใช้งานจริง เนื่องจากใน Start Command ถูกกำหนดให้รัน node server.js เพื่อสตาร์ต Express server รอรับ HTTP request ตลอดเวลา
2. ตั้งค่าที่เมนู Environment Variables บน Dashboard ของ Render สาเหตุที่ห้าม commit ไฟล์ .env เพราะมักเก็บข้อมูลสำคัญหรือความลับของระบบซึ่งเสี่ยงต่อความปลอดภัยหากเป็นสาธารณะ และสาเหตุที่ /api/info แสดง NOT SET เกิดจากยังไม่ได้ตั้งตัวแปร STUDENT_ID, ตั้งชื่อ Key ผิด หรือยังไม่ได้ redeploy หลังเพิ่มตัวแปร
3. ครั้งแรก 31.8 วินาที / ครั้งที่สอง 27.0 วินาที — ครั้งแรกใช้เวลานานกว่าเนื่องจากระบบเกิด Cold Start (instance ต้องตื่นขึ้นมาทำงานและสร้างการเชื่อมต่อใหม่) ส่วนครั้งที่สองเป็น Warm Start ที่มี instance และ connection พร้อมทำงานอยู่แล้ว
4. เมื่อสั่ง git push โค้ดจะถูกส่งไปที่ GitHub จากนั้น GitHub จะส่ง Webhook ไปแจ้ง Render ให้ดึงโค้ดล่าสุด บิลด์ด้วยคำสั่ง npm install และสตาร์ตเซิร์ฟเวอร์ใหม่โดยอัตโนมัติ ทำให้หน้าเว็บเปลี่ยนเป็น Menu v2 และค่า commit ใน /api/info ตรงกับค่าจาก git log -1 --format=%H เสมอ
5. ไม่สามารถนำมา deploy ตรง ๆ ได้ เพราะแพลตฟอร์ม Free Tier ของ Render รองรับการ deploy แบบ 1 Service ต่อ 1 Web Service เท่านั้น ไม่รองรับการรัน multi-container ผ่าน docker-compose.yml หากต้องการรันระบบข้อ 1 ต้องแยกสร้าง 2 Service หรือใช้บริการ Container Orchestration/VPS