文本数据格式
----
###### 1.段数据格式
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
| type                  | 1-文本;2-html;                               |
| position              | 索引(add-后台返回当前文章内容段落的最大索引) |
| textColor             | 文本颜色                                     |
| textSize              | 文本大小                                     |
| lineSpacingMultiplier | 默认1.5倍行距                                |
| firstLineIndentation  | 首行是否缩进（0：不缩进；1缩进;）            |
| isBlod                | 是否加粗糙                                   |
| alignType             | 对齐方式(0:左对齐;1:右对齐;)                 |
| paragraphSpace        | 对齐方式(0:左对齐;1:右对齐;)                 |