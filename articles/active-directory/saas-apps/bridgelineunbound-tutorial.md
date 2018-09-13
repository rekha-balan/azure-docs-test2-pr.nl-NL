---
title: 'Tutorial: Azure Active Directory integration with Bridgeline Unbound | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bridgeline Unbound.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b018472f-c8b3-403d-ae66-9ed26a35f413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2018
ms.author: jeedes
ms.openlocfilehash: c429afa12bc11db68d041fef96f66b3f4c7f0b1b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869457"
---
# <a name="tutorial-azure-active-directory-integration-with-bridgeline-unbound"></a><span data-ttu-id="ceee6-103">Tutorial: Azure Active Directory integration with Bridgeline Unbound</span><span class="sxs-lookup"><span data-stu-id="ceee6-103">Tutorial: Azure Active Directory integration with Bridgeline Unbound</span></span>

<span data-ttu-id="ceee6-104">In this tutorial, you learn how to integrate Bridgeline Unbound with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ceee6-104">In this tutorial, you learn how to integrate Bridgeline Unbound with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ceee6-105">Integrating Bridgeline Unbound with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ceee6-105">Integrating Bridgeline Unbound with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ceee6-106">You can control in Azure AD who has access to Bridgeline Unbound.</span><span class="sxs-lookup"><span data-stu-id="ceee6-106">You can control in Azure AD who has access to Bridgeline Unbound.</span></span>
- <span data-ttu-id="ceee6-107">You can enable your users to automatically get signed-on to Bridgeline Unbound (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="ceee6-107">You can enable your users to automatically get signed-on to Bridgeline Unbound (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ceee6-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ceee6-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ceee6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ceee6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ceee6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ceee6-110">Prerequisites</span></span>

<span data-ttu-id="ceee6-111">To configure Azure AD integration with Bridgeline Unbound, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ceee6-111">To configure Azure AD integration with Bridgeline Unbound, you need the following items:</span></span>

- <span data-ttu-id="ceee6-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ceee6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ceee6-113">A Bridgeline Unbound single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ceee6-113">A Bridgeline Unbound single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ceee6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ceee6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ceee6-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ceee6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ceee6-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ceee6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ceee6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ceee6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ceee6-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ceee6-118">Scenario description</span></span>
<span data-ttu-id="ceee6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ceee6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ceee6-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ceee6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ceee6-121">Adding Bridgeline Unbound from the gallery</span><span class="sxs-lookup"><span data-stu-id="ceee6-121">Adding Bridgeline Unbound from the gallery</span></span>
2. <span data-ttu-id="ceee6-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ceee6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bridgeline-unbound-from-the-gallery"></a><span data-ttu-id="ceee6-123">Adding Bridgeline Unbound from the gallery</span><span class="sxs-lookup"><span data-stu-id="ceee6-123">Adding Bridgeline Unbound from the gallery</span></span>
<span data-ttu-id="ceee6-124">To configure the integration of Bridgeline Unbound into Azure AD, you need to add Bridgeline Unbound from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ceee6-124">To configure the integration of Bridgeline Unbound into Azure AD, you need to add Bridgeline Unbound from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ceee6-125">**To add Bridgeline Unbound from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ceee6-125">**To add Bridgeline Unbound from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ceee6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ceee6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="ceee6-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ceee6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ceee6-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ceee6-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="ceee6-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ceee6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="ceee6-133">In the search box, type **Bridgeline Unbound**, select **Bridgeline Unbound** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ceee6-133">In the search box, type **Bridgeline Unbound**, select **Bridgeline Unbound** from result panel then click **Add** button to add the application.</span></span>

    ![Bridgeline Unbound in the results list](./media/bridgelineunbound-tutorial/tutorial_bridgelineunbound_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ceee6-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ceee6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ceee6-136">In this section, you configure and test Azure AD single sign-on with Bridgeline Unbound based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ceee6-136">In this section, you configure and test Azure AD single sign-on with Bridgeline Unbound based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ceee6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bridgeline Unbound is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ceee6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bridgeline Unbound is to a user in Azure AD.</span></span> <span data-ttu-id="ceee6-138">In other words, a link relationship between an Azure AD user and the related user in Bridgeline Unbound needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ceee6-138">In other words, a link relationship between an Azure AD user and the related user in Bridgeline Unbound needs to be established.</span></span>

<span data-ttu-id="ceee6-139">To configure and test Azure AD single sign-on with Bridgeline Unbound, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ceee6-139">To configure and test Azure AD single sign-on with Bridgeline Unbound, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ceee6-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ceee6-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ceee6-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ceee6-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ceee6-142">**[Create a Bridgeline Unbound test user](#create-a-bridgeline-unbound-test-user)** - to have a counterpart of Britta Simon in Bridgeline Unbound that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ceee6-142">**[Create a Bridgeline Unbound test user](#create-a-bridgeline-unbound-test-user)** - to have a counterpart of Britta Simon in Bridgeline Unbound that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ceee6-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ceee6-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ceee6-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ceee6-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ceee6-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ceee6-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ceee6-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bridgeline Unbound application.</span><span class="sxs-lookup"><span data-stu-id="ceee6-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bridgeline Unbound application.</span></span>

<span data-ttu-id="ceee6-147">**To configure Azure AD single sign-on with Bridgeline Unbound, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ceee6-147">**To configure Azure AD single sign-on with Bridgeline Unbound, perform the following steps:**</span></span>

1. <span data-ttu-id="ceee6-148">In the Azure portal, on the **Bridgeline Unbound** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ceee6-148">In the Azure portal, on the **Bridgeline Unbound** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="ceee6-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ceee6-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/bridgelineunbound-tutorial/tutorial_bridgelineunbound_samlbase.png)
 
3. <span data-ttu-id="ceee6-152">On the **Bridgeline Unbound Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="ceee6-152">On the **Bridgeline Unbound Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Bridgeline Domain and URLs single sign-on information](./media/bridgelineunbound-tutorial/tutorial_bridgelineunbound_url.png)

    <span data-ttu-id="ceee6-154">a.</span><span class="sxs-lookup"><span data-stu-id="ceee6-154">a.</span></span> <span data-ttu-id="ceee6-155">In the **Identifier** textbox, type a URL using the following pattern: `iApps_UPSTT_<ENVIRONMENTNAME>`</span><span class="sxs-lookup"><span data-stu-id="ceee6-155">In the **Identifier** textbox, type a URL using the following pattern: `iApps_UPSTT_<ENVIRONMENTNAME>`</span></span>

    <span data-ttu-id="ceee6-156">b.</span><span class="sxs-lookup"><span data-stu-id="ceee6-156">b.</span></span> <span data-ttu-id="ceee6-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.iapps.com/SAMLAssertionService.aspx`</span><span class="sxs-lookup"><span data-stu-id="ceee6-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.iapps.com/SAMLAssertionService.aspx`</span></span>

4. <span data-ttu-id="ceee6-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="ceee6-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Bridgeline Domain and URLs single sign-on information](./media/bridgelineunbound-tutorial/tutorial_bridgelineunbound_url1.png)

    <span data-ttu-id="ceee6-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.iapps.com/CommonLogin/login?<INSTANCENAME>`</span><span class="sxs-lookup"><span data-stu-id="ceee6-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.iapps.com/CommonLogin/login?<INSTANCENAME>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ceee6-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="ceee6-161">These values are not real.</span></span> <span data-ttu-id="ceee6-162">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="ceee6-162">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="ceee6-163">Contact [Bridgeline Unbound Client support team](mailto:support@iapps.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="ceee6-163">Contact [Bridgeline Unbound Client support team](mailto:support@iapps.com) to get these values.</span></span> 

4. <span data-ttu-id="ceee6-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ceee6-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/bridgelineunbound-tutorial/tutorial_bridgelineunbound_certificate.png) 

5. <span data-ttu-id="ceee6-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ceee6-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/bridgelineunbound-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ceee6-168">On the **Bridgeline Unbound Configuration** section, click **Configure Bridgeline Unbound** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="ceee6-168">On the **Bridgeline Unbound Configuration** section, click **Configure Bridgeline Unbound** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ceee6-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="ceee6-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Bridgeline Unbound Configuration](./media/bridgelineunbound-tutorial/tutorial_bridgelineunbound_configure.png) 

7. <span data-ttu-id="ceee6-171">To configure single sign-on on **Bridgeline Unbound** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Bridgeline Unbound support team](mailto:support@iapps.com).</span><span class="sxs-lookup"><span data-stu-id="ceee6-171">To configure single sign-on on **Bridgeline Unbound** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Bridgeline Unbound support team](mailto:support@iapps.com).</span></span> <span data-ttu-id="ceee6-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="ceee6-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ceee6-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ceee6-173">Create an Azure AD test user</span></span>

