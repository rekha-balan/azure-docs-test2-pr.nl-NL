---
title: 'Modify an ExpressRoute circuit: PowerShell: Azure classic| Microsoft Docs'
description: This article walks you through the steps to check the status, update, or delete and deprovision your ExpressRoute classic deployment model circuit.
services: expressroute
author: ganesr
ms.service: expressroute
ms.topic: conceptual
ms.date: 07/26/2018
ms.author: ganesr;cherylmc
ms.openlocfilehash: 407782ff59147f227f5f34bc3318333093b4f57e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791432"
---
# <a name="modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="1fc21-103">Modify an ExpressRoute circuit using PowerShell (classic)</span><span class="sxs-lookup"><span data-stu-id="1fc21-103">Modify an ExpressRoute circuit using PowerShell (classic)</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [Video - Azure portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classic)](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="1fc21-109">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="1fc21-109">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="1fc21-110">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="1fc21-110">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="1fc21-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1fc21-111">Before you begin</span></span>

<span data-ttu-id="1fc21-112">Install the latest versions of the Azure Service Management (SM) PowerShell modules and the ExpressRoute module.</span><span class="sxs-lookup"><span data-stu-id="1fc21-112">Install the latest versions of the Azure Service Management (SM) PowerShell modules and the ExpressRoute module.</span></span>  <span data-ttu-id="1fc21-113">When using the following example, note that the version number (in this example, 5.1.1) will change as newer versions of the cmdlets are released.</span><span class="sxs-lookup"><span data-stu-id="1fc21-113">When using the following example, note that the version number (in this example, 5.1.1) will change as newer versions of the cmdlets are released.</span></span>

```powershell
Import-Module 'C:\Program Files\WindowsPowerShell\Modules\Azure\5.1.1\Azure\Azure.psd1'
Import-Module 'C:\Program Files\WindowsPowerShell\Modules\Azure\5.1.1\ExpressRoute\ExpressRoute.psd1'
```

<span data-ttu-id="1fc21-114">If you need more information about Azure PowerShell, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="1fc21-114">If you need more information about Azure PowerShell, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

<span data-ttu-id="1fc21-115">To sign in to your Azure account, use the following example:</span><span class="sxs-lookup"><span data-stu-id="1fc21-115">To sign in to your Azure account, use the following example:</span></span>

1. <span data-ttu-id="1fc21-116">Open your PowerShell console with elevated rights and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="1fc21-116">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="1fc21-117">Use the following example to help you connect:</span><span class="sxs-lookup"><span data-stu-id="1fc21-117">Use the following example to help you connect:</span></span>

  ```powershel
  Connect-AzureRmAccount
  ```
2. <span data-ttu-id="1fc21-118">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="1fc21-118">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="1fc21-119">If you have more than one subscription, select the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="1fc21-119">If you have more than one subscription, select the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

4. <span data-ttu-id="1fc21-120">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="1fc21-120">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

  ```powershell
  Add-AzureAccount
  ```

## <a name="get-the-status-of-a-circuit"></a><span data-ttu-id="1fc21-121">Get the status of a circuit</span><span class="sxs-lookup"><span data-stu-id="1fc21-121">Get the status of a circuit</span></span>

<span data-ttu-id="1fc21-122">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fc21-122">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="1fc21-123">Making the call without any parameters lists all the circuits.</span><span class="sxs-lookup"><span data-stu-id="1fc21-123">Making the call without any parameters lists all the circuits.</span></span>

```powershell
Get-AzureDedicatedCircuit

Bandwidth                        : 200
CircuitName                      : MyTestCircuit
Location                         : Silicon Valley
ServiceKey                       : *********************************
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Standard
Status                           : Enabled

Bandwidth                        : 1000
CircuitName                      : MyAsiaCircuit
Location                         : Singapore
ServiceKey                       : #################################
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Standard
Status                           : Enabled
```

<span data-ttu-id="1fc21-124">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span><span class="sxs-lookup"><span data-stu-id="1fc21-124">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span></span>

```powershell
Get-AzureDedicatedCircuit -ServiceKey "*********************************"

Bandwidth                        : 200
CircuitName                      : MyTestCircuit
Location                         : Silicon Valley
ServiceKey                       : *********************************
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Standard
Status                           : Enabled
```

