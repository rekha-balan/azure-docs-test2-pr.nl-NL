---
title: Deploy and Manage Notification Hubs using PowerShell
description: How to Create and Manage Notification Hubs Using PowerShell for Automation
services: notification-hubs
documentationcenter: ''
author: ysxu
manager: erikre
editor: ''
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 4db058e4bd91dc287b14e887abc6c378c65c4a2b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662594"
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="439dd-103">Deploy and Manage Notification Hubs using PowerShell</span><span class="sxs-lookup"><span data-stu-id="439dd-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="439dd-104">Overview</span><span class="sxs-lookup"><span data-stu-id="439dd-104">Overview</span></span>
<span data-ttu-id="439dd-105">This article shows you how to use Create and Manage Azure Notification Hubs using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="439dd-105">This article shows you how to use Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="439dd-106">The following common automation tasks are shown in this topic.</span><span class="sxs-lookup"><span data-stu-id="439dd-106">The following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="439dd-107">Create a Notification Hub</span><span class="sxs-lookup"><span data-stu-id="439dd-107">Create a Notification Hub</span></span>
* <span data-ttu-id="439dd-108">Set Credentials</span><span class="sxs-lookup"><span data-stu-id="439dd-108">Set Credentials</span></span>

<span data-ttu-id="439dd-109">If you also need to create a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="439dd-109">If you also need to create a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="439dd-110">Managing Notifications Hubs is not supported directly by the cmdlets included with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="439dd-110">Managing Notifications Hubs is not supported directly by the cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="439dd-111">The best approach from PowerShell is to reference the Microsoft.Azure.NotificationHubs.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="439dd-111">The best approach from PowerShell is to reference the Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="439dd-112">The assembly is distributed with the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="439dd-112">The assembly is distributed with the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="439dd-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="439dd-113">Prerequisites</span></span>
<span data-ttu-id="439dd-114">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="439dd-114">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="439dd-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="439dd-115">An Azure subscription.</span></span> <span data-ttu-id="439dd-116">Azure is a subscription-based platform.</span><span class="sxs-lookup"><span data-stu-id="439dd-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="439dd-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span><span class="sxs-lookup"><span data-stu-id="439dd-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="439dd-118">A computer with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="439dd-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="439dd-119">For instructions, see [Install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="439dd-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="439dd-120">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="439dd-120">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="including-a-reference-to-the-net-assembly-for-service-bus"></a><span data-ttu-id="439dd-121">Including a reference to the .NET assembly for Service Bus</span><span class="sxs-lookup"><span data-stu-id="439dd-121">Including a reference to the .NET assembly for Service Bus</span></span>
<span data-ttu-id="439dd-122">Managing Azure Notification Hubs is not yet included with the PowerShell cmdlets in Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="439dd-122">Managing Azure Notification Hubs is not yet included with the PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="439dd-123">To provision notification hubs, you can use the .NET client provided in the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="439dd-123">To provision notification hubs, you can use the .NET client provided in the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="439dd-124">First, make sure your script can locate the **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="439dd-124">First, make sure your script can locate the **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="439dd-125">In order to be flexible, the script performs these steps:</span><span class="sxs-lookup"><span data-stu-id="439dd-125">In order to be flexible, the script performs these steps:</span></span>

1. <span data-ttu-id="439dd-126">Determines the path at which it was invoked.</span><span class="sxs-lookup"><span data-stu-id="439dd-126">Determines the path at which it was invoked.</span></span>
2. <span data-ttu-id="439dd-127">Traverses the path until it finds a folder named `packages`.</span><span class="sxs-lookup"><span data-stu-id="439dd-127">Traverses the path until it finds a folder named `packages`.</span></span> <span data-ttu-id="439dd-128">This folder is created when you install NuGet packages for Visual Studio projects.</span><span class="sxs-lookup"><span data-stu-id="439dd-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="439dd-129">Recursively searches the `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="439dd-129">Recursively searches the `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="439dd-130">References the assembly so that the types are available for later use.</span><span class="sxs-lookup"><span data-stu-id="439dd-130">References the assembly so that the types are available for later use.</span></span>

<span data-ttu-id="439dd-131">Here's how these steps are implemented in a PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="439dd-131">Here's how these steps are implemented in a PowerShell script:</span></span>

``` powershell

try
{
    # WARNING: Make sure to reference the latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding the [Microsoft.Azure.NotificationHubs.dll] assembly to the script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "The [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added to the script."
}

catch [System.Exception]
{
    Write-Error("Could not add the Microsoft.Azure.NotificationHubs.dll assembly to the script. Make sure you build the solution before running the provisioning script.")
}
```

