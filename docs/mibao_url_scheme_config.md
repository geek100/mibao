蜜宝Url Scheme配置

![images](/docs/images/url_scheme_start_type.png)

-------
###### 0.用途
```text
1.【如果有安装APP】通过扫描直接打开;
2.H5内部通过指定协议换起相应App相应页面;
```
###### 1.启动app
```text
mibaostore://tenancy

//java代码换启方式
Uri uri=Uri.parse("mibaostore://tenancy");  
Intent intent=new Intent(Intent.ACTION_VIEW,uri);  
startActivity(intent);
```
###### 2.商品
```text
æ 聚合页
 [category]:可选，空为商品聚合页;非空为具体某一分类下的商品聚合页
 mibaostore://tenancy/pd/[category]
æ 详情(其中最后为参数)
 mibaostore://tenancy/pd/detail/[?id=&....]
```
###### 3.商户
```text
æ 主页(其中最后为商户主页参数)
 mibaostore://tenancy/mer/home/[?...&...]
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
###### 5.打开蜜宝App内部H5页面
```text
æ 分享的连接地址换起(预留，可能会被第三方拦截,但以浏览器打开可以换起;)
 http://xxxxx?p=[mibaostore://tenancy/协议(需要加密处理)]
 //此方式需要h5在初始化时对协议做跳转处理;
æ H5页面里面的换起
 mibaostore://tenancy/[url:http://xxxxxx]
```

### Scheme与类名对应关系
| Number | Describsion     | SchemeType | Scheme Path                        | Android Activity Name           | IOS Controller Name                         |
|:------:|-----------------|------------|------------------------------------|---------------------------------|---------------------------------------------|
|  10000 | 启动应用        | 0          | mibaostore://tenancy/[tab/[0~3]]   | Main                            | DB_HomePageTopScrollController              |
|  10002 | 商品列表        | 1          | mibaostore://tenancy/pd/           | Main                            | DB_HomePageTopScrollController              |
|  10003 | 商品详情页      | 2          | mibaostore://tenancy/pd/detail/    | SelfSupportGoodsDetailsActivity | DBProject.DB_GoodsDetailController          |
|  10004 | 商户首页        | 3          | mibaostore://tenancy/mer/home/     | ShopActivity                    | DBProject.DB_HomePageShopHomePageController |
|  10005 | App内部的H5页面 | -1         | mibaostore://tenancy/h5/?url=[...] | H5WebViewActivity               | DBProject.DB_CommonWebViewController        |
| 10006  | 优惠券页面      | 4          | mibaostore://tenancy/coupons/list/ | MineGiftCertificatesActivity    | DB_MineCouponViewController                 |

### 页面参数
| Number | Scheme Params | Android Params | IOS Params | Describsion                                       |
|:------:|---------------|----------------|------------|---------------------------------------------------|
|  10003 | gid           | GOODS_ID       | goodsID    | 商品id                                            |
|  10004 | merId         | MERCHANT_ID    | merchantId | 商户id                                            |
|  10005 | url           | [url] [type-]  | webUrl     | url地址                                           |
|        | type          | type           | type       | 0:url,1:html代码,2:api,一般指有额外的接口需要请求 |

### 人脸验证成功回调Scheme Url
| Scheme URL                                         | Describsion                                 |
|----------------------------------------------------|---------------------------------------------|
| mibaostore://tenancy/subscribe/success[/?回调参数] | 预约成功回调页面;具体参数跟在scheme url后面 |