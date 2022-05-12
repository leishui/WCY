# We重邮有关每日打卡的一些接口分享
***
2022/5/12 新增[三小时离校申请接口](https://github.com/leishui/WCY/blob/main/We%E9%87%8D%E9%82%AE%E6%8E%A5%E5%8F%A3%E7%A6%BB%E6%A0%A1.md)
***
2022/3/29 新增了渝康码颜色选项`"jkmresult":"绿色"`
***
## 一、打卡接口

### **请求网址**：

```http
https://we.cqu.pt/api/mrdk/post_mrdk_info.php
```

### **请求方式**：

post，表单提交

### **请求参数**：

```json
{"key":"eyJuYW1lIjoiWFhYIiwieGgiOiIyMFhYWFhYWFhYIiwieGIiOiLnlLciLCJvcGVuaWQiOiJYWFgiLCJsb2NhdGlvbkJpZyI6IuS4reWbvSxYWOecgSxYWOW4gixYWOWMuiIsImxvY2F0aW9uU21hbGwiOiJYWOecgVhY5biCWFjljLpYWOi3r1hY5Y+3IiwibGF0aXR1ZGUiOlhYLlhYWCwibG9uZ2l0dWRlIjpYWFguWFhYWFgsInN6ZHEiOiJYWOecgSxYWOW4gixYWOWMuiIsInh4ZHoiOiJYWFhYWCIsInl3amNxemJsIjoi5L2O6aOO6ZmpIiwieXdqY2hibGoiOiLml6AiLCJ4anpkeXdxemJsIjoi5pegIiwidHdzZnpjIjoi5pivIiwieXd5dGR6eiI6IuaXoCIsImJlaXpodSI6IuaXoCIsIm1yZGtrZXkiOiJFYzZ3MUJDNSIsInRpbWVzdGFtcCI6MTYxMjU4Nzc4OX0="}
```

| 参数名 | 参数类型 | 是否必须 | 范例                                                         |
| ------ | -------- | -------- | :----------------------------------------------------------- |
| key    | String   | true     | eyJuYW1lIjoiWFhYIiwieGgiOiIyMFhYWFhYWFhYIiwieGIiOiLnlLciLCJvcGVuaWQiOiJYWFgiLCJsb2NhdGlvbkJpZyI6IuS4reWbvSxYWOecgSxYWOW4gixYWOWMuiIsImxvY2F0aW9uU21hbGwiOiJYWOecgVhY5biCWFjljLpYWOi3r1hY5Y+3IiwibGF0aXR1ZGUiOlhYLlhYWCwibG9uZ2l0dWRlIjpYWFguWFhYWFgsInN6ZHEiOiJYWOecgSxYWOW4gixYWOWMuiIsInh4ZHoiOiJYWFhYWCIsInl3amNxemJsIjoi5L2O6aOO6ZmpIiwieXdqY2hibGoiOiLml6AiLCJ4anpkeXdxemJsIjoi5pegIiwidHdzZnpjIjoi5pivIiwieXd5dGR6eiI6IuaXoCIsImJlaXpodSI6IuaXoCIsIm1yZGtrZXkiOiJFYzZ3MUJDNSIsInRpbWVzdGFtcCI6MTYxMjU4Nzc4OX0= |

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
{"name":"XX","xh":"20XXXXXXXX","xb":"男","openid":"XXX","locationBig":"中国,XX省,XX市,XX区","locationSmall":"XX省XX市XX区XX路XX号","latitude":XX.XXX,"longitude":XXX.XXXXX,"szdq":"XX省,XX市,XX区","xxdz":"XXXXX","ywjcqzbl":"低风险","ywjchblj":"无","xjzdywqzbl":"无","twsfzc":"是","ywytdzz":"无","beizhu":"无","mrdkkey":"Ec6w1BC5","timestamp":1612587789}
```

#### 参数说明

```json
//【注】除最后两项参数外，其他参数建议抓包获得 用抓包软件抓取电脑端微信中的微信小程序
//格式化后的Json
{
	"name": "XXX",//姓名
	"xh": "20XXXXXXXX",//学号
	"xb": "男",//性别["男","女"]
	"openid": "XXX",//1.抓包获得 2.用下面的Bind接口自己设
    //======此部分在we重邮中均通过定位获取，不是用户自己设的========
    //也可以通过地图获取到这些定位信息再手动填上
	"locationBig": "中国,XX省,XX市,XX区",//大位置
	"locationSmall": "XX省XX市XX区XX路XX号",//小位置
	"latitude": 11.111,//纬度
	"longitude": 111.11111,//经度
    //==========此部分与We重邮相符==============================
	"szdq": "XX省,XX市,XX区",//所在地区
	"xxdz": "XXXXX",//详细地址
	"ywjcqzbl": "低风险",//新冠风险等级
	"ywjchblj": "无",//14天高风险旅居史
	"xjzdywqzbl": "无",//14天接触高风险人员
	"twsfzc": "是",//体温是否正常
	"ywytdzz": "无",//有无感染有关症状
	"beizhu": "无",//备注
	"mrdkkey": "Ec6w1BC5",//由下面方法计算得
	"timestamp": 1612587789//当前时间的时间戳
}
//【例】
{
	//。。。
	"locationBig": "中国,重庆市,重庆市,南岸区",//大位置
	"locationSmall": "重庆邮电大学",//小位置
	"latitude": 29.53304,//纬度
	"longitude": 106.60770,//经度
	"szdq": "重庆市,重庆市,南岸区",//所在地区
	"xxdz": "重庆邮电大学 xx栋xxx",//详细地址
	//。。。
}
```

#### `mrdkkey`获得方法：

```javascript
//日期【0-30】
r=["s9ZS","jQkB","RuQM","O0_L","Buxf","LepV","Ec6w","zPLD","eZry","QjBF","XPB0","zlTr","YDr2","Mfdu","HSoi","frhT","GOdB","AEN0","zX0T","wJg1","fCmn","SM3z","2U5I","LI3u","3rAY","aoa4","Jf9u","M69T","XCea","63gc","6_Kf"]
//小时【0-23】
u=["89KC","pzTS","wgte","29_3","GpdG","FDYl","vsE9","SPJk","_buC","GPHN","OKax","_Kk4","hYxa","1BC5","oBk_","JgUW","0CPR","jlEh","gBGg","frS6","4ads","Iwfk","TCgR","wbjP"];
keymrdk:function(e,f){return r[e]+u[f]}
//与月份无关，由日期与当前小时有关
//【例】2021/2/22 15:28
//日期为22，小时为15
//即mrdkkey 为 r[22]+u[15] 为 2U5IoBk_
//【注】这里小时没什么问题 是0时至23时
//【注】但是日期31时我没试过，可能是用r[0]="s9ZS" 感觉这里We重邮是设计问题还是故意为之就无从得知了
```

## 二、Bind接口

用于绑定`openid`

### 请求网址：

```http
https://we.cqupt.edu.cn/api/users/bind.php
```

### 请求方式：

post，表单提交

### 请求参数：

```json
//同样需要Base64进行加密解密
{"key":"eyJvcGVuaWQiOiJ4eHgiLCJ5a3RpZCI6IjEiLCJwYXNzd2QiOiIxIiwidGltZXN0YW1wIjoxNjQ1NTE2OTc0fQ=="}
```

| 参数名 | 参数类型 | 是否必须 | 范例                                                         |
| ------ | -------- | -------- | :----------------------------------------------------------- |
| key    | String   | true     | eyJvcGVuaWQiOiJ4eHgiLCJ5a3RpZCI6IjEiLCJwYXNzd2QiOiIxIiwidGltZXN0YW1wIjoxNjQ1NTE2OTc0fQ== |

#### 成功返回：

```json
{"status":200,"message":"ok","data":{"openid":"xxx","name":"xxx","xh":"20xxxxxxxx","sfzh":"","ykth":"xxxxxx","build":"","room":"","yxm":"xxxx学院","type":"本科生","sex":"男","volunteer_uid":""}}
```

#### 失败返回：

```json
{"status":400,"message":"账号或密码错误","data":{"openid":"xxx","yktid":"1","passwd":"1","timestamp":1645516974}}
```

### key生成步骤：

```json
//将以下格式Json进行Base64加密生成key
{"openid":"xxx","yktid":"1","passwd":"1","timestamp":1645516974}
```

#### 参数说明：

```json
{
	"openid": "xxx",//可以自己随便设置别跟别人重了就行，请求成功后可以用这个id调用每日打卡和其他接口
	"yktid": "1",//账号（统一认证码）
	"passwd": "1",//密码
	"timestamp": 1645516974//当前时间的时间戳
}
```

## 三、get_mrdk_flag接口

用于判断是否打过卡

### 请求网址：

```http
https://we.cqupt.edu.cn/api/mrdk/get_mrdk_flag.php
```

### 请求方式：

post，表单提交

### 请求参数：

```json
//同样需要Base64进行加密解密
{"key":"eyJ4aCI6IjIweHh4eHh4eHgiLCJvcGVuaWQiOiJ4eHh4IiwidGltZXN0YW1wIjoxNjQ1NTE4ODkzfQ"}
```

| 参数名 | 参数类型 | 是否必须 | 范例                                                         |
| ------ | -------- | -------- | :----------------------------------------------------------- |
| key    | String   | true     | eyJ4aCI6IjIweHh4eHh4eHgiLCJvcGVuaWQiOiJ4eHh4IiwidGltZXN0YW1wIjoxNjQ1NTE4ODkzfQ |

#### 成功返回：

```json
{"status":200,"message":"ok","data":{"count":"1"}}//count表示打过几次卡，没打就是"0"
```

#### 失败返回：

```json
{"status":"403","message":"已过期","data":null}
```

### key生成步骤：

```json
//将以下格式Json进行Base64加密生成key
{"xh":"20xxxxxxxx","openid":"xxxx","timestamp":1645518893}
```

#### 参数说明：

```json
{
	"openid": "xxx",//目前随便啥填都可以
	"xh": "20xxxxxxxx",//学号
	"timestamp": 1645516974//当前时间的时间戳
}
```

