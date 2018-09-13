---
title: 'Tutorial: Azure Active Directory integration with Salesforce | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2018
ms.author: jeedes
ms.openlocfilehash: 2f87c4a15ac21241b3304d1fdf0a5bd0ae715615
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866225"
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="39c64-103">Tutorial: Azure Active Directory integration with Salesforce</span><span class="sxs-lookup"><span data-stu-id="39c64-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="39c64-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39c64-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39c64-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="39c64-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="39c64-106">You can control in Azure AD who has access to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="39c64-106">You can control in Azure AD who has access to Salesforce.</span></span>
- <span data-ttu-id="39c64-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="39c64-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="39c64-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="39c64-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="39c64-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="39c64-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39c64-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="39c64-110">Prerequisites</span></span>

<span data-ttu-id="39c64-111">To configure Azure AD integration with Salesforce, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="39c64-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="39c64-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="39c64-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39c64-113">A Salesforce single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="39c64-113">A Salesforce single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39c64-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="39c64-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39c64-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="39c64-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39c64-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="39c64-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39c64-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39c64-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39c64-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="39c64-118">Scenario description</span></span>
<span data-ttu-id="39c64-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="39c64-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39c64-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="39c64-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39c64-121">Adding Salesforce from the gallery</span><span class="sxs-lookup"><span data-stu-id="39c64-121">Adding Salesforce from the gallery</span></span>
1. <span data-ttu-id="39c64-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="39c64-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="39c64-123">Adding Salesforce from the gallery</span><span class="sxs-lookup"><span data-stu-id="39c64-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="39c64-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="39c64-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="39c64-125">**To add Salesforce from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39c64-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="39c64-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="39c64-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="39c64-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="39c64-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="39c64-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="39c64-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

