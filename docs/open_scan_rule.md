对外二维码规则定义与获取规范
----
```text
对外二维码一般有以下几个特点

1.一但生成后即不可随意更改;
2.二维码所提供的信息要根据时段活动规则得有相应的变化;
3.同时要符合各个段兼容;
```

###### 1.二维码内容
```text
https://m.mibaostore.com/merchant/#/index?stype=1&appId=4567834567&merId=236

参数:
1.stype:1-商户;
2.merId:商户id,后面加解密时需要;

--对于内容我们采用以下加解密方式:
  1.平面字符对称加解密;
  2.merId作为散列key处理;
```

###### 2.规则获取
```text
1.根据stype和merId获取相应的规则;
2.规则结构如下:
{
  //规则参数
  "ruleParames": {
    "scanType": "扫码类型",
    "showType": "逻辑处理过程中显示的类型,一般指page或alert",
    "schemePath": "scheme路径,用于获取规则(例):/mer/home/",
    "appId": "45609875679(客户端appId,用于验证此次活动是否符合的客户端来扫码)",
    "minVersion": 34//app最小版本,用于验证当前应用是否符合版本要求
  },
  "periodRule": {
    //规则内容,具体的规则内部传输
  }
}
```