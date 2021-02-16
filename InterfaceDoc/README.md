- ### 接口调用说明

		测试接口统一调用地址: http://api.huhuixin.com
		调用格式基本遵循restfull风格

- ### 返回值说明

		返回json格式的数据 基本格式为 {"status":200,"msg":"成功"}
		1000以内的返回码遵循Http标准状态码标准,1000以上的返回码为自定义返回码,具体解释详见返回码解释

- ### 其他

		为避免精度丢失,接口中涉及金额的处理一律使用整型数据,金额单位为分,移动端展示时需自行处理


-------


- ## 全局错误码

| 错误码  | 错误解释  |
| ------------ | ------------ |
|  200 |  成功 |
|  204 |  未获取到内容 |
|  401 |  用户认证失败 |
|  404 |  资源找不到 |
|  415 |  请求格式错误 |
|  409 |  引用了非法或已经失效的资源 |
|  412 |  缺少参数 |
|  421 |  请求频率过快 |
|  500 |  服务异常 |
|  503 |  系统繁忙 |
|  1002 |  返回列表为空 |
|  1003 |  手机号格式有误 |
|  1004 |  已截单 |
|  1005 |  库存不足 |
|  1006 |  支付超时 |
|  1007 |  地址不在配送区域内 |



-------


## 修改记录


- **2018-04-17：**

    -  食品详情新增剩余库存字段
    -  合并 地址级联信息  餐店地址列表信息  配送时间列表信息
    -  用户提交购物车时 返回订单详情（如果用户有地址则同时返回配送费用）用户地址列表等信息 并且订单状态为已创建未提交，允许用户修改地址
    -  新增用户在历史记录中支付订单接口 ， 返回订单详情 ， 订单状态为 已提交，不允许用户修改地址信息

- **2018-04-18：**

    - 接口新增食品分类列表返回值 , 分类名称 categoryName 更改为 categoryId  (列表中对应的分类id) 

- **2018-04-25：**

    - 添加资源限制通用返回值
    - 修正3.7接口描述
    - Get方式请求时不再显式的将openId展现在url上 , 受影响的接口
        - 3.7 获取订单详情 
        - 3.6历史订单发起支付
        
- **2018-04-30：**
    
    - 3.2 接口，将取餐点ID和用户地址ID合并为同一个字段
            根据deliveryType的不同传入不同类型的ID,新增openId参数
    - 为方便做统一用户认证处理，所有订单相关的接口都需要传入openId参数且不再用get方式请求
            受影响的接口  3.4   3.6   3.7
    - 3.1提交购物车返回分组订单中 新增groupNumber字段 , 3.3 接口提交收获时间接口去除时间餐点改为用分组订单编号
    
- **2018-04-30：**

    - 新增2.4 删除用户地址接口
    
- **2018-05-03：**

    - 3.1 创建订单接口添加返回值 deliveryPrice 配送费
    - 3.3 发起支付接口新增字段 remark ,订单备注
    - 全局错误码更新
    
- **2018-05-04：**

    - 3.5 获取历史订单接口添加修改返回值
    - 3.1 - 3.6 isSubmit 替换 orderStatus
    - 3.6 添加配送类型字段
        3.6接口中当用户要提交支付的历史订单 没有提交过支付信息时(submit为false),
        返回的信息与提交购物车完全相同,此时允许用户修改地址等信息,提交过信息时,将不再返回
        用户地址列表,改为返回上次用户提交提付信息时该订单绑定的配送信息,deliveryType + chooseAddress
    - 移除取消订单接口
    - 3.7 获取订单详情接口大量修改
    
- **2018-05-06:**

    - 新增模拟支付接口,测试支付用,详见4.1

- **2018-05-22:**

    - 提交购物车接口, 历史纪录发起支付接口, 订单详情接口添加失效时间限制
    - 发起支付接口返回值改动,由于关键字冲突, 将package 改为 packageValue

