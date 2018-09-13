---
title: 'Tutorial: Azure Active Directory integration with Oneteam | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Oneteam.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b7c2ac18a683ccbe07c7c4cdc750399d8466c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967158"
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="e379b-103">Tutorial: Azure Active Directory integration with Oneteam</span><span class="sxs-lookup"><span data-stu-id="e379b-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="e379b-104">In this tutorial, you learn how to integrate Oneteam with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e379b-104">In this tutorial, you learn how to integrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e379b-105">Integrating Oneteam with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e379b-105">Integrating Oneteam with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e379b-106">You can control in Azure AD who has access to Oneteam</span><span class="sxs-lookup"><span data-stu-id="e379b-106">You can control in Azure AD who has access to Oneteam</span></span>
- <span data-ttu-id="e379b-107">You can enable your users to automatically get signed-on to Oneteam (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e379b-107">You can enable your users to automatically get signed-on to Oneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e379b-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e379b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e379b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e379b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e379b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e379b-110">Prerequisites</span></span>

<span data-ttu-id="e379b-111">To configure Azure AD integration with Oneteam, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e379b-111">To configure Azure AD integration with Oneteam, you need the following items:</span></span>

- <span data-ttu-id="e379b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e379b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e379b-113">A Oneteam single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e379b-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e379b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e379b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e379b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e379b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e379b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e379b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e379b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e379b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e379b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e379b-118">Scenario description</span></span>
<span data-ttu-id="e379b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e379b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e379b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e379b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e379b-121">Adding Oneteam from the gallery</span><span class="sxs-lookup"><span data-stu-id="e379b-121">Adding Oneteam from the gallery</span></span>
1. <span data-ttu-id="e379b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e379b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-the-gallery"></a><span data-ttu-id="e379b-123">Adding Oneteam from the gallery</span><span class="sxs-lookup"><span data-stu-id="e379b-123">Adding Oneteam from the gallery</span></span>
<span data-ttu-id="e379b-124">To configure the integration of Oneteam into Azure AD, you need to add Oneteam from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e379b-124">To configure the integration of Oneteam into Azure AD, you need to add Oneteam from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e379b-125">**To add Oneteam from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e379b-125">**To add Oneteam from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e379b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e379b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="e379b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e379b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e379b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e379b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="e379b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e379b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="e379b-133">In the search box, type **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="e379b-133">In the search box, type **Oneteam**.</span></span>

    ![Creating an Azure AD test user](./media/oneteam-tutorial/tutorial_oneteam_search.png)

1. <span data-ttu-id="e379b-135">In the results panel, select **Oneteam**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e379b-135">In the results panel, select **Oneteam**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e379b-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e379b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e379b-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e379b-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e379b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Oneteam is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e379b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Oneteam is to a user in Azure AD.</span></span> <span data-ttu-id="e379b-140">In other words, a link relationship between an Azure AD user and the related user in Oneteam needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e379b-140">In other words, a link relationship between an Azure AD user and the related user in Oneteam needs to be established.</span></span>

<span data-ttu-id="e379b-141">In Oneteam, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="e379b-141">In Oneteam, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e379b-142">To configure and test Azure AD single sign-on with Oneteam, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e379b-142">To configure and test Azure AD single sign-on with Oneteam, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e379b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e379b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e379b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e379b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e379b-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - to have a counterpart of Britta Simon in Oneteam that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e379b-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - to have a counterpart of Britta Simon in Oneteam that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e379b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e379b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e379b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e379b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e379b-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e379b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e379b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Oneteam application.</span><span class="sxs-lookup"><span data-stu-id="e379b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="e379b-150">**To configure Azure AD single sign-on with Oneteam, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e379b-150">**To configure Azure AD single sign-on with Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="e379b-151">In the Azure portal, on the **Oneteam** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e379b-151">In the Azure portal, on the **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="e379b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e379b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/oneteam-tutorial/tutorial_oneteam_samlbase.png)

1. <span data-ttu-id="e379b-155">On the **Oneteam Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="e379b-155">On the **Oneteam Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="e379b-157">a.</span><span class="sxs-lookup"><span data-stu-id="e379b-157">a.</span></span> <span data-ttu-id="e379b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="e379b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="e379b-159">b.</span><span class="sxs-lookup"><span data-stu-id="e379b-159">b.</span></span> <span data-ttu-id="e379b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="e379b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

