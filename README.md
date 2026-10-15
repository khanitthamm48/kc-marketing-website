# KC MARKETING CMS — starter kit

เว็บ React + Vite พร้อมหน้าบริษัท, portfolio, news และหน้า Admin ที่ล็อกอินผ่าน Supabase Auth

## ข้อมูลที่ใส่ไว้แล้ว
- LINE: `@155vpvkt` → https://line.me/R/ti/p/@155vpvkt
- โทรศัพท์: `0633136927`
- ดีไซน์: Modern Luxury ดำ/ทอง
- ผู้ดูแล: ออกแบบสำหรับผู้ดูแล 1 บัญชี

## สิ่งที่ต้องเตรียมก่อนเปิดใช้จริง
1. สร้างโปรเจกต์ Supabase และคัดลอก Project URL กับ publishable/anon key
2. เปิด SQL Editor แล้วรัน `supabase/schema.sql`
3. ใน Supabase Auth สร้างผู้ใช้ผู้ดูแล 1 คนด้วยอีเมล/รหัสผ่าน จากนั้นคัดลอก UUID ของผู้ใช้นั้น แล้วเพิ่มลงใน `public.admin_users` ตามคำสั่งตัวอย่างท้ายไฟล์ SQL และปิดการสมัครสมาชิกสาธารณะ
4. สร้างไฟล์ `.env` จาก `.env.example` แล้วกรอกค่า:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
5. ติดตั้งและรัน:
   ```bash
   npm install
   npm run dev
   ```
6. ทดสอบหน้าเว็บ, ล็อกอิน, เพิ่ม/แก้ไข/ลบผลงานและข่าวสาร
7. Deploy ไป Cloudflare Pages หรือ Vercel และตั้ง Environment Variables ซ้ำในหน้า Hosting

## ข้อควรระวังด้านความปลอดภัย
- ใช้เฉพาะ publishable/anon key ใน frontend เท่านั้น
- ห้ามนำ `service_role` หรือ secret key ใส่ใน `.env` ฝั่งเว็บ
- สร้างบัญชี Auth ผู้ดูแลด้วยตนเองเพียงบัญชีเดียว และปิด public sign-up
- SQL ใช้ตาราง `admin_users` เป็น allowlist และตรวจ `auth.uid()` ก่อนอนุญาตเขียน/แก้ไข/ลบเนื้อหา
- ก่อนเผยแพร่จริง ควรเพิ่ม storage bucket สำหรับอัปโหลดรูป, rate limiting, backup และทดสอบ security policies

## ข้อจำกัดของชุดเริ่มต้น
ชุดนี้เป็น source code ที่เตรียมโครงสร้างการเชื่อมต่อฐานข้อมูลและล็อกอินไว้ แต่ยังไม่ออนไลน์จนกว่าจะสร้าง Supabase project, ใส่ keys, สร้างบัญชี admin และ deploy เอง


## Deploy on Cloudflare Pages (Free plan)
- Connect the GitHub repository in Cloudflare Dashboard > Workers & Pages > Create > Pages > Connect to Git.
- Framework preset: Vite
- Build command: `npm run build`
- Build output directory: `dist`
- Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` as production environment variables.
- Deploy. Test the generated `*.pages.dev` URL before attaching the purchased domain.
- For `kcmarketing.com` (apex/root domain), add the domain as a Cloudflare zone and change the registrar's nameservers to the two nameservers Cloudflare assigns. Then in Pages > project > Custom domains, add `kcmarketing.com` and follow activation checks.
- Also add `www.kcmarketing.com` as a custom domain if you want the www address, then configure the redirect/canonical URL after it is active.

The `.com` registration itself is a separate paid annual registration; Cloudflare Pages hosting can remain on the Free plan. Domain availability and current registrar pricing must be checked at the time of purchase.
