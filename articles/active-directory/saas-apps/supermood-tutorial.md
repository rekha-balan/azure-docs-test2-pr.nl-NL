---
title: 'Tutorial: Azure Active Directory integration with Supermood | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Supermood.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: afc04efa-2eba-4e47-8ce4-b71eb293cd09
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2018
ms.author: jeedes
ms.openlocfilehash: 98a39c52f206f19d3330695fd05f9a96c0bf4d36
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869357"
---
# <a name="tutorial-azure-active-directory-integration-with-supermood"></a><span data-ttu-id="7cc0f-103">Tutorial: Azure Active Directory integration with Supermood</span><span class="sxs-lookup"><span data-stu-id="7cc0f-103">Tutorial: Azure Active Directory integration with Supermood</span></span>

<span data-ttu-id="7cc0f-104">In this tutorial, you learn how to integrate Supermood with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7cc0f-104">In this tutorial, you learn how to integrate Supermood with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7cc0f-105">Integrating Supermood with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7cc0f-105">Integrating Supermood with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7cc0f-106">You can control in Azure AD who has access to Supermood.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-106">You can control in Azure AD who has access to Supermood.</span></span>
- <span data-ttu-id="7cc0f-107">You can enable your users to automatically get signed-on to Supermood (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-107">You can enable your users to automatically get signed-on to Supermood (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7cc0f-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7cc0f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7cc0f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cc0f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7cc0f-110">Prerequisites</span></span>

<span data-ttu-id="7cc0f-111">To configure Azure AD integration with Supermood, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7cc0f-111">To configure Azure AD integration with Supermood, you need the following items:</span></span>

- <span data-ttu-id="7cc0f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7cc0f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7cc0f-113">A Supermood single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7cc0f-113">A Supermood single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7cc0f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7cc0f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7cc0f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7cc0f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7cc0f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7cc0f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7cc0f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7cc0f-118">Scenario description</span></span>
<span data-ttu-id="7cc0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7cc0f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7cc0f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7cc0f-121">Adding Supermood from the gallery</span><span class="sxs-lookup"><span data-stu-id="7cc0f-121">Adding Supermood from the gallery</span></span>
1. <span data-ttu-id="7cc0f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7cc0f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-supermood-from-the-gallery"></a><span data-ttu-id="7cc0f-123">Adding Supermood from the gallery</span><span class="sxs-lookup"><span data-stu-id="7cc0f-123">Adding Supermood from the gallery</span></span>
<span data-ttu-id="7cc0f-124">To configure the integration of Supermood into Azure AD, you need to add Supermood from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-124">To configure the integration of Supermood into Azure AD, you need to add Supermood from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7cc0f-125">**To add Supermood from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7cc0f-125">**To add Supermood from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7cc0f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="7cc0f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7cc0f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="7cc0f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="7cc0f-133">In the search box, type **Supermood**, select **Supermood** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-133">In the search box, type **Supermood**, select **Supermood** from result panel then click **Add** button to add the application.</span></span>

    ![Supermood in the results list](./media/supermood-tutorial/tutorial_supermood_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7cc0f-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7cc0f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7cc0f-136">In this section, you configure and test Azure AD single sign-on with Supermood based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7cc0f-136">In this section, you configure and test Azure AD single sign-on with Supermood based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7cc0f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Supermood is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Supermood is to a user in Azure AD.</span></span> <span data-ttu-id="7cc0f-138">In other words, a link relationship between an Azure AD user and the related user in Supermood needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-138">In other words, a link relationship between an Azure AD user and the related user in Supermood needs to be established.</span></span>

<span data-ttu-id="7cc0f-139">To configure and test Azure AD single sign-on with Supermood, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7cc0f-139">To configure and test Azure AD single sign-on with Supermood, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7cc0f-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7cc0f-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7cc0f-142">**[Create a Supermood test user](#create-a-supermood-test-user)** - to have a counterpart of Britta Simon in Supermood that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-142">**[Create a Supermood test user](#create-a-supermood-test-user)** - to have a counterpart of Britta Simon in Supermood that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7cc0f-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7cc0f-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7cc0f-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7cc0f-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7cc0f-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Supermood application.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Supermood application.</span></span>

<span data-ttu-id="7cc0f-147">**To configure Azure AD single sign-on with Supermood, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7cc0f-147">**To configure Azure AD single sign-on with Supermood, perform the following steps:**</span></span>

1. <span data-ttu-id="7cc0f-148">In the Azure portal, on the **Supermood** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-148">In the Azure portal, on the **Supermood** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="7cc0f-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/supermood-tutorial/tutorial_supermood_samlbase.png)

1. <span data-ttu-id="7cc0f-152">On the **Supermood Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7cc0f-152">On the **Supermood Domain and URLs** section, perform the following steps:</span></span>

    ![Supermood Domain and URLs single sign-on information](./media/supermood-tutorial/tutorial_supermood_url.png)

    <span data-ttu-id="7cc0f-154">a.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-154">a.</span></span> <span data-ttu-id="7cc0f-155">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-155">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="7cc0f-156">b.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-156">b.</span></span> <span data-ttu-id="7cc0f-157">If you wish to configure the application in **IDP** initiated mode, in the **Relay State** textbox, type a URL: `https://supermood.co/auth/sso/saml20`</span><span class="sxs-lookup"><span data-stu-id="7cc0f-157">If you wish to configure the application in **IDP** initiated mode, in the **Relay State** textbox, type a URL: `https://supermood.co/auth/sso/saml20`</span></span>

    <span data-ttu-id="7cc0f-158">c.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-158">c.</span></span> <span data-ttu-id="7cc0f-159">If you wish to configure the application in **SP** initiated mode, in the **Sign-on URL** textbox, type a URL: `https://supermood.co/app/#!/loginv2`</span><span class="sxs-lookup"><span data-stu-id="7cc0f-159">If you wish to configure the application in **SP** initiated mode, in the **Sign-on URL** textbox, type a URL: `https://supermood.co/app/#!/loginv2`</span></span>

1. <span data-ttu-id="7cc0f-160">Supermood application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-160">Supermood application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="7cc0f-161">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-161">Configure the following claims for this application.</span></span> <span data-ttu-id="7cc0f-162">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-162">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="7cc0f-163">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-163">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/supermood-tutorial/tutorial_supermood_attribute.png)

1. <span data-ttu-id="7cc0f-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7cc0f-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="7cc0f-166">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="7cc0f-166">Attribute Name</span></span> | <span data-ttu-id="7cc0f-167">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="7cc0f-167">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="7cc0f-168">firstName</span><span class="sxs-lookup"><span data-stu-id="7cc0f-168">firstName</span></span> | <span data-ttu-id="7cc0f-169">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7cc0f-169">user.givenname</span></span> |
    | <span data-ttu-id="7cc0f-170">lastName</span><span class="sxs-lookup"><span data-stu-id="7cc0f-170">lastName</span></span> | <span data-ttu-id="7cc0f-171">user.surname</span><span class="sxs-lookup"><span data-stu-id="7cc0f-171">user.surname</span></span> |

    <span data-ttu-id="7cc0f-172">a.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-172">a.</span></span> <span data-ttu-id="7cc0f-173">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/supermood-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/supermood-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="7cc0f-176">b.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-176">b.</span></span> <span data-ttu-id="7cc0f-177">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7cc0f-178">c.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-178">c.</span></span> <span data-ttu-id="7cc0f-179">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-179">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="7cc0f-180">d.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-180">d.</span></span> <span data-ttu-id="7cc0f-181">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-181">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="7cc0f-182">d.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-182">d.</span></span> <span data-ttu-id="7cc0f-183">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="7cc0f-183">Click **Ok**</span></span>

1. <span data-ttu-id="7cc0f-184">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-184">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/supermood-tutorial/tutorial_supermood_certificate.png) 

1. <span data-ttu-id="7cc0f-186">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-186">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/supermood-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="7cc0f-188">Go to your Supermood.co admin panel as Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-188">Go to your Supermood.co admin panel as Security Administrator.</span></span>

1. <span data-ttu-id="7cc0f-189">Click on **My account** (bottom left) and **Single Sign On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-189">Click on **My account** (bottom left) and **Single Sign On (SSO)**.</span></span>

    ![The Certificate single](./media/supermood-tutorial/tutorial_supermood_single.png)
1. <span data-ttu-id="7cc0f-191">On **Your SAML 2.0 configurations**, Click **Add an SAML 2.0 configuration for an email domain**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-191">On **Your SAML 2.0 configurations**, Click **Add an SAML 2.0 configuration for an email domain**.</span></span>

    ![The Certificate add](./media/supermood-tutorial/tutorial_supermood_add.png)

1. <span data-ttu-id="7cc0f-193">On **Add an SAML 2.0 configuration for an email domain**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-193">On **Add an SAML 2.0 configuration for an email domain**.</span></span> <span data-ttu-id="7cc0f-194">section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7cc0f-194">section, perform the following steps:</span></span>

    ![The Certificate saml](./media/supermood-tutorial/tutorial_supermood_saml.png)

    <span data-ttu-id="7cc0f-196">a.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-196">a.</span></span> <span data-ttu-id="7cc0f-197">In the **email domain for this Identity provider** textbox, type your domain.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-197">In the **email domain for this Identity provider** textbox, type your domain.</span></span>

    <span data-ttu-id="7cc0f-198">b.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-198">b.</span></span> <span data-ttu-id="7cc0f-199">In the **Use a metadata URL** textbox, paste the **App Federation Metadata Url** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-199">In the **Use a metadata URL** textbox, paste the **App Federation Metadata Url** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7cc0f-200">c.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-200">c.</span></span> <span data-ttu-id="7cc0f-201">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-201">Click **Add**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7cc0f-202">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7cc0f-202">Create an Azure AD test user</span></span>

<span data-ttu-id="7cc0f-203">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-203">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="7cc0f-205">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7cc0f-205">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7cc0f-206">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-206">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/supermood-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="7cc0f-208">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-208">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/supermood-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="7cc0f-210">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-210">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/supermood-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="7cc0f-212">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7cc0f-212">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/supermood-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7cc0f-214">a.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-214">a.</span></span> <span data-ttu-id="7cc0f-215">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-215">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7cc0f-216">b.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-216">b.</span></span> <span data-ttu-id="7cc0f-217">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-217">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7cc0f-218">c.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-218">c.</span></span> <span data-ttu-id="7cc0f-219">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-219">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7cc0f-220">d.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-220">d.</span></span> <span data-ttu-id="7cc0f-221">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-221">Click **Create**.</span></span>
 
### <a name="create-a-supermood-test-user"></a><span data-ttu-id="7cc0f-222">Create a Supermood test user</span><span class="sxs-lookup"><span data-stu-id="7cc0f-222">Create a Supermood test user</span></span>

<span data-ttu-id="7cc0f-223">In this section, you create a user called Britta Simon in Supermood.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-223">In this section, you create a user called Britta Simon in Supermood.</span></span> <span data-ttu-id="7cc0f-224">Supermood supports just-in-time provisioning, which is by default enabled for users whose emails belong to the domains which are added during the configuration at Supermood end.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-224">Supermood supports just-in-time provisioning, which is by default enabled for users whose emails belong to the domains which are added during the configuration at Supermood end.</span></span> <span data-ttu-id="7cc0f-225">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-225">There is no action item for you in this section.</span></span> <span data-ttu-id="7cc0f-226">A new user is created during an attempt to access Supermood if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-226">A new user is created during an attempt to access Supermood if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="7cc0f-227">If you need to create a user manually, contact [Supermood support team](mailto:hello@supermood.fr).</span><span class="sxs-lookup"><span data-stu-id="7cc0f-227">If you need to create a user manually, contact [Supermood support team](mailto:hello@supermood.fr).</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7cc0f-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7cc0f-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="7cc0f-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Supermood.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Supermood.</span></span>

![Assign the user role][200] 

<span data-ttu-id="7cc0f-231">**To assign Britta Simon to Supermood, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7cc0f-231">**To assign Britta Simon to Supermood, perform the following steps:**</span></span>

1. <span data-ttu-id="7cc0f-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7cc0f-234">In the applications list, select **Supermood**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-234">In the applications list, select **Supermood**.</span></span>

    ![The Supermood link in the Applications list](./media/supermood-tutorial/tutorial_supermood_app.png)  

1. <span data-ttu-id="7cc0f-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-236">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="7cc0f-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-238">Click **Add** button.</span></span> <span data-ttu-id="7cc0f-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="7cc0f-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7cc0f-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-242">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7cc0f-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7cc0f-244">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7cc0f-244">Test single sign-on</span></span>

<span data-ttu-id="7cc0f-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7cc0f-246">When you click the Supermood tile in the Access Panel, you should get automatically signed-on to your Supermood application.</span><span class="sxs-lookup"><span data-stu-id="7cc0f-246">When you click the Supermood tile in the Access Panel, you should get automatically signed-on to your Supermood application.</span></span>
<span data-ttu-id="7cc0f-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7cc0f-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7cc0f-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7cc0f-248">Additional resources</span></span>

* [<span data-ttu-id="7cc0f-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7cc0f-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7cc0f-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7cc0f-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/supermood-tutorial/tutorial_general_01.png
[2]: ./media/supermood-tutorial/tutorial_general_02.png
[3]: ./media/supermood-tutorial/tutorial_general_03.png
[4]: ./media/supermood-tutorial/tutorial_general_04.png

[100]: ./media/supermood-tutorial/tutorial_general_100.png

[200]: ./media/supermood-tutorial/tutorial_general_200.png
[201]: ./media/supermood-tutorial/tutorial_general_201.png
[202]: ./media/supermood-tutorial/tutorial_general_202.png
[203]: ./media/supermood-tutorial/tutorial_general_203.png

