# Establish a connection between a VPC and an on-premises data center {#concept_c4h_slz_wdb .concept}

This topic describes how to create an IPsec-VPN connection between a VPC and an on-premises data center.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13351/15675809673312_en-US.png)

## Prerequisites {#section_q3w_ylz_wdb .section}

Before you use the IPsec-VPN function to create a VPN connection between a VPC and an on-premises data center, make sure that the following conditions are met:

-   The gateway device of the on-premises data center is normal. Alibaba Cloud VPN Gateway supports standard IKEv1 and IKEv2 protocols. Devices that support these two protocols can connect to Alibaba Cloud VPN Gateway, including devices of Huawei, H3C, Hillstone, SANGFOR, Cisco ASA, Juniper, SonicWall, Nokia, IBM, Ixia, and more.
-   A static public IP address is configured for the gateway device of the on-premises data center.
-   The CIDR blocks of the on-premises data center and the VPC to be connected do not conflict with each other.

## Step 1: Create a VPN Gateway {#section_vfk_2mz_wdb .section}

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


## Step 2: Create a customer gateway {#section_upz_wmz_wdb .section}

To create a customer gateway, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **Customer Gateways**.
2.  Select a region.
3.  On the Customer Gateways page, click **Create Customer Gateway**.
4.  On the Create Customer Gateway page, configure the customer gateway according to the following information, and click **OK**.
    -   **Name**: Enter a customer gateway name.
    -   **IP Address**: Enter the public IP address of the local gateway.
    -   **Description**: Enter a description of the customer gateway.

## Step 3: Create an IPsec-VPN connection {#section_ty2_jnz_wdb .section}

To create an IPsec-VPN connection, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.
2.  Select a region.
3.  On the IPsec Connections page, click **Create IPsec Connection**.
4.  On the Create IPsec Connection page, configure the IPsec-VPN connection according to the following information and click **OK**.
    -   **Name**: Enter a name for the IPsec-VPN connection.
    -   **VPN Gateway**: Select the created VPN Gateway.
    -   **Customer Gateway**: Select the created customer gateway.
    -   **Local Network**: Enter the IP address range of the VPC to which the selected VPN Gateway belongs.
    -   **Destination CIDR Block**: Enter the CIDR block of the local data center.
    -   **Effective Immediately**: Select whether to start the negotiation immediately.
        -   Yes: Start the negotiation immediately once the configuration is complete.
        -   No: Start the negotiation only when traffic is detected in the tunnel.
    -   **Pre-Shared Key**: Enter a pre-shared key. This value must be the same as the one configured in the local gateway.

        Use the default configurations for other options.


## Step 4: Configure the local gateway {#section_ptn_44z_wdb .section}

To configure the local gateway, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.
2.  Select a region.
3.  On the IPsec Connections page, find the target IPsec-VPN connection, and click **Download Configuration** in the **Actions** column.
4.  Configure the local gateway accordingly. For more information, see [Local gateway configuration](../../../../reseller.en-US/User Guide/Configure IPsec-VPN connections/Configure local gateways/Configure an IPsec-VPN connection through a USG series Next-Generation Firewall device (Huawei).md#).

    The items RemoteSubnet and LocalSubnet in the downloaded configurations operate converse to the setup of the local network and the remote network you configured when you create the IPsec-VPN connection. From the perspective of VPN Gateway, the remote network is the local IDC and the local network is the VPC. However, from the perspective of the local gateway, LocalSubnet is the CIDR block of the on-premises data center and RemoteSubnet is the CIDR block of the VPC.


## Step 5: Configure a route for the VPN Gateway {#section_tfw_9lp_avu .section}

To configure a route of the VPN Gateway, follow these steps:

1.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.
2.  Select the region of the target VPN Gateway.
3.  On the VPN Gateways page, find the target VPN Gateway and click the instance ID in the Instance ID/Name column.
4.  On the Destination-based Routing page, click **Add Route Entry**.
5.  On the Add Route Entry page, configure a destination-based route according to the following information, and click **OK**.
    -   **Destination CIDR Block**: Enter the private CIDR block of the on-premises data center.
    -   **Next Hop**: Select the target IPsec-VPN connection instance.
    -   **Publish to VPC**: Select whether to publish the new route to the VPC route table. In this example, select Yes.
    -   **Weight**: Select a weight. In this tutorial, select 100.

## Step 6: Test the connection {#section_ojw_ylz_wdb .section}

Log on to an ECS instance \(without a public IP address\) in the connected VPC. Use the ping command to ping the private IP address of a server in the on-premises data center to check whether the connection is established.

