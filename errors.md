# Error codes for Binance (2018-07-18)
Errors consist of two parts: an error code and a message. Codes are universal, but messages can vary. Here is the error JSON payload:

{
  "code":-1121,
  "msg":"Invalid symbol."
}
## 10xx - General Server or Network issues
##### -1000 UNKNOWN
An unknown error occured while processing the request.
##### -1001 DISCONNECTED
Internal error; unable to process your request. Please try again.
##### -1002 UNAUTHORIZED
You are not authorized to execute this request.
##### -1003 TOO_MANY_REQUESTS
Too many requests; please use the websocket for live updates.
Too many requests; current limit is %s requests per minute. Please use the websocket for live updates to avoid polling the API.
Way too many requests; IP banned until %s. Please use the websocket for live updates to avoid bans.
##### -1006 UNEXPECTED_RESP
An unexpected response was received from the message bus. Execution status unknown.
##### -1007 TIMEOUT
Timeout waiting for response from backend server. Send status unknown; execution status unknown.
##### -1014 UNKNOWN_ORDER_COMPOSITION
Unsupported order combination.
##### -1015 TOO_MANY_ORDERS
Too many new orders.
Too many new orders; current limit is %s orders per %s.
##### -1016 SERVICE_SHUTTING_DOWN
This service is no longer available.
##### -1020 UNSUPPORTED_OPERATION
This operation is not supported.
##### -1021 INVALID_TIMESTAMP
Timestamp for this request is outside of the recvWindow.
Timestamp for this request was 1000ms ahead of the server's time.
##### -1022 INVALID_SIGNATURE
Signature for this request is not valid.
11xx - Request issues
##### -1100 ILLEGAL_CHARS
Illegal characters found in a parameter.
Illegal characters found in parameter '%s'; legal range is '%s'.
##### -1101 TOO_MANY_PARAMETERS
Too many parameters sent for this endpoint.
Too many parameters; expected '%s' and received '%s'.
Duplicate values for a parameter detected.
##### -1102 MANDATORY_PARAM_EMPTY_OR_MALFORMED
A mandatory parameter was not sent, was empty/null, or malformed.
Mandatory parameter '%s' was not sent, was empty/null, or malformed.
Param '%s' or '%s' must be sent, but both were empty/null!
##### -1103 UNKNOWN_PARAM
An unknown parameter was sent.
##### -1104 UNREAD_PARAMETERS
Not all sent parameters were read.
Not all sent parameters were read; read '%s' parameter(s) but was sent '%s'.
##### -1105 PARAM_EMPTY
A parameter was empty.
Parameter '%s' was empty.
##### -1106 PARAM_NOT_REQUIRED
A parameter was sent when not required.
Parameter '%s' sent when not required.
##### -1111 BAD_PRECISION
Precision is over the maximum defined for this asset.
##### -1112 NO_DEPTH
No orders on book for symbol.
##### -1114 TIF_NOT_REQUIRED
TimeInForce parameter sent when not required.
##### -1115 INVALID_TIF
Invalid timeInForce.
##### -1116 INVALID_ORDER_TYPE
Invalid orderType.
##### -1117 INVALID_SIDE
Invalid side.
##### -1118 EMPTY_NEW_CL_ORD_ID
New client order ID was empty.
##### -1119 EMPTY_ORG_CL_ORD_ID
Original client order ID was empty.
##### -1120 BAD_INTERVAL
Invalid interval.
##### -1121 BAD_SYMBOL
Invalid symbol.
##### -1125 INVALID_LISTEN_KEY
This listenKey does not exist.
##### -1127 MORE_THAN_XX_HOURS
Lookup interval is too big.
More than %s hours between startTime and endTime.
##### -1128 OPTIONAL_PARAMS_BAD_COMBO
Combination of optional parameters invalid.
##### -1130 INVALID_PARAMETER
Invalid data sent for a parameter.
Data sent for paramter '%s' is not valid.
##### -2010 NEW_ORDER_REJECTED
NEW_ORDER_REJECTED
##### -2011 CANCEL_REJECTED
CANCEL_REJECTED
##### -2013 NO_SUCH_ORDER
Order does not exist.
##### -2014 BAD_API_KEY_FMT
API-key format invalid.
##### -2015 REJECTED_MBX_KEY
Invalid API-key, IP, or permissions for action.
##### -2016 NO_TRADING_WINDOW
No trading window could be found for the symbol. Try ticker/24hrs instead.
## Messages for -1010 ERROR_MSG_RECEIVED, -2010 NEW_ORDER_REJECTED, and  -2011 CANCEL_REJECTED
Error message | Description
--- | --- 
"Unknown order sent." | The order (by either orderId, clOrdId, origClOrdId) could not be found

## -9xxx Filter failures
Error message | Description
--- | --- 
"Unknown order sent." | The order (by either orderId, clOrdId, origClOrdId) could not be found