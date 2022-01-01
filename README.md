# AT90CAN128_cal_CAN

- 환경



   - Atmel studio 7
   - (로보블럭)AT90CAN128 트레이닝키트
   - kvaser canking driver
   - Kvaser 00685-0 Can Module, Usb, Leaf Light V2, 1Ch & RS232 cable




      <img width="30%" src="https://user-images.githubusercontent.com/87747013/147848861-174bead8-8e0f-4b45-8b99-7bd87eec3b01.jpg"/>  

---
1. 4X4 keypad를 이용하여 계산기 만들기


   PORTB, PORTD는 7-segment(debug)에 연결, PORTE는 4x4 keypad에 연결한다.



- lcd결선



  <img width="20%" src="https://user-images.githubusercontent.com/87747013/147848592-5c6240a0-44e4-4cb6-9161-7358a19a1366.png"/>  





- lcd_회로도
<img width="30%" src="https://user-images.githubusercontent.com/87747013/147848587-ea492573-05a0-4548-ac22-ef2caa60c2f7.png"/>  
- 4x4_keypad
<img width="30%" src="https://user-images.githubusercontent.com/87747013/147848587-ea492573-05a0-4548-ac22-ef2caa60c2f7.png"/>  
- timing chart
 <img width="30%" src="https://user-images.githubusercontent.com/87747013/147848596-0a2ea308-e14c-45ee-879e-3b7fb74e0854.png"/>  
- initialization
<img width="30%" src="https://user-images.githubusercontent.com/87747013/147848590-340057d5-0f1c-4670-a669-c86d290e55b5.png "/>  


설계조건:
* operator: +, -, x
* 입력되는 숫자와 연산기호, 해답은 LCD에 출력
* 한 항에 입력되는 숫자의 크기는 세자리 수 이하

<소스코드>

```c++
#include <iostream>
using namespace std;
int main(){
  cout<<"hello world!"<endl;
  retrun 0;
}
```

---
2. CAN 통신 실습
   MCU의 CAN pheriphral측에서 PORTD.5는 TXCAN, PORTD.6는 RXCAN이다.
   
   
   
   이는 transcevier에 연결되며(연결할 필요x),
   CAN_H, CAN_L는 can_to_usb케이블(kvaser+RS232)에 연결한다.
   PORTE는 LED에 연결한다.

- can 통신부
- <img width="30%" src="https://user-images.githubusercontent.com/87747013/147848589-9aec4e69-1b61-46df-b4f6-c44e1220b8bf.png"/>  

- led_part_1
<img width="30%" src="https://user-images.githubusercontent.com/87747013/147848593-d17d503e-da7a-47de-9500-f50947d359af.png"/>  

- led_part_2
<img width="30%" src="https://user-images.githubusercontent.com/87747013/147848595-1b3a0638-7ef6-4cb8-9b4c-0a5af7211fbb.png"/>  


1. PC에서 전송되는 0x100, 0x200, 0x300, 0x400, 0x500, 0x600, 0x700, 0x800,0x150, 0x250의 10개 CAN Frame Data를 수신하고, 
LED에 수신될 때마다 Toggle 할 것 (D9-0x100, D10-0x200, … D16-0x800, D23-0x150, D24-0x250)
<소스코드>
```c++
#include <iostream>
using namespace std;
int main(){
  cout<<"hello world!"<endl;
  retrun 0;
}
```
2. AT90CAN128 보드에서 3개의 Tx Data 송출할 것
Tx Data: 0x110(10msec), 0x210(50msec), 0x310(100msec)
<소스코드>
```c++
#include <iostream>
using namespace std;
int main(){
  cout<<"hello world!"<endl;
  retrun 0;
}
```


AT90CAN128의 CAN통신부의 feature
---
- 15 Mob(message object)를 담을 수 있는 data buffer(MOb는 CAN 프레임 기술자이다. 메일박스에 송수신되는 메시지의 동작모드 결정.).
- id tag, id mask는 11bit(rev 2.0A) or 29bit(rev 2.0B)
- data buffer는 8byte 




