## 修改记录

- **2018-07-23：**

```
增加获取小区列表接口, 详情接口增加取餐点详情信息
```

- **2018-07-05：**

```
增加登录接口,重构接口参数
```

- **2018-07-05：**

```
打印列表接口增加是否已打印的筛选入参
```

- **2018-07-04：**

```
初始文档，增加列表&打印接口
```

## 接口

-   http://app.babymeal.cn/app

### 登录

**请求方式**

- GET

**接口入参**

- /login?username=hhx&password=123456

**返回示例**

```
{
    "status": 200,
    "msg": "成功",
    "data": "0dea0061-cd59-48a7-a25d-d130275bd154"
}
```



### 获取小区列表

**请求方式**

- GET

**接口入参**

- /app/common/fence?token=abd4e91b-c4b6-4cab-b92e-a028b318d7eb

**返回示例**

```
{
    "status": 200,
    "msg": "成功",
    "data": [
        {
            "id": 1,
            "name": "枫丹一号(一期,二期)"
        },
        {
            "id": 2,
            "name": "中信新城"
        },
        {
            "id": 3,
            "name": "紫禁壹号院"
        },
        {
            "id": 4,
            "name": "金茂悦北区"
        },
        {
            "id": 5,
            "name": "金茂悦南区"
        },
        {
            "id": 6,
            "name": "金域东郡"
        },
        {
            "id": 7,
            "name": "大雄城市花园"
        }
    ]
}
```


### 出餐列表

**请求方式**

- GET

**接口入参**

- /delivery/order?token=1937b7fa-b218-4334-bf4b-029f1c117e15&deliveryStatus=0&number=1&size=20&deliveryDate=2018-07-06&mealType=2
&deliveryType=0


 **请求参数说明** 
 
|参数名|说明
|-----|-----
|token|认证标识
|deliveryType| 取餐类型 0 自取 1 送餐到家
|deliveryStatus| 0等待出餐 1已出餐(已打印) 2已到达自提点 3已完成
|mealType| 出餐点 0早餐 1午餐 2晚餐
|deliveryDate| 出餐日期
|fenceId | 小区ID,接口获取
|number| 页号，从1开始
|size| 每页大小 默认10


**返回示例**

```
{
    "status": 200,
    "msg": "成功",
    "data": [
        {
            "groupNumber": "f06292005320qGvl00",
            "deliveryDate": "2018-06-30",
            "mealType": 2,
            "deliveryType": 0,
            "deliveryStatus": 0,
            "username": "胡汇鑫",
            "tel": "13888888888",
            "deliveryAddress": "3号种植园",
            "createTime": "2018-06-29 12:05:32",
            "remark": null,
            "items": [
                {
                    "foodName": "脱骨肘子套餐",
                    "itemName": "儿童份",
                    "number": 10
                }
            ],
            "deliveryTypeDesc": "餐点自取",
            "mealTypeDesc": "晚餐",
            "deliveryStatusDesc": "等待发货"
        },
        {
            "groupNumber": "f0702084902pMCIY00",
            "deliveryDate": "2018-07-03",
            "mealType": 2,
            "deliveryType": 0,
            "deliveryStatus": 0,
            "username": "胡汇鑫1",
            "tel": "13888888881",
            "deliveryAddress": "3号种植园",
            "createTime": "2018-07-02 00:49:03",
            "remark": null,
            "items": [
                {
                    "foodName": "脱骨肘子套餐",
                    "itemName": "儿童份",
                    "number": 10
                }
            ],
            "deliveryTypeDesc": "餐点自取",
            "mealTypeDesc": "晚餐",
            "deliveryStatusDesc": "等待发货"
        }
    ]
}
```

### 出餐打印

**请求方式**

- GET

**接口入参**

- /delivery/print?token=1937b7fa-b218-4334-bf4b-029f1c117e15&groupNumbers=f0629194242NzIDM00&flag=0


 **请求参数说明** 
 
|参数名|说明
|-----|-----
|token|认证标识
|orderNumbers|子订单号列表
|flag| 0第一次打单 1补打 2打印预览


**返回示例**

```
{
    "status": 200,
    "msg": "成功",
    "data": [
        {
            "groupNumber": "f0711192223hEY8o00",
            "createTime": "2018-07-11 11:22:24",
            "deliveryType": 0,
            "deliveryTypeDesc": "餐点自取",
            "username": "胡汇鑫",
            "tel": "13888888888",
            "deliveryAddress": "枫丹一号 枫丹一号",
            "items": [
                {
                    "foodName": "脱骨肘子套餐",
                    "itemName": "儿童份",
                    "number": 5,
                    "price": 1900
                }
            ],
            "prices": [
                {
                    "name": "餐盒费",
                    "price": 100
                },
                {
                    "name": "配送费",
                    "price": 0
                },
                {
                    "name": "总计",
                    "price": 1900
                }
            ],
            "pay": 1900,
            "serviceTel": "18910344126",
            "pickupPoint": {
                "id": 2,
                "username": "黄牧",
                "tel": "18910344126",
                "detailAddress": "枫丹一号一期物业大堂"
            }
        }
    ]
}
```

