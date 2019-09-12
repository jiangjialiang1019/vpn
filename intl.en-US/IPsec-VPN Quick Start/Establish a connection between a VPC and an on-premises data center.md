# Establish a connection between a VPC and an on-premises data center {#concept_c4h_slz_wdb .concept}

This topic describes how to use the IPsec-VPN function to establish a connection between a VPC and an on-premises data center.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13351/15682509553312_en-US.png)

## Prerequisites {#section_q3w_ylz_wdb .section}

Before you can use the IPsec-VPN function to establish a connection between a VPC and an on-premises data center, the following conditions must be met:

-   The gateway device of the on-premises data center operates properly. Alibaba Cloud VPN Gateways support standard IKEv1 and IKEv2 protocols. Devices that support these two protocols can connect to Alibaba Cloud VPN Gateways, including devices from Huawei, H3C, Hillstone, SANGFOR, Cisco ASA, Juniper, SonicWall, Nokia, IBM, and Ixia.
-   A static public IP address is configured for the gateway device of the on-premises data center.
-   The CIDR block of the on-premises data center does not overlap the CIDR block of the VPC.

## Step 1: Create a VPN Gateway {#section_vfk_2mz_wdb .section}

To create a VPN Gateway, follow these steps:

1.  Log on to the [VPC console](https://partners-intl.aliyun.com/login-required#/vpc).
2.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.
3.  On the VPN Gateways page, click **Create VPN Gateway**.
4.  On the purchase page, set the parameters, and then click **Buy Now** to complete the payment.
    -   **Name**: Enter a name for the VPN Gateway.
    -   **Region**: Select a region for the VPN Gateway.

        **Note:** The VPN Gateway must be in the same region as the VPC.

    -   **VPC**: Select the VPC to be connected.
    -   **Peak Bandwidth**: Select a peak bandwidth. The bandwidth is the Internet bandwidth of the VPN Gateway.
    -   **IPsec-VPN**: Enable the IPsec-VPN function.
    -   **SSL-VPN**: Select whether to enable the SSL-VPN function. The SSL-VPN function allows access to the VPC from a computer anywhere.
    -   **SSL connections**: Select the maximum number of clients to which you want to connect simultaneously.

        **Note:** This parameter is valid only after the SSL-VPN function is enabled.

    -   **Billing Cycle**: Select a billing cycle.
5.  Go back to the VPN Gateways page to check the created VPN Gateway.

    The initial status of the VPN Gateway is Preparing. The status changes to Normal in about two minutes and then the VPN Gateway is ready to use.

    **Note:** It takes one to five minutes to create a VPN Gateway.


## Step 2: Create a customer gateway {#section_upz_wmz_wdb .section}

To create a customer gateway, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **Cusomer Gateways**.
2.  Select the region in which you want to create a customer gateway.
3.  On the Customer Gateways page, click **Create Customer Gateway**.
4.  On the Create Customer Gateway page, set the parameters, and then click **OK**.
    -   **Name**: Enter a name for the customer gateway.
    -   **IP Address**: Enter the private IP address of the gateway device in the on-premises data center.
    -   **Description**: Enter a description of the customer gateway.

## Step 3: Create an IPsec connection {#section_ty2_jnz_wdb .section}

To create an IPsec connection, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.
2.  Select the region in which you want to create an IPsec connection.
3.  On the IPsec Connections page, click **Create IPsec Connection**.
4.  On the Create IPsec Connection page, set the parameters, and then click **OK**.
    -   **Name**: Enter a name for the IPsec connection.
    -   **VPN Gateway**: Select the created VPN Gateway.
    -   **Customer Gateway**: Select the customer gateway to be connected.
    -   **Local Network**: Enter the CIDR block of the VPC to which the selected VPN Gateway belongs.
    -   **Remote Network**: Enter the CIDR block of the on-premises data center.
    -   **Effective Immediately**: Select whether to negotiate immediately.
        -   Yes: Both ends of the IPsec connection negotiate immediately after the configuration is completed.
        -   No: Both ends of the IPsec connection negotiate only when traffic is detected in the tunnel.
    -   **Pre-Shared Key**: Enter a pre-shared key. It must be the same as that configured for the local gateway.

        Use the default settings for other parameters.


## Step 4: Load the VPN configuration to the local gateway {#section_ptn_44z_wdb .section}

To load the VPN configuration to the local gateway, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.
2.  Select the region to which the target IPsec connection belongs.
3.  On the IPsec Connections page, find the target IPsec connection, and then click **Download Configuration** in the **Actions** column.
4.  Add the downloaded configuration to the local gateway device. For more information, see [Local gateway configuration](../../../../reseller.en-US/User Guide/Configure IPsec-VPN connections/Configure local gateways/Configure an IPsec-VPN connection through a USG series Next-Generation Firewall device (Huawei).md#).

    RemotSubnet and LocalSubnet are opposite to the Local Network and Remote Network that you set when you create an IPsec connection in Step 3. Specifically, for the VPN Gateway, its remote network is the CIDR block of the on-premises data center and its local network is the CIDR block of the VPC. For the local gateway, LocalSubnet is the CIDR block of the on-premises data center and RemoteSubnet is the CIDR block of the VPC.


## Step 5: Configure a route for the VPN Gateway {#section_tfw_9lp_avu .section}

To configure a route for the VPN Gateway, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.
2.  Select the region to which the target VPN gateway belongs.
3.  On the VPN Gateways page, find the target VPN Gateway, and then click the instance ID in the Instance ID/Name column.
4.  On the Destination-based Routing tab, click **Add Route Entry**.
5.  On the Add Route Entry page, set the parameters, and then click **OK**.
    -   **Destination CIDR Block**: Enter the private CIDR block of the on-premises data center.
    -   **Next Hop**: Select the IPsec connection instance.
    -   **Publish to VPC**: Select whether to publish the new route to the VPC route table. In this example, select Yes.
    -   **Weight**: Select a weight. In this example, select 100.

## Step 6: Test the connection {#section_ojw_ylz_wdb .section}

Log on to an ECS instance \(without a public IP address\) in the connected VPC. Use the ping command to ping the private IP address of a server in the on-premises data center to check whether the connection is established.

