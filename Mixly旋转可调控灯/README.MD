# 实验材料与环境
硬件：Arduino、LED灯、按键、电位器、LCD1602液晶显示器、面包板、I2C转接板  
软件：Mixly IDE  

# 【实验】旋转可调灯
达到效果：通过按键把灯打开，通过旋转电位器来实现调控灯的亮度，液晶屏显示灯的亮度值。灯没打开时，电位器旋转不起效果。  
## 1.软硬件连接
电位器的接法：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191101184720909.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
我的接法是：  
电位器：接地的接GND，输出接A0，输入接5V  （电位器的范围是：0-1023）  
转接板：GND对GND，vcc接5v，scl接A1，sda接A2  
灯：9号  
按键：6号  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191101184704476.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 2.图形化编程块
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191101181516248.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 3.代码块

```
#include <LiquidCrystal_SoftI2C.h>
#include <SoftI2CMaster.h>

volatile int LED;
LiquidCrystal_SoftI2C mylcd(0x27,16,2,A1,A2);
volatile boolean flag;

void setup(){
  mylcd.init();
  mylcd.backlight();
  pinMode(6, INPUT);
  Serial.begin(9600);
  flag = 0;
  LED = 0;
  pinMode(6, INPUT_PULLUP);
}

void loop(){
  if (digitalRead(6) == LOW) {
    delay(20);
    if (digitalRead(6) == LOW) {
      flag = !flag;

    }

  }
  if (flag == 1) {
    Serial.println(analogRead(A0));
    analogWrite(9,(map(analogRead(A0), 1, 1023, 1, 255)));
    LED = (map(analogRead(A0), 0, 1023, 0, 255));

  } else {
    analogWrite(9,0);
    LED = 0;

  }
  mylcd.setCursor(0, 0);
  mylcd.print("2017764325 LED:");
  mylcd.setCursor(0, 1);
  mylcd.print(LED);

}
```

## 4.效果
[B站](https://www.bilibili.com/video/av74153823/)：[https://www.bilibili.com/video/av74153823/](https://www.bilibili.com/video/av74153823/)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191101185252789.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
