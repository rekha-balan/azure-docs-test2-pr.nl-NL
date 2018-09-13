---
title: 'Tutorial: Azure Active Directory integration with Yonyx Interactive Guides | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Yonyx Interactive Guides.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: a7166ac295c8bac3c7bb8d2e053a6f49fe533cc8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967835"
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="08127-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="08127-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="08127-104">In this tutorial, you learn how to integrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="08127-104">In this tutorial, you learn how to integrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08127-105">Integrating Yonyx Interactive Guides with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="08127-105">Integrating Yonyx Interactive Guides with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="08127-106">You can control in Azure AD who has access to Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="08127-106">You can control in Azure AD who has access to Yonyx Interactive Guides</span></span>
- <span data-ttu-id="08127-107">You can enable your users to automatically get signed-on to Yonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="08127-107">You can enable your users to automatically get signed-on to Yonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="08127-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="08127-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="08127-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="08127-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08127-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="08127-110">Prerequisites</span></span>

<span data-ttu-id="08127-111">To configure Azure AD integration with Yonyx Interactive Guides, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="08127-111">To configure Azure AD integration with Yonyx Interactive Guides, you need the following items:</span></span>

- <span data-ttu-id="08127-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="08127-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08127-113">A Yonyx Interactive Guides single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="08127-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08127-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="08127-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08127-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="08127-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08127-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="08127-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08127-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08127-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08127-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="08127-118">Scenario description</span></span>
<span data-ttu-id="08127-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="08127-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08127-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="08127-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08127-121">Adding Yonyx Interactive Guides from the gallery</span><span class="sxs-lookup"><span data-stu-id="08127-121">Adding Yonyx Interactive Guides from the gallery</span></span>
1. <span data-ttu-id="08127-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="08127-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-the-gallery"></a><span data-ttu-id="08127-123">Adding Yonyx Interactive Guides from the gallery</span><span class="sxs-lookup"><span data-stu-id="08127-123">Adding Yonyx Interactive Guides from the gallery</span></span>
<span data-ttu-id="08127-124">To configure the integration of Yonyx Interactive Guides into Azure AD, you need to add Yonyx Interactive Guides from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="08127-124">To configure the integration of Yonyx Interactive Guides into Azure AD, you need to add Yonyx Interactive Guides from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="08127-125">**To add Yonyx Interactive Guides from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="08127-125">**To add Yonyx Interactive Guides from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="08127-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="08127-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="08127-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="08127-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="08127-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="08127-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="08127-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="08127-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="08127-133">In the search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="08127-133">In the search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button to add the application.</span></span>

    ![Yonyx Interactive Guides in the results list](./media/yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="08127-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="08127-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="08127-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="08127-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="08127-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Yonyx Interactive Guides is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08127-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Yonyx Interactive Guides is to a user in Azure AD.</span></span> <span data-ttu-id="08127-138">In other words, a link relationship between an Azure AD user and the related user in Yonyx Interactive Guides needs to be established.</span><span class="sxs-lookup"><span data-stu-id="08127-138">In other words, a link relationship between an Azure AD user and the related user in Yonyx Interactive Guides needs to be established.</span></span>

<span data-ttu-id="08127-139">In Yonyx Interactive Guides, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="08127-139">In Yonyx Interactive Guides, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="08127-140">To configure and test Azure AD single sign-on with Yonyx Interactive Guides, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="08127-140">To configure and test Azure AD single sign-on with Yonyx Interactive Guides, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="08127-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="08127-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="08127-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08127-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="08127-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - to have a counterpart of Britta Simon in Yonyx Interactive Guides that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="08127-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - to have a counterpart of Britta Simon in Yonyx Interactive Guides that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="08127-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="08127-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="08127-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="08127-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="08127-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="08127-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="08127-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span><span class="sxs-lookup"><span data-stu-id="08127-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="08127-148">**To configure Azure AD single sign-on with Yonyx Interactive Guides, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="08127-148">**To configure Azure AD single sign-on with Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="08127-149">In the Azure portal, on the **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="08127-149">In the Azure portal, on the **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="08127-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="08127-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

1. <span data-ttu-id="08127-153">On the **Yonyx Interactive Guides Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="08127-153">On the **Yonyx Interactive Guides Domain and URLs** section, perform the following steps:</span></span>

    ![Yonyx Interactive Guides Domain and URLs single sign-on information](./media/yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="08127-155">a.</span><span class="sxs-lookup"><span data-stu-id="08127-155">a.</span></span> <span data-ttu-id="08127-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span><span class="sxs-lookup"><span data-stu-id="08127-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="08127-157">b.</span><span class="sxs-lookup"><span data-stu-id="08127-157">b.</span></span> <span data-ttu-id="08127-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="08127-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="08127-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="08127-159">These values are not real.</span></span> <span data-ttu-id="08127-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="08127-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="08127-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="08127-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) to get these values.</span></span> 
 
1. <span data-ttu-id="08127-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="08127-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

1. <span data-ttu-id="08127-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="08127-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/yonyx-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="08127-166">On the **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="08127-166">On the **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** to open **Configure sign-on** window.</span></span> <span data-ttu-id="08127-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="08127-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Yonyx Interactive Guides Configuration](./media/yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

1. <span data-ttu-id="08127-169">To configure single sign-on on **Yonyx Interactive Guides** side, you need to send the downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** to [Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="08127-169">To configure single sign-on on **Yonyx Interactive Guides** side, you need to send the downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** to [Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="08127-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="08127-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="08127-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="08127-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="08127-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="08127-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="08127-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08127-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="08127-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="08127-174">Create an Azure AD test user</span></span>

<span data-ttu-id="08127-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08127-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

  ![Create an Azure AD test user][100]

<span data-ttu-id="08127-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="08127-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="08127-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="08127-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button](./media/yonyx-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="08127-180">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="08127-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/yonyx-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="08127-182">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="08127-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![The Add button](./media/yonyx-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="08127-184">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="08127-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![The User dialog box](./media/yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="08127-186">a.</span><span class="sxs-lookup"><span data-stu-id="08127-186">a.</span></span> <span data-ttu-id="08127-187">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="08127-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08127-188">b.</span><span class="sxs-lookup"><span data-stu-id="08127-188">b.</span></span> <span data-ttu-id="08127-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="08127-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="08127-190">c.</span><span class="sxs-lookup"><span data-stu-id="08127-190">c.</span></span> <span data-ttu-id="08127-191">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="08127-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="08127-192">d.</span><span class="sxs-lookup"><span data-stu-id="08127-192">d.</span></span> <span data-ttu-id="08127-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="08127-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="08127-194">Create a Yonyx Interactive Guides test user</span><span class="sxs-lookup"><span data-stu-id="08127-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="08127-195">The objective of this section is to create a user called Britta Simon in Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="08127-195">The objective of this section is to create a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="08127-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="08127-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="08127-197">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="08127-197">There is no action item for you in this section.</span></span> <span data-ttu-id="08127-198">A new user is created during an attempt to access Yonyx Interactive Guides if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="08127-198">A new user is created during an attempt to access Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="08127-199">If you need to create a user manually, you need to contact the Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span><span class="sxs-lookup"><span data-stu-id="08127-199">If you need to create a user manually, you need to contact the Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="08127-200">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="08127-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="08127-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="08127-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yonyx Interactive Guides.</span></span>

![Assign the user role][200]

<span data-ttu-id="08127-203">**To assign Britta Simon to Yonyx Interactive Guides, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="08127-203">**To assign Britta Simon to Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="08127-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="08127-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="08127-206">In the applications list, select **Yonyx Interactive Guides**.</span><span class="sxs-lookup"><span data-stu-id="08127-206">In the applications list, select **Yonyx Interactive Guides**.</span></span>

    ![The Yonyx Interactive Guides link in the Applications list](./media/yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

1. <span data-ttu-id="08127-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="08127-208">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="08127-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="08127-210">Click **Add** button.</span></span> <span data-ttu-id="08127-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="08127-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="08127-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="08127-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="08127-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="08127-214">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="08127-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="08127-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="08127-216">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="08127-216">Test single sign-on</span></span>

<span data-ttu-id="08127-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="08127-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="08127-218">When you click the Yonyx Interactive Guides tile in the Access Panel, you should get automatically signed-on to your Yonyx Interactive Guides application.</span><span class="sxs-lookup"><span data-stu-id="08127-218">When you click the Yonyx Interactive Guides tile in the Access Panel, you should get automatically signed-on to your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="08127-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="08127-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08127-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="08127-220">Additional resources</span></span>

* [<span data-ttu-id="08127-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08127-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="08127-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="08127-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/yonyx-tutorial/tutorial_general_01.png
[2]: ./media/yonyx-tutorial/tutorial_general_02.png
[3]: ./media/yonyx-tutorial/tutorial_general_03.png
[4]: ./media/yonyx-tutorial/tutorial_general_04.png

[100]: ./media/yonyx-tutorial/tutorial_general_100.png

[200]: ./media/yonyx-tutorial/tutorial_general_200.png
[201]: ./media/yonyx-tutorial/tutorial_general_201.png
[202]: ./media/yonyx-tutorial/tutorial_general_202.png
[203]: ./media/yonyx-tutorial/tutorial_general_203.png

