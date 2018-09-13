---
title: 'Tutorial: Azure Active Directory integration with Workplace by Facebook | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Workplace by Facebook.
services: active-directory
documentationcenter: ''
author: asmalser-msft
manager: femila
editor: ''
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: asmalser
ms.openlocfilehash: fd27fe6efbd8ef63a9994bf4c0b004179c80ac40
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552928"
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="f251b-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="f251b-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>
<span data-ttu-id="f251b-104">The objective of this tutorial is to show you how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f251b-104">The objective of this tutorial is to show you how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f251b-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f251b-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="f251b-106">You can control in Azure AD who has access to Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="f251b-106">You can control in Azure AD who has access to Workplace by Facebook</span></span> 
* <span data-ttu-id="f251b-107">You can automatically provision account for users who have been granted access to Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="f251b-107">You can automatically provision account for users who have been granted access to Workplace by Facebook</span></span>
* <span data-ttu-id="f251b-108">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f251b-108">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="f251b-109">You can manage your accounts in one central location</span><span class="sxs-lookup"><span data-stu-id="f251b-109">You can manage your accounts in one central location</span></span> 

<span data-ttu-id="f251b-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f251b-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f251b-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f251b-111">Prerequisites</span></span>
<span data-ttu-id="f251b-112">To configure Azure AD integration with CS Stars, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f251b-112">To configure Azure AD integration with CS Stars, you need the following items:</span></span>

* <span data-ttu-id="f251b-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f251b-113">An Azure AD subscription</span></span>
* <span data-ttu-id="f251b-114">Workplace by Facebook with single sign on enabled</span><span class="sxs-lookup"><span data-stu-id="f251b-114">Workplace by Facebook with single sign on enabled</span></span>

<span data-ttu-id="f251b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f251b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="f251b-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="f251b-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="f251b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f251b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="f251b-118">Adding Workplace by Facebook from the gallery</span><span class="sxs-lookup"><span data-stu-id="f251b-118">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="f251b-119">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f251b-119">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f251b-120">**To add Workplace by Facebook from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f251b-120">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f251b-121">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f251b-121">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="f251b-123">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f251b-123">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="f251b-124">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f251b-124">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="f251b-126">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="f251b-126">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="f251b-128">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="f251b-128">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="f251b-130">In the search box, type **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="f251b-130">In the search box, type **Workplace by Facebook**.</span></span>
7. <span data-ttu-id="f251b-131">In the results pane, select **Workplace by Facebook**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="f251b-131">In the results pane, select **Workplace by Facebook**, and then click **Complete** to add the application.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f251b-132">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f251b-132">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="f251b-133">This section outlines how to enable users to authenticate to Workplace by Facebook with their account in Azure Active Directory, using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="f251b-133">This section outlines how to enable users to authenticate to Workplace by Facebook with their account in Azure Active Directory, using federation based on the SAML protocol.</span></span>