- **2018-05-24:**

    - 发起支付接口,历史记录发起支付接口,订单详情接口增加图片url和食品ID
    - 支付状态调整为 0 = 未支付  2 = 已支付  3 = 支付超时
    - 获取历史记录接口,订单详情接口 orderStatus更名为 payStatus , orderStatusDesc更名为 payStatusDesc
    - 配送状态调整为 待接单＝1 待取货＝2 配送中＝3 已完成＝4 已取消＝5 已过期＝7 指派单=8 妥投异常之物品返回中=9 妥投异常之物品返回完成=10
    - 订单详情添加配送状态描述 deliveryStatusDesc
    
- **2018-05-27:**
    
    - 订单详情接口,完善物流状态展示
    - 获取商品售卖信息接口分类增加 全部(id=0)
    - 获取订单历史记录列表接口,增加商品列表,总数量字段
    - 提交购物车接口,修改为只返回用户默认地址
    - 增加获取用户地址列表接口
    - 提交订单接口新增食品和餐盒费单价
    - 订单详情group中deliveryDate -> date,配送员姓名和电话转移到配送详情中展示
    
- **2018-06-04:**

    - 公共信息接口,移除区域和取餐地址列表,增加客服电话
    - 添加编辑用户地址,请求内容增加定位名称,经纬度,返回值增加是否支持配送(在最大配送范围之内),以及对应的提示文本,获取地址列表,提交购物车,历史记录发起支付等接口返回的默认地址也增加上述字段
    
- **2018-06-16:**

    - 获取详情接口,图片营养等返回数组形式
    - 统一返回值增加参数判断


- **2018-06-29:**
    
    - 统一返回值增加已截单和区域不支持配送返回值
    - 统一信息配置接口:移除配餐时间列表,只保留客服电话
    - 新增,编辑,获取地址列表接口调整,增加是否免费和取餐点返回值
    - 下单接口新增除去配送费的价格,默认地址新增取餐点,是否免费等字段(历史订单发起支付同提交购物车接口)
    -  
-------




## 接口

## 一、商品接口

#### 1.1获取首页商品的展示信息,包含商品规格,标签,售卖日期等

**请求URL：** 

- ` http://api.huhuixin.com/v1/food `
  
**请求方式：**

- GET 

**参数：** 

无

**返回示例**

