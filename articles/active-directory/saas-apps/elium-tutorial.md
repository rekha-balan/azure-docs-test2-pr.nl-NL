---
title: 'Tutorial: Azure Active Directory integration with Elium | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Elium.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: fae344b3-5bd9-40e2-9a1d-448dcd58155f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/05/2018
ms.author: jeedes
ms.openlocfilehash: dfa90474632b2cf18055e0ba95994f120cb293ef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865807"
---
# <a name="tutorial-azure-active-directory-integration-with-elium"></a><span data-ttu-id="23376-103">Tutorial: Azure Active Directory integration with Elium</span><span class="sxs-lookup"><span data-stu-id="23376-103">Tutorial: Azure Active Directory integration with Elium</span></span>

<span data-ttu-id="23376-104">In this tutorial, you learn how to integrate Elium with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="23376-104">In this tutorial, you learn how to integrate Elium with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23376-105">Integrating Elium with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="23376-105">Integrating Elium with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="23376-106">You can control in Azure AD who has access to Elium.</span><span class="sxs-lookup"><span data-stu-id="23376-106">You can control in Azure AD who has access to Elium.</span></span>
- <span data-ttu-id="23376-107">You can enable your users to automatically get signed-on to Elium (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="23376-107">You can enable your users to automatically get signed-on to Elium (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="23376-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23376-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="23376-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="23376-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23376-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="23376-110">Prerequisites</span></span>

<span data-ttu-id="23376-111">To configure Azure AD integration with Elium, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="23376-111">To configure Azure AD integration with Elium, you need the following items:</span></span>

- <span data-ttu-id="23376-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="23376-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23376-113">An Elium single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="23376-113">An Elium single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23376-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="23376-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23376-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="23376-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23376-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="23376-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23376-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="23376-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23376-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="23376-118">Scenario description</span></span>
<span data-ttu-id="23376-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="23376-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23376-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="23376-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23376-121">Adding Elium from the gallery</span><span class="sxs-lookup"><span data-stu-id="23376-121">Adding Elium from the gallery</span></span>
1. <span data-ttu-id="23376-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="23376-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-elium-from-the-gallery"></a><span data-ttu-id="23376-123">Adding Elium from the gallery</span><span class="sxs-lookup"><span data-stu-id="23376-123">Adding Elium from the gallery</span></span>
<span data-ttu-id="23376-124">To configure the integration of Elium into Azure AD, you need to add Elium from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="23376-124">To configure the integration of Elium into Azure AD, you need to add Elium from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="23376-125">**To add Elium from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="23376-125">**To add Elium from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="23376-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="23376-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="23376-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="23376-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="23376-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="23376-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="23376-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="23376-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="23376-133">In the search box, type **Elium**, select **Elium** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="23376-133">In the search box, type **Elium**, select **Elium** from result panel then click **Add** button to add the application.</span></span>

    ![Elium in the results list](./media/elium-tutorial/tutorial_elium_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="23376-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="23376-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="23376-136">In this section, you configure and test Azure AD single sign-on with Elium based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="23376-136">In this section, you configure and test Azure AD single sign-on with Elium based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="23376-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Elium is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23376-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Elium is to a user in Azure AD.</span></span> <span data-ttu-id="23376-138">In other words, a link relationship between an Azure AD user and the related user in Elium needs to be established.</span><span class="sxs-lookup"><span data-stu-id="23376-138">In other words, a link relationship between an Azure AD user and the related user in Elium needs to be established.</span></span>

<span data-ttu-id="23376-139">To configure and test Azure AD single sign-on with Elium, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="23376-139">To configure and test Azure AD single sign-on with Elium, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="23376-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="23376-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="23376-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23376-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="23376-142">**[Create an Elium test user](#create-an-elium-test-user)** - to have a counterpart of Britta Simon in Elium that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="23376-142">**[Create an Elium test user](#create-an-elium-test-user)** - to have a counterpart of Britta Simon in Elium that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="23376-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="23376-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="23376-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="23376-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="23376-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="23376-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="23376-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Elium application.</span><span class="sxs-lookup"><span data-stu-id="23376-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Elium application.</span></span>

<span data-ttu-id="23376-147">**To configure Azure AD single sign-on with Elium, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="23376-147">**To configure Azure AD single sign-on with Elium, perform the following steps:**</span></span>

1. <span data-ttu-id="23376-148">In the Azure portal, on the **Elium** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="23376-148">In the Azure portal, on the **Elium** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="23376-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="23376-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/elium-tutorial/tutorial_elium_samlbase.png)

1. <span data-ttu-id="23376-152">On the **Elium Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="23376-152">On the **Elium Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Elium Domain and URLs single sign-on information](./media/elium-tutorial/tutorial_elium_url.png)

    <span data-ttu-id="23376-154">a.</span><span class="sxs-lookup"><span data-stu-id="23376-154">a.</span></span> <span data-ttu-id="23376-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<platform-domain>.elium.com/login/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="23376-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<platform-domain>.elium.com/login/saml2/metadata`</span></span>

    <span data-ttu-id="23376-156">b.</span><span class="sxs-lookup"><span data-stu-id="23376-156">b.</span></span> <span data-ttu-id="23376-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<platform-domain>.elium.com/login/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="23376-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<platform-domain>.elium.com/login/saml2/acs`</span></span>

1. <span data-ttu-id="23376-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="23376-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Elium Domain and URLs single sign-on information](./media/elium-tutorial/tutorial_elium_url1.png)

    <span data-ttu-id="23376-160">In the **Sign-on URL** textbox, type a URL using the following pattern: ` https://<platform-domain>.elium.com/login/saml2/login`</span><span class="sxs-lookup"><span data-stu-id="23376-160">In the **Sign-on URL** textbox, type a URL using the following pattern: ` https://<platform-domain>.elium.com/login/saml2/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="23376-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="23376-161">These values are not real.</span></span> <span data-ttu-id="23376-162">You will get these values from the **SP metadata file** downloadable at `https://<platform-domain>.elium.com/login/saml2/metadata`, which is explained later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="23376-162">You will get these values from the **SP metadata file** downloadable at `https://<platform-domain>.elium.com/login/saml2/metadata`, which is explained later in this tutorial.</span></span>

