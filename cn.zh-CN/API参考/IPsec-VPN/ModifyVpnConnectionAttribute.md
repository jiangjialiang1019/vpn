# ModifyVpnConnectionAttribute {#doc_api_Vpc_ModifyVpnConnectionAttribute .reference}

调用ModifyVpnConnectionAttribute接口修改IPsec连接的配置信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=ModifyVpnConnectionAttribute&type=RPC&version=2016-04-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyVpnConnectionAttribute|要执行的操作，取值： **ModifyVpnConnectionAttribute**。

 |
|RegionId|String|是|cn-shanghai|IPsec连接所在的地域。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。

 |
|VpnConnectionId|String|是|vco-bp1bbi27hojx80nck\*\*\*\*|IPsec连接的ID。

 |
|AutoConfigRoute|Boolean|否|true|是否自动发布路由。

 |
|ClientToken|String|否|02fb3da4-130e-11e9-8e44-0016e04115b|用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符。

 |
|EffectImmediately|Boolean|否|false|是否删除当前已协商成功的IPsec隧道并重新发起协商。取值：

 -   **true**：配置完成后立即进行协商。
-   **false**（默认值）：当有流量进入时进行协商。

 |
|IkeConfig|String|否|ikev1, ikev2|第一阶段协商的配置信息：

 -   **IkeConfig.Psk**：用于IPsec VPN网关与用户网关之间的身份认证。默认情况下会随机生成，也可以手动指定密钥。长度限制为100个字符。
-   **IkeConfig.IkeVersion**：IKE协议的版本。取值：ikev1|ikev2，默认值：ikev1。
-   **IkeConfig.IkeMode**：IKE V1版本的协商模式。取值：main（主模式）|aggressive（野蛮模式），默认值：main。
-   **IkeConfig.IkeEncAlg**：第一阶段协商的加密算法，取值：aes|aes192|aes256|des|3des，默认值：aes。
-   **IkeConfig.IkeAuthAlg**：第一阶段协商的认证算法，取值：md5|sha1，默认值：sha。

IkeConfig.IkePfs：第一阶段协商使用的Diffie-Hellman密钥交换算法，取值：group1|group2|group5|group14|group24，默认值：group2。

-   **IkeConfig.IkeLifetime**：第一阶段协商出的SA的生存周期。取值范围为0~86400，单位为秒，默认值：86400。
-   **IkeConfig.LocalIdIPsec**：VPN网关的标识，长度限制为100个字符，默认值为VPN网关的公网IP地址。
-   **IkeConfig.RemoteId**：用户网关的标识，长度限制为100个字符，默认值为用户网关的公网IP地址。

 |
|IpsecConfig|String|否|sha1|第二阶段协商的配置信息：

 -   **IpsecConfig.IpsecEncAlg**：第二阶段协商的加密算法，取值：aes|aes192|aes256|des|3des，默认值：aes。
-   **IpsecConfig. IpsecAuthAlg**：第二阶段协商的认证算法，取值：md5|sha1，默认值：sha1。
-   **IpsecConfig. IpsecPfs**：转发所有协议的报文。第一阶段协商使用的Diffie-Hellman密钥交换算法，取值：group1|group2|group5|group14|group24，默认值：group2。
-   **IpsecConfig. IpsecLifetime**：第二阶段协商出的SA的生存周期。取值范围为0~86400，单位为秒，默认值：86400。

 |
|LocalSubnet|String|否|1.1.1.0/24,1.1.2.0/24|需要和本地IDC互连的VPC侧的网段，用于第二阶段协商。

 多个网段之间用逗号分隔，例如：192.168.1.0/24,192.168.2.0/24。

 |
|Name|String|否|IPsec|IPsec连接的名称。

 长度为2~128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-）。但不能以`http://`或`https://`开头。

 |
|RemoteSubnet|String|否|1.1.1.0/24,1.1.2.0/24|本地IDC的网段，用于第二阶段协商。

 多个网段之间用逗号分隔，例如：192.168.3.0/24,192.168.4.0/24。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|VpnConnectionId|String|vco-bp1bbi27hojx80nck\*\*\*\*|IPsec连接的ID。

 |
|CustomerGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|用户网关的ID。

 |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|VPN网关的ID。

 |
|Name|String|test|IPsec连接的名称。

 |
|LocalSubnet|String|1.1.1.0/24,1.1.2.0/24|VPC侧的网段。

 |
|RemoteSubnet|String|1.1.1.0/24,1.1.2.0/24|本地IDC侧的网段。

 |
|CreateTime|Long|1492753817000|IPsec连接的创建时间。

 |
|Description|String|description|描述信息。

 |
|EffectImmediately|Boolean|false|IPsec连接是否立即生效。

 |
|IkeConfig| | |第一阶段协商的配置。

 |
|IkeAuthAlg|String|sha1|IKE认证算法，可选sha1和MD5。

 |
|IkeEncAlg|String|aes|IKE加密算法。

 |
|IkeLifetime|Long|86400|IKE生存时间。

 |
