APP跳转参数说明
----------
| 字段        | 类型    |  描述 |  示例(IOS\Android根据需要自行定义)  |

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

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