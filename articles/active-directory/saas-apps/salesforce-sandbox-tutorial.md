---
title: 'Tutorial: Azure Active Directory integration with Salesforce Sandbox | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2018
ms.author: jeedes
ms.openlocfilehash: 6feafba41cf65a752dd5bf0819b0b93bacff0aff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867718"
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="a5a56-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="a5a56-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="a5a56-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5a56-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5a56-105">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span><span class="sxs-lookup"><span data-stu-id="a5a56-105">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>
<span data-ttu-id="a5a56-106">For more details, see [Sandbox Overview](https://help.salesforce.com/articleView?id=create_test_instance.htm&language=en_us&type=5).</span><span class="sxs-lookup"><span data-stu-id="a5a56-106">For more details, see [Sandbox Overview](https://help.salesforce.com/articleView?id=create_test_instance.htm&language=en_us&type=5).</span></span>

<span data-ttu-id="a5a56-107">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a5a56-107">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5a56-108">You can control in Azure AD who has access to Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="a5a56-108">You can control in Azure AD who has access to Salesforce Sandbox.</span></span>
- <span data-ttu-id="a5a56-109">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a5a56-109">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a5a56-110">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5a56-110">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a5a56-111">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a5a56-111">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5a56-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a5a56-112">Prerequisites</span></span>

<span data-ttu-id="a5a56-113">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a5a56-113">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="a5a56-114">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a5a56-114">An Azure AD subscription</span></span>
- <span data-ttu-id="a5a56-115">A Salesforce Sandbox single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a5a56-115">A Salesforce Sandbox single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5a56-116">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a5a56-116">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5a56-117">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a5a56-117">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5a56-118">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a5a56-118">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5a56-119">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5a56-119">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5a56-120">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a5a56-120">Scenario description</span></span>

<span data-ttu-id="a5a56-121">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a5a56-121">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5a56-122">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a5a56-122">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5a56-123">Adding Salesforce Sandbox from the gallery</span><span class="sxs-lookup"><span data-stu-id="a5a56-123">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="a5a56-124">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5a56-124">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="a5a56-125">Adding Salesforce Sandbox from the gallery</span><span class="sxs-lookup"><span data-stu-id="a5a56-125">Adding Salesforce Sandbox from the gallery</span></span>

<span data-ttu-id="a5a56-126">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a5a56-126">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a5a56-127">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5a56-127">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a5a56-128">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a5a56-128">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="a5a56-130">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-130">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a5a56-131">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-131">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="a5a56-133">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a5a56-133">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="a5a56-135">In the search box, type **Salesforce Sandbox**, select **Salesforce Sandbox** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a5a56-135">In the search box, type **Salesforce Sandbox**, select **Salesforce Sandbox** from result panel then click **Add** button to add the application.</span></span>

    ![Salesforce Sandbox in the results list](./media/salesforce-sandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a5a56-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5a56-137">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a5a56-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a5a56-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a5a56-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5a56-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="a5a56-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a5a56-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="a5a56-141">In Salesforce Sandbox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a5a56-141">In Salesforce Sandbox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a5a56-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a5a56-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5a56-143">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a5a56-143">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a5a56-144">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5a56-144">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5a56-145">**[Create a Salesforce Sandbox test user](#create-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a5a56-145">**[Create a Salesforce Sandbox test user](#create-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5a56-146">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a5a56-146">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5a56-147">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a5a56-147">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a5a56-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5a56-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a5a56-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span><span class="sxs-lookup"><span data-stu-id="a5a56-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="a5a56-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5a56-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="a5a56-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="a5a56-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a5a56-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/salesforce-sandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="a5a56-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="a5a56-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

   ![Salesforce Sandbox Domain and URLs single sign-on information](./media/salesforce-sandbox-tutorial/tutorial_salesforcesandbox_url1.png)

   <span data-ttu-id="a5a56-157">In the **Reply URL** textbox, type your organization specific **Reply URL**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-157">In the **Reply URL** textbox, type your organization specific **Reply URL**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a5a56-158">Update Reply URL value with the actual Reply URL which is explained later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a5a56-158">Update Reply URL value with the actual Reply URL which is explained later in this tutorial.</span></span>

4. <span data-ttu-id="a5a56-159">On the **SAML Signing Certificate** section, click **Certificate(RAW)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a5a56-159">On the **SAML Signing Certificate** section, click **Certificate(RAW)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/salesforce-sandbox-tutorial/tutorial_salesforcesandbox_certificate.png)

5. <span data-ttu-id="a5a56-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a5a56-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/salesforce-sandbox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a5a56-163">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a5a56-163">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a5a56-164">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a5a56-164">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/tutorial_salesforcesandbox_configure.png)

7. <span data-ttu-id="a5a56-166">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span><span class="sxs-lookup"><span data-stu-id="a5a56-166">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

8. <span data-ttu-id="a5a56-167">Click on the **Setup** under **settings icon** on the top right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="a5a56-167">Click on the **Setup** under **settings icon** on the top right corner of the page.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/configure1.png)

9. <span data-ttu-id="a5a56-169">Scroll down to the **SETTINGS** in the left navigation pane, click **Identity** to expand the related section.</span><span class="sxs-lookup"><span data-stu-id="a5a56-169">Scroll down to the **SETTINGS** in the left navigation pane, click **Identity** to expand the related section.</span></span> <span data-ttu-id="a5a56-170">Then click **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-170">Then click **Single Sign-On Settings**.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/sf-admin-sso.png)

10. <span data-ttu-id="a5a56-172">On the **Single Sign-On Settings** page, click the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="a5a56-172">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/configure3.png)

11. <span data-ttu-id="a5a56-174">Select **SAML Enabled**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-174">Select **SAML Enabled**, and then click **Save**.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/sf-enable-saml.png)

12. <span data-ttu-id="a5a56-176">To configure your SAML single sign-on settings, click **New**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-176">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/sf-admin-sso-new.png)

13. <span data-ttu-id="a5a56-178">On the **Single Sign-On Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5a56-178">On the **Single Sign-On Settings** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/sf-saml-config1.png)

    <span data-ttu-id="a5a56-180">a.</span><span class="sxs-lookup"><span data-stu-id="a5a56-180">a.</span></span> <span data-ttu-id="a5a56-181">Select **SAML Enabled** checkbox.</span><span class="sxs-lookup"><span data-stu-id="a5a56-181">Select **SAML Enabled** checkbox.</span></span>

    <span data-ttu-id="a5a56-182">b.</span><span class="sxs-lookup"><span data-stu-id="a5a56-182">b.</span></span> <span data-ttu-id="a5a56-183">In the **Issuer** field, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5a56-183">In the **Issuer** field, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a5a56-184">c.</span><span class="sxs-lookup"><span data-stu-id="a5a56-184">c.</span></span> <span data-ttu-id="a5a56-185">To upload the **Identity Provider Certificate**, click **Browse** to browse and select the certificate file, which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5a56-185">To upload the **Identity Provider Certificate**, click **Browse** to browse and select the certificate file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="a5a56-186">d.</span><span class="sxs-lookup"><span data-stu-id="a5a56-186">d.</span></span> <span data-ttu-id="a5a56-187">In **Identity Provider Login URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5a56-187">In **Identity Provider Login URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a5a56-188">e.</span><span class="sxs-lookup"><span data-stu-id="a5a56-188">e.</span></span> <span data-ttu-id="a5a56-189">As **SAML Identity Type**, choose one of the following options:</span><span class="sxs-lookup"><span data-stu-id="a5a56-189">As **SAML Identity Type**, choose one of the following options:</span></span>

      * <span data-ttu-id="a5a56-190">Select **Assertion contains the User's Salesforce username**, if user's Salesforce Username is being passed in SAML assertion</span><span class="sxs-lookup"><span data-stu-id="a5a56-190">Select **Assertion contains the User's Salesforce username**, if user's Salesforce Username is being passed in SAML assertion</span></span>

      * <span data-ttu-id="a5a56-191">Select **Assertion contains the Federation ID from the User object**, if Federation ID from the User object is being passed in SAML assertion</span><span class="sxs-lookup"><span data-stu-id="a5a56-191">Select **Assertion contains the Federation ID from the User object**, if Federation ID from the User object is being passed in SAML assertion</span></span>
  
    <span data-ttu-id="a5a56-192">f.</span><span class="sxs-lookup"><span data-stu-id="a5a56-192">f.</span></span> <span data-ttu-id="a5a56-193">As **SAML Identity Location**, select **Identity is an Attribute element**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-193">As **SAML Identity Location**, select **Identity is an Attribute element**.</span></span>

    <span data-ttu-id="a5a56-194">g.</span><span class="sxs-lookup"><span data-stu-id="a5a56-194">g.</span></span> <span data-ttu-id="a5a56-195">SFDC does not support SAML logout.</span><span class="sxs-lookup"><span data-stu-id="a5a56-195">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="a5a56-196">As a workaround, paste `https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0` into the **Custom Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="a5a56-196">As a workaround, paste `https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0` into the **Custom Logout URL** textbox.</span></span>

    <span data-ttu-id="a5a56-197">h.</span><span class="sxs-lookup"><span data-stu-id="a5a56-197">h.</span></span> <span data-ttu-id="a5a56-198">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-198">Click **Save**.</span></span>

14. <span data-ttu-id="a5a56-199">On the **Single Sign-On Settings** page, click the **Download Metadata** button.</span><span class="sxs-lookup"><span data-stu-id="a5a56-199">On the **Single Sign-On Settings** page, click the **Download Metadata** button.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/configure4.png)

