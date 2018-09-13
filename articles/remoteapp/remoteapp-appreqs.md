---
title: App requirements for Azure RemoteApp | Microsoft Docs
description: Learn about the requirements for apps that you want to use in Azure RemoteApp
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a9a305e4c07e2c348b1c1503d53f1da05da57966
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553597"
---
# <a name="app-requirements"></a><span data-ttu-id="7ef6c-103">App requirements</span><span class="sxs-lookup"><span data-stu-id="7ef6c-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7ef6c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7ef6c-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7ef6c-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="7ef6c-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="7ef6c-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="7ef6c-109">The following information provides guidance for developing applications in a Remote Desktop Services environment and testing to ensure compatibility.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-109">The following information provides guidance for developing applications in a Remote Desktop Services environment and testing to ensure compatibility.</span></span>

<span data-ttu-id="7ef6c-110">Tip: We're working on creating some working examples of apps for you.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="7ef6c-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="7ef6c-112">Requirements</span><span class="sxs-lookup"><span data-stu-id="7ef6c-112">Requirements</span></span>
<span data-ttu-id="7ef6c-113">These three requirements, if followed, help your application run well in RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="7ef6c-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="7ef6c-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere to [Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere to [Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="7ef6c-115">Applications should never store data locally on the image or RemoteApp instances that can be lost.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-115">Applications should never store data locally on the image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="7ef6c-116">After you create a RemoteApp collection, the instances are cloned and are stateless and should only contain applications.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-116">After you create a RemoteApp collection, the instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="7ef6c-117">Store data in an external source or within the user's profile.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-117">Store data in an external source or within the user's profile.</span></span>
3. <span data-ttu-id="7ef6c-118">Custom images should never contain data that can be lost.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="7ef6c-119">Testing your apps</span><span class="sxs-lookup"><span data-stu-id="7ef6c-119">Testing your apps</span></span>
<span data-ttu-id="7ef6c-120">Use these steps to testing applications:</span><span class="sxs-lookup"><span data-stu-id="7ef6c-120">Use these steps to testing applications:</span></span>

1. <span data-ttu-id="7ef6c-121">Install Windows Server 2012 R2 and your application</span><span class="sxs-lookup"><span data-stu-id="7ef6c-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="7ef6c-122">Enable Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="7ef6c-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="7ef6c-123">Create two user accounts, UserA and UserB, adding both user accounts to the Remote Desktop security group.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-123">Create two user accounts, UserA and UserB, adding both user accounts to the Remote Desktop security group.</span></span>
4. <span data-ttu-id="7ef6c-124">Check multi-session compatibility by establishing two simultaneous RDS sessions to the PC while launching the application.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-124">Check multi-session compatibility by establishing two simultaneous RDS sessions to the PC while launching the application.</span></span>
5. <span data-ttu-id="7ef6c-125">Validate app behavior</span><span class="sxs-lookup"><span data-stu-id="7ef6c-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="7ef6c-126">Application development guidelines</span><span class="sxs-lookup"><span data-stu-id="7ef6c-126">Application development guidelines</span></span>
<span data-ttu-id="7ef6c-127">Use the following guidelines for developing applications for RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-127">Use the following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="7ef6c-128">Multiple users</span><span class="sxs-lookup"><span data-stu-id="7ef6c-128">Multiple users</span></span>
* <span data-ttu-id="7ef6c-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="7ef6c-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies to all users.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies to all users.</span></span>
* <span data-ttu-id="7ef6c-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="7ef6c-132">It is not safe to assume that the computer name or the [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned to the computer are associated with a single user because multiple users can be logged on simultaneously to a Remote Desktop Session Host (RD Session Host) server.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-132">It is not safe to assume that the computer name or the [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned to the computer are associated with a single user because multiple users can be logged on simultaneously to a Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="7ef6c-133">Performance</span><span class="sxs-lookup"><span data-stu-id="7ef6c-133">Performance</span></span>
* <span data-ttu-id="7ef6c-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app to RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app to RemoteApp.</span></span>
* <span data-ttu-id="7ef6c-135">To maximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-135">To maximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="7ef6c-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="7ef6c-137">To optimize performance, it is good practice for applications to [detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span><span class="sxs-lookup"><span data-stu-id="7ef6c-137">To optimize performance, it is good practice for applications to [detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