<span data-ttu-id="1fc21-125">You can get detailed descriptions of all the parameters by running the following example:</span><span class="sxs-lookup"><span data-stu-id="1fc21-125">You can get detailed descriptions of all the parameters by running the following example:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify-a-circuit"></a><span data-ttu-id="1fc21-126">Modify a circuit</span><span class="sxs-lookup"><span data-stu-id="1fc21-126">Modify a circuit</span></span>

<span data-ttu-id="1fc21-127">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span><span class="sxs-lookup"><span data-stu-id="1fc21-127">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="1fc21-128">You can do the following tasks with no downtime:</span><span class="sxs-lookup"><span data-stu-id="1fc21-128">You can do the following tasks with no downtime:</span></span>

* <span data-ttu-id="1fc21-129">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="1fc21-129">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="1fc21-130">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span><span class="sxs-lookup"><span data-stu-id="1fc21-130">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="1fc21-131">Downgrading the bandwidth of a circuit is not supported.</span><span class="sxs-lookup"><span data-stu-id="1fc21-131">Downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="1fc21-132">Change the metering plan from Metered Data to Unlimited Data.</span><span class="sxs-lookup"><span data-stu-id="1fc21-132">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="1fc21-133">Changing the metering plan from Unlimited Data to Metered Data is not supported.</span><span class="sxs-lookup"><span data-stu-id="1fc21-133">Changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="1fc21-134">You can enable and disable *Allow Classic Operations*.</span><span class="sxs-lookup"><span data-stu-id="1fc21-134">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="1fc21-135">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span><span class="sxs-lookup"><span data-stu-id="1fc21-135">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="enable-the-expressroute-premium-add-on"></a><span data-ttu-id="1fc21-136">Enable the ExpressRoute premium add-on</span><span class="sxs-lookup"><span data-stu-id="1fc21-136">Enable the ExpressRoute premium add-on</span></span>

<span data-ttu-id="1fc21-137">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1fc21-137">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

```powershell
Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

Bandwidth                        : 1000
CircuitName                      : TestCircuit
Location                         : Silicon Valley
ServiceKey                       : *********************************
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Premium
Status                           : Enabled
```

<span data-ttu-id="1fc21-138">Your circuit will now have the ExpressRoute premium add-on features enabled.</span><span class="sxs-lookup"><span data-stu-id="1fc21-138">Your circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="1fc21-139">As soon as the command has been successfully run, billing for the premium add-on capability begins.</span><span class="sxs-lookup"><span data-stu-id="1fc21-139">As soon as the command has been successfully run, billing for the premium add-on capability begins.</span></span>

### <a name="disable-the-expressroute-premium-add-on"></a><span data-ttu-id="1fc21-140">Disable the ExpressRoute premium add-on</span><span class="sxs-lookup"><span data-stu-id="1fc21-140">Disable the ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.
> 
> 

#### <a name="considerations"></a><span data-ttu-id="1fc21-142">Considerations</span><span class="sxs-lookup"><span data-stu-id="1fc21-142">Considerations</span></span>

* <span data-ttu-id="1fc21-143">Make sure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span><span class="sxs-lookup"><span data-stu-id="1fc21-143">Make sure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span></span> <span data-ttu-id="1fc21-144">If you don't do this, your update request fails, and you are billed the premium rates.</span><span class="sxs-lookup"><span data-stu-id="1fc21-144">If you don't do this, your update request fails, and you are billed the premium rates.</span></span>
* <span data-ttu-id="1fc21-145">You must unlink all virtual networks in other geopolitical regions.</span><span class="sxs-lookup"><span data-stu-id="1fc21-145">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="1fc21-146">If you don't, your update request fails, and you are billed the premium rates.</span><span class="sxs-lookup"><span data-stu-id="1fc21-146">If you don't, your update request fails, and you are billed the premium rates.</span></span>
* <span data-ttu-id="1fc21-147">Your route table must be less than 4,000 routes for private peering.</span><span class="sxs-lookup"><span data-stu-id="1fc21-147">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="1fc21-148">If your route table size is greater than 4,000 routes, the BGP session drops and won't be reenabled until the number of advertised prefixes goes below 4,000.</span><span class="sxs-lookup"><span data-stu-id="1fc21-148">If your route table size is greater than 4,000 routes, the BGP session drops and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