15. <span data-ttu-id="a5a56-201">Open the downloaded Metadata in a different browser window and copy the **Location** value and paste it into the **Reply URL** textbox on the **Salesforce Sandbox Domain and URLs** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5a56-201">Open the downloaded Metadata in a different browser window and copy the **Location** value and paste it into the **Reply URL** textbox on the **Salesforce Sandbox Domain and URLs** section in the Azure portal.</span></span>  

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/configure5.png)

16. <span data-ttu-id="a5a56-203">If you wish to configure the application in **SP** initiated mode, following are the prerequisites for that:</span><span class="sxs-lookup"><span data-stu-id="a5a56-203">If you wish to configure the application in **SP** initiated mode, following are the prerequisites for that:</span></span>

    <span data-ttu-id="a5a56-204">a.</span><span class="sxs-lookup"><span data-stu-id="a5a56-204">a.</span></span> <span data-ttu-id="a5a56-205">You should have a verified domain.</span><span class="sxs-lookup"><span data-stu-id="a5a56-205">You should have a verified domain.</span></span>

    <span data-ttu-id="a5a56-206">b.</span><span class="sxs-lookup"><span data-stu-id="a5a56-206">b.</span></span> <span data-ttu-id="a5a56-207">You need to configure and enable your domain on Salesforce Sandbox, steps for this are explained later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a5a56-207">You need to configure and enable your domain on Salesforce Sandbox, steps for this are explained later in this tutorial.</span></span>

    <span data-ttu-id="a5a56-208">c.</span><span class="sxs-lookup"><span data-stu-id="a5a56-208">c.</span></span> <span data-ttu-id="a5a56-209">In the Azure portal, on the **Salesforce Sandbox Domain and URLs** section, check **Show advanced URL settings** and perform the following step:</span><span class="sxs-lookup"><span data-stu-id="a5a56-209">In the Azure portal, on the **Salesforce Sandbox Domain and URLs** section, check **Show advanced URL settings** and perform the following step:</span></span>
  
    ![Salesforce Sandbox Domain and URLs single sign-on information](./media/salesforce-sandbox-tutorial/tutorial_salesforcesandbox_url.png)

    <span data-ttu-id="a5a56-211">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instancename>--Sandbox.<entityid>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="a5a56-211">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instancename>--Sandbox.<entityid>.my.salesforce.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5a56-212">This value should be copied from the Salesforce Sandbox portal once you have enabled the domain.</span><span class="sxs-lookup"><span data-stu-id="a5a56-212">This value should be copied from the Salesforce Sandbox portal once you have enabled the domain.</span></span>

