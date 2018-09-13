---
title: Change the Azure Active Directory tenant in Azure RemoteApp | Microsoft Docs
description: Learn how to change the Azure Active Directory tenant associated with Azure RemoteApp
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 1199ca2378cfe4adba2d591bfab204113b4a0468
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553486"
---
# <a name="change-the-azure-active-directory-tenant-in-azure-remoteapp"></a><span data-ttu-id="cf7f6-103">Change the Azure Active Directory tenant in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cf7f6-103">Change the Azure Active Directory tenant in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cf7f6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cf7f6-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cf7f6-106">Azure RemoteApp uses Azure Active Directory (Azure AD) to allow user access.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-106">Azure RemoteApp uses Azure Active Directory (Azure AD) to allow user access.</span></span> <span data-ttu-id="cf7f6-107">The only Azure AD tenant that you can use in Azure RemoteApp is the one associated with the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-107">The only Azure AD tenant that you can use in Azure RemoteApp is the one associated with the Azure subscription.</span></span> <span data-ttu-id="cf7f6-108">You can view the associated subscription on the **Settings** page in the portal.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-108">You can view the associated subscription on the **Settings** page in the portal.</span></span> <span data-ttu-id="cf7f6-109">Look at the **Directory** column on the **Subscriptions** tab.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-109">Look at the **Directory** column on the **Subscriptions** tab.</span></span>

> [!NOTE]
> <span data-ttu-id="cf7f6-110">For this change to succeed, first remove all users from the existing Azure Active Directory tenant from all Azure RemoteApp collections.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-110">For this change to succeed, first remove all users from the existing Azure Active Directory tenant from all Azure RemoteApp collections.</span></span> <span data-ttu-id="cf7f6-111">To do this, go to the Azure Portal, go to the **Azure RemoteApp** tab and open every Azure RemoteApp collection.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-111">To do this, go to the Azure Portal, go to the **Azure RemoteApp** tab and open every Azure RemoteApp collection.</span></span> <span data-ttu-id="cf7f6-112">Go to the **Users** tab and remove users that belong to your current Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-112">Go to the **Users** tab and remove users that belong to your current Azure Active Directory tenant.</span></span> <span data-ttu-id="cf7f6-113">Repeat for all existing Azure RemoteApp collections.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-113">Repeat for all existing Azure RemoteApp collections.</span></span> <span data-ttu-id="cf7f6-114">Without doing this, you will not be able to create or patch collections.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-114">Without doing this, you will not be able to create or patch collections.</span></span>
> 
> 

<span data-ttu-id="cf7f6-115">If you want to use a different tenant, use these steps to change the association with your subscription:</span><span class="sxs-lookup"><span data-stu-id="cf7f6-115">If you want to use a different tenant, use these steps to change the association with your subscription:</span></span>

1. <span data-ttu-id="cf7f6-116">In the portal, remove any Azure AD users to which you’ve given access to Azure RemoteApp collections.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-116">In the portal, remove any Azure AD users to which you’ve given access to Azure RemoteApp collections.</span></span> <span data-ttu-id="cf7f6-117">(See the note above for steps on how to do this.)</span><span class="sxs-lookup"><span data-stu-id="cf7f6-117">(See the note above for steps on how to do this.)</span></span>
2. <span data-ttu-id="cf7f6-118">Set a Microsoft account (formerly called a Live ID) as the Service administrator.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-118">Set a Microsoft account (formerly called a Live ID) as the Service administrator.</span></span> <span data-ttu-id="cf7f6-119">(Don't know if you already are the service admin?</span><span class="sxs-lookup"><span data-stu-id="cf7f6-119">(Don't know if you already are the service admin?</span></span> <span data-ttu-id="cf7f6-120">You can find out by clicking **Settings -> Administrators**.) Now, here's how you change that:</span><span class="sxs-lookup"><span data-stu-id="cf7f6-120">You can find out by clicking **Settings -> Administrators**.) Now, here's how you change that:</span></span>
   
   1. <span data-ttu-id="cf7f6-121">Click the user in the upper right corner, and then click **View my bill**.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-121">Click the user in the upper right corner, and then click **View my bill**.</span></span>
   2. <span data-ttu-id="cf7f6-122">Click the subscription.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-122">Click the subscription.</span></span> <span data-ttu-id="cf7f6-123">Then, on the new page, scroll down and click **Edit subscription details** in the right.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-123">Then, on the new page, scroll down and click **Edit subscription details** in the right.</span></span> <span data-ttu-id="cf7f6-124">(Sort of the middle bottom right, if that helps you find it.)</span><span class="sxs-lookup"><span data-stu-id="cf7f6-124">(Sort of the middle bottom right, if that helps you find it.)</span></span>
   3. <span data-ttu-id="cf7f6-125">Type the Microsoft account for the user that should be the service admin.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-125">Type the Microsoft account for the user that should be the service admin.</span></span>
3. <span data-ttu-id="cf7f6-126">Now, sign out of the portal, and then sign back in with the Microsoft account you specified in the previous step.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-126">Now, sign out of the portal, and then sign back in with the Microsoft account you specified in the previous step.</span></span>
4. <span data-ttu-id="cf7f6-127">Click **New -> App Services -> Active Directory -> Directory -> Custom Create**.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-127">Click **New -> App Services -> Active Directory -> Directory -> Custom Create**.</span></span>
5. <span data-ttu-id="cf7f6-128">Under **Directory**, choose **Use existing directory**.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-128">Under **Directory**, choose **Use existing directory**.</span></span> <span data-ttu-id="cf7f6-129">We're going to have to sign you out of the portal now, so choose **I am ready to be signed out now**.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-129">We're going to have to sign you out of the portal now, so choose **I am ready to be signed out now**.</span></span>
6. <span data-ttu-id="cf7f6-130">Sign back into the portal as a global admin of the directory you want to add.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-130">Sign back into the portal as a global admin of the directory you want to add.</span></span> <span data-ttu-id="cf7f6-131">(If you weren't already a global admin, you will be after a round of sign in and then sign out.)</span><span class="sxs-lookup"><span data-stu-id="cf7f6-131">(If you weren't already a global admin, you will be after a round of sign in and then sign out.)</span></span>
7. <span data-ttu-id="cf7f6-132">You'll be asked when you sign in if you want to use your existing AD tenant with your subscription.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-132">You'll be asked when you sign in if you want to use your existing AD tenant with your subscription.</span></span> <span data-ttu-id="cf7f6-133">Click **Continue**, and then click **Sign out now**.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-133">Click **Continue**, and then click **Sign out now**.</span></span>
8. <span data-ttu-id="cf7f6-134">Sign back in again, and go back to **Settings -> Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-134">Sign back in again, and go back to **Settings -> Subscriptions**.</span></span> <span data-ttu-id="cf7f6-135">Select your subscription, and then click **Edit Directory**.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-135">Select your subscription, and then click **Edit Directory**.</span></span> <span data-ttu-id="cf7f6-136">Select the Azure AD tenant that you want to use.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-136">Select the Azure AD tenant that you want to use.</span></span>

<span data-ttu-id="cf7f6-137">You can now use the new Azure AD tenant to control access to the Azure subscription and to configure user access in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cf7f6-137">You can now use the new Azure AD tenant to control access to the Azure subscription and to configure user access in Azure RemoteApp.</span></span>

