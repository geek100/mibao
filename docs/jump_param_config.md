APP跳转参数说明
----------
| 字段         | 类型      | 描述                                 | 示例(IOS\Android根据需要自行定义)    |
| ------------ |:--------:| :----------------------------------:| :-------------------------------- |
| deviceType   | int      | 设备类型(1:ios;2:android;)            | ios                              |
| pageName     | string   | $页面名称(跳转开发时由产品定)            | CreditDetail                     |
| version      | int      | 版本                                 | Android用versionCode;IOS用build   |
| params       | array    | 数组类型(具体参数数量和值每个版本可自定义) | [{"key","value"},...]            |
| createType   | int      | 0.直接初始化, 1.加载XIB                | 1                                |
| changeType   | int      | 0.push新页面, 1.模态新页面             | 0                                |
| enabled      | boolean  | true:配置可用，false:配置不可用;        | true                             |
| uniqueTag    | string   | 配置唯一标识码                         | guid                             |
| description  | string   | 资源位描述                            | 什么页面，比如说banner页面           |

```java
{
  "uniqueTag": "5bdd9be78eb14e2e9801b45121fad298",
  "description": "资源位描述",
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
      "params": [
        "id": 1000
      ],
      "enabled": true
    }
  ]
}
```