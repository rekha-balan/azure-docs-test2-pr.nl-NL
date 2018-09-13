---
title: 'Tutorial: Azure Active Directory integration with CylancePROTECT | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and CylancePROTECT.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ea392d8c-c8aa-4475-99d0-b08524ef0f3a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2018
ms.author: jeedes
ms.openlocfilehash: 0baeea0dc8f32182fecf0b15fede56bf8c1f9b44
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867297"
---
# <a name="tutorial-azure-active-directory-integration-with-cylanceprotect"></a><span data-ttu-id="76734-103">Tutorial: Azure Active Directory integration with CylancePROTECT</span><span class="sxs-lookup"><span data-stu-id="76734-103">Tutorial: Azure Active Directory integration with CylancePROTECT</span></span>

<span data-ttu-id="76734-104">In this tutorial, you learn how to integrate CylancePROTECT with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76734-104">In this tutorial, you learn how to integrate CylancePROTECT with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76734-105">Integrating CylancePROTECT with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="76734-105">Integrating CylancePROTECT with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="76734-106">You can control in Azure AD who has access to CylancePROTECT.</span><span class="sxs-lookup"><span data-stu-id="76734-106">You can control in Azure AD who has access to CylancePROTECT.</span></span>
- <span data-ttu-id="76734-107">You can enable your users to automatically get signed-on to CylancePROTECT (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="76734-107">You can enable your users to automatically get signed-on to CylancePROTECT (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="76734-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="76734-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="76734-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="76734-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76734-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="76734-110">Prerequisites</span></span>

<span data-ttu-id="76734-111">To configure Azure AD integration with CylancePROTECT, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="76734-111">To configure Azure AD integration with CylancePROTECT, you need the following items:</span></span>

- <span data-ttu-id="76734-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="76734-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76734-113">A CylancePROTECT single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="76734-113">A CylancePROTECT single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="76734-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="76734-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="76734-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="76734-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76734-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="76734-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="76734-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76734-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="76734-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="76734-118">Scenario description</span></span>
<span data-ttu-id="76734-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="76734-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="76734-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="76734-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76734-121">Adding CylancePROTECT from the gallery</span><span class="sxs-lookup"><span data-stu-id="76734-121">Adding CylancePROTECT from the gallery</span></span>
1. <span data-ttu-id="76734-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="76734-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cylanceprotect-from-the-gallery"></a><span data-ttu-id="76734-123">Adding CylancePROTECT from the gallery</span><span class="sxs-lookup"><span data-stu-id="76734-123">Adding CylancePROTECT from the gallery</span></span>
<span data-ttu-id="76734-124">To configure the integration of CylancePROTECT into Azure AD, you need to add CylancePROTECT from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="76734-124">To configure the integration of CylancePROTECT into Azure AD, you need to add CylancePROTECT from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="76734-125">**To add CylancePROTECT from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="76734-125">**To add CylancePROTECT from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="76734-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="76734-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="76734-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="76734-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="76734-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="76734-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="76734-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="76734-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="76734-133">In the search box, type **CylancePROTECT**, select **CylancePROTECT** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="76734-133">In the search box, type **CylancePROTECT**, select **CylancePROTECT** from result panel then click **Add** button to add the application.</span></span>

    ![CylancePROTECT in the results list](./media/cylanceprotect-tutorial/tutorial_cylanceprotect_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="76734-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="76734-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="76734-136">In this section, you configure and test Azure AD single sign-on with CylancePROTECT based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="76734-136">In this section, you configure and test Azure AD single sign-on with CylancePROTECT based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="76734-137">For single sign-on to work, Azure AD needs to know what the counterpart user in CylancePROTECT is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76734-137">For single sign-on to work, Azure AD needs to know what the counterpart user in CylancePROTECT is to a user in Azure AD.</span></span> <span data-ttu-id="76734-138">In other words, a link relationship between an Azure AD user and the related user in CylancePROTECT needs to be established.</span><span class="sxs-lookup"><span data-stu-id="76734-138">In other words, a link relationship between an Azure AD user and the related user in CylancePROTECT needs to be established.</span></span>

<span data-ttu-id="76734-139">To configure and test Azure AD single sign-on with CylancePROTECT, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="76734-139">To configure and test Azure AD single sign-on with CylancePROTECT, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="76734-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="76734-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="76734-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76734-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="76734-142">**[Create a CylancePROTECT test user](#create-a-cylanceprotect-test-user)** - to have a counterpart of Britta Simon in CylancePROTECT that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="76734-142">**[Create a CylancePROTECT test user](#create-a-cylanceprotect-test-user)** - to have a counterpart of Britta Simon in CylancePROTECT that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="76734-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="76734-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="76734-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="76734-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="76734-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="76734-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="76734-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CylancePROTECT application.</span><span class="sxs-lookup"><span data-stu-id="76734-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CylancePROTECT application.</span></span>

<span data-ttu-id="76734-147">**To configure Azure AD single sign-on with CylancePROTECT, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="76734-147">**To configure Azure AD single sign-on with CylancePROTECT, perform the following steps:**</span></span>

1. <span data-ttu-id="76734-148">In the Azure portal, on the **CylancePROTECT** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="76734-148">In the Azure portal, on the **CylancePROTECT** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="76734-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="76734-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/cylanceprotect-tutorial/tutorial_cylanceprotect_samlbase.png)

1. <span data-ttu-id="76734-152">On the **CylancePROTECT Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="76734-152">On the **CylancePROTECT Domain and URLs** section, perform the following steps:</span></span>

    ![CylancePROTECT Domain and URLs single sign-on information](./media/cylanceprotect-tutorial/tutorial_cylanceprotect_url.png)

    <span data-ttu-id="76734-154">a.</span><span class="sxs-lookup"><span data-stu-id="76734-154">a.</span></span> <span data-ttu-id="76734-155">In the **Identifier** textbox, type the URL:</span><span class="sxs-lookup"><span data-stu-id="76734-155">In the **Identifier** textbox, type the URL:</span></span>
    
    | <span data-ttu-id="76734-156">Region</span><span class="sxs-lookup"><span data-stu-id="76734-156">Region</span></span> | <span data-ttu-id="76734-157">URL Value</span><span class="sxs-lookup"><span data-stu-id="76734-157">URL Value</span></span> |
    |----------|---------|
    | <span data-ttu-id="76734-158">Asia-Pacific Northeast (APNE1)</span><span class="sxs-lookup"><span data-stu-id="76734-158">Asia-Pacific Northeast (APNE1)</span></span>| ` https://login-apne1.cylance.com/EnterpriseLogin/ConsumeSaml`|
    | <span data-ttu-id="76734-159">Asia-Pacific Southeast (AU)</span><span class="sxs-lookup"><span data-stu-id="76734-159">Asia-Pacific Southeast (AU)</span></span> | `https://login-au.cylance.com/EnterpriseLogin/ConsumeSaml` |
    | <span data-ttu-id="76734-160">Europe Central (EUC1)</span><span class="sxs-lookup"><span data-stu-id="76734-160">Europe Central (EUC1)</span></span>|`https://login-euc1.cylance.com/EnterpriseLogin/ConsumeSaml`|
    | <span data-ttu-id="76734-161">North America</span><span class="sxs-lookup"><span data-stu-id="76734-161">North America</span></span>|`https://login.cylance.com/EnterpriseLogin/ConsumeSaml`|
    | <span data-ttu-id="76734-162">South America (SAE1)</span><span class="sxs-lookup"><span data-stu-id="76734-162">South America (SAE1)</span></span>|`https://login-sae1.cylance.com/EnterpriseLogin/ConsumeSaml`|
    
    <span data-ttu-id="76734-163">b.</span><span class="sxs-lookup"><span data-stu-id="76734-163">b.</span></span> <span data-ttu-id="76734-164">In the **Reply URL** textbox, type the URL:</span><span class="sxs-lookup"><span data-stu-id="76734-164">In the **Reply URL** textbox, type the URL:</span></span>
    
    | <span data-ttu-id="76734-165">Region</span><span class="sxs-lookup"><span data-stu-id="76734-165">Region</span></span> | <span data-ttu-id="76734-166">URL Value</span><span class="sxs-lookup"><span data-stu-id="76734-166">URL Value</span></span> |
    |----------|---------|
    | <span data-ttu-id="76734-167">Asia-Pacific Northeast (APNE1)</span><span class="sxs-lookup"><span data-stu-id="76734-167">Asia-Pacific Northeast (APNE1)</span></span>|`https://login-apne1.cylance.com/EnterpriseLogin/ConsumeSaml`|
    | <span data-ttu-id="76734-168">Asia-Pacific Southeast (AU)</span><span class="sxs-lookup"><span data-stu-id="76734-168">Asia-Pacific Southeast (AU)</span></span>|`https://login-au.cylance.com/EnterpriseLogin/ConsumeSaml`|
    | <span data-ttu-id="76734-169">Europe Central (EUC1)</span><span class="sxs-lookup"><span data-stu-id="76734-169">Europe Central (EUC1)</span></span>|`https://login-euc1.cylance.com/EnterpriseLogin/ConsumeSaml`|
    | <span data-ttu-id="76734-170">North America</span><span class="sxs-lookup"><span data-stu-id="76734-170">North America</span></span>|`https://login.cylance.com/EnterpriseLogin/ConsumeSaml`|
    | <span data-ttu-id="76734-171">South America (SAE1)</span><span class="sxs-lookup"><span data-stu-id="76734-171">South America (SAE1)</span></span>|`https://login-sae1.cylance.com/EnterpriseLogin/ConsumeSaml`|

1. <span data-ttu-id="76734-172">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the cerificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="76734-172">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the cerificate file on your computer.</span></span>

    ![The Certificate download link](./media/cylanceprotect-tutorial/tutorial_cylanceprotect_certificate.png) 

1. <span data-ttu-id="76734-174">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="76734-174">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/cylanceprotect-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="76734-176">On the **CylancePROTECT Configuration** section, click **Configure CylancePROTECT** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="76734-176">On the **CylancePROTECT Configuration** section, click **Configure CylancePROTECT** to open **Configure sign-on** window.</span></span> <span data-ttu-id="76734-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="76734-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![CylancePROTECT Configuration](./media/cylanceprotect-tutorial/tutorial_cylanceprotect_configure.png) 

1. <span data-ttu-id="76734-179">To configure single sign-on on **CylancePROTECT** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to console administrator.</span><span class="sxs-lookup"><span data-stu-id="76734-179">To configure single sign-on on **CylancePROTECT** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to console administrator.</span></span> <span data-ttu-id="76734-180">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="76734-180">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="76734-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="76734-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="76734-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="76734-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="76734-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="76734-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="76734-184">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="76734-184">Create an Azure AD test user</span></span>

<span data-ttu-id="76734-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76734-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="76734-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="76734-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="76734-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="76734-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/cylanceprotect-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="76734-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="76734-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/cylanceprotect-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="76734-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="76734-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/cylanceprotect-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="76734-194">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="76734-194">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/cylanceprotect-tutorial/create_aaduser_04.png)

    <span data-ttu-id="76734-196">a.</span><span class="sxs-lookup"><span data-stu-id="76734-196">a.</span></span> <span data-ttu-id="76734-197">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="76734-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76734-198">b.</span><span class="sxs-lookup"><span data-stu-id="76734-198">b.</span></span> <span data-ttu-id="76734-199">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76734-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="76734-200">c.</span><span class="sxs-lookup"><span data-stu-id="76734-200">c.</span></span> <span data-ttu-id="76734-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="76734-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="76734-202">d.</span><span class="sxs-lookup"><span data-stu-id="76734-202">d.</span></span> <span data-ttu-id="76734-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="76734-203">Click **Create**.</span></span>
  
### <a name="create-a-cylanceprotect-test-user"></a><span data-ttu-id="76734-204">Create a CylancePROTECT test user</span><span class="sxs-lookup"><span data-stu-id="76734-204">Create a CylancePROTECT test user</span></span>

<span data-ttu-id="76734-205">In this section, you create a user called Britta Simon in CylancePROTECT.</span><span class="sxs-lookup"><span data-stu-id="76734-205">In this section, you create a user called Britta Simon in CylancePROTECT.</span></span> <span data-ttu-id="76734-206">Work with console administrator to add the users in the CylancePROTECT platform.</span><span class="sxs-lookup"><span data-stu-id="76734-206">Work with console administrator to add the users in the CylancePROTECT platform.</span></span> <span data-ttu-id="76734-207">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="76734-207">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="76734-208">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="76734-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="76734-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CylancePROTECT.</span><span class="sxs-lookup"><span data-stu-id="76734-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CylancePROTECT.</span></span>

![Assign the user role][200] 

<span data-ttu-id="76734-211">**To assign Britta Simon to CylancePROTECT, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="76734-211">**To assign Britta Simon to CylancePROTECT, perform the following steps:**</span></span>

1. <span data-ttu-id="76734-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="76734-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="76734-214">In the applications list, select **CylancePROTECT**.</span><span class="sxs-lookup"><span data-stu-id="76734-214">In the applications list, select **CylancePROTECT**.</span></span>

    ![The CylancePROTECT link in the Applications list](./media/cylanceprotect-tutorial/tutorial_cylanceprotect_app.png)  

1. <span data-ttu-id="76734-216">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="76734-216">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="76734-218">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="76734-218">Click **Add** button.</span></span> <span data-ttu-id="76734-219">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="76734-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="76734-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="76734-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="76734-222">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="76734-222">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="76734-223">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="76734-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="76734-224">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="76734-224">Test single sign-on</span></span>

<span data-ttu-id="76734-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="76734-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="76734-226">When you click the CylancePROTECT tile in the Access Panel, you should get automatically signed-on to your CylancePROTECT application.</span><span class="sxs-lookup"><span data-stu-id="76734-226">When you click the CylancePROTECT tile in the Access Panel, you should get automatically signed-on to your CylancePROTECT application.</span></span>
<span data-ttu-id="76734-227">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76734-227">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="76734-228">Additional resources</span><span class="sxs-lookup"><span data-stu-id="76734-228">Additional resources</span></span>

* [<span data-ttu-id="76734-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76734-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="76734-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="76734-230">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/cylanceprotect-tutorial/tutorial_general_01.png
[2]: ./media/cylanceprotect-tutorial/tutorial_general_02.png
[3]: ./media/cylanceprotect-tutorial/tutorial_general_03.png
[4]: ./media/cylanceprotect-tutorial/tutorial_general_04.png

[100]: ./media/cylanceprotect-tutorial/tutorial_general_100.png

[200]: ./media/cylanceprotect-tutorial/tutorial_general_200.png
[201]: ./media/cylanceprotect-tutorial/tutorial_general_201.png
[202]: ./media/cylanceprotect-tutorial/tutorial_general_202.png
[203]: ./media/cylanceprotect-tutorial/tutorial_general_203.png

