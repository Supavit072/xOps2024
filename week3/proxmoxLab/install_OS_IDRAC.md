# การติดตั้ง Proxmox และการทำ Cluster ด้วย IDRAC

## ขั้นตอนการติดตั้ง Proxmox 8.2 ผ่าน IDRAC

### 1. เชื่อมต่อ VPN ของเซิร์ฟเวอร์ผ่าน FortiClient VPN
- ![fortiClientVPN](/image/fortiClientVPN.png)

### 2. การเข้า Login IDRAC ผ่าน IP
- เข้าสู่ระบบ IDRAC โดยใช้ IP 10.85.xxx.xxx
- ![568B](/image/Straight_through_Cable_568B.jpg)
- ![568B](/image/Straight_through_Cable_568B.jpg)

### 3. การบูตแผ่นติดตั้ง Proxmox
- เข้าสู่เมนู Virtual Media ใน IDRAC
- เลือก `Connect Virtual Media` และเลือกไฟล์ ISO ของ Proxmox 8.2
- รีบูตเซิร์ฟเวอร์และเข้าสู่เมนู Boot
- เลือกบูตจาก Virtual CD/DVD/ISO

### 4. การติดตั้ง Proxmox 8.2
- เมื่อเข้าสู่หน้าจอการติดตั้ง Proxmox ให้คลิก "Install Proxmox VE"
- เลือก Hard Disk ที่ต้องการติดตั้ง Proxmox VE และเลือก Filesystem ที่ต้องการ (ext4, xfs, zfs, btrfs)
  - **ext4**: เหมาะสำหรับการใช้งานทั่วไป
  - **xfs**: เหมาะสำหรับการจัดการไฟล์ขนาดใหญ่
  - **zfs**: เหมาะสำหรับความปลอดภัยและการจัดการข้อมูล
  - **btrfs**: เหมาะสำหรับการทำ Snapshot
- กำหนดค่าขนาดของ Hard Disk, Swap, Root, Min Free, และ VZ ตามต้องการ
- ตั้งค่า Network Configuration และตั้งค่า IP Address เช่น 10.85.xxx.xxx/24

### 5. การเข้าสู่ Proxmox
- เปิดเบราว์เซอร์และเข้าสู่ Proxmox ด้วย IP 10.85.xxx.xxx:8006
- ![568B](/image/Straight_through_Cable_568B.jpg)

### 6. การอัปเดต Repository ของ Proxmox
- เลือก `Repositories`
- ลบ `Enterprise Repository`
- เพิ่ม `No-Subscription Repository` โดยการคลิก "Add" และเลือก "No-Subscription"
- เพิ่ม `Ceph Reef No-Subscription Repository` ในลักษณะเดียวกัน
- ![568B](/image/Straight_through_Cable_568B.jpg)
- ![568B](/image/Straight_through_Cable_568B.jpg)

### 7. การกำหนด Network
- ไปที่ `Datacenter` และเลือก `Node` ที่ต้องการกำหนด Network
- เลือก `Network`
- ลบ `vmbr0` ที่เป็น Linux Bridge
- สร้าง `vmbr0` ที่เป็น OVS Bridge ใหม่ โดยเลือก "Create" และเลือก "OVS Bridge"
- ตั้งค่า `vmbr851` โดยเลือก "Create" และเลือก "OVS Bridge" จากนั้นตั้งค่า IP Address เป็น 10.85.xxx.xxx/24 และ Gateway เป็น 10.85.xxx.xxx
- ตั้งค่า Bridge Port เป็น `eno1`
- สร้าง `ovs bond0` โดยเลือก "Create" และเลือก "OVS Bond"
- ![568B](/image/Straight_through_Cable_568B.jpg)

### 8. การทำ Cluster
- ทำการติดตั้ง Proxmox ทั้ง 3 Node: cpe001, cpe002, cpe003
- ไปที่ `Datacenter` บน cpe001 และเลือก `Cluster`
- คลิก "Create Cluster" และตั้งชื่อ Cluster
- บันทึก Cluster Config
- ไปที่ cpe002 และ cpe003 และเข้าร่วม Cluster โดยการเลือก `Cluster` และคลิก "Join Cluster" จากนั้นใช้ข้อมูลจาก cpe001 เพื่อเข้าร่วม

### 9. การทำ Ceph
- ไปที่ `Datacenter` และเลือก `Ceph`
- คลิก "Install Ceph"
- สร้าง Monitor โดยเลือก "Create Monitor"
- เพิ่ม OSD โดยเลือก "Create OSD"
- สร้าง CephFS โดยเลือก "Create CephFS"
- สร้าง Pool โดยเลือก "Create Pool"
