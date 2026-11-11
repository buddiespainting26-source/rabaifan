# Atelier Manager Cloud — GitHub Pages + Supabase

## ก่อนเริ่ม
ชุดนี้เพิ่มหน้า Login และ Cloud sync ให้กับ PWA เดิม โดยคงหน้าหลักเดิมไว้
รุ่นเริ่มต้นเก็บข้อมูลของร้านเป็น JSON payload หนึ่งแถวใน `workspace_state` เพื่อให้เข้ากับโครงสร้างเดิมได้ก่อน ใช้ revision check ป้องกันการเขียนทับกันเงียบ ๆ เมื่อสองเครื่องแก้พร้อมกัน หากชนกัน ระบบโหลดข้อมูลล่าสุดและให้ผู้ใช้ตรวจสอบ/ทำรายการใหม่

การจัดการสมาชิกในรุ่นนี้ทำผ่าน Supabase Dashboard/SQL Editor โดย Owner เท่านั้น ยังไม่มีหน้าจัดการสมาชิกในแอป และยังไม่ใช่ offline-write queue

## 1) สร้าง Supabase
1. ไปที่ https://supabase.com/dashboard แล้วสร้าง New project
2. เปิด SQL Editor
3. รันไฟล์ `supabase/migrations/001_atelier_cloud.sql`

## 2) สร้าง Owner และ Workspace
1. ไป Authentication > Users > Add user เพื่อสร้าง Owner
2. คัดลอก UUID ของ Owner
3. รัน `insert into public.businesses(name) values ('Atelier Manager') returning id;`
4. คัดลอก Business UUID แล้วรัน:
   `insert into public.business_members(business_id,user_id,role) values ('BUSINESS_UUID','OWNER_USER_UUID','owner');`

## 3) เพิ่ม Member
1. Authentication > Users > Invite user
2. คัดลอก UUID ของสมาชิกที่ได้รับเชิญ
3. รัน:
   `insert into public.business_members(business_id,user_id,role) values ('BUSINESS_UUID','MEMBER_USER_UUID','member');`

## 4) ตั้งค่าการเชื่อมต่อ
ไป Project Settings > API Keys หรือ Project Connect แล้วคัดลอก:
- Project URL
- Publishable key (`sb_publishable_...`)

ใส่ใน `supabase-config.js`:
```js
window.ATELIER_SUPABASE_CONFIG = {
  url: "https://YOUR_PROJECT_REF.supabase.co",
  publishableKey: "sb_publishable_..."
};
```
ห้ามใช้ Secret Key หรือ `service_role` ในหน้าเว็บ

## 5) ทดสอบ
1. เปิดเว็บผ่าน HTTPS (GitHub Pages) หรือ localhost ไม่ใช่ file://
2. Login ด้วย Owner
3. **ครั้งแรกให้ Login Owner จากอุปกรณ์/เบราว์เซอร์เดิมที่มีข้อมูล Atelier Manager ใน localStorage อยู่** เพื่อให้ระบบนำข้อมูลเดิมขึ้น Cloud; ถ้าเปิดจากเครื่องใหม่ที่ไม่มีข้อมูลก่อน ระบบอาจสร้าง workspace ว่างเป็นชุดแรก
4. ตรวจข้อมูลที่แสดงและเก็บ backup เดิมไว้
5. Login ด้วย Member บนอุปกรณ์/เบราว์เซอร์อีกเครื่อง
6. ทดลองบันทึกและดูการอัปเดต Realtime
7. ทดสอบกรณีแก้ไขพร้อมกัน และตรวจยอดเงิน/สต็อกก่อนใช้งานจริง

## 6) GitHub Pages
อัปโหลดไฟล์และโฟลเดอร์ทั้งหมดใน ZIP ไปยัง root ของ repository จากนั้น Settings > Pages > Deploy from a branch > main > /(root)

## PWA
- iPhone/iPad: Safari > Share > Add to Home Screen
- Android: Chrome > Install app
- Desktop: เมนูเบราว์เซอร์ > Install app (ถ้ารองรับ)

## ข้อจำกัดและงานระยะถัดไป
- JSON workspace payload เป็นสะพานเชื่อมระบบเดิม ยังไม่ใช่ relational schema เต็มรูปแบบ
- ยังไม่มีหน้าจัดการสมาชิกในแอป (Owner เพิ่ม/ลบสมาชิกผ่าน Supabase Dashboard/SQL)
- Realtime จะโหลดหน้าใหม่เมื่อมีการเปลี่ยนข้อมูลจากอีกเครื่อง
- หากมีการบันทึกพร้อมกัน revision check จะป้องกันการเขียนทับแบบเงียบ แต่ผู้ใช้ที่ชนกันต้องตรวจสอบและทำรายการใหม่
- ยังไม่รองรับการบันทึกขณะออฟไลน์
- รูปภาพสินค้าเดิมอาจเก็บเป็น Data URL ใน payload; ควรย้ายไป Supabase Storage เพื่อให้เหมาะกับการใช้งานระยะยาว
- เก็บ ZIP backup เดิมก่อน migrate และตรวจสอบข้อมูลทั้งหมดก่อนเปิดใช้งานจริง
