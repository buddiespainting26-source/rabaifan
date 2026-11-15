ATELIER MANAGER — LOCAL EDITION (LOGO UPDATE)

ไฟล์ในชุดนี้เป็นไฟล์ที่จำเป็นสำหรับ GitHub Pages เท่านั้น:
- index.html             หน้าแอปและระบบจัดการทั้งหมด
- manifest.webmanifest   ข้อมูลสำหรับติดตั้งเป็น PWA
- sw.js                  Service Worker / cache ของแอป
- icon-192.png           ไอคอนแอป 192x192
- icon-512.png           ไอคอนแอป 512x512
- favicon.png            ไอคอนแท็บเบราว์เซอร์

วิธีอัปเดต Repository เดิมอย่างปลอดภัย
1) เปิดแอปเดิม แล้วไปที่ ตั้งค่า > ส่งออกข้อมูลสำรอง (JSON) เพื่อเก็บข้อมูลไว้ก่อน
2) ดาวน์โหลด ZIP นี้และแตกไฟล์
3) ใน GitHub Repository เดิม ให้อัปโหลดไฟล์ทั้ง 6 รายการจากโฟลเดอร์นี้ไปไว้ที่ Root (ระดับเดียวกับ index.html เดิม)
4) เลือก Replace/Commit changes เมื่อ GitHub ถามให้แทนที่ไฟล์เดิม
5) รอ GitHub Pages เผยแพร่ แล้วเปิดเว็บใหม่/รีเฟรชแบบล้าง cache หากจำเป็น

การลบไฟล์เก่า
- ไม่จำเป็นต้องลบ Repository หรือสร้าง Repository ใหม่
- หลังอัปโหลดชุดนี้และทดสอบว่าเว็บเปิดได้แล้ว ค่อยลบไฟล์ที่เกี่ยวกับระบบ Cloud เดิม เช่น supabase-config.js, ไฟล์ config/auth/cloud เฉพาะที่ใช้กับ Supabase และไฟล์สำรอง ZIP/ไฟล์ทดสอบที่ไม่ใช่ส่วนของเว็บไซต์
- อย่าลบ .git, โฟลเดอร์ .github (ถ้ามี), หรือไฟล์ workflow ที่ใช้ deploy GitHub Pages
- อย่าลบ index.html, manifest.webmanifest, sw.js, icon-192.png, icon-512.png, favicon.png ที่เป็นชุดใหม่นี้
- ถ้าไม่แน่ใจว่าไฟล์ใดเป็นไฟล์ Cloud อย่าเพิ่งลบ ส่งภาพหน้า Repository มาให้ตรวจสอบก่อน

ข้อมูลและข้อจำกัด
- แอปนี้ใช้ Local Storage ในเบราว์เซอร์ของแต่ละอุปกรณ์ ไม่ใช้ Supabase หรือ Cloud database
- คอมพิวเตอร์และ iPad มีข้อมูลแยกกัน การย้ายข้อมูลใช้ Export/Import JSON
- การล้างข้อมูลเว็บไซต์/Browser data อาจทำให้ข้อมูลในเครื่องนั้นหาย ควรสำรอง JSON เป็นประจำ
- รูปโลโก้ใหม่ถูกใช้ในหัวแอป, ไอคอน PWA และ favicon
