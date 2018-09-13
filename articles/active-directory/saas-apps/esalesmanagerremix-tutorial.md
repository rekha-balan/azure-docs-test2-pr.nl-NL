---
title: 'Tutorial: Azure Active Directory integration with E Sales Manager Remix | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and E Sales Manager Remix.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 89b5022c-0d5b-4103-9877-ddd32b6e1c02
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2018
ms.author: jeedes
ms.openlocfilehash: d96fd1eacc98e88dc8578b259781cc661cf85933
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866877"
---
# <a name="integrate-azure-active-directory-with-e-sales-manager-remix"></a><span data-ttu-id="67a40-103">Integrate Azure Active Directory with E Sales Manager Remix</span><span class="sxs-lookup"><span data-stu-id="67a40-103">Integrate Azure Active Directory with E Sales Manager Remix</span></span>

<span data-ttu-id="67a40-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with E Sales Manager Remix.</span><span class="sxs-lookup"><span data-stu-id="67a40-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with E Sales Manager Remix.</span></span>

<span data-ttu-id="67a40-105">By integrating Azure AD with E Sales Manager Remix, you get the following benefits:</span><span class="sxs-lookup"><span data-stu-id="67a40-105">By integrating Azure AD with E Sales Manager Remix, you get the following benefits:</span></span>