#### <a name="to-disable-the-premium-add-on"></a><span data-ttu-id="1fc21-149">To disable the premium add-on</span><span class="sxs-lookup"><span data-stu-id="1fc21-149">To disable the premium add-on</span></span>

<span data-ttu-id="1fc21-150">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1fc21-150">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

```powershell

Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

Bandwidth                        : 1000
CircuitName                      : TestCircuit
Location                         : Silicon Valley
ServiceKey                       : *********************************
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Standard
Status                           : Enabled
```

### <a name="update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="1fc21-151">Update the ExpressRoute circuit bandwidth</span><span class="sxs-lookup"><span data-stu-id="1fc21-151">Update the ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="1fc21-152">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span><span class="sxs-lookup"><span data-stu-id="1fc21-152">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="1fc21-153">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span><span class="sxs-lookup"><span data-stu-id="1fc21-153">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port. You cannot upgrade the circuit if there is no additional capacity available at that location.
>
> You cannot reduce the bandwidth of an ExpressRoute circuit without disruption. Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="1fc21-158">Resize a circuit</span><span class="sxs-lookup"><span data-stu-id="1fc21-158">Resize a circuit</span></span>

<span data-ttu-id="1fc21-159">After you decide what size you need, you can use the following command to resize your circuit:</span><span class="sxs-lookup"><span data-stu-id="1fc21-159">After you decide what size you need, you can use the following command to resize your circuit:</span></span>

```powershell
Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

Bandwidth                        : 1000
CircuitName                      : TestCircuit
Location                         : Silicon Valley
ServiceKey                       : *********************************
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Standard
Status                           : Enabled
```

<span data-ttu-id="1fc21-160">Once your circuit has been sized up on the Microsoft side, you must contact your connectivity provider to update configurations on their side to match this change.</span><span class="sxs-lookup"><span data-stu-id="1fc21-160">Once your circuit has been sized up on the Microsoft side, you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="1fc21-161">Billing begins for the updated bandwidth option from this point on.</span><span class="sxs-lookup"><span data-stu-id="1fc21-161">Billing begins for the updated bandwidth option from this point on.</span></span>

<span data-ttu-id="1fc21-162">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span><span class="sxs-lookup"><span data-stu-id="1fc21-162">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span></span> <span data-ttu-id="1fc21-163">You must delete this circuit and create a new circuit of the size you need.</span><span class="sxs-lookup"><span data-stu-id="1fc21-163">You must delete this circuit and create a new circuit of the size you need.</span></span>

```powershell
Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available to perform this circuit
update operation
At line:1 char:1
+ Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
  + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand
```

## <a name="deprovision-and-delete-a-circuit"></a><span data-ttu-id="1fc21-164">Deprovision and delete a circuit</span><span class="sxs-lookup"><span data-stu-id="1fc21-164">Deprovision and delete a circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="1fc21-165">Considerations</span><span class="sxs-lookup"><span data-stu-id="1fc21-165">Considerations</span></span>

* <span data-ttu-id="1fc21-166">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span><span class="sxs-lookup"><span data-stu-id="1fc21-166">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span></span> <span data-ttu-id="1fc21-167">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span><span class="sxs-lookup"><span data-stu-id="1fc21-167">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span></span>
* <span data-ttu-id="1fc21-168">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span><span class="sxs-lookup"><span data-stu-id="1fc21-168">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="1fc21-169">We continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span><span class="sxs-lookup"><span data-stu-id="1fc21-169">We continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="1fc21-170">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**), you can then delete the circuit.</span><span class="sxs-lookup"><span data-stu-id="1fc21-170">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**), you can then delete the circuit.</span></span> <span data-ttu-id="1fc21-171">This stops billing for the circuit.</span><span class="sxs-lookup"><span data-stu-id="1fc21-171">This stops billing for the circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="1fc21-172">Delete a circuit</span><span class="sxs-lookup"><span data-stu-id="1fc21-172">Delete a circuit</span></span>

<span data-ttu-id="1fc21-173">You can delete your ExpressRoute circuit by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1fc21-173">You can delete your ExpressRoute circuit by running the following command:</span></span>

```powershell
Remove-AzureDedicatedCircuit -ServiceKey "*********************************"
```