1. <span data-ttu-id="39c64-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="39c64-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="39c64-133">In the search box, type **Salesforce**, select **Salesforce** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="39c64-133">In the search box, type **Salesforce**, select **Salesforce** from result panel then click **Add** button to add the application.</span></span>

    ![Salesforce in the results list](./media/salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="39c64-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="39c64-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="39c64-136">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="39c64-136">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="39c64-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39c64-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="39c64-138">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span><span class="sxs-lookup"><span data-stu-id="39c64-138">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="39c64-139">In Salesforce, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="39c64-139">In Salesforce, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="39c64-140">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="39c64-140">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="39c64-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="39c64-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="39c64-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39c64-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="39c64-143">**[Create a Salesforce test user](#create-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="39c64-143">**[Create a Salesforce test user](#create-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="39c64-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="39c64-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="39c64-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="39c64-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="39c64-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="39c64-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="39c64-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span><span class="sxs-lookup"><span data-stu-id="39c64-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="39c64-148">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39c64-148">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="39c64-149">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="39c64-149">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="39c64-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="39c64-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/salesforce-tutorial/tutorial_salesforce_samlbase.png)

1. <span data-ttu-id="39c64-153">On the **Salesforce Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="39c64-153">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![Salesforce Domain and URLs single sign-on information](./media/salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="39c64-155">a.</span><span class="sxs-lookup"><span data-stu-id="39c64-155">a.</span></span> <span data-ttu-id="39c64-156">In the **Sign-on URL** textbox, type the value using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="39c64-156">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span>

    <span data-ttu-id="39c64-157">Enterprise account: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="39c64-157">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>

    <span data-ttu-id="39c64-158">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="39c64-158">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    <span data-ttu-id="39c64-159">b.</span><span class="sxs-lookup"><span data-stu-id="39c64-159">b.</span></span> <span data-ttu-id="39c64-160">In the **Identifier** textbox, type the value using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="39c64-160">In the **Identifier** textbox, type the value using the following pattern:</span></span>

    <span data-ttu-id="39c64-161">Enterprise account: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="39c64-161">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>

    <span data-ttu-id="39c64-162">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="39c64-162">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="39c64-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="39c64-163">These values are not real.</span></span> <span data-ttu-id="39c64-164">Update these values with the actual Sign-on URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="39c64-164">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="39c64-165">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="39c64-165">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span>

1. <span data-ttu-id="39c64-166">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="39c64-166">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/salesforce-tutorial/tutorial_salesforce_certificate.png) 

1. <span data-ttu-id="39c64-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="39c64-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/salesforce-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="39c64-170">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="39c64-170">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="39c64-171">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="39c64-171">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Salesforce Configuration](./media/salesforce-tutorial/tutorial_salesforce_configure.png) 

1. <span data-ttu-id="39c64-173">Open a new tab in your browser and log in to your Salesforce administrator account.</span><span class="sxs-lookup"><span data-stu-id="39c64-173">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

1. <span data-ttu-id="39c64-174">Click on the **Setup** under **settings icon** on the top right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="39c64-174">Click on the **Setup** under **settings icon** on the top right corner of the page.</span></span>

    ![Configure Single Sign-On](./media/salesforce-tutorial/configure1.png)

1. <span data-ttu-id="39c64-176">Scroll down to the **SETTINGS** in the navigation pane, click **Identity** to expand the related section.</span><span class="sxs-lookup"><span data-stu-id="39c64-176">Scroll down to the **SETTINGS** in the navigation pane, click **Identity** to expand the related section.</span></span> <span data-ttu-id="39c64-177">Then click **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="39c64-177">Then click **Single Sign-On Settings**.</span></span>

    ![Configure Single Sign-On](./media/salesforce-tutorial/sf-admin-sso.png)

1. <span data-ttu-id="39c64-179">On the **Single Sign-On Settings** page, click the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="39c64-179">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>

    ![Configure Single Sign-On](./media/salesforce-tutorial/sf-admin-sso-edit.png)
    
    > [!NOTE]
    > <span data-ttu-id="39c64-181">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="39c64-181">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

1. <span data-ttu-id="39c64-182">Select **SAML Enabled**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="39c64-182">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Configure Single Sign-On](./media/salesforce-tutorial/sf-enable-saml.png)
1. <span data-ttu-id="39c64-184">To configure your SAML single sign-on settings, click **New**.</span><span class="sxs-lookup"><span data-stu-id="39c64-184">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Configure Single Sign-On](./media/salesforce-tutorial/sf-admin-sso-new.png)

