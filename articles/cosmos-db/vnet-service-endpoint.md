---
title: Secure access to an Azure Cosmos DB account by using Azure Virtual Network service endpoint | Microsoft Docs
description: This document describes steps required to setup Azure Cosmos DB virtual network service endpoint.
services: cosmos-db
author: kanshiG
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 05/07/2018
ms.author: govindk
ms.openlocfilehash: e6b263c1eb9fe3b151f0a51b5da9a92b8ced4549
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967931"
---
# <a name="secure-access-to-an-azure-cosmos-db-account-by-using-azure-virtual-network-service-endpoint"></a><span data-ttu-id="6a691-103">Secure access to an Azure Cosmos DB account by using Azure Virtual Network service endpoint</span><span class="sxs-lookup"><span data-stu-id="6a691-103">Secure access to an Azure Cosmos DB account by using Azure Virtual Network service endpoint</span></span>

<span data-ttu-id="6a691-104">Azure CosmosDB accounts can be configured to allow access only from specific subnet of Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="6a691-104">Azure CosmosDB accounts can be configured to allow access only from specific subnet of Azure Virtual Network.</span></span> <span data-ttu-id="6a691-105">By enabling a [Service Endpoint](../virtual-network/virtual-network-service-endpoints-overview.md) for Azure CosmosDB from a Virtual Network and its subnet, traffic is ensured an optimal and secure route to the Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6a691-105">By enabling a [Service Endpoint](../virtual-network/virtual-network-service-endpoints-overview.md) for Azure CosmosDB from a Virtual Network and its subnet, traffic is ensured an optimal and secure route to the Azure Cosmos DB.</span></span>  

<span data-ttu-id="6a691-106">Azure Cosmos DB is a globally distributed, multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="6a691-106">Azure Cosmos DB is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="6a691-107">You can replicate the data present in Azure Cosmos DB account to multiple regions.</span><span class="sxs-lookup"><span data-stu-id="6a691-107">You can replicate the data present in Azure Cosmos DB account to multiple regions.</span></span> <span data-ttu-id="6a691-108">When Azure Cosmos DB is configured with a virtual network service endpoint, each virtual network allows access from IPs that belong to specicifc subnet.</span><span class="sxs-lookup"><span data-stu-id="6a691-108">When Azure Cosmos DB is configured with a virtual network service endpoint, each virtual network allows access from IPs that belong to specicifc subnet.</span></span> <span data-ttu-id="6a691-109">The following image shows an illustration of an Azure Cosmos DB that has virtual network service endpoint enabled:</span><span class="sxs-lookup"><span data-stu-id="6a691-109">The following image shows an illustration of an Azure Cosmos DB that has virtual network service endpoint enabled:</span></span>

![virtual network service endpoint architecture](./media/vnet-service-endpoint/vnet-service-endpoint-architecture.png)

