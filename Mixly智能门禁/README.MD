# 【实验一】读取校园卡ID 号
# 实验材料与环境
硬件：Arduino、RC522读卡器、校园卡   
软件：Mixly IDE 
## 1.软硬件连接
此次实验我接的口为：  
SDA：10号  
SCK：13号  
MOSI：11号  
MISO：12号  
GND对应GND，3.3v对应3.3v  
## 2.图形化编程块
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191027152412922.PNG)
## 3.代码块

```
#include <RFID.h>
#include <SPI.h>

RFID rfid(10,5);
unsigned char RC_size;
unsigned char blockAddr;        //选择操作的块地址0～63
unsigned char i,tmp;
unsigned char status;
unsigned char str[MAX_LEN];

String RFID_readcardnum() {

 rfid.readCardSerial();
  String stringserNum=String(rfid.serNum[0], HEX)+String(rfid.serNum[1], HEX)+String(rfid.serNum[2], HEX)+String(rfid.serNum[3], HEX)+String(rfid.serNum[4], HEX);
      //选卡，返回卡容量（锁定卡片，防止多次读写）
      rfid.selectTag(rfid.serNum);
  return stringserNum;
}

//4字节卡序列号，第5字节为校验字节
//新扇区A密码，16个扇区，每个扇区密码6Byte
unsigned char sectorNewKeyA[16][16] = {
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xff,0x07,0x80,0x69, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xff,0x07,0x80,0x69, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},};
unsigned char serNum[5];
//写卡数据
//原扇区A密码，16个扇区，每个扇区密码6Byte
unsigned char sectorKeyA[16][16] = {
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},};

void setup(){
  Serial.begin(9600);
  SPI.begin();
  rfid.init();
  Serial.begin(9600);
}

void loop(){
  if ( rfid.isCard()  ) {
    Serial.println(RFID_readcardnum());
  }

}
```

## 4.实验成果
出现的字符串则为卡的编号，每张卡的编号是唯一的。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191027152609272.png)
# 【实验二】读取到指定校园卡使用S90舵机开门，并延时3秒后自动关闭
# 实验材料与环境
硬件：Arduino、RC522读 卡器、S90舵机、校园卡   
软件：Mixly IDE 
## 1.软硬件连接
RFID的接口与实验1相同，舵机的接法为：红正褐负橙数据。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019102715282574.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 2.图形化编程块
将上一实验中读出的卡编号输入到字符串中。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191027153031353.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 3.代码块

```
#include <RFID.h>
#include <SPI.h>
#include <Servo.h>

String RC;
RFID rfid(10,5);
unsigned char RC_size;
unsigned char blockAddr;        //选择操作的块地址0～63
unsigned char i,tmp;
unsigned char status;
unsigned char str[MAX_LEN];
Servo servo_5;
char * card[]={"b09ae4a6e","804fb4a8e"};

String RFID_readcardnum() {

 rfid.readCardSerial();
  String stringserNum=String(rfid.serNum[0], HEX)+String(rfid.serNum[1], HEX)+String(rfid.serNum[2], HEX)+String(rfid.serNum[3], HEX)+String(rfid.serNum[4], HEX);
      //选卡，返回卡容量（锁定卡片，防止多次读写）
      rfid.selectTag(rfid.serNum);
  return stringserNum;
}

//4字节卡序列号，第5字节为校验字节
//新扇区A密码，16个扇区，每个扇区密码6Byte
unsigned char sectorNewKeyA[16][16] = {
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xff,0x07,0x80,0x69, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xff,0x07,0x80,0x69, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},};
unsigned char serNum[5];
//写卡数据
//原扇区A密码，16个扇区，每个扇区密码6Byte
unsigned char sectorKeyA[16][16] = {
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},
 {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF},};

void setup(){
  RC = "";
  Serial.begin(9600);
  SPI.begin();
  rfid.init();
  Serial.begin(9600);
  servo_5.attach(5);
}

void loop(){
  if ( rfid.isCard()  ) {
    RC = RFID_readcardnum();
    Serial.println(RC);
    for (int i = (1); i <= (sizeof(card)/sizeof(card[0])); i = i + (1)) {
      if (RC == card[(int)(i - 1)]) {
        servo_5.write(90);
        delay(3000);
        servo_5.write(0);
        delay(0);

      }
    }
  }

}
```

## 4.实验成果
[B站](https://www.bilibili.com/video/av73507767/)：https://www.bilibili.com/video/av73507767/  
(https://raw.githubusercontent.com/liangyingshi0/Arduino/master/Mixly%E6%99%BA%E8%83%BD%E9%97%A8%E7%A6%81/Photo/%E6%95%88%E6%9E%9C.gif)
