---
title: Create a zone redundant Azure application gateway
description: Learn how to create a zone redundant application gateway that does not require a seperarte gateway in each zone.
services: application-gateway
author: amsriva
manager: jpconnock
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/8/2018
ms.author: victorh
ms.openlocfilehash: 03bc58db813534fdd17c9567f6425ab7357ed901
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867676"
---
# <a name="create-a-zone-redundant-azure-application-gateway---private-preview"></a><span data-ttu-id="6fc2d-103">Create a zone redundant Azure application gateway - private preview</span><span class="sxs-lookup"><span data-stu-id="6fc2d-103">Create a zone redundant Azure application gateway - private preview</span></span>

<span data-ttu-id="6fc2d-104">The application gateway zone redundant platform is a new SKU that offers many enhancements over the existing application gateway SKU including:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-104">The application gateway zone redundant platform is a new SKU that offers many enhancements over the existing application gateway SKU including:</span></span>
- <span data-ttu-id="6fc2d-105">**Zone resiliency** - An application gateway deployment can now span multiple Availability Zones, removing the need to provision and pin separate application gateway instances in each zone with a traffic manager.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-105">**Zone resiliency** - An application gateway deployment can now span multiple Availability Zones, removing the need to provision and pin separate application gateway instances in each zone with a traffic manager.</span></span> <span data-ttu-id="6fc2d-106">You can choose a single zone or multiple zones where application gateway instances are deployed, thus ensuring zone failure resiliency.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-106">You can choose a single zone or multiple zones where application gateway instances are deployed, thus ensuring zone failure resiliency.</span></span> <span data-ttu-id="6fc2d-107">The backend pool for applications can be similarly distributed across availability zones.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-107">The backend pool for applications can be similarly distributed across availability zones.</span></span>
- <span data-ttu-id="6fc2d-108">**Performance enhancements**</span><span class="sxs-lookup"><span data-stu-id="6fc2d-108">**Performance enhancements**</span></span>
- <span data-ttu-id="6fc2d-109">**Static VIP** - The application gateway VIP now supports the static VIP type exclusively.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-109">**Static VIP** - The application gateway VIP now supports the static VIP type exclusively.</span></span> <span data-ttu-id="6fc2d-110">This ensures that the VIP associated with application gateway does not change after a restart.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-110">This ensures that the VIP associated with application gateway does not change after a restart.</span></span>
- <span data-ttu-id="6fc2d-111">**Key vault integration for customer SSL certificates**</span><span class="sxs-lookup"><span data-stu-id="6fc2d-111">**Key vault integration for customer SSL certificates**</span></span>
- <span data-ttu-id="6fc2d-112">**Faster deployment and update time**</span><span class="sxs-lookup"><span data-stu-id="6fc2d-112">**Faster deployment and update time**</span></span>

> [!NOTE]
> <span data-ttu-id="6fc2d-113">The zone redundant application gateway is currently in private preview.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-113">The zone redundant application gateway is currently in private preview.</span></span> <span data-ttu-id="6fc2d-114">This preview is provided without a service level agreement and is not recommended for production workloads.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-114">This preview is provided without a service level agreement and is not recommended for production workloads.</span></span> <span data-ttu-id="6fc2d-115">Certain features may not be supported or may have constrained capabilities.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-115">Certain features may not be supported or may have constrained capabilities.</span></span> <span data-ttu-id="6fc2d-116">See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for details.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-116">See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for details.</span></span>

## <a name="supported-regions"></a><span data-ttu-id="6fc2d-117">Supported regions</span><span class="sxs-lookup"><span data-stu-id="6fc2d-117">Supported regions</span></span>

<span data-ttu-id="6fc2d-118">Zone redundant application gateways are currently supported in the East US 2 region.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-118">Zone redundant application gateways are currently supported in the East US 2 region.</span></span> <span data-ttu-id="6fc2d-119">More regions will be added soon.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-119">More regions will be added soon.</span></span>

