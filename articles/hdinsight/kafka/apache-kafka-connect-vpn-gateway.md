---
title: Connect to Kafka using virtual networks - Azure HDInsight
description: Learn how to directly connect to Kafka on HDInsight through an Azure Virtual Network. Learn how to connect to Kafka from development clients using a VPN gateway, or from clients in your on-premises network by using a VPN gateway device.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/02/2018
ms.openlocfilehash: 973563a0c9a986bb4dec785b4521566acb657d15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857031"
---
# <a name="connect-to-kafka-on-hdinsight-through-an-azure-virtual-network"></a><span data-ttu-id="8764b-104">Connect to Kafka on HDInsight through an Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="8764b-104">Connect to Kafka on HDInsight through an Azure Virtual Network</span></span>

<span data-ttu-id="8764b-105">Learn how to directly connect to Kafka on HDInsight through an Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="8764b-105">Learn how to directly connect to Kafka on HDInsight through an Azure Virtual Network.</span></span> <span data-ttu-id="8764b-106">This document provides information on connecting to Kafka using the following configurations:</span><span class="sxs-lookup"><span data-stu-id="8764b-106">This document provides information on connecting to Kafka using the following configurations:</span></span>

* <span data-ttu-id="8764b-107">From resources in an on-premises network.</span><span class="sxs-lookup"><span data-stu-id="8764b-107">From resources in an on-premises network.</span></span> <span data-ttu-id="8764b-108">This connection is established by using a VPN device (software or hardware) on your local network.</span><span class="sxs-lookup"><span data-stu-id="8764b-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="8764b-109">From a development environment using a VPN software client.</span><span class="sxs-lookup"><span data-stu-id="8764b-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="8764b-110">Architecture and planning</span><span class="sxs-lookup"><span data-stu-id="8764b-110">Architecture and planning</span></span>

<span data-ttu-id="8764b-111">HDInsight does not allow direct connection to Kafka over the public internet.</span><span class="sxs-lookup"><span data-stu-id="8764b-111">HDInsight does not allow direct connection to Kafka over the public internet.</span></span> <span data-ttu-id="8764b-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span><span class="sxs-lookup"><span data-stu-id="8764b-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span></span>

* <span data-ttu-id="8764b-113">Run the client in the same virtual network as Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8764b-113">Run the client in the same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="8764b-114">This configuration is used in the [Start with Apache Kafka on HDInsight](apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="8764b-114">This configuration is used in the [Start with Apache Kafka on HDInsight](apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="8764b-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span><span class="sxs-lookup"><span data-stu-id="8764b-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span></span>

