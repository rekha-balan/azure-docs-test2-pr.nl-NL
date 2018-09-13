---
title: Use PowerShell to manage Azure Service Bus resources | Microsoft Docs
description: Use PowerShell module to create and manage Service Bus resources
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: b4acb01f4939b55317ac0c78eb467159d872f47a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671851"
---
# <a name="use-powershell-to-manage-service-bus-resources"></a><span data-ttu-id="d23af-103">Use PowerShell to manage Service Bus resources</span><span class="sxs-lookup"><span data-stu-id="d23af-103">Use PowerShell to manage Service Bus resources</span></span>

<span data-ttu-id="d23af-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span><span class="sxs-lookup"><span data-stu-id="d23af-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="d23af-105">This article describes how to use the [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus/?view=azurermps-3.7.0#service_bus) to provision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span><span class="sxs-lookup"><span data-stu-id="d23af-105">This article describes how to use the [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus/?view=azurermps-3.7.0#service_bus) to provision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="d23af-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="d23af-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="d23af-107">For more information, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d23af-107">For more information, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d23af-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d23af-108">Prerequisites</span></span>

<span data-ttu-id="d23af-109">Before you begin, you'll need the following:</span><span class="sxs-lookup"><span data-stu-id="d23af-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="d23af-110">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d23af-110">An Azure subscription.</span></span> <span data-ttu-id="d23af-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span><span class="sxs-lookup"><span data-stu-id="d23af-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="d23af-112">A computer with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d23af-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="d23af-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="d23af-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="d23af-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d23af-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="d23af-115">Get started</span><span class="sxs-lookup"><span data-stu-id="d23af-115">Get started</span></span>

<span data-ttu-id="d23af-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d23af-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="d23af-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, and retrieve and access the resources in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d23af-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, and retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="d23af-118">Provision a Service Bus namespace</span><span class="sxs-lookup"><span data-stu-id="d23af-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="d23af-119">When working with Service Bus namespaces, you can use the [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d23af-119">When working with Service Bus namespaces, you can use the [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="d23af-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span><span class="sxs-lookup"><span data-stu-id="d23af-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="d23af-121">`$Namespace` is the name of the Service Bus namespace with which we want to work.</span><span class="sxs-lookup"><span data-stu-id="d23af-121">`$Namespace` is the name of the Service Bus namespace with which we want to work.</span></span>
* <span data-ttu-id="d23af-122">`$Location` identifies the data center in which will we provision the namespace.</span><span class="sxs-lookup"><span data-stu-id="d23af-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="d23af-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span><span class="sxs-lookup"><span data-stu-id="d23af-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="d23af-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span><span class="sxs-lookup"><span data-stu-id="d23af-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="d23af-125">This part of the script does the following:</span><span class="sxs-lookup"><span data-stu-id="d23af-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="d23af-126">Attempts to retrieve a Service Bus namespace with the specified name.</span><span class="sxs-lookup"><span data-stu-id="d23af-126">Attempts to retrieve a Service Bus namespace with the specified name.</span></span>
2. <span data-ttu-id="d23af-127">If the namespace is found, it reports what was found.</span><span class="sxs-lookup"><span data-stu-id="d23af-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="d23af-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span><span class="sxs-lookup"><span data-stu-id="d23af-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>
   
    ``` powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="d23af-129">Create a namespace authorization rule</span><span class="sxs-lookup"><span data-stu-id="d23af-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="d23af-130">The following example shows how to manage namespace authorization rules using the [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="d23af-130">The following example shows how to manage namespace authorization rules using the [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query to see if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if the rule already exists or needs to be created
if ($CurrentRule)
{
    Write-Host "The $AuthRule rule already exists for the namespace $Namespace."
}
else
{
    Write-Host "The $AuthRule rule does not exist."
    Write-Host "Creating the $AuthRule rule for the $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "The $AuthRule rule for the $Namespace namespace has been successfully created."

    Write-Host "Setting rights on the namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights to the namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a><span data-ttu-id="d23af-131">Create a queue</span><span class="sxs-lookup"><span data-stu-id="d23af-131">Create a queue</span></span>

<span data-ttu-id="d23af-132">To create a queue or topic, perform a namespace check using the script in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d23af-132">To create a queue or topic, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="d23af-133">Then, create the queue:</span><span class="sxs-lookup"><span data-stu-id="d23af-133">Then, create the queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "The queue $QueueName already exists in the $Location region:"
}
else
{
    Write-Host "The $QueueName queue does not exist."
    Write-Host "Creating the $QueueName queue in the $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "The $QueueName queue in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="d23af-134">Modify queue properties</span><span class="sxs-lookup"><span data-stu-id="d23af-134">Modify queue properties</span></span>

<span data-ttu-id="d23af-135">After executing the script in the preceding section, you can use the [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet to update the properties of a queue, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="d23af-135">After executing the script in the preceding section, you can use the [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet to update the properties of a queue, as in the following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="d23af-136">Provisioning other Service Bus entities</span><span class="sxs-lookup"><span data-stu-id="d23af-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="d23af-137">You can use the [Service Bus PowerShell module](/powershell/module/azurerm.servicebus/?view=azurermps-3.7.0#service_bus) to provision other entities, such as topics and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="d23af-137">You can use the [Service Bus PowerShell module](/powershell/module/azurerm.servicebus/?view=azurermps-3.7.0#service_bus) to provision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="d23af-138">These cmdlets are syntactically similar to the queue creation cmdlets demonstrated in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d23af-138">These cmdlets are syntactically similar to the queue creation cmdlets demonstrated in the previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d23af-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="d23af-139">Next steps</span></span>

- <span data-ttu-id="d23af-140">See the complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus/?view=azurermps-3.7.0#service_bus).</span><span class="sxs-lookup"><span data-stu-id="d23af-140">See the complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus/?view=azurermps-3.7.0#service_bus).</span></span> <span data-ttu-id="d23af-141">This page lists all available cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d23af-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="d23af-142">For information about using Azure Resource Manager templates, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d23af-142">For information about using Azure Resource Manager templates, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="d23af-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="d23af-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="d23af-144">There are some alternate ways to manage Service Bus entities, as described in these blog posts:</span><span class="sxs-lookup"><span data-stu-id="d23af-144">There are some alternate ways to manage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="d23af-145">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="d23af-145">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="d23af-146">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="d23af-146">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="d23af-147">Service Bus PowerShell Scripts</span><span class="sxs-lookup"><span data-stu-id="d23af-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
