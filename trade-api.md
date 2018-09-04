# 交易api
## 终端交易数据
##### 委托下单
    GET /api/v5/order
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbol | string | yes | 商品名
side | number | yes | BUY买单 SELL卖单
type | string | yes | LIMIT限价 MARKET市价
price | number | yes | 委托价
quantity | number | yes | 委托数量
newClientOrderID | number | yes | 订单ID
timeInForce | number | yes | 订单生效时间
recvWindow | number | yes | 过期时间
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
data | object | yes |
data.trader | string | yes | 交易者ID
data.symbol | string | yes | 商品代码
data.orderId | number | yes | 订单号码
data.clientOrderId | string | yes | 客户端下单id
data.transactTime | number | yes | 下单时间
data.price | string | yes | 委托价格
data.origQty | string | yes | 委托数量
data.executedQty | string | yes | 已成交数量
data.status | string | yes | 状态[BUY --买 SELL--卖 CANCEL--撤单 PARTIAL--部分成交 FULL--全部成交]
data.timeInForce | string | yes | 有效时间，目前默认GTC(挂单到成交为止)
data.type | string | yes | 0限价 1市价
data.side | string | yes | b买单 s卖单
##### 委托查询
    GET /api/v5/allOrders
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbol | string | no | 商品名
side | number | no | BUY买单 SELL卖单
orderID | number | no | 订单ID
startTime | number | no | 最早开始时间，返回值逆时间顺序排列
limit | number | no | 返回数量上限
status | string | yes | 委托状态
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
symbol | string | yes | 商品名
orderId | number | yes | 订单号码
side | string | yes | 买卖类型BUY买单 SELL卖单
price | string | yes | 委托价
origQty | string | yes | 委托数量
executedQty | string | yes | 已成交数量
status | string | yes | 状态【NEW--委托成功 CANCEL--撤单 PARTIAL--部分成交 FULL--全部成交 
updateTime | string | yes | 委托时间
tiemInForce | string | yes | 有效时间，目前默认GTC(挂单到成交为止)
clientOrderID | string | yes | 客户端下单id
type | string | yes | 下单类型:LIMIT, MARKET
icebergQty | string | yes | 保留
matchTime | string | yes | 成交时间
executedPrice | string | yes | 成交价格
stopPrice | string | yes | 保留
commision | string | yes | 手续费
quoteAsset | string | yes | 使用资产
baseAsset | string | yes | 总资产
##### 成交查询
    GET /api/v5/deal
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbol | string | no | 商品名
side | number | no | BUY买单 SELL卖单
orderID | number | no | 订单ID
startTime | number | no | 最早开始时间，返回值逆时间顺序排列
limit | number | no | 返回数量上限
status | string | yes | 委托状态
traderID | string | yes | 成交id
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
symbol | string | yes | 商品名
orderId | number | yes | 订单号码
side | string | yes | 买卖类型BUY买单 SELL卖单
matchTime | string | yes | 成交时间
matcherId | string | yes | 成交的对方用户ID
matchId | string | yes | 成交的对方订单号
executedPrice | string | yes | 成交价
executedQty | string | yes | 成交量
price | string | yes | 委托价
origQty | string | yes | 委托数量
executedQty | string | yes | 已成交数量
status | string | yes | 状态【NEW--委托成功 CANCEL--撤单 PARTIAL--部分成交 FULL--全部成交 
updateTime | string | yes | 委托时间
tiemInForce | string | yes | 有效时间，目前默认GTC(挂单到成交为止)
clientOrderID | string | yes | 客户端下单id
type | string | yes | 下单类型:LIMIT, MARKET
icebergQty | string | yes | 保留
matchTime | string | yes | 成交时间
executedPrice | string | yes | 成交价格
stopPrice | string | yes | 保留
commision | string | yes | 手续费
quoteAsset | string | yes | 使用资产
baseAsset | string | yes | 总资产
tradeID | string | yes | 成交id
tradePrice | string | yes | 成交价格
tradeAmount | string | yes | 成交数量
tradeTime | string | yes | 成交时间
tradeCommission | number | yes | 成交手续费
##### 取消委托订单
    GET /api/v5/cancelOrder
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbol | string | no | 商品名
orderID | number | yes | 订单ID
origClientOrderID | string | no | 
newClientOrderID | string | no | 客户端下单id
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
symbol | string | yes |
orderId | number | yes | 订单号码
origClientOrderId | string | yes | 
clientOrderId | string | yes | 客户端下单id
##### 成交订单
    GET /api/v5/trade
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
orderID | number | yes | 订单ID
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
trader_id | string | yes | 交易者id
user_code | number | yes | 用户id
trade_id | string | yes | 交易id
price | string | yes | 价格
amount | string | yes | 数量
side | string | yes | 买卖方向
type | string | yes | 订单类型
update_time | string | yes | 成交时间
order_id | string | yes | 订单id
symbol | string | yes | 商品名
commission | string | yes | 手续费
matcher_id | string | yes | 成交对方id
match_id | string | yes | 对方成交单号
##### 平台总成交量
    GET /api/v5/total_trades
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
date | string | no | 日期
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
amount | number | yes | 折合USD的成交总量
target | number | yes | 盯市目标
pending_rebate | number | yes | 待分红
##### 平台发币量
    GET /api/v5/total_token
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
date | string | no | 日期
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
amount_22 | number | yes | 22点发币量
amount_24 | number | yes | 22-24点发币量
##### 平台用户交易量
    GET /api/v5/trader_trades
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbol | string | no | 商品名
date | string | no | 日期
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
amount | number | yes | 总数量
commission | number | yes | 手续费
##### 平台用户交易量
    GET /api/v5/trader_rebate
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbol | string | no | 商品名
date | string | no | 日期
type | number | no | 0 平台币　1分红
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
amounts | array[object] | yes | 
amounts.amount | string | yes | 数量
amounts.hour | number | yes | 
amounts.symbol | string | yes | 商品名
##### 平台用户交易量
    GET /api/v5/listAssetFlow
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
symbol | string | no | 商品名
startTime | string | no | 开始时间
endTime | number | no | 结束时间
assetFlowType | number | no | 资产类型
limit | number | no | 限制数量
offset | number | no | 偏移量
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
success | bool | yes | 是否成功
total | number | yes | 总数量
assetFlowList | array[object] | yes |
assetFlowList.flowId | number | yes | 
assetFlowList.trader | number | yes | 
assetFlowList.orderId | number | yes | 
assetFlowList.tradeId | number | yes | 
assetFlowList.matchTime | number | yes | 
assetFlowList.symbolCP | string | yes | 
assetFlowList.insertTime | number | yes | 
assetFlowList.assetBefore | string | yes | 
assetFlowList.assetAfter | string | yes | 
assetFlowList.amt | string | yes | 
assetFlowList.commission | string | yes | 
assetFlowList.assetFreeBefore | string | yes | 
assetFlowList.assetLockedBefore | string | yes | 
assetFlowList.assetFreeAfter | string | yes | 
assetFlowList.assetLockedAfter | string | yes | 
assetFlowList.symbol | string | yes | 
assetFlowList.type | string | yes | 
assetFlowList.assetFlowType | string | yes | 
##### 用户提现记录
    GET /api/v5/withdraw/list
##### Parameters:
Name | Type | Mandatory | Description
--- | --- | --- | ---
asset | string | no | 资产
status | number | no | 状态
startTime | number | no | 开始时间
endTime | number | no | 结束时间
trader | number | no | 交易者
##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
success | bool | yes | 是否成功
WithdrawList | array[object] | yes |
WithdrawList.insertTime | number | yes | 提现时间
WithdrawList.amount | number | yes | 提现金额
WithdrawList.asset | string | yes | 
WithdrawList.status | string | yes | 状态
WithdrawList.id | number | yes | 
##### 交易货币规则限制信息
    GET /api/v5/exchangeAllInfo
##### Parameters:NONE

##### Response:
Name | Type | Mandatory | Description
--- | --- | --- | ---
code | number | yes | 返回码 0表示正确，反 之表示错误码
msg | string | yes | 描述
symbols | array[object] | yes | 
symbols.symbol | string | yes | 商品名
symbols.price_filter | string | yes | 价格限制
symbols.qty_filter | string | yes | 数量限制