* <span data-ttu-id="8764b-116">Connect a private network, such as your on-premises network, to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="8764b-116">Connect a private network, such as your on-premises network, to the virtual network.</span></span> <span data-ttu-id="8764b-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span><span class="sxs-lookup"><span data-stu-id="8764b-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span></span> <span data-ttu-id="8764b-118">To enable this configuration, perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8764b-118">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="8764b-119">Create a virtual network.</span><span class="sxs-lookup"><span data-stu-id="8764b-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="8764b-120">Create a VPN gateway that uses a site-to-site configuration.</span><span class="sxs-lookup"><span data-stu-id="8764b-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="8764b-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="8764b-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="8764b-122">Create a DNS server in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="8764b-122">Create a DNS server in the virtual network.</span></span>
    4. <span data-ttu-id="8764b-123">Configure forwarding between the DNS server in each network.</span><span class="sxs-lookup"><span data-stu-id="8764b-123">Configure forwarding between the DNS server in each network.</span></span>
    5. <span data-ttu-id="8764b-124">Install Kafka on HDInsight into the virtual network.</span><span class="sxs-lookup"><span data-stu-id="8764b-124">Install Kafka on HDInsight into the virtual network.</span></span>

    <span data-ttu-id="8764b-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span><span class="sxs-lookup"><span data-stu-id="8764b-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="8764b-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span><span class="sxs-lookup"><span data-stu-id="8764b-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="8764b-127">To enable this configuration, perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8764b-127">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="8764b-128">Create a virtual network.</span><span class="sxs-lookup"><span data-stu-id="8764b-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="8764b-129">Create a VPN gateway that uses a point-to-site configuration.</span><span class="sxs-lookup"><span data-stu-id="8764b-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="8764b-130">This configuration can be used with both Windows and MacOS clients.</span><span class="sxs-lookup"><span data-stu-id="8764b-130">This configuration can be used with both Windows and MacOS clients.</span></span>
    3. <span data-ttu-id="8764b-131">Install Kafka on HDInsight into the virtual network.</span><span class="sxs-lookup"><span data-stu-id="8764b-131">Install Kafka on HDInsight into the virtual network.</span></span>
    4. <span data-ttu-id="8764b-132">Configure Kafka for IP advertising.</span><span class="sxs-lookup"><span data-stu-id="8764b-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="8764b-133">This configuration allows the client to connect using IP addressing instead of domain names.</span><span class="sxs-lookup"><span data-stu-id="8764b-133">This configuration allows the client to connect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="8764b-134">Download and use the VPN client on the development system.</span><span class="sxs-lookup"><span data-stu-id="8764b-134">Download and use the VPN client on the development system.</span></span>

    <span data-ttu-id="8764b-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span><span class="sxs-lookup"><span data-stu-id="8764b-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="8764b-136">This configuration is only recommended for development purposes because of the following limitations:</span><span class="sxs-lookup"><span data-stu-id="8764b-136">This configuration is only recommended for development purposes because of the following limitations:</span></span>
    >
    > * <span data-ttu-id="8764b-137">Each client must connect using a VPN software client.</span><span class="sxs-lookup"><span data-stu-id="8764b-137">Each client must connect using a VPN software client.</span></span>
    > * <span data-ttu-id="8764b-138">The VPN client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span><span class="sxs-lookup"><span data-stu-id="8764b-138">The VPN client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span></span> <span data-ttu-id="8764b-139">IP communication requires additional configuration on the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="8764b-139">IP communication requires additional configuration on the Kafka cluster.</span></span>

