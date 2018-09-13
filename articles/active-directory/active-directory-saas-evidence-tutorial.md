---
title: 'Tutorial: Azure Active Directory integration with Evidence.com | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Evidence.com.
services: active-directory
documentationcenter: ''
author: asmalser-msft
manager: femila
editor: ''
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2016
ms.author: asmalser
ms.openlocfilehash: 5d5183b136a0ceca939f754f67130d1179f6f4f7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550587"
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="d2114-103">Tutorial: Azure Active Directory integration with Evidence.com</span><span class="sxs-lookup"><span data-stu-id="d2114-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>
<span data-ttu-id="d2114-104">The objective of this tutorial is to show how to set up single sign-on between Azure Active Directory (AAD) and Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="d2114-104">The objective of this tutorial is to show how to set up single sign-on between Azure Active Directory (AAD) and Evidence.com.</span></span> <span data-ttu-id="d2114-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="d2114-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="d2114-106">A valid Microsoft Azure subscription</span><span class="sxs-lookup"><span data-stu-id="d2114-106">A valid Microsoft Azure subscription</span></span>
* <span data-ttu-id="d2114-107">An Evidence.com subscription with single sign On enabled (email earlyaccess@evidence.com if SAML-based single sign on is not enabled)</span><span class="sxs-lookup"><span data-stu-id="d2114-107">An Evidence.com subscription with single sign On enabled (email earlyaccess@evidence.com if SAML-based single sign on is not enabled)</span></span>

<span data-ttu-id="d2114-108">After completing this tutorial, the AAD users to whom you have assigned Evidence.com access will be able to single sign into the application using the AAD Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d2114-108">After completing this tutorial, the AAD users to whom you have assigned Evidence.com access will be able to single sign into the application using the AAD Access Panel.</span></span>

## <a name="add-evidencecom-to-your-directory"></a><span data-ttu-id="d2114-109">Add Evidence.com to your directory</span><span class="sxs-lookup"><span data-stu-id="d2114-109">Add Evidence.com to your directory</span></span>
<span data-ttu-id="d2114-110">This section outlines how to add Evidence.com as an integrated application in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d2114-110">This section outlines how to add Evidence.com as an integrated application in Azure Active Directory.</span></span>

<span data-ttu-id="d2114-111">**To enable the application integration for Evidence:**</span><span class="sxs-lookup"><span data-stu-id="d2114-111">**To enable the application integration for Evidence:**</span></span>

1. <span data-ttu-id="d2114-112">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d2114-112">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
2. <span data-ttu-id="d2114-113">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d2114-113">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d2114-114">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d2114-114">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
4. <span data-ttu-id="d2114-115">To open the Application Gallery, click **Add**, and then click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d2114-115">To open the Application Gallery, click **Add**, and then click **Add an application from the gallery**.</span></span>
5. <span data-ttu-id="d2114-116">In the search box, type **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="d2114-116">In the search box, type **Evidence.com**.</span></span>
6. <span data-ttu-id="d2114-117">In the results pane, select **Evidence.com**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d2114-117">In the results pane, select **Evidence.com**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="d2114-118">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="d2114-118">Configuring single sign-on</span></span>
<span data-ttu-id="d2114-119">This section outlines how to enable users to authenticate to Evidence.com with their account in Azure Active Directory, using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="d2114-119">This section outlines how to enable users to authenticate to Evidence.com with their account in Azure Active Directory, using federation based on the SAML protocol.</span></span>

