# aipass bridge

**ทำให้ AiPASS ใช้งานได้เต็มที่ยิ่งขึ้น — ตอนนี้ใช้ผ่าน Terminal ได้แล้ว**

AiPASS เปิดให้คนไทยเข้าถึงโมเดล AI ระดับโปรมากกว่า 30 โมเดลได้ฟรี โปรเจกต์นี้นำ AiPASS มาเชื่อมกับ Terminal, Editor และเครื่องมือที่รองรับ OpenAI-compatible API พร้อมความสามารถในการอ่านและเขียนไฟล์ภายในเครื่อง

## ทำอะไรได้บ้าง

- แชตจาก Terminal แบบ streaming พร้อม Web Search และแหล่งอ้างอิง
- ใช้โมเดลทั้งหมดที่บัญชีเลือกได้ รวม 33 โมเดล ทั้งโมเดลสร้างภาพ วิดีโอ และเพลง
- สร้างภาพและรับไฟล์ PNG
- แนบเอกสารและถามเกี่ยวกับเอกสาร
- สร้างวิดีโอและเพลง เช่น Seedance, Veo และ Lyria
- แก้ไขไฟล์ในเครื่องด้วย agent ที่อ่าน ค้นหา และแก้ไขโปรเจกต์
- ตรวจสอบ credit pool ได้จาก popup และหลังการทำงานของ agent
- ใช้เป็น OpenAI-compatible endpoint สำหรับ SDK และเครื่องมือที่รองรับ Base URL
- รันแบบ headless บนเซิร์ฟเวอร์ได้

Credential ไม่ออกจากเบราว์เซอร์ คำขอจริงทำงานภายในแท็บ Chrome ที่ล็อกอินอยู่ และ bridge จะไม่เห็น session cookie หรือเขียน credential ลงดิสก์

## เริ่มต้นใช้งาน

    npm run dev

จากนั้นเปิด chrome://extensions → Developer mode → Load unpacked → เลือก aipass-bridge/extension และเปิดแท็บ https://de.aipass.net/chat โดย popup ควรแสดง Connected

### คำสั่งที่ใช้บ่อย

    npm run doctor
    npm run setup-assistant
    npm run chat -- "ช่วยสรุปข่าว AI วันนี้"
    npm run chat -- "แมวน่ารัก" --model gpt-image-2
    npm run chat -- "summarise this" --file report.pdf
    npm run chat -- "a street at night" --model seedance-2.0-mini
    npm run agent -- "add a /health route" --root .
    npm run models
    npm run credits

หมายเหตุ: ต้องใส่ -- ก่อน flags ที่เป็นของ script เอง เช่น npm run chat -- --new ทุกคำสั่งสามารถใช้ -- --help เพื่อดูวิธีใช้งานได้

หากมีปัญหา npm run doctor จะตรวจสอบ chain ทั้งหมดและระบุจุดที่ต้องแก้

## ใช้เป็น OpenAI-compatible API

Bridge เปิด endpoint สำหรับเครื่องมือที่รองรับ OpenAI-compatible API โดยใช้ Base URL ของ bridge เป็น http://127.0.0.1:8787/v1

## เอกสาร

- เอกสารฉบับเต็ม — การติดตั้ง, coding assistant, conversations, models, การสร้างภาพ/วิดีโอ/เพลง, credits, configuration, troubleshooting และ tests
- Headless deployment — Docker + noVNC สำหรับรัน 24×7 บนเซิร์ฟเวอร์

## หมายเหตุ

โปรเจกต์นี้ทำงานผ่านบัญชี AiPASS ของคุณเอง โดยใช้แท็บเบราว์เซอร์ที่คุณล็อกอินอยู่ ไม่ได้ bypass authentication, scrape หรือแชร์ credential ใด ๆ แต่เป็นการเพิ่ม developer interface ให้กับบริการที่มีอยู่

ควรใช้งานอย่างเหมาะสม และแนะนำให้เก็บ bridge ไว้บนเครื่องหรือเครือข่ายที่คุณควบคุมได้

## ความปลอดภัย

Bridge ไม่มี authentication ของตัวเอง ควร bind ไว้ที่ 127.0.0.1 เท่านั้น เพราะทุกสิ่งที่เข้าถึงพอร์ตได้อาจใช้ credit ของบัญชี AiPASS ได้

หาก clone หรือ fork ก่อนวันที่ 2 กันยายน 2026 ควรอัปเดต เนื่องจากสำเนาก่อน commit 8cad676 มี bridge ที่เว็บไซต์ที่คุณเข้าชมอาจสั่งงานได้ โปรดดู SECURITY.md

## การมีส่วนร่วม

ดูรายละเอียดใน CONTRIBUTING.md โดยควรตรวจสอบ git config user.email ก่อน commit, รัน npm test และระบุไฟล์ทุกไฟล์ที่แก้ไข

## Credits

- astrathezero — headless Docker deployment, image upload และ offscreen keepalive
- meatasit — Windows path resolution ใน test harness และบั๊กของ CLI 2 รายการ

## License

MIT — ยินดีรับ contributions ภายใต้เงื่อนไขเดียวกัน
