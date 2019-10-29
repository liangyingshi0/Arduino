# 实验材料与环境
硬件：Arduino、LED灯、人体红外检测器、光敏传感器、5V声音检测传感器模块  
软件：Mixly IDE  

# 【实验】模拟楼道灯
达到效果：当检测到白天时，任何时候不亮灯；当检测到暗度很黑，模拟夜晚情况时，检测到有人或声音大于某值时，灯亮起，过2秒后熄灭。在夜晚情况下，灯亮起的条件只需满足其中一个条件。
## 1.软硬件连接
人体红外感应模块：数据接D3号口；vcc接5V，GND对应GND  
灯接D9号接口  
声音检测模块：数据接A3号口；vcc接5V，GND对应GND  
光敏传感器：数据接A5接口，+接5V，-对应GND  
![在这里插入图片描述](https://raw.githubusercontent.com/liangyingshi0/Arduino/master/Mixly%E6%A8%A1%E6%8B%9F%E6%A5%BC%E9%81%93%E7%81%AF%EF%BC%8C%E5%A3%B0%E9%9F%B3%2B%E4%BA%BA%E4%BD%93%E7%BA%A2%E5%A4%96%E6%A3%80%E6%B5%8B%2B%E4%BA%AE%E5%BA%A6%E6%A3%80%E6%B5%8B/photo/%E4%BA%BA%E4%BD%93%2B%E5%A3%B0%E9%9F%B3%2B%E4%BA%AE%E5%BA%A6.jpg)
## 2.图形化编程块
人体红外：0是没人，1是检测到人。  
声音探测我这里设为超过65就亮起。  
我用手握住模拟黑暗状态的数据大约是600，所以我这里设为，当大于600时是黑夜环境，只需满足其中一个条件就能亮灯。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029212041936.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 3.代码块

```
volatile int bright;
volatile boolean people;
volatile int voice;

void setup(){
  pinMode(3, INPUT);
  pinMode(9, OUTPUT);
  Serial.begin(9600);
  people = 0;
  voice = 0;
  bright = 0;
}

void loop(){
  bright = analogRead(A5);
  people = digitalRead(3);
  voice = analogRead(A3);
  if (bright > 600) {
    if (people == 1 || voice > 65) {
      digitalWrite(9,HIGH);
      delay(2000);

    } else {
      digitalWrite(9,LOW);

    }

  } else {
    digitalWrite(9,LOW);

  }
  Serial.print("光亮：");
  Serial.println(bright);
  Serial.print("声音：");
  Serial.println(voice);
  Serial.print("人体检测：");
  Serial.println(people);

}
```

## 4.效果
效果我已上传到[B站](https://www.bilibili.com/video/av73836598/)，欢迎指导与提问：[https://www.bilibili.com/video/av73836598/](https://www.bilibili.com/video/av73836598/)