17. <span data-ttu-id="a5a56-213">On the **SAML Signing Certificate** section, click **Certificate(RAW)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a5a56-213">On the **SAML Signing Certificate** section, click **Certificate(RAW)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/salesforce-sandbox-tutorial/tutorial_salesforcesandbox_certificate.png)

18. <span data-ttu-id="a5a56-215">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a5a56-215">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/salesforce-sandbox-tutorial/tutorial_general_400.png)

19. <span data-ttu-id="a5a56-217">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a5a56-217">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a5a56-218">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a5a56-218">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/tutorial_salesforcesandbox_configure.png)

20. <span data-ttu-id="a5a56-220">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span><span class="sxs-lookup"><span data-stu-id="a5a56-220">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

21. <span data-ttu-id="a5a56-221">Click on the **Setup** under **settings icon** on the top right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="a5a56-221">Click on the **Setup** under **settings icon** on the top right corner of the page.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/configure1.png)

22. <span data-ttu-id="a5a56-223">Scroll down to the **SETTINGS** in the left navigation pane, click **Identity** to expand the related section.</span><span class="sxs-lookup"><span data-stu-id="a5a56-223">Scroll down to the **SETTINGS** in the left navigation pane, click **Identity** to expand the related section.</span></span> <span data-ttu-id="a5a56-224">Then click **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-224">Then click **Single Sign-On Settings**.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/sf-admin-sso.png)