1. <span data-ttu-id="39c64-186">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span><span class="sxs-lookup"><span data-stu-id="39c64-186">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![Configure Single Sign-On](./media/salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="39c64-188">a.</span><span class="sxs-lookup"><span data-stu-id="39c64-188">a.</span></span> <span data-ttu-id="39c64-189">For the **Name** field, type in a friendly name for this configuration.</span><span class="sxs-lookup"><span data-stu-id="39c64-189">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="39c64-190">Providing a value for **Name** automatically populate the **API Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="39c64-190">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="39c64-191">b.</span><span class="sxs-lookup"><span data-stu-id="39c64-191">b.</span></span> <span data-ttu-id="39c64-192">In the **Issuer** field, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="39c64-192">In the **Issuer** field, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="39c64-193">c.</span><span class="sxs-lookup"><span data-stu-id="39c64-193">c.</span></span> <span data-ttu-id="39c64-194">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="39c64-194">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>

      * <span data-ttu-id="39c64-195">Enterprise account: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="39c64-195">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="39c64-196">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="39c64-196">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    <span data-ttu-id="39c64-197">d.</span><span class="sxs-lookup"><span data-stu-id="39c64-197">d.</span></span> <span data-ttu-id="39c64-198">To upload the **Identity Provider Certificate**, click **Choose File** to browse and select the certificate file, which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="39c64-198">To upload the **Identity Provider Certificate**, click **Choose File** to browse and select the certificate file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="39c64-199">e.</span><span class="sxs-lookup"><span data-stu-id="39c64-199">e.</span></span> <span data-ttu-id="39c64-200">As **SAML Identity Type**, choose one of the following options:</span><span class="sxs-lookup"><span data-stu-id="39c64-200">As **SAML Identity Type**, choose one of the following options:</span></span>

      * <span data-ttu-id="39c64-201">Select **Assertion contains the User's Salesforce username**, if user's Salesforce Username is being passed in SAML assertion</span><span class="sxs-lookup"><span data-stu-id="39c64-201">Select **Assertion contains the User's Salesforce username**, if user's Salesforce Username is being passed in SAML assertion</span></span>

      * <span data-ttu-id="39c64-202">Select **Assertion contains the Federation ID from the User object**, if Federation ID from the User object is being passed in SAML assertion</span><span class="sxs-lookup"><span data-stu-id="39c64-202">Select **Assertion contains the Federation ID from the User object**, if Federation ID from the User object is being passed in SAML assertion</span></span>

      * <span data-ttu-id="39c64-203">Select **Assertion contains the Use ID from the User object**, if User ID from the User object is being passed in SAML assertion</span><span class="sxs-lookup"><span data-stu-id="39c64-203">Select **Assertion contains the Use ID from the User object**, if User ID from the User object is being passed in SAML assertion</span></span>

    <span data-ttu-id="39c64-204">f.</span><span class="sxs-lookup"><span data-stu-id="39c64-204">f.</span></span> <span data-ttu-id="39c64-205">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="39c64-205">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="39c64-206">g.</span><span class="sxs-lookup"><span data-stu-id="39c64-206">g.</span></span> <span data-ttu-id="39c64-207">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span><span class="sxs-lookup"><span data-stu-id="39c64-207">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="39c64-208">h.</span><span class="sxs-lookup"><span data-stu-id="39c64-208">h.</span></span> <span data-ttu-id="39c64-209">In **Identity Provider Login URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal</span><span class="sxs-lookup"><span data-stu-id="39c64-209">In **Identity Provider Login URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal</span></span>

    <span data-ttu-id="39c64-210">i.</span><span class="sxs-lookup"><span data-stu-id="39c64-210">i.</span></span> <span data-ttu-id="39c64-211">Finally, click **Save** to apply your SAML single sign-on settings.</span><span class="sxs-lookup"><span data-stu-id="39c64-211">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

1. <span data-ttu-id="39c64-212">On the left navigation pane in Salesforce, click **Company Settings** to expand the related section, and then click **My Domain**.</span><span class="sxs-lookup"><span data-stu-id="39c64-212">On the left navigation pane in Salesforce, click **Company Settings** to expand the related section, and then click **My Domain**.</span></span>

    ![Configure Single Sign-On](./media/salesforce-tutorial/sf-my-domain.png)

1. <span data-ttu-id="39c64-214">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="39c64-214">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![Configure Single Sign-On](./media/salesforce-tutorial/sf-edit-auth-config.png)

1. <span data-ttu-id="39c64-216">In the **Authentication Configuration** section, Check the **AzureSSO** as **Authentication Servie** of your SAML SSO configuration, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="39c64-216">In the **Authentication Configuration** section, Check the **AzureSSO** as **Authentication Servie** of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Configure Single Sign-On](./media/salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="39c64-218">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span><span class="sxs-lookup"><span data-stu-id="39c64-218">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="39c64-219">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span><span class="sxs-lookup"><span data-stu-id="39c64-219">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="39c64-220">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="39c64-220">Create an Azure AD test user</span></span>

<span data-ttu-id="39c64-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39c64-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="39c64-223">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39c64-223">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="39c64-224">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="39c64-224">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/salesforce-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="39c64-226">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="39c64-226">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/salesforce-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="39c64-228">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="39c64-228">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/salesforce-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="39c64-230">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="39c64-230">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/salesforce-tutorial/create_aaduser_04.png)

    <span data-ttu-id="39c64-232">a.</span><span class="sxs-lookup"><span data-stu-id="39c64-232">a.</span></span> <span data-ttu-id="39c64-233">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39c64-233">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39c64-234">b.</span><span class="sxs-lookup"><span data-stu-id="39c64-234">b.</span></span> <span data-ttu-id="39c64-235">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39c64-235">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="39c64-236">c.</span><span class="sxs-lookup"><span data-stu-id="39c64-236">c.</span></span> <span data-ttu-id="39c64-237">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="39c64-237">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="39c64-238">d.</span><span class="sxs-lookup"><span data-stu-id="39c64-238">d.</span></span> <span data-ttu-id="39c64-239">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="39c64-239">Click **Create**.</span></span>

