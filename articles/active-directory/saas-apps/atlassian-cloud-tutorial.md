---
title: 'Tutorial: Azure Active Directory integration with Atlassian Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Atlassian Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2018
ms.author: jeedes
ms.openlocfilehash: 68613b8613a2e5a9139b83eb23e66884659efc47
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857232"
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="3f6fa-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="3f6fa-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="3f6fa-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3f6fa-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f6fa-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3f6fa-106">You can control in Azure AD who has access to Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-106">You can control in Azure AD who has access to Atlassian Cloud.</span></span>
- <span data-ttu-id="3f6fa-107">You can enable your users to be signed on automatically (single sign-on) to Atlassian Cloud with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-107">You can enable your users to be signed on automatically (single sign-on) to Atlassian Cloud with their Azure AD accounts.</span></span>
- <span data-ttu-id="3f6fa-108">You can manage your accounts in one central location, the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="3f6fa-109">For more information about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3f6fa-109">For more information about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f6fa-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3f6fa-110">Prerequisites</span></span>

<span data-ttu-id="3f6fa-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span></span>

- <span data-ttu-id="3f6fa-112">An Azure AD subscription.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="3f6fa-113">To enable Security Assertion Markup Language (SAML) single sign-on for Atlassian Cloud products, you need to set up Atlassian Access.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-113">To enable Security Assertion Markup Language (SAML) single sign-on for Atlassian Cloud products, you need to set up Atlassian Access.</span></span> <span data-ttu-id="3f6fa-114">Learn more about [Atlassian Access]( https://www.atlassian.com/enterprise/cloud/identity-manager).</span><span class="sxs-lookup"><span data-stu-id="3f6fa-114">Learn more about [Atlassian Access]( https://www.atlassian.com/enterprise/cloud/identity-manager).</span></span>

> [!NOTE]
> <span data-ttu-id="3f6fa-115">When you test the steps in this tutorial, we recommend that you not use a production environment.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-115">When you test the steps in this tutorial, we recommend that you not use a production environment.</span></span>

<span data-ttu-id="3f6fa-116">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="3f6fa-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f6fa-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f6fa-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f6fa-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3f6fa-119">Scenario description</span></span>
<span data-ttu-id="3f6fa-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="3f6fa-121">The scenario outlined in the tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-121">The scenario outlined in the tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="3f6fa-122">Adding Atlassian Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="3f6fa-122">Adding Atlassian Cloud from the gallery</span></span>
* <span data-ttu-id="3f6fa-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3f6fa-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-atlassian-cloud-from-the-gallery"></a><span data-ttu-id="3f6fa-124">Add Atlassian Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="3f6fa-124">Add Atlassian Cloud from the gallery</span></span>
<span data-ttu-id="3f6fa-125">To configure the integration of Atlassian Cloud with Azure AD, add Atlassian Cloud from the gallery to your list of managed SaaS apps by doing the following:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-125">To configure the integration of Atlassian Cloud with Azure AD, add Atlassian Cloud from the gallery to your list of managed SaaS apps by doing the following:</span></span>

1. <span data-ttu-id="3f6fa-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="3f6fa-128">Select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-128">Select **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications pane][2]
    
3. <span data-ttu-id="3f6fa-130">To add an application, select **New application**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-130">To add an application, select **New application**.</span></span>

    ![The "New application" button][3]

