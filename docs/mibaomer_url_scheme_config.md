蜜宝商户端Url Scheme配置

![images](/docs/images/url_scheme_start_type.png)

-------
###### 0.用途
```text
1.【如果有安装APP】通过扫描直接打开;
2.H5内部通过指定协议换起相应App相应页面;
```
###### 1.启动app
```text
mibaomer://tenancy

//java代码换启方式
Uri uri=Uri.parse("mibaomer://tenancy");  
Intent intent=new Intent(Intent.ACTION_VIEW,uri);  
startActivity(intent);
```
###### 4.剪贴板方式启动
```text
æ 口令(一般上线前预设)
 文本描述 [口令号]
 1.弹窗领取红包;
 2.打开特定的活动页;

æ 带协议的url地址(暂定,后期预留)
 http://m.mibaostore.com?p=[协议]
```
###### 5.打开蜜宝商户App内部H5页面
```text
æ 分享的连接地址换起(预留，可能会被第三方拦截,但以浏览器打开可以换起;)
 http://xxxxx?p=[mibaomer://tenancy/协议(需要加密处理)]
 //此方式需要h5在初始化时对协议做跳转处理;
æ H5页面里面的换起
 mibaomer://tenancy/[url:http://xxxxxx]
```