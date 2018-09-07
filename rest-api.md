# EXCHBTC公共API
## 通用API信息
- 终端的地址是：https://www.exchbtc.com
- 所以终端返回一个json对象或数组
- 数据以升序返回。
- 所有时间和时间戳相关字段都以毫秒为单位。
- HTTP 4XX返回码用于格式错误的请求;问题在于请求方。
- HTTP 429返回代码用于请求速率限制。
- HTTP 418返回码是当IP在接收到429码后被自动禁止继续发送请求时使用的。
- HTTP 5XX返回码是

## 限制
- /api/v7/exchangeInfo rateLimits数组包含与交换器的REQUEST_WEIGHT和订单速率限制相关的对象。
- 当违反任何一个速率限制时，将返回429。
- 每个路由都有一个权重，它决定每个端点计数的请求数量。较重的端点和对多个符号进行操作的端点的权重更大。
- 当收到429时，作为一个API，您有义务退后一步，不要向API发送垃圾信息。
- 反复违反速率限制和/或在接收429秒后不后退将导致自动IP禁用(http st)
## 端点安全类型
- 每个端点都有一个确定您将如何与其交互的安全类型。
- API键通过X-MBX-APIKEY头传递到Rest API。
- api键和秘钥是区分大小写的。
- 可以将api键配置为只访问特定类型的安全端点。例如，一个API-key只能用于贸易，而另一个API-key只能访问除贸易路线之外的所有内容。
- 默认情况下，api -key可以访问所有安全路由。

安全类型 | 描述
--- | ---
行情 | 终端可以自由访问。
交易 | 端点需要发送有效的API-KEY和签名。
## 签名(交易和USER_DATA)端点安全性
- 终端签名需要在查询字符串或请求体中发送额外的参数签名。
- 终端使用HMAC SHA256签名。HMAC SHA256签名是一个键控的HMAC SHA256操作。使用secretKey作为键，totalParams作为HMAC操作的值。
- 签名不区分大小写。
- totalParams定义为与请求主体连接的查询字符串。
## 时间的安全
- 签名端点还需要发送一个参数timestamp，该参数应该是创建和发送请求时的毫秒时间戳。
- 可以发送一个额外的参数recvWindow来指定请求有效的时间戳之后的毫秒数。如果不发送recvWindow，则默认为5000。
- 逻辑如下:`if (timestamp < (serverTime + 1000)) && (serverTime - timestamp) <= recvWindow) {// process request} else {// reject request}`
- 真正的交易是关于时机的。网络可能是不稳定和不可靠的，这可能导致请求花费不同的时间到达服务器。使用recvWindow，您可以指定请求必须在一定毫秒内被处理或被服务器拒绝。
- 建议使用5000或更少的recvWindow !
## GET /api/v7/order的终端签名示例
Key | Value
--- | ---
apiKey | vmPUZE6mv9SD5VNHk4HlWFsOr6aKE2zvsw0MuIgwCIPy6utIco14y7Ju91duEh8A
secretKey | NhqPtmdSJYdKjVHjA7PZj4Mge3R5YNiP1e3UZjInClVN65XAbvqqM6A7H5fATj0j

Parameter | Value
--- | ---
symbol | EBBTC
side | BUY
type | LIMIT
quantity | 1
price | 0.1
newClientOrderID | d292cfdc-0104-4b37-997c-7804770063cf
timeInForce | GTC
recvWindow | 5000
## 示例:作为查询字符串
- 查询字符串:
symbol=EBBTC&side=BUY&type=LIMIT&timeInForce=GTC&quantity=1&price=0.1&recvWindow=5000&newClientOrderID=d292cfdc-0104-4b37-997c-7804770063cf&timestamp=1499827319559
- HMAC SHA256签名:

[linux]$ echo -n "symbol=LTCBTC&side=BUY&type=LIMIT&timeInForce=GTC&quantity=1&price=0.1&recvWindow=5000&timestamp=1499827319559" | openssl dgst -sha256 -hmac "NhqPtmdSJYdKjVHjA7PZj4Mge3R5YNiP1e3UZjInClVN65XAbvqqM6A7H5fATj0j"
(stdin)= c8db56825ae71d6d79447849e617115f4a920fa2acdcab2b053c4b2838bd6b71
- curl命令:

(HMAC SHA256)
[linux]$ curl -H "X-MBX-APIKEY: vmPUZE6mv9SD5VNHk4HlWFsOr6aKE2zvsw0MuIgwCIPy6utIco14y7Ju91duEh8A" -X GET 'https://www.exchbtc.com/api/v3/order?symbol=LTCBTC&side=BUY&type=LIMIT&timeInForce=GTC&quantity=1&price=0.1&recvWindow=5000&timestamp=1499827319559&signature=c8db56825ae71d6d79447849e617115f4a920fa2acdcab2b053c4b2838bd6b71'
# 终端公共API
## 术语
- base asset refers to the asset that is the quantity of a symbol.
- quote asset refers to the asset that is the price of a symbol.
## 枚举定义
##### 订单状态:
- NEW
- PARTIALLY_FILLED
- FILLED
- CANCELED
- PENDING_CANCEL (currently unused)
- REJECTED
- EXPIRED
##### 订单类型:
- LIMIT
- MARKET
##### 订单方向:
- BUY
- SELL
##### Time in force:
- GTC
- IOC
- FOK
##### K线/柱状图间隔
m -> minutes; h -> hours; d -> days; w -> weeks; 
- 1m
- 5m
- 15m
- 30m
- 1h
- 2h
- 4h
- 6h
- 12h
- 1d
- 1w
##### 速率限制
- REQUESTS_WEIGHT
- ORDERS
##### 速率限制的间隔
- SECOND
- MINUTE
- DAY
##### 连接测试
    GET /ping
