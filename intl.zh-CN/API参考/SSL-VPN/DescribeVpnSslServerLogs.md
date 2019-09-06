# DescribeVpnSslServerLogs {#doc_api_Vpc_DescribeVpnSslServerLogs .reference}

调用DescribeVpnSslServerLogs查看SSL服务端的日志。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=DescribeVpnSslServerLogs&type=RPC&version=2016-04-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVpnSslServerLogs|要执行的操作，取值：**DescribeVpnSslServerLogs**。

 |
|RegionId|String|是|cn-hangzhou|SSL服务端所在的地域。您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。

 |
|VpnSslServerId|String|是|vss-bp155e9yclsg1xgq4\*\*\*\*|SSL服务端的ID。

 |
|From|Integer|否|2018020201|日志起始时间。

 |
|MinutePeriod|Integer|否|10|日志周期。

 |
|PageNumber|Integer|否|1|列表的页码，默认值为**1**。

 |
|PageSize|Integer|否|10|分页查询时每页的行数，最大值为**50**，默认值为**10**。

 |
|To|Integer|否|2018020206|日志结束时间。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Count|Integer|10|日志条目数。

 |
|Data| |test|数组，数组中的每一项都为一条日志。

 |
|IsCompleted|Boolean|true|查询的日志是否精确，取值：

 -   **true**：精确。
-   **false**：不精确。

 |
|PageNumber|Integer|1|当前页码。

 |
|PageSize|Integer|1|每页包含的条目数。

 |
|RequestId|String|5BE01CD7-5A50-472D-AC14-CA181C5C03BE|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeVpnSslServerLogs
&RegionId=cn-hangzhou
&VpnSslServerId=vss-bp155e9yclsg1xgq4****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeVpnSslServerLogsResponse>
	  <Data></Data>
	  <PageNumber>1</PageNumber>
	  <Count>0</Count>
	  <PageSize>10</PageSize>
	  <IsCompleted>true</IsCompleted>
	  <RequestId>26641E42-66C7-4942-9FEC-F99213914F8F</RequestId>
</DescribeVpnSslServerLogsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"Data":{
		"Logs":[]
	},
	"Count":0,
	"IsCompleted":true,
	"PageSize":10,
	"RequestId":"26641E42-66C7-4942-9FEC-F99213914F8F"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Vpc)查看更多错误码。

