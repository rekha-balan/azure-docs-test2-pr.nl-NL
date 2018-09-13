---
title: Azure RemoteApp best practices | Microsoft Docs
description: Best practices for configuring and using Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: fda356fc5fd6e9888138a06a0b72232e3581567b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555257"
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="8557e-103">Best practices for configuring and using Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8557e-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8557e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="8557e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8557e-105">Read the [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span><span class="sxs-lookup"><span data-stu-id="8557e-105">Read the [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="8557e-106">The following information can help you configure and use Azure RemoteApp productively.</span><span class="sxs-lookup"><span data-stu-id="8557e-106">The following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="8557e-107">Connectivity</span><span class="sxs-lookup"><span data-stu-id="8557e-107">Connectivity</span></span>
* <span data-ttu-id="8557e-108">Always use the latest client version.</span><span class="sxs-lookup"><span data-stu-id="8557e-108">Always use the latest client version.</span></span> <span data-ttu-id="8557e-109">Using older clients might result in connectivity issues and other degraded experiences.</span><span class="sxs-lookup"><span data-stu-id="8557e-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="8557e-110">Enabling automatic application updates for your device will ensure that the latest client is always installed.</span><span class="sxs-lookup"><span data-stu-id="8557e-110">Enabling automatic application updates for your device will ensure that the latest client is always installed.</span></span>
* <span data-ttu-id="8557e-111">Always use the most stable and reliable internet connection available to you.</span><span class="sxs-lookup"><span data-stu-id="8557e-111">Always use the most stable and reliable internet connection available to you.</span></span>  
* <span data-ttu-id="8557e-112">Use only supported proxy connections for optimal connectivity performance.</span><span class="sxs-lookup"><span data-stu-id="8557e-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="8557e-113">The SOCKS proxy is not supported.</span><span class="sxs-lookup"><span data-stu-id="8557e-113">The SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="8557e-114">Applications</span><span class="sxs-lookup"><span data-stu-id="8557e-114">Applications</span></span>
* <span data-ttu-id="8557e-115">Save and close RemoteApp applications when you are done with the application.</span><span class="sxs-lookup"><span data-stu-id="8557e-115">Save and close RemoteApp applications when you are done with the application.</span></span> <span data-ttu-id="8557e-116">Not closing the application might result in data loss.</span><span class="sxs-lookup"><span data-stu-id="8557e-116">Not closing the application might result in data loss.</span></span>
* <span data-ttu-id="8557e-117">Validate custom applications before using them in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8557e-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="8557e-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in the same collection.</span><span class="sxs-lookup"><span data-stu-id="8557e-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in the same collection.</span></span> <span data-ttu-id="8557e-119">For information, download and review the [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span><span class="sxs-lookup"><span data-stu-id="8557e-119">For information, download and review the [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="8557e-120">Configuration and management</span><span class="sxs-lookup"><span data-stu-id="8557e-120">Configuration and management</span></span>
* <span data-ttu-id="8557e-121">Keep your template images up to date, installing software updates and other critical fixes as needed.</span><span class="sxs-lookup"><span data-stu-id="8557e-121">Keep your template images up to date, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="8557e-122">This ensures that as Azure RemoteApp auto-scales to meet your capacity, each instance is patched.</span><span class="sxs-lookup"><span data-stu-id="8557e-122">This ensures that as Azure RemoteApp auto-scales to meet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="8557e-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span><span class="sxs-lookup"><span data-stu-id="8557e-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="8557e-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8557e-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="8557e-125">Configure template images with installed applications, roles, or features such that they are stateless.</span><span class="sxs-lookup"><span data-stu-id="8557e-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="8557e-126">They should not rely on any instances of the virtual machines in a RemoteApp service being in a persistent state.</span><span class="sxs-lookup"><span data-stu-id="8557e-126">They should not rely on any instances of the virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="8557e-127">Store all user data in user profiles or other storage locations external to the service, such as on-premises file shares or OneDrive.</span><span class="sxs-lookup"><span data-stu-id="8557e-127">Store all user data in user profiles or other storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="8557e-128">Store shared data in storage locations external to the service, such as on-premises file shares or OneDrive.</span><span class="sxs-lookup"><span data-stu-id="8557e-128">Store shared data in storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="8557e-129">Configure any system-wide settings in the template image rather than on individual virtual machines in a service.</span><span class="sxs-lookup"><span data-stu-id="8557e-129">Configure any system-wide settings in the template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="8557e-130">Disable automatic software updates for published applications - instead apply them manually to the template image and test them before you deploy  from the template.</span><span class="sxs-lookup"><span data-stu-id="8557e-130">Disable automatic software updates for published applications - instead apply them manually to the template image and test them before you deploy  from the template.</span></span>

