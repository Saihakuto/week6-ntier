# 📋 Task Board - N-Tier Architecture (Week 6)

โปรเจกต์ระบบจัดการงาน (Task Board) ที่พัฒนาขึ้นโดยใช้สถาปัตยกรรมแบบ **N-Tier Architecture บน Single VM** ซึ่งเป็นการจำลองการแยกส่วนประกอบของระบบ (Physical Separation) เพื่อความปลอดภัย การจัดการที่ง่ายขึ้น และเตรียมพร้อมสำหรับการขยายตัว (Scalability) ในอนาคต

## 🏗️ Architecture Overview

ระบบถูกออกแบบโดยแบ่งออกเป็น 3 Tiers หลัก ดังนี้:

1. **🌐 Tier 1: Web Server (Nginx)** - ทำหน้าที่เป็น Reverse Proxy
   - จัดการ SSL Termination (HTTPS Port 443)
   - ให้บริการ Static Files (HTML, CSS, JS)
2. **⚙️ Tier 2: Application Server (Node.js + Express)** - ทำหน้าที่ประมวลผล Business Logic (Port 3000)
   - ให้บริการ RESTful API
   - ออกแบบโครงสร้างภายในแบบ Layered Architecture (Controllers, Services, Repositories)
3. **🗄️ Tier 3: Database Server (PostgreSQL)** - ทำหน้าที่จัดเก็บข้อมูล (Port 5432)
   - จัดการ ACID Transactions และ Connection Pooling

**Request Flow:** `Browser` ➔ `Nginx (HTTPS)` ➔ `Node.js (API)` ➔ `PostgreSQL (Data)`

## 🛠️ Technologies Used

| Tier | Component | Technology | Version |
| :--- | :--- | :--- | :--- |
| **Web** | Web Server / Proxy | Nginx | 1.24+ |
| **App** | Backend API | Node.js + Express.js | 20+ |
| **Data** | Database | PostgreSQL | 16+ |
| **Client**| Frontend UI | HTML5, CSS3, Vanilla JS | - |


```

## 🚀 Quick Start

### 1. Requirements
* Ubuntu VM (22.04 / 24.04)
* Node.js (v20+)
* PostgreSQL installed and configured
* Nginx installed and configured with self-signed SSL

### 2. Start All Services
สามารถรันสคริปต์เพื่อเปิดใช้งานทั้ง PostgreSQL, Nginx และ Node.js (ผ่าน PM2) ได้ในคำสั่งเดียว:

```bash
chmod +x scripts/start-all.sh
./scripts/start-all.sh
```

### 3. Access the Application
เปิด Web Browser และเข้าถึงระบบผ่าน HTTPS (ต้องกดยอมรับ Self-signed Certificate):

* **Frontend URL:** `https://taskboard.local`
* **Health Check API:** `https://taskboard.local/api/health`

*(หมายเหตุ: ต้องมีการตั้งค่า `127.0.0.1 taskboard.local` ในไฟล์ `/etc/hosts` ของเครื่อง Client)*

## 🧪 Testing

รัน API Test script เพื่อตรวจสอบการทำงานของ Endpoints ทั้งหมด:

```bash
chmod +x scripts/test-api.sh
./scripts/test-api.sh
```
