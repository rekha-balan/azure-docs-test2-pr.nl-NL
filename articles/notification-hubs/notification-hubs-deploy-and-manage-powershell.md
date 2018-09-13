---
title: Deploy and Manage Notification Hubs using PowerShell
description: How to Create and Manage Notification Hubs Using PowerShell for Automation
services: notification-hubs
documentationcenter: ''
author: dimazaid
manager: kpiteira
editor: spelluru
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: 5a134e14768e0576c501232b6aedb1f836bc05b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774962"
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="edbe0-103">Deploy and Manage Notification Hubs using PowerShell</span><span class="sxs-lookup"><span data-stu-id="edbe0-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="edbe0-104">Overview</span><span class="sxs-lookup"><span data-stu-id="edbe0-104">Overview</span></span>
<span data-ttu-id="edbe0-105">This article shows you how to use Create and Manage Azure Notification Hubs using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edbe0-105">This article shows you how to use Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="edbe0-106">The following common automation tasks are shown in this article.</span><span class="sxs-lookup"><span data-stu-id="edbe0-106">The following common automation tasks are shown in this article.</span></span>

* <span data-ttu-id="edbe0-107">Create a Notification Hub</span><span class="sxs-lookup"><span data-stu-id="edbe0-107">Create a Notification Hub</span></span>
* <span data-ttu-id="edbe0-108">Set Credentials</span><span class="sxs-lookup"><span data-stu-id="edbe0-108">Set Credentials</span></span>

<span data-ttu-id="edbe0-109">If you also need to create a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="edbe0-109">If you also need to create a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="edbe0-110">Managing Notifications Hubs is not supported directly by the cmdlets included with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edbe0-110">Managing Notifications Hubs is not supported directly by the cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="edbe0-111">The best approach from PowerShell is to reference the Microsoft.Azure.NotificationHubs.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="edbe0-111">The best approach from PowerShell is to reference the Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="edbe0-112">The assembly is distributed with the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="edbe0-112">The assembly is distributed with the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edbe0-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="edbe0-113">Prerequisites</span></span>

