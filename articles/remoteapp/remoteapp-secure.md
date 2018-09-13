---
title: Secure apps and resources in Azure RemoteApp | Microsoft Docs
description: Learn how to lock down apps and resources in Azure RemoteApp
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 13085f51529dadb739b4c629bb50d8aff0c9d8c2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564476"
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a><span data-ttu-id="89064-103">Secure apps and resources in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="89064-103">Secure apps and resources in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="89064-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="89064-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="89064-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="89064-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="89064-106">Azure RemoteApp provides users access to centrally-managed Windows apps, which lets you control what your users can and can't do.</span><span class="sxs-lookup"><span data-stu-id="89064-106">Azure RemoteApp provides users access to centrally-managed Windows apps, which lets you control what your users can and can't do.</span></span>  <span data-ttu-id="89064-107">This is particularly useful when the user is connecting from an unmanaged device (like their personal Macbook) and you want to control the user access or experience.</span><span class="sxs-lookup"><span data-stu-id="89064-107">This is particularly useful when the user is connecting from an unmanaged device (like their personal Macbook) and you want to control the user access or experience.</span></span>

<span data-ttu-id="89064-108">For example, if you are using Active Directory for user authentication and you want to prevent your users from copying data out of an app, you can configure a Remote Desktop Group Policy to block users from copying data.</span><span class="sxs-lookup"><span data-stu-id="89064-108">For example, if you are using Active Directory for user authentication and you want to prevent your users from copying data out of an app, you can configure a Remote Desktop Group Policy to block users from copying data.</span></span>

<span data-ttu-id="89064-109">Another example is if you want to block internet access for a particular app in your collection.</span><span class="sxs-lookup"><span data-stu-id="89064-109">Another example is if you want to block internet access for a particular app in your collection.</span></span> <span data-ttu-id="89064-110">You can create a Windows Firewall rule that blocks the access when you create the image for your collection.</span><span class="sxs-lookup"><span data-stu-id="89064-110">You can create a Windows Firewall rule that blocks the access when you create the image for your collection.</span></span>

## <a name="implementation-options"></a><span data-ttu-id="89064-111">Implementation options</span><span class="sxs-lookup"><span data-stu-id="89064-111">Implementation options</span></span>
  <span data-ttu-id="89064-112">Here are the key implementation options, which can be used individually or in tandem as needed:</span><span class="sxs-lookup"><span data-stu-id="89064-112">Here are the key implementation options, which can be used individually or in tandem as needed:</span></span>

