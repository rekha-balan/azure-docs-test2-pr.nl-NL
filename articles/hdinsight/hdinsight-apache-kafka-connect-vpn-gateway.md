---
title: Connect to Kafka on HDInsight using virtual networks - Azure | Microsoft Docs
description: Learn how to remotely connect to Kafka on HDInsight using the kafka-python client. The configuration in this document uses HDInsight inside an Azure Virtual Network. The remote client connects to the virtual network through a point-to-site VPN gateway.
services: hdinsight
documentationCenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: ''
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/18/2017
ms.author: larryfr
ms.openlocfilehash: e1d01e1d094d30cd6dc77f8d4fee8f5a4f06c376
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555192"
---
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="2a0f4-105">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="2a0f4-105">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="2a0f4-106">Learn how to connect to Kafka on HDInsight using Azure Virtual Networks.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-106">Learn how to connect to Kafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="2a0f4-107">Kafka clients (producers and consumers) can run either directly on HDInsight or on remote systems.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-107">Kafka clients (producers and consumers) can run either directly on HDInsight or on remote systems.</span></span> <span data-ttu-id="2a0f4-108">Remote clients must connect to Kafka on HDInsight through an Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-108">Remote clients must connect to Kafka on HDInsight through an Azure Virtual Network.</span></span> <span data-ttu-id="2a0f4-109">Use the information in this document to understand how remote clients can connect to HDInsight by using Azure Virtual Networks.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-109">Use the information in this document to understand how remote clients can connect to HDInsight by using Azure Virtual Networks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a0f4-110">Several of the configurations discussed in this document can be used with Windows, macOS, or Linux clients.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-110">Several of the configurations discussed in this document can be used with Windows, macOS, or Linux clients.</span></span> <span data-ttu-id="2a0f4-111">However the included point-to-site example only provides a VPN client for Windows.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-111">However the included point-to-site example only provides a VPN client for Windows.</span></span>
>
> <span data-ttu-id="2a0f4-112">The example also uses a Python client ([kafka-python](http://kafka-python.readthedocs.io/en/master/)) to verify communication with Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-112">The example also uses a Python client ([kafka-python](http://kafka-python.readthedocs.io/en/master/)) to verify communication with Kafka on HDInsight.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="2a0f4-113">Architecture and planning</span><span class="sxs-lookup"><span data-stu-id="2a0f4-113">Architecture and planning</span></span>

<span data-ttu-id="2a0f4-114">HDInsight clusters are secured inside an Azure Virtual Network, and only allow incoming SSH and HTTPS traffic.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-114">HDInsight clusters are secured inside an Azure Virtual Network, and only allow incoming SSH and HTTPS traffic.</span></span> <span data-ttu-id="2a0f4-115">Traffic arrives through a public gateway, which does not route traffic from Kafka clients.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-115">Traffic arrives through a public gateway, which does not route traffic from Kafka clients.</span></span> <span data-ttu-id="2a0f4-116">To access Kafka from a remote client, you must create an Azure Virtual Network that provides a virtual private network (VPN) gateway.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-116">To access Kafka from a remote client, you must create an Azure Virtual Network that provides a virtual private network (VPN) gateway.</span></span> <span data-ttu-id="2a0f4-117">Once you have configured the virtual network and gateway, install HDInsight into the virtual network and connect to it using the VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-117">Once you have configured the virtual network and gateway, install HDInsight into the virtual network and connect to it using the VPN gateway.</span></span>

![A diagram of HDInsight inside an Azure Virtual Network with a client connected over VPN](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-connect-vpn-gateway/hdinsight-in-virtual-network.png)

<span data-ttu-id="2a0f4-119">The following list contains information on the process of using Kafka on HDInsight with a virtual network:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-119">The following list contains information on the process of using Kafka on HDInsight with a virtual network:</span></span>

1. <span data-ttu-id="2a0f4-120">Create a virtual network.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-120">Create a virtual network.</span></span> <span data-ttu-id="2a0f4-121">For specific information on using HDInsight with Azure Virtual Networks, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-121">For specific information on using HDInsight with Azure Virtual Networks, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

2. <span data-ttu-id="2a0f4-122">(Optional) Create an Azure Virtual Machine inside the virtual network and install a custom DNS server on it.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-122">(Optional) Create an Azure Virtual Machine inside the virtual network and install a custom DNS server on it.</span></span> <span data-ttu-id="2a0f4-123">This DNS server is used to enable name resolution for remote clients in a site-to-site or vnet-to-vnet configuration.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-123">This DNS server is used to enable name resolution for remote clients in a site-to-site or vnet-to-vnet configuration.</span></span> <span data-ttu-id="2a0f4-124">For more information, see the [Name resolution for VMs and cloud services](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-124">For more information, see the [Name resolution for VMs and cloud services](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

3. <span data-ttu-id="2a0f4-125">Create a VPN Gateway for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-125">Create a VPN Gateway for the virtual network.</span></span> <span data-ttu-id="2a0f4-126">For more information on VPN gateway configurations, see the [About VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) document.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-126">For more information on VPN gateway configurations, see the [About VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) document.</span></span>

4. <span data-ttu-id="2a0f4-127">Create HDInsight inside the virtual network.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-127">Create HDInsight inside the virtual network.</span></span> <span data-ttu-id="2a0f4-128">If you configured a custom DNS server for the network, HDInsight is automatically configured to use it.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-128">If you configured a custom DNS server for the network, HDInsight is automatically configured to use it.</span></span>

5. <span data-ttu-id="2a0f4-129">(Optional) If you did not use a custom DNS server, and do not have name resolution between clients and the virtual network, you must configure Kafka for IP advertising.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-129">(Optional) If you did not use a custom DNS server, and do not have name resolution between clients and the virtual network, you must configure Kafka for IP advertising.</span></span> <span data-ttu-id="2a0f4-130">For more information, see the [Configure Kafka for IP advertising](#configure-kafka-for-ip-advertising) section of this document.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-130">For more information, see the [Configure Kafka for IP advertising](#configure-kafka-for-ip-advertising) section of this document.</span></span>

## <a name="create-using-powershell"></a><span data-ttu-id="2a0f4-131">Create: Using PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a0f4-131">Create: Using PowerShell</span></span>

<span data-ttu-id="2a0f4-132">The steps in this section create the following configuration using [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/):</span><span class="sxs-lookup"><span data-stu-id="2a0f4-132">The steps in this section create the following configuration using [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/):</span></span>

* <span data-ttu-id="2a0f4-133">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="2a0f4-133">Azure Virtual Network</span></span>
* <span data-ttu-id="2a0f4-134">Point-to-site VPN gateway</span><span class="sxs-lookup"><span data-stu-id="2a0f4-134">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="2a0f4-135">Azure Storage Account (used by HDInsight)</span><span class="sxs-lookup"><span data-stu-id="2a0f4-135">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="2a0f4-136">Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a0f4-136">Kafka on HDInsight</span></span>

1. <span data-ttu-id="2a0f4-137">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document to create the certificates needed for the gateway.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-137">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document to create the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="2a0f4-138">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-138">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="2a0f4-139">Use the following code to create variables that contain configuration information:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-139">Use the following code to create variables that contain configuration information:</span></span>

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
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. <span data-ttu-id="2a0f4-140">Use the following code to create the Azure resource group and virtual network:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-140">Use the following code to create the Azure resource group and virtual network:</span></span>

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
    > <span data-ttu-id="2a0f4-141">It can take several minutes for this process to complete.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-141">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="2a0f4-142">Use the following code to create the Azure Storage Account and blob container:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-142">Use the following code to create the Azure Storage Account and blob container:</span></span>

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

6. <span data-ttu-id="2a0f4-143">Use the following code to create the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-143">Use the following code to create the HDInsight cluster:</span></span>

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
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > <span data-ttu-id="2a0f4-144">This process takes around 20 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-144">This process takes around 20 minutes to complete.</span></span>

8. <span data-ttu-id="2a0f4-145">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-145">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="2a0f4-146">To download the Windows VPN client, use the returned URI in your web browser.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-146">To download the Windows VPN client, use the returned URI in your web browser.</span></span>

## <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="2a0f4-147">Configure Kafka for IP advertising</span><span class="sxs-lookup"><span data-stu-id="2a0f4-147">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="2a0f4-148">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-148">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="2a0f4-149">This configuration does not work for the VPN client, as it cannot use name resolution for entities in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-149">This configuration does not work for the VPN client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="2a0f4-150">Use the following steps to configure Kafka on HDInsight to advertise IP addresses instead of domain names:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-150">Use the following steps to configure Kafka on HDInsight to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="2a0f4-151">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-151">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="2a0f4-152">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-152">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="2a0f4-153">When prompted, use the HTTPS user name and password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-153">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="2a0f4-154">The Ambari Web UI for the cluster is displayed.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-154">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="2a0f4-155">To view information on Kafka, select __Kafka__ from the list on the left.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-155">To view information on Kafka, select __Kafka__ from the list on the left.</span></span> 

    ![Service list with Kafka highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="2a0f4-157">To view Kafka configuration, select __Configs__ from the top middle.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-157">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Configs links for Kafka](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="2a0f4-159">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-159">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Kafka configuration, for kafka-env](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="2a0f4-161">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-161">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="2a0f4-162">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-162">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="2a0f4-163">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:92092`.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-163">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:92092`.</span></span>

8. <span data-ttu-id="2a0f4-164">To save the configuration changes, use the __Save__ button.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-164">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="2a0f4-165">Enter a text message describing the changes.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-165">Enter a text message describing the changes.</span></span> <span data-ttu-id="2a0f4-166">Select __OK__ once the changes have been saved.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-166">Select __OK__ once the changes have been saved.</span></span>

    ![Save configuration button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="2a0f4-168">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-168">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="2a0f4-169">Select OK to complete this operation.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-169">Select OK to complete this operation.</span></span>

    ![Service actions, with turn on maintenance highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="2a0f4-171">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-171">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="2a0f4-172">Confirm the restart, and then use the __OK__ button after the operation has completed.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-172">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![Restart button with restart all affected highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="2a0f4-174">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-174">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="2a0f4-175">Select **OK** to complete this operation.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-175">Select **OK** to complete this operation.</span></span>

## <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="2a0f4-176">Connect to the VPN gateway</span><span class="sxs-lookup"><span data-stu-id="2a0f4-176">Connect to the VPN gateway</span></span>

<span data-ttu-id="2a0f4-177">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#a-nameconnectapart-7---connect-to-azure) document.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-177">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#a-nameconnectapart-7---connect-to-azure) document.</span></span>

## <a name="remote-kafka-client"></a><span data-ttu-id="2a0f4-178">Remote Kafka client</span><span class="sxs-lookup"><span data-stu-id="2a0f4-178">Remote Kafka client</span></span>

<span data-ttu-id="2a0f4-179">To connect to Kafka from the client machine, you must use the IP address of the Kafka brokers or Zookeeper nodes (whichever your client requires).</span><span class="sxs-lookup"><span data-stu-id="2a0f4-179">To connect to Kafka from the client machine, you must use the IP address of the Kafka brokers or Zookeeper nodes (whichever your client requires).</span></span> <span data-ttu-id="2a0f4-180">Use the following steps to retrieve the IP address of the Kafka brokers and then use them from a Python application</span><span class="sxs-lookup"><span data-stu-id="2a0f4-180">Use the following steps to retrieve the IP address of the Kafka brokers and then use them from a Python application</span></span>

1. <span data-ttu-id="2a0f4-181">Use the following script to retrieve the IP addresses of the nodes in the cluster:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-181">Use the following script to retrieve the IP addresses of the nodes in the cluster:</span></span>

    ```powershell
    # Get the NICs for the HDInsight workernodes (names contain 'workernode').
    $nodes = Get-AzureRmNetworkInterface `
        -ResourceGroupName $resourceGroupName `
        | where-object {$_.Name -like "*workernode*"}

    # Loop through each node and get the IP address
    foreach($node in $nodes) {
        $node.IpConfigurations.PrivateIpAddress
    }
    ```

    <span data-ttu-id="2a0f4-182">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-182">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span> <span data-ttu-id="2a0f4-183">The output of the script is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-183">The output of the script is similar to the following text:</span></span>

        10.0.0.12
        10.0.0.6
        10.0.0.13
        10.0.0.5

    > [!NOTE]
    > <span data-ttu-id="2a0f4-184">If your Kafka client uses Zookeeper nodes instead of Kafka brokers, replace `*workernode*` with `*zookeepernode*` in the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-184">If your Kafka client uses Zookeeper nodes instead of Kafka brokers, replace `*workernode*` with `*zookeepernode*` in the PowerShell script.</span></span>

    > [!WARNING]
    > <span data-ttu-id="2a0f4-185">If you scale the cluster, or nodes fail and are replaced, the IP addresses may change.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-185">If you scale the cluster, or nodes fail and are replaced, the IP addresses may change.</span></span> <span data-ttu-id="2a0f4-186">There is currently no way to pre-assign specific IP addresses for nodes in an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-186">There is currently no way to pre-assign specific IP addresses for nodes in an HDInsight cluster.</span></span>

2. <span data-ttu-id="2a0f4-187">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-187">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="2a0f4-188">To send data to Kafka, use the following Python code:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-188">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  producer = KafkaProducer(bootstrap_servers=['ip_address1','ip_address2','ip_adderess3','ip_address4'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="2a0f4-189">Replace the `'ip_address'` entries with the addresses returned from step 1 in this section.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-189">Replace the `'ip_address'` entries with the addresses returned from step 1 in this section.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="2a0f4-190">This code sends the string `test message` to the topic `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-190">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="2a0f4-191">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-191">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="2a0f4-192">To retrieve the messages from Kafka, use the following Python code:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-192">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['ip_address1','ip_address2','ip_adderess3','ip_address4'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="2a0f4-193">Replace the `'ip_address'` entries with the addresses returned from step 1 in this section.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-193">Replace the `'ip_address'` entries with the addresses returned from step 1 in this section.</span></span> <span data-ttu-id="2a0f4-194">The output contains the test message sent to the producer in the previous step.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-194">The output contains the test message sent to the producer in the previous step.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2a0f4-195">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="2a0f4-195">Troubleshooting</span></span>

<span data-ttu-id="2a0f4-196">If you have problems connecting to the virtual network, or connecting to HDInsight through the network, see the [Troubleshoot virtual network gateway and connections](../network-watcher/network-watcher-troubleshoot-manage-powershell.md) document for guidance.</span><span class="sxs-lookup"><span data-stu-id="2a0f4-196">If you have problems connecting to the virtual network, or connecting to HDInsight through the network, see the [Troubleshoot virtual network gateway and connections](../network-watcher/network-watcher-troubleshoot-manage-powershell.md) document for guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a0f4-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a0f4-197">Next steps</span></span>

<span data-ttu-id="2a0f4-198">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-198">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="2a0f4-199">Configure a Point-to-Site connection using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2a0f4-199">Configure a Point-to-Site connection using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="2a0f4-200">Configure a Point-to-Site connection using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a0f4-200">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="2a0f4-201">For more information on working with Kafka on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="2a0f4-201">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="2a0f4-202">Get started with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a0f4-202">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="2a0f4-203">Use mirroring with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a0f4-203">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)