1. <span data-ttu-id="23376-163">The Elium application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="23376-163">The Elium application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="23376-164">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="23376-164">Configure the following claims for this application.</span></span> <span data-ttu-id="23376-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="23376-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span>

    ![Configure Single Sign-On](./media/elium-tutorial/tutorial_attribute.png)

1. <span data-ttu-id="23376-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="23376-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
           
    | <span data-ttu-id="23376-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="23376-168">Attribute Name</span></span> | <span data-ttu-id="23376-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="23376-169">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="23376-170">email</span><span class="sxs-lookup"><span data-stu-id="23376-170">email</span></span>   |<span data-ttu-id="23376-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="23376-171">user.mail</span></span> |
    | <span data-ttu-id="23376-172">first_name</span><span class="sxs-lookup"><span data-stu-id="23376-172">first_name</span></span>| <span data-ttu-id="23376-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="23376-173">user.givenname</span></span> |
    | <span data-ttu-id="23376-174">last_name</span><span class="sxs-lookup"><span data-stu-id="23376-174">last_name</span></span>| <span data-ttu-id="23376-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="23376-175">user.surname</span></span>|
    | <span data-ttu-id="23376-176">job_title</span><span class="sxs-lookup"><span data-stu-id="23376-176">job_title</span></span>| <span data-ttu-id="23376-177">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="23376-177">user.jobtitle</span></span>|
    | <span data-ttu-id="23376-178">company</span><span class="sxs-lookup"><span data-stu-id="23376-178">company</span></span>| <span data-ttu-id="23376-179">user.companyname</span><span class="sxs-lookup"><span data-stu-id="23376-179">user.companyname</span></span>|
    
    > [!NOTE]
    > <span data-ttu-id="23376-180">These are the default claims.</span><span class="sxs-lookup"><span data-stu-id="23376-180">These are the default claims.</span></span> <span data-ttu-id="23376-181">**Only email claim is required**.</span><span class="sxs-lookup"><span data-stu-id="23376-181">**Only email claim is required**.</span></span> <span data-ttu-id="23376-182">For JIT provisioning also only email claim is mandatory.</span><span class="sxs-lookup"><span data-stu-id="23376-182">For JIT provisioning also only email claim is mandatory.</span></span> <span data-ttu-id="23376-183">Other custom claims can vary from one customer platform to another customer platform.</span><span class="sxs-lookup"><span data-stu-id="23376-183">Other custom claims can vary from one customer platform to another customer platform.</span></span>

    <span data-ttu-id="23376-184">a.</span><span class="sxs-lookup"><span data-stu-id="23376-184">a.</span></span> <span data-ttu-id="23376-185">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="23376-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/elium-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="23376-187">b.</span><span class="sxs-lookup"><span data-stu-id="23376-187">b.</span></span> <span data-ttu-id="23376-188">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="23376-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configure Single Sign-On](./media/elium-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="23376-190">c.</span><span class="sxs-lookup"><span data-stu-id="23376-190">c.</span></span> <span data-ttu-id="23376-191">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="23376-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="23376-192">d.</span><span class="sxs-lookup"><span data-stu-id="23376-192">d.</span></span> <span data-ttu-id="23376-193">Leave namespace as blank.</span><span class="sxs-lookup"><span data-stu-id="23376-193">Leave namespace as blank.</span></span>
    
    <span data-ttu-id="23376-194">e.</span><span class="sxs-lookup"><span data-stu-id="23376-194">e.</span></span> <span data-ttu-id="23376-195">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="23376-195">Click **Ok**.</span></span> 

1. <span data-ttu-id="23376-196">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="23376-196">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/elium-tutorial/tutorial_elium_certificate.png) 