1. <span data-ttu-id="89064-113">If your RemoteApp collection is domain joined you can enforce any [Group Policy](https://technet.microsoft.com/library/cc725828.aspx) (with the exception of the Idle and Disconnect timeout policies described [here](../azure-subscription-service-limits.md)).</span><span class="sxs-lookup"><span data-stu-id="89064-113">If your RemoteApp collection is domain joined you can enforce any [Group Policy](https://technet.microsoft.com/library/cc725828.aspx) (with the exception of the Idle and Disconnect timeout policies described [here](../azure-subscription-service-limits.md)).</span></span>
2. <span data-ttu-id="89064-114">As an alternative to Group Policy (if your collection is not domain joined or you don't have the right privileges in AD), you can configure [Local Polices](https://technet.microsoft.com/library/cc775702.aspx) into your template image.</span><span class="sxs-lookup"><span data-stu-id="89064-114">As an alternative to Group Policy (if your collection is not domain joined or you don't have the right privileges in AD), you can configure [Local Polices](https://technet.microsoft.com/library/cc775702.aspx) into your template image.</span></span>  <span data-ttu-id="89064-115">Note that group polices trump local policies when there is a conflict.</span><span class="sxs-lookup"><span data-stu-id="89064-115">Note that group polices trump local policies when there is a conflict.</span></span>
3. <span data-ttu-id="89064-116">Some OS/app settings are not configurable via policy, but can be via registry key using the [RegEdit tool](remoteapp-hybridtrouble.md) while configuring your template image.</span><span class="sxs-lookup"><span data-stu-id="89064-116">Some OS/app settings are not configurable via policy, but can be via registry key using the [RegEdit tool](remoteapp-hybridtrouble.md) while configuring your template image.</span></span>
4. <span data-ttu-id="89064-117">You can use [Windows Firewall](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) to control network access to and from the machine where the app is running.</span><span class="sxs-lookup"><span data-stu-id="89064-117">You can use [Windows Firewall](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) to control network access to and from the machine where the app is running.</span></span> <span data-ttu-id="89064-118">Just make sure you don't block the URLs and ports defined here.</span><span class="sxs-lookup"><span data-stu-id="89064-118">Just make sure you don't block the URLs and ports defined here.</span></span>
5. <span data-ttu-id="89064-119">You can use [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) to control which applications and files users can run.</span><span class="sxs-lookup"><span data-stu-id="89064-119">You can use [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) to control which applications and files users can run.</span></span> <span data-ttu-id="89064-120">For example, savvy users can figure out how to run applications that you did not publish but that are available in the image you used to create the collection - AppLocker can block this.</span><span class="sxs-lookup"><span data-stu-id="89064-120">For example, savvy users can figure out how to run applications that you did not publish but that are available in the image you used to create the collection - AppLocker can block this.</span></span>

## <a name="detailed-information"></a><span data-ttu-id="89064-121">Detailed information</span><span class="sxs-lookup"><span data-stu-id="89064-121">Detailed information</span></span>
* <span data-ttu-id="89064-122">The following RDS policies are likely to be most useful:</span><span class="sxs-lookup"><span data-stu-id="89064-122">The following RDS policies are likely to be most useful:</span></span>
  * [<span data-ttu-id="89064-123">Device and Resource Redirection</span><span class="sxs-lookup"><span data-stu-id="89064-123">Device and Resource Redirection</span></span>](https://technet.microsoft.com/library/ee791794.aspx)
  * [<span data-ttu-id="89064-124">Printer Redirection</span><span class="sxs-lookup"><span data-stu-id="89064-124">Printer Redirection</span></span>](https://technet.microsoft.com/library/ee791784.aspx)
  * <span data-ttu-id="89064-125">[Profiles](https://technet.microsoft.com/library/ee791865.aspx).</span><span class="sxs-lookup"><span data-stu-id="89064-125">[Profiles](https://technet.microsoft.com/library/ee791865.aspx).</span></span>
* <span data-ttu-id="89064-126">Note that configuring redirections via the RemoteApp PowerShell module (as seen [here](remoteapp-redirection.md)) relies on the client machine to enforce the policy, so if security is the primary objective you'll want to enforce the policy via the template image local policy or via group policy.</span><span class="sxs-lookup"><span data-stu-id="89064-126">Note that configuring redirections via the RemoteApp PowerShell module (as seen [here](remoteapp-redirection.md)) relies on the client machine to enforce the policy, so if security is the primary objective you'll want to enforce the policy via the template image local policy or via group policy.</span></span>
* <span data-ttu-id="89064-127">[Windows Server 2012 R2 policies](https://technet.microsoft.com/library/hh831791.aspx).</span><span class="sxs-lookup"><span data-stu-id="89064-127">[Windows Server 2012 R2 policies](https://technet.microsoft.com/library/hh831791.aspx).</span></span>
* <span data-ttu-id="89064-128">[Office 2013 polices](https://technet.microsoft.com/library/cc178969.aspx) (including [how to customize the Office toolbar](https://technet.microsoft.com/library/cc179143.aspx)).</span><span class="sxs-lookup"><span data-stu-id="89064-128">[Office 2013 polices](https://technet.microsoft.com/library/cc178969.aspx) (including [how to customize the Office toolbar](https://technet.microsoft.com/library/cc179143.aspx)).</span></span>

