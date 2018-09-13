---
title: 'Tutorial: Azure Active Directory integration with Jamf Pro | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Jamf Pro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 35e86d08-c29e-49ca-8545-b0ff559c5faf
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2018
ms.author: jeedes
ms.openlocfilehash: 94b8b935728110cd5dd07b2066e8320274e3b082
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965669"
---
# <a name="tutorial-azure-active-directory-integration-with-jamf-pro"></a><span data-ttu-id="1e414-103">Tutorial: Azure Active Directory integration with Jamf Pro</span><span class="sxs-lookup"><span data-stu-id="1e414-103">Tutorial: Azure Active Directory integration with Jamf Pro</span></span>

<span data-ttu-id="1e414-104">In this tutorial, you learn how to integrate Jamf Pro with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e414-104">In this tutorial, you learn how to integrate Jamf Pro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e414-105">Integrating Jamf Pro with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1e414-105">Integrating Jamf Pro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1e414-106">You can control in Azure AD who has access to Jamf Pro.</span><span class="sxs-lookup"><span data-stu-id="1e414-106">You can control in Azure AD who has access to Jamf Pro.</span></span>
- <span data-ttu-id="1e414-107">You can enable your users to automatically get signed-on to Jamf Pro (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="1e414-107">You can enable your users to automatically get signed-on to Jamf Pro (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1e414-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e414-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1e414-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1e414-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e414-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1e414-110">Prerequisites</span></span>

<span data-ttu-id="1e414-111">To configure Azure AD integration with Jamf Pro, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1e414-111">To configure Azure AD integration with Jamf Pro, you need the following items:</span></span>

- <span data-ttu-id="1e414-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1e414-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e414-113">A Jamf Pro single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1e414-113">A Jamf Pro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e414-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1e414-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e414-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1e414-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e414-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1e414-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e414-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e414-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e414-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1e414-118">Scenario description</span></span>
<span data-ttu-id="1e414-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1e414-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e414-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1e414-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e414-121">Adding Jamf Pro from the gallery</span><span class="sxs-lookup"><span data-stu-id="1e414-121">Adding Jamf Pro from the gallery</span></span>
1. <span data-ttu-id="1e414-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1e414-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jamf-pro-from-the-gallery"></a><span data-ttu-id="1e414-123">Adding Jamf Pro from the gallery</span><span class="sxs-lookup"><span data-stu-id="1e414-123">Adding Jamf Pro from the gallery</span></span>
<span data-ttu-id="1e414-124">To configure the integration of Jamf Pro into Azure AD, you need to add Jamf Pro from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1e414-124">To configure the integration of Jamf Pro into Azure AD, you need to add Jamf Pro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1e414-125">**To add Jamf Pro from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1e414-125">**To add Jamf Pro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e414-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1e414-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="1e414-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1e414-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1e414-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1e414-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="1e414-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1e414-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="1e414-133">In the search box, type **Jamf Pro**, select **Jamf Pro** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1e414-133">In the search box, type **Jamf Pro**, select **Jamf Pro** from result panel then click **Add** button to add the application.</span></span>

    ![Jamf Pro in the results list](./media/jamfprosamlconnector-tutorial/tutorial_jamfprosamlconnector_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1e414-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1e414-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1e414-136">In this section, you configure and test Azure AD single sign-on with Jamf Pro based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1e414-136">In this section, you configure and test Azure AD single sign-on with Jamf Pro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e414-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Jamf Pro is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e414-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Jamf Pro is to a user in Azure AD.</span></span> <span data-ttu-id="1e414-138">In other words, a link relationship between an Azure AD user and the related user in Jamf Pro needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1e414-138">In other words, a link relationship between an Azure AD user and the related user in Jamf Pro needs to be established.</span></span>

<span data-ttu-id="1e414-139">To configure and test Azure AD single sign-on with Jamf Pro, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1e414-139">To configure and test Azure AD single sign-on with Jamf Pro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1e414-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1e414-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="1e414-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e414-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="1e414-142">**[Create a Jamf Pro test user](#create-a-jamf-pro-test-user)** - to have a counterpart of Britta Simon in Jamf Pro that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1e414-142">**[Create a Jamf Pro test user](#create-a-jamf-pro-test-user)** - to have a counterpart of Britta Simon in Jamf Pro that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="1e414-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1e414-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="1e414-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1e414-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1e414-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1e414-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1e414-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jamf Pro application.</span><span class="sxs-lookup"><span data-stu-id="1e414-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jamf Pro application.</span></span>

<span data-ttu-id="1e414-147">**To configure Azure AD single sign-on with Jamf Pro, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1e414-147">**To configure Azure AD single sign-on with Jamf Pro, perform the following steps:**</span></span>

1. <span data-ttu-id="1e414-148">In the Azure portal, on the **Jamf Pro** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1e414-148">In the Azure portal, on the **Jamf Pro** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="1e414-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1e414-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/jamfprosamlconnector-tutorial/tutorial_jamfprosamlconnector_samlbase.png)

1. <span data-ttu-id="1e414-152">On the **Jamf Pro Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="1e414-152">On the **Jamf Pro Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Jamf Pro Domain and URLs single sign-on information](./media/jamfprosamlconnector-tutorial/tutorial_jamfprosamlconnector_url.png)

    <span data-ttu-id="1e414-154">a.</span><span class="sxs-lookup"><span data-stu-id="1e414-154">a.</span></span> <span data-ttu-id="1e414-155">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern: `https://<subdomain>.jamfcloud.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="1e414-155">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern: `https://<subdomain>.jamfcloud.com/saml/metadata`</span></span>

    <span data-ttu-id="1e414-156">b.</span><span class="sxs-lookup"><span data-stu-id="1e414-156">b.</span></span> <span data-ttu-id="1e414-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.jamfcloud.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="1e414-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.jamfcloud.com/saml/SSO`</span></span>

1. <span data-ttu-id="1e414-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="1e414-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Jamf Pro Domain and URLs single sign-on information](./media/jamfprosamlconnector-tutorial/tutorial_jamfprosamlconnector_url1.png)

    <span data-ttu-id="1e414-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.jamfcloud.com`</span><span class="sxs-lookup"><span data-stu-id="1e414-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.jamfcloud.com`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="1e414-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1e414-161">These values are not real.</span></span> <span data-ttu-id="1e414-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="1e414-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1e414-163">You will get the actual Identifier value from **Single Sign-On** section in Jamf Pro portal, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="1e414-163">You will get the actual Identifier value from **Single Sign-On** section in Jamf Pro portal, which is explained later in the tutorial.</span></span> <span data-ttu-id="1e414-164">You can extract the actual **subdomain** value from the identifier value and use that **subdomain** information in Sign-on URL and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="1e414-164">You can extract the actual **subdomain** value from the identifier value and use that **subdomain** information in Sign-on URL and Reply URL.</span></span>

1. <span data-ttu-id="1e414-165">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into Notepad.</span><span class="sxs-lookup"><span data-stu-id="1e414-165">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into Notepad.</span></span>

    ![The Certificate download link](./media/jamfprosamlconnector-tutorial/tutorial_jamfprosamlconnector_certificate.png) 

1. <span data-ttu-id="1e414-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1e414-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/jamfprosamlconnector-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="1e414-169">In a different web browser window, log into your Jamf Pro company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1e414-169">In a different web browser window, log into your Jamf Pro company site as an administrator.</span></span>

1. <span data-ttu-id="1e414-170">Click on the **Settings icon** from the top right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="1e414-170">Click on the **Settings icon** from the top right corner of the page.</span></span>

    ![Jamf Pro Configuration](./media/jamfprosamlconnector-tutorial/configure1.png)

1. <span data-ttu-id="1e414-172">Click on **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="1e414-172">Click on **Single Sign On**.</span></span>

    ![Jamf Pro Configuration](./media/jamfprosamlconnector-tutorial/configure2.png)

1. <span data-ttu-id="1e414-174">On the **Single Sign-On** page perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1e414-174">On the **Single Sign-On** page perform the following steps:</span></span>

    ![Jamf Pro single](./media/jamfprosamlconnector-tutorial/tutorial_jamfprosamlconnector_single.png)

    <span data-ttu-id="1e414-176">a.</span><span class="sxs-lookup"><span data-stu-id="1e414-176">a.</span></span> <span data-ttu-id="1e414-177">Select **Jamf Pro Server** to enable Single Sign-On access.</span><span class="sxs-lookup"><span data-stu-id="1e414-177">Select **Jamf Pro Server** to enable Single Sign-On access.</span></span>

    <span data-ttu-id="1e414-178">b.</span><span class="sxs-lookup"><span data-stu-id="1e414-178">b.</span></span> <span data-ttu-id="1e414-179">By selecting **Allow bypass for all users** users will not be redirected to the Identity Provider login page for authentication, but can log in to Jamf Pro directly instead.</span><span class="sxs-lookup"><span data-stu-id="1e414-179">By selecting **Allow bypass for all users** users will not be redirected to the Identity Provider login page for authentication, but can log in to Jamf Pro directly instead.</span></span> <span data-ttu-id="1e414-180">When a user tries to access Jamf Pro via the Identity Provider, IdP-initiated SSO authentication and authorization occurs.</span><span class="sxs-lookup"><span data-stu-id="1e414-180">When a user tries to access Jamf Pro via the Identity Provider, IdP-initiated SSO authentication and authorization occurs.</span></span>

    <span data-ttu-id="1e414-181">c.</span><span class="sxs-lookup"><span data-stu-id="1e414-181">c.</span></span> <span data-ttu-id="1e414-182">Select the **NameID** option for **USER MAPPING: SAML**.</span><span class="sxs-lookup"><span data-stu-id="1e414-182">Select the **NameID** option for **USER MAPPING: SAML**.</span></span> <span data-ttu-id="1e414-183">By default, this setting is set to **NameID** but you may define a custom attribute.</span><span class="sxs-lookup"><span data-stu-id="1e414-183">By default, this setting is set to **NameID** but you may define a custom attribute.</span></span>

    <span data-ttu-id="1e414-184">d.</span><span class="sxs-lookup"><span data-stu-id="1e414-184">d.</span></span> <span data-ttu-id="1e414-185">Select **Email** for **USER MAPPING: JAMF PRO**.</span><span class="sxs-lookup"><span data-stu-id="1e414-185">Select **Email** for **USER MAPPING: JAMF PRO**.</span></span> <span data-ttu-id="1e414-186">Jamf Pro maps SAML attributes sent by the IdP in the following ways: by users and by groups.</span><span class="sxs-lookup"><span data-stu-id="1e414-186">Jamf Pro maps SAML attributes sent by the IdP in the following ways: by users and by groups.</span></span> <span data-ttu-id="1e414-187">When a user tries to access Jamf Pro, by default Jamf Pro gets information about the user from the Identity Provider and matches it against Jamf Pro user accounts.</span><span class="sxs-lookup"><span data-stu-id="1e414-187">When a user tries to access Jamf Pro, by default Jamf Pro gets information about the user from the Identity Provider and matches it against Jamf Pro user accounts.</span></span> <span data-ttu-id="1e414-188">If the incoming user account does not exist in Jamf Pro, then group name matching occurs.</span><span class="sxs-lookup"><span data-stu-id="1e414-188">If the incoming user account does not exist in Jamf Pro, then group name matching occurs.</span></span>

    <span data-ttu-id="1e414-189">e.</span><span class="sxs-lookup"><span data-stu-id="1e414-189">e.</span></span> <span data-ttu-id="1e414-190">Paste the value `http://schemas.microsoft.com/ws/2008/06/identity/claims/groups` in the **GROUP ATTRIBUTE NAME** textbox.</span><span class="sxs-lookup"><span data-stu-id="1e414-190">Paste the value `http://schemas.microsoft.com/ws/2008/06/identity/claims/groups` in the **GROUP ATTRIBUTE NAME** textbox.</span></span>
 
1. <span data-ttu-id="1e414-191">On the same page scroll down upto **IDENTITY PROVIDER** under the **Single Sign-On** section and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1e414-191">On the same page scroll down upto **IDENTITY PROVIDER** under the **Single Sign-On** section and perform the following steps:</span></span>

    ![Jamf Pro Configuration](./media/jamfprosamlconnector-tutorial/configure3.png)

    <span data-ttu-id="1e414-193">a.</span><span class="sxs-lookup"><span data-stu-id="1e414-193">a.</span></span> <span data-ttu-id="1e414-194">Select **Other** as a option from the **IDENTITY PROVIDER** dropdown.</span><span class="sxs-lookup"><span data-stu-id="1e414-194">Select **Other** as a option from the **IDENTITY PROVIDER** dropdown.</span></span>

    <span data-ttu-id="1e414-195">b.</span><span class="sxs-lookup"><span data-stu-id="1e414-195">b.</span></span> <span data-ttu-id="1e414-196">In the **OTHER PROVIDER** textbox, enter **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="1e414-196">In the **OTHER PROVIDER** textbox, enter **Azure AD**.</span></span>

    <span data-ttu-id="1e414-197">c.</span><span class="sxs-lookup"><span data-stu-id="1e414-197">c.</span></span> <span data-ttu-id="1e414-198">Select **Metadata URL** as a option from the **IDENTITY PROVIDER METADATA SOURCE** dropdown and in the following textbox, paste the **App Federation Metadata Url** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e414-198">Select **Metadata URL** as a option from the **IDENTITY PROVIDER METADATA SOURCE** dropdown and in the following textbox, paste the **App Federation Metadata Url** value which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="1e414-199">d.</span><span class="sxs-lookup"><span data-stu-id="1e414-199">d.</span></span> <span data-ttu-id="1e414-200">Copy the **Entity ID** value and paste it into the **Identifier (Entity ID)** textbox in **Jamf Pro Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e414-200">Copy the **Entity ID** value and paste it into the **Identifier (Entity ID)** textbox in **Jamf Pro Domain and URLs** section on Azure portal.</span></span>

    >[!NOTE]
    > <span data-ttu-id="1e414-201">Here blurred value is the subdomain part .Use this value to complete the Sign-on URL and Reply URL in the **Jamf Pro Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e414-201">Here blurred value is the subdomain part .Use this value to complete the Sign-on URL and Reply URL in the **Jamf Pro Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="1e414-202">e.</span><span class="sxs-lookup"><span data-stu-id="1e414-202">e.</span></span> <span data-ttu-id="1e414-203">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1e414-203">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1e414-204">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1e414-204">Create an Azure AD test user</span></span>

<span data-ttu-id="1e414-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e414-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="1e414-207">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1e414-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1e414-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="1e414-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/jamfprosamlconnector-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="1e414-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1e414-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/jamfprosamlconnector-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="1e414-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="1e414-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/jamfprosamlconnector-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="1e414-214">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1e414-214">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/jamfprosamlconnector-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1e414-216">a.</span><span class="sxs-lookup"><span data-stu-id="1e414-216">a.</span></span> <span data-ttu-id="1e414-217">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e414-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e414-218">b.</span><span class="sxs-lookup"><span data-stu-id="1e414-218">b.</span></span> <span data-ttu-id="1e414-219">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e414-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1e414-220">c.</span><span class="sxs-lookup"><span data-stu-id="1e414-220">c.</span></span> <span data-ttu-id="1e414-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="1e414-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1e414-222">d.</span><span class="sxs-lookup"><span data-stu-id="1e414-222">d.</span></span> <span data-ttu-id="1e414-223">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1e414-223">Click **Create**.</span></span>
 
### <a name="create-a-jamf-pro-test-user"></a><span data-ttu-id="1e414-224">Create a Jamf Pro test user</span><span class="sxs-lookup"><span data-stu-id="1e414-224">Create a Jamf Pro test user</span></span>

<span data-ttu-id="1e414-225">To enable Azure AD users to log in to Jamf Pro, they must be provisioned into Jamf Pro.</span><span class="sxs-lookup"><span data-stu-id="1e414-225">To enable Azure AD users to log in to Jamf Pro, they must be provisioned into Jamf Pro.</span></span> <span data-ttu-id="1e414-226">In the case of Jamf Pro, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="1e414-226">In the case of Jamf Pro, provisioning is a manual task.</span></span>

<span data-ttu-id="1e414-227">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1e414-227">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1e414-228">Log in to your Jamf Pro company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1e414-228">Log in to your Jamf Pro company site as an administrator.</span></span>

1. <span data-ttu-id="1e414-229">Click on the **Settings icon** from the top right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="1e414-229">Click on the **Settings icon** from the top right corner of the page.</span></span>

    ![Add Employee](./media/jamfprosamlconnector-tutorial/configure1.png)

1. <span data-ttu-id="1e414-231">Click on **Jamf Pro User Accounts & Groups**.</span><span class="sxs-lookup"><span data-stu-id="1e414-231">Click on **Jamf Pro User Accounts & Groups**.</span></span>

    ![Add Employee](./media/jamfprosamlconnector-tutorial/user1.png)

1. <span data-ttu-id="1e414-233">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="1e414-233">Click **New**.</span></span>

    ![Add Employee](./media/jamfprosamlconnector-tutorial/user2.png)

1. <span data-ttu-id="1e414-235">Select **Create Standard Account**.</span><span class="sxs-lookup"><span data-stu-id="1e414-235">Select **Create Standard Account**.</span></span>

    ![Add Employee](./media/jamfprosamlconnector-tutorial/user3.png)

1. <span data-ttu-id="1e414-237">On the **New Account** dailog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1e414-237">On the **New Account** dailog, perform the following steps:</span></span>

    ![Add Employee](./media/jamfprosamlconnector-tutorial/user4.png)

    <span data-ttu-id="1e414-239">a.</span><span class="sxs-lookup"><span data-stu-id="1e414-239">a.</span></span> <span data-ttu-id="1e414-240">In the **USERNAME** textbox, type the full name of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e414-240">In the **USERNAME** textbox, type the full name of BrittaSimon.</span></span>

    <span data-ttu-id="1e414-241">b.</span><span class="sxs-lookup"><span data-stu-id="1e414-241">b.</span></span> <span data-ttu-id="1e414-242">Select appropriate options as per your organization for **ACCESS LEVEL**, **PRIVILEGE SET**, and for **ACCESS STATUS**.</span><span class="sxs-lookup"><span data-stu-id="1e414-242">Select appropriate options as per your organization for **ACCESS LEVEL**, **PRIVILEGE SET**, and for **ACCESS STATUS**.</span></span>
    
    <span data-ttu-id="1e414-243">c.</span><span class="sxs-lookup"><span data-stu-id="1e414-243">c.</span></span> <span data-ttu-id="1e414-244">In the **FULL NAME** textbox, type the full name of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e414-244">In the **FULL NAME** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="1e414-245">d.</span><span class="sxs-lookup"><span data-stu-id="1e414-245">d.</span></span> <span data-ttu-id="1e414-246">In the **EMAIL ADDRESS** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="1e414-246">In the **EMAIL ADDRESS** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="1e414-247">e.</span><span class="sxs-lookup"><span data-stu-id="1e414-247">e.</span></span> <span data-ttu-id="1e414-248">In the **PASSWORD** textbox, type the password of the user.</span><span class="sxs-lookup"><span data-stu-id="1e414-248">In the **PASSWORD** textbox, type the password of the user.</span></span>

    <span data-ttu-id="1e414-249">f.</span><span class="sxs-lookup"><span data-stu-id="1e414-249">f.</span></span> <span data-ttu-id="1e414-250">In the **VERIFY PASSWORD** textbox, type the password of the user.</span><span class="sxs-lookup"><span data-stu-id="1e414-250">In the **VERIFY PASSWORD** textbox, type the password of the user.</span></span>

    <span data-ttu-id="1e414-251">g.</span><span class="sxs-lookup"><span data-stu-id="1e414-251">g.</span></span> <span data-ttu-id="1e414-252">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1e414-252">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1e414-253">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1e414-253">Assign the Azure AD test user</span></span>

<span data-ttu-id="1e414-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jamf Pro.</span><span class="sxs-lookup"><span data-stu-id="1e414-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jamf Pro.</span></span>

![Assign the user role][200] 

<span data-ttu-id="1e414-256">**To assign Britta Simon to Jamf Pro, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1e414-256">**To assign Britta Simon to Jamf Pro, perform the following steps:**</span></span>

1. <span data-ttu-id="1e414-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1e414-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="1e414-259">In the applications list, select **Jamf Pro**.</span><span class="sxs-lookup"><span data-stu-id="1e414-259">In the applications list, select **Jamf Pro**.</span></span>

    ![The Jamf Pro link in the Applications list](./media/jamfprosamlconnector-tutorial/tutorial_jamfprosamlconnector_app.png)  

1. <span data-ttu-id="1e414-261">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1e414-261">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="1e414-263">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1e414-263">Click **Add** button.</span></span> <span data-ttu-id="1e414-264">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1e414-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="1e414-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1e414-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="1e414-267">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1e414-267">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="1e414-268">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1e414-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1e414-269">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1e414-269">Test single sign-on</span></span>

<span data-ttu-id="1e414-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1e414-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1e414-271">When you click the Jamf Pro tile in the Access Panel, you should get automatically signed-on to your Jamf Pro application.</span><span class="sxs-lookup"><span data-stu-id="1e414-271">When you click the Jamf Pro tile in the Access Panel, you should get automatically signed-on to your Jamf Pro application.</span></span>
<span data-ttu-id="1e414-272">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e414-272">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1e414-273">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1e414-273">Additional resources</span></span>

* [<span data-ttu-id="1e414-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e414-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1e414-275">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e414-275">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/jamfprosamlconnector-tutorial/tutorial_general_01.png
[2]: ./media/jamfprosamlconnector-tutorial/tutorial_general_02.png
[3]: ./media/jamfprosamlconnector-tutorial/tutorial_general_03.png
[4]: ./media/jamfprosamlconnector-tutorial/tutorial_general_04.png

[100]: ./media/jamfprosamlconnector-tutorial/tutorial_general_100.png

[200]: ./media/jamfprosamlconnector-tutorial/tutorial_general_200.png
[201]: ./media/jamfprosamlconnector-tutorial/tutorial_general_201.png
[202]: ./media/jamfprosamlconnector-tutorial/tutorial_general_202.png
[203]: ./media/jamfprosamlconnector-tutorial/tutorial_general_203.png