1. <span data-ttu-id="23376-198">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="23376-198">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/elium-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="23376-200">In a different web browser window, log in to your Elium company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="23376-200">In a different web browser window, log in to your Elium company site as an administrator.</span></span>

1. <span data-ttu-id="23376-201">Click on the **User profile** from right top corner and then select **Administration**.</span><span class="sxs-lookup"><span data-stu-id="23376-201">Click on the **User profile** from right top corner and then select **Administration**.</span></span>

    ![Configure Single Sign-On](./media/elium-tutorial/user1.png)

1. <span data-ttu-id="23376-203">Select **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="23376-203">Select **Security** tab.</span></span>

    ![Configure Single Sign-On](./media/elium-tutorial/user2.png)

1. <span data-ttu-id="23376-205">Scroll down to the **Single sign-on (SSO)** section and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="23376-205">Scroll down to the **Single sign-on (SSO)** section and perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/elium-tutorial/user3.png)

    <span data-ttu-id="23376-207">a.</span><span class="sxs-lookup"><span data-stu-id="23376-207">a.</span></span> <span data-ttu-id="23376-208">Copy the value of **Verify that SAML2 authentication works for your account** and paste it in the **Sign-on URL** textbox on the **Elium Domain and URLs** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23376-208">Copy the value of **Verify that SAML2 authentication works for your account** and paste it in the **Sign-on URL** textbox on the **Elium Domain and URLs** section in the Azure portal.</span></span>

    > [!NOTE]
    > <span data-ttu-id="23376-209">After configuring SSO, you can always access the default remote login page at the following URL: `https://<platform_domain>/login/regular/login`</span><span class="sxs-lookup"><span data-stu-id="23376-209">After configuring SSO, you can always access the default remote login page at the following URL: `https://<platform_domain>/login/regular/login`</span></span> 

    <span data-ttu-id="23376-210">b.</span><span class="sxs-lookup"><span data-stu-id="23376-210">b.</span></span> <span data-ttu-id="23376-211">Select **Enable SAML2 federation** checkbox.</span><span class="sxs-lookup"><span data-stu-id="23376-211">Select **Enable SAML2 federation** checkbox.</span></span>

    <span data-ttu-id="23376-212">c.</span><span class="sxs-lookup"><span data-stu-id="23376-212">c.</span></span> <span data-ttu-id="23376-213">Select **JIT Provisioning** checkbox.</span><span class="sxs-lookup"><span data-stu-id="23376-213">Select **JIT Provisioning** checkbox.</span></span>

    <span data-ttu-id="23376-214">d.</span><span class="sxs-lookup"><span data-stu-id="23376-214">d.</span></span> <span data-ttu-id="23376-215">Open the **SP Metadata** by clicking on the **Download** button.</span><span class="sxs-lookup"><span data-stu-id="23376-215">Open the **SP Metadata** by clicking on the **Download** button.</span></span>

    <span data-ttu-id="23376-216">e.</span><span class="sxs-lookup"><span data-stu-id="23376-216">e.</span></span> <span data-ttu-id="23376-217">Search for the **entityID** in the **SP Metadata** file, copy the **entityID** value and paste it in the **Identifier** textbox on the **Elium Domain and URLs** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23376-217">Search for the **entityID** in the **SP Metadata** file, copy the **entityID** value and paste it in the **Identifier** textbox on the **Elium Domain and URLs** section in the Azure portal.</span></span> 

    ![Configure Single Sign-On](./media/elium-tutorial/user4.png)

    <span data-ttu-id="23376-219">f.</span><span class="sxs-lookup"><span data-stu-id="23376-219">f.</span></span> <span data-ttu-id="23376-220">Search for the **AssertionConsumerService** in the **SP Metadata** file, copy the **Location** value and paste it in the **Reply URL** textbox on the **Elium Domain and URLs** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23376-220">Search for the **AssertionConsumerService** in the **SP Metadata** file, copy the **Location** value and paste it in the **Reply URL** textbox on the **Elium Domain and URLs** section in the Azure portal.</span></span>

    ![Configure Single Sign-On](./media/elium-tutorial/user5.png)

    <span data-ttu-id="23376-222">g.</span><span class="sxs-lookup"><span data-stu-id="23376-222">g.</span></span> <span data-ttu-id="23376-223">Open the downloaded metadata file from Azure portal into notepad, copy the content and paste it into the **IdP Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="23376-223">Open the downloaded metadata file from Azure portal into notepad, copy the content and paste it into the **IdP Metadata** textbox.</span></span>

    <span data-ttu-id="23376-224">h.</span><span class="sxs-lookup"><span data-stu-id="23376-224">h.</span></span> <span data-ttu-id="23376-225">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="23376-225">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="23376-226">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="23376-226">Create an Azure AD test user</span></span>

