# git-introduction

git เป็น software ควบคุม version ที่มีการเก็บรักษา source code รวมทั้งไฟล์ต่าง ๆ ไว้ในเครื่องคอมพิวเตอร์ของผู้ใช้และบน server ได้พร้อมๆ กัน โดยจะเรียกพื้นที่เก็บไฟล์ว่า  'repository' 

ในขณะที่กำลังพัฒนาโปรแกรมหรือแก้ไขเอกสารต่างๆ เราสามารถใช้ git เป็นตัวช่วยการติดตามการเปลี่ยนแปลงและรวมส่วนต่างๆ ของโปรแกรมหรือเอกสารเข้าด้วยกัน จนกระทั่งได้โปรแกรมหรือเอกสารที่สมบูรณ์ และหากมีข้อผิดพลาด เราสามารถใช้ git เพื่อเปรียบเทียบความแตกต่างระหว่างการแก้ไขในแต่ละรุ่น นอกจากนี้ git ยังมีความสามารถอีกมากมายซึ่งจะได้กล่าวถึงในลำดับถัดไป

ผู้ใช้ที่มีสิทธิ์เข้าถึง repository สามารถช่วยกันพัฒนาโปรแกรมหรือช่วยกันแก้ไขเอกสารได้ โดยสามารถแก้ไขงานได้ที่เครื่องของตนเอง (local) และสามารถ upload การเปลี่ยนแปลงใดๆ ขึ้นไปเก็บบน server ได้ตามต้องการ

ภาพรวมในการทำงานของ git ทั้งฝั่ง local และ server แสดงได้ดังรูปที่ 1

![image](./Pictures/gi-intro/Slide2.PNG)

รูปที่ 1

จากรูปที่ 1 สมมติว่าผู้ใช้ทำการแก้ไข source code ของโปรแกรมบนคอมพิวเตอร์ส่วนบุคคล และใช้ git เป็นตัวช่วยติดตามการเปลี่ยนแปลง

### ฝั่ง Local computer ###

เมื่อผู้ใช้สร้าง local repository ขึ้นใน folder ที่กำลังแก้ไข source code นั้น โปรแกรม  git ก็จะสร้างโฟลเดอร์ที่มี attribute เป็น hidden โดยตั้งชื่อว่า .git 
ทำหน้าที่เป็น local repository เพื่อเอาไว้ sync กับ remote repository บน server

หากเราต้องการจะเข้าไปดูไฟล์ต่าง ๆ ในโฟลเดอร์นั้น เราต้องกำหนดตัวเลือกของ file browser ให้มองเห็นโฟลเดอร์ที่ซ่อนอยู่

#### ภายในโฟลเดอร์ .git ####
ภายในโฟลเดอร์ .git (local repository) จะมีองค์ประกอบสองอย่างคือ 

1. __Local database__ ทำหน้าที่เก็บเนื้อหาเริ่มต้นและการเปลี่ยนแปลงเนื้อหาของไฟล์ ซึ่งใน database จะเก็บเฉพาะส่วนที่มีการเปลี่ยนแปลงนับจากการบันทึกไฟล์ครั้งก่อนหน้า ซึ่งอาจจะเป็นการเพิ่มหรือลบเนื้อหาก็ได้ ดังนั้นถ้าจะดูว่าเนื้อหาจริงๆ ของไฟล์นั้นๆ คืออะไร ก็ต้องติดตามการเปลี่ยนแปลงทีละขั้นจนถึงจุดที่เรียกดูข้อมูลในไฟล์นั้น ๆ 
 
 ตัวอย่าง เช่น ไฟล์ source code ไฟล์หนึ่งมีการแก้ไขทั้งหมด 10 ครั้ง ถ้าต้องการดูเนื้อหาที่เกิดจากการแก้ไขครั้งที่ 7 ก็ต้องนำเนื้อหาตั้งแต่เริ่มต้น (initial) นำมาปรับปรุงตามการแก้ไขแต่ละครั้ง (เพิ่มหรือลบเนื้อหา ตามที่เก็บไว้ใน database) จนถึงครั้งที่ 7 ก็จะได้เนื้อหาของการแก้ครั้งที่ 7 ออกมา 

 2. __Staging area__ เป็นพื้นที่เก็บเนื้อหาที่จะนำไปบันทึกใน local database เนื้อหาในส่วนนี้จะไม่มีความเป็นไฟล์ของ source code จะมีเพียงแค่การรุบะความแตกต่างระหว่างรุ่นของไฟล์ต่างๆ เท่านั้น เช่นมีการแก้ไขบรรทัดเท่าใด แก้ไขเนื้อหาจากอะไรเป็นอะไร เป็นต้น

#### ภายในโฟลเดอร์ทำงาน  ####

ในโฟลเดอร์ที่มีโฟลเดอร์ .git ตั้งออยู่ จะเป็นพื้นที่ทำงาน (Working Area) ซึ่งใช้เป็นที่เก็บ source code หรือเอกสารที่ต้องการให้ git ติดตามการเปลี่ยนแปลง 
ไฟล์ทั้งหมดที่ถูกสั่งให้มีการติดตามโดย git จะถูกนำไปเปรียบเทียบกับไฟล์ที่อยู่ใน database ในทันทีที่ได้รับการบันทึกลงใน harddisk ผลต่างที่ได้สามารถส่งไปยังพื้นที่ staging area ได้ 

อย่างไรก็ตาม เราสามารถเลือกได้ว่าจะให้ git ติดตามการเปลี่ยนแปลงของไฟล์หรือไม่ (ติดตามได้ทั้งระดับ folder หรือตามชื่อและชนิดของไฟล์) โดยสามารถกำหนด spec ของโฟลเดอร์หรือไฟล์ไว้ในเอกสารที่ชื่อว่า .gitignore หรือ .gitinclude


### ฝั่ง Server ###



![image](./Pictures/gi-intro/Slide3.PNG)

รูปที่ 2

![image](./Pictures/gi-intro/Slide4.PNG)

รูปที่ 3

![image](./Pictures/gi-intro/Slide5.PNG)

รูปที่ 4

![image](./Pictures/gi-intro/Slide6.PNG)

รูปที่ 5
 
