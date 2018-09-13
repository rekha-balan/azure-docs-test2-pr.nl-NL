---
title: 'Tutorial: Azure Active Directory integration with Riskware | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Riskware.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81866167-b163-4695-8978-fd29a25dac7a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2018
ms.author: jeedes
ms.openlocfilehash: 4c664fac99e93e94b46f5d917a63aa6530b695bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865896"
---
# <a name="tutorial-azure-active-directory-integration-with-riskware"></a><span data-ttu-id="e8e63-103">Tutorial: Azure Active Directory integration with Riskware</span><span class="sxs-lookup"><span data-stu-id="e8e63-103">Tutorial: Azure Active Directory integration with Riskware</span></span>

<span data-ttu-id="e8e63-104">In this tutorial, you learn how to integrate Riskware with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e8e63-104">In this tutorial, you learn how to integrate Riskware with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8e63-105">Integrating Riskware with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e8e63-105">Integrating Riskware with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e8e63-106">You can control in Azure AD who has access to Riskware.</span><span class="sxs-lookup"><span data-stu-id="e8e63-106">You can control in Azure AD who has access to Riskware.</span></span>
- <span data-ttu-id="e8e63-107">You can enable your users to automatically get signed-on to Riskware (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="e8e63-107">You can enable your users to automatically get signed-on to Riskware (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e8e63-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e8e63-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e8e63-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e8e63-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8e63-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e8e63-110">Prerequisites</span></span>

<span data-ttu-id="e8e63-111">To configure Azure AD integration with Riskware, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e8e63-111">To configure Azure AD integration with Riskware, you need the following items:</span></span>

- <span data-ttu-id="e8e63-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e8e63-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8e63-113">A Riskware single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e8e63-113">A Riskware single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8e63-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e8e63-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8e63-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e8e63-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8e63-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e8e63-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8e63-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8e63-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8e63-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e8e63-118">Scenario description</span></span>
<span data-ttu-id="e8e63-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e8e63-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8e63-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e8e63-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8e63-121">Adding Riskware from the gallery</span><span class="sxs-lookup"><span data-stu-id="e8e63-121">Adding Riskware from the gallery</span></span>
1. <span data-ttu-id="e8e63-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e8e63-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-riskware-from-the-gallery"></a><span data-ttu-id="e8e63-123">Adding Riskware from the gallery</span><span class="sxs-lookup"><span data-stu-id="e8e63-123">Adding Riskware from the gallery</span></span>
<span data-ttu-id="e8e63-124">To configure the integration of Riskware into Azure AD, you need to add Riskware from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e8e63-124">To configure the integration of Riskware into Azure AD, you need to add Riskware from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e8e63-125">**To add Riskware from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e8e63-125">**To add Riskware from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e8e63-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e8e63-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="e8e63-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e8e63-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

1. <span data-ttu-id="e8e63-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e8e63-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="e8e63-133">In the search box, type **Riskware**, select **Riskware** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e8e63-133">In the search box, type **Riskware**, select **Riskware** from result panel then click **Add** button to add the application.</span></span>

    ![Riskware in the results list](./media/riskware-tutorial/tutorial_riskware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e8e63-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e8e63-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e8e63-136">In this section, you configure and test Azure AD single sign-on with Riskware based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e8e63-136">In this section, you configure and test Azure AD single sign-on with Riskware based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8e63-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Riskware is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8e63-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Riskware is to a user in Azure AD.</span></span> <span data-ttu-id="e8e63-138">In other words, a link relationship between an Azure AD user and the related user in Riskware needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e8e63-138">In other words, a link relationship between an Azure AD user and the related user in Riskware needs to be established.</span></span>

<span data-ttu-id="e8e63-139">To configure and test Azure AD single sign-on with Riskware, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e8e63-139">To configure and test Azure AD single sign-on with Riskware, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e8e63-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e8e63-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e8e63-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8e63-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e8e63-142">**[Create a Riskware test user](#create-a-riskware-test-user)** - to have a counterpart of Britta Simon in Riskware that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e8e63-142">**[Create a Riskware test user](#create-a-riskware-test-user)** - to have a counterpart of Britta Simon in Riskware that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e8e63-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e8e63-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e8e63-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e8e63-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e8e63-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e8e63-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e8e63-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Riskware application.</span><span class="sxs-lookup"><span data-stu-id="e8e63-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Riskware application.</span></span>

<span data-ttu-id="e8e63-147">**To configure Azure AD single sign-on with Riskware, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e8e63-147">**To configure Azure AD single sign-on with Riskware, perform the following steps:**</span></span>

1. <span data-ttu-id="e8e63-148">In the Azure portal, on the **Riskware** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-148">In the Azure portal, on the **Riskware** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="e8e63-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e8e63-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/riskware-tutorial/tutorial_riskware_samlbase.png)

1. <span data-ttu-id="e8e63-152">On the **Riskware Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e8e63-152">On the **Riskware Domain and URLs** section, perform the following steps:</span></span>

    ![Riskware Domain and URLs single sign-on information](./media/riskware-tutorial/tutorial_riskware_url.png)

    <span data-ttu-id="e8e63-154">a.</span><span class="sxs-lookup"><span data-stu-id="e8e63-154">a.</span></span> <span data-ttu-id="e8e63-155">In the **Sign on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="e8e63-155">In the **Sign on URL** textbox, type a URL using the following pattern:</span></span>
    | <span data-ttu-id="e8e63-156">Environment</span><span class="sxs-lookup"><span data-stu-id="e8e63-156">Environment</span></span>| <span data-ttu-id="e8e63-157">URL Pattern</span><span class="sxs-lookup"><span data-stu-id="e8e63-157">URL Pattern</span></span>|
    |--|--|
    | <span data-ttu-id="e8e63-158">UAT</span><span class="sxs-lookup"><span data-stu-id="e8e63-158">UAT</span></span>|  `https://riskcloud.net/uat?ccode=<COMPANYCODE>` |
    | <span data-ttu-id="e8e63-159">PROD</span><span class="sxs-lookup"><span data-stu-id="e8e63-159">PROD</span></span>| `https://riskcloud.net/prod?ccode=<COMPANYCODE>` |
    | <span data-ttu-id="e8e63-160">DEMO</span><span class="sxs-lookup"><span data-stu-id="e8e63-160">DEMO</span></span>| `https://riskcloud.net/demo?ccode=<COMPANYCODE>` |
    |||

    <span data-ttu-id="e8e63-161">b.</span><span class="sxs-lookup"><span data-stu-id="e8e63-161">b.</span></span> <span data-ttu-id="e8e63-162">In the **Identifier (Entity ID)** textbox, type a URL:</span><span class="sxs-lookup"><span data-stu-id="e8e63-162">In the **Identifier (Entity ID)** textbox, type a URL:</span></span>
    | <span data-ttu-id="e8e63-163">Environment</span><span class="sxs-lookup"><span data-stu-id="e8e63-163">Environment</span></span>| <span data-ttu-id="e8e63-164">URL Pattern</span><span class="sxs-lookup"><span data-stu-id="e8e63-164">URL Pattern</span></span>|
    |--|--|
    | <span data-ttu-id="e8e63-165">UAT</span><span class="sxs-lookup"><span data-stu-id="e8e63-165">UAT</span></span>| `https://riskcloud.net/uat` |
    | <span data-ttu-id="e8e63-166">PROD</span><span class="sxs-lookup"><span data-stu-id="e8e63-166">PROD</span></span>| `https://riskcloud.net/prod` |
    | <span data-ttu-id="e8e63-167">DEMO</span><span class="sxs-lookup"><span data-stu-id="e8e63-167">DEMO</span></span>| `https://riskcloud.net/demo` |
    |||

    > [!NOTE]
    > <span data-ttu-id="e8e63-168">The Sign on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="e8e63-168">The Sign on URL value is not real.</span></span> <span data-ttu-id="e8e63-169">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="e8e63-169">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="e8e63-170">Contact [Riskware Client support team](mailto:support@pansoftware.com.au) to get the value.</span><span class="sxs-lookup"><span data-stu-id="e8e63-170">Contact [Riskware Client support team](mailto:support@pansoftware.com.au) to get the value.</span></span>

1. <span data-ttu-id="e8e63-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e8e63-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/riskware-tutorial/tutorial_riskware_certificate.png) 

1. <span data-ttu-id="e8e63-173">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e8e63-173">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/riskware-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e8e63-175">On the **Riskware Configuration** section, click **Configure Riskware** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="e8e63-175">On the **Riskware Configuration** section, click **Configure Riskware** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e8e63-176">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="e8e63-176">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Riskware Configuration](./media/riskware-tutorial/tutorial_riskware_configure.png)

1. <span data-ttu-id="e8e63-178">In a different web browser window, sign in to your Riskware company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e8e63-178">In a different web browser window, sign in to your Riskware company site as an administrator.</span></span>

1. <span data-ttu-id="e8e63-179">On the top right, click **Maintenance** to open the maintenance page.</span><span class="sxs-lookup"><span data-stu-id="e8e63-179">On the top right, click **Maintenance** to open the maintenance page.</span></span>

    ![Riskware Configurations maintain](./media/riskware-tutorial/tutorial_riskware_maintain.png)

1. <span data-ttu-id="e8e63-181">In the maintenance page, click **Authentication**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-181">In the maintenance page, click **Authentication**.</span></span>

    ![Riskware Configuration authen](./media/riskware-tutorial/tutorial_riskware_authen.png)

1. <span data-ttu-id="e8e63-183">In **Authentication Configuration** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e8e63-183">In **Authentication Configuration** page, perform the following steps:</span></span>

    ![Riskware Configuration authenconfig](./media/riskware-tutorial/tutorial_riskware_config.png)

    <span data-ttu-id="e8e63-185">a.</span><span class="sxs-lookup"><span data-stu-id="e8e63-185">a.</span></span> <span data-ttu-id="e8e63-186">Select **Type** as **SAML** for authentication.</span><span class="sxs-lookup"><span data-stu-id="e8e63-186">Select **Type** as **SAML** for authentication.</span></span>

    <span data-ttu-id="e8e63-187">b.</span><span class="sxs-lookup"><span data-stu-id="e8e63-187">b.</span></span> <span data-ttu-id="e8e63-188">In the **Code** textbox, type your code like AZURE_UAT.</span><span class="sxs-lookup"><span data-stu-id="e8e63-188">In the **Code** textbox, type your code like AZURE_UAT.</span></span>

    <span data-ttu-id="e8e63-189">c.</span><span class="sxs-lookup"><span data-stu-id="e8e63-189">c.</span></span> <span data-ttu-id="e8e63-190">In the **Description** textbox, type your description like AZURE Configuration for SSO.</span><span class="sxs-lookup"><span data-stu-id="e8e63-190">In the **Description** textbox, type your description like AZURE Configuration for SSO.</span></span>

    <span data-ttu-id="e8e63-191">d.</span><span class="sxs-lookup"><span data-stu-id="e8e63-191">d.</span></span> <span data-ttu-id="e8e63-192">In **Single Sign On Page** textbox, paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e8e63-192">In **Single Sign On Page** textbox, paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e8e63-193">e.</span><span class="sxs-lookup"><span data-stu-id="e8e63-193">e.</span></span> <span data-ttu-id="e8e63-194">In **Sign out Page** textbox, paste the **Sign-Out URL** value, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e8e63-194">In **Sign out Page** textbox, paste the **Sign-Out URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e8e63-195">f.</span><span class="sxs-lookup"><span data-stu-id="e8e63-195">f.</span></span> <span data-ttu-id="e8e63-196">In the **Post Form Field** textbox, type the field name present in Post Response that contains SAML like SAMLResponse</span><span class="sxs-lookup"><span data-stu-id="e8e63-196">In the **Post Form Field** textbox, type the field name present in Post Response that contains SAML like SAMLResponse</span></span>

    <span data-ttu-id="e8e63-197">g.</span><span class="sxs-lookup"><span data-stu-id="e8e63-197">g.</span></span> <span data-ttu-id="e8e63-198">In the **XML Identity Tag Name** textbox, type attribute, which contains the unique identifier in the SAML response like NameID.</span><span class="sxs-lookup"><span data-stu-id="e8e63-198">In the **XML Identity Tag Name** textbox, type attribute, which contains the unique identifier in the SAML response like NameID.</span></span>

    <span data-ttu-id="e8e63-199">h.</span><span class="sxs-lookup"><span data-stu-id="e8e63-199">h.</span></span> <span data-ttu-id="e8e63-200">Open the downloaded **Metadata Xml** from Azure portal in notepad, copy the certificate from the Metadata file and paste it into the **Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="e8e63-200">Open the downloaded **Metadata Xml** from Azure portal in notepad, copy the certificate from the Metadata file and paste it into the **Certificate** textbox</span></span>

    <span data-ttu-id="e8e63-201">i.</span><span class="sxs-lookup"><span data-stu-id="e8e63-201">i.</span></span> <span data-ttu-id="e8e63-202">In **Consumer URL** textbox, paste the value of **Reply URL**, which you get from the support team.</span><span class="sxs-lookup"><span data-stu-id="e8e63-202">In **Consumer URL** textbox, paste the value of **Reply URL**, which you get from the support team.</span></span>

    <span data-ttu-id="e8e63-203">j.</span><span class="sxs-lookup"><span data-stu-id="e8e63-203">j.</span></span> <span data-ttu-id="e8e63-204">In **Issuer** textbox, paste the value of **Identifier**, which you get from the support team.</span><span class="sxs-lookup"><span data-stu-id="e8e63-204">In **Issuer** textbox, paste the value of **Identifier**, which you get from the support team.</span></span>

    > [!Note]
    > <span data-ttu-id="e8e63-205">Contact [Riskware Client support team](mailto:support@pansoftware.com.au) to get these values</span><span class="sxs-lookup"><span data-stu-id="e8e63-205">Contact [Riskware Client support team](mailto:support@pansoftware.com.au) to get these values</span></span>

    <span data-ttu-id="e8e63-206">k.</span><span class="sxs-lookup"><span data-stu-id="e8e63-206">k.</span></span> <span data-ttu-id="e8e63-207">Select **Use POST** checkbox.</span><span class="sxs-lookup"><span data-stu-id="e8e63-207">Select **Use POST** checkbox.</span></span>

    <span data-ttu-id="e8e63-208">l.</span><span class="sxs-lookup"><span data-stu-id="e8e63-208">l.</span></span> <span data-ttu-id="e8e63-209">Select **Use SAML Request** checkbox.</span><span class="sxs-lookup"><span data-stu-id="e8e63-209">Select **Use SAML Request** checkbox.</span></span>

    <span data-ttu-id="e8e63-210">m.</span><span class="sxs-lookup"><span data-stu-id="e8e63-210">m.</span></span> <span data-ttu-id="e8e63-211">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-211">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e8e63-212">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e8e63-212">Create an Azure AD test user</span></span>

<span data-ttu-id="e8e63-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8e63-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="e8e63-215">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e8e63-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e8e63-216">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="e8e63-216">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/riskware-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="e8e63-218">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-218">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/riskware-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="e8e63-220">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="e8e63-220">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/riskware-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="e8e63-222">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e8e63-222">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/riskware-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e8e63-224">a.</span><span class="sxs-lookup"><span data-stu-id="e8e63-224">a.</span></span> <span data-ttu-id="e8e63-225">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-225">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8e63-226">b.</span><span class="sxs-lookup"><span data-stu-id="e8e63-226">b.</span></span> <span data-ttu-id="e8e63-227">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8e63-227">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e8e63-228">c.</span><span class="sxs-lookup"><span data-stu-id="e8e63-228">c.</span></span> <span data-ttu-id="e8e63-229">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="e8e63-229">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e8e63-230">d.</span><span class="sxs-lookup"><span data-stu-id="e8e63-230">d.</span></span> <span data-ttu-id="e8e63-231">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-231">Click **Create**.</span></span>

### <a name="create-a-riskware-test-user"></a><span data-ttu-id="e8e63-232">Create a Riskware test user</span><span class="sxs-lookup"><span data-stu-id="e8e63-232">Create a Riskware test user</span></span>

<span data-ttu-id="e8e63-233">To enable Azure AD users to sign in to Riskware, they must be provisioned into Riskware.</span><span class="sxs-lookup"><span data-stu-id="e8e63-233">To enable Azure AD users to sign in to Riskware, they must be provisioned into Riskware.</span></span> <span data-ttu-id="e8e63-234">In Riskware, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="e8e63-234">In Riskware, provisioning is a manual task.</span></span>

<span data-ttu-id="e8e63-235">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e8e63-235">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e8e63-236">Sign in to Riskware as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="e8e63-236">Sign in to Riskware as a Security Administrator.</span></span>

1. <span data-ttu-id="e8e63-237">On the top right, click **Maintenance** to open the maintenance page.</span><span class="sxs-lookup"><span data-stu-id="e8e63-237">On the top right, click **Maintenance** to open the maintenance page.</span></span> 

    ![Riskware Configuration maintains](./media/riskware-tutorial/tutorial_riskware_maintain.png)

1. <span data-ttu-id="e8e63-239">In the maintenance page, click **People**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-239">In the maintenance page, click **People**.</span></span>

    ![Riskware Configuration people](./media/riskware-tutorial/tutorial_riskware_people.png)

1. <span data-ttu-id="e8e63-241">Select **Details** tab and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e8e63-241">Select **Details** tab and perform the following steps:</span></span>

    ![Riskware Configuration details](./media/riskware-tutorial/tutorial_riskware_details.png)

    <span data-ttu-id="e8e63-243">a.</span><span class="sxs-lookup"><span data-stu-id="e8e63-243">a.</span></span> <span data-ttu-id="e8e63-244">Select **Person Type** like Employee.</span><span class="sxs-lookup"><span data-stu-id="e8e63-244">Select **Person Type** like Employee.</span></span>

    <span data-ttu-id="e8e63-245">b.</span><span class="sxs-lookup"><span data-stu-id="e8e63-245">b.</span></span> <span data-ttu-id="e8e63-246">In **First Name** textbox, enter the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-246">In **First Name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="e8e63-247">c.</span><span class="sxs-lookup"><span data-stu-id="e8e63-247">c.</span></span> <span data-ttu-id="e8e63-248">In **Surname** textbox, enter the last name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-248">In **Surname** textbox, enter the last name of user like **Simon**.</span></span>

1. <span data-ttu-id="e8e63-249">On the **Security** tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e8e63-249">On the **Security** tab, perform the following steps:</span></span>

    ![Riskware Configuration security](./media/riskware-tutorial/tutorial_riskware_security.png)

    <span data-ttu-id="e8e63-251">a.</span><span class="sxs-lookup"><span data-stu-id="e8e63-251">a.</span></span> <span data-ttu-id="e8e63-252">Under **Authentication** section, select the **Authentication** mode, which you have setup like AZURE Configuration for SSO.</span><span class="sxs-lookup"><span data-stu-id="e8e63-252">Under **Authentication** section, select the **Authentication** mode, which you have setup like AZURE Configuration for SSO.</span></span>

    <span data-ttu-id="e8e63-253">b.</span><span class="sxs-lookup"><span data-stu-id="e8e63-253">b.</span></span> <span data-ttu-id="e8e63-254">Under **Logon Details** section, in the **User ID** textbox, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-254">Under **Logon Details** section, in the **User ID** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="e8e63-255">c.</span><span class="sxs-lookup"><span data-stu-id="e8e63-255">c.</span></span> <span data-ttu-id="e8e63-256">In the **Password** textbox, enter password of the user.</span><span class="sxs-lookup"><span data-stu-id="e8e63-256">In the **Password** textbox, enter password of the user.</span></span>

1. <span data-ttu-id="e8e63-257">On the **Organization** tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e8e63-257">On the **Organization** tab, perform the following steps:</span></span>

    ![Riskware Configuration org](./media/riskware-tutorial/tutorial_riskware_org.png)

    <span data-ttu-id="e8e63-259">a.</span><span class="sxs-lookup"><span data-stu-id="e8e63-259">a.</span></span> <span data-ttu-id="e8e63-260">Select the option as **Level1** organization.</span><span class="sxs-lookup"><span data-stu-id="e8e63-260">Select the option as **Level1** organization.</span></span>

    <span data-ttu-id="e8e63-261">b.</span><span class="sxs-lookup"><span data-stu-id="e8e63-261">b.</span></span> <span data-ttu-id="e8e63-262">Under **Person's Primary Workplace** section, in the **Location** textbox, type your location.</span><span class="sxs-lookup"><span data-stu-id="e8e63-262">Under **Person's Primary Workplace** section, in the **Location** textbox, type your location.</span></span>

    <span data-ttu-id="e8e63-263">c.</span><span class="sxs-lookup"><span data-stu-id="e8e63-263">c.</span></span> <span data-ttu-id="e8e63-264">Under **Employee** section, select **Employee Status** like Casual.</span><span class="sxs-lookup"><span data-stu-id="e8e63-264">Under **Employee** section, select **Employee Status** like Casual.</span></span>

1. <span data-ttu-id="e8e63-265">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-265">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e8e63-266">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e8e63-266">Assign the Azure AD test user</span></span>

<span data-ttu-id="e8e63-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Riskware.</span><span class="sxs-lookup"><span data-stu-id="e8e63-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Riskware.</span></span>

![Assign the user role][200]

<span data-ttu-id="e8e63-269">**To assign Britta Simon to Riskware, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e8e63-269">**To assign Britta Simon to Riskware, perform the following steps:**</span></span>

1. <span data-ttu-id="e8e63-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e8e63-272">In the applications list, select **Riskware**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-272">In the applications list, select **Riskware**.</span></span>

    ![The Riskware link in the Applications list](./media/riskware-tutorial/tutorial_riskware_app.png)  

1. <span data-ttu-id="e8e63-274">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e8e63-274">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="e8e63-276">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e8e63-276">Click **Add** button.</span></span> <span data-ttu-id="e8e63-277">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e8e63-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="e8e63-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e8e63-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e8e63-280">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e8e63-280">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e8e63-281">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e8e63-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e8e63-282">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e8e63-282">Test single sign-on</span></span>

<span data-ttu-id="e8e63-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e8e63-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e8e63-284">When you click the Riskware tile in the Access Panel, you should get automatically signed-on to your Riskware application.</span><span class="sxs-lookup"><span data-stu-id="e8e63-284">When you click the Riskware tile in the Access Panel, you should get automatically signed-on to your Riskware application.</span></span>
<span data-ttu-id="e8e63-285">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e8e63-285">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e8e63-286">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e8e63-286">Additional resources</span></span>

* [<span data-ttu-id="e8e63-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8e63-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e8e63-288">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e8e63-288">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/riskware-tutorial/tutorial_general_01.png
[2]: ./media/riskware-tutorial/tutorial_general_02.png
[3]: ./media/riskware-tutorial/tutorial_general_03.png
[4]: ./media/riskware-tutorial/tutorial_general_04.png

[100]: ./media/riskware-tutorial/tutorial_general_100.png

[200]: ./media/riskware-tutorial/tutorial_general_200.png
[201]: ./media/riskware-tutorial/tutorial_general_201.png
[202]: ./media/riskware-tutorial/tutorial_general_202.png
[203]: ./media/riskware-tutorial/tutorial_general_203.png

