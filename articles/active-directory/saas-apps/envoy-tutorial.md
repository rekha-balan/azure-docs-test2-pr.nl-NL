---
title: 'Tutorial: Azure Active Directory integration with Envoy | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Envoy.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 06cccaeaea3ff43bd5a4100ef0d4628e8cc77254
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869602"
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="994db-103">Tutorial: Azure Active Directory integration with Envoy</span><span class="sxs-lookup"><span data-stu-id="994db-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="994db-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="994db-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="994db-105">Integrating Envoy with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="994db-105">Integrating Envoy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="994db-106">You can control in Azure AD who has access to Envoy.</span><span class="sxs-lookup"><span data-stu-id="994db-106">You can control in Azure AD who has access to Envoy.</span></span>
- <span data-ttu-id="994db-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="994db-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="994db-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="994db-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="994db-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="994db-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="994db-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="994db-110">Prerequisites</span></span>

<span data-ttu-id="994db-111">To configure Azure AD integration with Envoy, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="994db-111">To configure Azure AD integration with Envoy, you need the following items:</span></span>

- <span data-ttu-id="994db-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="994db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="994db-113">An Envoy single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="994db-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="994db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="994db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="994db-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="994db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="994db-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="994db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="994db-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="994db-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="994db-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="994db-118">Scenario description</span></span>
<span data-ttu-id="994db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="994db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="994db-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="994db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="994db-121">Adding Envoy from the gallery</span><span class="sxs-lookup"><span data-stu-id="994db-121">Adding Envoy from the gallery</span></span>
1. <span data-ttu-id="994db-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="994db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-the-gallery"></a><span data-ttu-id="994db-123">Adding Envoy from the gallery</span><span class="sxs-lookup"><span data-stu-id="994db-123">Adding Envoy from the gallery</span></span>
<span data-ttu-id="994db-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="994db-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="994db-125">**To add Envoy from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="994db-125">**To add Envoy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="994db-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="994db-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="994db-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="994db-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="994db-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="994db-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="994db-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="994db-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="994db-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="994db-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span></span>

    ![Envoy in the results list](./media/envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="994db-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="994db-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="994db-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="994db-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="994db-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="994db-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span></span> <span data-ttu-id="994db-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span><span class="sxs-lookup"><span data-stu-id="994db-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span></span>

<span data-ttu-id="994db-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="994db-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="994db-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="994db-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="994db-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="994db-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="994db-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="994db-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="994db-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="994db-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="994db-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="994db-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="994db-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="994db-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="994db-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="994db-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="994db-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span><span class="sxs-lookup"><span data-stu-id="994db-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="994db-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="994db-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="994db-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="994db-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="994db-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="994db-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/envoy-tutorial/tutorial_envoy_samlbase.png)

1. <span data-ttu-id="994db-153">On the **Envoy Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="994db-153">On the **Envoy Domain and URLs** section, perform the following steps:</span></span>

    ![Envoy Domain and URLs single sign-on information](./media/envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="994db-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.envoy.com/a/saml/auth/<company-ID-from-Envoy>`</span><span class="sxs-lookup"><span data-stu-id="994db-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.envoy.com/a/saml/auth/<company-ID-from-Envoy>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="994db-156">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="994db-156">This value is not real.</span></span> <span data-ttu-id="994db-157">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="994db-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="994db-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="994db-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span></span>

1. <span data-ttu-id="994db-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span><span class="sxs-lookup"><span data-stu-id="994db-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span></span>

    ![The Certificate download link](./media/envoy-tutorial/tutorial_envoy_certificate.png) 

1. <span data-ttu-id="994db-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="994db-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/envoy-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="994db-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="994db-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="994db-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="994db-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Envoy Configuration](./media/envoy-tutorial/tutorial_envoy_configure.png)

1. <span data-ttu-id="994db-166">In a different web browser window, log into your Envoy company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="994db-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

