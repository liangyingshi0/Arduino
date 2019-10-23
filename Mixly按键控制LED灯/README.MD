# 说明  
# 实验材料与环境
硬件：Arduino、LED
软件：Mixly IDE
# 【实验】实现按键控制LED灯
## 1.软硬件连接  
根据需求，把按键与灯接入相关接口。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191023173319789.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191023173340192.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 2.图形化编程块
数字管脚输入低的意思是等不亮。  
延时20毫秒是为了去抖动，里面的条件嵌套是为了检测松手操作，若按下按键未松手，则灯的状态不变。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191023173517596.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 3.代码块
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191023173841530.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 4.实验成果  
[B站](https://www.bilibili.com/video/av73150844/)：https://www.bilibili.com/video/av73150844/  