<span data-ttu-id="23376-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23376-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="23376-229">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="23376-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="23376-230">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="23376-230">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/elium-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="23376-232">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="23376-232">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/elium-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="23376-234">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="23376-234">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/elium-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="23376-236">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="23376-236">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/elium-tutorial/create_aaduser_04.png)

    <span data-ttu-id="23376-238">a.</span><span class="sxs-lookup"><span data-stu-id="23376-238">a.</span></span> <span data-ttu-id="23376-239">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="23376-239">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23376-240">b.</span><span class="sxs-lookup"><span data-stu-id="23376-240">b.</span></span> <span data-ttu-id="23376-241">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23376-241">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="23376-242">c.</span><span class="sxs-lookup"><span data-stu-id="23376-242">c.</span></span> <span data-ttu-id="23376-243">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="23376-243">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="23376-244">d.</span><span class="sxs-lookup"><span data-stu-id="23376-244">d.</span></span> <span data-ttu-id="23376-245">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="23376-245">Click **Create**.</span></span>
 
### <a name="create-an-elium-test-user"></a><span data-ttu-id="23376-246">Create an Elium test user</span><span class="sxs-lookup"><span data-stu-id="23376-246">Create an Elium test user</span></span>

<span data-ttu-id="23376-247">The objective of this section is to create a user called Britta Simon in Elium.</span><span class="sxs-lookup"><span data-stu-id="23376-247">The objective of this section is to create a user called Britta Simon in Elium.</span></span> <span data-ttu-id="23376-248">Elium supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="23376-248">Elium supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="23376-249">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="23376-249">There is no action item for you in this section.</span></span> <span data-ttu-id="23376-250">A new user is created during an attempt to access Elium if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="23376-250">A new user is created during an attempt to access Elium if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="23376-251">If you need to create a user manually, contact [Elium support team](mailto:support@elium.com).</span><span class="sxs-lookup"><span data-stu-id="23376-251">If you need to create a user manually, contact [Elium support team](mailto:support@elium.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="23376-252">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="23376-252">Assign the Azure AD test user</span></span>

<span data-ttu-id="23376-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Elium.</span><span class="sxs-lookup"><span data-stu-id="23376-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Elium.</span></span>

![Assign the user role][200] 

<span data-ttu-id="23376-255">**To assign Britta Simon to Elium, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="23376-255">**To assign Britta Simon to Elium, perform the following steps:**</span></span>

1. <span data-ttu-id="23376-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="23376-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="23376-258">In the applications list, select **Elium**.</span><span class="sxs-lookup"><span data-stu-id="23376-258">In the applications list, select **Elium**.</span></span>

    ![The Elium link in the Applications list](./media/elium-tutorial/tutorial_elium_app.png)  

1. <span data-ttu-id="23376-260">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="23376-260">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="23376-262">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="23376-262">Click **Add** button.</span></span> <span data-ttu-id="23376-263">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="23376-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="23376-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="23376-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="23376-266">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="23376-266">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="23376-267">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="23376-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="23376-268">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="23376-268">Test single sign-on</span></span>

<span data-ttu-id="23376-269">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="23376-269">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="23376-270">When you click the Elium tile in the Access Panel, you should get automatically signed-on to your Elium application.</span><span class="sxs-lookup"><span data-stu-id="23376-270">When you click the Elium tile in the Access Panel, you should get automatically signed-on to your Elium application.</span></span>
<span data-ttu-id="23376-271">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="23376-271">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="23376-272">Additional resources</span><span class="sxs-lookup"><span data-stu-id="23376-272">Additional resources</span></span>

* [<span data-ttu-id="23376-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23376-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="23376-274">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="23376-274">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/elium-tutorial/tutorial_general_01.png
[2]: ./media/elium-tutorial/tutorial_general_02.png
[3]: ./media/elium-tutorial/tutorial_general_03.png
[4]: ./media/elium-tutorial/tutorial_general_04.png

[100]: ./media/elium-tutorial/tutorial_general_100.png

[200]: ./media/elium-tutorial/tutorial_general_200.png
[201]: ./media/elium-tutorial/tutorial_general_201.png
[202]: ./media/elium-tutorial/tutorial_general_202.png
[203]: ./media/elium-tutorial/tutorial_general_203.png

