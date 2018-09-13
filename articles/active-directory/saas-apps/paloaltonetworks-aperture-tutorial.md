---
title: 'Tutorial: Azure Active Directory integration with Palo Alto Networks - Aperture | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Palo Alto Networks - Aperture.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a5ea18d3-3aaf-4bc6-957c-783e9371d0f1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2018
ms.author: jeedes
ms.openlocfilehash: 7bb4782fa390ad2cc324a79a1f544c3db062c921
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866550"
---
# <a name="tutorial-azure-active-directory-integration-with-palo-alto-networks---aperture"></a><span data-ttu-id="91cc9-103">Tutorial: Azure Active Directory integration with Palo Alto Networks - Aperture</span><span class="sxs-lookup"><span data-stu-id="91cc9-103">Tutorial: Azure Active Directory integration with Palo Alto Networks - Aperture</span></span>

<span data-ttu-id="91cc9-104">In this tutorial, you learn how to integrate Palo Alto Networks - Aperture with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91cc9-104">In this tutorial, you learn how to integrate Palo Alto Networks - Aperture with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91cc9-105">Integrating Palo Alto Networks - Aperture with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="91cc9-105">Integrating Palo Alto Networks - Aperture with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="91cc9-106">You can control in Azure AD who has access to Palo Alto Networks - Aperture.</span><span class="sxs-lookup"><span data-stu-id="91cc9-106">You can control in Azure AD who has access to Palo Alto Networks - Aperture.</span></span>
- <span data-ttu-id="91cc9-107">You can enable your users to automatically get signed-on to Palo Alto Networks - Aperture (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="91cc9-107">You can enable your users to automatically get signed-on to Palo Alto Networks - Aperture (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="91cc9-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91cc9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="91cc9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="91cc9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91cc9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91cc9-110">Prerequisites</span></span>

<span data-ttu-id="91cc9-111">To configure Azure AD integration with Palo Alto Networks - Aperture, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="91cc9-111">To configure Azure AD integration with Palo Alto Networks - Aperture, you need the following items:</span></span>

- <span data-ttu-id="91cc9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="91cc9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91cc9-113">A Palo Alto Networks - Aperture single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="91cc9-113">A Palo Alto Networks - Aperture single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91cc9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="91cc9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91cc9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="91cc9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91cc9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="91cc9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91cc9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91cc9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91cc9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="91cc9-118">Scenario description</span></span>
<span data-ttu-id="91cc9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="91cc9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91cc9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="91cc9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91cc9-121">Adding Palo Alto Networks - Aperture from the gallery</span><span class="sxs-lookup"><span data-stu-id="91cc9-121">Adding Palo Alto Networks - Aperture from the gallery</span></span>
1. <span data-ttu-id="91cc9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91cc9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-palo-alto-networks---aperture-from-the-gallery"></a><span data-ttu-id="91cc9-123">Adding Palo Alto Networks - Aperture from the gallery</span><span class="sxs-lookup"><span data-stu-id="91cc9-123">Adding Palo Alto Networks - Aperture from the gallery</span></span>
<span data-ttu-id="91cc9-124">To configure the integration of Palo Alto Networks - Aperture into Azure AD, you need to add Palo Alto Networks - Aperture from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="91cc9-124">To configure the integration of Palo Alto Networks - Aperture into Azure AD, you need to add Palo Alto Networks - Aperture from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91cc9-125">**To add Palo Alto Networks - Aperture from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91cc9-125">**To add Palo Alto Networks - Aperture from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="91cc9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="91cc9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="91cc9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="91cc9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="91cc9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="91cc9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="91cc9-133">In the search box, type **Palo Alto Networks - Aperture**, select **Palo Alto Networks - Aperture** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="91cc9-133">In the search box, type **Palo Alto Networks - Aperture**, select **Palo Alto Networks - Aperture** from result panel then click **Add** button to add the application.</span></span>

    ![Palo Alto Networks - Aperture in the results list](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="91cc9-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91cc9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="91cc9-136">In this section, you configure and test Azure AD single sign-on with Palo Alto Networks - Aperture based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="91cc9-136">In this section, you configure and test Azure AD single sign-on with Palo Alto Networks - Aperture based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91cc9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Palo Alto Networks - Aperture is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91cc9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Palo Alto Networks - Aperture is to a user in Azure AD.</span></span> <span data-ttu-id="91cc9-138">In other words, a link relationship between an Azure AD user and the related user in Palo Alto Networks - Aperture needs to be established.</span><span class="sxs-lookup"><span data-stu-id="91cc9-138">In other words, a link relationship between an Azure AD user and the related user in Palo Alto Networks - Aperture needs to be established.</span></span>

<span data-ttu-id="91cc9-139">To configure and test Azure AD single sign-on with Palo Alto Networks - Aperture, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="91cc9-139">To configure and test Azure AD single sign-on with Palo Alto Networks - Aperture, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="91cc9-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="91cc9-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="91cc9-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91cc9-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="91cc9-142">**[Create a Palo Alto Networks - Aperture test user](#create-a-palo-alto-networks---aperture-test-user)** - to have a counterpart of Britta Simon in Palo Alto Networks - Aperture that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="91cc9-142">**[Create a Palo Alto Networks - Aperture test user](#create-a-palo-alto-networks---aperture-test-user)** - to have a counterpart of Britta Simon in Palo Alto Networks - Aperture that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="91cc9-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91cc9-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="91cc9-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="91cc9-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="91cc9-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91cc9-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="91cc9-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Palo Alto Networks - Aperture application.</span><span class="sxs-lookup"><span data-stu-id="91cc9-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Palo Alto Networks - Aperture application.</span></span>

<span data-ttu-id="91cc9-147">**To configure Azure AD single sign-on with Palo Alto Networks - Aperture, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91cc9-147">**To configure Azure AD single sign-on with Palo Alto Networks - Aperture, perform the following steps:**</span></span>

1. <span data-ttu-id="91cc9-148">In the Azure portal, on the **Palo Alto Networks - Aperture** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-148">In the Azure portal, on the **Palo Alto Networks - Aperture** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="91cc9-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91cc9-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_samlbase.png)

1. <span data-ttu-id="91cc9-152">On the **Palo Alto Networks - Aperture Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="91cc9-152">On the **Palo Alto Networks - Aperture Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Palo Alto Networks - Aperture Domain and URLs single sign-on information](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_url.png)

    <span data-ttu-id="91cc9-154">a.</span><span class="sxs-lookup"><span data-stu-id="91cc9-154">a.</span></span> <span data-ttu-id="91cc9-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="91cc9-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/metadata`</span></span>

    <span data-ttu-id="91cc9-156">b.</span><span class="sxs-lookup"><span data-stu-id="91cc9-156">b.</span></span> <span data-ttu-id="91cc9-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="91cc9-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/auth`</span></span>

1. <span data-ttu-id="91cc9-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="91cc9-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Palo Alto Networks - Aperture Domain and URLs single sign-on information](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_url1.png)

    <span data-ttu-id="91cc9-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/sign_in`</span><span class="sxs-lookup"><span data-stu-id="91cc9-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/sign_in`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="91cc9-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="91cc9-161">These values are not real.</span></span> <span data-ttu-id="91cc9-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="91cc9-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="91cc9-163">Contact [Palo Alto Networks - Aperture Client support team](https://live.paloaltonetworks.com/t5/custom/page/page-id/Support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="91cc9-163">Contact [Palo Alto Networks - Aperture Client support team](https://live.paloaltonetworks.com/t5/custom/page/page-id/Support) to get these values.</span></span> 

1. <span data-ttu-id="91cc9-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="91cc9-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_certificate.png) 

1. <span data-ttu-id="91cc9-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="91cc9-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/paloaltonetworks-aperture-tutorial/tutorial_general_400.png)


1. <span data-ttu-id="91cc9-168">On the **Palo Alto Networks - Aperture Configuration** section, click **Configure Palo Alto Networks - Aperture** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="91cc9-168">On the **Palo Alto Networks - Aperture Configuration** section, click **Configure Palo Alto Networks - Aperture** to open **Configure sign-on** window.</span></span> <span data-ttu-id="91cc9-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="91cc9-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![The configure link](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_configure.png)

1. <span data-ttu-id="91cc9-171">In a different web browser window, login to Palo Alto Networks - Aperture as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="91cc9-171">In a different web browser window, login to Palo Alto Networks - Aperture as an Administrator.</span></span>

1. <span data-ttu-id="91cc9-172">On the top menu bar, click **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-172">On the top menu bar, click **SETTINGS**.</span></span>

    ![The settings tab](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_settings.png)

1. <span data-ttu-id="91cc9-174">Navigate to **APPLICATION** section click **Authentication** form the left side of menu.</span><span class="sxs-lookup"><span data-stu-id="91cc9-174">Navigate to **APPLICATION** section click **Authentication** form the left side of menu.</span></span>

    ![The Auth tab](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_auth.png)
    
1. <span data-ttu-id="91cc9-176">On the **Authentication** page perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91cc9-176">On the **Authentication** page perform the following steps:</span></span>
    
    ![The authentication tab](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_singlesignon.png)

    <span data-ttu-id="91cc9-178">a.</span><span class="sxs-lookup"><span data-stu-id="91cc9-178">a.</span></span> <span data-ttu-id="91cc9-179">Check the **Enable Single Sign-On(Supported SSP Providers are Okta, Onelogin)** from **Single Sign-On** field.</span><span class="sxs-lookup"><span data-stu-id="91cc9-179">Check the **Enable Single Sign-On(Supported SSP Providers are Okta, Onelogin)** from **Single Sign-On** field.</span></span>

    <span data-ttu-id="91cc9-180">b.</span><span class="sxs-lookup"><span data-stu-id="91cc9-180">b.</span></span> <span data-ttu-id="91cc9-181">In the **Identity Provider ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91cc9-181">In the **Identity Provider ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="91cc9-182">c.</span><span class="sxs-lookup"><span data-stu-id="91cc9-182">c.</span></span> <span data-ttu-id="91cc9-183">Click **Choose File** to upload the downloaded Certificate from Azure AD in the **Identity Provider Certificate** field.</span><span class="sxs-lookup"><span data-stu-id="91cc9-183">Click **Choose File** to upload the downloaded Certificate from Azure AD in the **Identity Provider Certificate** field.</span></span>

    <span data-ttu-id="91cc9-184">d.</span><span class="sxs-lookup"><span data-stu-id="91cc9-184">d.</span></span> <span data-ttu-id="91cc9-185">In the **Identity Provider SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91cc9-185">In the **Identity Provider SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="91cc9-186">e.</span><span class="sxs-lookup"><span data-stu-id="91cc9-186">e.</span></span> <span data-ttu-id="91cc9-187">Review the IdP information from **Aperture Info** section and download the certificate from **Aperture Key** field.</span><span class="sxs-lookup"><span data-stu-id="91cc9-187">Review the IdP information from **Aperture Info** section and download the certificate from **Aperture Key** field.</span></span>

    <span data-ttu-id="91cc9-188">f.</span><span class="sxs-lookup"><span data-stu-id="91cc9-188">f.</span></span> <span data-ttu-id="91cc9-189">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="91cc9-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="91cc9-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="91cc9-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="91cc9-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="91cc9-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91cc9-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="91cc9-193">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="91cc9-193">Create an Azure AD test user</span></span>

<span data-ttu-id="91cc9-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91cc9-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="91cc9-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91cc9-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="91cc9-197">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="91cc9-197">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/paloaltonetworks-aperture-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="91cc9-199">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-199">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/paloaltonetworks-aperture-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="91cc9-201">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="91cc9-201">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/paloaltonetworks-aperture-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="91cc9-203">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91cc9-203">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/paloaltonetworks-aperture-tutorial/create_aaduser_04.png)

    <span data-ttu-id="91cc9-205">a.</span><span class="sxs-lookup"><span data-stu-id="91cc9-205">a.</span></span> <span data-ttu-id="91cc9-206">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-206">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91cc9-207">b.</span><span class="sxs-lookup"><span data-stu-id="91cc9-207">b.</span></span> <span data-ttu-id="91cc9-208">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91cc9-208">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="91cc9-209">c.</span><span class="sxs-lookup"><span data-stu-id="91cc9-209">c.</span></span> <span data-ttu-id="91cc9-210">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="91cc9-210">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="91cc9-211">d.</span><span class="sxs-lookup"><span data-stu-id="91cc9-211">d.</span></span> <span data-ttu-id="91cc9-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-212">Click **Create**.</span></span>
 
### <a name="create-a-palo-alto-networks---aperture-test-user"></a><span data-ttu-id="91cc9-213">Create a Palo Alto Networks - Aperture test user</span><span class="sxs-lookup"><span data-stu-id="91cc9-213">Create a Palo Alto Networks - Aperture test user</span></span>

<span data-ttu-id="91cc9-214">In this section, you create a user called Britta Simon in Palo Alto Networks - Aperture.</span><span class="sxs-lookup"><span data-stu-id="91cc9-214">In this section, you create a user called Britta Simon in Palo Alto Networks - Aperture.</span></span> <span data-ttu-id="91cc9-215">Work with [Palo Alto Networks - Aperture Client support team](https://live.paloaltonetworks.com/t5/custom/page/page-id/Support) to add the users in the Palo Alto Networks - Aperture platform.</span><span class="sxs-lookup"><span data-stu-id="91cc9-215">Work with [Palo Alto Networks - Aperture Client support team](https://live.paloaltonetworks.com/t5/custom/page/page-id/Support) to add the users in the Palo Alto Networks - Aperture platform.</span></span> <span data-ttu-id="91cc9-216">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91cc9-216">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="91cc9-217">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="91cc9-217">Assign the Azure AD test user</span></span>

<span data-ttu-id="91cc9-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Palo Alto Networks - Aperture.</span><span class="sxs-lookup"><span data-stu-id="91cc9-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Palo Alto Networks - Aperture.</span></span>

![Assign the user role][200] 

<span data-ttu-id="91cc9-220">**To assign Britta Simon to Palo Alto Networks - Aperture, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91cc9-220">**To assign Britta Simon to Palo Alto Networks - Aperture, perform the following steps:**</span></span>

1. <span data-ttu-id="91cc9-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="91cc9-223">In the applications list, select **Palo Alto Networks - Aperture**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-223">In the applications list, select **Palo Alto Networks - Aperture**.</span></span>

    ![The Palo Alto Networks - Aperture link in the Applications list](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_app.png)  

1. <span data-ttu-id="91cc9-225">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="91cc9-225">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="91cc9-227">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="91cc9-227">Click **Add** button.</span></span> <span data-ttu-id="91cc9-228">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="91cc9-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="91cc9-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="91cc9-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="91cc9-231">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="91cc9-231">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="91cc9-232">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="91cc9-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="91cc9-233">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="91cc9-233">Test single sign-on</span></span>

<span data-ttu-id="91cc9-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="91cc9-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="91cc9-235">When you click the Palo Alto Networks - Aperture tile in the Access Panel, you should get automatically signed-on to your Palo Alto Networks - Aperture application.</span><span class="sxs-lookup"><span data-stu-id="91cc9-235">When you click the Palo Alto Networks - Aperture tile in the Access Panel, you should get automatically signed-on to your Palo Alto Networks - Aperture application.</span></span>
<span data-ttu-id="91cc9-236">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="91cc9-236">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="91cc9-237">Additional resources</span><span class="sxs-lookup"><span data-stu-id="91cc9-237">Additional resources</span></span>

* [<span data-ttu-id="91cc9-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91cc9-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="91cc9-239">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91cc9-239">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_01.png
[2]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_02.png
[3]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_03.png
[4]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_04.png

[100]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_100.png

[200]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_200.png
[201]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_201.png
[202]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_202.png
[203]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_203.png