<span data-ttu-id="6a691-111">Once an Azure Cosmos DB account is configured with a virtual network service endpoint, it can be accessed only from the specified subnet, all public/internet access is removed.</span><span class="sxs-lookup"><span data-stu-id="6a691-111">Once an Azure Cosmos DB account is configured with a virtual network service endpoint, it can be accessed only from the specified subnet, all public/internet access is removed.</span></span> <span data-ttu-id="6a691-112">To learn in detailed about service endpoints, refer to the Azure [Virtual network service endpoints overview](../virtual-network/virtual-network-service-endpoints-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="6a691-112">To learn in detailed about service endpoints, refer to the Azure [Virtual network service endpoints overview](../virtual-network/virtual-network-service-endpoints-overview.md) article.</span></span>

> [!NOTE]
> <span data-ttu-id="6a691-113">Currently Virtual Network service endpoints can be configured for Azure Cosmos DB SQL API or Mongo API accounts.</span><span class="sxs-lookup"><span data-stu-id="6a691-113">Currently Virtual Network service endpoints can be configured for Azure Cosmos DB SQL API or Mongo API accounts.</span></span> <span data-ttu-id="6a691-114">Ability to configure service endpoints for other  APIs and sovereign clouds such as Azure Germany or Azure Government will be available soon.</span><span class="sxs-lookup"><span data-stu-id="6a691-114">Ability to configure service endpoints for other  APIs and sovereign clouds such as Azure Germany or Azure Government will be available soon.</span></span> <span data-ttu-id="6a691-115">If you have an existing IP firewall configured for your Azure Cosmos DB account, please note the firewall configuration, remove the IP firewall and then configure the service endpoint ACL.</span><span class="sxs-lookup"><span data-stu-id="6a691-115">If you have an existing IP firewall configured for your Azure Cosmos DB account, please note the firewall configuration, remove the IP firewall and then configure the service endpoint ACL.</span></span> <span data-ttu-id="6a691-116">After you configure service endpoint, you can re-enable the IP firewall if needed.</span><span class="sxs-lookup"><span data-stu-id="6a691-116">After you configure service endpoint, you can re-enable the IP firewall if needed.</span></span>

## <a name="configure-service-endpoint-by-using-azure-portal"></a><span data-ttu-id="6a691-117">Configure service endpoint by using Azure portal</span><span class="sxs-lookup"><span data-stu-id="6a691-117">Configure service endpoint by using Azure portal</span></span>
### <a name="configure-service-endpoint-for-an-existing-azure-virtual-network-and-subnet"></a><span data-ttu-id="6a691-118">Configure service endpoint for an existing Azure virtual network and subnet</span><span class="sxs-lookup"><span data-stu-id="6a691-118">Configure service endpoint for an existing Azure virtual network and subnet</span></span>

1. <span data-ttu-id="6a691-119">From **All resources** blade, find the virtual network you want to configure service endpoint for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6a691-119">From **All resources** blade, find the virtual network you want to configure service endpoint for Azure Cosmos DB.</span></span> <span data-ttu-id="6a691-120">Navigate to the **Service endpoints** blade and make sure that the subnet of the virtual network has been enabled for the "Azure.CosmosDB" service endpoint.</span><span class="sxs-lookup"><span data-stu-id="6a691-120">Navigate to the **Service endpoints** blade and make sure that the subnet of the virtual network has been enabled for the "Azure.CosmosDB" service endpoint.</span></span>  

   ![Confirm service endpoint enabled](./media/vnet-service-endpoint/confirm-service-endpoint-enabled.png)

2. <span data-ttu-id="6a691-122">From **All resources** blade, find the Azure Cosmos DB account you want to secure.</span><span class="sxs-lookup"><span data-stu-id="6a691-122">From **All resources** blade, find the Azure Cosmos DB account you want to secure.</span></span>  

3. <span data-ttu-id="6a691-123">Before enabling virtual network service endpoint, copy the IP firewall information associated with your Azure Cosmos DB account for future usage.</span><span class="sxs-lookup"><span data-stu-id="6a691-123">Before enabling virtual network service endpoint, copy the IP firewall information associated with your Azure Cosmos DB account for future usage.</span></span> <span data-ttu-id="6a691-124">You can re-enable IP firewall after configuring service endpoint.</span><span class="sxs-lookup"><span data-stu-id="6a691-124">You can re-enable IP firewall after configuring service endpoint.</span></span>  

4. <span data-ttu-id="6a691-125">Select **Firewalls and virtual networks** from settings menu and choose allow access from **Selected networks**.</span><span class="sxs-lookup"><span data-stu-id="6a691-125">Select **Firewalls and virtual networks** from settings menu and choose allow access from **Selected networks**.</span></span>  

3. <span data-ttu-id="6a691-126">To grant access to an existing virtual network's subnet, under Virtual networks, select **Add existing Azure virtual network**.</span><span class="sxs-lookup"><span data-stu-id="6a691-126">To grant access to an existing virtual network's subnet, under Virtual networks, select **Add existing Azure virtual network**.</span></span>  

4. <span data-ttu-id="6a691-127">Select the **Subscription** from which you want to add Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="6a691-127">Select the **Subscription** from which you want to add Azure virtual network.</span></span> <span data-ttu-id="6a691-128">Select the Azure **Virtual networks** and **Subnets** that you wish to provide access to your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="6a691-128">Select the Azure **Virtual networks** and **Subnets** that you wish to provide access to your Azure Cosmos DB account.</span></span> <span data-ttu-id="6a691-129">Next select **Enable** to enable selected networks with service endpoints for "Microsoft.AzureCosmosDB".</span><span class="sxs-lookup"><span data-stu-id="6a691-129">Next select **Enable** to enable selected networks with service endpoints for "Microsoft.AzureCosmosDB".</span></span> <span data-ttu-id="6a691-130">When it’s complete, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="6a691-130">When it’s complete, select **Add**.</span></span>  

   ![Select virtual network and subnet](./media/vnet-service-endpoint/choose-subnet-and-vnet.png)

   > [!NOTE]
   > <span data-ttu-id="6a691-132">If service endpoint for Azure Cosmos DB isn’t previously configured for the selected Azure virtual networks and subnets, it can be configured as a part of this operation.</span><span class="sxs-lookup"><span data-stu-id="6a691-132">If service endpoint for Azure Cosmos DB isn’t previously configured for the selected Azure virtual networks and subnets, it can be configured as a part of this operation.</span></span> <span data-ttu-id="6a691-133">Enabling access will take up to 15 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="6a691-133">Enabling access will take up to 15 minutes to complete.</span></span> <span data-ttu-id="6a691-134">It is very important to disable the IP firewall after noting down the contents of the firewall ACL for renabling them later.</span><span class="sxs-lookup"><span data-stu-id="6a691-134">It is very important to disable the IP firewall after noting down the contents of the firewall ACL for renabling them later.</span></span> 

   ![virtual network and subnet configured successfully](./media/vnet-service-endpoint/vnet-and-subnet-configured-successfully.png)

<span data-ttu-id="6a691-136">Now your Azure Cosmos DB account will only allow traffic from this chosen subnet.</span><span class="sxs-lookup"><span data-stu-id="6a691-136">Now your Azure Cosmos DB account will only allow traffic from this chosen subnet.</span></span> <span data-ttu-id="6a691-137">If you had previously enabled  IP firewall, please re-enable them by using earlier information.</span><span class="sxs-lookup"><span data-stu-id="6a691-137">If you had previously enabled  IP firewall, please re-enable them by using earlier information.</span></span>

### <a name="configure-service-endpoint-for-a-new-azure-virtual-network-and-subnet"></a><span data-ttu-id="6a691-138">Configure service endpoint for a new Azure virtual network and subnet</span><span class="sxs-lookup"><span data-stu-id="6a691-138">Configure service endpoint for a new Azure virtual network and subnet</span></span>

1. <span data-ttu-id="6a691-139">From **All resources** blade, find the Azure Cosmos DB account you want to secure.</span><span class="sxs-lookup"><span data-stu-id="6a691-139">From **All resources** blade, find the Azure Cosmos DB account you want to secure.</span></span>  

> [!NOTE]
> <span data-ttu-id="6a691-140">If you have an existing IP firewall configured for your Azure Cosmos DB account, please note the firewall configuration, remove the IP firewall and then enable the Service endpoint.</span><span class="sxs-lookup"><span data-stu-id="6a691-140">If you have an existing IP firewall configured for your Azure Cosmos DB account, please note the firewall configuration, remove the IP firewall and then enable the Service endpoint.</span></span> <span data-ttu-id="6a691-141">If you enable the Service endpoint without disbling the firewall, the traffic from that ip range will loose the virtual IP identity and it's dropped with an IP filter error message.</span><span class="sxs-lookup"><span data-stu-id="6a691-141">If you enable the Service endpoint without disbling the firewall, the traffic from that ip range will loose the virtual IP identity and it's dropped with an IP filter error message.</span></span> <span data-ttu-id="6a691-142">So to prevent this error you should always disable the firewall rules, copy them, enable service endpoint from the subnet and finally ACL the subnet from Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6a691-142">So to prevent this error you should always disable the firewall rules, copy them, enable service endpoint from the subnet and finally ACL the subnet from Cosmos DB.</span></span> <span data-ttu-id="6a691-143">After you configure service endpoint and add the ACL you can re-enable the IP firewall again if needed.</span><span class="sxs-lookup"><span data-stu-id="6a691-143">After you configure service endpoint and add the ACL you can re-enable the IP firewall again if needed.</span></span>

2. <span data-ttu-id="6a691-144">Before enabling virtual network service endpoint, copy the IP firewall information associated with your Azure Cosmos DB account for future usage.</span><span class="sxs-lookup"><span data-stu-id="6a691-144">Before enabling virtual network service endpoint, copy the IP firewall information associated with your Azure Cosmos DB account for future usage.</span></span> <span data-ttu-id="6a691-145">You can re-enable IP firewall after configuring service endpoint.</span><span class="sxs-lookup"><span data-stu-id="6a691-145">You can re-enable IP firewall after configuring service endpoint.</span></span>  

3. <span data-ttu-id="6a691-146">Select **Firewalls and Azure virtual networks** from settings menu and choose allow access from **Selected networks**.</span><span class="sxs-lookup"><span data-stu-id="6a691-146">Select **Firewalls and Azure virtual networks** from settings menu and choose allow access from **Selected networks**.</span></span>  

4. <span data-ttu-id="6a691-147">To grant access to a new Azure virtual network, under Virtual networks, select **Add new virtual network**.</span><span class="sxs-lookup"><span data-stu-id="6a691-147">To grant access to a new Azure virtual network, under Virtual networks, select **Add new virtual network**.</span></span>  

5. <span data-ttu-id="6a691-148">Provide the details required to create a new virtual network, and then select Create.</span><span class="sxs-lookup"><span data-stu-id="6a691-148">Provide the details required to create a new virtual network, and then select Create.</span></span> <span data-ttu-id="6a691-149">The subnet will be created with a service endpoint for "Microsoft.AzureCosmosDB" enabled.</span><span class="sxs-lookup"><span data-stu-id="6a691-149">The subnet will be created with a service endpoint for "Microsoft.AzureCosmosDB" enabled.</span></span>

   ![Select virtual network and subnet for new virtual network](./media/vnet-service-endpoint/choose-subnet-and-vnet-new-vnet.png)

## <a name="allow-access-from-azure-portal"></a><span data-ttu-id="6a691-151">Allow access from Azure portal</span><span class="sxs-lookup"><span data-stu-id="6a691-151">Allow access from Azure portal</span></span>

<span data-ttu-id="6a691-152">After Azure Virtual Network service endpoints are enabled for your Azure Cosmos DB database account, access from portal or other Azure services is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="6a691-152">After Azure Virtual Network service endpoints are enabled for your Azure Cosmos DB database account, access from portal or other Azure services is disabled by default.</span></span> <span data-ttu-id="6a691-153">Access to your Azure Cosmos DB database account from machines outside the configured subnet are blocked including access from portal.</span><span class="sxs-lookup"><span data-stu-id="6a691-153">Access to your Azure Cosmos DB database account from machines outside the configured subnet are blocked including access from portal.</span></span>

![Allow access from portal](./media/vnet-service-endpoint/allow-access-from-portal.png)

<span data-ttu-id="6a691-155">If your Azure Cosmos DB account is used by other Azure services like Azure Search, or accessed from Stream analytics or Power BI, you allow access by checking **Allow access to Azure Services**.</span><span class="sxs-lookup"><span data-stu-id="6a691-155">If your Azure Cosmos DB account is used by other Azure services like Azure Search, or accessed from Stream analytics or Power BI, you allow access by checking **Allow access to Azure Services**.</span></span>

<span data-ttu-id="6a691-156">To ensure you have access to Azure Cosmos DB metrics from the portal, you need to enable **Allow access to Azure portal** options.</span><span class="sxs-lookup"><span data-stu-id="6a691-156">To ensure you have access to Azure Cosmos DB metrics from the portal, you need to enable **Allow access to Azure portal** options.</span></span> <span data-ttu-id="6a691-157">To learn more about these options, see [connections from Azure portal](firewall-support.md#connections-from-the-azure-portal) and [connections from Azure PaaS services](firewall-support.md#connections-from-global-azure-datacenters-or-azure-paas-services) sections.</span><span class="sxs-lookup"><span data-stu-id="6a691-157">To learn more about these options, see [connections from Azure portal](firewall-support.md#connections-from-the-azure-portal) and [connections from Azure PaaS services](firewall-support.md#connections-from-global-azure-datacenters-or-azure-paas-services) sections.</span></span> <span data-ttu-id="6a691-158">After selecting access, select **Save** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="6a691-158">After selecting access, select **Save** to save the settings.</span></span>

## <a name="remove-a-virtual-network-or-subnet"></a><span data-ttu-id="6a691-159">Remove a virtual network or subnet</span><span class="sxs-lookup"><span data-stu-id="6a691-159">Remove a virtual network or subnet</span></span> 

1. <span data-ttu-id="6a691-160">From **All resources** blade, find the Azure Cosmos DB account for which you assigned service endpoints.</span><span class="sxs-lookup"><span data-stu-id="6a691-160">From **All resources** blade, find the Azure Cosmos DB account for which you assigned service endpoints.</span></span>  

2. <span data-ttu-id="6a691-161">Select **Firewalls and virtual networks** from settings menu.</span><span class="sxs-lookup"><span data-stu-id="6a691-161">Select **Firewalls and virtual networks** from settings menu.</span></span>  

3. <span data-ttu-id="6a691-162">To remove a virtual network or subnet rule, select "..." next to the virtual network or subnet and select **Remove**.</span><span class="sxs-lookup"><span data-stu-id="6a691-162">To remove a virtual network or subnet rule, select "..." next to the virtual network or subnet and select **Remove**.</span></span>

   ![Remove a virtual network](./media/vnet-service-endpoint/remove-a-vnet.png)

4.  <span data-ttu-id="6a691-164">Click **Save** to apply your changes.</span><span class="sxs-lookup"><span data-stu-id="6a691-164">Click **Save** to apply your changes.</span></span>

## <a name="configure-service-endpoint-by-using-azure-powershell"></a><span data-ttu-id="6a691-165">Configure Service endpoint by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a691-165">Configure Service endpoint by using Azure PowerShell</span></span> 

<span data-ttu-id="6a691-166">Use the following steps to configure Service endpoint to an Azure Cosmos DB account by using Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6a691-166">Use the following steps to configure Service endpoint to an Azure Cosmos DB account by using Azure PowerShell:</span></span>  

1. <span data-ttu-id="6a691-167">Install the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) and [Login](https://docs.microsoft.com/powershell/azure/authenticate-azureps).</span><span class="sxs-lookup"><span data-stu-id="6a691-167">Install the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) and [Login](https://docs.microsoft.com/powershell/azure/authenticate-azureps).</span></span>  <span data-ttu-id="6a691-168">Ensure you note the IP firewall settings and delete the IP firewall completely before enabling Service endpoint for the account.</span><span class="sxs-lookup"><span data-stu-id="6a691-168">Ensure you note the IP firewall settings and delete the IP firewall completely before enabling Service endpoint for the account.</span></span>


> [!NOTE]
> <span data-ttu-id="6a691-169">If you have an existing IP firewall configured for your Azure Cosmos DB account, please note the firewall configuration, remove the IP firewall and then enable the Service endpoint.</span><span class="sxs-lookup"><span data-stu-id="6a691-169">If you have an existing IP firewall configured for your Azure Cosmos DB account, please note the firewall configuration, remove the IP firewall and then enable the Service endpoint.</span></span> <span data-ttu-id="6a691-170">If you enable the Service endpoint without disbling the firewall, the traffic from that ip range will loose the virtual IP identity and it's dropped with an IP filter error message.</span><span class="sxs-lookup"><span data-stu-id="6a691-170">If you enable the Service endpoint without disbling the firewall, the traffic from that ip range will loose the virtual IP identity and it's dropped with an IP filter error message.</span></span> <span data-ttu-id="6a691-171">So to prevent this error you should always disable the firewall rules, copy them, enable service endpoint from the subnet and finally ACL the subnet from Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6a691-171">So to prevent this error you should always disable the firewall rules, copy them, enable service endpoint from the subnet and finally ACL the subnet from Cosmos DB.</span></span> <span data-ttu-id="6a691-172">After you configure service endpoint and add the ACL you can re-enable the IP firewall again if needed.</span><span class="sxs-lookup"><span data-stu-id="6a691-172">After you configure service endpoint and add the ACL you can re-enable the IP firewall again if needed.</span></span>

2. <span data-ttu-id="6a691-173">Before enabling virtual network service endpoint, copy the IP firewall information associated with your Azure Cosmos DB account for future usage.</span><span class="sxs-lookup"><span data-stu-id="6a691-173">Before enabling virtual network service endpoint, copy the IP firewall information associated with your Azure Cosmos DB account for future usage.</span></span> <span data-ttu-id="6a691-174">You will re-enable IP firewall after configuring service endpoint.</span><span class="sxs-lookup"><span data-stu-id="6a691-174">You will re-enable IP firewall after configuring service endpoint.</span></span>  

3. <span data-ttu-id="6a691-175">Enable the service endpoint for an existing subnet of a virtual network.</span><span class="sxs-lookup"><span data-stu-id="6a691-175">Enable the service endpoint for an existing subnet of a virtual network.</span></span>  

   ```powershell
   $rgname= "<Resource group name>"
   $vnName = "<virtual network name>"
   $sname = "<Subnet name>"
   $subnetPrefix = "<Subnet address range>"

   Get-AzureRmVirtualNetwork `
    -ResourceGroupName $rgname `
    -Name $vnName | Set-AzureRmVirtualNetworkSubnetConfig `
    -Name $sname  `
    -AddressPrefix $subnetPrefix `
    -ServiceEndpoint "Microsoft.AzureCosmosDB" | Set-AzureRmVirtualNetwork
   ```

4. <span data-ttu-id="6a691-176">Get ready for the enablement of ACL on the CosmosDB Account by making sure that the virtual network and subnet have service endpoint enabled for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6a691-176">Get ready for the enablement of ACL on the CosmosDB Account by making sure that the virtual network and subnet have service endpoint enabled for Azure Cosmos DB.</span></span>

   ```powershell
   $vnProp = Get-AzureRmVirtualNetwork `
     -Name $vnName  -ResourceGroupName $rgName
   ```

5. <span data-ttu-id="6a691-177">Get properties of Azure Cosmos DB account by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6a691-177">Get properties of Azure Cosmos DB account by running the following cmdlet:</span></span>  

   ```powershell
   $apiVersion = "2015-04-08"
   $acctName = "<Azure Cosmos DB account name>"

   $cosmosDBConfiguration = Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" `
     -ApiVersion $apiVersion `
     -ResourceGroupName $rgName `
     -Name $acctName
   ```

6. <span data-ttu-id="6a691-178">Initialize the variables for use later.</span><span class="sxs-lookup"><span data-stu-id="6a691-178">Initialize the variables for use later.</span></span> <span data-ttu-id="6a691-179">Set up all the variables from the existing account definition, if you have multiple locations, you need to add them as part of the array.</span><span class="sxs-lookup"><span data-stu-id="6a691-179">Set up all the variables from the existing account definition, if you have multiple locations, you need to add them as part of the array.</span></span> <span data-ttu-id="6a691-180">In this step, you also configure virtual network service endpoint by setting the "accountVNETFilterEnabled" variable to "True".</span><span class="sxs-lookup"><span data-stu-id="6a691-180">In this step, you also configure virtual network service endpoint by setting the "accountVNETFilterEnabled" variable to "True".</span></span> <span data-ttu-id="6a691-181">This value is later assigned to the "isVirtualNetworkFilterEnabled" parameter.</span><span class="sxs-lookup"><span data-stu-id="6a691-181">This value is later assigned to the "isVirtualNetworkFilterEnabled" parameter.</span></span>  

   ```powershell
   $locations = @(@{})

   <# If you have read regions in addition to a write region, use the following code to set the $locations variable instead.

   $locations = @(@{"locationName"="<Write location>"; 
                 "failoverPriority"=0}, 
               @{"locationName"="<Read location>"; 
                  "failoverPriority"=1}) #>

   $consistencyPolicy = @{}
   $cosmosDBProperties = @{}

   $locations[0]['failoverPriority'] = $cosmosDBConfiguration.Properties.failoverPolicies.failoverPriority
   $locations[0]['locationName'] = $cosmosDBConfiguration.Properties.failoverPolicies.locationName

   $consistencyPolicy = $cosmosDBConfiguration.Properties.consistencyPolicy

   $accountVNETFilterEnabled = $True
   $subnetID = $vnProp.Id+"/subnets/" + $sname  
   $virtualNetworkRules = @(@{"id"=$subnetID})
   $databaseAccountOfferType = $cosmosDBConfiguration.Properties.databaseAccountOfferType
   ```

7. <span data-ttu-id="6a691-182">Update Azure Cosmos DB account properties with the new configuration by running the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="6a691-182">Update Azure Cosmos DB account properties with the new configuration by running the following cmdlets:</span></span> 

   ```powershell
   $cosmosDBProperties['databaseAccountOfferType'] = $databaseAccountOfferType
   $cosmosDBProperties['locations'] = $locations
   $cosmosDBProperties['consistencyPolicy'] = $consistencyPolicy
   $cosmosDBProperties['virtualNetworkRules'] = $virtualNetworkRules
   $cosmosDBProperties['isVirtualNetworkFilterEnabled'] = $accountVNETFilterEnabled

   Set-AzureRmResource `
     -ResourceType "Microsoft.DocumentDb/databaseAccounts" `
     -ApiVersion $apiVersion `
     -ResourceGroupName $rgName `
     -Name $acctName -Properties $CosmosDBProperties
   ```

8. <span data-ttu-id="6a691-183">Run the following command to verify that your Azure Cosmos DB account is updated with the virtual network service endpoint that you configured in the previous step:</span><span class="sxs-lookup"><span data-stu-id="6a691-183">Run the following command to verify that your Azure Cosmos DB account is updated with the virtual network service endpoint that you configured in the previous step:</span></span>

   ```powershell
   $UpdatedcosmosDBConfiguration = Get-AzureRmResource `
     -ResourceType "Microsoft.DocumentDb/databaseAccounts" `
     -ApiVersion $apiVersion `
     -ResourceGroupName $rgName `
     -Name $acctName

   $UpdatedcosmosDBConfiguration.Properties
   ```

## <a name="add-virtual-network-service-endpoint-for-an-azure-cosmos-db-account-that-has-ip-firewall-enabled"></a><span data-ttu-id="6a691-184">Add virtual network service endpoint for an Azure Cosmos DB account that has IP Firewall enabled</span><span class="sxs-lookup"><span data-stu-id="6a691-184">Add virtual network service endpoint for an Azure Cosmos DB account that has IP Firewall enabled</span></span>

1. <span data-ttu-id="6a691-185">First disable the IP firewall access to Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="6a691-185">First disable the IP firewall access to Azure Cosmos DB account.</span></span>  

2. <span data-ttu-id="6a691-186">Enable virtual network endpoint to the Azure Cosmos DB account by using one of the methods described in the previous sections.</span><span class="sxs-lookup"><span data-stu-id="6a691-186">Enable virtual network endpoint to the Azure Cosmos DB account by using one of the methods described in the previous sections.</span></span>  

3. <span data-ttu-id="6a691-187">Re-enable the IP firewall access.</span><span class="sxs-lookup"><span data-stu-id="6a691-187">Re-enable the IP firewall access.</span></span> 

## <a name="test-the-access"></a><span data-ttu-id="6a691-188">Test the access</span><span class="sxs-lookup"><span data-stu-id="6a691-188">Test the access</span></span>

<span data-ttu-id="6a691-189">To check if service endpoints for Azure Cosmos DB are configured as expected, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a691-189">To check if service endpoints for Azure Cosmos DB are configured as expected, use the following steps:</span></span>

* <span data-ttu-id="6a691-190">Set up two subnets in a virtual network as frontend and backend, enable Cosmos DB service endpoint for the backend subnet.</span><span class="sxs-lookup"><span data-stu-id="6a691-190">Set up two subnets in a virtual network as frontend and backend, enable Cosmos DB service endpoint for the backend subnet.</span></span>  

* <span data-ttu-id="6a691-191">Enable access in the Cosmos DB account for the backend subnet.</span><span class="sxs-lookup"><span data-stu-id="6a691-191">Enable access in the Cosmos DB account for the backend subnet.</span></span>  

* <span data-ttu-id="6a691-192">Create two virtual machines- one in backend subnet and another in the frontend subnet.</span><span class="sxs-lookup"><span data-stu-id="6a691-192">Create two virtual machines- one in backend subnet and another in the frontend subnet.</span></span>  

* <span data-ttu-id="6a691-193">Try accessing the Azure Cosmos DB account from both virtual machines.</span><span class="sxs-lookup"><span data-stu-id="6a691-193">Try accessing the Azure Cosmos DB account from both virtual machines.</span></span> <span data-ttu-id="6a691-194">You should be able to connect from virtual machine created in backend subnet but not from the one created in frontend subnet.</span><span class="sxs-lookup"><span data-stu-id="6a691-194">You should be able to connect from virtual machine created in backend subnet but not from the one created in frontend subnet.</span></span> <span data-ttu-id="6a691-195">The request will error out with 404 when you try connecting from the frontend subnet that confirms that the access to Azure Cosmos DB is secured by using the virtual network service endpoint.</span><span class="sxs-lookup"><span data-stu-id="6a691-195">The request will error out with 404 when you try connecting from the frontend subnet that confirms that the access to Azure Cosmos DB is secured by using the virtual network service endpoint.</span></span> <span data-ttu-id="6a691-196">The machine in the backend subnet will be able to work fine.</span><span class="sxs-lookup"><span data-stu-id="6a691-196">The machine in the backend subnet will be able to work fine.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="6a691-197">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="6a691-197">Frequently asked questions</span></span>

### <a name="what-happens-when-you-access-an-azure-cosmos-db-account-that-has-virtual-network-access-control-list-acl-enabled"></a><span data-ttu-id="6a691-198">What happens when you access an Azure Cosmos DB account that has virtual network Access Control List (ACL) enabled?</span><span class="sxs-lookup"><span data-stu-id="6a691-198">What happens when you access an Azure Cosmos DB account that has virtual network Access Control List (ACL) enabled?</span></span>  

<span data-ttu-id="6a691-199">HTTP 404 error is returned.</span><span class="sxs-lookup"><span data-stu-id="6a691-199">HTTP 404 error is returned.</span></span>  

### <a name="are-subnets-of-a-virtual-network-created-in-different-regions-allowed-to-access-an-azure-cosmos-db-account-in-another-region-for-example-if-azure-cosmos-db-account-is-in-west-us-or-east-us-and-virtual-networks-are-in-multiple-regions-can-the-virtual-network-access-azure-cosmos-db"></a><span data-ttu-id="6a691-200">Are subnets of a virtual network created in different regions allowed to access an Azure Cosmos DB account in another region?</span><span class="sxs-lookup"><span data-stu-id="6a691-200">Are subnets of a virtual network created in different regions allowed to access an Azure Cosmos DB account in another region?</span></span> <span data-ttu-id="6a691-201">For example, if Azure Cosmos DB account is in West US or East US and virtual network’s are in multiple regions, can the virtual network access Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="6a691-201">For example, if Azure Cosmos DB account is in West US or East US and virtual network’s are in multiple regions, can the virtual network access Azure Cosmos DB?</span></span>  

<span data-ttu-id="6a691-202">Yes, virtual networks created in different regions can access by the new capability.</span><span class="sxs-lookup"><span data-stu-id="6a691-202">Yes, virtual networks created in different regions can access by the new capability.</span></span> 

### <a name="can-an-azure-cosmos-db-account-have-both-virtual-network-service-endpoint-and-a-firewall"></a><span data-ttu-id="6a691-203">Can an Azure Cosmos DB account have both virtual network Service endpoint and a firewall?</span><span class="sxs-lookup"><span data-stu-id="6a691-203">Can an Azure Cosmos DB account have both virtual network Service endpoint and a firewall?</span></span>  

<span data-ttu-id="6a691-204">Yes, Virtual Network Service endpoint and a firewall can co-exist.</span><span class="sxs-lookup"><span data-stu-id="6a691-204">Yes, Virtual Network Service endpoint and a firewall can co-exist.</span></span> <span data-ttu-id="6a691-205">In general, you should ensure that access to portal is always enabled before configuring a virtual network service endpoint to enable you to view the metrics associated with the container.</span><span class="sxs-lookup"><span data-stu-id="6a691-205">In general, you should ensure that access to portal is always enabled before configuring a virtual network service endpoint to enable you to view the metrics associated with the container.</span></span>

### <a name="can-i-allow-access-to-other-azure-services-from-a-given-azure-region-when-service-endpoint-access-is-enabled-for-azure-cosmos-db"></a><span data-ttu-id="6a691-206">Can I "allow access to other Azure services from a given Azure region" when service endpoint access is enabled for Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="6a691-206">Can I "allow access to other Azure services from a given Azure region" when service endpoint access is enabled for Azure Cosmos DB?</span></span>  

<span data-ttu-id="6a691-207">This is required only when you want your Azure Cosmos DB account to be accessed by other Azure first party services like Azure Data factory, Azure Search or any service that is deployed in given Azure region.</span><span class="sxs-lookup"><span data-stu-id="6a691-207">This is required only when you want your Azure Cosmos DB account to be accessed by other Azure first party services like Azure Data factory, Azure Search or any service that is deployed in given Azure region.</span></span>

### <a name="how-many-virtual-network-service-endpoints-are-allowed-for-azure-cosmos-db"></a><span data-ttu-id="6a691-208">How many virtual network service endpoints are allowed for Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="6a691-208">How many virtual network service endpoints are allowed for Azure Cosmos DB?</span></span>  

<span data-ttu-id="6a691-209">64 virtual network service endpoints are allowed for an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="6a691-209">64 virtual network service endpoints are allowed for an Azure Cosmos DB account.</span></span>

### <a name="what-is-the-relationship-between-service-endpoint-and-network-security-group-nsg-rules"></a><span data-ttu-id="6a691-210">What is the relationship between Service Endpoint and Network Security Group (NSG) rules?</span><span class="sxs-lookup"><span data-stu-id="6a691-210">What is the relationship between Service Endpoint and Network Security Group (NSG) rules?</span></span>  

<span data-ttu-id="6a691-211">NSG rules in Azure Cosmos DB allow you to restrict access to specific Azure Cosmos DB IP address range.</span><span class="sxs-lookup"><span data-stu-id="6a691-211">NSG rules in Azure Cosmos DB allow you to restrict access to specific Azure Cosmos DB IP address range.</span></span> <span data-ttu-id="6a691-212">If you want to allow access to an Azure Cosmos DB instance that is present in a specific [region](https://azure.microsoft.com/global-infrastructure/regions/), you can specify the region in the following format:</span><span class="sxs-lookup"><span data-stu-id="6a691-212">If you want to allow access to an Azure Cosmos DB instance that is present in a specific [region](https://azure.microsoft.com/global-infrastructure/regions/), you can specify the region in the following format:</span></span> 

    AzureCosmosDB.<region name>

<span data-ttu-id="6a691-213">To learn more about NSG tags see [virtual network service tags](../virtual-network/security-overview.md#service-tags) article.</span><span class="sxs-lookup"><span data-stu-id="6a691-213">To learn more about NSG tags see [virtual network service tags](../virtual-network/security-overview.md#service-tags) article.</span></span> 
  
### <a name="what-is-relationship-between-an-ip-firewall-and-virtual-network-service-endpoint-capability"></a><span data-ttu-id="6a691-214">What is relationship between an IP firewall and Virtual Network service endpoint capability?</span><span class="sxs-lookup"><span data-stu-id="6a691-214">What is relationship between an IP firewall and Virtual Network service endpoint capability?</span></span>  

<span data-ttu-id="6a691-215">These two features complement each other to ensure isolation of Azure Cosmos DB assets and secure them.</span><span class="sxs-lookup"><span data-stu-id="6a691-215">These two features complement each other to ensure isolation of Azure Cosmos DB assets and secure them.</span></span> <span data-ttu-id="6a691-216">Using IP firewall ensures that static IPs can access Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="6a691-216">Using IP firewall ensures that static IPs can access Azure Cosmos DB account.</span></span>  

### <a name="can-an-on-premises-devices-ip-address-that-is-connected-through-azure-virtual-network-gatewayvpn-or-express-route-gateway-access-azure-cosmos-db-account"></a><span data-ttu-id="6a691-217">Can an on-premises device’s IP address that is connected through Azure Virtual Network gateway(VPN) or Express route gateway access Azure Cosmos DB account?</span><span class="sxs-lookup"><span data-stu-id="6a691-217">Can an on-premises device’s IP address that is connected through Azure Virtual Network gateway(VPN) or Express route gateway access Azure Cosmos DB account?</span></span>  

<span data-ttu-id="6a691-218">The on-premises device’s IP address or IP address range should be added to the list of static IPs’ in order to access the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="6a691-218">The on-premises device’s IP address or IP address range should be added to the list of static IPs’ in order to access the Azure Cosmos DB account.</span></span>  

### <a name="what-happens-if-you-delete-a-virtual-network-that-has-service-endpoint-setup-for-azure-cosmos-db"></a><span data-ttu-id="6a691-219">What happens if you delete a virtual network that has service endpoint setup for Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="6a691-219">What happens if you delete a virtual network that has service endpoint setup for Azure Cosmos DB?</span></span>  

<span data-ttu-id="6a691-220">When a virtual network is deleted, the ACL information associated with that Azure Cosmos DB is deleted and it removes the interaction between virtual network and the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="6a691-220">When a virtual network is deleted, the ACL information associated with that Azure Cosmos DB is deleted and it removes the interaction between virtual network and the Azure Cosmos DB account.</span></span> 

### <a name="what-happens-if-an-azure-cosmos-db-account-that-has-virtual-network-service-endpoint-enabled-is-deleted"></a><span data-ttu-id="6a691-221">What happens if an Azure Cosmos DB account that has virtual network service endpoint enabled is deleted?</span><span class="sxs-lookup"><span data-stu-id="6a691-221">What happens if an Azure Cosmos DB account that has virtual network service endpoint enabled is deleted?</span></span>

<span data-ttu-id="6a691-222">The metadata associated with the specific Azure Cosmos DB account is deleted from the subnet.</span><span class="sxs-lookup"><span data-stu-id="6a691-222">The metadata associated with the specific Azure Cosmos DB account is deleted from the subnet.</span></span> <span data-ttu-id="6a691-223">And it’s the end user’s responsibility to delete the subnet and virtual network used.</span><span class="sxs-lookup"><span data-stu-id="6a691-223">And it’s the end user’s responsibility to delete the subnet and virtual network used.</span></span>

### <a name="can-i-use-a-peered-virtual-network-to-create-service-endpoint-for-azure-cosmos-db"></a><span data-ttu-id="6a691-224">Can I use a peered virtual network to create service endpoint for Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="6a691-224">Can I use a peered virtual network to create service endpoint for Azure Cosmos DB?</span></span>  

<span data-ttu-id="6a691-225">No, only direct virtual network and their subnets can create Azure Cosmos DB service endpoints.</span><span class="sxs-lookup"><span data-stu-id="6a691-225">No, only direct virtual network and their subnets can create Azure Cosmos DB service endpoints.</span></span>

### <a name="what-happens-to-the-source-ip-address-of-resource-like-virtual-machine-in-the-subnet-that-has-azure-cosmos-db-service-endpoint-enabled"></a><span data-ttu-id="6a691-226">What happens to the source IP address of resource like virtual machine in the subnet that has Azure Cosmos DB service endpoint enabled?</span><span class="sxs-lookup"><span data-stu-id="6a691-226">What happens to the source IP address of resource like virtual machine in the subnet that has Azure Cosmos DB service endpoint enabled?</span></span>

<span data-ttu-id="6a691-227">When virtual network service endpoints are enabled, the source IP addresses of resources in your virtual network's subnet will switch from using public IPV4 addresses to Azure Virtual Network's private addresses for traffic to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6a691-227">When virtual network service endpoints are enabled, the source IP addresses of resources in your virtual network's subnet will switch from using public IPV4 addresses to Azure Virtual Network's private addresses for traffic to Azure Cosmos DB.</span></span>

### <a name="does-azure-cosmos-db-reside-in-the-azure-virtual-network--provided-by-the-customer"></a><span data-ttu-id="6a691-228">Does Azure Cosmos DB reside in the Azure virtual network  provided by the customer?</span><span class="sxs-lookup"><span data-stu-id="6a691-228">Does Azure Cosmos DB reside in the Azure virtual network  provided by the customer?</span></span>  

<span data-ttu-id="6a691-229">Azure Cosmos DB is a multi-tenant service with a public IP address.</span><span class="sxs-lookup"><span data-stu-id="6a691-229">Azure Cosmos DB is a multi-tenant service with a public IP address.</span></span> <span data-ttu-id="6a691-230">When you restrict access to a subnet of an Azure Virtual network by using the service endpoint feature, access is restricted for your Azure Cosmos DB account through the given Azure Virtual Network and its subnet.</span><span class="sxs-lookup"><span data-stu-id="6a691-230">When you restrict access to a subnet of an Azure Virtual network by using the service endpoint feature, access is restricted for your Azure Cosmos DB account through the given Azure Virtual Network and its subnet.</span></span>  <span data-ttu-id="6a691-231">Azure Cosmos DB account does not reside in that Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="6a691-231">Azure Cosmos DB account does not reside in that Azure Virtual Network.</span></span> 

### <a name="what-if-anything-will-be-logged-in-log-analyticsoms-if-it-is-enabled"></a><span data-ttu-id="6a691-232">What if anything will be logged in Log Analytics/OMS if it is enabled?</span><span class="sxs-lookup"><span data-stu-id="6a691-232">What if anything will be logged in Log Analytics/OMS if it is enabled?</span></span>  

<span data-ttu-id="6a691-233">Azure Cosmos DB will push logs with IP address (without the last octet) with status 403 for request blocked by ACL.</span><span class="sxs-lookup"><span data-stu-id="6a691-233">Azure Cosmos DB will push logs with IP address (without the last octet) with status 403 for request blocked by ACL.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="6a691-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a691-234">Next steps</span></span>
<span data-ttu-id="6a691-235">To configure a firewall for Azure Cosmos DB see [firewall support](firewall-support.md) article.</span><span class="sxs-lookup"><span data-stu-id="6a691-235">To configure a firewall for Azure Cosmos DB see [firewall support](firewall-support.md) article.</span></span>

