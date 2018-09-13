---
title: Enable Azure Active Directory Domain Services using PowerShell | Microsoft Docs
description: Enable Azure Active Directory Domain Services using PowerShell
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: d4bc5583-6537-4cd9-bc4b-7712fdd9272a
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 12/06/2017
ms.author: maheshu
ms.openlocfilehash: ee3f65b7afde19a1f9c730334043cc7dae9ea791
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866486"
---
# <a name="enable-azure-active-directory-domain-services-using-powershell"></a><span data-ttu-id="4d421-103">Enable Azure Active Directory Domain Services using PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d421-103">Enable Azure Active Directory Domain Services using PowerShell</span></span>
<span data-ttu-id="4d421-104">This article shows you how to enable Azure Active Directory (AD) Domain Services using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d421-104">This article shows you how to enable Azure Active Directory (AD) Domain Services using PowerShell.</span></span>

## <a name="task-1-install-the-required-powershell-modules"></a><span data-ttu-id="4d421-105">Task 1: Install the required PowerShell modules</span><span class="sxs-lookup"><span data-stu-id="4d421-105">Task 1: Install the required PowerShell modules</span></span>

### <a name="install-and-configure-azure-ad-powershell"></a><span data-ttu-id="4d421-106">Install and configure Azure AD PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d421-106">Install and configure Azure AD PowerShell</span></span>
<span data-ttu-id="4d421-107">Follow the instructions in the article to [install the Azure AD PowerShell module and connect to Azure AD](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?toc=%2fazure%2factive-directory-domain-services%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d421-107">Follow the instructions in the article to [install the Azure AD PowerShell module and connect to Azure AD](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?toc=%2fazure%2factive-directory-domain-services%2ftoc.json).</span></span>

### <a name="install-and-configure-azure-powershell"></a><span data-ttu-id="4d421-108">Install and configure Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d421-108">Install and configure Azure PowerShell</span></span>
<span data-ttu-id="4d421-109">Follow the instructions in the article to [install the Azure PowerShell module and connect to your Azure subscription](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?toc=%2fazure%2factive-directory-domain-services%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d421-109">Follow the instructions in the article to [install the Azure PowerShell module and connect to your Azure subscription](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?toc=%2fazure%2factive-directory-domain-services%2ftoc.json).</span></span>


## <a name="task-2-create-the-required-service-principal-in-your-azure-ad-directory"></a><span data-ttu-id="4d421-110">Task 2: Create the required service principal in your Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="4d421-110">Task 2: Create the required service principal in your Azure AD directory</span></span>
<span data-ttu-id="4d421-111">Type the following PowerShell command to create the service principal required for Azure AD Domain Services in your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="4d421-111">Type the following PowerShell command to create the service principal required for Azure AD Domain Services in your Azure AD directory.</span></span>
```powershell
# Create the service principal for Azure AD Domain Services.
New-AzureADServicePrincipal -AppId “2565bd9d-da50-47d4-8b85-4c97f669dc36”
```

## <a name="task-3-create-and-configure-the-aad-dc-administrators-group"></a><span data-ttu-id="4d421-112">Task 3: Create and configure the 'AAD DC Administrators' group</span><span class="sxs-lookup"><span data-stu-id="4d421-112">Task 3: Create and configure the 'AAD DC Administrators' group</span></span>
<span data-ttu-id="4d421-113">The next task is to create the administrator group that will be used to delegate administration tasks on your managed domain.</span><span class="sxs-lookup"><span data-stu-id="4d421-113">The next task is to create the administrator group that will be used to delegate administration tasks on your managed domain.</span></span>
```powershell
# Create the delegated administration group for AAD Domain Services.
New-AzureADGroup -DisplayName "AAD DC Administrators" `
  -Description "Delegated group to administer Azure AD Domain Services" `
  -SecurityEnabled $true -MailEnabled $false `
  -MailNickName "AADDCAdministrators"
```

<span data-ttu-id="4d421-114">Now that you've created the group, add a couple of users to the group.</span><span class="sxs-lookup"><span data-stu-id="4d421-114">Now that you've created the group, add a couple of users to the group.</span></span>
```powershell
# First, retrieve the object ID of the newly created 'AAD DC Administrators' group.
$GroupObjectId = Get-AzureADGroup `
  -Filter "DisplayName eq 'AAD DC Administrators'" | `
  Select-Object ObjectId

# Now, retrieve the object ID of the user you'd like to add to the group.
$UserObjectId = Get-AzureADUser `
  -Filter "UserPrincipalName eq 'admin@contoso100.onmicrosoft.com'" | `
  Select-Object ObjectId

# Add the user to the 'AAD DC Administrators' group.
Add-AzureADGroupMember -ObjectId $GroupObjectId.ObjectId -RefObjectId $UserObjectId.ObjectId
```

## <a name="task-4-register-the-azure-ad-domain-services-resource-provider"></a><span data-ttu-id="4d421-115">Task 4: Register the Azure AD Domain Services resource provider</span><span class="sxs-lookup"><span data-stu-id="4d421-115">Task 4: Register the Azure AD Domain Services resource provider</span></span>
<span data-ttu-id="4d421-116">Type the following PowerShell command to register the resource provider for Azure AD Domain Services:</span><span class="sxs-lookup"><span data-stu-id="4d421-116">Type the following PowerShell command to register the resource provider for Azure AD Domain Services:</span></span>
```powershell
# Register the resource provider for Azure AD Domain Services with Resource Manager.
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AAD
```

## <a name="task-5-create-a-resource-group"></a><span data-ttu-id="4d421-117">Task 5: Create a resource group</span><span class="sxs-lookup"><span data-stu-id="4d421-117">Task 5: Create a resource group</span></span>
<span data-ttu-id="4d421-118">Type the following PowerShell command to create a resource group:</span><span class="sxs-lookup"><span data-stu-id="4d421-118">Type the following PowerShell command to create a resource group:</span></span>
```powershell
$ResourceGroupName = "ContosoAaddsRg"
$AzureLocation = "westus"

# Create the resource group.
New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $AzureLocation
```

<span data-ttu-id="4d421-119">You can create the virtual network and the Azure AD Domain Services managed domain in this resource group.</span><span class="sxs-lookup"><span data-stu-id="4d421-119">You can create the virtual network and the Azure AD Domain Services managed domain in this resource group.</span></span>


## <a name="task-6-create-and-configure-the-virtual-network"></a><span data-ttu-id="4d421-120">Task 6: Create and configure the virtual network</span><span class="sxs-lookup"><span data-stu-id="4d421-120">Task 6: Create and configure the virtual network</span></span>
<span data-ttu-id="4d421-121">Now, create the virtual network in which you enable Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4d421-121">Now, create the virtual network in which you enable Azure AD Domain Services.</span></span> <span data-ttu-id="4d421-122">Ensure that you create a dedicated subnet for Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4d421-122">Ensure that you create a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="4d421-123">Do not deploy workload VMs into this dedicated subnet.</span><span class="sxs-lookup"><span data-stu-id="4d421-123">Do not deploy workload VMs into this dedicated subnet.</span></span>

<span data-ttu-id="4d421-124">Type the following PowerShell commands to create a virtual network with a dedicated subnet for Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4d421-124">Type the following PowerShell commands to create a virtual network with a dedicated subnet for Azure AD Domain Services.</span></span>

```powershell
$ResourceGroupName = "ContosoAaddsRg"
$VnetName = "DomainServicesVNet_WUS"

# Create the dedicated subnet for AAD Domain Services.
$AaddsSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name DomainServices `
  -AddressPrefix 10.0.0.0/24

$WorkloadSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name Workloads `
  -AddressPrefix 10.0.1.0/24

# Create the virtual network in which you will enable Azure AD Domain Services.
$Vnet=New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location westus `
  -Name $VnetName `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $AaddsSubnet,$WorkloadSubnet
```


## <a name="task-7-provision-the-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="4d421-125">Task 7: Provision the Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="4d421-125">Task 7: Provision the Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="4d421-126">Type the following PowerShell command to enable Azure AD Domain Services for your directory:</span><span class="sxs-lookup"><span data-stu-id="4d421-126">Type the following PowerShell command to enable Azure AD Domain Services for your directory:</span></span>

```powershell
$AzureSubscriptionId = "YOUR_AZURE_SUBSCRIPTION_ID"
$ManagedDomainName = "contoso100.com"
$ResourceGroupName = "ContosoAaddsRg"
$VnetName = "DomainServicesVNet_WUS"
$AzureLocation = "westus"

# Enable Azure AD Domain Services for the directory.
New-AzureRmResource -ResourceId "/subscriptions/$AzureSubscriptionId/resourceGroups/$ResourceGroupName/providers/Microsoft.AAD/DomainServices/$ManagedDomainName" `
  -Location $AzureLocation `
  -Properties @{"DomainName"=$ManagedDomainName; `
    "SubnetId"="/subscriptions/$AzureSubscriptionId/resourceGroups/$ResourceGroupName/providers/Microsoft.Network/virtualNetworks/$VnetName/subnets/DomainServices"} `
  -ApiVersion 2017-06-01 -Force -Verbose
```

> [!WARNING]
> <span data-ttu-id="4d421-127">**Don't forget the additional configuration steps after provisioning your managed domain.**</span><span class="sxs-lookup"><span data-stu-id="4d421-127">**Don't forget the additional configuration steps after provisioning your managed domain.**</span></span>
> <span data-ttu-id="4d421-128">After your managed domain is provisioned, you still need to complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="4d421-128">After your managed domain is provisioned, you still need to complete the following tasks:</span></span>
> * <span data-ttu-id="4d421-129">**[Update DNS settings](active-directory-ds-getting-started-dns.md)** for the virtual network so virtual machines can find the managed domain for domain join or authentication.</span><span class="sxs-lookup"><span data-stu-id="4d421-129">**[Update DNS settings](active-directory-ds-getting-started-dns.md)** for the virtual network so virtual machines can find the managed domain for domain join or authentication.</span></span>
* <span data-ttu-id="4d421-130">**[Enable password synchronization to Azure AD Domain Services](active-directory-ds-getting-started-password-sync.md)**, so end users can sign in to the managed domain using their corporate credentials.</span><span class="sxs-lookup"><span data-stu-id="4d421-130">**[Enable password synchronization to Azure AD Domain Services](active-directory-ds-getting-started-password-sync.md)**, so end users can sign in to the managed domain using their corporate credentials.</span></span>
>


## <a name="powershell-script"></a><span data-ttu-id="4d421-131">PowerShell script</span><span class="sxs-lookup"><span data-stu-id="4d421-131">PowerShell script</span></span>
<span data-ttu-id="4d421-132">The PowerShell script used to perform all tasks listed in this article is below.</span><span class="sxs-lookup"><span data-stu-id="4d421-132">The PowerShell script used to perform all tasks listed in this article is below.</span></span> <span data-ttu-id="4d421-133">Copy the script and save it to a file with a '.ps1' extension.</span><span class="sxs-lookup"><span data-stu-id="4d421-133">Copy the script and save it to a file with a '.ps1' extension.</span></span> <span data-ttu-id="4d421-134">Execute the script in PowerShell or using the PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="4d421-134">Execute the script in PowerShell or using the PowerShell Integrated Scripting Environment (ISE).</span></span>

> [!NOTE]
> <span data-ttu-id="4d421-135">**Permissions required to run this script** To enable Azure AD Domain Services, you need to be the global administrator for the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="4d421-135">**Permissions required to run this script** To enable Azure AD Domain Services, you need to be the global administrator for the Azure AD directory.</span></span> <span data-ttu-id="4d421-136">Additionally, you need at least "Contributor" privileges on the virtual network in which enable Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4d421-136">Additionally, you need at least "Contributor" privileges on the virtual network in which enable Azure AD Domain Services.</span></span>
>

```powershell
# Change the following values to match your deployment.
$AaddsAdminUserUpn = "admin@contoso100.onmicrosoft.com"
$AzureSubscriptionId = "YOUR_AZURE_SUBSCRIPTION_ID"
$ManagedDomainName = "contoso100.com"
$ResourceGroupName = "ContosoAaddsRg"
$VnetName = "DomainServicesVNet_WUS"
$AzureLocation = "westus"

# Connect to your Azure AD directory.
Connect-AzureAD

# Login to your Azure subscription.
Connect-AzureRmAccount

# Create the service principal for Azure AD Domain Services.
New-AzureADServicePrincipal -AppId “2565bd9d-da50-47d4-8b85-4c97f669dc36”

# Create the delegated administration group for AAD Domain Services.
New-AzureADGroup -DisplayName "AAD DC Administrators" `
  -Description "Delegated group to administer Azure AD Domain Services" `
  -SecurityEnabled $true -MailEnabled $false `
  -MailNickName "AADDCAdministrators"

# First, retrieve the object ID of the newly created 'AAD DC Administrators' group.
$GroupObjectId = Get-AzureADGroup `
  -Filter "DisplayName eq 'AAD DC Administrators'" | `
  Select-Object ObjectId

# Now, retrieve the object ID of the user you'd like to add to the group.
$UserObjectId = Get-AzureADUser `
  -Filter "UserPrincipalName eq '$AaddsAdminUserUpn'" | `
  Select-Object ObjectId

# Add the user to the 'AAD DC Administrators' group.
Add-AzureADGroupMember -ObjectId $GroupObjectId.ObjectId -RefObjectId $UserObjectId.ObjectId

# Register the resource provider for Azure AD Domain Services with Resource Manager.
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AAD

# Create the resource group.
New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $AzureLocation

# Create the dedicated subnet for AAD Domain Services.
$AaddsSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name DomainServices `
  -AddressPrefix 10.0.0.0/24

$WorkloadSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name Workloads `
  -AddressPrefix 10.0.1.0/24

# Create the virtual network in which you will enable Azure AD Domain Services.
$Vnet=New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $AzureLocation `
  -Name $VnetName `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $AaddsSubnet,$WorkloadSubnet

# Enable Azure AD Domain Services for the directory.
New-AzureRmResource -ResourceId "/subscriptions/$AzureSubscriptionId/resourceGroups/$ResourceGroupName/providers/Microsoft.AAD/DomainServices/$ManagedDomainName" `
  -Location $AzureLocation `
  -Properties @{"DomainName"=$ManagedDomainName; `
    "SubnetId"="/subscriptions/$AzureSubscriptionId/resourceGroups/$ResourceGroupName/providers/Microsoft.Network/virtualNetworks/$VnetName/subnets/DomainServices"} `
  -ApiVersion 2017-06-01 -Force -Verbose
```

> [!WARNING]
> <span data-ttu-id="4d421-137">**Don't forget the additional configuration steps after provisioning your managed domain.**</span><span class="sxs-lookup"><span data-stu-id="4d421-137">**Don't forget the additional configuration steps after provisioning your managed domain.**</span></span>
> <span data-ttu-id="4d421-138">After your managed domain is provisioned, you still need to complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="4d421-138">After your managed domain is provisioned, you still need to complete the following tasks:</span></span>
> * <span data-ttu-id="4d421-139">Update DNS settings for the virtual network so virtual machines can find the managed domain for domain join or authentication.</span><span class="sxs-lookup"><span data-stu-id="4d421-139">Update DNS settings for the virtual network so virtual machines can find the managed domain for domain join or authentication.</span></span>
* <span data-ttu-id="4d421-140">Enable password synchronization to Azure AD Domain Services so end users can sign in to the managed domain using their corporate credentials.</span><span class="sxs-lookup"><span data-stu-id="4d421-140">Enable password synchronization to Azure AD Domain Services so end users can sign in to the managed domain using their corporate credentials.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="4d421-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d421-141">Next steps</span></span>
<span data-ttu-id="4d421-142">After your managed domain is created, perform the following configuration tasks so you can use the managed domain:</span><span class="sxs-lookup"><span data-stu-id="4d421-142">After your managed domain is created, perform the following configuration tasks so you can use the managed domain:</span></span>

* [<span data-ttu-id="4d421-143">Update the DNS server settings for the virtual network to point to your managed domain</span><span class="sxs-lookup"><span data-stu-id="4d421-143">Update the DNS server settings for the virtual network to point to your managed domain</span></span>](active-directory-ds-getting-started-dns.md)
* [<span data-ttu-id="4d421-144">Enable password synchronization to your managed domain</span><span class="sxs-lookup"><span data-stu-id="4d421-144">Enable password synchronization to your managed domain</span></span>](active-directory-ds-getting-started-password-sync.md)