##### 检查服务器时间
    GET /time
##### Exchange information
    GET /api/v7/exchangeInfo
##### Parameters:NONE
##### Response:
    {
    "symbols":[
        {
            "symbol":"ETCBTC",
            "status":"TRADING",
            "baseAsset":"ETC",
            "baseAssetPrecision":2,
            "quoteAsset":"BTC",
            "quotePrecision":6,
            "orderTypes":"LIMIT,MARKET",
            "filters":""
        },
        {
            "symbol":"XRTNEO",
            "status":"TRADING",
            "baseAsset":"XRT",
            "baseAssetPrecision":8,
            "quoteAsset":"NEO",
            "quotePrecision":8,
            "orderTypes":"LIMIT,MARKET",
            "filters":""
        },
        {
            "symbol":"ZECBTC",
            "status":"TRADING",
            "baseAsset":"ZEC",
            "baseAssetPrecision":3,
            "quoteAsset":"BTC",
            "quotePrecision":6,
            "orderTypes":"LIMIT,MARKET",
            "filters":""
        },
        {
            "symbol":"XMRETH",
            "status":"TRADING",
            "baseAsset":"XMR",
            "baseAssetPrecision":3,
            "quoteAsset":"ETH",
            "quotePrecision":5,
            "orderTypes":"LIMIT,MARKET",
            "filters":""
        },
        {
            "symbol":"XRPUSDT",
            "status":"TRADING",
            "baseAsset":"XRP",
            "baseAssetPrecision":1,
            "quoteAsset":"USDT",
            "quotePrecision":5,
            "orderTypes":"LIMIT,MARKET",
            "filters":""
        }
        ......
    ]}
## 终端行情数据
##### 历史K线
    GET /api/v1/klines
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbol | string | yes | 商品名
interval | number | no | K线类型:MIN1 MIN3 MIN5 MIN15 MIN30 HOUR1 HOUR2 HOUR4 HOUR6 HOUR8 HOUR12 DAY1 DAY3 WEEK MONTH
limit | number | no | 行情数量
startTime | number | no | 开始时间
endTime | number | no | 结束时间
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
OpenTime | number | yes | 第一口价时间
Open | number | yes | 开盘价
High | number | yes | 最高价
Low | number | yes | 最低价
Close | number | yes | 收盘价
Volume | number | yes | 成交量
CloseTime | number | yes | 最一口价时间
##### 最新报价
    GET /api/v1/lastquote
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbol | string | yes | 商品名
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
s | string | yes | 商品代码
p | number | yes | 涨跌值
P | number | yes | 涨跌百分比
l | number | yes | 前一天的收盘价
o | number | yes | 开盘价
n | number | yes | 当前价
Q | number | yes | 当前成交量
v | number | yes | 成交量 包括买卖双方
m | number | yes | 成交金额
max | number | yes | 最高价
min | number | yes | 最低价
av | number | yes | 均价
c | number | yes | 成交笔数
O | number | yes | 开始时间
t | number | yes | 最后更新时间
F | number | yes | 第一笔成交ID
L | number | yes | 最后一笔成交ID
bids | array[number] | yes | 盘口行情（卖）
asks | array[number] | yes | 盘口行情（买）
d | number | yes | 买卖方向
u | boolean | yes | 
##### 成交明细
    GET /api/v1/tlk
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbol | string | yes | 商品名
limit | number | no | 行情数量
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
data | array[number] | yes | 
data.Price | number | yes | 价格
data.Volume | number | yes | 数量
data.Timestamp | number | yes | 时间
##### 实时行情
    GET /
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbols | string | yes | 商品名
fields | number | yes | 返回字段
depth | number | yes | 深度
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
s | string | yes | 商品代码
p | number | yes | 涨跌值
P | number | yes | 涨跌百分比
l | number | yes | 前一天的收盘价
o | number | yes | 开盘价
n | number | yes | 当前价
Q | number | yes | 当前成交量
v | number | yes | 成交量 包括买卖双方
m | number | yes | 成交金额
max | number | yes | 最高价
min | number | yes | 最低价
av | number | yes | 均价
c | number | yes | 成交笔数
O | number | yes | 开始时间
t | number | yes | 最后更新时间
F | number | yes | 第一笔成交ID
L | number | yes | 最后一笔成交ID
bids | array[number] | yes | 盘口行情（卖）
asks | array[number] | yes | 盘口行情（买）
d | number | yes | 买卖方向