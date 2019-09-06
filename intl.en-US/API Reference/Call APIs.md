# Call APIs {#concept_354701 .concept}

VPN Gateway and VPC use the same service address \(endpoint\). This means that when you call VPN Gateway APIs, HTTP GET requests are sent to the API end point of VPN Gateway, and the system responds according to the parameters set in the request. Both the requests and responses are UTF-8 encoded.

## Request syntax {#section_oh9_42n_k0m .section}

VPN Gateway APIs use RPC style. To call VPN Gateway APIs, send HTTP GET requests.

The structure of a VPN Gateway API request is as follows:

``` {#codeblock_cxj_4ce_kuw}
http://Endpoint/?Action=xx&Parameters
```

Where:

-   Endpoint: The endpoint of VPN Gateway APIs is `vpc.aliyuncs.com`.
-   Action: the name of the action. For example, if you need to create a VPN Gateway, the action is CreateVpnGateway.
-   Version: the version of the API. The version of VPN APIs is 2016-04-28.
-   Parameters: the request parameters. Separate multiple parameters by using ampersands \(&\).

    Request parameters include common parameters and API-specific parameters. Common parameters include API version and identity authentication information among other parameters. For more information, see [Common parameters](../../../../reseller.en-US/API reference/Common parameters.md#).


The following is an example of calling CreateVpnGateway to create a VPN Gateway:

**Note:** The following code has been edited to improve readability.

``` {#codeblock_c2t_00w_ifn}
https://vpc.aliyuncs.com/?Action=CreateVpnGateway
&Format=xml 
&Version=2016-04-28 
&Signature=xxxx%xxxx%3D
&SignatureMethod=HMAC-SHA1 
&SignatureNonce=15215528852396 
&SignatureVersion=1.0 
&AccessKeyId=key-test 
&Timestamp=2012-06-01T12:00:00Z 
…
```

## API authorization {#section_dg5_yrv_pxr .section}

To maintain account security, we recommend that you use the Access Keys \(AKs\) of RAM users to call APIs. Before you call APIs using the AKs of RAM users, you need to grant permissions to the RAM users by attaching corresponding policies to them.

For more information about the policies related to VPN Gateway APIs, see [RAM authentication](../../../../reseller.en-US/API reference/RAM authentication.md#).

## Request signature {#section_sbz_565_l4h .section}

Authentication is required by the VPN Gateway service for each API call, which is provided by the inclusion of signature information in the request.

VPN Gateway uses an AccessKeyID and AccessKeySecret pair \(that is, an AK\) and symmetric encryption to authenticate the identity of the request sender. AKs are certificates that Alibaba Cloud issues to Alibaba Cloud accounts and RAM users for authentication. It is similar to a logon password. The AccessKeyID is used to identify the visitor's identity. The AccessKeySecret is the key used to encrypt the signature string. The server uses the AccessKeySecret to decrypt the signature string. The AccessKeySecret must be kept confidential.

A request in an API call is signed in the following format:

`https://endpoint/?SignatureVersion=*1.0*&SignatureMethod=*HMAC-SHA1*&Signature=*XXXX%3D&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0axxxxxxxx*`

Take the API call of CreateVpnGateway as an example. If your AccessKey ID is `testid`, and your AccessKey Secret is `testsecret`, then, the URL in the signature is as follows:

``` {#codeblock_ymo_8xb_ocj}
http://vpc.aliyuncs.com/?Action=CreateVpnGateway
&Timestamp=2016-05-23T12:46:24Z 
&Format=XML 
&AccessKeyId=testid 
&SignatureMethod=HMAC-SHA1 
&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0axxxxxxxx 
&Version=2014-05-26 
&SignatureVersion=1.0 
```

To generate the signature, follow these steps:

1.  Create the string to be signed by using the request parameter.

    ``` {#codeblock_qky_psb_y4i}
    GET&%2F&AccessKeyId%3Dtestid&Action%3DCreateVpnGateway&Format%3DXML&SignatureMethod%3DHMAC-SHA1&SignatureNonce%3D3ee8c1b8-83d3-44af-a94f-4e0axxxxxxxx&SignatureVersion%3D1.0&TimeStamp%3D2016-02-23T12%253A46%253A24Z&Version%3D2014-05-15
    ```

    .

2.  Calculate the HMAC value of the string.

    Add an ampersand \(&\) after the AccessKeySecret to add the key of the HMAC value. In this example, the key is `testsecret&`.

    ``` {#codeblock_ahy_s0f_jx2}
    CT9X0VtwR86fNWS********juE=
    ```

3.  Add the signature to the request parameter.

    ``` {#codeblock_fo1_3fd_ars}
    http://vpc.aliyuncs.com/?Action=CreateVpnGateway
    &Timestamp=2016-05-23T12:46:24Z 
    &Format=XML
    &AccessKeyId=testid
    &SignatureMethod=HMAC-SHA1
    &SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0axxxxxxxx
    &Version=2014-05-26
    &SignatureVersion=1.0
    &Signature=XXXX%3D
    ```