<span data-ttu-id="d2114-120">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d2114-120">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="d2114-121">After adding Evidence.com in the Azure classic portal, click **Configure Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d2114-121">After adding Evidence.com in the Azure classic portal, click **Configure Single Sign-On**.</span></span> 
2. <span data-ttu-id="d2114-122">On the next screen, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d2114-122">On the next screen, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
3. <span data-ttu-id="d2114-123">In the Configure App URL screen, enter the URL where users will sign into your Evidence.com tenant URL (Example: https://yourtenant.evidence.com  and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d2114-123">In the Configure App URL screen, enter the URL where users will sign into your Evidence.com tenant URL (Example: https://yourtenant.evidence.com  and then click **Next**.</span></span> 
4. <span data-ttu-id="d2114-124">Click the **Download Certificate** link, and save it to your local drive.</span><span class="sxs-lookup"><span data-stu-id="d2114-124">Click the **Download Certificate** link, and save it to your local drive.</span></span> <span data-ttu-id="d2114-125">This certificate and the metadata URLs (  Entity ID, SSO Sign In URL and Sign Out URL ) will be used to set up SSO on Evidence.com site.</span><span class="sxs-lookup"><span data-stu-id="d2114-125">This certificate and the metadata URLs (  Entity ID, SSO Sign In URL and Sign Out URL ) will be used to set up SSO on Evidence.com site.</span></span> 
5. <span data-ttu-id="d2114-126">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span><span class="sxs-lookup"><span data-stu-id="d2114-126">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span></span>
6. <span data-ttu-id="d2114-127">Click on **Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="d2114-127">Click on **Agency Single Sign On**</span></span>
7. <span data-ttu-id="d2114-128">Select **SAML Based Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="d2114-128">Select **SAML Based Single Sign On**</span></span>
8. <span data-ttu-id="d2114-129">Copy the **Issuer URL**, **Single Sign On** and **Single Sign Out** values shown in the Azure classic portal and to the corresponding fields in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="d2114-129">Copy the **Issuer URL**, **Single Sign On** and **Single Sign Out** values shown in the Azure classic portal and to the corresponding fields in Evidence.com.</span></span>
9. <span data-ttu-id="d2114-130">Open the certificate downloaded in step 4 using a text editor like Notepad.exe, and copy and paste the contents into the **Security Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="d2114-130">Open the certificate downloaded in step 4 using a text editor like Notepad.exe, and copy and paste the contents into the **Security Certificate** box.</span></span> 
10. <span data-ttu-id="d2114-131">Save the configuration in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="d2114-131">Save the configuration in Evidence.com.</span></span>
11. <span data-ttu-id="d2114-132">In the Azure classic portal, check **Confirm that you have configured single sign-on as described above**.</span><span class="sxs-lookup"><span data-stu-id="d2114-132">In the Azure classic portal, check **Confirm that you have configured single sign-on as described above**.</span></span> <span data-ttu-id="d2114-133">Checking this will enable the current certificate to start working for this application checkbox.</span><span class="sxs-lookup"><span data-stu-id="d2114-133">Checking this will enable the current certificate to start working for this application checkbox.</span></span>
12. <span data-ttu-id="d2114-134">On the Single sign-on confirmation page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d2114-134">On the Single sign-on confirmation page, click **Complete**.</span></span>  

## <a name="creating-an-evidencecom-test-user"></a><span data-ttu-id="d2114-135">Creating an Evidence.com test user</span><span class="sxs-lookup"><span data-stu-id="d2114-135">Creating an Evidence.com test user</span></span>
<span data-ttu-id="d2114-136">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span><span class="sxs-lookup"><span data-stu-id="d2114-136">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span></span> <span data-ttu-id="d2114-137">This section describes how to create Azure AD user accounts inside Evidence.com</span><span class="sxs-lookup"><span data-stu-id="d2114-137">This section describes how to create Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="d2114-138">**To provision a user account in Evidence.com:**</span><span class="sxs-lookup"><span data-stu-id="d2114-138">**To provision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="d2114-139">In a web browser window, log into your Evidence.com company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d2114-139">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>
2. <span data-ttu-id="d2114-140">Navigate to **Admin** tab.</span><span class="sxs-lookup"><span data-stu-id="d2114-140">Navigate to **Admin** tab.</span></span>
3. <span data-ttu-id="d2114-141">Click on **Add User**.</span><span class="sxs-lookup"><span data-stu-id="d2114-141">Click on **Add User**.</span></span>
4. <span data-ttu-id="d2114-142">Click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d2114-142">Click the **Add** button.</span></span>
5. <span data-ttu-id="d2114-143">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span><span class="sxs-lookup"><span data-stu-id="d2114-143">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span></span> <span data-ttu-id="d2114-144">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure classic portal to change the nameidenitifer sent to Evidence.com to be the email address.</span><span class="sxs-lookup"><span data-stu-id="d2114-144">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure classic portal to change the nameidenitifer sent to Evidence.com to be the email address.</span></span>

## <a name="assigning-users-to-evidencecom"></a><span data-ttu-id="d2114-145">Assigning users to Evidence.com</span><span class="sxs-lookup"><span data-stu-id="d2114-145">Assigning users to Evidence.com</span></span>
<span data-ttu-id="d2114-146">For provisioned AAD users to be able to see Evidence.com on their Access Panel, they must be assigned access inside the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="d2114-146">For provisioned AAD users to be able to see Evidence.com on their Access Panel, they must be assigned access inside the Azure classic portal.</span></span>

<span data-ttu-id="d2114-147">**To assign users to Evidence.com:**</span><span class="sxs-lookup"><span data-stu-id="d2114-147">**To assign users to Evidence.com:**</span></span>

1. <span data-ttu-id="d2114-148">On the quick start page for Evidence.com in the Azure classic portal, click **Assign users to Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="d2114-148">On the quick start page for Evidence.com in the Azure classic portal, click **Assign users to Evidence.com**.</span></span>
2. <span data-ttu-id="d2114-149">In the **Show** menu, select whether you want to assign a user or a group to Evidence.com, and click the Checkmark button.</span><span class="sxs-lookup"><span data-stu-id="d2114-149">In the **Show** menu, select whether you want to assign a user or a group to Evidence.com, and click the Checkmark button.</span></span>
3. <span data-ttu-id="d2114-150">In the **Users** list, select the users to group to whom you want to assign Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="d2114-150">In the **Users** list, select the users to group to whom you want to assign Evidence.com.</span></span>
4. <span data-ttu-id="d2114-151">In the page footer, click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="d2114-151">In the page footer, click the **Assign** button.</span></span>

