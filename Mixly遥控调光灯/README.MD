# 说明  
.mix文件是源代码文件，需米思齐软件打开
## 题目  
按遥控器上的CH键实现LED的开关。开了LED的情况下可以通过CH+和CH-键实现控制LED的光亮变化。LED关闭状态CH+和CH-无效。  
  
# 实验材料与文件
硬件：Arduino、红外遥控传感器、遥控器
软件：Mixly IDE

# 【实验】遥控灯实验步骤
## 1.软硬件连接
--号连接GND
S是连数据接口
中间则连5V
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022164154790.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 2.图形化编程块
我给了灯亮度的约束值，最暗的亮度我给了5，不让它熄灭，最亮是255。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022165636968.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
## 3.代码块

```
#include <IRremote.h>

volatile int LED;
volatile boolean LED_status;
IRrecv irrecv_5(5);
decode_results results_5;

long ir_item;

void setup(){
  LED = 0;
  LED_status = 0;
  Serial.begin(9600);
  irrecv_5.enableIRIn();
}

void loop(){
  if (irrecv_5.decode(&results_5)) {
    ir_item=results_5.value;
    String type="UNKNOWN";
    String typelist[14]={"UNKNOWN", "NEC", "SONY", "RC5", "RC6", "DISH", "SHARP", "PANASONIC", "JVC", "SANYO", "MITSUBISHI", "SAMSUNG", "LG", "WHYNTER"};
    if(results_5.decode_type>=1&&results_5.decode_type<=13){
      type=typelist[results_5.decode_type];
    }
    Serial.print("IR TYPE:"+type+"  ");
    Serial.println(ir_item,HEX);
    irrecv_5.resume();
  } else {
  }
  if (ir_item == 0XFF629D) {
    LED_status = !LED_status;
    LED = LED_status * 128;

  }
  if (LED_status == 1) {
    if (ir_item == 0XFFA25D) {
      LED = constrain(LED - 5, 5, 255);			//我给了灯亮度的约束值，最暗的亮度我给了5，不让它熄灭，最亮是255。
      Serial.print("LED IS:");
      Serial.println(LED);

    }
    if (ir_item == 0XFFE21D) {
      LED = constrain(LED + 5, 5, 255);
      Serial.print("LED IS:");
      Serial.println(LED);

    }

  }
  analogWrite(9,LED);

}
```

## 4.实验成果  
实验效果视频在photo文件夹里  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022174311802.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNzY3NjQ3,size_16,color_FFFFFF,t_70)