<span data-ttu-id="f251b-134">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f251b-134">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="f251b-135">After adding Workplace by Facebook in the Azure classic portal, click **Configure Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f251b-135">After adding Workplace by Facebook in the Azure classic portal, click **Configure Single Sign-On**.</span></span>
2. <span data-ttu-id="f251b-136">In the **Configure App URL** screen, enter the URL where users will sign into your Workplace by Facebook application.</span><span class="sxs-lookup"><span data-stu-id="f251b-136">In the **Configure App URL** screen, enter the URL where users will sign into your Workplace by Facebook application.</span></span> <span data-ttu-id="f251b-137">This is your Workplace by Facebook tenant URL (Example: https://example.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="f251b-137">This is your Workplace by Facebook tenant URL (Example: https://example.facebook.com/).</span></span> <span data-ttu-id="f251b-138">Once finished, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f251b-138">Once finished, click **Next**.</span></span>
3. <span data-ttu-id="f251b-139">In a different web browser window, log into your Workplace by Facebook company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f251b-139">In a different web browser window, log into your Workplace by Facebook company site as an administrator.</span></span>
4. <span data-ttu-id="f251b-140">Follow the instructions at the following URL to configure Workplace by Facebook to use Azure AD as an identity provider: [https://developers.facebook.com/docs/facebook-at-work/authentication/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/authentication/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="f251b-140">Follow the instructions at the following URL to configure Workplace by Facebook to use Azure AD as an identity provider: [https://developers.facebook.com/docs/facebook-at-work/authentication/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/authentication/cloud-providers)</span></span>
5. <span data-ttu-id="f251b-141">Once completed, return to the browser windows showing the Azure classic portal, click the checkbox to confirm you have completed the procedure, then click **Next** and **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f251b-141">Once completed, return to the browser windows showing the Azure classic portal, click the checkbox to confirm you have completed the procedure, then click **Next** and **Complete**.</span></span>


## <a name="automatically-provisioning-users-to-workplace-by-facebook"></a><span data-ttu-id="f251b-142">Automatically provisioning users to Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="f251b-142">Automatically provisioning users to Workplace by Facebook</span></span>
<span data-ttu-id="f251b-143">Azure AD supports the ability to automatically synchonize the account details of assigned users to Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="f251b-143">Azure AD supports the ability to automatically synchonize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="f251b-144">This automatic sychronization enables Workplace by Facebook to get the data it needs to authorize users for access, in advance of them attempting to sign-in for the first time.</span><span class="sxs-lookup"><span data-stu-id="f251b-144">This automatic sychronization enables Workplace by Facebook to get the data it needs to authorize users for access, in advance of them attempting to sign-in for the first time.</span></span> <span data-ttu-id="f251b-145">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f251b-145">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

<span data-ttu-id="f251b-146">Automatic provisioning can be set up by clicking **Configure account provisioning** in the Azure classic portal window.</span><span class="sxs-lookup"><span data-stu-id="f251b-146">Automatic provisioning can be set up by clicking **Configure account provisioning** in the Azure classic portal window.</span></span>

<span data-ttu-id="f251b-147">For additional details on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="f251b-147">For additional details on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="f251b-148">Assigning users to Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="f251b-148">Assigning users to Workplace by Facebook</span></span>
<span data-ttu-id="f251b-149">For provisioned AAD users to be able to see Workplace by Facebook on their Access Panel, they must be assigned access inside the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="f251b-149">For provisioned AAD users to be able to see Workplace by Facebook on their Access Panel, they must be assigned access inside the Azure classic portal.</span></span>

<span data-ttu-id="f251b-150">**To assign users to Workplace by Facebook:**</span><span class="sxs-lookup"><span data-stu-id="f251b-150">**To assign users to Workplace by Facebook:**</span></span>

1. <span data-ttu-id="f251b-151">On the start page for Workplace by Facebook in the Azure classic portal, click **Assign accounts**.</span><span class="sxs-lookup"><span data-stu-id="f251b-151">On the start page for Workplace by Facebook in the Azure classic portal, click **Assign accounts**.</span></span>
2. <span data-ttu-id="f251b-152">In the **Show** menu, select whether you want to assign a user or a group to Workplace by Facebook and click the Checkmark button.</span><span class="sxs-lookup"><span data-stu-id="f251b-152">In the **Show** menu, select whether you want to assign a user or a group to Workplace by Facebook and click the Checkmark button.</span></span>
3. <span data-ttu-id="f251b-153">In the resulting list, select the users or group to whom you want to assign Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="f251b-153">In the resulting list, select the users or group to whom you want to assign Workplace by Facebook.</span></span>
4. <span data-ttu-id="f251b-154">In the page footer, click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="f251b-154">In the page footer, click the **Assign** button.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f251b-155">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="f251b-155">Additional Resources</span></span>
* [<span data-ttu-id="f251b-156">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f251b-156">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f251b-157">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f251b-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png








