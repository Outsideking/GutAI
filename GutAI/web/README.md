# GutAI API Console

หน้าเว็บแบบ static สำหรับทดลองเรียก endpoint ที่ระบุไว้:

- `POST /v1/iot/light/on`
- `POST /v1/iot/light/off`
- `POST /v1/chat` — ส่ง `{ provider, message, user }`
- `POST /v1/studio/create` — ส่ง `{ topic, user }`
- `GET /v1/search?q=...`
- `POST /v1/gc/install` — ส่ง `{ token }`
- `POST /v1/sale/issue-token` — ส่ง `{}` เนื่องจากข้อมูล endpoint ที่ให้มาไม่ได้ระบุ body

## ใช้งาน

เปิด `index.html` ผ่านเว็บเซิร์ฟเวอร์ static เช่น GitHub Pages หรือโฮสต์เว็บของคุณ แล้วใช้แบบฟอร์มบนหน้าเว็บได้เลย ไม่ต้องติดตั้งแพ็กเกจเพิ่มเติม

ตัวอย่างรันในเครื่องจากโฟลเดอร์ repository:

```bash
python -m http.server 8000
```

จากนั้นเปิด `http://localhost:8000/GutAI/web/` ในเบราว์เซอร์

## ข้อควรทราบ

- API ถูกเรียกจาก browser โดยตรงที่ `https://api.cristal.com` หากการเรียกถูกบล็อก ให้ตรวจสอบ CORS ของ API และให้แน่ใจว่า API รองรับ origin ที่ใช้โฮสต์เว็บ
- หน้าเว็บไม่ฝังหรือเก็บ API secret/token กลางไว้ ผู้ใช้กรอก install token เฉพาะตอนใช้งาน และหน้านี้ล้างช่องหลังส่งคำขอ
- หากต้องใช้ secret ส่วนกลาง ให้ทำ backend proxy ของคุณเองและเก็บ secret ใน environment variable ฝั่งเซิร์ฟเวอร์ ไม่ควรใส่ secret ใน static frontend
- API schema ที่ผู้ใช้ให้มาไม่ได้ระบุ search parameter และ request body ของ `/v1/sale/issue-token`; หน้านี้ใช้ `q` สำหรับ search และส่ง `{}` สำหรับ issue-token ตามรูปแบบที่พบได้ทั่วไป แต่ต้องปรับตามเอกสารจริงของ API หากต่างออกไป
- ปุ่มเปิด/ปิดไฟ, ติดตั้ง และออก token ขอการยืนยันก่อนส่งคำขอ เนื่องจากอาจมีผลต่ออุปกรณ์หรือบัญชีจริง
