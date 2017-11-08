跳转配置源数据格式
-----
APP点击转向具体的页面之前需要给出以下数据格式以满足我们跳转
###### 1.APP端以资源位图形式展示(H5、详情页、列表页)
```json
[
  {
    "dataId": 29,//数据id或分类id
    "imgUrl": "default/20171102/2785c16044e24c80aac1b568cc430bdd.png",//展示图片
    "isH5":false,//是否h5,
    "url":"",
    "uniqueTag": "5bdd9be78eb14e2e9801b45121fad298"//oss中对应的文件唯一标识
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