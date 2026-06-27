# DT-508 Workshop 3 — Haar Cascade Detection

โปรเจกต์นี้เป็นส่วนหนึ่งของวิชา DT-508 สาธิตการใช้ **Haar Cascade Classifier** ผ่าน OpenCV เพื่อตรวจจับใบหน้าคน รอยยิ้ม และหน้าแมวจากไฟล์วีดีโอแบบ Real-time

---

## โครงสร้างโปรเจกต์

```
workshop-3/
├── cat.py                   # ตรวจจับหน้าแมวจากวีดีโอ
├── haar_cascade.py          # ตรวจจับใบหน้าคนและรอยยิ้มจากวีดีโอ
├── dataset/
│   ├── haarcascade_frontalcatface.xml       # โมเดล Haar Cascade สำหรับหน้าแมว
│   ├── haarcascade_frontalface_default.xml  # โมเดล Haar Cascade สำหรับใบหน้าคน
│   └── haarcascade_smile.xml                # โมเดล Haar Cascade สำหรับรอยยิ้ม
└── videos/
    ├── 14636116_720_1280_30fps.mp4          # วีดีโอแมวสำหรับทดสอบ
    └── ryan.mp4                             # วีดีโอคนสำหรับทดสอบ
```

---

## ไฟล์และความสามารถ

### `cat.py` — Cat Face Detection
ตรวจจับหน้าแมวจากวีดีโอ และแสดงจำนวนแมวที่พบในแต่ละ frame

**วิธีทำงาน:**
1. โหลดวีดีโอจาก `videos/14636116_720_1280_30fps.mp4`
2. แปลง frame เป็น Grayscale เพื่อลดความซับซ้อน
3. ใช้ `haarcascade_frontalcatface.xml` ตรวจจับหน้าแมว
4. วาดกรอบสีเขียวรอบหน้าแมวแต่ละตัว
5. แสดงจำนวนแมวที่ตรวจพบบนหน้าจอ

**Parameter ที่ใช้:**
| Parameter | ค่า | ความหมาย |
|---|---|---|
| `scaleFactor` | `1.1` | ย่อภาพ 10% ในแต่ละรอบการค้นหา |
| `minNeighbors` | `15` | ต้องมี 15 detection ซ้อนกันถึงจะนับว่าเจอ (ป้องกัน false positive) |
| `minSize` | `(80, 80)` | ขนาดหน้าแมวขั้นต่ำที่จะตรวจจับ |

---

### `haar_cascade.py` — Face & Smile Detection
ตรวจจับใบหน้าคนและรอยยิ้มจากวีดีโอพร้อมกัน

**วิธีทำงาน:**
1. โหลดวีดีโอจาก `videos/ryan.mp4`
2. แปลง frame เป็น Grayscale
3. ตรวจจับใบหน้าคนด้วย `haarcascade_frontalface_default.xml` — วาดกรอบสีน้ำเงิน
4. ภายในบริเวณใบหน้า (ROI) ค้นหารอยยิ้มด้วย `haarcascade_smile.xml` — วาดกรอบสีเขียว
5. นับจำนวนรอยยิ้มสะสมและแสดงบนหน้าจอ

---

## วิธีรัน

### ติดตั้ง Dependencies
```bash
pip install opencv-python
```

### รันตรวจจับแมว
```bash
python cat.py
```

### รันตรวจจับใบหน้าและรอยยิ้ม
```bash
python haar_cascade.py
```

กด `q` เพื่อหยุดโปรแกรม

---

## Haar Cascade คืออะไร

**Haar Cascade** เป็น Machine Learning model แบบ Classical ที่ใช้ตรวจจับวัตถุในภาพ พัฒนาโดย Viola และ Jones ปี 2001 โดยเรียนรู้จาก feature ของภาพที่เรียกว่า "Haar-like features"

**ข้อดี:** เร็ว ทำงานได้บน CPU ทั่วไป
**ข้อเสีย:** แม่นยำน้อยกว่า Deep Learning โดยเฉพาะเมื่อวัตถุอยู่ในมุมที่แปลก หรือแสงไม่ดี

โมเดลที่ใช้ในโปรเจกต์นี้ดาวน์โหลดมาจาก:
https://github.com/austinjoyal/haar-cascade-files/tree/master
