---
title: 'Tutorial: Azure Active Directory integration with TalentLMS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TalentLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 79e3b853728f6f997ad97a653ac3c119b2760cbd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866046"
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="177b5-103">Tutorial: Azure Active Directory integration with TalentLMS</span><span class="sxs-lookup"><span data-stu-id="177b5-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="177b5-104">In this tutorial, you learn how to integrate TalentLMS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="177b5-104">In this tutorial, you learn how to integrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="177b5-105">Integrating TalentLMS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="177b5-105">Integrating TalentLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="177b5-106">You can control in Azure AD who has access to TalentLMS</span><span class="sxs-lookup"><span data-stu-id="177b5-106">You can control in Azure AD who has access to TalentLMS</span></span>
- <span data-ttu-id="177b5-107">You can enable your users to automatically get signed-on to TalentLMS (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="177b5-107">You can enable your users to automatically get signed-on to TalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="177b5-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="177b5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="177b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="177b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="177b5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="177b5-110">Prerequisites</span></span>

<span data-ttu-id="177b5-111">To configure Azure AD integration with TalentLMS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="177b5-111">To configure Azure AD integration with TalentLMS, you need the following items:</span></span>

- <span data-ttu-id="177b5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="177b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="177b5-113">A TalentLMS single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="177b5-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="177b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="177b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="177b5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="177b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="177b5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="177b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="177b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="177b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="177b5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="177b5-118">Scenario description</span></span>
<span data-ttu-id="177b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="177b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="177b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="177b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="177b5-121">Adding TalentLMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="177b5-121">Adding TalentLMS from the gallery</span></span>
1. <span data-ttu-id="177b5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="177b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-the-gallery"></a><span data-ttu-id="177b5-123">Adding TalentLMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="177b5-123">Adding TalentLMS from the gallery</span></span>
<span data-ttu-id="177b5-124">To configure the integration of TalentLMS into Azure AD, you need to add TalentLMS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="177b5-124">To configure the integration of TalentLMS into Azure AD, you need to add TalentLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="177b5-125">**To add TalentLMS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="177b5-125">**To add TalentLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="177b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="177b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="177b5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="177b5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="177b5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="177b5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="177b5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="177b5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="177b5-133">In the search box, type **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="177b5-133">In the search box, type **TalentLMS**.</span></span>

    ![Creating an Azure AD test user](./media/talentlms-tutorial/tutorial_talentlms_search.png)

1. <span data-ttu-id="177b5-135">In the results panel, select **TalentLMS**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="177b5-135">In the results panel, select **TalentLMS**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="177b5-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="177b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="177b5-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="177b5-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="177b5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TalentLMS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="177b5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TalentLMS is to a user in Azure AD.</span></span> <span data-ttu-id="177b5-140">In other words, a link relationship between an Azure AD user and the related user in TalentLMS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="177b5-140">In other words, a link relationship between an Azure AD user and the related user in TalentLMS needs to be established.</span></span>

<span data-ttu-id="177b5-141">In TalentLMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="177b5-141">In TalentLMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="177b5-142">To configure and test Azure AD single sign-on with TalentLMS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="177b5-142">To configure and test Azure AD single sign-on with TalentLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="177b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="177b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="177b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="177b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="177b5-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - to have a counterpart of Britta Simon in TalentLMS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="177b5-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - to have a counterpart of Britta Simon in TalentLMS that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="177b5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="177b5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="177b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="177b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="177b5-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="177b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="177b5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TalentLMS application.</span><span class="sxs-lookup"><span data-stu-id="177b5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="177b5-150">**To configure Azure AD single sign-on with TalentLMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="177b5-150">**To configure Azure AD single sign-on with TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="177b5-151">In the Azure portal, on the **TalentLMS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="177b5-151">In the Azure portal, on the **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="177b5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="177b5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_talentlms_samlbase.png)

