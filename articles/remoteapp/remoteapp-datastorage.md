---
title: Never store sensitive data on custom images for Azure RemoteApp | Microsoft Docs
description: Learn about the guidelines for storing data in custom images in Azure RemoteApp
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548747"
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="cb3d1-103">Never store sensitive data on custom images</span><span class="sxs-lookup"><span data-stu-id="cb3d1-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cb3d1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cb3d1-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cb3d1-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span></span> <span data-ttu-id="cb3d1-107">We use that custom image to create VM instances that serve your apps to your users.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-107">We use that custom image to create VM instances that serve your apps to your users.</span></span> <span data-ttu-id="cb3d1-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="cb3d1-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="cb3d1-110">The image should just host the application that connects to the data source and presents the data.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-110">The image should just host the application that connects to the data source and presents the data.</span></span> <span data-ttu-id="cb3d1-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="cb3d1-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span></span> <span data-ttu-id="cb3d1-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span></span> <span data-ttu-id="cb3d1-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span></span> <span data-ttu-id="cb3d1-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="cb3d1-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="cb3d1-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="cb3d1-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span></span> <span data-ttu-id="cb3d1-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="cb3d1-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="cb3d1-120">Example data that should not reside in the image:</span><span class="sxs-lookup"><span data-stu-id="cb3d1-120">Example data that should not reside in the image:</span></span>

* <span data-ttu-id="cb3d1-121">Shared data for users to access</span><span class="sxs-lookup"><span data-stu-id="cb3d1-121">Shared data for users to access</span></span>
* <span data-ttu-id="cb3d1-122">SQL DB or QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="cb3d1-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="cb3d1-123">Any data in D:\\</span><span class="sxs-lookup"><span data-stu-id="cb3d1-123">Any data in D:\\</span></span>

<span data-ttu-id="cb3d1-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span><span class="sxs-lookup"><span data-stu-id="cb3d1-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span></span>

* <span data-ttu-id="cb3d1-125">Configuration files per user</span><span class="sxs-lookup"><span data-stu-id="cb3d1-125">Configuration files per user</span></span>
* <span data-ttu-id="cb3d1-126">Scripts that users would need preserved in their UPD</span><span class="sxs-lookup"><span data-stu-id="cb3d1-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="cb3d1-127">Key points:</span><span class="sxs-lookup"><span data-stu-id="cb3d1-127">Key points:</span></span>

* <span data-ttu-id="cb3d1-128">Never store sensitive data that can be lost on the image when creating a custom image.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-128">Never store sensitive data that can be lost on the image when creating a custom image.</span></span>
* <span data-ttu-id="cb3d1-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cb3d1-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="cb3d1-130">User data is saved and persists in the user profile disk (UPD)</span><span class="sxs-lookup"><span data-stu-id="cb3d1-130">User data is saved and persists in the user profile disk (UPD)</span></span>

