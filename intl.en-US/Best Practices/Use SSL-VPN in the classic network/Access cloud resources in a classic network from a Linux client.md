# Access cloud resources in a classic network from a Linux client {#concept_qrk_klg_xdb .concept}

This topic describes how to use the SSL-VPN function of a VPN Gateway to access cloud resources deployed in a classic network from a Linux client.

Note that if you have configured the SSL-VPN, you only need to complete Step 5.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13374/15687924763605_en-US.png)

## Prerequisites {#section_oth_2mg_xdb .section}

Before you begin, the following conditions must be met:

-   The Linux client can access the Internet.

-   You have logged on to the new console.

-   A VPC is created and the CIDR block of the VPC is set to 172.16.0.0/12. If you use an existing VPC, the VPC must meet the following conditions:

|VPC CIDR block|Description|
|:-------------|:----------|
|172.16.0.0/12|The VPC does not have a custom route entry whose destination CIDR block is 10.0.0.0/8. You can view the added route entries on the route table details page of the VPC console.

 |
|192.168.0.0/16| -   The VPC does not have a custom route entry whose destination CIDR block is 10.0.0.0/8.

-   A route is added to an ECS instance of the classic network and the route is directed from 192.168.0.0/16 to the private NIC. You can [download a script](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/58095/cn_zh/1502878832385/route192.zip) to add the route.

**Note:** Read the readme file in the script carefully before you run the script.

 |


## Step 1: Create a VPN Gateway {#section_sj5_kmg_xdb .section}

If you use a classic network, the VPN Gateway purchased in the VPC can also be used in the VPC through the ClassicLink function.

To create a VPN Gateway, follow these steps:

1.  Log on to the [VPC console](https://vpcnext.console.aliyun.com).
2.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.
3.  On the displayed page, click **Create VPN Gateway**.
4.  On the purchase page, configure the VPN Gateway and complete the payment. In this example, the VPN Gateway is configured as follows:
    -   **Region**: Select the region to which the VPN Gateway belongs. In this example, select **China \(Hangzhou\)**.

**Note:** The VPN Gateway must be in the same region as the VPC.

    -   **VPC**: Select the target VPC.

    -   **Peak Bandwidth**: Select a peak bandwidth. The bandwidth is the Internet bandwidth of the VPN Gateway.

    -   **IPsec-VPN**: Select whether to enable the IPsec-VPN function, which applies to site-to-site connections.

    -   **SSL-VPN**: Select whether to enable the SSL-VPN function. In this example, select **Enable**.

    -   **SSL Connections**: Select the maximum number of clients to which you want to connect simultaneously.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13374/15687924763606_en-US.png)

5.  Go back to the VPN Gateways page to check the created VPN Gateway.

    The initial status of the VPN Gateway is Preparing. The status changes to Normal in about two minutes and then the VPN Gateway is ready to use.

    **Note:** It takes one to five minutes to create a VPN Gateway.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13374/15687924763607_en-US.png)


## Step 2: Create an SSL server {#section_v4f_2mg_xdb .section}

To create an SSL server, follow these steps:

1.  In the left-side navigation pane, choose**VPN** \> **SSL Servers**.
2.  Click **Create SSL Server**. In this example, the SSL server is configured as follows:
    -   **Name**: Enter a name for the SSL server.

    -   **VPN Gateway**: Select the VPN Gateway created in Step 1.

    -   **Local Network**: **Enter the intranet CIDR block of the ECS instance in the target classic network**. Click **Add Local Network** to add more intranet CIDR blocks.

        In this example, the intranet CIDR blocks are 10.1.0.0/16 and 10.2.0.0/16.

        **Note:** If the IP address of the newly created ECS instance is not in the intranet CIDR blocks, you must add the corresponding intranet CIDR block.

    -   **Client Subnet**: **Enter the IP address used to interconnect the client and the server in the format of CIDR block. The client CIDR block must be a subnet of the CIDR block of the VPC to which the VPN Gateway belongs.**

        In this example, the client CIDR block is 172.16.10.0/24.

        **Note:** The client CIDR block is not the existing IP address of your local client, but the IP address that is assigned to the client for access through SSL VPN.

    -   **Advanced Configuration**: Use the default advanced configuration.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13374/15687924763608_en-US.png)


## Step 3: Create a client certificate {#section_zw2_24g_xdb .section}

To create a client certificate, follow these steps:

1.  In the left-side navigation pane, choose**VPN** \> **SSL Clients** .
2.  Click **Create Client Certificate**.
3.  In the Create Client Certificate dialog box, enter a client certificate name, select the corresponding SSL server, and then click **OK**.
4.  On the SSL Clients page, find the created client certificate, and then click **Download** to download the client certificate.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13374/15687924763609_en-US.png)


## Step 4: Configure the client {#section_qdz_j4g_xdb .section}

To configure the client, follow these steps:

1.  Run the following command to install the OpenVPN client:

    ``` {#codeblock_jcf_a59_beg}
    yum install -y openvpn
    ```

2.  Decompress the certificate downloaded in Step 3 and copy it to the /etc/openvpn/conf/ directory.
3.  Run the following command to start the OpenVPN client:

    ``` {#codeblock_31o_5mn_h6h}
    openvpn --config /etc/openvpn/conf/config.ovpn –daemon
    ```


## Step 5: Establish a ClassicLink connection {#section_sk4_n4g_xdb .section}

To establish a ClassicLink connection, follow these steps:

1.  Log on to the VPC console.
2.  Select the region to which the target VPC belongs, and then click the ID of the target VPC.
3.  On the VPC Details page, click **Enable ClassicLink**.
4.  In the displayed dialog box, click **OK**.
5.  Log on to the ECS console.
6.  In the left-side navigation pane, click **Instances**.
7.  Select one or more ECS instances in the target classic network, and choose**More** \> **Connect to VPC** .

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13374/15687924763610_en-US.png)

8.  In the displayed dialog box, select the target VPC, and then click **OK**.
9.  In the left-side navigation pane, choose**Network & Security** \> **Security Groups** .
10. On the Security Groups page, click the **Internal Network Ingress** tab, and then click **Add Security Group Rule**. Configure the security group rule as follows:
    -   **Rule Direction**: Select Inbound.

    -   **Action**: Select Allow.

    -   **Protocol Type**: Select All.

    -   **Authorization Type**: Select IPv4 CIDR Block.

    -   **Authorization Objects**: Enter the private IP address \(for example, 172.16.3.44/32\) that needs to access the ECS instance through the VPN Gateway.

        Run the ifconfig command on the Linux client, and then find the message that is similar to `inet 172.16.10.6 --> 172.16.10.5 netmask 0xffffffff`, where `172.16.10.6` is the IP address of the client \(the authorization object configured for the security group\).

        **Note:** If you cannot access the ECS instance through the VPN Gateway, the client IP address has changed and you must add a new security group rule.

11. Go back to the ECS console, click the Column Filters icon on the right, select **Connection Status** in the displayed dialog box, and then click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13374/15687924763611_en-US.png)

12. Check the connection status of the ECS instance.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13374/15687924763612_en-US.png)

    After the configuration, you can access the applications deployed in the connected classic network ECS instance from the Linux client.


