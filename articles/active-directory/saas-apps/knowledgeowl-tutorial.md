---
title: 'Tutorial: Azure Active Directory integration with KnowledgeOwl | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and KnowledgeOwl.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2ae30996-864d-4872-90bc-f770e1ea159a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2018
ms.author: jeedes
ms.openlocfilehash: e902f5969611dd3b1074e899003abe5067857c04
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866109"
---
# <a name="tutorial-azure-active-directory-integration-with-knowledgeowl"></a><span data-ttu-id="309e2-103">Tutorial: Azure Active Directory integration with KnowledgeOwl</span><span class="sxs-lookup"><span data-stu-id="309e2-103">Tutorial: Azure Active Directory integration with KnowledgeOwl</span></span>

<span data-ttu-id="309e2-104">In this tutorial, you learn how to integrate KnowledgeOwl with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="309e2-104">In this tutorial, you learn how to integrate KnowledgeOwl with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="309e2-105">Integrating KnowledgeOwl with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="309e2-105">Integrating KnowledgeOwl with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="309e2-106">You can control in Azure AD who has access to KnowledgeOwl.</span><span class="sxs-lookup"><span data-stu-id="309e2-106">You can control in Azure AD who has access to KnowledgeOwl.</span></span>
- <span data-ttu-id="309e2-107">You can enable your users to automatically get signed-on to KnowledgeOwl (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="309e2-107">You can enable your users to automatically get signed-on to KnowledgeOwl (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="309e2-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="309e2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="309e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="309e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="309e2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="309e2-110">Prerequisites</span></span>

<span data-ttu-id="309e2-111">To configure Azure AD integration with KnowledgeOwl, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="309e2-111">To configure Azure AD integration with KnowledgeOwl, you need the following items:</span></span>

- <span data-ttu-id="309e2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="309e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="309e2-113">A KnowledgeOwl single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="309e2-113">A KnowledgeOwl single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="309e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="309e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="309e2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="309e2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="309e2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="309e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="309e2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="309e2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="309e2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="309e2-118">Scenario description</span></span>
<span data-ttu-id="309e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="309e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="309e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="309e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="309e2-121">Adding KnowledgeOwl from the gallery</span><span class="sxs-lookup"><span data-stu-id="309e2-121">Adding KnowledgeOwl from the gallery</span></span>
1. <span data-ttu-id="309e2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="309e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowledgeowl-from-the-gallery"></a><span data-ttu-id="309e2-123">Adding KnowledgeOwl from the gallery</span><span class="sxs-lookup"><span data-stu-id="309e2-123">Adding KnowledgeOwl from the gallery</span></span>
<span data-ttu-id="309e2-124">To configure the integration of KnowledgeOwl into Azure AD, you need to add KnowledgeOwl from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="309e2-124">To configure the integration of KnowledgeOwl into Azure AD, you need to add KnowledgeOwl from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="309e2-125">**To add KnowledgeOwl from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="309e2-125">**To add KnowledgeOwl from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="309e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="309e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="309e2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="309e2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="309e2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="309e2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="309e2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="309e2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="309e2-133">In the search box, type **KnowledgeOwl**, select **KnowledgeOwl** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="309e2-133">In the search box, type **KnowledgeOwl**, select **KnowledgeOwl** from result panel then click **Add** button to add the application.</span></span>

    ![KnowledgeOwl in the results list](./media/knowledgeowl-tutorial/tutorial_knowledgeowl_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="309e2-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="309e2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="309e2-136">In this section, you configure and test Azure AD single sign-on with KnowledgeOwl based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="309e2-136">In this section, you configure and test Azure AD single sign-on with KnowledgeOwl based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="309e2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in KnowledgeOwl is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="309e2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in KnowledgeOwl is to a user in Azure AD.</span></span> <span data-ttu-id="309e2-138">In other words, a link relationship between an Azure AD user and the related user in KnowledgeOwl needs to be established.</span><span class="sxs-lookup"><span data-stu-id="309e2-138">In other words, a link relationship between an Azure AD user and the related user in KnowledgeOwl needs to be established.</span></span>

<span data-ttu-id="309e2-139">To configure and test Azure AD single sign-on with KnowledgeOwl, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="309e2-139">To configure and test Azure AD single sign-on with KnowledgeOwl, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="309e2-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="309e2-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="309e2-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="309e2-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="309e2-142">**[Create a KnowledgeOwl test user](#create-a-knowledgeowl-test-user)** - to have a counterpart of Britta Simon in KnowledgeOwl that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="309e2-142">**[Create a KnowledgeOwl test user](#create-a-knowledgeowl-test-user)** - to have a counterpart of Britta Simon in KnowledgeOwl that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="309e2-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="309e2-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="309e2-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="309e2-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="309e2-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="309e2-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="309e2-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your KnowledgeOwl application.</span><span class="sxs-lookup"><span data-stu-id="309e2-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your KnowledgeOwl application.</span></span>

<span data-ttu-id="309e2-147">**To configure Azure AD single sign-on with KnowledgeOwl, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="309e2-147">**To configure Azure AD single sign-on with KnowledgeOwl, perform the following steps:**</span></span>

1. <span data-ttu-id="309e2-148">In the Azure portal, on the **KnowledgeOwl** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="309e2-148">In the Azure portal, on the **KnowledgeOwl** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="309e2-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="309e2-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/knowledgeowl-tutorial/tutorial_knowledgeowl_samlbase.png)

1. <span data-ttu-id="309e2-152">On the **KnowledgeOwl Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="309e2-152">On the **KnowledgeOwl Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![KnowledgeOwl Domain and URLs single sign-on information](./media/knowledgeowl-tutorial/tutorial_knowledgeowl_url.png)

    <span data-ttu-id="309e2-154">a.</span><span class="sxs-lookup"><span data-stu-id="309e2-154">a.</span></span> <span data-ttu-id="309e2-155">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="309e2-155">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern:</span></span>
    |||
    |-|-|
    | `https://app.knowledgeowl.com/sp`|
    | `https://app.knowledgeowl.com/sp/id/<unique ID>`|
    |||

    <span data-ttu-id="309e2-156">b.</span><span class="sxs-lookup"><span data-stu-id="309e2-156">b.</span></span> <span data-ttu-id="309e2-157">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="309e2-157">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    |||
    |-|-|
    | `https://subdomain.knowledgeowl.com/help/saml-login`|
    | `https://subdomain.knowledgeowl.com/docs/saml-login`|
    | `https://subdomain.knowledgeowl.com/home/saml-login`|
    | `https://privatedomain.com/help/saml-login`|
    | `https://privatedomain.com/docs/saml-login`|
    | `https://privatedomain.com/home/saml-login`|
    |||

1. <span data-ttu-id="309e2-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="309e2-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![KnowledgeOwl Domain and URLs single sign-on information](./media/knowledgeowl-tutorial/tutorial_knowledgeowl_url1.png)

    <span data-ttu-id="309e2-160">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="309e2-160">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |||
    |-|-|
    | `https://subdomain.knowledgeowl.com/help/saml-login`|
    | `https://subdomain.knowledgeowl.com/docs/saml-login`|
    | `https://subdomain.knowledgeowl.com/home/saml-login`|
    | `https://privatedomain.com/help/saml-login`|
    | `https://privatedomain.com/docs/saml-login`|
    | `https://privatedomain.com/home/saml-login`|
    |||
     
    > [!NOTE]
    > <span data-ttu-id="309e2-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="309e2-161">These values are not real.</span></span> <span data-ttu-id="309e2-162">You'll need to update these value from actual Identifier, Reply URL, and Sign-On URL which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="309e2-162">You'll need to update these value from actual Identifier, Reply URL, and Sign-On URL which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="309e2-163">The KnowledgeOwl application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="309e2-163">The KnowledgeOwl application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="309e2-164">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="309e2-164">Configure the following claims for this application.</span></span> <span data-ttu-id="309e2-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="309e2-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span>

    ![Configure Single Sign-On](./media/knowledgeowl-tutorial/attribute.png)

1. <span data-ttu-id="309e2-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="309e2-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="309e2-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="309e2-168">Attribute Name</span></span> | <span data-ttu-id="309e2-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="309e2-169">Attribute Value</span></span> | <span data-ttu-id="309e2-170">Namespace</span><span class="sxs-lookup"><span data-stu-id="309e2-170">Namespace</span></span>|
    | ------------------- | -------------------- | -----|
    | <span data-ttu-id="309e2-171">ssoid</span><span class="sxs-lookup"><span data-stu-id="309e2-171">ssoid</span></span> | <span data-ttu-id="309e2-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="309e2-172">user.mail</span></span> | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims`|
    
    <span data-ttu-id="309e2-173">a.</span><span class="sxs-lookup"><span data-stu-id="309e2-173">a.</span></span> <span data-ttu-id="309e2-174">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="309e2-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Configure Single Sign-On](./media/knowledgeowl-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/knowledgeowl-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="309e2-177">b.</span><span class="sxs-lookup"><span data-stu-id="309e2-177">b.</span></span> <span data-ttu-id="309e2-178">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="309e2-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="309e2-179">c.</span><span class="sxs-lookup"><span data-stu-id="309e2-179">c.</span></span> <span data-ttu-id="309e2-180">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="309e2-180">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="309e2-181">d.From the **Namespace** list, enter the namespace value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="309e2-181">d.From the **Namespace** list, enter the namespace value shown for that row.</span></span>
    
    <span data-ttu-id="309e2-182">e.</span><span class="sxs-lookup"><span data-stu-id="309e2-182">e.</span></span> <span data-ttu-id="309e2-183">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="309e2-183">Click **Ok**.</span></span>

1. <span data-ttu-id="309e2-184">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="309e2-184">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/knowledgeowl-tutorial/tutorial_knowledgeowl_certificate.png) 

1. <span data-ttu-id="309e2-186">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="309e2-186">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/knowledgeowl-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="309e2-188">On the **KnowledgeOwl Configuration** section, click **Configure KnowledgeOwl** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="309e2-188">On the **KnowledgeOwl Configuration** section, click **Configure KnowledgeOwl** to open **Configure sign-on** window.</span></span> <span data-ttu-id="309e2-189">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="309e2-189">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![KnowledgeOwl Configuration](./media/knowledgeowl-tutorial/tutorial_knowledgeowl_configure.png)

1. <span data-ttu-id="309e2-191">In a different web browser window, log into your KnowledgeOwl company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="309e2-191">In a different web browser window, log into your KnowledgeOwl company site as an administrator.</span></span>

1. <span data-ttu-id="309e2-192">Click on **Settings** and then select **Security**.</span><span class="sxs-lookup"><span data-stu-id="309e2-192">Click on **Settings** and then select **Security**.</span></span>

    ![KnowledgeOwl Configuration](./media/knowledgeowl-tutorial/configure1.png)

1. <span data-ttu-id="309e2-194">Scroll down upto the **SAML SSO Integration** and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="309e2-194">Scroll down upto the **SAML SSO Integration** and perform the following steps:</span></span>
    
    ![KnowledgeOwl Configuration](./media/knowledgeowl-tutorial/configure2.png)

    <span data-ttu-id="309e2-196">a.</span><span class="sxs-lookup"><span data-stu-id="309e2-196">a.</span></span> <span data-ttu-id="309e2-197">Select **Enable SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="309e2-197">Select **Enable SAML SSO**.</span></span>

    <span data-ttu-id="309e2-198">b.</span><span class="sxs-lookup"><span data-stu-id="309e2-198">b.</span></span> <span data-ttu-id="309e2-199">Copy the **SP Entity ID** value and paste it into the **Identifier (Entity ID)** in the **KnowledgeOwl Domain and URLs** section on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="309e2-199">Copy the **SP Entity ID** value and paste it into the **Identifier (Entity ID)** in the **KnowledgeOwl Domain and URLs** section on the Azure portal.</span></span>

    <span data-ttu-id="309e2-200">c.</span><span class="sxs-lookup"><span data-stu-id="309e2-200">c.</span></span> <span data-ttu-id="309e2-201">Copy the **SP Login URL** value and paste it into the **Sign-on URL and Reply URL** textboxes in the **KnowledgeOwl Domain and URLs** section on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="309e2-201">Copy the **SP Login URL** value and paste it into the **Sign-on URL and Reply URL** textboxes in the **KnowledgeOwl Domain and URLs** section on the Azure portal.</span></span>

    <span data-ttu-id="309e2-202">d.</span><span class="sxs-lookup"><span data-stu-id="309e2-202">d.</span></span> <span data-ttu-id="309e2-203">In the **IdP entityID** textbox, paste the **SAML Entity ID** value, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="309e2-203">In the **IdP entityID** textbox, paste the **SAML Entity ID** value, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="309e2-204">e.</span><span class="sxs-lookup"><span data-stu-id="309e2-204">e.</span></span> <span data-ttu-id="309e2-205">In the **IdP Login URL** textbox, paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="309e2-205">In the **IdP Login URL** textbox, paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="309e2-206">f.</span><span class="sxs-lookup"><span data-stu-id="309e2-206">f.</span></span> <span data-ttu-id="309e2-207">In the **IdP Logout URL** textbox, paste the **Sign-Out URL** value, which you have copied from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="309e2-207">In the **IdP Logout URL** textbox, paste the **Sign-Out URL** value, which you have copied from the Azure portal</span></span>

    <span data-ttu-id="309e2-208">g.</span><span class="sxs-lookup"><span data-stu-id="309e2-208">g.</span></span> <span data-ttu-id="309e2-209">Upload the downloaded certificate form the Azure portal by clicking the **Upload IdP Certificate**.</span><span class="sxs-lookup"><span data-stu-id="309e2-209">Upload the downloaded certificate form the Azure portal by clicking the **Upload IdP Certificate**.</span></span>

    <span data-ttu-id="309e2-210">h.</span><span class="sxs-lookup"><span data-stu-id="309e2-210">h.</span></span> <span data-ttu-id="309e2-211">Click on **Map SAML Attributes** to map attributes and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="309e2-211">Click on **Map SAML Attributes** to map attributes and perform the following steps:</span></span>
    
    ![KnowledgeOwl Configuration](./media/knowledgeowl-tutorial/configure3.png)

    * <span data-ttu-id="309e2-213">Enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/ssoid` into the **SSO ID** textbox</span><span class="sxs-lookup"><span data-stu-id="309e2-213">Enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/ssoid` into the **SSO ID** textbox</span></span>
    * <span data-ttu-id="309e2-214">Enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` into the **Username/Email** textbox.</span><span class="sxs-lookup"><span data-stu-id="309e2-214">Enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` into the **Username/Email** textbox.</span></span>
    * <span data-ttu-id="309e2-215">Enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname` into the **First Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="309e2-215">Enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname` into the **First Name** textbox.</span></span>
    * <span data-ttu-id="309e2-216">Enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname` into the **Last Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="309e2-216">Enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname` into the **Last Name** textbox.</span></span>
    * <span data-ttu-id="309e2-217">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="309e2-217">Click **Save**</span></span>

    <span data-ttu-id="309e2-218">i.</span><span class="sxs-lookup"><span data-stu-id="309e2-218">i.</span></span> <span data-ttu-id="309e2-219">Click **Save** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="309e2-219">Click **Save** at the bottom of the page.</span></span>

    ![KnowledgeOwl Configuration](./media/knowledgeowl-tutorial/configure4.png)

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="309e2-221">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="309e2-221">Create an Azure AD test user</span></span>

<span data-ttu-id="309e2-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="309e2-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="309e2-224">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="309e2-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="309e2-225">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="309e2-225">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/knowledgeowl-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="309e2-227">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="309e2-227">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/knowledgeowl-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="309e2-229">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="309e2-229">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/knowledgeowl-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="309e2-231">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="309e2-231">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/knowledgeowl-tutorial/create_aaduser_04.png)

    <span data-ttu-id="309e2-233">a.</span><span class="sxs-lookup"><span data-stu-id="309e2-233">a.</span></span> <span data-ttu-id="309e2-234">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="309e2-234">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="309e2-235">b.</span><span class="sxs-lookup"><span data-stu-id="309e2-235">b.</span></span> <span data-ttu-id="309e2-236">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="309e2-236">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="309e2-237">c.</span><span class="sxs-lookup"><span data-stu-id="309e2-237">c.</span></span> <span data-ttu-id="309e2-238">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="309e2-238">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="309e2-239">d.</span><span class="sxs-lookup"><span data-stu-id="309e2-239">d.</span></span> <span data-ttu-id="309e2-240">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="309e2-240">Click **Create**.</span></span>
 
### <a name="create-a-knowledgeowl-test-user"></a><span data-ttu-id="309e2-241">Create a KnowledgeOwl test user</span><span class="sxs-lookup"><span data-stu-id="309e2-241">Create a KnowledgeOwl test user</span></span>

<span data-ttu-id="309e2-242">The objective of this section is to create a user called Britta Simon in KnowledgeOwl.</span><span class="sxs-lookup"><span data-stu-id="309e2-242">The objective of this section is to create a user called Britta Simon in KnowledgeOwl.</span></span> <span data-ttu-id="309e2-243">KnowledgeOwl supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="309e2-243">KnowledgeOwl supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="309e2-244">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="309e2-244">There is no action item for you in this section.</span></span> <span data-ttu-id="309e2-245">A new user is created during an attempt to access KnowledgeOwl if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="309e2-245">A new user is created during an attempt to access KnowledgeOwl if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="309e2-246">If you need to create a user manually, contact [KnowledgeOwl support team](mailto:support@knowledgeowl.com).</span><span class="sxs-lookup"><span data-stu-id="309e2-246">If you need to create a user manually, contact [KnowledgeOwl support team](mailto:support@knowledgeowl.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="309e2-247">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="309e2-247">Assign the Azure AD test user</span></span>

<span data-ttu-id="309e2-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to KnowledgeOwl.</span><span class="sxs-lookup"><span data-stu-id="309e2-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to KnowledgeOwl.</span></span>

![Assign the user role][200] 

<span data-ttu-id="309e2-250">**To assign Britta Simon to KnowledgeOwl, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="309e2-250">**To assign Britta Simon to KnowledgeOwl, perform the following steps:**</span></span>

1. <span data-ttu-id="309e2-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="309e2-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="309e2-253">In the applications list, select **KnowledgeOwl**.</span><span class="sxs-lookup"><span data-stu-id="309e2-253">In the applications list, select **KnowledgeOwl**.</span></span>

    ![The KnowledgeOwl link in the Applications list](./media/knowledgeowl-tutorial/tutorial_knowledgeowl_app.png)  

1. <span data-ttu-id="309e2-255">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="309e2-255">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="309e2-257">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="309e2-257">Click **Add** button.</span></span> <span data-ttu-id="309e2-258">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="309e2-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="309e2-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="309e2-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="309e2-261">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="309e2-261">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="309e2-262">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="309e2-262">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="309e2-263">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="309e2-263">Test single sign-on</span></span>

<span data-ttu-id="309e2-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="309e2-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="309e2-265">When you click the KnowledgeOwl tile in the Access Panel, you should get automatically signed-on to your KnowledgeOwl application.</span><span class="sxs-lookup"><span data-stu-id="309e2-265">When you click the KnowledgeOwl tile in the Access Panel, you should get automatically signed-on to your KnowledgeOwl application.</span></span>
<span data-ttu-id="309e2-266">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="309e2-266">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="309e2-267">Additional resources</span><span class="sxs-lookup"><span data-stu-id="309e2-267">Additional resources</span></span>

* [<span data-ttu-id="309e2-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="309e2-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="309e2-269">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="309e2-269">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/knowledgeowl-tutorial/tutorial_general_01.png
[2]: ./media/knowledgeowl-tutorial/tutorial_general_02.png
[3]: ./media/knowledgeowl-tutorial/tutorial_general_03.png
[4]: ./media/knowledgeowl-tutorial/tutorial_general_04.png

[100]: ./media/knowledgeowl-tutorial/tutorial_general_100.png

[200]: ./media/knowledgeowl-tutorial/tutorial_general_200.png
[201]: ./media/knowledgeowl-tutorial/tutorial_general_201.png
[202]: ./media/knowledgeowl-tutorial/tutorial_general_202.png
[203]: ./media/knowledgeowl-tutorial/tutorial_general_203.png