- <span data-ttu-id="67a40-106">You can control in Azure AD who has access to E Sales Manager Remix.</span><span class="sxs-lookup"><span data-stu-id="67a40-106">You can control in Azure AD who has access to E Sales Manager Remix.</span></span>
- <span data-ttu-id="67a40-107">You can enable your users to get signed in automatically to E Sales Manager Remix (single sign-on, or SSO) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="67a40-107">You can enable your users to get signed in automatically to E Sales Manager Remix (single sign-on, or SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="67a40-108">You can manage your accounts in one central location, the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="67a40-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="67a40-109">To learn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="67a40-109">To learn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67a40-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="67a40-110">Prerequisites</span></span>

<span data-ttu-id="67a40-111">To configure Azure AD integration with E Sales Manager Remix, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="67a40-111">To configure Azure AD integration with E Sales Manager Remix, you need the following items:</span></span>

- <span data-ttu-id="67a40-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="67a40-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67a40-113">An E Sales Manager Remix SSO-enabled subscription</span><span class="sxs-lookup"><span data-stu-id="67a40-113">An E Sales Manager Remix SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67a40-114">When you test the steps in this tutorial, we recommend that you do *not* use a production environment.</span><span class="sxs-lookup"><span data-stu-id="67a40-114">When you test the steps in this tutorial, we recommend that you do *not* use a production environment.</span></span>

<span data-ttu-id="67a40-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="67a40-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="67a40-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="67a40-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67a40-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67a40-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67a40-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="67a40-118">Scenario description</span></span>
<span data-ttu-id="67a40-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="67a40-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="67a40-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="67a40-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="67a40-121">Adding E Sales Manager Remix from the gallery</span><span class="sxs-lookup"><span data-stu-id="67a40-121">Adding E Sales Manager Remix from the gallery</span></span>
* <span data-ttu-id="67a40-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="67a40-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-e-sales-manager-remix-from-the-gallery"></a><span data-ttu-id="67a40-123">Add E Sales Manager Remix from the gallery</span><span class="sxs-lookup"><span data-stu-id="67a40-123">Add E Sales Manager Remix from the gallery</span></span>
<span data-ttu-id="67a40-124">To configure the integration of Azure AD with E Sales Manager Remix, add E Sales Manager Remix from the gallery to your list of managed SaaS apps by doing the following:</span><span class="sxs-lookup"><span data-stu-id="67a40-124">To configure the integration of Azure AD with E Sales Manager Remix, add E Sales Manager Remix from the gallery to your list of managed SaaS apps by doing the following:</span></span>

1. <span data-ttu-id="67a40-125">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="67a40-125">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="67a40-127">Select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="67a40-127">Select **Enterprise applications** > **All applications**.</span></span>

    ![The "Enterprise applications" window][2]
    
1. <span data-ttu-id="67a40-129">To add a new application, select **New application** at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="67a40-129">To add a new application, select **New application** at the top of the window.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="67a40-131">In the search box, type **E Sales Manager Remix**, select **E Sales Manager Remix** in the results list, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="67a40-131">In the search box, type **E Sales Manager Remix**, select **E Sales Manager Remix** in the results list, and then select **Add**.</span></span>

    ![E Sales Manager Remix in the results list](./media/esalesmanagerremix-tutorial/tutorial_esalesmanagerremix_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="67a40-133">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="67a40-133">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="67a40-134">In this section, you configure and test Azure AD single sign-on with E Sales Manager Remix, based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="67a40-134">In this section, you configure and test Azure AD single sign-on with E Sales Manager Remix, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="67a40-135">For single sign-on to work, Azure AD needs to identify the E Sales Manager Remix user and its counterpart in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67a40-135">For single sign-on to work, Azure AD needs to identify the E Sales Manager Remix user and its counterpart in Azure AD.</span></span> <span data-ttu-id="67a40-136">In other words, a link relationship between an Azure AD user and the same user in E Sales Manager Remix must be established.</span><span class="sxs-lookup"><span data-stu-id="67a40-136">In other words, a link relationship between an Azure AD user and the same user in E Sales Manager Remix must be established.</span></span>

<span data-ttu-id="67a40-137">To configure and test Azure AD single sign-on with E Sales Manager Remix, complete the building blocks in the next five sections:</span><span class="sxs-lookup"><span data-stu-id="67a40-137">To configure and test Azure AD single sign-on with E Sales Manager Remix, complete the building blocks in the next five sections:</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="67a40-138">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="67a40-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="67a40-139">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your E Sales Manager Remix application by doing the following:</span><span class="sxs-lookup"><span data-stu-id="67a40-139">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your E Sales Manager Remix application by doing the following:</span></span>

1. <span data-ttu-id="67a40-140">In the Azure portal, on the **E Sales Manager Remix** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="67a40-140">In the Azure portal, on the **E Sales Manager Remix** application integration page, select **Single sign-on**.</span></span>

    ![The "Single sign-on" link][4]

1. <span data-ttu-id="67a40-142">In the **Single sign-on** window, in the **Single Sign-on Mode** box, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="67a40-142">In the **Single sign-on** window, in the **Single Sign-on Mode** box, select **SAML-based Sign-on**.</span></span>
 
    ![The "Single sign-on" window](./media/esalesmanagerremix-tutorial/tutorial_esalesmanagerremix_samlbase.png)

1. <span data-ttu-id="67a40-144">Under **E Sales Manager Remix Domain and URLs**, do the following:</span><span class="sxs-lookup"><span data-stu-id="67a40-144">Under **E Sales Manager Remix Domain and URLs**, do the following:</span></span>

    ![E Sales Manager Remix Domain and URLs single sign-on information](./media/esalesmanagerremix-tutorial/tutorial_esalesmanagerremix_url.png)

    <span data-ttu-id="67a40-146">a.</span><span class="sxs-lookup"><span data-stu-id="67a40-146">a.</span></span> <span data-ttu-id="67a40-147">In the **Sign-on URL** box, type a URL in the following format: *https://\<Server-Based-URL>/\<sub-domain>/esales-pc*.</span><span class="sxs-lookup"><span data-stu-id="67a40-147">In the **Sign-on URL** box, type a URL in the following format: *https://\<Server-Based-URL>/\<sub-domain>/esales-pc*.</span></span>

    <span data-ttu-id="67a40-148">b.</span><span class="sxs-lookup"><span data-stu-id="67a40-148">b.</span></span> <span data-ttu-id="67a40-149">In the **Identifier** box, type a URL in the following format: *https://\<Server-Based-URL>/\<sub-domain>/*.</span><span class="sxs-lookup"><span data-stu-id="67a40-149">In the **Identifier** box, type a URL in the following format: *https://\<Server-Based-URL>/\<sub-domain>/*.</span></span>

    <span data-ttu-id="67a40-150">c.</span><span class="sxs-lookup"><span data-stu-id="67a40-150">c.</span></span> <span data-ttu-id="67a40-151">Note the **Identifier** value for later use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="67a40-151">Note the **Identifier** value for later use in this tutorial.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="67a40-152">The preceding values are not real.</span><span class="sxs-lookup"><span data-stu-id="67a40-152">The preceding values are not real.</span></span> <span data-ttu-id="67a40-153">Update them with the actual sign-in URL and identifier.</span><span class="sxs-lookup"><span data-stu-id="67a40-153">Update them with the actual sign-in URL and identifier.</span></span> <span data-ttu-id="67a40-154">To obtain the values, contact [E Sales Manager Remix Client support team](mailto:esupport@softbrain.co.jp).</span><span class="sxs-lookup"><span data-stu-id="67a40-154">To obtain the values, contact [E Sales Manager Remix Client support team](mailto:esupport@softbrain.co.jp).</span></span>

1. <span data-ttu-id="67a40-155">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="67a40-155">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![The Certificate (Base64) download link](./media/esalesmanagerremix-tutorial/tutorial_esalesmanagerremix_certificate.png) 

1. <span data-ttu-id="67a40-157">Select the **View and edit all other user attributes** check box, and then select the **emailaddress** attribute.</span><span class="sxs-lookup"><span data-stu-id="67a40-157">Select the **View and edit all other user attributes** check box, and then select the **emailaddress** attribute.</span></span>
    
    ![The User Attributes window](./media/esalesmanagerremix-tutorial/configure1.png)

    <span data-ttu-id="67a40-159">The **Edit Attribute** window opens.</span><span class="sxs-lookup"><span data-stu-id="67a40-159">The **Edit Attribute** window opens.</span></span>

1. <span data-ttu-id="67a40-160">Copy the **Namespace** and **Name** values.</span><span class="sxs-lookup"><span data-stu-id="67a40-160">Copy the **Namespace** and **Name** values.</span></span> <span data-ttu-id="67a40-161">Generate the value in the pattern *\<Namespace>/\<Name>*, and save it for later use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="67a40-161">Generate the value in the pattern *\<Namespace>/\<Name>*, and save it for later use in this tutorial.</span></span>

    ![The Edit Attribute window](./media/esalesmanagerremix-tutorial/configure2.png)

1. <span data-ttu-id="67a40-163">Under **E Sales Manager Remix Configuration**, select **Configure E Sales Manager Remix**.</span><span class="sxs-lookup"><span data-stu-id="67a40-163">Under **E Sales Manager Remix Configuration**, select **Configure E Sales Manager Remix**.</span></span>

    ![E Sales Manager Remix Configuration](./media/esalesmanagerremix-tutorial/tutorial_esalesmanagerremix_configure.png) 

    <span data-ttu-id="67a40-165">The **Configure sign-on** window opens.</span><span class="sxs-lookup"><span data-stu-id="67a40-165">The **Configure sign-on** window opens.</span></span>

1. <span data-ttu-id="67a40-166">In the **Quick Reference** section, copy the sign-out URL and the SAML single sign-on service URL.</span><span class="sxs-lookup"><span data-stu-id="67a40-166">In the **Quick Reference** section, copy the sign-out URL and the SAML single sign-on service URL.</span></span>

1. <span data-ttu-id="67a40-167">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="67a40-167">Select **Save**.</span></span>

    ![The Save button](./media/esalesmanagerremix-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="67a40-169">Sign in to your E Sales Manager Remix application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="67a40-169">Sign in to your E Sales Manager Remix application as an administrator.</span></span>

1. <span data-ttu-id="67a40-170">At the top right, select **To Administrator Menu**.</span><span class="sxs-lookup"><span data-stu-id="67a40-170">At the top right, select **To Administrator Menu**.</span></span>

    ![The "To Administrator Menu" command](./media/esalesmanagerremix-tutorial/configure4.png)

1. <span data-ttu-id="67a40-172">In the left pane, select **System settings** > **Cooperation with external system**.</span><span class="sxs-lookup"><span data-stu-id="67a40-172">In the left pane, select **System settings** > **Cooperation with external system**.</span></span>

    ![The "System settings" and "Cooperation with external system" links](./media/esalesmanagerremix-tutorial/configure5.png)
    
1. <span data-ttu-id="67a40-174">In the **Cooperation with external system** window, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="67a40-174">In the **Cooperation with external system** window, select **SAML**.</span></span>

    ![The "Cooperation with external system" window](./media/esalesmanagerremix-tutorial/configure6.png)

1. <span data-ttu-id="67a40-176">Under **SAML authentication setting**, do the following:</span><span class="sxs-lookup"><span data-stu-id="67a40-176">Under **SAML authentication setting**, do the following:</span></span>

    ![The "SAML authentication setting" section](./media/esalesmanagerremix-tutorial/configure3.png)
    
    <span data-ttu-id="67a40-178">a.</span><span class="sxs-lookup"><span data-stu-id="67a40-178">a.</span></span> <span data-ttu-id="67a40-179">Select the **PC version** check box.</span><span class="sxs-lookup"><span data-stu-id="67a40-179">Select the **PC version** check box.</span></span>
    
    <span data-ttu-id="67a40-180">b.</span><span class="sxs-lookup"><span data-stu-id="67a40-180">b.</span></span> <span data-ttu-id="67a40-181">In the **Collaboration item** section, in the drop-down list, select **email**.</span><span class="sxs-lookup"><span data-stu-id="67a40-181">In the **Collaboration item** section, in the drop-down list, select **email**.</span></span>

    <span data-ttu-id="67a40-182">c.</span><span class="sxs-lookup"><span data-stu-id="67a40-182">c.</span></span> <span data-ttu-id="67a40-183">In the **Collaboration item** box, paste the claim value that you copied earlier from the Azure portal (that is, **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="67a40-183">In the **Collaboration item** box, paste the claim value that you copied earlier from the Azure portal (that is, **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**).</span></span>

    <span data-ttu-id="67a40-184">d.</span><span class="sxs-lookup"><span data-stu-id="67a40-184">d.</span></span> <span data-ttu-id="67a40-185">In the **Issuer (entity ID)** box, paste the identifier value that you copied earlier from the **E Sales Manager Remix Domain and URLs** section of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="67a40-185">In the **Issuer (entity ID)** box, paste the identifier value that you copied earlier from the **E Sales Manager Remix Domain and URLs** section of the Azure portal.</span></span>

    <span data-ttu-id="67a40-186">e.</span><span class="sxs-lookup"><span data-stu-id="67a40-186">e.</span></span> <span data-ttu-id="67a40-187">To upload your downloaded certificate from the Azure portal, select **File selection**.</span><span class="sxs-lookup"><span data-stu-id="67a40-187">To upload your downloaded certificate from the Azure portal, select **File selection**.</span></span>

    <span data-ttu-id="67a40-188">f.</span><span class="sxs-lookup"><span data-stu-id="67a40-188">f.</span></span> <span data-ttu-id="67a40-189">In the **ID provider login URL** box, paste the SAML single sign-on service URL that you copied earlier in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="67a40-189">In the **ID provider login URL** box, paste the SAML single sign-on service URL that you copied earlier in the Azure portal.</span></span>

    <span data-ttu-id="67a40-190">g.</span><span class="sxs-lookup"><span data-stu-id="67a40-190">g.</span></span> <span data-ttu-id="67a40-191">In **Identity Provider Logout URL** box, paste the sign-out URL value that you copied earlier in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="67a40-191">In **Identity Provider Logout URL** box, paste the sign-out URL value that you copied earlier in the Azure portal.</span></span>

    <span data-ttu-id="67a40-192">h.</span><span class="sxs-lookup"><span data-stu-id="67a40-192">h.</span></span> <span data-ttu-id="67a40-193">Select **Setting complete**.</span><span class="sxs-lookup"><span data-stu-id="67a40-193">Select **Setting complete**.</span></span>

> [!TIP]
> <span data-ttu-id="67a40-194">As you're setting up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67a40-194">As you're setting up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="67a40-195">After you've added the app in the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation in the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="67a40-195">After you've added the app in the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation in the **Configuration** section at the bottom.</span></span> <span data-ttu-id="67a40-196">For more information about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="67a40-196">For more information about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="67a40-197">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="67a40-197">Create an Azure AD test user</span></span>

<span data-ttu-id="67a40-198">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span><span class="sxs-lookup"><span data-stu-id="67a40-198">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Create an Azure AD test user][100]

1. <span data-ttu-id="67a40-200">In the Azure portal, in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="67a40-200">In the Azure portal, in the left pane, select **Azure Active Directory**.</span></span>

    ![The Azure Active Directory link](./media/paloaltoadmin-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="67a40-202">To display a list of current users, select **Users and groups** > **All users**.</span><span class="sxs-lookup"><span data-stu-id="67a40-202">To display a list of current users, select **Users and groups** > **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/paloaltoadmin-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="67a40-204">At the top of the **All Users** window, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="67a40-204">At the top of the **All Users** window, select **Add**.</span></span>

    ![The Add button](./media/paloaltoadmin-tutorial/create_aaduser_03.png)
    
    <span data-ttu-id="67a40-206">The **User** window opens.</span><span class="sxs-lookup"><span data-stu-id="67a40-206">The **User** window opens.</span></span>

1. <span data-ttu-id="67a40-207">In the **User** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="67a40-207">In the **User** window, do the following:</span></span>

    ![The User window](./media/paloaltoadmin-tutorial/create_aaduser_04.png)

    <span data-ttu-id="67a40-209">a.</span><span class="sxs-lookup"><span data-stu-id="67a40-209">a.</span></span> <span data-ttu-id="67a40-210">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="67a40-210">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67a40-211">b.</span><span class="sxs-lookup"><span data-stu-id="67a40-211">b.</span></span> <span data-ttu-id="67a40-212">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67a40-212">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="67a40-213">c.</span><span class="sxs-lookup"><span data-stu-id="67a40-213">c.</span></span> <span data-ttu-id="67a40-214">Select the **Show Password** check box, and then note the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="67a40-214">Select the **Show Password** check box, and then note the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="67a40-215">d.</span><span class="sxs-lookup"><span data-stu-id="67a40-215">d.</span></span> <span data-ttu-id="67a40-216">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="67a40-216">Select **Create**.</span></span>
 
### <a name="create-an-e-sales-manager-remix-test-user"></a><span data-ttu-id="67a40-217">Create an E Sales Manager Remix test user</span><span class="sxs-lookup"><span data-stu-id="67a40-217">Create an E Sales Manager Remix test user</span></span>

1. <span data-ttu-id="67a40-218">Sign on to your E Sales Manager Remix application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="67a40-218">Sign on to your E Sales Manager Remix application as an administrator.</span></span>

1. <span data-ttu-id="67a40-219">Select **To Administrator Menu** from the menu at the top right.</span><span class="sxs-lookup"><span data-stu-id="67a40-219">Select **To Administrator Menu** from the menu at the top right.</span></span>

    ![E Sales Manager Remix Configuration](./media/esalesmanagerremix-tutorial/configure4.png)

1. <span data-ttu-id="67a40-221">Select **Your company's settings** > **Maintenance of departments and employees**, and then select **Employees registered**.</span><span class="sxs-lookup"><span data-stu-id="67a40-221">Select **Your company's settings** > **Maintenance of departments and employees**, and then select **Employees registered**.</span></span>

    ![The "Employees registered" tab](./media/esalesmanagerremix-tutorial/user1.png)

1. <span data-ttu-id="67a40-223">In the **New employee registration** section, do the following:</span><span class="sxs-lookup"><span data-stu-id="67a40-223">In the **New employee registration** section, do the following:</span></span>
    
    ![The "New employee registration" section](./media/esalesmanagerremix-tutorial/user2.png)

    <span data-ttu-id="67a40-225">a.</span><span class="sxs-lookup"><span data-stu-id="67a40-225">a.</span></span> <span data-ttu-id="67a40-226">In the **Employee Name** box, type the name of the user (for example, **Britta**).</span><span class="sxs-lookup"><span data-stu-id="67a40-226">In the **Employee Name** box, type the name of the user (for example, **Britta**).</span></span>

    <span data-ttu-id="67a40-227">b.</span><span class="sxs-lookup"><span data-stu-id="67a40-227">b.</span></span> <span data-ttu-id="67a40-228">Complete the remaining required fields.</span><span class="sxs-lookup"><span data-stu-id="67a40-228">Complete the remaining required fields.</span></span>
    
    <span data-ttu-id="67a40-229">c.</span><span class="sxs-lookup"><span data-stu-id="67a40-229">c.</span></span> <span data-ttu-id="67a40-230">If you enable SAML, the administrator cannot sign in from the sign-in page.</span><span class="sxs-lookup"><span data-stu-id="67a40-230">If you enable SAML, the administrator cannot sign in from the sign-in page.</span></span> <span data-ttu-id="67a40-231">Grant administrator sign-in privileges to the user by selecting the **Admin Login** check box.</span><span class="sxs-lookup"><span data-stu-id="67a40-231">Grant administrator sign-in privileges to the user by selecting the **Admin Login** check box.</span></span>

    <span data-ttu-id="67a40-232">d.</span><span class="sxs-lookup"><span data-stu-id="67a40-232">d.</span></span> <span data-ttu-id="67a40-233">Select **Registration**.</span><span class="sxs-lookup"><span data-stu-id="67a40-233">Select **Registration**.</span></span>

1. <span data-ttu-id="67a40-234">In the future, to sign in as an administrator, sign in as the user who has administrator permissions and then, at the top right, select **To Administrator Menu**.</span><span class="sxs-lookup"><span data-stu-id="67a40-234">In the future, to sign in as an administrator, sign in as the user who has administrator permissions and then, at the top right, select **To Administrator Menu**.</span></span>

    ![The "To Administrator Menu" command](./media/esalesmanagerremix-tutorial/configure4.png)

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="67a40-236">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="67a40-236">Assign the Azure AD test user</span></span>

<span data-ttu-id="67a40-237">In this section, you enable user Britta Simon to use Azure single sign-on by granting access to E Sales Manager Remix.</span><span class="sxs-lookup"><span data-stu-id="67a40-237">In this section, you enable user Britta Simon to use Azure single sign-on by granting access to E Sales Manager Remix.</span></span> <span data-ttu-id="67a40-238">To do so, do the following:</span><span class="sxs-lookup"><span data-stu-id="67a40-238">To do so, do the following:</span></span> 

![Assign the user role][200] 

1. <span data-ttu-id="67a40-240">In the Azure portal, open the **Applications** view, go to the **Directory** view, and then select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="67a40-240">In the Azure portal, open the **Applications** view, go to the **Directory** view, and then select **Enterprise applications** > **All applications**.</span></span>

    ![The "Enterprise applications" and "All applications" links][201] 

1. <span data-ttu-id="67a40-242">In the **Applications** list, select **E Sales Manager Remix**.</span><span class="sxs-lookup"><span data-stu-id="67a40-242">In the **Applications** list, select **E Sales Manager Remix**.</span></span>

    ![The E Sales Manager Remix link](./media/esalesmanagerremix-tutorial/tutorial_esalesmanagerremix_app.png)  

1. <span data-ttu-id="67a40-244">In the left pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="67a40-244">In the left pane, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="67a40-246">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="67a40-246">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="67a40-248">In the **Users and groups** window, in the **Users** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="67a40-248">In the **Users and groups** window, in the **Users** list, select **Britta Simon**.</span></span>

1. <span data-ttu-id="67a40-249">Select the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="67a40-249">Select the **Select** button.</span></span>

1. <span data-ttu-id="67a40-250">In the **Add Assignment** window, select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="67a40-250">In the **Add Assignment** window, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="67a40-251">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="67a40-251">Test single sign-on</span></span>

<span data-ttu-id="67a40-252">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="67a40-252">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="67a40-253">When you select the E Sales Manager Remix tile in the Access Panel, you should be signed in automatically to your E Sales Manager Remix application.</span><span class="sxs-lookup"><span data-stu-id="67a40-253">When you select the E Sales Manager Remix tile in the Access Panel, you should be signed in automatically to your E Sales Manager Remix application.</span></span>

<span data-ttu-id="67a40-254">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="67a40-254">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="67a40-255">Additional resources</span><span class="sxs-lookup"><span data-stu-id="67a40-255">Additional resources</span></span>

* [<span data-ttu-id="67a40-256">List of tutorials about integrating SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67a40-256">List of tutorials about integrating SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="67a40-257">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="67a40-257">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/esalesmanagerremix-tutorial/tutorial_general_01.png
[2]: ./media/esalesmanagerremix-tutorial/tutorial_general_02.png
[3]: ./media/esalesmanagerremix-tutorial/tutorial_general_03.png
[4]: ./media/esalesmanagerremix-tutorial/tutorial_general_04.png

[100]: ./media/esalesmanagerremix-tutorial/tutorial_general_100.png

[200]: ./media/esalesmanagerremix-tutorial/tutorial_general_200.png
[201]: ./media/esalesmanagerremix-tutorial/tutorial_general_201.png
[202]: ./media/esalesmanagerremix-tutorial/tutorial_general_202.png
[203]: ./media/esalesmanagerremix-tutorial/tutorial_general_203.png