|IkeMode|String|main|IKE模式，可选main和aggressive模式,main模式安全性高，如果启用了NAT穿越，建议选择aggressive模式

 |
|IkePfs|String|group2|DH分组，可选group1，group2，group5，group14，group24。

 |
|IkeVersion|String|ikev1|IKE版本。

 |
|LocalId|String|116.62.69.64|本端ID，支持FQDN和IP格式，默认为当前选取的VPN网关IP地址。

 |
|Psk|String|pgw6dy7d1i8in7x5|预共享密钥。

 |
|RemoteId|String|139.196.32.167|对端ID，支持FQDN和IP格式，默认为当前选取的用户网关IP地址。

 |
|IpsecConfig| | |第二阶段协商的配置。

 |
|IpsecAuthAlg|String|sha1|IPsec认证算法，可选sha1和md5。

 |
|IpsecEncAlg|String|aes|IPsec加密算法。

 |
|IpsecLifetime|Long|86400|IPsec生存时间。

 |
|IpsecPfs|String|group2|DH分组。

 |
|RequestId|String|7DB79D0C-5F27-4AB5-995B-79BE55102F90|请求ID。

 |
|VcoHealthCheck| | |健康检查配置。

 |
|Dip|String|1.1.1.xx|目标IP。

 |
|Enable|String|true|是否开启健康检查：

 -   **true**：已开启。
-   **false**：未开启。

 |
|Interval|Integer|3|健康检查的重试间隔时间，单位是秒。

 |
|Retry|Integer|1|健康检查的重试发包次数。

 |
|Sip|String|2.2.2.xx|源IP。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://vpc.aliyuncs.com/?Action=ModifyVpnConnectionAttribute
&RegionId=cn-shanghai
&VpnConnectionId=vco-bp1bbi27hojx80nck****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyVpnConnectionAttributeResponse>
      <Name>vpn连接测试</Name>
      <CustomerGatewayId>cgw-bp1pvpl9r9adju6l5****</CustomerGatewayId>
      <RemoteSubnet>2.2.2.0/24</RemoteSubnet>
      <IpsecConfig>
            <IpsecLifetime>86400</IpsecLifetime>
            <IpsecAuthAlg>sha1</IpsecAuthAlg>
            <IpsecPfs>group2</IpsecPfs>
            <IpsecEncAlg>aes</IpsecEncAlg>
      </IpsecConfig>
      <EffectImmediately>false</EffectImmediately>
      <VpnGatewayId>vpn-bp1q8bgx4xnkm2ogj****</VpnGatewayId>
      <CreateTime>1492753817000</CreateTime>
      <VpnConnectionId>vco-bp10lz7aejumd2vxo****</VpnConnectionId>
      <RequestId>57070A3D-38F2-40A6-A1C9-DB14542EF54D</RequestId>
      <LocalSubnet>1.1.1.0/24,1.1.2.0/24</LocalSubnet>
      <IkeConfig>
            <IkeEncAlg>aes</IkeEncAlg>
            <RemoteId>139.196.32.xx</RemoteId>
            <IkePfs>group2</IkePfs>
            <IkeAuthAlg>sha1</IkeAuthAlg>
            <Psk>pgw6dy7d1i8i****</Psk>
            <IkeMode>main</IkeMode>
            <IkeLifetime>86400</IkeLifetime>
            <IkeVersion>ikev1</IkeVersion>
            <LocalId>116.62.69.xx</LocalId>
      </IkeConfig>
</ModifyVpnConnectionAttributeResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"CustomerGatewayId":"cgw-bp1pvpl9r9adju6l5****",
	"Name":"vpn连接测试",
	"RemoteSubnet":"2.2.2.0/24",
	"IpsecConfig":{
		"IpsecLifetime":86400,
		"IpsecAuthAlg":"sha1",
		"IpsecPfs":"group2",
		"IpsecEncAlg":"aes"
	},
	"VpnGatewayId":"vpn-bp1q8bgx4xnkm2ogj****",
	"EffectImmediately":false,
	"RequestId":"7DB79D0C-5F27-4AB5-995B-79BE55102F90",
	"VpnConnectionId":"vco-bp10lz7aejumd2vxo****",
	"CreateTime":1492753817000,
	"LocalSubnet":"1.1.1.0/24,1.1.2.0/24",
	"IkeConfig":{
		"IkeEncAlg":"aes",
		"IkePfs":"group2",
		"RemoteId":"139.196.32.xx",
		"IkeAuthAlg":"sha1",
		"Psk":"pgw6dy7d1i8i****",
		"IkeMode":"main",
		"IkeLifetime":86400,
		"IkeVersion":"ikev1",
		"LocalId":"116.62.69.xx"
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|404|InvalidVpnConnectionInstanceId.NotFound|The specified vpn connection instance id does not exist.|指定的 VPN 连接不存在，请您检查该 VPN 链接是否正确。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|该服务已欠费，请您先充值再操作。|
|400|InvalidName|The name is not valid|该名称格式不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

