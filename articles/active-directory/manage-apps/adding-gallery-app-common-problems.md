---
title: Problem adding an Azure AD Gallery application | Microsoft Docs
description: Understand the common problems people face when adding Azure AD Gallery applications and what you can do to resolve them
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: barbkess
ms.openlocfilehash: 4449246f9ca1a4232d3cfeec92c86db62d6834a4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865305"
---
# <a name="problem-adding-an-azure-ad-gallery-application"></a><span data-ttu-id="dcde1-103">Problem adding an Azure AD Gallery application</span><span class="sxs-lookup"><span data-stu-id="dcde1-103">Problem adding an Azure AD Gallery application</span></span>

<span data-ttu-id="dcde1-104">This article helps you understand the common problems people face when adding Azure AD Gallery applications and what you can do to resolve them.</span><span class="sxs-lookup"><span data-stu-id="dcde1-104">This article helps you understand the common problems people face when adding Azure AD Gallery applications and what you can do to resolve them.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="dcde1-105">I clicked the “add” button and my application took a long time to appear</span><span class="sxs-lookup"><span data-stu-id="dcde1-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="dcde1-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span><span class="sxs-lookup"><span data-stu-id="dcde1-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="dcde1-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application.**</span><span class="sxs-lookup"><span data-stu-id="dcde1-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application.**</span></span>

<span data-ttu-id="dcde1-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span><span class="sxs-lookup"><span data-stu-id="dcde1-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="dcde1-109">If you want more details about the error to learn more to or share with a support engineer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span><span class="sxs-lookup"><span data-stu-id="dcde1-109">If you want more details about the error to learn more to or share with a support engineer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="dcde1-110">I clicked the “add” button and my application didn’t appear</span><span class="sxs-lookup"><span data-stu-id="dcde1-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="dcde1-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span><span class="sxs-lookup"><span data-stu-id="dcde1-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="dcde1-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure portal and you see a red (!) icon next to your **Create application** notification.</span><span class="sxs-lookup"><span data-stu-id="dcde1-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="dcde1-113">This indicates there was an error when creating the application.</span><span class="sxs-lookup"><span data-stu-id="dcde1-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="dcde1-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span><span class="sxs-lookup"><span data-stu-id="dcde1-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="dcde1-115">If you want more details about the error to learn more to or share with a support engineer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span><span class="sxs-lookup"><span data-stu-id="dcde1-115">If you want more details about the error to learn more to or share with a support engineer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

 ## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="dcde1-116">I don’t know how to set up my application once I’ve added it</span><span class="sxs-lookup"><span data-stu-id="dcde1-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="dcde1-117">If you need help learning about applications, the [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) article is a good place to start.</span><span class="sxs-lookup"><span data-stu-id="dcde1-117">If you need help learning about applications, the [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) article is a good place to start.</span></span>

<span data-ttu-id="dcde1-118">In addition to this, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span><span class="sxs-lookup"><span data-stu-id="dcde1-118">In addition to this, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="dcde1-119">How to see the details of a portal notification</span><span class="sxs-lookup"><span data-stu-id="dcde1-119">How to see the details of a portal notification</span></span>

<span data-ttu-id="dcde1-120">You can see the details of any portal notification by following the steps below:</span><span class="sxs-lookup"><span data-stu-id="dcde1-120">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="dcde1-121">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dcde1-121">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="dcde1-122">Select any notification in an **Error** state (those with a red (!) next to them).</span><span class="sxs-lookup"><span data-stu-id="dcde1-122">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

    >[!NOTE]
    ><span data-ttu-id="dcde1-123">You cannot click notifications in a **Successful** or **In Progress** state.</span><span class="sxs-lookup"><span data-stu-id="dcde1-123">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
    >
    >

4.  <span data-ttu-id="dcde1-124">Use the information under **Notification Details** to understand more details about the problem.</span><span class="sxs-lookup"><span data-stu-id="dcde1-124">Use the information under **Notification Details** to understand more details about the problem.</span></span>

5.  <span data-ttu-id="dcde1-125">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span><span class="sxs-lookup"><span data-stu-id="dcde1-125">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="dcde1-126">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span><span class="sxs-lookup"><span data-stu-id="dcde1-126">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="dcde1-127">How to get help by sending notification details to a support engineer</span><span class="sxs-lookup"><span data-stu-id="dcde1-127">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="dcde1-128">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span><span class="sxs-lookup"><span data-stu-id="dcde1-128">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="dcde1-129">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span><span class="sxs-lookup"><span data-stu-id="dcde1-129">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="dcde1-130">Notification Details Explained</span><span class="sxs-lookup"><span data-stu-id="dcde1-130">Notification Details Explained</span></span>

