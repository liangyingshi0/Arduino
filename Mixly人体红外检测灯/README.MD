# 实验材料与环境
硬件：Arduino、LED灯、HC-SR501模块(人体红外感应模块)  
软件：Mixly IDE

# 【实验】人体红外检测灯
要求：当有人经过时，灯亮，经过后，灯熄灭。  
## 1.软硬件连接
我这里是：  
人体红外感应模块：数据接D3号口；vcc接5V，GND对应GND  
灯接D9号接口  
![在这里插入图片描述](https://raw.githubusercontent.com/liangyingshi0/Arduino/master/Mixly%E4%BA%BA%E4%BD%93%E7%BA%A2%E5%A4%96%E6%A3%80%E6%B5%8B%E7%81%AF/photo/%E4%BA%BA%E4%BD%93.jpg)
## 2.图形化编程块
人体红外：0是没人，1是检测到人。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029194332816.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 3.代码块

```
volatile boolean people;

void setup(){
  people = 0;
  pinMode(3, INPUT);
  pinMode(9, OUTPUT);
  Serial.begin(9600);
}

void loop(){
  people = digitalRead(3);
  if (people == 1) {
    digitalWrite(9,HIGH);

  } else {
    digitalWrite(9,LOW);

  }
  Serial.println(people);

}
```

## 4.效果
实验效果视频已上传到[B站](https://www.bilibili.com/video/av73832082/)：[https://www.bilibili.com/video/av73832082/](https://www.bilibili.com/video/av73832082/)
欢迎各位查看与指导。
