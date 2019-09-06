# DescribeVpnRouteEntries {#doc_api_Vpc_DescribeVpnRouteEntries .reference}

Queries a VPN destination route.

## Debug {#api_explorer .section}

[Use OpenAPI Explorer to perform debug operations and generate SDK code examples.](https://api.aliyun.com/#product=Vpc&api=DescribeVpnRouteEntries&type=RPC&version=2016-04-28)

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example value|Description|
|---------|----|---------|-------------|-----------|
|Action|String|Yes|DescribeVpnRouteEntries|The name of this action. Value: **DescribeVpnRouteEntries**.

 |
|RegionId|String|Yes|cn-hangzhou|The ID of the region to which the VPN destination route belongs. To query the region ID, call [DescribeRegions](~~36063~~).

 |
|VpnGatewayId|String|Yes|vpn-bp1a3kqjiiq9legfx\*\*\*\*|The ID of the VPN Gateway.

 |
|PageNumber|Integer|No|1|The page number. Default value: **1**.

 |
|PageSize|Integer|No|10|The number of rows per page in the paged query. Maximum value: **50**. Default value: **10**.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example value|Description|
|---------|----|-------------|-----------|
|PageNumber|Integer|10|The current page number.

 |
|PageSize|Integer|10|The number of entries per page.

 |
|RequestId|String|0ED8D006-F706-4D23-88ED-E11ED28DCAC0|The ID of the request.

 |
|TotalCount|Integer|10|The total number of entries.

 |
|VpnRouteEntries| | |The details of the VPN destination route.

 |
|CreateTime|Long|1492747187000|The time when the VPN route was created.

 |
|NextHop|String|vco-bp15oes1py4i66rmd\*\*\*\*|The next hop of the destination route.

 |
|RouteDest|String|10.0.0.0/24|The destination CIDR block of the destination route.

 |
|State|String|published|The status of the VPN destination route.

 |
|VpnInstanceId|String|vpn-bp1cmw7jh1nfe43m9\*\*\*\*|The ID of the VPN Gateway.

 |
|Weight|Integer|0|The weight of the destination route. Valid values: **0**|**100**.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://[Endpoint]/? Action=DescribeVpnRouteEntries
&RegionId=cn-hangzhou
&VpnGatewayId=vpn-bp1a3kqjiiq9legfx****
&<CommonParameters>

```

Response example

`XML` format

``` {#xml_return_success_demo}
<DescribeVpnRouteEntriesResponse>
	  <PageNumber>1</PageNumber>
	  <TotalCount>1</TotalCount>
	  <VpnRouteEntries>
		    <VpnRouteEntry>
			      <RouteDest>10.0.0.0/24</RouteDest>
			      <VpnInstanceId>vpn-bp1cmw7jh1nfe43m9****</VpnInstanceId>
			      <State>normal</State>
			      <Weight>100</Weight>
			      <CreateTime>1563874074000</CreateTime>
			      <NextHop>vco-bp1tui07ob10fmuro****</NextHop>
		    </VpnRouteEntry>
	  </VpnRouteEntries>
	  <PageSize>10</PageSize>
	  <RequestId>BF3995A6-FA4F-4C74-B90F-89ECF4BFF4D5</RequestId>
</DescribeVpnRouteEntriesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"VpnRouteEntries":{
		"VpnRouteEntry":[
			{
				"RouteDest":"10.0.0.0/24",
				"VpnInstanceId":"vpn-bp1cmw7jh1nfe43m9****",
				"Weight":100,
				"State":"normal",
				"NextHop":"vco-bp1tui07ob10fmuro****",
				"CreateTime":1563874074000
			}
		]
	},
	"RequestId":"BF3995A6-FA4F-4C74-B90F-89ECF4BFF4D5"
}
```

## Errors { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|Forbidden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|You are not authorized to use this resource. Apply for the permission and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|You are not authorized to use this resource. For more information, open a ticket.|

