# xOps2024

# กิจกรรมครั้งที่ 2: การตั้งค่าและการจัดการเครือข่ายผ่าน Fortigate Firewall

## ขั้นตอนการทำกิจกรรม:

### การเข้าหัวสายแลน
   - UTP (Unshielded Twisted Pair) จำนวน 7 เส้น
   - การต่อแบบตรง (Straight-through Cable หรือ Direct Cable) เพื่อเชื่อมต่อจากเครื่องคอมพิวเตอร์ ไปยังอุปกรณ์ Network
     
![568B](./image/Straight_through_Cable_568B.jpg)

image by เคที.ฮาร์ดแวร์เซอร์วิส

### การต่อสายเครือข่าย:
   - ต่อสาย Internet ที่มี IP Address **192.168.204.XXX** เข้ากับ **port WAN1** ของ Fortigate Firewall 
   - ต่อสายจาก **port 1, 2, 3, 4** ของ Fortigate Firewall เข้ากับ **port 23, 31, 19, 17** ของ Switch 1 ตามลำดับ
   - ต่อสายจาก **port 5** ของ Fortigate Firewall เข้ากับ **port 23** ของ Switch 2
   - ต่อสายจาก **port 24** ของ Switch 1 เข้ากับ PC1

### การกำหนด VLAN:
   - กำหนด VLAN 801-804 สำหรับ Switch 1 (Service)
   - กำหนด VLAN 851-852 สำหรับ Switch 2 (Management)
   - กำหนด IP Subnet ตามนี้:
     - VLAN 801 = **10.80.1.1/24**
     - VLAN 802 = **10.80.2.1/24**
     - VLAN 803 = **10.80.3.1/24**
     - VLAN 804 = **10.80.4.1/24**
     - VLAN 851 = **10.85.1.1/24**
     - VLAN 852 = **10.85.2.1/24**

### การสร้างการสื่อสารระหว่างอุปกรณ์:
   - ทำการตั้งค่าการสื่อสารแบบ VLAN Trunk ระหว่าง Fortigate Firewall กับ Switch 1 และ Switch 2
   - กำหนด Port ที่เชื่อมต่อระหว่างทั้งสามอุปกรณ์ให้เป็น Trunk Port
   - กำหนด VLAN Tagging ให้กับ Port ที่เชื่อมต่อระหว่าง Fortigate Firewall กับ Switch 1 และ Switch 2 เพื่อให้สามารถส่งข้อมูลระหว่าง VLAN ได้

### การสร้างการสื่อสารระหว่าง Switch 1 กับ PC1:
   - กำหนดการสื่อสารระหว่าง Switch 1 กับ PC1 เพื่อให้ PC1 สามารถเข้าถึง Internet และ Fortigate Firewall ได้

### การตรวจสอบและทดสอบ:
   - ทำการตรวจสอบการเชื่อมต่อและการกำหนดค่าที่ถูกต้องให้แน่ใจว่าทุกอุปกรณ์สามารถสื่อสารกันได้ตามที่ต้องการ
   - ทดสอบการเข้าถึง Internet และการสื่อสารระหว่าง PC1 กับ Fortigate Firewall เพื่อให้แน่ใจว่าการตั้งค่าเชื่อมต่อถูกต้องและทำงานได้อย่างถูกต้อง

## หมายเหตุ:
- นี่เป็นคำอธิบายคร่าวๆในสิ่งที่ได้เรียนรู้
- สิ่งที่ได้ศึกษาในวันนี้แต่หลงลืมไปหรือยังไม่เข้าใจทั้งหมด จะไม่ขออธิบายเพื่อป้องกันความผิดพลาด ขออภัยย~

## Diagram
![Diagram Lab 2](./image/Diagram_xOps2024_week_2.png)