``` 
{
    "status": 200,
    "msg": "成功",
    "data": {
        "foods": [
            {
                "foodId": 52,
                "name": "脱骨肘子套餐",
                "sellPoint": "酱汁腌制蒸至软烂脱骨，入口爽口顺滑。",
                "categoryId": 1,
                "imageUrl": "http://image.babymeal.cn/2018/06/24/203433768.jpg",
                "foodItems": [
                    {
                        "foodItemId": 76,
                        "itemName": "儿童份",
                        "price": 1800,
                        "isMain": true,
                        "boxesCost": 100
                    },
                    {
                        "foodItemId": 77,
                        "itemName": "成人份",
                        "price": 2500,
                        "isMain": false,
                        "boxesCost": 200
                    }
                ],
                "labels": [
                    "正餐"
                ],
                "repertory": [
                    {
                        "date": "2018-06-29",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-06-30",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-01",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-02",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-03",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-04",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-05",
                        "mealType": 2,
                        "repertory": 1000
                    }
                ]
            },
            {
                "foodId": 53,
                "name": "绿豆玫瑰冰粉",
                "sellPoint": "冰凉可口，生理期妥妥的保健品。",
                "categoryId": 6,
                "imageUrl": "http://image.babymeal.cn/2018/06/24/205825772.jpg",
                "foodItems": [
                    {
                        "foodItemId": 78,
                        "itemName": "标配",
                        "price": 1800,
                        "isMain": true,
                        "boxesCost": 100
                    }
                ],
                "labels": [
                    "饮品"
                ],
                "repertory": [
                    {
                        "date": "2018-06-30",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-01",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-02",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-03",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-04",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-05",
                        "mealType": 1,
                        "repertory": 1000
                    }
                ]
            },
            {
                "foodId": 54,
                "name": "测试支付",
                "sellPoint": "恭喜就快要上线了。",
                "categoryId": 1,
                "imageUrl": "http://image.babymeal.cn/2018/06/24/213536178.jpg",
                "foodItems": [
                    {
                        "foodItemId": 79,
                        "itemName": "测试",
                        "price": 1,
                        "isMain": true,
                        "boxesCost": 0
                    }
                ],
                "labels": [
                    "正餐"
                ],
                "repertory": [
                    {
                        "date": "2018-06-30",
                        "mealType": 0,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-01",
                        "mealType": 0,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-02",
                        "mealType": 0,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-03",
                        "mealType": 0,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-04",
                        "mealType": 0,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-05",
                        "mealType": 0,
                        "repertory": 3
                    },
                    {
                        "date": "2018-06-30",
                        "mealType": 1,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-01",
                        "mealType": 1,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-02",
                        "mealType": 1,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-03",
                        "mealType": 1,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-04",
                        "mealType": 1,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-05",
                        "mealType": 1,
                        "repertory": 3
                    },
                    {
                        "date": "2018-06-29",
                        "mealType": 2,
                        "repertory": 3
                    },
                    {
                        "date": "2018-06-30",
                        "mealType": 2,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-01",
                        "mealType": 2,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-02",
                        "mealType": 2,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-03",
                        "mealType": 2,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-04",
                        "mealType": 2,
                        "repertory": 3
                    },
                    {
                        "date": "2018-07-05",
                        "mealType": 2,
                        "repertory": 3
                    }
                ]
            },
            {
                "foodId": 55,
                "name": "黄粑",
                "sellPoint": "软糯香甜",
                "categoryId": 5,
                "imageUrl": "http://image.babymeal.cn/2018/06/25/182039185.jpg",
                "foodItems": [
                    {
                        "foodItemId": 80,
                        "itemName": "标准",
                        "price": 1200,
                        "isMain": true,
                        "boxesCost": 0
                    }
                ],
                "labels": [
                    "甜点"
                ],
                "repertory": [
                    {
                        "date": "2018-06-30",
                        "mealType": 0,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-01",
                        "mealType": 0,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-02",
                        "mealType": 0,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-03",
                        "mealType": 0,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-04",
                        "mealType": 0,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-05",
                        "mealType": 0,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-06-30",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-01",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-02",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-03",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-04",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-05",
                        "mealType": 1,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-06-29",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-06-30",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-01",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-02",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-03",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-04",
                        "mealType": 2,
                        "repertory": 1000
                    },
                    {
                        "date": "2018-07-05",
                        "mealType": 2,
                        "repertory": 1000
                    }
                ]
            }
        ],
        "categories": [
            {
                "id": 0,
                "name": "全部"
            },
            {
                "id": 1,
                "name": "正餐"
            },
            {
                "id": 5,
                "name": "甜点"
            },
            {
                "id": 6,
                "name": "饮品"
            }
        ]
    }
}
```

 **返回参数说明** 

|参数名|类型|说明|
|:-----|:-----|-----|
|isMain |boolean |是否是默认显示的规格  |
|boxesCost |int |餐盒费 |
|mealType |int |餐点类型 0早餐 1午餐 2晚餐 |
|repertory |int |剩余库存 |
|categories | array | 分类列表 |

---

#### 1.2 获取商品详情信息

**简要描述：** 

- 获取商品的详细信息,包含大图,营养成分,原材料等展示信息,具体格式待完善

**请求URL：** 

- ` http://api.huhuixin.com/v1/food/{foodId} `
  
**请求方式：**

- GET 

**参数：** 

无

 **返回示例**
 
``` 
{
    "status": 200,
    "msg": "成功",
    "data": {
        "material": [
            "应季食材",
            "原生态无添加"
        ],
        "nutrition": [
            "补钙",
            "维生素"
        ],
        "detailImageUrl": [
            "http://image.babymeal.cn/2018/06/24/203435703.jpg",
            "http://image.babymeal.cn/2018/06/24/203435718.jpg",
            "http://image.babymeal.cn/2018/06/24/203435734.jpg"
        ],
        "description": "孩子份：少许蜂蜜，洋葱，大葱，生姜，大蒜，苹果，雪梨，盐，少许蚝油，淡酱油，混合成酱汁腌制后，蒸软烂；\r\n大人份：孩子份基础上加入了迷迭香，大料，料酒。\r\n"
    }
}
```

 **返回参数说明** 

