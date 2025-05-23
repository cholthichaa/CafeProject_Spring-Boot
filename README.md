# Cafe Management System

ระบบจัดการร้านกาแฟที่ช่วยบริหารงานร้านอย่างมีประสิทธิภาพ รองรับการจัดการสมาชิก สินค้า หมวดหมู่ สต็อกสินค้า การขาย และรายงานยอดขาย

---

#### ภาพรวมระบบ
ระบบจัดการร้านกาแฟนี้ถูกออกแบบมาเพื่อช่วยในการบริหารงานร้านกาแฟอย่างมีประสิทธิภาพ รองรับการจัดการข้อมูลสมาชิก, สินค้า, หมวดหมู่สินค้า, วัตถุดิบ, สต็อกสินค้า, การขาย และรายงานต่าง ๆ เพื่อให้ร้านสามารถติดตามการขายและสต็อกสินค้าได้อย่างแม่นยำ รวมถึงการจัดการข้อมูลผู้ใช้งานทั้งพนักงานและผู้ดูแลระบบ


---

#### ภาษาและเทคโนโลยีที่ใช้
- **ภาษาโปรแกรม:** Java (Spring Boot Framework)  
- **Frontend:** HTML  
- **ฐานข้อมูล:** MySQL  
- **IDE:** IntelliJ IDEA  
- **Framework และเครื่องมือเสริม:**  
  - Spring Boot (ใช้สถาปัตยกรรม MVC)  
  - Spring Security (จัดการระบบล็อกอินและสิทธิ์การใช้งาน)  
  - JPA / Hibernate (ORM เชื่อมฐานข้อมูล)  
  - Lombok (ช่วยลดโค้ด boilerplate เช่น getter/setter)  

---

#### โครงสร้างระบบ (Architecture)
ใช้รูปแบบ **Model-View-Controller (MVC)**  
- **Model:** จัดการข้อมูลและแมปกับฐานข้อมูล (Entity Classes เช่น Admin, Customer, Product, Category, ShoppingCart, CartItem)  
- **View:** ส่วนแสดงผลบนเว็บ (HTML)  
- **Controller:** ตัวกลางประสานงานระหว่าง Model และ View รับคำขอจากผู้ใช้และประมวลผล  

---

#### ฐานข้อมูลและ Entity หลัก
- **Admins:** ข้อมูลผู้ดูแลระบบ  
- **Customers:** ข้อมูลลูกค้า  
- **Products:** รายละเอียดสินค้า เช่น ชื่อ, ราคา, รูปภาพ, สถานะ  
- **Categories:** หมวดหมู่สินค้า  
- **ShoppingCart:** ตะกร้าสินค้าของลูกค้า  
- **CartItems:** รายการสินค้าในตะกร้า  

**ความสัมพันธ์สำคัญ**  
- ลูกค้า (Customer) 1:1 ตะกร้าสินค้า (ShoppingCart)  
- ตะกร้าสินค้า 1:N รายการสินค้า (CartItem)  
- รายการสินค้า 1:1 สินค้า (Product)  
- สินค้า N:1 หมวดหมู่ (Category)  

---

#### ฟังก์ชันหลักของระบบ
- **จัดการข้อมูลผู้ใช้:**  
  - สมัครสมาชิก  
  - แก้ไขข้อมูลส่วนตัว  
  - ระบบล็อกอินและสิทธิ์เข้าถึง (Spring Security)  

- **จัดการสินค้าและคลังสินค้า:**  
  - เพิ่ม/แก้ไข/ลบสินค้าและหมวดหมู่  
  - ตรวจสอบและอัปเดตสต็อกสินค้าและวัตถุดิบ  

- **การขายสินค้า:**  
  - ลูกค้าเลือกสินค้าและเพิ่มในตะกร้า  
  - คำนวณราคาสินค้าในตะกร้า  
  - ติดตามยอดขายและประวัติการสั่งซื้อ  

- **ระบบผู้ดูแล (Admin):**  
  - ตรวจสอบและแก้ไขข้อมูลสมาชิก  
  - จัดการคำสั่งซื้อและยอดขาย  
  - สร้างรายงานต่างๆ  

---

#### การเชื่อมต่อฐานข้อมูล
- ใช้ **Spring Data JPA** เชื่อมต่อ MySQL  
- กำหนด Entity ด้วย annotation เช่น `@Entity`, `@Table`, `@Id`, `@GeneratedValue`  
- Repository interfaces สำหรับ Query ข้อมูล เช่น `AdminRepository`, `CustomerRepository`  

---

#### การจัดการ Dependency และ Injection
- การจัดการ Dependency และ Injection ใช้ @Autowired ใน Spring Boot เพื่อให้โปรแกรมเอา Service หรือ Repository มาใช้แบบอัตโนมัติ แทนที่เราจะต้องสร้างเองด้วยคำสั่ง new Spring จะจัดการสร้างให้อัตโนมัติเลย ช่วยให้โค้ดง่ายขึ้น ไม่ต้องเขียนซ้ำ และทำให้แต่ละส่วนเชื่อมต่อกันได้แบบง่าย ๆ ทำให้แก้ไขหรือปรับปรุงโค้ดในอนาคตได้สะดวกขึ้น
- แยก Business Logic ออกจาก Controller ผ่าน Service Layer  

---

#### วิธีใช้งานเบื้องต้น
1. สร้างฐานข้อมูล MySQL ตาม schema ที่กำหนด  
2. รันโปรเจกต์ด้วย IntelliJ IDEA หรือ IDE ที่รองรับ Spring Boot  
3. เข้าใช้งานผ่านเว็บเบราว์เซอร์  
4. ผู้ดูแลระบบล็อกอินเพื่อจัดการสินค้าและคำสั่งซื้อ  
5. ลูกค้าสมัครสมาชิกและสั่งซื้อสินค้าได้  

---