1. <span data-ttu-id="177b5-155">On the **TalentLMS Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="177b5-155">On the **TalentLMS Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="177b5-157">a.</span><span class="sxs-lookup"><span data-stu-id="177b5-157">a.</span></span> <span data-ttu-id="177b5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="177b5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="177b5-159">b.</span><span class="sxs-lookup"><span data-stu-id="177b5-159">b.</span></span> <span data-ttu-id="177b5-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="177b5-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="177b5-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="177b5-161">These values are not real.</span></span> <span data-ttu-id="177b5-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="177b5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="177b5-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="177b5-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values.</span></span> 
 
1. <span data-ttu-id="177b5-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span><span class="sxs-lookup"><span data-stu-id="177b5-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_talentlms_certificate.png) 

1. <span data-ttu-id="177b5-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="177b5-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="177b5-168">On the **TalentLMS Configuration** section, click **Configure TalentLMS** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="177b5-168">On the **TalentLMS Configuration** section, click **Configure TalentLMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="177b5-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="177b5-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_talentlms_configure.png)  

1. <span data-ttu-id="177b5-171">In a different web browser window, log in to your TalentLMS company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="177b5-171">In a different web browser window, log in to your TalentLMS company site as an administrator.</span></span>

1. <span data-ttu-id="177b5-172">In the **Account & Settings** section, click the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="177b5-172">In the **Account & Settings** section, click the **Users** tab.</span></span>
   
    <span data-ttu-id="177b5-173">![Account & Settings](./media/talentlms-tutorial/IC777296.png "Account & Settings")</span><span class="sxs-lookup"><span data-stu-id="177b5-173">![Account & Settings](./media/talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

1. <span data-ttu-id="177b5-174">Click **Single Sign-On (SSO)**,</span><span class="sxs-lookup"><span data-stu-id="177b5-174">Click **Single Sign-On (SSO)**,</span></span>

1. <span data-ttu-id="177b5-175">In the Single Sign-On section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="177b5-175">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="177b5-176">![Single Sign-On](./media/talentlms-tutorial/IC777297.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="177b5-176">![Single Sign-On](./media/talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="177b5-177">a.</span><span class="sxs-lookup"><span data-stu-id="177b5-177">a.</span></span> <span data-ttu-id="177b5-178">From the **SSO integration type** list, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="177b5-178">From the **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="177b5-179">b.</span><span class="sxs-lookup"><span data-stu-id="177b5-179">b.</span></span> <span data-ttu-id="177b5-180">In the **Identity provider (IDP)** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="177b5-180">In the **Identity provider (IDP)** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="177b5-181">c.</span><span class="sxs-lookup"><span data-stu-id="177b5-181">c.</span></span> <span data-ttu-id="177b5-182">Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="177b5-182">Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="177b5-183">d.</span><span class="sxs-lookup"><span data-stu-id="177b5-183">d.</span></span>  <span data-ttu-id="177b5-184">In the **Remote sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="177b5-184">In the **Remote sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="177b5-185">e.</span><span class="sxs-lookup"><span data-stu-id="177b5-185">e.</span></span> <span data-ttu-id="177b5-186">In the **Remote sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="177b5-186">In the **Remote sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="177b5-187">f.</span><span class="sxs-lookup"><span data-stu-id="177b5-187">f.</span></span> <span data-ttu-id="177b5-188">Fill in the following:</span><span class="sxs-lookup"><span data-stu-id="177b5-188">Fill in the following:</span></span> 

    * <span data-ttu-id="177b5-189">In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="177b5-189">In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="177b5-190">In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="177b5-190">In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="177b5-191">In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="177b5-191">In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="177b5-192">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="177b5-192">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
1. <span data-ttu-id="177b5-193">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="177b5-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="177b5-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="177b5-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="177b5-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="177b5-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="177b5-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="177b5-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="177b5-197">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="177b5-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="177b5-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="177b5-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="177b5-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="177b5-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="177b5-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="177b5-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/talentlms-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="177b5-203">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="177b5-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/talentlms-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="177b5-205">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="177b5-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/talentlms-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="177b5-207">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="177b5-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="177b5-209">a.</span><span class="sxs-lookup"><span data-stu-id="177b5-209">a.</span></span> <span data-ttu-id="177b5-210">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="177b5-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="177b5-211">b.</span><span class="sxs-lookup"><span data-stu-id="177b5-211">b.</span></span> <span data-ttu-id="177b5-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="177b5-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="177b5-213">c.</span><span class="sxs-lookup"><span data-stu-id="177b5-213">c.</span></span> <span data-ttu-id="177b5-214">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="177b5-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="177b5-215">d.</span><span class="sxs-lookup"><span data-stu-id="177b5-215">d.</span></span> <span data-ttu-id="177b5-216">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="177b5-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="177b5-217">Creating a TalentLMS test user</span><span class="sxs-lookup"><span data-stu-id="177b5-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="177b5-218">To enable Azure AD users to log in to TalentLMS, they must be provisioned into TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="177b5-218">To enable Azure AD users to log in to TalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="177b5-219">In the case of TalentLMS, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="177b5-219">In the case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="177b5-220">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="177b5-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="177b5-221">Log in to your **TalentLMS** tenant.</span><span class="sxs-lookup"><span data-stu-id="177b5-221">Log in to your **TalentLMS** tenant.</span></span>

1. <span data-ttu-id="177b5-222">Click **Users**, and then click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="177b5-222">Click **Users**, and then click **Add User**.</span></span>

1. <span data-ttu-id="177b5-223">On the **Add user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="177b5-223">On the **Add user** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="177b5-224">![Add User](./media/talentlms-tutorial/IC777299.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="177b5-224">![Add User](./media/talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="177b5-225">a.</span><span class="sxs-lookup"><span data-stu-id="177b5-225">a.</span></span> <span data-ttu-id="177b5-226">In the **First name** textbox, enter the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="177b5-226">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="177b5-227">b.</span><span class="sxs-lookup"><span data-stu-id="177b5-227">b.</span></span> <span data-ttu-id="177b5-228">In the **Last name** textbox, enter the last name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="177b5-228">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="177b5-229">c.</span><span class="sxs-lookup"><span data-stu-id="177b5-229">c.</span></span> <span data-ttu-id="177b5-230">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="177b5-230">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="177b5-231">d.</span><span class="sxs-lookup"><span data-stu-id="177b5-231">d.</span></span> <span data-ttu-id="177b5-232">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="177b5-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="177b5-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="177b5-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="177b5-234">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="177b5-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="177b5-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="177b5-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TalentLMS.</span></span>

![Assign User][200] 

<span data-ttu-id="177b5-237">**To assign Britta Simon to TalentLMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="177b5-237">**To assign Britta Simon to TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="177b5-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="177b5-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="177b5-240">In the applications list, select **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="177b5-240">In the applications list, select **TalentLMS**.</span></span>

    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_talentlms_app.png) 

1. <span data-ttu-id="177b5-242">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="177b5-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="177b5-244">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="177b5-244">Click **Add** button.</span></span> <span data-ttu-id="177b5-245">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="177b5-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="177b5-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="177b5-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="177b5-248">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="177b5-248">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="177b5-249">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="177b5-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="177b5-250">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="177b5-250">Testing single sign-on</span></span>

<span data-ttu-id="177b5-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="177b5-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="177b5-252">When you click the TalentLMS tile in the Access Panel, you should get automatically signed-on to your TalentLMS application</span><span class="sxs-lookup"><span data-stu-id="177b5-252">When you click the TalentLMS tile in the Access Panel, you should get automatically signed-on to your TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="177b5-253">Additional resources</span><span class="sxs-lookup"><span data-stu-id="177b5-253">Additional resources</span></span>

* [<span data-ttu-id="177b5-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="177b5-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="177b5-255">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="177b5-255">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/talentlms-tutorial/tutorial_general_01.png
[2]: ./media/talentlms-tutorial/tutorial_general_02.png
[3]: ./media/talentlms-tutorial/tutorial_general_03.png
[4]: ./media/talentlms-tutorial/tutorial_general_04.png

[100]: ./media/talentlms-tutorial/tutorial_general_100.png

[200]: ./media/talentlms-tutorial/tutorial_general_200.png
[201]: ./media/talentlms-tutorial/tutorial_general_201.png
[202]: ./media/talentlms-tutorial/tutorial_general_202.png
[203]: ./media/talentlms-tutorial/tutorial_general_203.png