无

## 二、地址接口

#### 2.1 获取公共地址信息配置

**简要描述：** 

- 获取城市,行政区,区域,居民区4级级联地址, 配送时间, 取餐列表等数据

**请求URL：** 

- ` http://api.huhuixin.com/v1/location/common `
  
**请求方式：**

- GET 

**参数：** 

无

 **返回示例**
 
``` 
{
    "status": 200,
    "msg": "成功",
    "data": {
        "serviceTel": "18611551449"
    }
}
```

 **返回参数说明** 
 
|参数名|类型|说明|
|---- | ----- | ---- |
|deliveryTimes | array | 配送时间列表 |

---

#### 2.2 新增用户地址

**简要描述：** 

- 添加用户收货地址

**请求URL：** 

- ` http://api.huhuixin.com/v1/location/address `
  
**请求方式：**

- POST 

**请求示例：** 



 ``` 
{
    "status": 200,
    "msg": "成功",
    "data": {
        "id": 2,
        "areaName": "区域2",
        "detailAddress": "随便选的地址,不在区域内",
        "isDefault": false,
        "name": "胡汇鑫1",
        "tel": "13888888881",
        "lng": 119.442001,
        "lat": 39.80331,
        "isSupport": false,
        "isFree": false,
        "message": "超出配送最大范围",
        "pickupPoint": null
    }
}
 ```
 
 **请求参数说明** 

|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|-----
|openId |是 |String   |微信openId  
|areaName |是 |String   |编号对应的名称  
|detailAddress |是 |String |详细地址 
|isDefault |否 |boolean |是否设置为默认
|name |是 |String |联系人姓名 
|tel |是 |String |联系人手机
|pickupPoint |否 | String| 去餐点信息


 **返回示例**

``` 
{
    "id": 8,
    "areaName": "地图定位名称",
    "detailAddress": "免费地址且包含取餐点",
    "isDefault": false,
    "name": "胡汇鑫",
    "tel": "13888888888",
    "lng": 116.482113,
    "lat": 39.784649,
    "isSupport": true,
    "isFree": true,
    "message": null,
    "pickupPoint": {
        "id": 1,
        "fenceId": 2,
        "username": "云天明",
        "tel": "13333333333",
        "detailAddress": "3号种植园"
    }
}
```

 **返回参数说明** 

|参数名|类型|说明
|:----- |:-----|-----
|id |int |新增地址的ID

---

#### 2.3 编辑用户地址

**简要描述：** 

- 编辑用户收货地址

**请求URL：** 

- ` http://api.huhuixin.com/v1/location/address `
  
**请求方式：**

- PUT 

**请求示例：** 


 ``` 
{
    "id": 3,
    "areaName": "地图定位名称",
    "detailAddress": "免费地址但不含取餐点",
    "isDefault": false,
    "name": "胡汇鑫",
    "tel": "13888888888",
    "lng": 116.462113,
    "lat": 39.764649,
    "isSupport": true,
    "isFree": true,
    "message": null,
    "pickupPoint": null
}
 ```

 **请求参数说明** 

|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|-----
|openId |是 |String   |微信openId  
|areaNumber |是 |String   |从接口获取到的区域编号  
|areaName |是 |String   |编号对应的名称  
|detailAddress |是 |String |详细地址 
|isDefault |否 |boolean |是否设置为默认
|name |是 |String |联系人姓名 
|tel |是 |String |联系人手机
| id |是 |int| 要修改的地址的ID |

 **返回示例**

``` 
{
    "status": 200,
    "msg": "成功",
    "data": {
        "id": 4,
        "areaName": "地图定位名称",
        "detailAddress": "详细地址2",
        "isDefault": true,
        "name": "胡汇鑫",
        "tel": "18611551449",
        "isSupport": false,
        "message": "超出配送最大范围"
    }
}
```

 **返回参数说明** 

返回修改后的数据

---

#### 2.4 删除用户地址

**简要描述：** 

- 删除用户地址

**请求URL：** 

- ` http://api.huhuixin.com/v1/location/address `
  
**请求方式：**

