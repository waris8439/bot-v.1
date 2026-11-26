# ผู้ช่วยส่วนตัว – แอพมือถือ (Android + iOS)

โค้ดแอพอยู่ใน `www/` (ไฟล์เดียวกับเว็บ ฟีเจอร์ครบเหมือนเดิม) ห่อเป็นแอพจริงด้วย Capacitor

## วิธีที่ 1: ติดตั้งทันทีแบบ PWA (ไม่ต้องบิลด์)
อัปโหลดโฟลเดอร์ `www/` ขึ้นเว็บที่เป็น https (GitHub Pages / Netlify / Cloudflare Pages ฟรี) แล้วเปิดจากมือถือ
- Android (Chrome): เมนู ⋮ → ติดตั้งแอป
- iPhone (Safari): ปุ่มแชร์ → เพิ่มลงหน้าจอโฮม

## วิธีที่ 2: Android APK (ไม่ต้องลง Android Studio)
1. สร้าง repo บน GitHub แล้วอัปโหลดไฟล์ทั้งหมดในโฟลเดอร์นี้ (รวม `.github`)
2. แท็บ Actions → Build Android APK → Run workflow
3. ดาวน์โหลด `app-debug-apk` จาก Artifacts แล้วส่งเข้ามือถือติดตั้ง (เปิดอนุญาตติดตั้งจากแหล่งอื่น)

หรือบิลด์เองบนเครื่อง: `npm install && npx cap add android && npx capacitor-assets generate --android && npx cap sync && npx cap open android` แล้วกด Build ใน Android Studio
(ถ้าต้องการให้ขอตำแหน่งได้ ให้เพิ่ม ACCESS_COARSE_LOCATION และ ACCESS_FINE_LOCATION ใน AndroidManifest.xml)

## วิธีที่ 3: iOS (ต้องใช้ Mac + Xcode)
```
npm install
npx cap add ios
npx capacitor-assets generate --ios
npx cap sync ios
npx cap open ios
```
ใน `ios/App/App/Info.plist` เพิ่ม
`NSLocationWhenInUseUsageDescription` = "ใช้แสดงสภาพอากาศและฝุ่นใกล้ตัว"
แล้วเลือก Team (Apple ID) ใน Xcode กด Run ลงเครื่อง
ถ้าจะขึ้น App Store ต้องมี Apple Developer Program (ประมาณ 99 USD/ปี)
ไม่มี Mac: ใช้บริการคลาวด์ เช่น Codemagic หรือ Ionic Appflow แทนได้

## หมายเหตุ
- ข้อมูลยังเก็บใน Google Sheets ตาม URL ที่ตั้งไว้เหมือนเดิม ถ้าไม่ตั้งจะเก็บในเครื่อง
- แก้ไฟล์ `www/index.html` แล้วรัน `npx cap sync` เพื่ออัปเดตแอพ