### <a name="create-a-salesforce-test-user"></a><span data-ttu-id="39c64-240">Create a Salesforce test user</span><span class="sxs-lookup"><span data-stu-id="39c64-240">Create a Salesforce test user</span></span>

<span data-ttu-id="39c64-241">In this section, a user called Britta Simon is created in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="39c64-241">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="39c64-242">Salesforce supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="39c64-242">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span> <span data-ttu-id="39c64-243">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="39c64-243">There is no action item for you in this section.</span></span> <span data-ttu-id="39c64-244">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span><span class="sxs-lookup"><span data-stu-id="39c64-244">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span> <span data-ttu-id="39c64-245">Salesforce also supports automatic user provisioning, you can find more details [here](salesforce-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="39c64-245">Salesforce also supports automatic user provisioning, you can find more details [here](salesforce-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="39c64-246">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="39c64-246">Assign the Azure AD test user</span></span>

<span data-ttu-id="39c64-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="39c64-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![Assign the user role][200]

<span data-ttu-id="39c64-249">**To assign Britta Simon to Salesforce, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39c64-249">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="39c64-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="39c64-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="39c64-252">In the applications list, select **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="39c64-252">In the applications list, select **Salesforce**.</span></span>

    ![The Salesforce link in the Applications list](./media/salesforce-tutorial/tutorial_salesforce_app.png)

1. <span data-ttu-id="39c64-254">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="39c64-254">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="39c64-256">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="39c64-256">Click **Add** button.</span></span> <span data-ttu-id="39c64-257">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="39c64-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="39c64-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="39c64-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="39c64-260">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="39c64-260">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="39c64-261">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="39c64-261">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="39c64-262">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="39c64-262">Test single sign-on</span></span>

<span data-ttu-id="39c64-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="39c64-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="39c64-264">When you click the Salesforce tile in the Access Panel, you should get automatically signed-on to your Salesforce application.</span><span class="sxs-lookup"><span data-stu-id="39c64-264">When you click the Salesforce tile in the Access Panel, you should get automatically signed-on to your Salesforce application.</span></span>
<span data-ttu-id="39c64-265">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39c64-265">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="39c64-266">Additional resources</span><span class="sxs-lookup"><span data-stu-id="39c64-266">Additional resources</span></span>

* [<span data-ttu-id="39c64-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39c64-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="39c64-268">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39c64-268">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="39c64-269">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="39c64-269">Configure User Provisioning</span></span>](salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/salesforce-tutorial/tutorial_general_01.png
[2]: ./media/salesforce-tutorial/tutorial_general_02.png
[3]: ./media/salesforce-tutorial/tutorial_general_03.png
[4]: ./media/salesforce-tutorial/tutorial_general_04.png

[100]: ./media/salesforce-tutorial/tutorial_general_100.png

[200]: ./media/salesforce-tutorial/tutorial_general_200.png
[201]: ./media/salesforce-tutorial/tutorial_general_201.png
[202]: ./media/salesforce-tutorial/tutorial_general_202.png
[203]: ./media/salesforce-tutorial/tutorial_general_203.png