- DELETE 

**请求示例：** 


 ``` 
 
 { 
     "openId" : "String", 
     "id" : 1 
 } 

 ```

 **请求参数说明** 

|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|-----
|openId |是 |String   |微信openId  
| id |是 |int| 要移除的地址的ID |

 **返回示例**

``` 
 {
    "status": 200,
    "msg": "成功",
    "data": true
}
```

 **返回参数说明** 

返回成功

---

#### 2.5 获取用户地址列表

**简要描述：** 

- 获取用户地址列表

**请求URL：** 

- ` http://api.huhuixin.com/v1/location/addresses `
  
**请求方式：**

- POST 

**请求示例：** 

 ``` 
 { 
     "openId" : "String"
 } 
 ```

 **返回示例**

``` 
{
    "status": 200,
    "msg": "成功",
    "data": [
        {
            "id": 1,
            "areaName": "区域1",
            "detailAddress": "在区域内",
            "isDefault": false,
            "name": "胡汇鑫1",
            "tel": "13888888881",
            "lng": 116.442001,
            "lat": 39.80331,
            "isSupport": true,
            "isFree": false,
            "message": null,
            "pickupPoint": null
        },
        {
            "id": 2,
            "areaName": "区域2",
            "detailAddress": "随便选的地址,不在区域内",
            "isDefault": false,
            "name": "胡汇鑫1",
            "tel": "13888888881",
            "lng": 119.442001,
            "lat": 39.80331,
            "isSupport": false,
            "isFree": false,
            "message": "超出配送最大范围",
            "pickupPoint": null
        },
        {
            "id": 3,
            "areaName": "地图定位名称",
            "detailAddress": "免费地址但不含取餐点",
            "isDefault": false,
            "name": "胡汇鑫",
            "tel": "13888888888",
            "lng": 116.462113,
            "lat": 39.764649,
            "isSupport": true,
            "isFree": true,
            "message": null,
            "pickupPoint": null
        },
        {
            "id": 8,
            "areaName": "地图定位名称",
            "detailAddress": "免费地址且包含取餐点",
            "isDefault": false,
            "name": "胡汇鑫",
            "tel": "13888888888",
            "lng": 116.482113,
            "lat": 39.784649,
            "isSupport": true,
            "isFree": true,
            "message": null,
            "pickupPoint": {
                "id": 1,
                "fenceId": 2,
                "username": "云天明",
                "tel": "13333333333",
                "detailAddress": "3号种植园"
            }
        }
    ]
}
```

 **返回参数说明** 

|参数名|类型|说明
|:----- |:-----|-----
|isDefault |boolean |是否是默认地址

---


## 三、订单相关

#### 3.1提交购物车(创建订单)

**简要描述：** 

- 创建订单的时候需要按组提交购物车信息,返回订单信息和用户地址列表

**请求URL：** 

- ` http://api.huhuixin.com/v1/order `
  
**请求方式：**

- POST 

**请求示例：** 


 ``` 
{
    "openId": "String", 
    "groups": [
        {
            "date": "String", 
            "mealType": 1, 
            "cartItems": [
                {
                    "foodItemId": 1, 
                    "number": 1
                }
            ]
        }
    ]
}
 ```
 
 **请求参数说明** 
 
 
|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|----- |
|openId |是 |String   |微信openId | 
| groups |是 |array  | 按照日期餐点分组 |
| date |是 | string| 分组日期 |
| mealType |是 | int | 分组餐点 0 1 2 早中晚餐 |
| cartItems |是 |array  | 组内商品列表 |
| foodItemId |是 | int | 商品规格ID |
| number |是 | int | 数量 |

 **返回示例**