## <a name="topologies"></a><span data-ttu-id="6fc2d-120">Topologies</span><span class="sxs-lookup"><span data-stu-id="6fc2d-120">Topologies</span></span>

<span data-ttu-id="6fc2d-121">With the current release, you no longer need to create zone pinned application gateways to get zonal redundancy.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-121">With the current release, you no longer need to create zone pinned application gateways to get zonal redundancy.</span></span> <span data-ttu-id="6fc2d-122">The same application gateway deployment can now span multiple zones.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-122">The same application gateway deployment can now span multiple zones.</span></span>

<span data-ttu-id="6fc2d-123">At least three instances are required to ensure that they are spread across all three zones.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-123">At least three instances are required to ensure that they are spread across all three zones.</span></span> <span data-ttu-id="6fc2d-124">Application gateway distributes instances across zones as more instances are added.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-124">Application gateway distributes instances across zones as more instances are added.</span></span>

<span data-ttu-id="6fc2d-125">Previous zone redundant topologies looked like the following diagram:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-125">Previous zone redundant topologies looked like the following diagram:</span></span>

![Old redundant topology](media/create-zone-redundant/old-redundant.png)

<span data-ttu-id="6fc2d-127">The new zone redundant topology looks like this diagram:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-127">The new zone redundant topology looks like this diagram:</span></span>

![New zone redundant topology](media/create-zone-redundant/new-redundant.png)

## <a name="deployment"></a><span data-ttu-id="6fc2d-129">Deployment</span><span class="sxs-lookup"><span data-stu-id="6fc2d-129">Deployment</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6fc2d-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6fc2d-130">Prerequisites</span></span>

<span data-ttu-id="6fc2d-131">Currently zone redundant capability is only available in private preview.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-131">Currently zone redundant capability is only available in private preview.</span></span> <span data-ttu-id="6fc2d-132">You must email appgwxzone@microsoft.com to be whitelisted.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-132">You must email appgwxzone@microsoft.com to be whitelisted.</span></span> <span data-ttu-id="6fc2d-133">Once you receive a confirmation, you can proceed to the next steps.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-133">Once you receive a confirmation, you can proceed to the next steps.</span></span> <span data-ttu-id="6fc2d-134">Include the following information in your email for whitelisting:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-134">Include the following information in your email for whitelisting:</span></span>

- <span data-ttu-id="6fc2d-135">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="6fc2d-135">Subscription ID</span></span>
- <span data-ttu-id="6fc2d-136">Region name</span><span class="sxs-lookup"><span data-stu-id="6fc2d-136">Region name</span></span>
- <span data-ttu-id="6fc2d-137">Approximate count of application gateways required</span><span class="sxs-lookup"><span data-stu-id="6fc2d-137">Approximate count of application gateways required</span></span>

### <a name="resource-manager-template-deployment"></a><span data-ttu-id="6fc2d-138">Resource Manager template deployment</span><span class="sxs-lookup"><span data-stu-id="6fc2d-138">Resource Manager template deployment</span></span>

1. <span data-ttu-id="6fc2d-139">Make sure the subscription you use is whitelisted as previously mentioned.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-139">Make sure the subscription you use is whitelisted as previously mentioned.</span></span>
2. <span data-ttu-id="6fc2d-140">After you receive a confirmation, sign in to the Azure account and select the appropriate subscription if more than one subscription is present.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-140">After you receive a confirmation, sign in to the Azure account and select the appropriate subscription if more than one subscription is present.</span></span> <span data-ttu-id="6fc2d-141">Make sure you select the subscription that was whitelisted.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-141">Make sure you select the subscription that was whitelisted.</span></span>

   ```PowerShell
   Login-AzureRmAccount

   Select-AzureRmSubscription -Subscription "<whitelisted subscription name>”
   ```
3. <span data-ttu-id="6fc2d-142">Create a new resource group</span><span class="sxs-lookup"><span data-stu-id="6fc2d-142">Create a new resource group</span></span>

   ``` PowerShell
   New-AzureRmResourceGroup -Name <resource group name> -Location "East US 2"
   ```