* <span data-ttu-id="edbe0-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="edbe0-114">An Azure subscription.</span></span> <span data-ttu-id="edbe0-115">Azure is a subscription-based platform.</span><span class="sxs-lookup"><span data-stu-id="edbe0-115">Azure is a subscription-based platform.</span></span> <span data-ttu-id="edbe0-116">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span><span class="sxs-lookup"><span data-stu-id="edbe0-116">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="edbe0-117">A computer with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edbe0-117">A computer with Azure PowerShell.</span></span> <span data-ttu-id="edbe0-118">For instructions, see [Install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="edbe0-118">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="edbe0-119">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="edbe0-119">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="including-a-reference-to-the-net-assembly-for-service-bus"></a><span data-ttu-id="edbe0-120">Including a reference to the .NET assembly for Service Bus</span><span class="sxs-lookup"><span data-stu-id="edbe0-120">Including a reference to the .NET assembly for Service Bus</span></span>
<span data-ttu-id="edbe0-121">Managing Azure Notification Hubs is not yet included with the PowerShell cmdlets in Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edbe0-121">Managing Azure Notification Hubs is not yet included with the PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="edbe0-122">To provision notification hubs, you can use the .NET client provided in the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="edbe0-122">To provision notification hubs, you can use the .NET client provided in the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="edbe0-123">First, make sure your script can locate the **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="edbe0-123">First, make sure your script can locate the **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="edbe0-124">In order to be flexible, the script performs these steps:</span><span class="sxs-lookup"><span data-stu-id="edbe0-124">In order to be flexible, the script performs these steps:</span></span>

1. <span data-ttu-id="edbe0-125">Determines the path at which it was invoked.</span><span class="sxs-lookup"><span data-stu-id="edbe0-125">Determines the path at which it was invoked.</span></span>
2. <span data-ttu-id="edbe0-126">Traverses the path until it finds a folder named `packages`.</span><span class="sxs-lookup"><span data-stu-id="edbe0-126">Traverses the path until it finds a folder named `packages`.</span></span> <span data-ttu-id="edbe0-127">This folder is created when you install NuGet packages for Visual Studio projects.</span><span class="sxs-lookup"><span data-stu-id="edbe0-127">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="edbe0-128">Recursively searches the `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="edbe0-128">Recursively searches the `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="edbe0-129">References the assembly so that the types are available for later use.</span><span class="sxs-lookup"><span data-stu-id="edbe0-129">References the assembly so that the types are available for later use.</span></span>

<span data-ttu-id="edbe0-130">Here's how these steps are implemented in a PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="edbe0-130">Here's how these steps are implemented in a PowerShell script:</span></span>

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

## <a name="create-the-namespacemanager-class"></a><span data-ttu-id="edbe0-131">Create the NamespaceManager class</span><span class="sxs-lookup"><span data-stu-id="edbe0-131">Create the NamespaceManager class</span></span>
<span data-ttu-id="edbe0-132">To provision Notification Hubs, create an instance of the [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from the SDK.</span><span class="sxs-lookup"><span data-stu-id="edbe0-132">To provision Notification Hubs, create an instance of the [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from the SDK.</span></span> 

<span data-ttu-id="edbe0-133">You can use the [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell to retrieve an authorization rule that's used to provide a connection string.</span><span class="sxs-lookup"><span data-stu-id="edbe0-133">You can use the [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell to retrieve an authorization rule that's used to provide a connection string.</span></span> <span data-ttu-id="edbe0-134">A reference to the `NamespaceManager` instance is stored in the `$NamespaceManager` variable.</span><span class="sxs-lookup"><span data-stu-id="edbe0-134">A reference to the `NamespaceManager` instance is stored in the `$NamespaceManager` variable.</span></span> <span data-ttu-id="edbe0-135">`$NamespaceManager` is used to provision a notification hub.</span><span class="sxs-lookup"><span data-stu-id="edbe0-135">`$NamespaceManager` is used to provision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create the NamespaceManager object to create the hub
Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="edbe0-136">Provisioning a new Notification Hub</span><span class="sxs-lookup"><span data-stu-id="edbe0-136">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="edbe0-137">To provision a new notification hub, use the [.NET API for Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="edbe0-137">To provision a new notification hub, use the [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="edbe0-138">In this part of the script, you set up four local variables.</span><span class="sxs-lookup"><span data-stu-id="edbe0-138">In this part of the script, you set up four local variables.</span></span> 

1. <span data-ttu-id="edbe0-139">`$Namespace`: Set this to the name of the namespace where you want to create a notification hub.</span><span class="sxs-lookup"><span data-stu-id="edbe0-139">`$Namespace`: Set this to the name of the namespace where you want to create a notification hub.</span></span>
2. <span data-ttu-id="edbe0-140">`$Path`: Set this path to the name of the new notification hub.</span><span class="sxs-lookup"><span data-stu-id="edbe0-140">`$Path`: Set this path to the name of the new notification hub.</span></span>  <span data-ttu-id="edbe0-141">For example, "MyHub".</span><span class="sxs-lookup"><span data-stu-id="edbe0-141">For example, "MyHub".</span></span>    
3. <span data-ttu-id="edbe0-142">`$WnsPackageSid`: Set this to the package SID for your Windows App from the [Windows Dev Center](https://developer.microsoft.com/en-us/windows).</span><span class="sxs-lookup"><span data-stu-id="edbe0-142">`$WnsPackageSid`: Set this to the package SID for your Windows App from the [Windows Dev Center](https://developer.microsoft.com/en-us/windows).</span></span>
4. <span data-ttu-id="edbe0-143">`$WnsSecretkey`: Set this to the secret key for your Windows App from the [Windows Dev Center](https://developer.microsoft.com/en-us/windows).</span><span class="sxs-lookup"><span data-stu-id="edbe0-143">`$WnsSecretkey`: Set this to the secret key for your Windows App from the [Windows Dev Center](https://developer.microsoft.com/en-us/windows).</span></span>

<span data-ttu-id="edbe0-144">These variables are used to connect to your namespace and create a new Notification Hub configured to handle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span><span class="sxs-lookup"><span data-stu-id="edbe0-144">These variables are used to connect to your namespace and create a new Notification Hub configured to handle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="edbe0-145">For information on obtaining the package SID and secret key see, the [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="edbe0-145">For information on obtaining the package SID and secret key see, the [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="edbe0-146">The script snippet uses the `NamespaceManager` object to check to see if the Notification Hub identified by `$Path` exists.</span><span class="sxs-lookup"><span data-stu-id="edbe0-146">The script snippet uses the `NamespaceManager` object to check to see if the Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="edbe0-147">If it does not exist, the script creates `NotificationHubDescription` with WNS credentials and passes it to the `NamespaceManager` class `CreateNotificationHub` method.</span><span class="sxs-lookup"><span data-stu-id="edbe0-147">If it does not exist, the script creates `NotificationHubDescription` with WNS credentials and passes it to the `NamespaceManager` class `CreateNotificationHub` method.</span></span>

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




## <a name="additional-resources"></a><span data-ttu-id="edbe0-148">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="edbe0-148">Additional Resources</span></span>
* [<span data-ttu-id="edbe0-149">Manage Service Bus with PowerShell</span><span class="sxs-lookup"><span data-stu-id="edbe0-149">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="edbe0-150">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="edbe0-150">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="edbe0-151">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="edbe0-151">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="edbe0-152">Some ready-made scripts are also available for download:</span><span class="sxs-lookup"><span data-stu-id="edbe0-152">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="edbe0-153">Service Bus PowerShell Scripts</span><span class="sxs-lookup"><span data-stu-id="edbe0-153">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Purchase Options]: http://azure.microsoft.com/pricing/purchase-options/
[Member Offers]: http://azure.microsoft.com/pricing/member-offers/
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[.NET API for Notification Hubs]: https://docs.microsoft.com/en-us/dotnet/api/overview/azure/notification-hubs?view=azure-dotnet
[Get-AzureSBNamespace]: https://docs.microsoft.com/powershell/module/servicemanagement/azure/get-azuresbnamespace
[New-AzureSBNamespace]: https://docs.microsoft.com/powershell/module/servicemanagement/azure/new-azuresbnamespace
[Get-AzureSBAuthorizationRule]: https://docs.microsoft.com/powershell/module/servicemanagement/azure/get-azuresbauthorizationrule