``` 
{
    "status": 200,
    "msg": "成功",
    "data": {
        "masterNumber": "f0629192845Y8xKM",
        "foodPrice": 18000,
        "boxPrice": 1000,
        "deliveryPrice": 0,
        "totalPrice": 19000,
        "isSubmit": false,
        "userDefaultAddress": {
            "id": 8,
            "areaName": "地图定位名称",
            "detailAddress": "免费地址且包含取餐点",
            "isDefault": false,
            "name": "胡汇鑫",
            "tel": "13888888888",
            "lng": 116.482113,
            "lat": 39.784649,
            "isSupport": true,
            "isFree": true,
            "message": null,
            "pickupPoint": {
                "id": 1,
                "fenceId": 2,
                "username": "云天明",
                "tel": "13333333333",
                "detailAddress": "3号种植园"
            }
        },
        "orderGroups": [
            {
                "date": "2018-06-30",
                "mealType": 2,
                "groupNumber": "f0629192845Y8xKM00",
                "foodPrice": 18000,
                "boxPrice": 1000,
                "deliveryPrice": 0,
                "items": [
                    {
                        "foodId": 52,
                        "foodName": "脱骨肘子套餐-儿童份",
                        "imageUrl": "http://image.babymeal.cn/2018/06/24/203433768.jpg",
                        "number": 10,
                        "foodPrice": 1800,
                        "boxPrice": 100
                    }
                ]
            }
        ],
        "createTime": 1530271725835,
        "payTimeout": 15,
        "withoutDeliveryPrice": 19000
    }
}
```

 **返回参数说明** 

|参数|类型|描述|
|:-------|:-------|:-------|
| orderNumber | string | 订单编号 |
| foodPrice | int | 食品总价格 |
| boxPrice | int | 餐盒费总价 |
| countPrice | int | 总价 |
| createTime | long | 订单创建时间(支付限时开始时间) |
| orderStatus | int | 订单状态已创建 |
| orderGroups | array | 订单分组状态 |

---

#### 3.2 订单内改变收货方式获取运费

**简要描述：** 

- 订单内改变收货方式,切换收货地址时获取运费信息

**请求URL：** 

- ` http://api.huhuixin.com/v1/order/delivery `
  
**请求方式：**

- PUT 

**请求示例：** 

 ``` 
 {
     "openId":"openId",
     "orderNumber":"String",
     "deliveryType":1,
     "deliveryLocationId":1,
 } 
 ```
 
 **请求参数说明** 

|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|-----
|orderNumber |是 |string   |创建订单返回的订单编号  
|deliveryType |是 |int   |配送类型 0 自取 1 送货上门 
|deliveryLocationId |否 |int   |取货点ID 或 用户地址ID deliveryType类型为0是不能为空

 **返回示例**

``` 
{
    "status": 200,
    "msg": "成功",
    "data": 874
}
```

**返回参数说明** 

- 直接返回运费金额(暂定,考虑按餐点分组返回运费)

---

#### 3.3 发起支付

**简要描述：** 

- 发起支付请求

**请求URL：** 

- ` http://api.huhuixin.com/v1/order/pay `
  
**请求方式：**

- POST 

**请求示例：** 

 ``` 
{
  "openId": "String",
  "orderNumber": "String",
  "remark":"这是一个备注信息",
  "deliveryTimes": [
    {
      "groupNumber": "groupNumber",
      "deliveryTime": "String"
    }
  ]
}
 ```
 
 **请求参数说明** 

|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|-----
|openId |是 |String   |微信openId  
|orderNumber |是 |String   |提交购物车返回的订单编号
|deliveryTimes |否 |object |当获改变运费接口设置的类型为送货上门时此项不能为空
|date |是 |String |日期 
|mealType |否 |boolean |餐点类型
|deliveryTime |是 |String |选择的时间 


 **返回示例**

``` 
{
    "status": 200,
    "msg": "成功",
    "data": {
        "appId": "wx1e909c8be352b629",
        "timeStamp": "1526986907",
        "nonceStr": "1526986907479",
        "packageValue": "prepay_id=wx22190138864857bb215eef0c3829117088",
        "signType": "MD5",
        "paySign": "34860955AAB2C08030CF1362A79A96D0"
    }
}
```

 **返回参数说明** 

- 返回的数据为微信公众号支付的参数,直接使用即可


---

#### 3.4 确认支付结果

  
**简要描述：** 

- 用户支付后可以调用此接口确认用户是否支付成功,或者由用户主动确认/查询支付结果

**请求URL：** 

- ` http://api.huhuixin.com/v1/order/verify `
  