1. <span data-ttu-id="994db-167">In the toolbar on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="994db-167">In the toolbar on the top, click **Settings**.</span></span>

    <span data-ttu-id="994db-168">![Envoy](./media/envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="994db-168">![Envoy](./media/envoy-tutorial/ic776782.png "Envoy")</span></span>

1. <span data-ttu-id="994db-169">Click **Company**.</span><span class="sxs-lookup"><span data-stu-id="994db-169">Click **Company**.</span></span>

    <span data-ttu-id="994db-170">![Company](./media/envoy-tutorial/ic776783.png "Company")</span><span class="sxs-lookup"><span data-stu-id="994db-170">![Company](./media/envoy-tutorial/ic776783.png "Company")</span></span>

1. <span data-ttu-id="994db-171">Click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="994db-171">Click **SAML**.</span></span>

    <span data-ttu-id="994db-172">![SAML](./media/envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="994db-172">![SAML](./media/envoy-tutorial/ic776784.png "SAML")</span></span>

1. <span data-ttu-id="994db-173">In the **SAML Authentication** configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="994db-173">In the **SAML Authentication** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="994db-174">![SAML authentication](./media/envoy-tutorial/ic776785.png "SAML authentication")</span><span class="sxs-lookup"><span data-stu-id="994db-174">![SAML authentication](./media/envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="994db-175">The value for the HQ location ID is auto generated by the application.</span><span class="sxs-lookup"><span data-stu-id="994db-175">The value for the HQ location ID is auto generated by the application.</span></span>
    
    <span data-ttu-id="994db-176">a.</span><span class="sxs-lookup"><span data-stu-id="994db-176">a.</span></span> <span data-ttu-id="994db-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="994db-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="994db-178">b.</span><span class="sxs-lookup"><span data-stu-id="994db-178">b.</span></span> <span data-ttu-id="994db-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="994db-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="994db-180">c.</span><span class="sxs-lookup"><span data-stu-id="994db-180">c.</span></span> <span data-ttu-id="994db-181">Click **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="994db-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="994db-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="994db-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="994db-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="994db-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="994db-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="994db-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="994db-185">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="994db-185">Create an Azure AD test user</span></span>

<span data-ttu-id="994db-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="994db-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="994db-188">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="994db-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="994db-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="994db-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/envoy-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="994db-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="994db-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/envoy-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="994db-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="994db-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/envoy-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="994db-195">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="994db-195">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="994db-197">a.</span><span class="sxs-lookup"><span data-stu-id="994db-197">a.</span></span> <span data-ttu-id="994db-198">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="994db-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="994db-199">b.</span><span class="sxs-lookup"><span data-stu-id="994db-199">b.</span></span> <span data-ttu-id="994db-200">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="994db-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="994db-201">c.</span><span class="sxs-lookup"><span data-stu-id="994db-201">c.</span></span> <span data-ttu-id="994db-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="994db-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="994db-203">d.</span><span class="sxs-lookup"><span data-stu-id="994db-203">d.</span></span> <span data-ttu-id="994db-204">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="994db-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="994db-205">Create an Envoy test user</span><span class="sxs-lookup"><span data-stu-id="994db-205">Create an Envoy test user</span></span>

<span data-ttu-id="994db-206">There is no action item for you to configure user provisioning to Envoy.</span><span class="sxs-lookup"><span data-stu-id="994db-206">There is no action item for you to configure user provisioning to Envoy.</span></span> <span data-ttu-id="994db-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="994db-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span> <span data-ttu-id="994db-208">If there is no user account available yet, it is automatically created by Envoy.</span><span class="sxs-lookup"><span data-stu-id="994db-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="994db-209">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="994db-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="994db-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span><span class="sxs-lookup"><span data-stu-id="994db-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span></span>

![Assign the user role][200] 

<span data-ttu-id="994db-212">**To assign Britta Simon to Envoy, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="994db-212">**To assign Britta Simon to Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="994db-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="994db-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="994db-215">In the applications list, select **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="994db-215">In the applications list, select **Envoy**.</span></span>

    ![The Envoy link in the Applications list](./media/envoy-tutorial/tutorial_envoy_app.png)  

1. <span data-ttu-id="994db-217">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="994db-217">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="994db-219">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="994db-219">Click **Add** button.</span></span> <span data-ttu-id="994db-220">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="994db-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="994db-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="994db-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="994db-223">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="994db-223">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="994db-224">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="994db-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="994db-225">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="994db-225">Test single sign-on</span></span>

<span data-ttu-id="994db-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="994db-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="994db-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span><span class="sxs-lookup"><span data-stu-id="994db-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span></span>
<span data-ttu-id="994db-228">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="994db-228">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="994db-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="994db-229">Additional resources</span></span>

* [<span data-ttu-id="994db-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="994db-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="994db-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="994db-231">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/envoy-tutorial/tutorial_general_01.png
[2]: ./media/envoy-tutorial/tutorial_general_02.png
[3]: ./media/envoy-tutorial/tutorial_general_03.png
[4]: ./media/envoy-tutorial/tutorial_general_04.png

[100]: ./media/envoy-tutorial/tutorial_general_100.png

[200]: ./media/envoy-tutorial/tutorial_general_200.png
[201]: ./media/envoy-tutorial/tutorial_general_201.png
[202]: ./media/envoy-tutorial/tutorial_general_202.png
[203]: ./media/envoy-tutorial/tutorial_general_203.png