23. <span data-ttu-id="a5a56-226">On the **Single Sign-On Settings** page, click the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="a5a56-226">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/configure3.png)

24. <span data-ttu-id="a5a56-228">Select **SAML Enabled**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-228">Select **SAML Enabled**, and then click **Save**.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/sf-enable-saml.png)

25. <span data-ttu-id="a5a56-230">To configure your SAML single sign-on settings, click **New**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-230">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/sf-admin-sso-new.png)

26. <span data-ttu-id="a5a56-232">If you are adding a second instance, you need to enable a domain as we mentioned above (SP initiated case).</span><span class="sxs-lookup"><span data-stu-id="a5a56-232">If you are adding a second instance, you need to enable a domain as we mentioned above (SP initiated case).</span></span> <span data-ttu-id="a5a56-233">On the SAML Single Sign-On Settings section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5a56-233">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/sf-saml-config.png)

    <span data-ttu-id="a5a56-235">a.</span><span class="sxs-lookup"><span data-stu-id="a5a56-235">a.</span></span> <span data-ttu-id="a5a56-236">In the **Name** textbox, type the name of the configuration (for example: *SPSSOWAAD_Test*).</span><span class="sxs-lookup"><span data-stu-id="a5a56-236">In the **Name** textbox, type the name of the configuration (for example: *SPSSOWAAD_Test*).</span></span>

    <span data-ttu-id="a5a56-237">b.</span><span class="sxs-lookup"><span data-stu-id="a5a56-237">b.</span></span> <span data-ttu-id="a5a56-238">In the **Issuer** field, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5a56-238">In the **Issuer** field, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a5a56-239">c.</span><span class="sxs-lookup"><span data-stu-id="a5a56-239">c.</span></span> <span data-ttu-id="a5a56-240">In the **Entity ID** textbox, use `https://test.salesforce.com` value for first instance and from second instance of the application you can use the tenant specific Identifier value.</span><span class="sxs-lookup"><span data-stu-id="a5a56-240">In the **Entity ID** textbox, use `https://test.salesforce.com` value for first instance and from second instance of the application you can use the tenant specific Identifier value.</span></span>

    <span data-ttu-id="a5a56-241">d.</span><span class="sxs-lookup"><span data-stu-id="a5a56-241">d.</span></span> <span data-ttu-id="a5a56-242">To upload the **Identity Provider Certificate**, click **Choose File** to browse and select the certificate file, which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5a56-242">To upload the **Identity Provider Certificate**, click **Choose File** to browse and select the certificate file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="a5a56-243">e.</span><span class="sxs-lookup"><span data-stu-id="a5a56-243">e.</span></span> <span data-ttu-id="a5a56-244">As **SAML Identity Type**, choose one of the following options:</span><span class="sxs-lookup"><span data-stu-id="a5a56-244">As **SAML Identity Type**, choose one of the following options:</span></span>

      * <span data-ttu-id="a5a56-245">Select **Assertion contains the User's Salesforce username**, if user's Salesforce Username is being passed in SAML assertion</span><span class="sxs-lookup"><span data-stu-id="a5a56-245">Select **Assertion contains the User's Salesforce username**, if user's Salesforce Username is being passed in SAML assertion</span></span>

      * <span data-ttu-id="a5a56-246">Select **Assertion contains the Federation ID from the User object**, if Federation ID from the User object is being passed in SAML assertion</span><span class="sxs-lookup"><span data-stu-id="a5a56-246">Select **Assertion contains the Federation ID from the User object**, if Federation ID from the User object is being passed in SAML assertion</span></span>

      * <span data-ttu-id="a5a56-247">Select **Assertion contains the Use ID from the User object**, if User ID from the User object is being passed in SAML assertion</span><span class="sxs-lookup"><span data-stu-id="a5a56-247">Select **Assertion contains the Use ID from the User object**, if User ID from the User object is being passed in SAML assertion</span></span>

    <span data-ttu-id="a5a56-248">f.</span><span class="sxs-lookup"><span data-stu-id="a5a56-248">f.</span></span> <span data-ttu-id="a5a56-249">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-249">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="a5a56-250">g.</span><span class="sxs-lookup"><span data-stu-id="a5a56-250">g.</span></span> <span data-ttu-id="a5a56-251">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-251">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span>

    <span data-ttu-id="a5a56-252">h.</span><span class="sxs-lookup"><span data-stu-id="a5a56-252">h.</span></span> <span data-ttu-id="a5a56-253">In **Identity Provider Login URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5a56-253">In **Identity Provider Login URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a5a56-254">i.</span><span class="sxs-lookup"><span data-stu-id="a5a56-254">i.</span></span> <span data-ttu-id="a5a56-255">SFDC does not support SAML logout.</span><span class="sxs-lookup"><span data-stu-id="a5a56-255">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="a5a56-256">As a workaround, paste `https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0` it into the **Custom Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="a5a56-256">As a workaround, paste `https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0` it into the **Custom Logout URL** textbox.</span></span>

    <span data-ttu-id="a5a56-257">j.</span><span class="sxs-lookup"><span data-stu-id="a5a56-257">j.</span></span> <span data-ttu-id="a5a56-258">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-258">Click **Save**.</span></span>