**请求方式：**

- POST 

**请求示例：** 

 ``` 
{
  "openId": "String",
  "orderNumber": "String"
}
 ```
 
 **请求参数说明** 

|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|-----
|openId |是 |String   |微信openId  
|orderNumber |是 |String   |提交购物车返回的订单编号

 **返回示例**

``` 
{
    "status": 200,
    "msg": "成功"
}
```

 **返回参数说明** 

- 返回200即为支付成功

---

#### 3.5 获取订单历史记录


**简要描述：** 

- 获取订单历史记录

**请求URL：** 

- ` http://api.huhuixin.com/v1/order/history `
  
**请求方式：**

- POST 

**请求示例：** 

 ``` 
{
    "pageNumber":1,
    "pageSize":10,
    "openId":"ofn7-ty4GOSVYp0RqQPmWCWp2VVk",
    "payStatus":1
}
 ```
 
 **请求参数说明** 

|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|-----
|openId |是 |String   |微信openId  
|pageNumber |否 |int   |第几页 默认 1 
|pageSize |否 |int   | 每页条数 默认 10
|payStatus |否 |int |状态 , 不填则获取全部

 **返回示例**

``` 
{
    "status": 200,
    "msg": "成功",
    "data": [
        {
            "masterNumber": "f0522145704Eoby4",
            "pay": 3600,
            "createTime": 1526972224000,
            "payStatus": 0,
            "payStatusDesc": "未支付",
            "itemCount": 2,
            "items": [
                {
                    "foodName": "食品747-秘制",
                    "number": 2
                }
            ]
        },
        {
            "masterNumber": "f0522160253ermbP",
            "pay": 4200,
            "createTime": 1526976174000,
            "payStatus": 0,
            "payStatusDesc": "未支付",
            "itemCount": 2,
            "items": [
                {
                    "foodName": "食品747-秘制",
                    "number": 1
                },
                {
                    "foodName": "食品747-秘制",
                    "number": 1
                }
            ]
        }
    ]
}
```

 **返回参数说明** 

|参数名|类型|说明
|:----- |:-----|-----
|orderNumber |String |订单编号
|actualPrice |int |订单实付款
|orderStatus |int |订单状态 -1支付超时 0已创建未支付 1已支付未付款 2已付款

---

#### 3.6 历史记录中对未支付的订单发起支付

**简要描述**

- 历史记录中对未支付的订单发起支付

**请求URL：** 

- ` http://api.huhuixin.com/v1/order/history/pay `
  
**请求方式：**

- PUT 

**请求示例：** 

 ``` 
{
  "openId": "String",
  "orderNumber": "String"
}
 ```
 
 **请求参数说明** 

|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|-----
|openId |是 |String   |微信openId  
|orderNumber |是 |String   |提交购物车返回的订单编号

**返回示例**

``` 
{
    "status": 200,
    "msg": "成功",
    "data": {
        "masterNumber": "f06292005320qGvl",
        "foodPrice": 18000,
        "boxPrice": 1000,
        "deliveryPrice": 500,
        "totalPrice": 19500,
        "isSubmit": false,
        "userDefaultAddress": {
            "id": 8,
            "areaName": "地图定位名称",
            "detailAddress": "免费地址且包含取餐点",
            "isDefault": false,
            "name": "胡汇鑫",
            "tel": "13888888888",
            "lng": 116.482113,
            "lat": 39.784649,
            "isSupport": true,
            "isFree": true,
            "message": null,
            "pickupPoint": {
                "id": 1,
                "fenceId": 2,
                "username": "云天明",
                "tel": "13333333333",
                "detailAddress": "3号种植园"
            }
        },
        "orderGroups": [
            {
                "date": "2018-06-30",
                "mealType": 2,
                "groupNumber": "f06292005320qGvl00",
                "foodPrice": 18000,
                "boxPrice": 1000,
                "deliveryPrice": 500,
                "items": [
                    {
                        "foodId": 52,
                        "foodName": "脱骨肘子套餐-儿童份",
                        "imageUrl": "http://image.babymeal.cn/2018/06/24/203433768.jpg",
                        "number": 10,
                        "foodPrice": 1800,
                        "boxPrice": 100
                    }
                ]
            }
        ],
        "createTime": 1530273932185,
        "payTimeout": 15,
        "withoutDeliveryPrice": 19000
    }
}
```

 **返回参数说明** 