## <a name="create-the-namespacemanager-class"></a><span data-ttu-id="439dd-132">Create the NamespaceManager class</span><span class="sxs-lookup"><span data-stu-id="439dd-132">Create the NamespaceManager class</span></span>
<span data-ttu-id="439dd-133">To provision Notification Hubs, create an instance of the [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from the SDK.</span><span class="sxs-lookup"><span data-stu-id="439dd-133">To provision Notification Hubs, create an instance of the [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from the SDK.</span></span> 

<span data-ttu-id="439dd-134">You can use the [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell to retrieve an authorization rule that's used to provide a connection string.</span><span class="sxs-lookup"><span data-stu-id="439dd-134">You can use the [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell to retrieve an authorization rule that's used to provide a connection string.</span></span> <span data-ttu-id="439dd-135">We'll store a reference to the `NamespaceManager` instance in the `$NamespaceManager` variable.</span><span class="sxs-lookup"><span data-stu-id="439dd-135">We'll store a reference to the `NamespaceManager` instance in the `$NamespaceManager` variable.</span></span> <span data-ttu-id="439dd-136">We will use `$NamespaceManager` to provision a notification hub.</span><span class="sxs-lookup"><span data-stu-id="439dd-136">We will use `$NamespaceManager` to provision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create the NamespaceManager object to create the hub
Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="439dd-137">Provisioning a new Notification Hub</span><span class="sxs-lookup"><span data-stu-id="439dd-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="439dd-138">To provision a new notification hub, use the [.NET API for Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="439dd-138">To provision a new notification hub, use the [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="439dd-139">In this part of the script you set up four local variables.</span><span class="sxs-lookup"><span data-stu-id="439dd-139">In this part of the script you set up four local variables.</span></span> 

1. <span data-ttu-id="439dd-140">`$Namespace` : Set this to the name of the namespace where you want to create a notification hub.</span><span class="sxs-lookup"><span data-stu-id="439dd-140">`$Namespace` : Set this to the name of the namespace where you want to create a notification hub.</span></span>
2. <span data-ttu-id="439dd-141">`$Path` : Set this path to the name of the new notification hub.</span><span class="sxs-lookup"><span data-stu-id="439dd-141">`$Path` : Set this path to the name of the new notification hub.</span></span>  <span data-ttu-id="439dd-142">For example, "MyHub".</span><span class="sxs-lookup"><span data-stu-id="439dd-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="439dd-143">`$WnsPackageSid` : Set this to the package SID for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="439dd-143">`$WnsPackageSid` : Set this to the package SID for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="439dd-144">`$WnsSecretkey`: Set this to the secret key for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="439dd-144">`$WnsSecretkey`: Set this to the secret key for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="439dd-145">These variables are used to connect to your namespace and create a new Notification Hub configured to handle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span><span class="sxs-lookup"><span data-stu-id="439dd-145">These variables are used to connect to your namespace and create a new Notification Hub configured to handle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="439dd-146">For information on obtaining the package SID and secret key see, the [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="439dd-146">For information on obtaining the package SID and secret key see, the [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="439dd-147">The script snippet uses the `NamespaceManager` object to check to see if the Notification Hub identified by `$Path` exists.</span><span class="sxs-lookup"><span data-stu-id="439dd-147">The script snippet uses the `NamespaceManager` object to check to see if the Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="439dd-148">If it does not exist, the script will create an `NotificationHubDescription` with WNS credentials and pass that to the `NamespaceManager` class `CreateNotificationHub` method.</span><span class="sxs-lookup"><span data-stu-id="439dd-148">If it does not exist, the script will create an `NotificationHubDescription` with WNS credentials and pass that to the `NamespaceManager` class `CreateNotificationHub` method.</span></span>

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query the namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if the namespace already exists
if ($CurrentNamespace)
{
    Write-Output "The namespace [$Namespace] in the [$($CurrentNamespace.Region)] region was found."

    # Create the NamespaceManager object used to create a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."

    # Check to see if the Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "The [$Path] notification hub already exists in the [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating the [$Path] notification hub in the [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "The [$Path] notification hub was created in the [$Namespace] namespace."
    }
}
else
{
    Write-Host "The [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a><span data-ttu-id="439dd-149">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="439dd-149">Additional Resources</span></span>
* [<span data-ttu-id="439dd-150">Manage Service Bus with PowerShell</span><span class="sxs-lookup"><span data-stu-id="439dd-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="439dd-151">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="439dd-151">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="439dd-152">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="439dd-152">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="439dd-153">Some ready-made scripts are also available for download:</span><span class="sxs-lookup"><span data-stu-id="439dd-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="439dd-154">Service Bus PowerShell Scripts</span><span class="sxs-lookup"><span data-stu-id="439dd-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Purchase Options]: http://azure.microsoft.com/pricing/purchase-options/
[Member Offers]: http://azure.microsoft.com/pricing/member-offers/
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[.NET API for Notification Hubs]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