<span data-ttu-id="dcde1-131">See the following descriptions for more details about the notifications.</span><span class="sxs-lookup"><span data-stu-id="dcde1-131">See the following descriptions for more details about the notifications.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="dcde1-132">Essential Notification Items</span><span class="sxs-lookup"><span data-stu-id="dcde1-132">Essential Notification Items</span></span>

-   <span data-ttu-id="dcde1-133">**Title** – the descriptive title of the notification</span><span class="sxs-lookup"><span data-stu-id="dcde1-133">**Title** – the descriptive title of the notification</span></span>

  * <span data-ttu-id="dcde1-134">Example – **Application proxy settings**</span><span class="sxs-lookup"><span data-stu-id="dcde1-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="dcde1-135">**Description** – the description of what occurred as a result of the operation</span><span class="sxs-lookup"><span data-stu-id="dcde1-135">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="dcde1-136">Example – **Internal url entered is already being used by another application**</span><span class="sxs-lookup"><span data-stu-id="dcde1-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="dcde1-137">**Notification ID** – the unique ID of the notification</span><span class="sxs-lookup"><span data-stu-id="dcde1-137">**Notification ID** – the unique ID of the notification</span></span>

    -   <span data-ttu-id="dcde1-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="dcde1-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="dcde1-139">**Client Request ID** – the specific request ID made by your browser</span><span class="sxs-lookup"><span data-stu-id="dcde1-139">**Client Request ID** – the specific request ID made by your browser</span></span>

    -   <span data-ttu-id="dcde1-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="dcde1-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="dcde1-141">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span><span class="sxs-lookup"><span data-stu-id="dcde1-141">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="dcde1-142">Example – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="dcde1-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="dcde1-143">**Internal Transaction ID** – the internal ID we can use to look the error up in our systems</span><span class="sxs-lookup"><span data-stu-id="dcde1-143">**Internal Transaction ID** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="dcde1-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="dcde1-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="dcde1-145">**UPN** – the user who performed the operation</span><span class="sxs-lookup"><span data-stu-id="dcde1-145">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="dcde1-146">Example – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="dcde1-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="dcde1-147">**Tenant ID** – the unique ID of the tenant that the user who performed the operation was a member of</span><span class="sxs-lookup"><span data-stu-id="dcde1-147">**Tenant ID** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="dcde1-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="dcde1-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="dcde1-149">**User object ID** – the unique ID of the user who performed the operation</span><span class="sxs-lookup"><span data-stu-id="dcde1-149">**User object ID** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="dcde1-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="dcde1-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="dcde1-151">Detailed Notification Items</span><span class="sxs-lookup"><span data-stu-id="dcde1-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="dcde1-152">**Display Name** – **(can be empty)** a more detailed display name for the error</span><span class="sxs-lookup"><span data-stu-id="dcde1-152">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="dcde1-153">Example – **Application proxy settings**</span><span class="sxs-lookup"><span data-stu-id="dcde1-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="dcde1-154">**Status** – the specific status of the notification</span><span class="sxs-lookup"><span data-stu-id="dcde1-154">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="dcde1-155">Example – **Failed**</span><span class="sxs-lookup"><span data-stu-id="dcde1-155">Example – **Failed**</span></span>

-   <span data-ttu-id="dcde1-156">**Object ID** – **(can be empty)** the object ID against which the operation was performed</span><span class="sxs-lookup"><span data-stu-id="dcde1-156">**Object ID** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="dcde1-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="dcde1-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="dcde1-158">**Details** – the detailed description of what occurred as a result of the operation</span><span class="sxs-lookup"><span data-stu-id="dcde1-158">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="dcde1-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span><span class="sxs-lookup"><span data-stu-id="dcde1-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="dcde1-160">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group</span><span class="sxs-lookup"><span data-stu-id="dcde1-160">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group</span></span> 
-   <span data-ttu-id="dcde1-161">engineer</span><span class="sxs-lookup"><span data-stu-id="dcde1-161">engineer</span></span>

    -   <span data-ttu-id="dcde1-162">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="dcde1-162">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcde1-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="dcde1-163">Next steps</span></span>
[<span data-ttu-id="dcde1-164">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dcde1-164">Managing Applications with Azure Active Directory</span></span>](what-is-application-management.md)