<span data-ttu-id="ceee6-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ceee6-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="ceee6-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ceee6-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ceee6-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="ceee6-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/bridgelineunbound-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ceee6-179">To display the list of users, go to **Users and grobridgelineinbound**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ceee6-179">To display the list of users, go to **Users and grobridgelineinbound**, and then click **All users**.</span></span>

    ![The "Users and grobridgelineinbound" and "All users" links](./media/bridgelineunbound-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ceee6-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ceee6-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/bridgelineunbound-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ceee6-183">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ceee6-183">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/bridgelineunbound-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ceee6-185">a.</span><span class="sxs-lookup"><span data-stu-id="ceee6-185">a.</span></span> <span data-ttu-id="ceee6-186">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ceee6-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ceee6-187">b.</span><span class="sxs-lookup"><span data-stu-id="ceee6-187">b.</span></span> <span data-ttu-id="ceee6-188">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ceee6-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ceee6-189">c.</span><span class="sxs-lookup"><span data-stu-id="ceee6-189">c.</span></span> <span data-ttu-id="ceee6-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="ceee6-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ceee6-191">d.</span><span class="sxs-lookup"><span data-stu-id="ceee6-191">d.</span></span> <span data-ttu-id="ceee6-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ceee6-192">Click **Create**.</span></span>
 
### <a name="create-a-bridgeline-unbound-test-user"></a><span data-ttu-id="ceee6-193">Create a Bridgeline Unbound test user</span><span class="sxs-lookup"><span data-stu-id="ceee6-193">Create a Bridgeline Unbound test user</span></span>

<span data-ttu-id="ceee6-194">The objective of this section is to create a user called Britta Simon in Bridgeline Unbound.</span><span class="sxs-lookup"><span data-stu-id="ceee6-194">The objective of this section is to create a user called Britta Simon in Bridgeline Unbound.</span></span> <span data-ttu-id="ceee6-195">Bridgeline Unbound supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="ceee6-195">Bridgeline Unbound supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="ceee6-196">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="ceee6-196">There is no action item for you in this section.</span></span> <span data-ttu-id="ceee6-197">A new user is created during an attempt to access Bridgeline Unbound if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="ceee6-197">A new user is created during an attempt to access Bridgeline Unbound if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="ceee6-198">If you need to create a user manually, contact [Bridgeline Unbound support team](mailto:support@iapps.com).</span><span class="sxs-lookup"><span data-stu-id="ceee6-198">If you need to create a user manually, contact [Bridgeline Unbound support team](mailto:support@iapps.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ceee6-199">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ceee6-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="ceee6-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bridgeline Unbound.</span><span class="sxs-lookup"><span data-stu-id="ceee6-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bridgeline Unbound.</span></span>

![Assign the user role][200] 

<span data-ttu-id="ceee6-202">**To assign Britta Simon to Bridgeline Unbound, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ceee6-202">**To assign Britta Simon to Bridgeline Unbound, perform the following steps:**</span></span>

1. <span data-ttu-id="ceee6-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ceee6-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="ceee6-205">In the applications list, select **Bridgeline Unbound**.</span><span class="sxs-lookup"><span data-stu-id="ceee6-205">In the applications list, select **Bridgeline Unbound**.</span></span>

    ![The Bridgeline Unbound link in the Applications list](./media/bridgelineunbound-tutorial/tutorial_bridgelineunbound_app.png)  

3. <span data-ttu-id="ceee6-207">In the menu on the left, click **Users and grobridgelineinbound**.</span><span class="sxs-lookup"><span data-stu-id="ceee6-207">In the menu on the left, click **Users and grobridgelineinbound**.</span></span>

    ![The "Users and grobridgelineinbound" link][202]

4. <span data-ttu-id="ceee6-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ceee6-209">Click **Add** button.</span></span> <span data-ttu-id="ceee6-210">Then select **Users and grobridgelineinbound** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ceee6-210">Then select **Users and grobridgelineinbound** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="ceee6-212">On **Users and grobridgelineinbound** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ceee6-212">On **Users and grobridgelineinbound** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ceee6-213">Click **Select** button on **Users and grobridgelineinbound** dialog.</span><span class="sxs-lookup"><span data-stu-id="ceee6-213">Click **Select** button on **Users and grobridgelineinbound** dialog.</span></span>

7. <span data-ttu-id="ceee6-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ceee6-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ceee6-215">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ceee6-215">Test single sign-on</span></span>

<span data-ttu-id="ceee6-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ceee6-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ceee6-217">When you click the Bridgeline Unbound tile in the Access Panel, you should get automatically signed-on to your Bridgeline Unbound application.</span><span class="sxs-lookup"><span data-stu-id="ceee6-217">When you click the Bridgeline Unbound tile in the Access Panel, you should get automatically signed-on to your Bridgeline Unbound application.</span></span>
<span data-ttu-id="ceee6-218">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ceee6-218">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ceee6-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ceee6-219">Additional resources</span></span>

* [<span data-ttu-id="ceee6-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ceee6-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ceee6-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ceee6-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bridgelineunbound-tutorial/tutorial_general_01.png
[2]: ./media/bridgelineunbound-tutorial/tutorial_general_02.png
[3]: ./media/bridgelineunbound-tutorial/tutorial_general_03.png
[4]: ./media/bridgelineunbound-tutorial/tutorial_general_04.png

[100]: ./media/bridgelineunbound-tutorial/tutorial_general_100.png

[200]: ./media/bridgelineunbound-tutorial/tutorial_general_200.png
[201]: ./media/bridgelineunbound-tutorial/tutorial_general_201.png
[202]: ./media/bridgelineunbound-tutorial/tutorial_general_202.png
[203]: ./media/bridgelineunbound-tutorial/tutorial_general_203.png

