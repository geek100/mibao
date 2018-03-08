商户二维码生成规则
----
###### 1.二维码格式
```java
{
  "sc":"https://m.mibaostore.com/merchant/#/index?stype=1&merId=更新商户id",
  "sk":"加密串生成的key",
  "st":"1"
}

参数(sc)分析:
  1.主要由https://m.mibaostore.com/merchant/#/index 和 stype=1&merId=更新商户id 两部分组成;
  2.下面用sk所说的加密主要对 stype=1&merId=更新商户id 进行加密处理;
```

###### 2.加密key生成过程(sk)
```text
根据参考值第一位和最后一位ASCII码值相加的结果(R1)插入参考值中,R1长度与参考值取余的位置;

示例:
   1.如果merId=61,那么第一位ASCII值为54  最后一位的ASCII值为49;
   2.根据定义第一位ASCII值+最后一位ASCII值=103,我们简称为AT;
   3.根据1和2得到余数，即要插入的索引处;yu=AT.lenght()%merId.lenght();
   4.结果=merId前部分+AT+merId后部分;

具体key生成方法及加解密内部传输
```

###### 3.最后二维码内容(形式)——实际使用时需要换成真实数据
```java
{
  "sc":"https://m.mibaostore.com/merchant/#/index?需要替换成密文",
  "sk":"加密串生成的key",
  "st":"1"
}
```

*注：在生成二维码之前将所有的空格去掉,提高识别速度;*