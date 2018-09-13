---
title: 'Tutorial: Azure Active Directory integration with Projectplace | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Projectplace.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 4bbe1fc855dfaf637f5893fff795f47b50bd80c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968966"
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="293ac-103">Tutorial: Azure Active Directory integration with Projectplace</span><span class="sxs-lookup"><span data-stu-id="293ac-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="293ac-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="293ac-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="293ac-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="293ac-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="293ac-106">You can control in Azure AD who has access to Projectplace</span><span class="sxs-lookup"><span data-stu-id="293ac-106">You can control in Azure AD who has access to Projectplace</span></span>
- <span data-ttu-id="293ac-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="293ac-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="293ac-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="293ac-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="293ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="293ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="293ac-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="293ac-110">Prerequisites</span></span>

<span data-ttu-id="293ac-111">To configure Azure AD integration with Projectplace, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="293ac-111">To configure Azure AD integration with Projectplace, you need the following items:</span></span>

- <span data-ttu-id="293ac-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="293ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="293ac-113">A Projectplace single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="293ac-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="293ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="293ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="293ac-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="293ac-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="293ac-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="293ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="293ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="293ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="293ac-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="293ac-118">Scenario description</span></span>
<span data-ttu-id="293ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="293ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="293ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="293ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="293ac-121">Adding Projectplace from the gallery</span><span class="sxs-lookup"><span data-stu-id="293ac-121">Adding Projectplace from the gallery</span></span>
1. <span data-ttu-id="293ac-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="293ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-the-gallery"></a><span data-ttu-id="293ac-123">Adding Projectplace from the gallery</span><span class="sxs-lookup"><span data-stu-id="293ac-123">Adding Projectplace from the gallery</span></span>
<span data-ttu-id="293ac-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="293ac-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="293ac-125">**To add Projectplace from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="293ac-125">**To add Projectplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="293ac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="293ac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="293ac-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="293ac-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="293ac-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="293ac-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="293ac-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="293ac-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="293ac-133">In the search box, type **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="293ac-133">In the search box, type **Projectplace**.</span></span>

    ![Creating an Azure AD test user](./media/projectplace-tutorial/tutorial_projectplace_search.png)

1. <span data-ttu-id="293ac-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="293ac-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="293ac-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="293ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="293ac-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="293ac-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="293ac-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="293ac-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span></span> <span data-ttu-id="293ac-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span><span class="sxs-lookup"><span data-stu-id="293ac-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span></span>

<span data-ttu-id="293ac-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="293ac-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="293ac-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="293ac-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="293ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="293ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="293ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="293ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="293ac-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="293ac-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="293ac-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="293ac-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="293ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="293ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="293ac-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="293ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="293ac-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span><span class="sxs-lookup"><span data-stu-id="293ac-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="293ac-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="293ac-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="293ac-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="293ac-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="293ac-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="293ac-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/projectplace-tutorial/tutorial_projectplace_samlbase.png)

1. <span data-ttu-id="293ac-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="293ac-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="293ac-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="293ac-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="293ac-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="293ac-158">This value is not real.</span></span> <span data-ttu-id="293ac-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="293ac-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="293ac-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span><span class="sxs-lookup"><span data-stu-id="293ac-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span></span> 
 
1. <span data-ttu-id="293ac-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="293ac-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/projectplace-tutorial/tutorial_projectplace_certificate.png) 

1. <span data-ttu-id="293ac-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="293ac-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/projectplace-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="293ac-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="293ac-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="293ac-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="293ac-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="293ac-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="293ac-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="293ac-168">You will get a notification as soon as the configuration has been completed.</span><span class="sxs-lookup"><span data-stu-id="293ac-168">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="293ac-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="293ac-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="293ac-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="293ac-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="293ac-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="293ac-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="293ac-172">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="293ac-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="293ac-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="293ac-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="293ac-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="293ac-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="293ac-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="293ac-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/projectplace-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="293ac-178">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="293ac-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/projectplace-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="293ac-180">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="293ac-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/projectplace-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="293ac-182">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="293ac-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="293ac-184">a.</span><span class="sxs-lookup"><span data-stu-id="293ac-184">a.</span></span> <span data-ttu-id="293ac-185">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="293ac-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="293ac-186">b.</span><span class="sxs-lookup"><span data-stu-id="293ac-186">b.</span></span> <span data-ttu-id="293ac-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="293ac-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="293ac-188">c.</span><span class="sxs-lookup"><span data-stu-id="293ac-188">c.</span></span> <span data-ttu-id="293ac-189">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="293ac-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="293ac-190">d.</span><span class="sxs-lookup"><span data-stu-id="293ac-190">d.</span></span> <span data-ttu-id="293ac-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="293ac-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="293ac-192">Creating a Projectplace test user</span><span class="sxs-lookup"><span data-stu-id="293ac-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="293ac-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span><span class="sxs-lookup"><span data-stu-id="293ac-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="293ac-194">In the case of Projectplace, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="293ac-194">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="293ac-195">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="293ac-195">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="293ac-196">Log in to your **Projectplace** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="293ac-196">Log in to your **Projectplace** company site as an administrator.</span></span>

