---
title: Scale an Azure cloud service in Windows PowerShell | Microsoft Docs
description: (classic) Learn how to use PowerShell to scale a web role or worker role in or out in Azure.
services: cloud-services
documentationcenter: ''
author: seanmck
manager: timlt
editor: ''
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: seanmck
ms.openlocfilehash: 21156462b6565acad9d8d12ff9f7ec0c0a72e736
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552465"
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a><span data-ttu-id="83931-103">How to scale a cloud service in PowerShell</span><span class="sxs-lookup"><span data-stu-id="83931-103">How to scale a cloud service in PowerShell</span></span>

<span data-ttu-id="83931-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span><span class="sxs-lookup"><span data-stu-id="83931-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="83931-105">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="83931-105">Log in to Azure</span></span>

<span data-ttu-id="83931-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span><span class="sxs-lookup"><span data-stu-id="83931-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="83931-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span><span class="sxs-lookup"><span data-stu-id="83931-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="83931-108">To check the current subscription, run:</span><span class="sxs-lookup"><span data-stu-id="83931-108">To check the current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="83931-109">If you need to change the current subscription, run:</span><span class="sxs-lookup"><span data-stu-id="83931-109">If you need to change the current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a><span data-ttu-id="83931-110">Check the current instance count for your role</span><span class="sxs-lookup"><span data-stu-id="83931-110">Check the current instance count for your role</span></span>

<span data-ttu-id="83931-111">To check the current state of your role, run:</span><span class="sxs-lookup"><span data-stu-id="83931-111">To check the current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="83931-112">You should get back information about the role, including its current OS version and instance count.</span><span class="sxs-lookup"><span data-stu-id="83931-112">You should get back information about the role, including its current OS version and instance count.</span></span> <span data-ttu-id="83931-113">In this case, the role has a single instance.</span><span class="sxs-lookup"><span data-stu-id="83931-113">In this case, the role has a single instance.</span></span>

![Information about the role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-powershell/get-azure-role.PNG)

## <a name="scale-out-the-role-by-adding-more-instances"></a><span data-ttu-id="83931-115">Scale out the role by adding more instances</span><span class="sxs-lookup"><span data-stu-id="83931-115">Scale out the role by adding more instances</span></span>

<span data-ttu-id="83931-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="83931-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="83931-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span><span class="sxs-lookup"><span data-stu-id="83931-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span></span> <span data-ttu-id="83931-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span><span class="sxs-lookup"><span data-stu-id="83931-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span></span> <span data-ttu-id="83931-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span><span class="sxs-lookup"><span data-stu-id="83931-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span></span>

![VM instance starting in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-powershell/role-instance-starting.PNG)

<span data-ttu-id="83931-121">Once the new instances have started, the cmdlet will return successfully:</span><span class="sxs-lookup"><span data-stu-id="83931-121">Once the new instances have started, the cmdlet will return successfully:</span></span>

![Role instance increase success](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-powershell/set-azure-role-success.PNG)

## <a name="scale-in-the-role-by-removing-instances"></a><span data-ttu-id="83931-123">Scale in the role by removing instances</span><span class="sxs-lookup"><span data-stu-id="83931-123">Scale in the role by removing instances</span></span>

<span data-ttu-id="83931-124">You can scale in a role by removing instances in the same way.</span><span class="sxs-lookup"><span data-stu-id="83931-124">You can scale in a role by removing instances in the same way.</span></span> <span data-ttu-id="83931-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span><span class="sxs-lookup"><span data-stu-id="83931-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83931-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="83931-126">Next steps</span></span>

<span data-ttu-id="83931-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83931-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="83931-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="83931-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>