<span data-ttu-id="8764b-140">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](../hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="8764b-140">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](../hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <a id="on-premises"></a> <span data-ttu-id="8764b-141">Connect to Kafka from an on-premises network</span><span class="sxs-lookup"><span data-stu-id="8764b-141">Connect to Kafka from an on-premises network</span></span>

<span data-ttu-id="8764b-142">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./../connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="8764b-142">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./../connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8764b-143">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span><span class="sxs-lookup"><span data-stu-id="8764b-143">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span></span>

<span data-ttu-id="8764b-144">These steps create the following configuration:</span><span class="sxs-lookup"><span data-stu-id="8764b-144">These steps create the following configuration:</span></span>

* <span data-ttu-id="8764b-145">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="8764b-145">Azure Virtual Network</span></span>
* <span data-ttu-id="8764b-146">Site-to-site VPN gateway</span><span class="sxs-lookup"><span data-stu-id="8764b-146">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="8764b-147">Azure Storage account (used by HDInsight)</span><span class="sxs-lookup"><span data-stu-id="8764b-147">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="8764b-148">Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8764b-148">Kafka on HDInsight</span></span>

<span data-ttu-id="8764b-149">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span><span class="sxs-lookup"><span data-stu-id="8764b-149">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span></span>

## <a id="vpnclient"></a> <span data-ttu-id="8764b-150">Connect to Kafka with a VPN client</span><span class="sxs-lookup"><span data-stu-id="8764b-150">Connect to Kafka with a VPN client</span></span>

<span data-ttu-id="8764b-151">Use the steps in this section to create the following configuration:</span><span class="sxs-lookup"><span data-stu-id="8764b-151">Use the steps in this section to create the following configuration:</span></span>

* <span data-ttu-id="8764b-152">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="8764b-152">Azure Virtual Network</span></span>
* <span data-ttu-id="8764b-153">Point-to-site VPN gateway</span><span class="sxs-lookup"><span data-stu-id="8764b-153">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="8764b-154">Azure Storage Account (used by HDInsight)</span><span class="sxs-lookup"><span data-stu-id="8764b-154">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="8764b-155">Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8764b-155">Kafka on HDInsight</span></span>

1. <span data-ttu-id="8764b-156">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span><span class="sxs-lookup"><span data-stu-id="8764b-156">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="8764b-157">This document creates the certificates needed for the gateway.</span><span class="sxs-lookup"><span data-stu-id="8764b-157">This document creates the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="8764b-158">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="8764b-158">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Connect-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="8764b-159">Use the following code to create variables that contain configuration information:</span><span class="sxs-lookup"><span data-stu-id="8764b-159">Use the following code to create variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is the resource group name?"
    $baseName = Read-Host "What is the base name? It is used to create names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want to create the resources in?"
    $rootCert = Read-Host "What is the file path to the root certificate? It is used to secure the VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter the HTTPS user name and password for the HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter the SSH user name and password for the HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.6"
    $hdiType = "Kafka"
    ```

4. <span data-ttu-id="8764b-160">Use the following code to create the Azure resource group and virtual network:</span><span class="sxs-lookup"><span data-stu-id="8764b-160">Use the following code to create the Azure resource group and virtual network:</span></span>

    ```powershell
    # Create the resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create the subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get the network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for the gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get the certificate info
    # Get the full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create the VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > <span data-ttu-id="8764b-161">It can take several minutes for this process to complete.</span><span class="sxs-lookup"><span data-stu-id="8764b-161">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="8764b-162">Use the following code to create the Azure Storage Account and blob container:</span><span class="sxs-lookup"><span data-stu-id="8764b-162">Use the following code to create the Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create the storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get the storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create the default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="8764b-163">Use the following code to create the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="8764b-163">Use the following code to create the HDInsight cluster:</span></span>

    ```powershell
    # Create the HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -DisksPerWorkerNode 2 `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > <span data-ttu-id="8764b-164">This process takes around 15 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="8764b-164">This process takes around 15 minutes to complete.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="8764b-165">Configure Kafka for IP advertising</span><span class="sxs-lookup"><span data-stu-id="8764b-165">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="8764b-166">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span><span class="sxs-lookup"><span data-stu-id="8764b-166">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="8764b-167">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="8764b-167">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="8764b-168">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span><span class="sxs-lookup"><span data-stu-id="8764b-168">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="8764b-169">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="8764b-169">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="8764b-170">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="8764b-170">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="8764b-171">When prompted, use the HTTPS user name and password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="8764b-171">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="8764b-172">The Ambari Web UI for the cluster is displayed.</span><span class="sxs-lookup"><span data-stu-id="8764b-172">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="8764b-173">To view information on Kafka, select __Kafka__ from the list on the left.</span><span class="sxs-lookup"><span data-stu-id="8764b-173">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![Service list with Kafka highlighted](./media/apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="8764b-175">To view Kafka configuration, select __Configs__ from the top middle.</span><span class="sxs-lookup"><span data-stu-id="8764b-175">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Configs links for Kafka](./media/apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="8764b-177">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span><span class="sxs-lookup"><span data-stu-id="8764b-177">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Kafka configuration, for kafka-env](./media/apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="8764b-179">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span><span class="sxs-lookup"><span data-stu-id="8764b-179">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="8764b-180">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span><span class="sxs-lookup"><span data-stu-id="8764b-180">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="8764b-181">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="8764b-181">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="8764b-182">To save the configuration changes, use the __Save__ button.</span><span class="sxs-lookup"><span data-stu-id="8764b-182">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="8764b-183">Enter a text message describing the changes.</span><span class="sxs-lookup"><span data-stu-id="8764b-183">Enter a text message describing the changes.</span></span> <span data-ttu-id="8764b-184">Select __OK__ once the changes have been saved.</span><span class="sxs-lookup"><span data-stu-id="8764b-184">Select __OK__ once the changes have been saved.</span></span>

    ![Save configuration button](./media/apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="8764b-186">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span><span class="sxs-lookup"><span data-stu-id="8764b-186">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="8764b-187">Select OK to complete this operation.</span><span class="sxs-lookup"><span data-stu-id="8764b-187">Select OK to complete this operation.</span></span>

    ![Service actions, with turn on maintenance highlighted](./media/apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="8764b-189">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span><span class="sxs-lookup"><span data-stu-id="8764b-189">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="8764b-190">Confirm the restart, and then use the __OK__ button after the operation has completed.</span><span class="sxs-lookup"><span data-stu-id="8764b-190">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![Restart button with restart all affected highlighted](./media/apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="8764b-192">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span><span class="sxs-lookup"><span data-stu-id="8764b-192">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="8764b-193">Select **OK** to complete this operation.</span><span class="sxs-lookup"><span data-stu-id="8764b-193">Select **OK** to complete this operation.</span></span>

### <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="8764b-194">Connect to the VPN gateway</span><span class="sxs-lookup"><span data-stu-id="8764b-194">Connect to the VPN gateway</span></span>

<span data-ttu-id="8764b-195">To connect to the VPN gateway, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#connect) document.</span><span class="sxs-lookup"><span data-stu-id="8764b-195">To connect to the VPN gateway, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#connect) document.</span></span>

## <a id="python-client"></a> <span data-ttu-id="8764b-196">Example: Python client</span><span class="sxs-lookup"><span data-stu-id="8764b-196">Example: Python client</span></span>

<span data-ttu-id="8764b-197">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span><span class="sxs-lookup"><span data-stu-id="8764b-197">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="8764b-198">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span><span class="sxs-lookup"><span data-stu-id="8764b-198">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="8764b-199">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span><span class="sxs-lookup"><span data-stu-id="8764b-199">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span>

    <span data-ttu-id="8764b-200">Save the returned information for use in the next steps.</span><span class="sxs-lookup"><span data-stu-id="8764b-200">Save the returned information for use in the next steps.</span></span>

2. <span data-ttu-id="8764b-201">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span><span class="sxs-lookup"><span data-stu-id="8764b-201">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="8764b-202">To send data to Kafka, use the following Python code:</span><span class="sxs-lookup"><span data-stu-id="8764b-202">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="8764b-203">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span><span class="sxs-lookup"><span data-stu-id="8764b-203">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="8764b-204">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span><span class="sxs-lookup"><span data-stu-id="8764b-204">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="8764b-205">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span><span class="sxs-lookup"><span data-stu-id="8764b-205">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8764b-206">This code sends the string `test message` to the topic `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="8764b-206">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="8764b-207">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="8764b-207">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="8764b-208">To retrieve the messages from Kafka, use the following Python code:</span><span class="sxs-lookup"><span data-stu-id="8764b-208">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Again, you only need one or two, not the full list.
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="8764b-209">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span><span class="sxs-lookup"><span data-stu-id="8764b-209">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="8764b-210">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span><span class="sxs-lookup"><span data-stu-id="8764b-210">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="8764b-211">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span><span class="sxs-lookup"><span data-stu-id="8764b-211">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8764b-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="8764b-212">Next steps</span></span>

<span data-ttu-id="8764b-213">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](../hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="8764b-213">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](../hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="8764b-214">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="8764b-214">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="8764b-215">Configure a Point-to-Site connection using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8764b-215">Configure a Point-to-Site connection using the Azure portal</span></span>](../../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="8764b-216">Configure a Point-to-Site connection using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8764b-216">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="8764b-217">For more information on working with Kafka on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="8764b-217">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="8764b-218">Get started with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8764b-218">Get started with Kafka on HDInsight</span></span>](apache-kafka-get-started.md)
* [<span data-ttu-id="8764b-219">Use mirroring with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8764b-219">Use mirroring with Kafka on HDInsight</span></span>](apache-kafka-mirroring.md)