4. <span data-ttu-id="3f6fa-132">In the search box, type **Atlassian Cloud**, in the results list, select **Atlassian Cloud**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-132">In the search box, type **Atlassian Cloud**, in the results list, select **Atlassian Cloud**, and then select **Add**.</span></span>

    ![Atlassian Cloud in the results list](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3f6fa-134">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3f6fa-134">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3f6fa-135">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud, based on a test user named *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-135">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud, based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="3f6fa-136">For single sign-on to work, Azure AD needs to identify the Atlassian Cloud user and its counterpart in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-136">For single sign-on to work, Azure AD needs to identify the Atlassian Cloud user and its counterpart in Azure AD.</span></span> <span data-ttu-id="3f6fa-137">In other words, you must establish a link relationship between an Azure AD user and the related user in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-137">In other words, you must establish a link relationship between an Azure AD user and the related user in Atlassian Cloud.</span></span>

<span data-ttu-id="3f6fa-138">To establish the link relationship, assign as the Atlassian Cloud *Username* the same value that's assigned to the Azure AD *user name*.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-138">To establish the link relationship, assign as the Atlassian Cloud *Username* the same value that's assigned to the Azure AD *user name*.</span></span>

<span data-ttu-id="3f6fa-139">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the building blocks in the following sections.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-139">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the building blocks in the following sections.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3f6fa-140">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3f6fa-140">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3f6fa-141">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atlassian Cloud application.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-141">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="3f6fa-142">To configure Azure AD single sign-on with Atlassian Cloud, do the following:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-142">To configure Azure AD single sign-on with Atlassian Cloud, do the following:</span></span>

1. <span data-ttu-id="3f6fa-143">In the Azure portal, in the **Atlassian Cloud** application integration pane, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-143">In the Azure portal, in the **Atlassian Cloud** application integration pane, select **Single sign-on**.</span></span>

    ![Configure Single sign-on link][4]

2. <span data-ttu-id="3f6fa-145">In the **Single sign-on** window, in the **Single Sign-on Mode** box, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-145">In the **Single sign-on** window, in the **Single Sign-on Mode** box, select **SAML-based Sign-on**.</span></span>

    ![Single sign-on window](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="3f6fa-147">To configure the application in **IDP-initiated** mode, under **Atlassian Cloud Domain and URLs**, do the following:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-147">To configure the application in **IDP-initiated** mode, under **Atlassian Cloud Domain and URLs**, do the following:</span></span>

    ![Atlassian Cloud domain and URLs single sign-on information](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)
    
    <span data-ttu-id="3f6fa-149">a.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-149">a.</span></span> <span data-ttu-id="3f6fa-150">In the **Identifier** box, type a URL with the following pattern: `https://auth.atlassian.com/saml/<unique ID>`.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-150">In the **Identifier** box, type a URL with the following pattern: `https://auth.atlassian.com/saml/<unique ID>`.</span></span>
    
    <span data-ttu-id="3f6fa-151">b.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-151">b.</span></span> <span data-ttu-id="3f6fa-152">In the **Reply URL** box, type a URL with the following pattern: `https://auth.atlassian.com/login/callback?connection=saml-<unique ID>`.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-152">In the **Reply URL** box, type a URL with the following pattern: `https://auth.atlassian.com/login/callback?connection=saml-<unique ID>`.</span></span>

    <span data-ttu-id="3f6fa-153">c.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-153">c.</span></span> <span data-ttu-id="3f6fa-154">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-154">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="3f6fa-155">d.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-155">d.</span></span> <span data-ttu-id="3f6fa-156">In the **Relay State** box, type a URL with the following pattern: `https://<instancename>.atlassian.net`.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-156">In the **Relay State** box, type a URL with the following pattern: `https://<instancename>.atlassian.net`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3f6fa-157">The preceding values are not real.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-157">The preceding values are not real.</span></span> <span data-ttu-id="3f6fa-158">Update these values with the actual identifier and reply URL.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-158">Update these values with the actual identifier and reply URL.</span></span> <span data-ttu-id="3f6fa-159">You will get these real values from the Atlassian Cloud SAML Configuration screen which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-159">You will get these real values from the Atlassian Cloud SAML Configuration screen which is explained later in the tutorial.</span></span>

4. <span data-ttu-id="3f6fa-160">To configure the application in SP-initiated mode, select the **Show advanced URL settings** and then, in the **Sign on URL** box, type a URL with the following pattern: `https://<instancename>.atlassian.net`.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-160">To configure the application in SP-initiated mode, select the **Show advanced URL settings** and then, in the **Sign on URL** box, type a URL with the following pattern: `https://<instancename>.atlassian.net`.</span></span>

    ![Atlassian Cloud domain and URLs single sign-on information](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    > [!NOTE]
    > <span data-ttu-id="3f6fa-162">The preceding Sign on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-162">The preceding Sign on URL value is not real.</span></span> <span data-ttu-id="3f6fa-163">Update the value with the actual Sign on URL.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-163">Update the value with the actual Sign on URL.</span></span> <span data-ttu-id="3f6fa-164">Contact [Atlassian Cloud Client support team](https://support.atlassian.com/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-164">Contact [Atlassian Cloud Client support team](https://support.atlassian.com/) to get this value.</span></span>

5. <span data-ttu-id="3f6fa-165">Under **SAML Signing Certificate**, select **Certificate(Base64)**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-165">Under **SAML Signing Certificate**, select **Certificate(Base64)**, and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png)

6. <span data-ttu-id="3f6fa-167">Your Atlassian Cloud application expects to find the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML Token Attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-167">Your Atlassian Cloud application expects to find the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML Token Attributes configuration.</span></span> 

    <span data-ttu-id="3f6fa-168">By default, the **User Identifier** value is mapped to user.userprincipalname.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-168">By default, the **User Identifier** value is mapped to user.userprincipalname.</span></span> <span data-ttu-id="3f6fa-169">Change this value to map to user.mail.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-169">Change this value to map to user.mail.</span></span> <span data-ttu-id="3f6fa-170">You can also choose any other appropriate value according to your organization's setup but, in most of the cases, email should work.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-170">You can also choose any other appropriate value according to your organization's setup but, in most of the cases, email should work.</span></span>

    ![The Certificate download link](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_attribute.png)

7. <span data-ttu-id="3f6fa-172">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-172">Select **Save**.</span></span>

    ![The Configure single sign-on Save button](./media/atlassian-cloud-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3f6fa-174">To open the **Configure sign-on** window, in the **Atlassian Cloud Configuration** section, select **Configure Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-174">To open the **Configure sign-on** window, in the **Atlassian Cloud Configuration** section, select **Configure Atlassian Cloud**.</span></span>

9. <span data-ttu-id="3f6fa-175">In the **Quick Reference** section, copy the **SAML Entity ID** and **SAML Single Sign-On Service URL**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-175">In the **Quick Reference** section, copy the **SAML Entity ID** and **SAML Single Sign-On Service URL**.</span></span>

    ![Atlassian Cloud configuration](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png)

10. <span data-ttu-id="3f6fa-177">To get SSO configured for your application, sign in to the Atlassian portal with administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-177">To get SSO configured for your application, sign in to the Atlassian portal with administrator credentials.</span></span>

11. <span data-ttu-id="3f6fa-178">You need to verify your domain before going to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-178">You need to verify your domain before going to configure single sign-on.</span></span> <span data-ttu-id="3f6fa-179">For more information, see [Atlassian domain verification](https://confluence.atlassian.com/cloud/domain-verification-873871234.html) document.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-179">For more information, see [Atlassian domain verification](https://confluence.atlassian.com/cloud/domain-verification-873871234.html) document.</span></span>

12. <span data-ttu-id="3f6fa-180">In the left pane, select **SAML single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-180">In the left pane, select **SAML single sign-on**.</span></span> <span data-ttu-id="3f6fa-181">If you haven't already done so, subscribe to Atlassian Identity Manager.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-181">If you haven't already done so, subscribe to Atlassian Identity Manager.</span></span>

    ![Configure single sign-on](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

13. <span data-ttu-id="3f6fa-183">In the **Add SAML configuration** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-183">In the **Add SAML configuration** window, do the following:</span></span>

    ![Configure single sign-on](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="3f6fa-185">a.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-185">a.</span></span> <span data-ttu-id="3f6fa-186">In the **Identity provider Entity ID** box, paste the SAML entity ID that you copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-186">In the **Identity provider Entity ID** box, paste the SAML entity ID that you copied from the Azure portal.</span></span>

    <span data-ttu-id="3f6fa-187">b.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-187">b.</span></span> <span data-ttu-id="3f6fa-188">In the **Identity provider SSO URL** box, paste the SAML single sign-on service URL that you copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-188">In the **Identity provider SSO URL** box, paste the SAML single sign-on service URL that you copied from the Azure portal.</span></span>

    <span data-ttu-id="3f6fa-189">c.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-189">c.</span></span> <span data-ttu-id="3f6fa-190">Open the downloaded certificate from the Azure portal in a .txt file, copy the value (without the *Begin Certificate* and *End Certificate* lines), and then paste it in the **Public X509 certificate** box.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-190">Open the downloaded certificate from the Azure portal in a .txt file, copy the value (without the *Begin Certificate* and *End Certificate* lines), and then paste it in the **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="3f6fa-191">d.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-191">d.</span></span> <span data-ttu-id="3f6fa-192">Select **Save Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-192">Select **Save Configuration**.</span></span>
     
14. <span data-ttu-id="3f6fa-193">To ensure that you have set up the correct URLs, update the Azure AD settings by doing the following:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-193">To ensure that you have set up the correct URLs, update the Azure AD settings by doing the following:</span></span>

    ![Configure single sign-on](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)

    <span data-ttu-id="3f6fa-195">a.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-195">a.</span></span> <span data-ttu-id="3f6fa-196">In the SAML window, copy the **SP Identity ID** and then, in the Azure portal, under Atlassian Cloud **Domain and URLs**, paste it in the **Identifier** box.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-196">In the SAML window, copy the **SP Identity ID** and then, in the Azure portal, under Atlassian Cloud **Domain and URLs**, paste it in the **Identifier** box.</span></span>
    
    <span data-ttu-id="3f6fa-197">b.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-197">b.</span></span> <span data-ttu-id="3f6fa-198">In the SAML window, copy the **SP Assertion Consumer Service URL** and then, in the Azure portal, under Atlassian Cloud **Domain and URLs**, paste it in the **Reply URL** box.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-198">In the SAML window, copy the **SP Assertion Consumer Service URL** and then, in the Azure portal, under Atlassian Cloud **Domain and URLs**, paste it in the **Reply URL** box.</span></span> <span data-ttu-id="3f6fa-199">The sign-on URL is the tenant URL of your Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-199">The sign-on URL is the tenant URL of your Atlassian Cloud.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3f6fa-200">If you're an existing customer, after you update the **SP Identity ID** and **SP Assertion Consumer Service URL** values in the Azure portal, select **Yes, update configuration**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-200">If you're an existing customer, after you update the **SP Identity ID** and **SP Assertion Consumer Service URL** values in the Azure portal, select **Yes, update configuration**.</span></span> <span data-ttu-id="3f6fa-201">If you're a new customer, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-201">If you're a new customer, you can skip this step.</span></span>
    
15. <span data-ttu-id="3f6fa-202">In the Azure portal, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-202">In the Azure portal, select **Save**.</span></span>

    ![Configure single sign-on](./media/atlassian-cloud-tutorial/tutorial_general_400.png)

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3f6fa-204">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3f6fa-204">Create an Azure AD test user</span></span>

<span data-ttu-id="3f6fa-205">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-205">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

   ![Create an Azure AD test user][100]

1. <span data-ttu-id="3f6fa-207">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-207">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/atlassian-cloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3f6fa-209">To display the list of users, select **Users and groups** > **All users**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-209">To display the list of users, select **Users and groups** > **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/atlassian-cloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3f6fa-211">In the **All Users** window, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-211">In the **All Users** window, select **Add**.</span></span>

    ![The Add button](./media/atlassian-cloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3f6fa-213">In the **User** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-213">In the **User** window, do the following:</span></span>

    ![The User window](./media/atlassian-cloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3f6fa-215">a.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-215">a.</span></span> <span data-ttu-id="3f6fa-216">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-216">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f6fa-217">b.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-217">b.</span></span> <span data-ttu-id="3f6fa-218">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-218">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3f6fa-219">c.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-219">c.</span></span> <span data-ttu-id="3f6fa-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3f6fa-221">d.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-221">d.</span></span> <span data-ttu-id="3f6fa-222">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-222">Select **Create**.</span></span>

### <a name="create-an-atlassian-cloud-test-user"></a><span data-ttu-id="3f6fa-223">Create an Atlassian Cloud test user</span><span class="sxs-lookup"><span data-stu-id="3f6fa-223">Create an Atlassian Cloud test user</span></span>

<span data-ttu-id="3f6fa-224">To enable Azure AD users to sign in to Atlassian Cloud, provision the user accounts manually in Atlassian Cloud by doing the following:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-224">To enable Azure AD users to sign in to Atlassian Cloud, provision the user accounts manually in Atlassian Cloud by doing the following:</span></span>

1. <span data-ttu-id="3f6fa-225">In the **Administration** pane, select **Users**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-225">In the **Administration** pane, select **Users**.</span></span>

    ![The Atlassian Cloud Users link](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png)

2. <span data-ttu-id="3f6fa-227">To create a user in Atlassian Cloud, select **Invite user**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-227">To create a user in Atlassian Cloud, select **Invite user**.</span></span>

    ![Create an Atlassian Cloud user](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png)

3. <span data-ttu-id="3f6fa-229">In the **Email address** box, enter the user's email address, and then assign the application access.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-229">In the **Email address** box, enter the user's email address, and then assign the application access.</span></span>

    ![Create an Atlassian Cloud user](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)

4. <span data-ttu-id="3f6fa-231">To send an email invitation to the user, select **Invite users**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-231">To send an email invitation to the user, select **Invite users**.</span></span> <span data-ttu-id="3f6fa-232">An email invitation is sent to the user and, after accepting the invitation, the user is active in the system.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-232">An email invitation is sent to the user and, after accepting the invitation, the user is active in the system.</span></span>

>[!NOTE]
><span data-ttu-id="3f6fa-233">You can also bulk-create users by selecting the **Bulk Create** button in the **Users** section.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-233">You can also bulk-create users by selecting the **Bulk Create** button in the **Users** section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3f6fa-234">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3f6fa-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="3f6fa-235">In this section, you enable user Britta Simon to use Azure single sign-on by granting access to Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-235">In this section, you enable user Britta Simon to use Azure single sign-on by granting access to Atlassian Cloud.</span></span> <span data-ttu-id="3f6fa-236">To do so, do the following:</span><span class="sxs-lookup"><span data-stu-id="3f6fa-236">To do so, do the following:</span></span>

![Assign the user role][200]

1. <span data-ttu-id="3f6fa-238">In the Azure portal, open the **Applications** view, go to the directory view, and then select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-238">In the Azure portal, open the **Applications** view, go to the directory view, and then select **Enterprise applications** > **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="3f6fa-240">In the **Applications** list, select **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-240">In the **Applications** list, select **Atlassian Cloud**.</span></span>

    ![The Atlassian Cloud link in the Applications list](./media/atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png)

3. <span data-ttu-id="3f6fa-242">In the left pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-242">In the left pane, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="3f6fa-244">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-244">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="3f6fa-246">In the **Users and groups** window, in the **Users** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-246">In the **Users and groups** window, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="3f6fa-247">In the **Users and groups** window, select **Select**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-247">In the **Users and groups** window, select **Select**.</span></span>

7. <span data-ttu-id="3f6fa-248">In the **Add Assignment** window, select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-248">In the **Add Assignment** window, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3f6fa-249">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3f6fa-249">Test single sign-on</span></span>

<span data-ttu-id="3f6fa-250">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-250">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="3f6fa-251">When you select the **Atlassian Cloud** tile in the Access Panel, you should be signed on automatically to your Atlassian Cloud application.</span><span class="sxs-lookup"><span data-stu-id="3f6fa-251">When you select the **Atlassian Cloud** tile in the Access Panel, you should be signed on automatically to your Atlassian Cloud application.</span></span>
<span data-ttu-id="3f6fa-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3f6fa-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3f6fa-253">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3f6fa-253">Additional resources</span></span>

* [<span data-ttu-id="3f6fa-254">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f6fa-254">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3f6fa-255">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3f6fa-255">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/atlassian-cloud-tutorial/tutorial_general_203.png