1. <span data-ttu-id="e379b-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="e379b-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="e379b-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="e379b-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="e379b-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="e379b-164">These values are not real.</span></span> <span data-ttu-id="e379b-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="e379b-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e379b-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) to get these values.</span><span class="sxs-lookup"><span data-stu-id="e379b-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) to get these values.</span></span> 



1. <span data-ttu-id="e379b-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e379b-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/oneteam-tutorial/tutorial_oneteam_certificate.png) 

1. <span data-ttu-id="e379b-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e379b-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/oneteam-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="e379b-171">To get SSO configured for your application, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them the downloaded **Metadata**.</span><span class="sxs-lookup"><span data-stu-id="e379b-171">To get SSO configured for your application, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them the downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="e379b-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="e379b-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e379b-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="e379b-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e379b-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e379b-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e379b-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e379b-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="e379b-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e379b-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="e379b-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e379b-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e379b-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e379b-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/oneteam-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="e379b-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e379b-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/oneteam-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="e379b-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="e379b-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/oneteam-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="e379b-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e379b-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e379b-187">a.</span><span class="sxs-lookup"><span data-stu-id="e379b-187">a.</span></span> <span data-ttu-id="e379b-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e379b-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e379b-189">b.</span><span class="sxs-lookup"><span data-stu-id="e379b-189">b.</span></span> <span data-ttu-id="e379b-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e379b-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e379b-191">c.</span><span class="sxs-lookup"><span data-stu-id="e379b-191">c.</span></span> <span data-ttu-id="e379b-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="e379b-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e379b-193">d.</span><span class="sxs-lookup"><span data-stu-id="e379b-193">d.</span></span> <span data-ttu-id="e379b-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e379b-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="e379b-195">Creating a Oneteam test user</span><span class="sxs-lookup"><span data-stu-id="e379b-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="e379b-196">The objective of this section is to create a user called Britta Simon in Oneteam.</span><span class="sxs-lookup"><span data-stu-id="e379b-196">The objective of this section is to create a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="e379b-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="e379b-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="e379b-198">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="e379b-198">There is no action item for you in this section.</span></span> <span data-ttu-id="e379b-199">A new user will be created during an attempt to access Oneteam, if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="e379b-199">A new user will be created during an attempt to access Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="e379b-200">If you need to create an user manually, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="e379b-200">If you need to create an user manually, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e379b-201">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e379b-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e379b-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Oneteam.</span><span class="sxs-lookup"><span data-stu-id="e379b-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Oneteam.</span></span>

![Assign User][200] 

<span data-ttu-id="e379b-204">**To assign Britta Simon to Oneteam, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e379b-204">**To assign Britta Simon to Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="e379b-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e379b-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e379b-207">In the applications list, select **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="e379b-207">In the applications list, select **Oneteam**.</span></span>

    ![Configure Single Sign-On](./media/oneteam-tutorial/tutorial_oneteam_app.png) 

1. <span data-ttu-id="e379b-209">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e379b-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="e379b-211">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e379b-211">Click **Add** button.</span></span> <span data-ttu-id="e379b-212">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e379b-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="e379b-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e379b-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e379b-215">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e379b-215">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e379b-216">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e379b-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e379b-217">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="e379b-217">Testing single sign-on</span></span>

<span data-ttu-id="e379b-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e379b-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e379b-219">When you click the Oneteam tile in the Access Panel, you should get automatically signed-on to your Oneteam application.</span><span class="sxs-lookup"><span data-stu-id="e379b-219">When you click the Oneteam tile in the Access Panel, you should get automatically signed-on to your Oneteam application.</span></span>
<span data-ttu-id="e379b-220">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e379b-220">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e379b-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e379b-221">Additional resources</span></span>

* [<span data-ttu-id="e379b-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e379b-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e379b-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e379b-223">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/oneteam-tutorial/tutorial_general_01.png
[2]: ./media/oneteam-tutorial/tutorial_general_02.png
[3]: ./media/oneteam-tutorial/tutorial_general_03.png
[4]: ./media/oneteam-tutorial/tutorial_general_04.png

[100]: ./media/oneteam-tutorial/tutorial_general_100.png

[200]: ./media/oneteam-tutorial/tutorial_general_200.png
[201]: ./media/oneteam-tutorial/tutorial_general_201.png
[202]: ./media/oneteam-tutorial/tutorial_general_202.png
[203]: ./media/oneteam-tutorial/tutorial_general_203.png