27. <span data-ttu-id="a5a56-259">To enable your domain on Salesforce Sandbox, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5a56-259">To enable your domain on Salesforce Sandbox, perform the following steps:</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5a56-260">Before enabling the domain you need to create the same on Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="a5a56-260">Before enabling the domain you need to create the same on Salesforce Sandbox.</span></span> <span data-ttu-id="a5a56-261">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="a5a56-261">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span> <span data-ttu-id="a5a56-262">Once the domain is created, please make sure that it's configured correctly.</span><span class="sxs-lookup"><span data-stu-id="a5a56-262">Once the domain is created, please make sure that it's configured correctly.</span></span>

    * <span data-ttu-id="a5a56-263">On the left navigation pane in Salesforce Sandbox, click **Company Settings** to expand the related section, and then click **My Domain**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-263">On the left navigation pane in Salesforce Sandbox, click **Company Settings** to expand the related section, and then click **My Domain**.</span></span>

         ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/sf-my-domain.png)

    * <span data-ttu-id="a5a56-265">In the **Authentication Configuration** section, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-265">In the **Authentication Configuration** section, click **Edit**.</span></span>

        ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/sf-edit-auth-config.png)

    * <span data-ttu-id="a5a56-267">In the **Authentication Configuration** section, as **Authentication Service**, select the name of the SAML Single Sign-On Setting which you have set during SSO configuration in Salesforce Sandbox and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-267">In the **Authentication Configuration** section, as **Authentication Service**, select the name of the SAML Single Sign-On Setting which you have set during SSO configuration in Salesforce Sandbox and click **Save**.</span></span>

        ![Configure Single Sign-On](./media/salesforce-sandbox-tutorial/configure2.png)

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a5a56-269">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a5a56-269">Create an Azure AD test user</span></span>

