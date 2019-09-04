# DownloadVpnConnectionConfig {#doc_api_Vpc_DownloadVpnConnectionConfig .reference}

调用DownloadVpnConnectionConfig接口获取IPsec连接的配置信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=DownloadVpnConnectionConfig&type=RPC&version=2016-04-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DownloadVpnConnectionConfig|要执行的操作，取值： **DownloadVpnConnectionConfig**。

 |
|RegionId|String|是|cn-shanghai|IPsec连接所在的地域。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。

 |
|VpnConnectionId|String|是|vco-bp1bbi27hojx80nck\*\*\*\*|IPsec连接的ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|0C68048B-0F70-40DA-B8AE-1B79B5CF62E3|请求ID。

 |
|VpnConnectionConfig| | |IPsec连接的配置信息。

 |
|IkeConfig| | |IKE配置相关配置信息。

 |
|IkeAuthAlg|String|sha1|IKE认证算法，支持sha1和MD5。

 |
|IkeEncAlg|String|aes|IKE加密算法。

 |
|IkeLifetime|Long|86400|IKE生存时间。

 |
|IkeMode|String|main|IKE模式，支持main和aggressive模式。main模式安全性高，如果启用了NAT穿越，建议使用aggressive模式。

 |
|IkePfs|String|group2|DH分组。

 |
|IkeVersion|String|ikev1|IKE版本。

 |
|LocalId|String|116.62.69.xx|本端ID，支持FQDN和IP格式，默认为当前选取的VPN网关IP地址。

 |
|Psk|String|pgw6dy7d1i8i\*\*\*\*|预共享密钥。

 |
|RemoteId|String|139.196.32.xx|对端ID，支持FQDN和IP格式，默认为当前选取的用户网关IP地址。

 |
|IpsecConfig| | |IPsec配置信息。

 |
|IpsecAuthAlg|String|sha1|IPsec认证算法，支持sha1和md5。

 |
|IpsecEncAlg|String|aes|IPsec加密算法。

 |
|IpsecLifetime|Long|86400|IPsec生存时间。

 |
|IpsecPfs|String|group2|DH分组。

 |
|Local|String|139.196.32.xx|IPsec VPN网关的标识。

 |
|LocalSubnet|String|1.1.1.0/24,1.1.2.0/24|VPC侧的网段。

 |
|Remote|String|116.62.69.xx|用户网关的标识。

 |
|RemoteSubnet|String|1.1.1.0/24,1.1.2.0/24|本地IDC侧的网段。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://vpc.aliyuncs.com/?Action=DownloadVpnConnectionConfig
&RegionId=cn-shanghai
&VpnConnectionId=vco-bp1bbi27hojx80nck****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DownloadVpnConnectionConfigResponse>
      <RequestId>6F4A035F-7060-45D7-B9BD-719372782AF6</RequestId>
      <VpnConnectionConfig>
            <RemoteSubnet>1.1.1.0/24,1.1.2.0/24</RemoteSubnet>
            <Local>139.196.32.xx</Local>
            <IpsecConfig>
                  <IpsecLifetime>86400</IpsecLifetime>
                  <IpsecAuthAlg>sha1</IpsecAuthAlg>
                  <IpsecPfs>group2</IpsecPfs>
                  <IpsecEncAlg>aes</IpsecEncAlg>
            </IpsecConfig>
            <Remote>116.62.69.xx</Remote>
            <LocalSubnet>2.2.2.0/24</LocalSubnet>
            <IkeConfig>
                  <IkeEncAlg>aes</IkeEncAlg>
                  <IkePfs>group2</IkePfs>
                  <RemoteId>116.62.69.xx</RemoteId>
                  <IkeAuthAlg>sha1</IkeAuthAlg>
                  <Psk>pgw6dy7d1i8i****</Psk>
                  <IkeMode>main</IkeMode>
                  <IkeLifetime>86400</IkeLifetime>
                  <IkeVersion>ikev1</IkeVersion>
                  <LocalId>139.196.32.xx</LocalId>
            </IkeConfig>
      </VpnConnectionConfig>
</DownloadVpnConnectionConfigResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"0C68048B-0F70-40DA-B8AE-1B79B5CF62E3",
	"VpnConnectionConfig":{
		"RemoteSubnet":"1.1.1.0/24,1.1.2.0/24",
		"IpsecConfig":{
			"IpsecLifetime":86400,
			"IpsecAuthAlg":"sha1",
			"IpsecPfs":"group2",
			"IpsecEncAlg":"aes"
		},
		"Local":"139.196.32.xx",
		"Remote":"116.62.69.64",
		"LocalSubnet":"2.2.2.0/24",
		"IkeConfig":{
			"IkeEncAlg":"aes",
			"RemoteId":"116.62.69.xx",
			"IkePfs":"group2",
			"IkeAuthAlg":"sha1",
			"Psk":"pgw6dy7d1i8i****",
			"IkeMode":"main",
			"IkeLifetime":86400,
			"IkeVersion":"ikev1",
			"LocalId":"139.196.32.xx"
		}
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|404|InvalidVpnConnectionInstanceId.NotFound|The specified vpn connection instance id does not exist.|指定的 VPN 连接不存在，请您检查该 VPN 链接是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

