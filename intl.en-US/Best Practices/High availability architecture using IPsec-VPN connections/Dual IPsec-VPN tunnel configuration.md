# Dual IPsec-VPN tunnel configuration {#concept_qrk_klg_xdb .concept}

This topic describes how to establish two IPsec-VPN tunnels with a VPN Gateway to implement active and standby tunnels. This configuration is suitable for a local gateway with two public IP addresses.

## Overview {#section_km4_rsq_fhb .section}

You can connect a VPN Gateway with two public IP addresses \(in this example, they are labeled as IP1 and IP2\) to establish two IPsec-VPN connections, and enable health checks. Afterwards, you can set the weights of the corresponding two routes to set one route as the active route and the other route as the standby route. The IPsec-VPN tunnel associated with the active route is the active tunnel, and the IPsec-VPN tunnel associated with the standby route is the standby tunnel.

-   In this way, when the IP1-based Internet link is normal, all traffic between the on-premises data center and the VPC is forwarded only through this connection because it is the active tunnel.
-   When the IP1-based Internet link is abnormal, all traffic between the on-premises data center and the VPC is directed to the standby tunnel.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136912/156163056441844_en-US.png)

## Prerequisites {#section_oth_2mg_xdb .section}

Before you begin, make sure that the following conditions are met:

-   The gateway device of the on-premises data center is normal. Alibaba Cloud VPN Gateway supports standard IKEv1 and IKEv2 protocols. Devices that support these two protocols can connect to Alibaba Cloud VPN Gateway, including devices of Huawei, H3C, Hillstone, SANGFOR, Cisco ASA, Juniper, SonicWall, Nokia, IBM, Ixia, and more.
-   A static public IP address is configured for the gateway device of the on-premises data center.
-   The CIDR blocks of the on-premises data center and the VPC to be connected do not conflict with each other.

## Step 1: Create a VPN Gateway {#section_jgc_bf6_3np .section}

To create a VPN Gateway, follow these steps:

1.  Log on to the [VPC console](https://partners-intl.aliyun.com/login-required#/vpc).
2.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.
3.  On the VPN Gateways page, click **Create VPN Gateway**.
4.  On the purchase page, configure the VPN Gateway according to the following information and click **Buy Now**.
    -   **Name**: Enter the name of the VPN Gateway.
    -   **Region**: Select the region to which the VPN Gateway belongs.

        **Note:** Make sure that the VPC and the VPN Gateway are in the same region.

    -   **VPC**: Select the VPC to be connected.
    -   **Peak Bandwidth**: Select a bandwidth. The bandwidth is the Internet bandwidth of the VPN Gateway.
    -   **IPsec-VPN**: Select whether to enable the IPsec-VPN feature.
    -   **SSL-VPN**: Select whether to enable the SSL-VPN feature. The SSL-VPN feature allows you to connect to a VPC from a computer anywhere.
    -   **SSL connections**: Select the maximum number of clients you want to connect to simultaneously.

        **Note:** You can only configure this option after you enable the SSL-VPN feature.

    -   **Billing Cycle**: Select the validity period of the purchase.
5.  Go back to the VPN Gateways page to view the created VPN Gateway.

    The initial status of a VPN Gateway is Preparing. It changes to Normal in about two minutes. When it changes to Normal, it indicates that the VPN Gateway is ready to use.

    **Note:** It usually takes 1 to 5 minutes to create a VPN Gateway.


## Step 2: Create two customer gateways {#section_upz_wmz_wdb .section}

Create two customer gateways and register the two public IP addresses of the local gateways to the customer gateways to create IPsec-VPN connections. To do so, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **Customer Gateways**.
2.  Select a region.
3.  On the Customer Gateways page, click **Create Customer Gateway**.
4.  Configure the customer gateway according to the following information:
    -    **Name**: Enter the name of the customer gateway.
    -    **IP Address**: Enter the public IP address of the local gateway.
    -    **Description**: Enter a description of the customer gateway.
5.  On the Create Customer Gateway page, click **+ Add** to add multiple customer gateways.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136913/156163056441711_en-US.png)


## Step 3: Create two IPsec-VPN connections {#section_ty2_jnz_wdb .section}

Create two IPsec-VPN connections to connect the VPN Gateway with the two customer gateways. To do so, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.
2.  Select a region.
3.  On the IPsec Connections page, click **Create IPsec Connection**.
4.  Configure the IPsec-VPN connection according to the following information and click **OK**.
    -    **Name**: Enter the name of the IPsec-VPN connection.
    -    **VPN Gateway**: Select the created VPN Gateway.
    -    **Customer Gateway**: Select the created customer gateway.
    -    **Local Network**: Enter the IP address range of the VPC to which the selected VPN Gateway belongs.
    -    **Destination CIDR Block**: Enter the CIDR block of the local data center.
    -    **Effective Immediately**: Select whether to start the negotiation immediately.
        -   Yes: Start the negotiation immediately once the configuration is complete.
        -   No: Start the negotiation only when traffic is detected in the tunnel.
    -    **Pre-Shared Key**: Enter a pre-shared key. This value must be the same as the one configured in the local gateway.
    -    **Health Check**: Enable health checks and enter the destination IP address, source IP address, retry interval, and number of retries.

        Use the default configurations for other parameters.

5.  Repeat the preceding steps to create an IPsec-VPN connection for the other customer gateway.

## Step 4: Configure the local gateway {#section_ptn_44z_wdb .section}

To configure the local gateway, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.
2.  Select the target region.
3.  Find the target IPsec-VPN connection and click **Download Configuration**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136913/156163056441714_en-US.png)

4.  Configure the local gateways by loading the downloaded IPsec-VPN connection configurations to the local gateway device. For more information, see [Local gateway configuration](../reseller.en-US/User Guide/Configure IPsec-VPN connections/Configure local gateways/Configure an IPsec-VPN connection through a USG series Next-Generation Firewall device (Huawei).md#).

    The RemoteSubnet and LocalSubnet in the downloaded configurations are the converse in the actual operations of the local network and the remote network you configured when you create the IPsec-VPN connection. From the perspective of VPN Gateway, the remote network is the local IDC and the local network is the VPC. However, from the perspective of the local gateway, LocalSubnet is the CIDR block of the on-premises data center and RemoteSubnet is the CIDR block of the VPC.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136913/156163056441715_en-US.png)


## Step 5: Configure the VPN Gateway route {#section_jhd_yfa_nyk .section}

To configure a route for the VPN Gateway, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.
2.  On the VPN Gateways page, select the region of the VPN Gateway.
3.  Find the target VPN Gateway, and click the instance ID in the Instance ID/Name column.
4.  On the Destination-based Routing tab page, click **Add Route Entry**.
5.  Configure the route entry according to the following information and then click **OK**.

    -    **Destination CIDR Block**: Enter the private CIDR block of the local gateway.
    -    **Next Hop**: Select the target IPsec-VPN connection instance.
    -    **Publish to VPC**: Select whether to publish the new route to the VPC route table.
    -    **Weight**: Select a weight.
    The routes used in this example are as follows:

    |CIDR Block|Next Hop|Publish to VPC|Weight|
    |:---------|:-------|--------------|------|
    |The private CIDR block of the local gateway|IPsec-VPN connection instance 1|Yes|100|
    |The private CIDR block of the local gateway|IPsec-VPN connection instance 2|Yes|0|


