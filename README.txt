ATELIER PAINTING WORKSHOP MANAGER — PREVIEW 0.4
รายรับ: เลือกวันที่อย่างเดียว (ไม่มีเวลา), เลือกประเภทลูกค้า เด็ก/คู่รัก/ผู้ใหญ่/วัยรุ่น
เลือกสินค้าได้หลายรายการในบิลเดียว และแสดงรูปสินค้าเมื่อเลือก
สต็อก: เพิ่มชื่อ รายละเอียด รูปภาพ จำนวน ต้นทุนต่อหน่วย และราคาขายต่อหน่วย
รูปภาพเก็บในเบราว์เซอร์และรวมอยู่ในไฟล์ JSON backup
เมื่อบันทึกการขายจะตัดสต็อกตามจำนวน
ข้อมูลยังอยู่ในเบราว์เซอร์เครื่องนี้ ยังไม่ได้เชื่อม Supabase/ฐานข้อมูลออนไลน์
เปิด index.html ใน Chrome เพื่อทดลอง


Version 0.6 update:
- Added full product editing in stock: name, description, quantity, unit, cost, sale price, and image.
- Existing image is retained when editing unless a replacement image is selected.
- Kept the quick quantity adjustment button.


Version 0.7 update:
- Expense form now uses date only; time and payment-channel fields removed.
- Expense categories are dynamic and can be added by the user.
- Selecting the "สินค้า" category reveals product, quantity, unit, and total purchase cost fields.
- Saving a product expense automatically adds quantity to the selected stock item or creates a new stock item.
- Purchase total is recorded as an expense and unit cost is updated using a weighted average.
- Expense list shows date, category, item, quantity, and total expense.


Version 0.8 update:
- Product purchase selector is populated directly from the current stock products list.
- Selecting an existing stock product shows its current quantity, unit cost, and sale price.
- The purchase unit defaults to the selected stock product's unit.
- Shows the purchase's calculated unit cost before saving.
- Stock cards display unit cost and sale price as separate, clearly labeled values.
- Saving a purchase increases the selected product's stock quantity, updates weighted-average unit cost, and preserves the product's sale price.
