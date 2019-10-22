# 说明  
此实验我的博客地址：https://blog.csdn.net/qq_42767647/article/details/102651930  
  
## 实验说明  
### 实验材料与环境  
硬件：Arduino、TM1637数码管  
软件：Mixly IDE  
### 软硬件连接  
TM1637数码管正面：  
![TM1637数码管](https://img-blog.csdnimg.cn/20191022104343847.jpg)  
TM1637数码管反面与接口接法：  
数据接口是DIGITAL  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022110846903.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)  

### 【实验一】实现滚动显示自定义字符串。  
#### 1.图形化编程块
在显示框里可输入任意字符串，观察数码管输出编号，当字符串多于4位，则会滚动显示。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019102211160991.png)  
#### 2.代码块

```
#include <SevenSegmentTM1637.h>

SevenSegmentTM1637  display(5,4);

void setup(){
   display.begin();
}

void loop(){
  display.print("152zfsbjkre,ee");  //print里就是输出的字符串

}
```

#### 3.效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022120012886.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)  
### 【实验二】实现显示自定义时间。  
#### 1.图形化编程块  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022121234888.PNG)    
延时1000毫秒既是1秒，表示闪烁频率，时钟点高即是亮起来。  
#### 2.代码块

```
#include <SevenSegmentExtended.h>
#include <SevenSegmentTM1637.h>

SevenSegmentExtended  display(5,4);

void setup(){
   display.begin();
}

void loop(){
  delay(1000);
  display.printTime(12,30,HIGH);

}
```

#### 3.效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022121604862.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)  
### 【实验三】实现显示秒表。  

#### 1.图形化编程块   
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022122134252.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)   
#### 2.代码块

```
#include <SevenSegmentExtended.h>
#include <SevenSegmentTM1637.h>

SevenSegmentExtended  display(5,4);
volatile int min2;
volatile int sec;

void setup(){
  min2 = 0;
  sec = 0;
   display.begin();
}

void loop(){
  delay(1000);
  display.printTime(min2,sec,HIGH);
  sec = sec + 1;
  if (sec == 60) { 		 //当到60秒时，分钟加1
    min2 = min2 + 1;
    sec = 0;

  }
  if (min2 == 60) {    	//我这设了最多纪录到60分钟，所以到了60min归0
    min2 = 0;
    sec = 0;

  }

}
```
  
#### 3.效果图  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022122531236.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
