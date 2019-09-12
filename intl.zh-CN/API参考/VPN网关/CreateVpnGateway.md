# CreateVpnGateway {#doc_api_Vpc_CreateVpnGateway .reference}

调用CreateVpnGateway接口创建一个VPN网关。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=CreateVpnGateway&type=RPC&version=2016-04-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateVpnGateway|要执行的操作，取值：**CreateVpnGateway**。

 |
|Bandwidth|Integer|是|5|VPN网关的公网带宽，单位Mbps。

 取值：**5|10|20|50|100**。

 |
|RegionId|String|是|cn-hangzhou|VPN网关所在的地域。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。

 |
|VpcId|String|是|vpc-bp1ub1yt9cvakoelj\*\*\*\*|VPN网关所属的VPC ID。

 |
|AutoPay|Boolean|否|false|是否自动支付VPN网关的账单，取值：

 -   **true**：自动支付VPN网关的账单。
-   **false**\(默认值\) ：不自动支付VPN网关的账单。

 |
|EnableIpsec|Boolean|否|true|是否开启IPsec-VPN功能。IPsec-VPN功能提供站点到站点的连接。您可以通过创建IPsec隧道将本地数据中心网络和专有网络或两个专有网络安全地连接起来。取值：

 -   **true**\(默认值\)：开启IPsec-VPN功能。
-   **false**：不开启IPsec-VPN功能。

 |
|EnableSsl|Boolean|否|true|开启SSL-VPN功能。提供点到站点的VPN连接，不需要配置客户网关，终端直接接入。取值：

 -   **true**：开启SSL-VPN功能。
-   **false**\(默认值\) ：不开启SSL-VPN功能。

 |
|InstanceChargeType|String|否|PREPAY|VPN网关的计费方式，取值：

 **POSTPAY**：按量计费。

 |
|Name|String|否|MYVPN|VPN网关的名称，默认值为VPN网关的ID。

 长度为2~100个英文或中文字符，必须以大小字母或中文开头，可包含数字、下划线（\_）和短横线（-），不能以`http://`或`https://`开头。

 |
|Period|Integer|否|1|购买时长，取值：**1~9|12|24|36**。

 **说明：** **InstanceChargeType**参数的值为**PREPAY**时，该参数必选。

 |
|SslConnections|Integer|否|2|允许同时连接的最大客户端数量。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Name|String|myVpn|VPN网关的名称。

 |
|OrderId|Long|20224940022015|订单ID，请前往阿里云控制台完成支付。

 |
|RequestId|String|54B48E3D-DF70-471B-AA93-08E683A1B457|请求ID。

 |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|VPN网关的ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=CreateVpnGateway
&Bandwidth=5
&RegionId=cn-hangzhou
&VpcId=vpc-bp1ub1yt9cvakoelj****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateVpnGatewayResponse>
      <Name>myVpn</Name>
      <VpnGatewayId>vpn-bp1q8bgx4xnkm2ogj****</VpnGatewayId>
      <RequestId>54B48E3D-DF70-471B-AA93-08E683A1B457</RequestId>
</CreateVpnGatewayResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"CreateVpnGatewayResponse":{
		"Name":"myVpn",
		"VpnGatewayId":"vpn-bp1q8bgx4xnkm2ogj****",
		"RequestId":"54B48E3D-DF70-471B-AA93-08E683A1B457"
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Resource.QuotaFull|The quota of resource is full|资源配额已达上限。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Vpc)查看更多错误码。

