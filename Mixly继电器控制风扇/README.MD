# 材料与环境
硬件：Arduino、按键、继电器、直流电机、风扇、1.5V电池（因为直接接在Arduino上，电压会不足）  
软件：Mixly IDE  

# 【实验名称】继电器控制小风扇
达到效果：当按下按键时，继电器工作，小风扇运作，再次按下按键后，继电器内部线路不连通，风扇停止运转。  
## 1.软硬件连接
NO口不接线  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191105174012660.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191105170638592.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 2.图形化编程块
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191105172638522.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 3.代码块

```c
volatile boolean flag;

void setup(){
  flag = 0;
  pinMode(11, INPUT_PULLUP);
  pinMode(6, OUTPUT);
}

void loop(){
  if (digitalRead(11) == LOW) {
    delay(20);
    if (digitalRead(11) == LOW) {
      flag = !flag;
      while (digitalRead(11) == LOW) {
      }

    }

  }
  if (flag == 1) {
    digitalWrite(6,HIGH);

  } else {
    digitalWrite(6,LOW);

  }

}
```

## 4.效果  
实验效果已上传至[B站](https://www.bilibili.com/video/av74642565/)：[https://www.bilibili.com/video/av74642565/](https://www.bilibili.com/video/av74642565/)
