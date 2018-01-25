文章发布协议
----
###### 1.使用方式及场景描述
场景:
```text
1.文本；
2.图片；
3.图文；
4.图文中带有链接；
```
接入:
```text
0.添加段落(事件)
1.文本(操作)——首行缩进、文本颜色、文本大小、是否加粗、对齐[左、中、右]
2.图片\文本\链接[单张](操作)——
  a).如果段落开始为文本，则需要要首行缩进功能;否则不需要有首行缩进;
  b).文本颜色、文本大小、是否加粗、对齐[左、中、右];
  c).图片组功能:[s-img][e-img]
  d).链接——选择文本后单击插入链接，显示输入链接地址对话框
```
###### 2.段落数据结构
--json
```json
[{
  "subject": "文章内容",
  "type": 0,
  "position": 0,
  "style": {
    "textColor": "#323232",
    "textSize": 12,
    "lineSpacingMultiplier": 1.5,
    "firstLineIndentation": 0,
    "isBlod": 0,
    "alignType": 0,
    "paragraphSpace": 16
  }
}]
```

| 字段                  | 描述                                         |
|-----------------------|----------------------------------------------|
| subject               | 文章内容                                     |
| type                  | 1-文本;2-图片;                               |
| position              | 索引(add-后台返回当前文章内容段落的最大索引) |
| textColor             | 文本颜色                                     |
| textSize              | 文本大小                                     |
| lineSpacingMultiplier | 默认1.5倍行距                                |
| firstLineIndentation  | 首行是否缩进（0：不缩进；1缩进;）            |
| isBlod                | 是否加粗糙                                   |
| alignType             | 对齐方式(0:左对齐;1:右对齐;)                 |
| paragraphSpace        | 对齐方式(0:左对齐;1:右对齐;)                 |