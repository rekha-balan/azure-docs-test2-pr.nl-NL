---
title: Add a user to your Azure RemoteApp collection | Microsoft Docs
description: Learn how to add users to your Azure RemoteApp collection
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a84aa7e3ac7de717c2a628abcf6f5f11b05411e8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553734"
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a><span data-ttu-id="7cb94-103">How to add a user to your Azure RemoteApp collection</span><span class="sxs-lookup"><span data-stu-id="7cb94-103">How to add a user to your Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7cb94-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="7cb94-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7cb94-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="7cb94-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7cb94-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span><span class="sxs-lookup"><span data-stu-id="7cb94-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span></span> <span data-ttu-id="7cb94-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span><span class="sxs-lookup"><span data-stu-id="7cb94-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span></span>

<span data-ttu-id="7cb94-108">What account information do you need?</span><span class="sxs-lookup"><span data-stu-id="7cb94-108">What account information do you need?</span></span> <span data-ttu-id="7cb94-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span><span class="sxs-lookup"><span data-stu-id="7cb94-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="7cb94-110">Supported user identities</span><span class="sxs-lookup"><span data-stu-id="7cb94-110">Supported user identities</span></span>
<span data-ttu-id="7cb94-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span><span class="sxs-lookup"><span data-stu-id="7cb94-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span></span>  

<span data-ttu-id="7cb94-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span><span class="sxs-lookup"><span data-stu-id="7cb94-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="7cb94-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span><span class="sxs-lookup"><span data-stu-id="7cb94-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span></span>  

<span data-ttu-id="7cb94-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span><span class="sxs-lookup"><span data-stu-id="7cb94-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span></span>  <span data-ttu-id="7cb94-115">See the table below.</span><span class="sxs-lookup"><span data-stu-id="7cb94-115">See the table below.</span></span>

<span data-ttu-id="7cb94-116">Office 365 users are Azure Active Directory users.</span><span class="sxs-lookup"><span data-stu-id="7cb94-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="7cb94-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span><span class="sxs-lookup"><span data-stu-id="7cb94-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="7cb94-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span><span class="sxs-lookup"><span data-stu-id="7cb94-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span></span>

| <span data-ttu-id="7cb94-119">User accounts</span><span class="sxs-lookup"><span data-stu-id="7cb94-119">User accounts</span></span> | <span data-ttu-id="7cb94-120">Cloud</span><span class="sxs-lookup"><span data-stu-id="7cb94-120">Cloud</span></span> | <span data-ttu-id="7cb94-121">Hybrid</span><span class="sxs-lookup"><span data-stu-id="7cb94-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cb94-122">Microsoft Account</span><span class="sxs-lookup"><span data-stu-id="7cb94-122">Microsoft Account</span></span> |<span data-ttu-id="7cb94-123">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-123">Yes</span></span> |<span data-ttu-id="7cb94-124">No</span><span class="sxs-lookup"><span data-stu-id="7cb94-124">No</span></span> |
| <span data-ttu-id="7cb94-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="7cb94-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="7cb94-126">Azure AD cloud only</span><span class="sxs-lookup"><span data-stu-id="7cb94-126">Azure AD cloud only</span></span> |<span data-ttu-id="7cb94-127">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-127">Yes</span></span> |<span data-ttu-id="7cb94-128">No</span><span class="sxs-lookup"><span data-stu-id="7cb94-128">No</span></span> |
| <span data-ttu-id="7cb94-129">ADsync with password sync</span><span class="sxs-lookup"><span data-stu-id="7cb94-129">ADsync with password sync</span></span> |<span data-ttu-id="7cb94-130">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-130">Yes</span></span> |<span data-ttu-id="7cb94-131">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-131">Yes</span></span> |
| <span data-ttu-id="7cb94-132">ADsync without password sync</span><span class="sxs-lookup"><span data-stu-id="7cb94-132">ADsync without password sync</span></span> |<span data-ttu-id="7cb94-133">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-133">Yes</span></span> |<span data-ttu-id="7cb94-134">No</span><span class="sxs-lookup"><span data-stu-id="7cb94-134">No</span></span> |
| <span data-ttu-id="7cb94-135">ADsync with AD FS</span><span class="sxs-lookup"><span data-stu-id="7cb94-135">ADsync with AD FS</span></span> |<span data-ttu-id="7cb94-136">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-136">Yes</span></span> |<span data-ttu-id="7cb94-137">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-137">Yes</span></span> |
| <span data-ttu-id="7cb94-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span><span class="sxs-lookup"><span data-stu-id="7cb94-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="7cb94-139">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-139">Yes</span></span> |<span data-ttu-id="7cb94-140">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-140">Yes</span></span> |
| <span data-ttu-id="7cb94-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="7cb94-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="7cb94-142">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-142">Yes</span></span> |<span data-ttu-id="7cb94-143">Yes</span><span class="sxs-lookup"><span data-stu-id="7cb94-143">Yes</span></span> |

<span data-ttu-id="7cb94-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7cb94-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="7cb94-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span><span class="sxs-lookup"><span data-stu-id="7cb94-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span></span> <span data-ttu-id="7cb94-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span><span class="sxs-lookup"><span data-stu-id="7cb94-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span></span> <span data-ttu-id="7cb94-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span><span class="sxs-lookup"><span data-stu-id="7cb94-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="7cb94-148">Office 365 ProPlus user account information</span><span class="sxs-lookup"><span data-stu-id="7cb94-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="7cb94-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span><span class="sxs-lookup"><span data-stu-id="7cb94-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span></span> <span data-ttu-id="7cb94-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="7cb94-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