1. <span data-ttu-id="293ac-197">Go to **People**, and then click **Members**.</span><span class="sxs-lookup"><span data-stu-id="293ac-197">Go to **People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="293ac-198">![People](./media/projectplace-tutorial/ic790228.png "People")</span><span class="sxs-lookup"><span data-stu-id="293ac-198">![People](./media/projectplace-tutorial/ic790228.png "People")</span></span>

1. <span data-ttu-id="293ac-199">Click **Add Member**.</span><span class="sxs-lookup"><span data-stu-id="293ac-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="293ac-200">![Add Members](./media/projectplace-tutorial/ic790232.png "Add Members")</span><span class="sxs-lookup"><span data-stu-id="293ac-200">![Add Members](./media/projectplace-tutorial/ic790232.png "Add Members")</span></span>

1. <span data-ttu-id="293ac-201">In the **Add Member** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="293ac-201">In the **Add Member** section, perform the following steps:</span></span>
   
    <span data-ttu-id="293ac-202">![New Members](./media/projectplace-tutorial/ic790233.png "New Members")</span><span class="sxs-lookup"><span data-stu-id="293ac-202">![New Members](./media/projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="293ac-203">a.</span><span class="sxs-lookup"><span data-stu-id="293ac-203">a.</span></span> <span data-ttu-id="293ac-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="293ac-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="293ac-205">b.</span><span class="sxs-lookup"><span data-stu-id="293ac-205">b.</span></span> <span data-ttu-id="293ac-206">Click **Send**.</span><span class="sxs-lookup"><span data-stu-id="293ac-206">Click **Send**.</span></span>

   <span data-ttu-id="293ac-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span><span class="sxs-lookup"><span data-stu-id="293ac-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="293ac-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="293ac-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="293ac-209">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="293ac-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="293ac-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span><span class="sxs-lookup"><span data-stu-id="293ac-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span></span>

![Assign User][200] 

<span data-ttu-id="293ac-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="293ac-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="293ac-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="293ac-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="293ac-215">In the applications list, select **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="293ac-215">In the applications list, select **Projectplace**.</span></span>

    ![Configure Single Sign-On](./media/projectplace-tutorial/tutorial_projectplace_app.png) 

1. <span data-ttu-id="293ac-217">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="293ac-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="293ac-219">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="293ac-219">Click **Add** button.</span></span> <span data-ttu-id="293ac-220">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="293ac-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="293ac-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="293ac-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="293ac-223">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="293ac-223">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="293ac-224">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="293ac-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="293ac-225">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="293ac-225">Testing single sign-on</span></span>

<span data-ttu-id="293ac-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="293ac-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="293ac-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span><span class="sxs-lookup"><span data-stu-id="293ac-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span></span>
<span data-ttu-id="293ac-228">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="293ac-228">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="293ac-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="293ac-229">Additional resources</span></span>

* [<span data-ttu-id="293ac-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="293ac-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="293ac-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="293ac-231">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/projectplace-tutorial/tutorial_general_01.png
[2]: ./media/projectplace-tutorial/tutorial_general_02.png
[3]: ./media/projectplace-tutorial/tutorial_general_03.png
[4]: ./media/projectplace-tutorial/tutorial_general_04.png

[100]: ./media/projectplace-tutorial/tutorial_general_100.png

[200]: ./media/projectplace-tutorial/tutorial_general_200.png
[201]: ./media/projectplace-tutorial/tutorial_general_201.png
[202]: ./media/projectplace-tutorial/tutorial_general_202.png
[203]: ./media/projectplace-tutorial/tutorial_general_203.png
