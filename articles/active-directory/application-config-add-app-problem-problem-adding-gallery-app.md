---
title: Problem adding an Azure AD Gallery application | Microsoft Docs
description: Understand the common problems people face when adding Azure AD Gallery applications and what you can do to resolve them
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: b47b5dfb1b7e19170bde932ff143ebca0dec19ef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550931"
---
# <a name="problem-adding-an-azure-ad-gallery-application"></a><span data-ttu-id="bf771-103">Problem adding an Azure AD Gallery application</span><span class="sxs-lookup"><span data-stu-id="bf771-103">Problem adding an Azure AD Gallery application</span></span>

<span data-ttu-id="bf771-104">This article help you to understand the common problems people face when adding Azure AD Gallery applications and what you can do to resolve them.</span><span class="sxs-lookup"><span data-stu-id="bf771-104">This article help you to understand the common problems people face when adding Azure AD Gallery applications and what you can do to resolve them.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="bf771-105">I clicked the “add” button and my application took a long time to appear</span><span class="sxs-lookup"><span data-stu-id="bf771-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="bf771-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span><span class="sxs-lookup"><span data-stu-id="bf771-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="bf771-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application.**</span><span class="sxs-lookup"><span data-stu-id="bf771-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application.**</span></span>

<span data-ttu-id="bf771-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span><span class="sxs-lookup"><span data-stu-id="bf771-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="bf771-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span><span class="sxs-lookup"><span data-stu-id="bf771-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="bf771-110">I clicked the “add” button and my application didn’t appear</span><span class="sxs-lookup"><span data-stu-id="bf771-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="bf771-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span><span class="sxs-lookup"><span data-stu-id="bf771-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="bf771-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span><span class="sxs-lookup"><span data-stu-id="bf771-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="bf771-113">This indicates there was an error when creating the application.</span><span class="sxs-lookup"><span data-stu-id="bf771-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="bf771-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span><span class="sxs-lookup"><span data-stu-id="bf771-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="bf771-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span><span class="sxs-lookup"><span data-stu-id="bf771-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

 ## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="bf771-116">I don’t know how to set up my application once I’ve added it</span><span class="sxs-lookup"><span data-stu-id="bf771-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="bf771-117">If you need help learning about applications, the [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) article is a good place to start.</span><span class="sxs-lookup"><span data-stu-id="bf771-117">If you need help learning about applications, the [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) article is a good place to start.</span></span>

<span data-ttu-id="bf771-118">In addition to this, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span><span class="sxs-lookup"><span data-stu-id="bf771-118">In addition to this, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="bf771-119">How to see the details of a portal notification</span><span class="sxs-lookup"><span data-stu-id="bf771-119">How to see the details of a portal notification</span></span>

<span data-ttu-id="bf771-120">You can see the details of any portal notification by following the steps below:</span><span class="sxs-lookup"><span data-stu-id="bf771-120">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="bf771-121">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bf771-121">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="bf771-122">Select any notification in an **Error** state (those with a red (!) next to them).</span><span class="sxs-lookup"><span data-stu-id="bf771-122">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

    >[!NOTE]
    ><span data-ttu-id="bf771-123">You cannot click notifications in a **Successful** or **In Progress** state.</span><span class="sxs-lookup"><span data-stu-id="bf771-123">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
    >
    >

3.  <span data-ttu-id="bf771-124">This open the **Notification Details** blade.</span><span class="sxs-lookup"><span data-stu-id="bf771-124">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="bf771-125">Use this information yourself to understand more details about the problem.</span><span class="sxs-lookup"><span data-stu-id="bf771-125">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="bf771-126">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span><span class="sxs-lookup"><span data-stu-id="bf771-126">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="bf771-127">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span><span class="sxs-lookup"><span data-stu-id="bf771-127">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="bf771-128">How to get help by sending notification details to a support engineer</span><span class="sxs-lookup"><span data-stu-id="bf771-128">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="bf771-129">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span><span class="sxs-lookup"><span data-stu-id="bf771-129">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="bf771-130">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span><span class="sxs-lookup"><span data-stu-id="bf771-130">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="bf771-131">Notification Details Explained</span><span class="sxs-lookup"><span data-stu-id="bf771-131">Notification Details Explained</span></span>

<span data-ttu-id="bf771-132">The below explains more what each of the notification items means, and gives examples of each of them.</span><span class="sxs-lookup"><span data-stu-id="bf771-132">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="bf771-133">Essential Notification Items</span><span class="sxs-lookup"><span data-stu-id="bf771-133">Essential Notification Items</span></span>

-   <span data-ttu-id="bf771-134">**Title** – the descriptive title of the notification</span><span class="sxs-lookup"><span data-stu-id="bf771-134">**Title** – the descriptive title of the notification</span></span>

  * <span data-ttu-id="bf771-135">Example – **Application proxy settings**</span><span class="sxs-lookup"><span data-stu-id="bf771-135">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="bf771-136">**Description** – the description of what occurred as a result of the operation</span><span class="sxs-lookup"><span data-stu-id="bf771-136">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="bf771-137">Example – **Internal url entered is already being used by another application**</span><span class="sxs-lookup"><span data-stu-id="bf771-137">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="bf771-138">**Notification Id** – the unique id of the notification</span><span class="sxs-lookup"><span data-stu-id="bf771-138">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="bf771-139">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="bf771-139">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="bf771-140">**Client Request Id** – the specific request id made by your browser</span><span class="sxs-lookup"><span data-stu-id="bf771-140">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="bf771-141">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="bf771-141">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="bf771-142">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span><span class="sxs-lookup"><span data-stu-id="bf771-142">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="bf771-143">Example – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="bf771-143">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="bf771-144">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span><span class="sxs-lookup"><span data-stu-id="bf771-144">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="bf771-145">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="bf771-145">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="bf771-146">**UPN** – the user who performed the operation</span><span class="sxs-lookup"><span data-stu-id="bf771-146">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="bf771-147">Example – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="bf771-147">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="bf771-148">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span><span class="sxs-lookup"><span data-stu-id="bf771-148">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="bf771-149">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="bf771-149">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="bf771-150">**User object Id** – the unique ID of the user who performed the operation</span><span class="sxs-lookup"><span data-stu-id="bf771-150">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="bf771-151">Example – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="bf771-151">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="bf771-152">Detailed Notification Items</span><span class="sxs-lookup"><span data-stu-id="bf771-152">Detailed Notification Items</span></span>

-   <span data-ttu-id="bf771-153">**Display Name** – **(can be empty)** a more detailed display name for the error</span><span class="sxs-lookup"><span data-stu-id="bf771-153">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="bf771-154">Example – **Application proxy settings**</span><span class="sxs-lookup"><span data-stu-id="bf771-154">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="bf771-155">**Status** – the specific status of the notification</span><span class="sxs-lookup"><span data-stu-id="bf771-155">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="bf771-156">Example – **Failed**</span><span class="sxs-lookup"><span data-stu-id="bf771-156">Example – **Failed**</span></span>

-   <span data-ttu-id="bf771-157">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span><span class="sxs-lookup"><span data-stu-id="bf771-157">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="bf771-158">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="bf771-158">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="bf771-159">**Details** – the detailed description of what occurred as a result of the operation</span><span class="sxs-lookup"><span data-stu-id="bf771-159">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="bf771-160">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span><span class="sxs-lookup"><span data-stu-id="bf771-160">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="bf771-161">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span><span class="sxs-lookup"><span data-stu-id="bf771-161">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="bf771-162">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="bf771-162">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf771-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="bf771-163">Next steps</span></span>
[<span data-ttu-id="bf771-164">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf771-164">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
