跳转配置源数据格式
-----
APP点击转向具体的页面之前需要给出以下数据格式以满足我们跳转
###### 1.配置参数说明
| 字段             | 类型      | 描述                                          |
| ------------    |:--------:| :-------------------------------------------: |
| dataId          | int      | 数据id或分类id                                  |
| imgUrl          | string   | 图片地址                                        |
| isH5            | boolean  | true:h5;false:原生;                            |
| url             | string   | 若是h5,则该url为要跳转的目标地址                   |
| goConfigVersion | int      | 0:客户端配置；1:服务端配置与数据一起返回【后期使用】   |
| configs         | object   | 配置列表项(具体参数APP跳转参数说明)【后期使用】       |

###### 2.APP端以资源位图形式展示(H5、详情页、列表页)
```json
[
  {
    "dataId": 29,
    "imgUrl": "default/20171102/2785c16044e24c80aac1b568cc430bdd.png",//展示图片
    "isH5":false,//是否h5,
    "url":"",
    "uniqueTag": "5bdd9be78eb14e2e9801b45121fad298",//oss中对应的文件唯一标识
    "goConfigVersion":0,
    "configs":[]
  },
  {
    "dataId": 2,//数据id或分类id
    "imgUrl": "default/20171102/2785c16044e24c80aac1b568cc430bdd.png",//展示图片
    "isH5":true,//是否h5,
    "url":"www.baidu.com"
    "uniqueTag": "5bdd9be78eb14e2e9801b45121fad298"//oss中对应的文件唯一标识
  }
  ....
]
```