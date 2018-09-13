---
title: 'Tutorial: Azure Active Directory integration with SAML SSO for Bitbucket by resolution GmbH | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAML SSO for Bitbucket by resolution GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: fc947df1-f24e-43ae-9a34-518293583d69
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/04/2017
ms.author: jeedes
ms.openlocfilehash: c91f62aa2f47cfab7de22def631a7149ab37ba46
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857237"
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-bitbucket-by-resolution-gmbh"></a><span data-ttu-id="cc670-103">Tutorial: Azure Active Directory integration with SAML SSO for Bitbucket by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="cc670-103">Tutorial: Azure Active Directory integration with SAML SSO for Bitbucket by resolution GmbH</span></span>

<span data-ttu-id="cc670-104">In this tutorial, you learn how to integrate SAML SSO for Bitbucket by resolution GmbH with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc670-104">In this tutorial, you learn how to integrate SAML SSO for Bitbucket by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc670-105">Integrating SAML SSO for Bitbucket by resolution GmbH with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cc670-105">Integrating SAML SSO for Bitbucket by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cc670-106">You can control in Azure AD who has access to SAML SSO for Bitbucket by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="cc670-106">You can control in Azure AD who has access to SAML SSO for Bitbucket by resolution GmbH.</span></span>
- <span data-ttu-id="cc670-107">You can enable your users to automatically get signed-on to SAML SSO for Bitbucket by resolution GmbH (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="cc670-107">You can enable your users to automatically get signed-on to SAML SSO for Bitbucket by resolution GmbH (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cc670-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cc670-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="cc670-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cc670-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc670-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cc670-110">Prerequisites</span></span>

<span data-ttu-id="cc670-111">To configure Azure AD integration with SAML SSO for Bitbucket by resolution GmbH, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cc670-111">To configure Azure AD integration with SAML SSO for Bitbucket by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="cc670-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cc670-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc670-113">A SAML SSO for Bitbucket by resolution GmbH single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cc670-113">A SAML SSO for Bitbucket by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc670-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="cc670-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc670-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cc670-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc670-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cc670-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc670-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc670-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc670-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cc670-118">Scenario description</span></span>
<span data-ttu-id="cc670-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cc670-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc670-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cc670-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc670-121">Adding SAML SSO for Bitbucket by resolution GmbH from the gallery</span><span class="sxs-lookup"><span data-stu-id="cc670-121">Adding SAML SSO for Bitbucket by resolution GmbH from the gallery</span></span>
1. <span data-ttu-id="cc670-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc670-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-bitbucket-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="cc670-123">Adding SAML SSO for Bitbucket by resolution GmbH from the gallery</span><span class="sxs-lookup"><span data-stu-id="cc670-123">Adding SAML SSO for Bitbucket by resolution GmbH from the gallery</span></span>
<span data-ttu-id="cc670-124">To configure the integration of SAML SSO for Bitbucket by resolution GmbH into Azure AD, you need to add SAML SSO for Bitbucket by resolution GmbH from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cc670-124">To configure the integration of SAML SSO for Bitbucket by resolution GmbH into Azure AD, you need to add SAML SSO for Bitbucket by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cc670-125">**To add SAML SSO for Bitbucket by resolution GmbH from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc670-125">**To add SAML SSO for Bitbucket by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cc670-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cc670-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="cc670-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="cc670-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cc670-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cc670-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="cc670-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="cc670-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="cc670-133">In the search box, type **SAML SSO for Bitbucket by resolution GmbH**, select **SAML SSO for Bitbucket by resolution GmbH** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="cc670-133">In the search box, type **SAML SSO for Bitbucket by resolution GmbH**, select **SAML SSO for Bitbucket by resolution GmbH** from result panel then click **Add** button to add the application.</span></span>

    ![SAML SSO for Bitbucket by resolution GmbH in the results list](./media/bitbucket-tutorial/tutorial_bitbucket_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cc670-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc670-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cc670-136">In this section, you configure and test Azure AD single sign-on with SAML SSO for Bitbucket by resolution GmbH based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc670-136">In this section, you configure and test Azure AD single sign-on with SAML SSO for Bitbucket by resolution GmbH based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc670-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Bitbucket by resolution GmbH is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc670-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Bitbucket by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="cc670-138">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Bitbucket by resolution GmbH needs to be established.</span><span class="sxs-lookup"><span data-stu-id="cc670-138">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Bitbucket by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="cc670-139">In SAML SSO for Bitbucket by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="cc670-139">In SAML SSO for Bitbucket by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cc670-140">To configure and test Azure AD single sign-on with SAML SSO for Bitbucket by resolution GmbH, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cc670-140">To configure and test Azure AD single sign-on with SAML SSO for Bitbucket by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cc670-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="cc670-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="cc670-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc670-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="cc670-143">**[Create a SAML SSO for Bitbucket by resolution GmbH test user](#create-a-saml-sso-for-bitbucket-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Bitbucket by resolution GmbH that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="cc670-143">**[Create a SAML SSO for Bitbucket by resolution GmbH test user](#create-a-saml-sso-for-bitbucket-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Bitbucket by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="cc670-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc670-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="cc670-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="cc670-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cc670-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc670-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cc670-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Bitbucket by resolution GmbH application.</span><span class="sxs-lookup"><span data-stu-id="cc670-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Bitbucket by resolution GmbH application.</span></span>

<span data-ttu-id="cc670-148">**To configure Azure AD single sign-on with SAML SSO for Bitbucket by resolution GmbH, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc670-148">**To configure Azure AD single sign-on with SAML SSO for Bitbucket by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="cc670-149">In the Azure portal, on the **SAML SSO for Bitbucket by resolution GmbH** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cc670-149">In the Azure portal, on the **SAML SSO for Bitbucket by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="cc670-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc670-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/bitbucket-tutorial/tutorial_bitbucket_samlbase.png)

1. <span data-ttu-id="cc670-153">On the **SAML SSO for Bitbucket by resolution GmbH Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="cc670-153">On the **SAML SSO for Bitbucket by resolution GmbH Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![SAML SSO for Bitbucket by resolution GmbH Domain and URLs single sign-on information](./media/bitbucket-tutorial/tutorial_bitbucket_url.png)

    <span data-ttu-id="cc670-155">a.</span><span class="sxs-lookup"><span data-stu-id="cc670-155">a.</span></span> <span data-ttu-id="cc670-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="cc670-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="cc670-157">b.</span><span class="sxs-lookup"><span data-stu-id="cc670-157">b.</span></span> <span data-ttu-id="cc670-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="cc670-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

1. <span data-ttu-id="cc670-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="cc670-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![SAML SSO for Bitbucket by resolution GmbH Domain and URLs single sign-on information](./media/bitbucket-tutorial/tutorial_bitbucket_url1.png)

    <span data-ttu-id="cc670-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="cc670-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="cc670-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="cc670-162">These values are not real.</span></span> <span data-ttu-id="cc670-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="cc670-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="cc670-164">Contact [SAML SSO for Bitbucket by resolution GmbH Client support team](https://marketplace.atlassian.com/plugins/com.resolution.atlasplugins.samlsso-bitbucket/server/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="cc670-164">Contact [SAML SSO for Bitbucket by resolution GmbH Client support team](https://marketplace.atlassian.com/plugins/com.resolution.atlasplugins.samlsso-bitbucket/server/support) to get these values.</span></span> 

1. <span data-ttu-id="cc670-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="cc670-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/bitbucket-tutorial/tutorial_bitbucket_certificate.png) 

1. <span data-ttu-id="cc670-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cc670-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/bitbucket-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="cc670-169">Sign-on to your SAML SSO for Bitbucket by resolution GmbH company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="cc670-169">Sign-on to your SAML SSO for Bitbucket by resolution GmbH company site as administrator.</span></span>

1. <span data-ttu-id="cc670-170">On the right side of the main toolbar, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="cc670-170">On the right side of the main toolbar, click **Settings**.</span></span>

1. <span data-ttu-id="cc670-171">Go to ACCOUNTS section, click on **SAML SingleSignOn** on the Menubar.</span><span class="sxs-lookup"><span data-stu-id="cc670-171">Go to ACCOUNTS section, click on **SAML SingleSignOn** on the Menubar.</span></span>

    ![The Samlsingle](./media/bitbucket-tutorial/tutorial_bitbucket_samlsingle.png)

1. <span data-ttu-id="cc670-173">On the **SAML SIngleSignOn Plugin Configuration page**, click **Add idp**.</span><span class="sxs-lookup"><span data-stu-id="cc670-173">On the **SAML SIngleSignOn Plugin Configuration page**, click **Add idp**.</span></span> 

    ![The Add idp](./media/bitbucket-tutorial/tutorial_bitbucket_addidp.png)

1. <span data-ttu-id="cc670-175">On the **Choose your SAML Identity Provider** Page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc670-175">On the **Choose your SAML Identity Provider** Page, perform the following steps:</span></span>

    ![The identity provider](./media/bitbucket-tutorial/tutorial_bitbucket_identityprovider.png)

    <span data-ttu-id="cc670-177">a.</span><span class="sxs-lookup"><span data-stu-id="cc670-177">a.</span></span> <span data-ttu-id="cc670-178">Select **Idp Type** as **AZURE AD**.</span><span class="sxs-lookup"><span data-stu-id="cc670-178">Select **Idp Type** as **AZURE AD**.</span></span>

    <span data-ttu-id="cc670-179">b.</span><span class="sxs-lookup"><span data-stu-id="cc670-179">b.</span></span> <span data-ttu-id="cc670-180">In the **Name** textbox, type the name.</span><span class="sxs-lookup"><span data-stu-id="cc670-180">In the **Name** textbox, type the name.</span></span>

    <span data-ttu-id="cc670-181">c.</span><span class="sxs-lookup"><span data-stu-id="cc670-181">c.</span></span> <span data-ttu-id="cc670-182">In the **Description** textbox, type the description.</span><span class="sxs-lookup"><span data-stu-id="cc670-182">In the **Description** textbox, type the description.</span></span>

    <span data-ttu-id="cc670-183">d.</span><span class="sxs-lookup"><span data-stu-id="cc670-183">d.</span></span> <span data-ttu-id="cc670-184">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cc670-184">Click **Next**.</span></span>

1. <span data-ttu-id="cc670-185">On the **Identity provider configuration page**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cc670-185">On the **Identity provider configuration page**, click **Next**.</span></span>

    ![The identity config](./media/bitbucket-tutorial/tutorial_bitbucket_identityconfig.png)

1.  <span data-ttu-id="cc670-187">On the **Import SAML Idp Metadata** Page, click **Load File** to upload the **METADATA XML** file which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cc670-187">On the **Import SAML Idp Metadata** Page, click **Load File** to upload the **METADATA XML** file which you have downloaded from Azure portal.</span></span>

    ![The idpmetadata](./media/bitbucket-tutorial/tutorial_bitbucket_idpmetadata.png)
    
1. <span data-ttu-id="cc670-189">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cc670-189">Click **Next**.</span></span>

1. <span data-ttu-id="cc670-190">Click **Save settings**.</span><span class="sxs-lookup"><span data-stu-id="cc670-190">Click **Save settings**.</span></span>

    ![The save](./media/bitbucket-tutorial/tutorial_bitbucket_save.png)

> [!TIP]
> <span data-ttu-id="cc670-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="cc670-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cc670-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="cc670-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cc670-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc670-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cc670-195">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cc670-195">Create an Azure AD test user</span></span>

<span data-ttu-id="cc670-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc670-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="cc670-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc670-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cc670-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="cc670-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/bitbucket-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="cc670-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="cc670-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/bitbucket-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="cc670-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="cc670-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/bitbucket-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="cc670-205">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc670-205">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/bitbucket-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cc670-207">a.</span><span class="sxs-lookup"><span data-stu-id="cc670-207">a.</span></span> <span data-ttu-id="cc670-208">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc670-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc670-209">b.</span><span class="sxs-lookup"><span data-stu-id="cc670-209">b.</span></span> <span data-ttu-id="cc670-210">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc670-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="cc670-211">c.</span><span class="sxs-lookup"><span data-stu-id="cc670-211">c.</span></span> <span data-ttu-id="cc670-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="cc670-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="cc670-213">d.</span><span class="sxs-lookup"><span data-stu-id="cc670-213">d.</span></span> <span data-ttu-id="cc670-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc670-214">Click **Create**.</span></span>
 
### <a name="create-a-saml-sso-for-bitbucket-by-resolution-gmbh-test-user"></a><span data-ttu-id="cc670-215">Create a SAML SSO for Bitbucket by resolution GmbH test user</span><span class="sxs-lookup"><span data-stu-id="cc670-215">Create a SAML SSO for Bitbucket by resolution GmbH test user</span></span>

<span data-ttu-id="cc670-216">The objective of this section is to create a user called Britta Simon in SAML SSO for Bitbucket by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="cc670-216">The objective of this section is to create a user called Britta Simon in SAML SSO for Bitbucket by resolution GmbH.</span></span> <span data-ttu-id="cc670-217">SAML SSO for Bitbucket by resolution GmbH supports just-in-time provisioning and also users can be created manually, contact [SAML SSO for Bitbucket by resolution GmbH Client support team](https://marketplace.atlassian.com/plugins/com.resolution.atlasplugins.samlsso-bitbucket/server/support) as per your requirement.</span><span class="sxs-lookup"><span data-stu-id="cc670-217">SAML SSO for Bitbucket by resolution GmbH supports just-in-time provisioning and also users can be created manually, contact [SAML SSO for Bitbucket by resolution GmbH Client support team](https://marketplace.atlassian.com/plugins/com.resolution.atlasplugins.samlsso-bitbucket/server/support) as per your requirement.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="cc670-218">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cc670-218">Assign the Azure AD test user</span></span>

<span data-ttu-id="cc670-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Bitbucket by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="cc670-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Bitbucket by resolution GmbH.</span></span>

![Assign the user role][200] 

<span data-ttu-id="cc670-221">**To assign Britta Simon to SAML SSO for Bitbucket by resolution GmbH, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc670-221">**To assign Britta Simon to SAML SSO for Bitbucket by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="cc670-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cc670-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cc670-224">In the applications list, select **SAML SSO for Bitbucket by resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="cc670-224">In the applications list, select **SAML SSO for Bitbucket by resolution GmbH**.</span></span>

    ![The SAML SSO for Bitbucket by resolution GmbH link in the Applications list](./media/bitbucket-tutorial/tutorial_bitbucket_app.png)  

1. <span data-ttu-id="cc670-226">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cc670-226">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="cc670-228">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cc670-228">Click **Add** button.</span></span> <span data-ttu-id="cc670-229">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc670-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="cc670-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="cc670-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="cc670-232">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc670-232">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="cc670-233">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc670-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cc670-234">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc670-234">Test single sign-on</span></span>

<span data-ttu-id="cc670-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cc670-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cc670-236">When you click the SAML SSO for Bitbucket by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Bitbucket by resolution GmbH application.</span><span class="sxs-lookup"><span data-stu-id="cc670-236">When you click the SAML SSO for Bitbucket by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Bitbucket by resolution GmbH application.</span></span>
<span data-ttu-id="cc670-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc670-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cc670-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cc670-238">Additional resources</span></span>

* [<span data-ttu-id="cc670-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc670-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cc670-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc670-240">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bitbucket-tutorial/tutorial_general_01.png
[2]: ./media/bitbucket-tutorial/tutorial_general_02.png
[3]: ./media/bitbucket-tutorial/tutorial_general_03.png
[4]: ./media/bitbucket-tutorial/tutorial_general_04.png

[100]: ./media/bitbucket-tutorial/tutorial_general_100.png

[200]: ./media/bitbucket-tutorial/tutorial_general_200.png
[201]: ./media/bitbucket-tutorial/tutorial_general_201.png
[202]: ./media/bitbucket-tutorial/tutorial_general_202.png
[203]: ./media/bitbucket-tutorial/tutorial_general_203.png

