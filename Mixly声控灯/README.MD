# 实验材料与环境
硬件：Arduino、LED灯、5V声音检测传感器模块  
软件：Mixly IDE  

# 【实验】声音检测控制灯
要求：当检测到声音大于某个值时，灯亮。  
## 1.软硬件连接
我这里是：  
灯接D9号接口  
声音检测模块：数据接A3号口；vcc接5V，GND对应GND  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029204253567.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 2.图形化编程块
声音探测我这里设为超过65就亮起。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029205106334.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 3.代码块

```
volatile int voice;

void setup(){
  voice = 0;
  pinMode(9, OUTPUT);
  Serial.begin(9600);
}

void loop(){
  voice = analogRead(A3);
  if (voice > 65) {
    digitalWrite(9,HIGH);
    delay(3000);

  } else {
    digitalWrite(9,LOW);

  }
  Serial.println(voice);

}
```

## 4.效果
实验效果已上传到[B站](https://www.bilibili.com/video/av73832721/)，欢迎各位指导与提问：[https://www.bilibili.com/video/av73832721/](https://www.bilibili.com/video/av73832721/)
