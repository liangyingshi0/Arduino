# 实验材料与环境
硬件：Arduino、LED灯、HC-SR501模块(人体红外感应模块)、5V声音检测传感器模块  
软件：Mixly IDE  

# 【实验】人体&声控灯
达到效果：当检测到人或声音大于某值时，灯亮起，过2秒后熄灭。灯亮起的条件只需满足其中一个条件。  
## 1.软硬件连接
人体红外感应模块：数据接D3号口；vcc接5V，GND对应GND  
灯接D9号接口  
声音检测模块：数据接A3号口；vcc接5V，GND对应GND  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029210402285.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 2.图形化编程块
人体红外：0是没人，1是检测到人。  
声音探测我这里设为超过65就亮起。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029210509337.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 3.代码块

```
volatile boolean people;
volatile int voice;

void setup(){
  people = 0;
  voice = 0;
  pinMode(3, INPUT);
  pinMode(9, OUTPUT);
  Serial.begin(9600);
}

void loop(){
  people = digitalRead(3);
  voice = analogRead(A3);
  if (people == 1 || voice > 65) {
    digitalWrite(9,HIGH);
    delay(2000);

  } else {
    digitalWrite(9,LOW);

  }
  Serial.print("声音：");
  Serial.println(voice);
  Serial.print("人体检测：");
  Serial.println(people);

}
```

## 4.效果
实验效果已上传到[B站](https://www.bilibili.com/video/av73833803/)：欢迎指导与提问：[https://www.bilibili.com/video/av73833803/](https://www.bilibili.com/video/av73833803/)