<span data-ttu-id="a5a56-270">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5a56-270">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a5a56-272">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5a56-272">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5a56-273">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a5a56-273">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/salesforce-sandbox-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a5a56-275">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-275">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/salesforce-sandbox-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a5a56-277">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a5a56-277">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/salesforce-sandbox-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a5a56-279">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5a56-279">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/salesforce-sandbox-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a5a56-281">a.</span><span class="sxs-lookup"><span data-stu-id="a5a56-281">a.</span></span> <span data-ttu-id="a5a56-282">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-282">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5a56-283">b.</span><span class="sxs-lookup"><span data-stu-id="a5a56-283">b.</span></span> <span data-ttu-id="a5a56-284">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5a56-284">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a5a56-285">c.</span><span class="sxs-lookup"><span data-stu-id="a5a56-285">c.</span></span> <span data-ttu-id="a5a56-286">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a5a56-286">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a5a56-287">d.</span><span class="sxs-lookup"><span data-stu-id="a5a56-287">d.</span></span> <span data-ttu-id="a5a56-288">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-288">Click **Create**.</span></span>

### <a name="create-a-salesforce-sandbox-test-user"></a><span data-ttu-id="a5a56-289">Create a Salesforce Sandbox test user</span><span class="sxs-lookup"><span data-stu-id="a5a56-289">Create a Salesforce Sandbox test user</span></span>

<span data-ttu-id="a5a56-290">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="a5a56-290">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="a5a56-291">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="a5a56-291">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span> <span data-ttu-id="a5a56-292">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="a5a56-292">There is no action item for you in this section.</span></span> <span data-ttu-id="a5a56-293">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="a5a56-293">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span> <span data-ttu-id="a5a56-294">Salesforce Sandbox also supports automatic user provisioning, you can find more details [here](salesforce-sandbox-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="a5a56-294">Salesforce Sandbox also supports automatic user provisioning, you can find more details [here](salesforce-sandbox-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a5a56-295">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a5a56-295">Assign the Azure AD test user</span></span>

<span data-ttu-id="a5a56-296">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="a5a56-296">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![Assign the user role][200]

<span data-ttu-id="a5a56-298">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5a56-298">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="a5a56-299">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-299">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="a5a56-301">In the applications list, select **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-301">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![The Salesforce Sandbox link in the Applications list](./media/salesforce-sandbox-tutorial/tutorial_salesforcesandbox_app.png)  

3. <span data-ttu-id="a5a56-303">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a5a56-303">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="a5a56-305">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a5a56-305">Click **Add** button.</span></span> <span data-ttu-id="a5a56-306">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5a56-306">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="a5a56-308">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a5a56-308">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a5a56-309">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5a56-309">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5a56-310">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5a56-310">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a5a56-311">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5a56-311">Test single sign-on</span></span>

<span data-ttu-id="a5a56-312">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a5a56-312">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a5a56-313">When you click the Salesforce Sandbox tile in the Access Panel, you should get automatically signed-on to your Salesforce Sandbox application.</span><span class="sxs-lookup"><span data-stu-id="a5a56-313">When you click the Salesforce Sandbox tile in the Access Panel, you should get automatically signed-on to your Salesforce Sandbox application.</span></span>
<span data-ttu-id="a5a56-314">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5a56-314">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5a56-315">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a5a56-315">Additional resources</span></span>

* [<span data-ttu-id="a5a56-316">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5a56-316">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a5a56-317">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a5a56-317">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="a5a56-318">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="a5a56-318">Configure User Provisioning</span></span>](salesforce-sandbox-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/salesforce-sandbox-tutorial/tutorial_general_01.png
[2]: ./media/salesforce-sandbox-tutorial/tutorial_general_02.png
[3]: ./media/salesforce-sandbox-tutorial/tutorial_general_03.png
[4]: ./media/salesforce-sandbox-tutorial/tutorial_general_04.png

[100]: ./media/salesforce-sandbox-tutorial/tutorial_general_100.png

[200]: ./media/salesforce-sandbox-tutorial/tutorial_general_200.png
[201]: ./media/salesforce-sandbox-tutorial/tutorial_general_201.png
[202]: ./media/salesforce-sandbox-tutorial/tutorial_general_202.png
[203]: ./media/salesforce-sandbox-tutorial/tutorial_general_203.png