4. <span data-ttu-id="6fc2d-143">Download the templates from [GitHub](https://github.com/amitsriva/CrossZonePreview) and note the folder where you save them.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-143">Download the templates from [GitHub](https://github.com/amitsriva/CrossZonePreview) and note the folder where you save them.</span></span>
5. <span data-ttu-id="6fc2d-144">Create a new deployment in the resource group you created.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-144">Create a new deployment in the resource group you created.</span></span> <span data-ttu-id="6fc2d-145">Modify the template and parameters file appropriately before you deploy.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-145">Modify the template and parameters file appropriately before you deploy.</span></span> 

   <span data-ttu-id="6fc2d-146">The following diagram shows where you can retrieve the tenant ID on the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-146">The following diagram shows where you can retrieve the tenant ID on the Azure portal:</span></span>

   ![Tenant ID from the portal](media/create-zone-redundant/tenant-id.png)

<span data-ttu-id="6fc2d-148">The template creates the following resources:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-148">The template creates the following resources:</span></span>

- <span data-ttu-id="6fc2d-149">**User Assigned Identity** - this is used for enabling application gateway instances to access key vault and retrieve the certificates stored by user.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-149">**User Assigned Identity** - this is used for enabling application gateway instances to access key vault and retrieve the certificates stored by user.</span></span>
- <span data-ttu-id="6fc2d-150">**KeyVault** – the Key Vault where the user’s certificate is stored.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-150">**KeyVault** – the Key Vault where the user’s certificate is stored.</span></span> <span data-ttu-id="6fc2d-151">This can be a pre-existing Key Vault as well.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-151">This can be a pre-existing Key Vault as well.</span></span>
- <span data-ttu-id="6fc2d-152">**Secret** – the private key that is stored in the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-152">**Secret** – the private key that is stored in the Key Vault.</span></span>
- <span data-ttu-id="6fc2d-153">**Access Policy** – An access policy applied on the Key Vault that grants permission using User Assigned Identity so that application gateway deployments can retrieve user certificates.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-153">**Access Policy** – An access policy applied on the Key Vault that grants permission using User Assigned Identity so that application gateway deployments can retrieve user certificates.</span></span>
- <span data-ttu-id="6fc2d-154">**Public IP address** – a reserved IP address that is used to access the application gateway.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-154">**Public IP address** – a reserved IP address that is used to access the application gateway.</span></span> <span data-ttu-id="6fc2d-155">This IP address never changes for the lifecycle of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-155">This IP address never changes for the lifecycle of the application gateway.</span></span>
- <span data-ttu-id="6fc2d-156">**Network Security Groups** – An NSG auto-created on the application gateway subnet that opens port traffic on the configured listener.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-156">**Network Security Groups** – An NSG auto-created on the application gateway subnet that opens port traffic on the configured listener.</span></span> <span data-ttu-id="6fc2d-157">This is explicitly created and managed in the new SKU compared to the previous SKU where this NSG was implicit.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-157">This is explicitly created and managed in the new SKU compared to the previous SKU where this NSG was implicit.</span></span>
- <span data-ttu-id="6fc2d-158">**Virtual Network** – The vnet where the application gateway and applications are deployed.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-158">**Virtual Network** – The vnet where the application gateway and applications are deployed.</span></span>
- <span data-ttu-id="6fc2d-159">**Application Gateway** – Creates an application gateway with instances in the required zones.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-159">**Application Gateway** – Creates an application gateway with instances in the required zones.</span></span> <span data-ttu-id="6fc2d-160">By default, all zones (1,2,3) are selected.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-160">By default, all zones (1,2,3) are selected.</span></span> <span data-ttu-id="6fc2d-161">The SKU name is changed to *Standard_v2*.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-161">The SKU name is changed to *Standard_v2*.</span></span> <span data-ttu-id="6fc2d-162">This SKU name is subject to change.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-162">This SKU name is subject to change.</span></span> <span data-ttu-id="6fc2d-163">Currently, the autoscale configuration has the min and max set to the required number of instances.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-163">Currently, the autoscale configuration has the min and max set to the required number of instances.</span></span> <span data-ttu-id="6fc2d-164">Once autoscaling is enabled, this can be adjusted.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-164">Once autoscaling is enabled, this can be adjusted.</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -Name Deployment1 -ResourceGroupName AmitVMSSLinuxTest9 -TemplateFile <complete path to template.json> -TemplateParameterFile <complete path to parameters.json>
```
### <a name="powershell-deployment"></a><span data-ttu-id="6fc2d-165">PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="6fc2d-165">PowerShell deployment</span></span>

1. <span data-ttu-id="6fc2d-166">Ensure that the subscription used is whitelisted as previously mentioned in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-166">Ensure that the subscription used is whitelisted as previously mentioned in the prerequisites.</span></span>
2. <span data-ttu-id="6fc2d-167">Download and install the private PowerShell MSI from [GitHub](https://github.com/amitsriva/CrossZonePreview/blob/master/Azure-Cmdlets-5.7.0.19009-x64.msi).</span><span class="sxs-lookup"><span data-stu-id="6fc2d-167">Download and install the private PowerShell MSI from [GitHub](https://github.com/amitsriva/CrossZonePreview/blob/master/Azure-Cmdlets-5.7.0.19009-x64.msi).</span></span>
3. <span data-ttu-id="6fc2d-168">Download the private PowerShell zip file from the location mentioned in preview registration confirmation email.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-168">Download the private PowerShell zip file from the location mentioned in preview registration confirmation email.</span></span> <span data-ttu-id="6fc2d-169">Unzip the file to your drive and note the location.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-169">Unzip the file to your drive and note the location.</span></span>
4. <span data-ttu-id="6fc2d-170">Once the preview is enabled, load the preview modules first before signing on to your account:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-170">Once the preview is enabled, load the preview modules first before signing on to your account:</span></span>

   ```PowerShell
   $azurePSPath = "<complete path to Azure-PowerShell folder>"
   import-module "$azurePSPath\AzureRM.Profile\AzureRM.Profile.psd1"
   import-module "$azurePSPath\Azure.Storage\Azure.Storage.psd1"
   import-module "$azurePSPath\AzureRM.Resources\AzureRM.Resources.psd1"
   import-module "$azurePSPath\AzureRM.Network\AzureRM.Network.psd1"
   import-module "$azurePSPath\AzureRM.KeyVault\AzureRM.KeyVault.psd1"
   ```

4. <span data-ttu-id="6fc2d-171">Sign in to the Azure account and select the desired subscription if more than one subscription is present.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-171">Sign in to the Azure account and select the desired subscription if more than one subscription is present.</span></span> <span data-ttu-id="6fc2d-172">Ensure you select the appropriate subscription that was whitelisted.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-172">Ensure you select the appropriate subscription that was whitelisted.</span></span>
5. <span data-ttu-id="6fc2d-173">Run the following commands to establish common constants that include names for most of the entities being created.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-173">Run the following commands to establish common constants that include names for most of the entities being created.</span></span> 

   <span data-ttu-id="6fc2d-174">Modify the entries as required for your naming preference.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-174">Modify the entries as required for your naming preference.</span></span>

   ```PowerShell
   $location = "eastus2"
   $version = "300"

   $rgname = "RG_A_$version"
   $appgwName = "AGW_A_$version"
   $vaultName = "KVA$version"
   $userAssignedIdentityName = "UI_A_$version"
   $certificateName = "KVCA$version"
   $nsgName = "NSG_A_$version"
   $vnetName = "VN_A_$version"
   $gwSubnetName = "SN_A_$version"
   $gipconfigname = "GC_A_$version"
   $publicIpName = "PIP_A_$version"
   $fipconfig01Name = "FC_A_$version"
   $poolName = "BP_A_$version"
   $frontendPort01Name = "FP1_A_$version"
   $frontendPort02Name = "FP2_A_$version"
   $poolSetting01Name = "BS_A_$version"
   $listener01Name = "HL1_A_$version"
   $listener02Name = "HL2_A_$version"
   $rule01Name = "RR1_A_$version"
   $rule02Name = "RR2_A_$version"
   $AddressPrefix = "111.111.222.0" 
   ```
6. <span data-ttu-id="6fc2d-175">Create the resource group:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-175">Create the resource group:</span></span>

   ```PowerShell
   $resourceGroup = New-AzureRmResourceGroup -Name $rgname -Location $location -Force
   ```
7. <span data-ttu-id="6fc2d-176">Create the User Assigned Identity used to give access to the application gateway to retrieve certificates from the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-176">Create the User Assigned Identity used to give access to the application gateway to retrieve certificates from the Key Vault.</span></span>

   ```PowerShell
   $userAssignedIdentity = New-AzureRmResource -ResourceGroupName $rgname -Location $location -ResourceName $userAssignedIdentityName -ResourceType Microsoft.ManagedIdentity/userAssignedIdentities -Force
   ```
8. <span data-ttu-id="6fc2d-177">Create the Key Vault used to store your certificates:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-177">Create the Key Vault used to store your certificates:</span></span>

   ```PowerShell
   $keyVault = New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $rgname -Location $location -EnableSoftDelete
   ```
9. <span data-ttu-id="6fc2d-178">Upload certificate to Key Vault as a secret:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-178">Upload certificate to Key Vault as a secret:</span></span>

   ```PowerShell
   $securepfxpwd = ConvertTo-SecureString -String "<password>" -AsPlainText -Force

   $cert = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name         $certificateName -FilePath ‘<path to pfx file>'  -Password $securepfxpwd
   ```
10. <span data-ttu-id="6fc2d-179">Assign access policy to the Key Vault using the User Assigned Identity.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-179">Assign access policy to the Key Vault using the User Assigned Identity.</span></span> <span data-ttu-id="6fc2d-180">This allows the application gateway instances to access the Key Vault secret:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-180">This allows the application gateway instances to access the Key Vault secret:</span></span>

   ```PowerShell
   Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $rgname -PermissionsToSecrets get -ObjectId $userAssignedIdentity.Properties.principalId
   ```
11. <span data-ttu-id="6fc2d-181">Create the Network Security Group (NSG) to allow access to the application gateway subnet on ports where new listeners are created.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-181">Create the Network Security Group (NSG) to allow access to the application gateway subnet on ports where new listeners are created.</span></span>

    <span data-ttu-id="6fc2d-182">For example, for HTTP/HTTPS on default ports the NSG would allow inbound access to 80, 443 and 65200-65535 for management operations.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-182">For example, for HTTP/HTTPS on default ports the NSG would allow inbound access to 80, 443 and 65200-65535 for management operations.</span></span>

   ```PowerShell
   $srule01 = New-AzureRmNetworkSecurityRuleConfig -Name "listeners" -Direction Inbound -SourceAddressPrefix * -SourcePortRange * -Protocol * -DestinationAddressPrefix * -DestinationPortRange 22,80,443 -Access Allow -Priority 100

   $srule02 = New-AzureRmNetworkSecurityRuleConfig -Name "managementPorts" -Direction Inbound -SourceAddressPrefix * -SourcePortRange * -Protocol * -DestinationAddressPrefix * -DestinationPortRange "65200-65535" -Access Allow -Priority 101

   $nsg = New-AzureRmNetworkSecurityGroup -Name $nsgName -ResourceGroupName $rgname -Location $location -SecurityRules $srule01,$srule02 -Force
   ```

12. <span data-ttu-id="6fc2d-183">Create VNet and subnets:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-183">Create VNet and subnets:</span></span>

   ```PowerShell
   $gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 
   $gwSubnetName -AddressPrefix "$AddressPrefix/24" -NetworkSecurityGroup $nsg

   $vnet = New-AzureRmvirtualNetwork -Name $vnetName -ResourceGroupName $rgname -Location $location -AddressPrefix "$AddressPrefix/24" -Subnet $gwSubnet -Force
   ```
13. <span data-ttu-id="6fc2d-184">Create a public IP address of type reserved/static:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-184">Create a public IP address of type reserved/static:</span></span>

   ```PowerShell
   $publicip = New-AzureRmPublicIpAddress -ResourceGroupName $rgname -name $publicIpName -location $location -AllocationMethod Static -Sku Standard -Force
   ```

14. <span data-ttu-id="6fc2d-185">Create the application gateway:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-185">Create the application gateway:</span></span>

   ```PowerShell
   $gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name $gipconfigname -Subnet $gwSubnet

   $fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name $fipconfig01Name -PublicIPAddress $publicip

   $pool = New-AzureRmApplicationGatewayBackendAddressPool -Name $poolName -BackendIPAddresses testbackend1.westus.cloudapp.azure.com, testbackend2.westus.cloudapp.azure.com

   $fp01 = New-AzureRmApplicationGatewayFrontendPort -Name $frontendPort01Name -Port 443

   $fp02 = New-AzureRmApplicationGatewayFrontendPort -Name $frontendPort02Name -Port 80

   $sslCert01 = New-AzureRmApplicationGatewaySslCertificate -Name "SSLCert" -KeyVaultSecretId $secret.Id

   $listener01 = New-AzureRmApplicationGatewayHttpListener -Name $listener01Name -Protocol Https -FrontendIPConfiguration
 $fipconfig01 -FrontendPort $fp01 -SslCertificate $sslCert01

   $listener02 = New-AzureRmApplicationGatewayHttpListener -Name $listener02Name -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp02

   $poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name $poolSetting01Name -Port 80 -Protocol Http -CookieBasedAffinity Disabled

   $rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name $rule01Name -RuleType basic -BackendHttpSettings $poolSetting01 -HttpListener $listener01 -BackendAddressPool $pool

   $rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name $rule02Name -RuleType basic -BackendHttpSettings $poolSetting01 -HttpListener $listener02 -BackendAddressPool $pool

   $sku = New-AzureRmApplicationGatewaySku -Name Standard_v2 -Tier Standard_v2 -Capacity 2

   $listeners = @($listener02)

   $fps = @($fp01, $fp02)

   $fipconfigs = @($fipconfig01)

   $sslCerts = @($sslCert01)

   $rules = @($rule01, $rule02)

   $listeners = @($listener01, $listener02)

   $appgw = New-AzureRmApplicationGateway -Name $appgwName -ResourceGroupName $rgname -Location $location -UserAssignedIdentityId $userAssignedIdentity.ResourceId -Probes $probeHttps -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting01 -GatewayIpConfigurations $gipconfig -FrontendIpConfigurations $fipconfigs -FrontendPorts $fps -HttpListeners $listeners -RequestRoutingRules $rules -Sku $sku -SslPolicy $sslPolicy -sslCertificates $sslCerts -Force
   ```

15. <span data-ttu-id="6fc2d-186">Retrieve the created application gateway’s public IP address:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-186">Retrieve the created application gateway’s public IP address:</span></span>

   ```PowerShell
   $pip = Get-AzureRmPublicIpAddress -Name $publicIpName -ResourceGroupName $rgname $pip.IpAddress
   ```

## <a name="frequently-asked-questions"></a><span data-ttu-id="6fc2d-187">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="6fc2d-187">Frequently asked questions</span></span>

-  <span data-ttu-id="6fc2d-188">Will I be billed for application gateway in preview?</span><span class="sxs-lookup"><span data-stu-id="6fc2d-188">Will I be billed for application gateway in preview?</span></span>

   <span data-ttu-id="6fc2d-189">During preview, there is no charge.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-189">During preview, there is no charge.</span></span> <span data-ttu-id="6fc2d-190">You will be billed for resources other than application gateway, such as Key Vault, virtual machines etc.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-190">You will be billed for resources other than application gateway, such as Key Vault, virtual machines etc.</span></span>
- <span data-ttu-id="6fc2d-191">What regions is the preview available in?</span><span class="sxs-lookup"><span data-stu-id="6fc2d-191">What regions is the preview available in?</span></span>

   <span data-ttu-id="6fc2d-192">The preview is currently available in the East US 2 region.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-192">The preview is currently available in the East US 2 region.</span></span> <span data-ttu-id="6fc2d-193">More regions will be added soon.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-193">More regions will be added soon.</span></span>
- <span data-ttu-id="6fc2d-194">Is the portal supported in the preview?</span><span class="sxs-lookup"><span data-stu-id="6fc2d-194">Is the portal supported in the preview?</span></span>

   <span data-ttu-id="6fc2d-195">No, support is limited to a private PowerShell module and Resource Manager template during the private preview.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-195">No, support is limited to a private PowerShell module and Resource Manager template during the private preview.</span></span>

- <span data-ttu-id="6fc2d-196">Is production workload supported during private preview?</span><span class="sxs-lookup"><span data-stu-id="6fc2d-196">Is production workload supported during private preview?</span></span>

   <span data-ttu-id="6fc2d-197">No, there is no SLA or support during the private preview.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-197">No, there is no SLA or support during the private preview.</span></span> <span data-ttu-id="6fc2d-198">It is not recommended to put production workloads during previews.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-198">It is not recommended to put production workloads during previews.</span></span> <span data-ttu-id="6fc2d-199">Support is limited to direct interaction with product group using the email alias for preview.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-199">Support is limited to direct interaction with product group using the email alias for preview.</span></span>

- <span data-ttu-id="6fc2d-200">How do I report issues?</span><span class="sxs-lookup"><span data-stu-id="6fc2d-200">How do I report issues?</span></span>

   <span data-ttu-id="6fc2d-201">The private preview may contain bugs and may have frequent code deployments.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-201">The private preview may contain bugs and may have frequent code deployments.</span></span> <span data-ttu-id="6fc2d-202">Use the support alias appgwxzone@microsoft.com for reporting issues and assistance.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-202">Use the support alias appgwxzone@microsoft.com for reporting issues and assistance.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="6fc2d-203">Known issues and limitations</span><span class="sxs-lookup"><span data-stu-id="6fc2d-203">Known issues and limitations</span></span>


|<span data-ttu-id="6fc2d-204">Issue</span><span class="sxs-lookup"><span data-stu-id="6fc2d-204">Issue</span></span>  |<span data-ttu-id="6fc2d-205">Details</span><span class="sxs-lookup"><span data-stu-id="6fc2d-205">Details</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="6fc2d-206">Billing</span><span class="sxs-lookup"><span data-stu-id="6fc2d-206">Billing</span></span>     |<span data-ttu-id="6fc2d-207">No billing currently</span><span class="sxs-lookup"><span data-stu-id="6fc2d-207">No billing currently</span></span>|
|<span data-ttu-id="6fc2d-208">Diagnostics logs (not metrics)</span><span class="sxs-lookup"><span data-stu-id="6fc2d-208">Diagnostics logs (not metrics)</span></span>     |<span data-ttu-id="6fc2d-209">Performance and request/response logs don’t appear currently</span><span class="sxs-lookup"><span data-stu-id="6fc2d-209">Performance and request/response logs don’t appear currently</span></span>|
|<span data-ttu-id="6fc2d-210">Portal/CLI/SDK</span><span class="sxs-lookup"><span data-stu-id="6fc2d-210">Portal/CLI/SDK</span></span>     |<span data-ttu-id="6fc2d-211">No support for portal, CLI, or SDK.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-211">No support for portal, CLI, or SDK.</span></span> <span data-ttu-id="6fc2d-212">The portal must not be used to issue updates to preview gateways.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-212">The portal must not be used to issue updates to preview gateways.</span></span>|
|<span data-ttu-id="6fc2d-213">Update via template fails occasionally</span><span class="sxs-lookup"><span data-stu-id="6fc2d-213">Update via template fails occasionally</span></span>     |<span data-ttu-id="6fc2d-214">This is due to race condition with KeyVault access policy</span><span class="sxs-lookup"><span data-stu-id="6fc2d-214">This is due to race condition with KeyVault access policy</span></span>|<span data-ttu-id="6fc2d-215">Once the Key Vault and User Assigned Identity is created, it can be removed from the template and only references to secret and identity are required in the template.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-215">Once the Key Vault and User Assigned Identity is created, it can be removed from the template and only references to secret and identity are required in the template.</span></span>|
|<span data-ttu-id="6fc2d-216">Autoscaling</span><span class="sxs-lookup"><span data-stu-id="6fc2d-216">Autoscaling</span></span>     |<span data-ttu-id="6fc2d-217">No support for autoscaling currently</span><span class="sxs-lookup"><span data-stu-id="6fc2d-217">No support for autoscaling currently</span></span>|
|<span data-ttu-id="6fc2d-218">WAF</span><span class="sxs-lookup"><span data-stu-id="6fc2d-218">WAF</span></span>     |<span data-ttu-id="6fc2d-219">Currently WAF is not supported</span><span class="sxs-lookup"><span data-stu-id="6fc2d-219">Currently WAF is not supported</span></span>|
|<span data-ttu-id="6fc2d-220">User supplied certificates and Dynamic VIPs</span><span class="sxs-lookup"><span data-stu-id="6fc2d-220">User supplied certificates and Dynamic VIPs</span></span>     |<span data-ttu-id="6fc2d-221">These are not supported in the new model.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-221">These are not supported in the new model.</span></span> <span data-ttu-id="6fc2d-222">Use Key Vault for storing certificates and static VIPs.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-222">Use Key Vault for storing certificates and static VIPs.</span></span>|
|<span data-ttu-id="6fc2d-223">Same subnet for old and preview version of application gateway</span><span class="sxs-lookup"><span data-stu-id="6fc2d-223">Same subnet for old and preview version of application gateway</span></span>     |<span data-ttu-id="6fc2d-224">A subnet with an existing application gateway (old model) cannot be used for the private preview version.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-224">A subnet with an existing application gateway (old model) cannot be used for the private preview version.</span></span>|
|<span data-ttu-id="6fc2d-225">HTTP/2, FIPS mode, WebSocket, Azure Web Apps as backend</span><span class="sxs-lookup"><span data-stu-id="6fc2d-225">HTTP/2, FIPS mode, WebSocket, Azure Web Apps as backend</span></span>     |<span data-ttu-id="6fc2d-226">Currently unsupported</span><span class="sxs-lookup"><span data-stu-id="6fc2d-226">Currently unsupported</span></span> |


## <a name="support-and-feedback"></a><span data-ttu-id="6fc2d-227">Support and feedback</span><span class="sxs-lookup"><span data-stu-id="6fc2d-227">Support and feedback</span></span>

<span data-ttu-id="6fc2d-228">For support and feedback, contact to appgwxzone@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-228">For support and feedback, contact to appgwxzone@microsoft.com.</span></span> <span data-ttu-id="6fc2d-229">The application gateway product group is happy to hear your feedback for enhancements and provide guidance where required.</span><span class="sxs-lookup"><span data-stu-id="6fc2d-229">The application gateway product group is happy to hear your feedback for enhancements and provide guidance where required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fc2d-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="6fc2d-230">Next steps</span></span>

<span data-ttu-id="6fc2d-231">Learn about other application gateway features:</span><span class="sxs-lookup"><span data-stu-id="6fc2d-231">Learn about other application gateway features:</span></span>

- [<span data-ttu-id="6fc2d-232">What is Azure Application Gateway?</span><span class="sxs-lookup"><span data-stu-id="6fc2d-232">What is Azure Application Gateway?</span></span>](overview.md)