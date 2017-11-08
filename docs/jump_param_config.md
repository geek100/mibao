APP跳转参数说明
----------
| 字段        | 类型    |  描述 |  示例(IOS\Android根据需要自行定义)  |
|   ----     | -----   | :----: |
| 香蕉        | $1      |   5    |
| 苹果        | $1      |   6    |
| 草莓        | $1      |       |


```java
{
  "configs": [
    {
      "deviceType": 1: android;2: ios;,
      "pageName": "CreditDetail",
      "createType": "0.直接初始化, 1.加载XIB",
      "changeType": "0.push新页面, 1.模态新页面",
      "version": [
        36,
        37,
        38,
        39
      ],
      "params": {
        "id": 1000
      }
    },
    {
      "deviceType": 2,
      "pageName": "BigVSayDetail",
      "version": [
        40
      ],
      "params": {
        "id": 1000
      }
    }
  ]
}
```