|参数名|类型|说明
|:----- |:-----|-----
|chooseAddress |object |订单已经锁定的收货地址
|orderStatus |int | 订单状态 1 已锁定

---

#### 3.7 获取订单详情

**简要描述：** 

- 获取订单详情,包含订单分组,子订单配送信息等

**请求URL：** 

- ` http://api.huhuixin.com/v1/order/detail `
  
**请求方式：**

- POST 

**请求示例：** 

 ``` 
{
  "openId": "String",
  "orderNumber": "String"
}
 ```
 
 **请求参数说明** 

|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|-----
|openId |是 |String   |微信openId  
|orderNumber |是 |String   |提交购物车返回的订单编号

 **返回示例**

``` 
{
    "status": 200,
    "msg": "成功",
    "data": {
        "masterNumber": "f05241715416vthM",
        "payStatus": 1,
        "payStatusDesc": "未支付",
        "deliveryType": 1,
        "deliveryAddress": "总部基地一区 金奔腾科技",
        "username": "胡汇鑫",
        "tel": "13838636728",
        "pay": 8820,
        "totalPrice": 8820,
        "foodPrice": 7220,
        "boxPrice": 600,
        "deliveryPrice": 1000,
        "disPrice": 0,
        "payTime": null,
        "createTime": 1527153342000,
        "payTimeout": 15,
        "groups": [
            {
                "groupNumber": "f05241715416vthM00",
                "foodPrice": 3400,
                "boxPrice": 200,
                "weight": 480,
                "deliveryPrice": 600,
                "deliveryDate": "2018-05-26",
                "mealType": 0,
                "deliveryTime": "11:31",
                "deliveryDetail": {
                    "items": [
                        {
                            "time": "2018-05-27 13:20:09",
                            "status": 2,
                            "statusDesc": "等待配送员取餐"
                        },
                        {
                            "time": "2018-05-27 13:23:56",
                            "status": 3,
                            "statusDesc": "配送中"
                        }
                    ],
                    "dmName": "达达骑手",
                    "dmMobile": "13546670420"
                },
                "deliveryStatus": 0,
                "deliveryStatusDesc" : "等待配送",
                "items": [
                    {
                        "foodId": 1,
                        "foodName": "食品747-秘制",
                        "imageUrl": "http://image.huhuixin.com/pig/food1.jpg",
                        "number": 2,
                        "foodPrice": 1700,
                        "boxPrice": 100
                    }
                ]
            },
            {
                "groupNumber": "f05241715416vthM01",
                "foodPrice": 3820,
                "boxPrice": 400,
                "weight": 340,
                "deliveryPrice": 400,
                "deliveryDate": "2018-05-26",
                "mealType": 2,
                "deliveryTime": "07:21",
                "deliveryDetail": null,
                "deliveryStatus": 0,
                "deliveryStatusDesc" : "等待配送",
                "dmName": null,
                "dmMobile": null,
                "items": [
                    {
                        "foodId": 1,
                        "foodName": "食品747-小份",
                        "imageUrl": "http://image.huhuixin.com/pig/food1.jpg",
                        "number": 2,
                        "foodPrice": 1910,
                        "boxPrice": 200
                    }
                ]
            }
        ]
    }
}
```

 **返回参数说明** 

|参数|类型|描述|
|:-------|:-------|:-------|
| dmName | string| 配送员姓名 |
| dmMobile | number| 配送员编号 |

---

## 四、DEV接口

#### 4.1 模拟支付

**简要描述：** 

- 提交支付信息后模拟支付结果

**请求URL：** 

- ` http://api.huhuixin.com/mock/{orderNumber}/{money} `
  
**请求方式：**

- PUT 

 **请求参数说明** 

|参数名|是否必选|类型|说明
|:----- |:-----  |:-----|-----
|money |是 |String   |订单金额  
|orderNumber |是 |String   |订单编号



