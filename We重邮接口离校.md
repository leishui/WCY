# We重邮有关申请离校的一些接口

## 一、三小时离校申请接口

### **请求网址**：

```http
https://we.cqupt.edu.cn/api/lxsp_new/post_lxsp_spxx.php
```

### **请求方式**：

post，表单提交

### **请求参数**：

```json
{"key":"ey..."}
```

| 参数名 | 参数类型 | 是否必须 | 范例  |
| ------ | -------- | -------- | :---- |
| key    | String   | true     | ey... |

#### **成功返回：**

```json
{"status":200,"message":"OK","data":null}
```

#### **失败返回：**

```json
{"status":"403","message":"已过期","data":null}
```

### key生成步骤：

```JSON
//将以下格式Json进行Base64加密生成key
{
    "xh": "20XXXXXXXX",//学号
    "name": "XX",//姓名
    "xy": "XX学院",//学院
    "nj": "20XX",//年级（入学年份）
    "openid": "XXX",
    "wcmdd": "重庆市,重庆市,南岸区",//外出大地址
    "qjsy": "吃饭",//请假事由
    "wcxxdd": " ",//外出详细地址
    "sfly": "请选择",//是否离渝 We重邮3小时离返校没有此选项 不用管 ?
    "wcrq": "2022-05-12 00:06:00",//【外出日期】对应出校开始时间
    "qjlx": "市内3小时离返校",//请假类型
    "yjfxsj": "2022-05-12 23:35:00",//【预计返校时间】对应出校截止时间
    //所以我好像懂了为什么 市内三小时离校 要选这对离谱的时间
    "beizhu": "",//备注
    "timestamp": 1652349765//当前时间的时间戳
}
```

#### 参数说明

```json

```
## 二、删除出入校申请接口

用于删除已经申报的出入校请求

### 请求网址：

```http
https://we.cqupt.edu.cn/api/lxsp_new/delete_lxsp.php
```

### 请求方式：

post，表单提交

### 请求参数：

```json
//同样需要Base64进行加密解密
{"key":"ey..."}
```

| 参数名 | 参数类型 | 是否必须 | 范例  |
| ------ | -------- | -------- | :---- |
| key    | String   | true     | ey... |

#### 成功返回：

```json
{"status":200,"message":"OK","data":null}
```

#### 失败返回：

```json
{"status":"403","message":"已过期","data":null}
```

### key生成步骤：

```json
//将以下格式Json进行Base64加密生成key
{"xh":"20XXXXXXXX","openid":"XXX","id":"1001XXXX","timestamp":1652350125}
```

#### 参数说明：

```json
{
    "xh": "20XXXXXXXX",//学号
    "openid": "XXX",
    "id": "1001XXXX",//要删除的那一条的id，通过下面的接口获取
    "timestamp": 1652350125//当前时间的时间戳
}
```

## 三、获取申请列表接口

### 请求网址：

```http
https://we.cqupt.edu.cn/api/lxsp_new/get_lxsp_student_list.php
```

### 请求方式：

post，表单提交

### 请求参数：

```json
//同样需要Base64进行加密解密
{"key":"ey..."}
```

| 参数名 | 参数类型 | 是否必须 | 范例  |
| ------ | -------- | -------- | :---- |
| key    | String   | true     | ey... |

### key生成步骤：

```json
//将以下格式Json进行Base64加密生成key
{"openid":"XXX","xh":"20XXXXXXXX","page":1,"timestamp":1652349767}
```

#### 参数说明：

```json
{
	"openid": "xxx",
	"xh": "20XXXXXXXX",//学号
	"page": 1,//页码
	"timestamp": 1645516974//当前时间的时间戳
}
```

