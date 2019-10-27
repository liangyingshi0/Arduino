# 说明
# 实验材料与环境
硬件：Arduino、LED灯、按钮  
软件：Mixly IDE  
# 软硬件连接
两个实验的接法相同，我的接法是：  
灯：9号（因为灯的亮度需变化，所以选择接：3，5，6，9接口）  
按钮：8号  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191027170310289.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
# 【实验一】呼吸灯  
## 1.图形化编程块  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191027173904482.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 2.代码块  

```
volatile boolean status;

void FadeOff(int time) {
  for (int i = 255; i >= 0; i = i + (-5)) {
    if (digitalRead(8) == LOW) {
      delay(200);
      if (digitalRead(8) == LOW) {
        status = !status;
        while (digitalRead(8) == LOW) {
        }

      }
      if (status == 0) {
        return;
      }

    }
    analogWrite(9,i);
    delay((time / (255 / 5)));
  }
}

void FadeOn(int time) {
  for (int i = 0; i <= 255; i = i + (5)) {
    if (digitalRead(8) == LOW) {
      delay(200);
      if (digitalRead(8) == LOW) {
        status = !status;
        while (digitalRead(8) == LOW) {
        }

      }
      if (status == 0) {
        return;
      }

    }
    analogWrite(9,i);
    delay((time / (255 / 5)));
  }
}

void setup(){
  status = 0;
  pinMode(8, INPUT_PULLUP);
  pinMode(9, OUTPUT);
  Serial.begin(9600);
}

void loop(){
  if (digitalRead(8) == LOW) {
    delay(200);
    if (digitalRead(8) == LOW) {
      status = !status;
      while (digitalRead(8) == LOW) {
      }

    }

  }
  if (status == 1) {
    FadeOn(2000);
    FadeOff(2000);

  } else {
    digitalWrite(9,LOW);

  }
  Serial.print(digitalRead(8));
  Serial.println(status);

}
```

## 3.实验成果
实验视频我放在了B站上：（是高清的）  
[B站](https://www.bilibili.com/video/av73622143/)：[https://www.bilibili.com/video/av73622143/](https://www.bilibili.com/video/av73622143/)

# 【实验二】可调档位灯
## 1.图形化编程块
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191027174237447.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 2.代码块

```
volatile int bright;
volatile int click;

void setup(){
  pinMode(8, INPUT);
  Serial.begin(9600);
  click = 0;
  bright = 0;
  pinMode(8, INPUT_PULLUP);
}

void loop(){
  if (digitalRead(8) == LOW) {
    delay(200);
    if (digitalRead(8) == LOW) {
      click = click + 1;
      if (click == 6) {
        click = 0;

      }
      while (digitalRead(8) == LOW) {
      }

    }

  }
  analogWrite(9,(click * 51));
  Serial.println(click);

}
```

## 3.实验成果
实验视频我放在了B站上：（由于拍摄手法不好，此视频不是高清）  
[B站](https://www.bilibili.com/video/av73518373/)：[https://www.bilibili.com/video/av73518373/](https://www.bilibili.com/video/av73518373/)
