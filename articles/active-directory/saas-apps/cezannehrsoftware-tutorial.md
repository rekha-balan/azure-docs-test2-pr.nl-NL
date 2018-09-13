---
title: 'Tutorial: Azure Active Directory integration with Cezanne HR Software | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cezanne HR Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 62b42e15-c282-492d-823a-a7c1c539f2cc
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: jeedes
ms.openlocfilehash: d617b7a1195f322ad33a47ae2fd99b7eb336b7b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871455"
---
# <a name="tutorial-azure-active-directory-integration-with-cezanne-hr-software"></a><span data-ttu-id="1f774-103">Tutorial: Azure Active Directory integration with Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="1f774-103">Tutorial: Azure Active Directory integration with Cezanne HR Software</span></span>

<span data-ttu-id="1f774-104">In this tutorial, you learn how to integrate Cezanne HR Software with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f774-104">In this tutorial, you learn how to integrate Cezanne HR Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f774-105">Integrating Cezanne HR Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1f774-105">Integrating Cezanne HR Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1f774-106">You can control in Azure AD who has access to Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="1f774-106">You can control in Azure AD who has access to Cezanne HR Software.</span></span>
- <span data-ttu-id="1f774-107">You can enable your users to automatically get signed-on to Cezanne HR Software (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="1f774-107">You can enable your users to automatically get signed-on to Cezanne HR Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1f774-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1f774-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1f774-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1f774-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f774-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1f774-110">Prerequisites</span></span>

<span data-ttu-id="1f774-111">To configure Azure AD integration with Cezanne HR Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1f774-111">To configure Azure AD integration with Cezanne HR Software, you need the following items:</span></span>

- <span data-ttu-id="1f774-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1f774-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f774-113">A Cezanne HR Software single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1f774-113">A Cezanne HR Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f774-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1f774-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f774-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1f774-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f774-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1f774-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f774-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f774-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f774-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1f774-118">Scenario description</span></span>
<span data-ttu-id="1f774-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1f774-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f774-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1f774-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f774-121">Adding Cezanne HR Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="1f774-121">Adding Cezanne HR Software from the gallery</span></span>
1. <span data-ttu-id="1f774-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1f774-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cezanne-hr-software-from-the-gallery"></a><span data-ttu-id="1f774-123">Adding Cezanne HR Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="1f774-123">Adding Cezanne HR Software from the gallery</span></span>
<span data-ttu-id="1f774-124">To configure the integration of Cezanne HR Software into Azure AD, you need to add Cezanne HR Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1f774-124">To configure the integration of Cezanne HR Software into Azure AD, you need to add Cezanne HR Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1f774-125">**To add Cezanne HR Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1f774-125">**To add Cezanne HR Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1f774-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1f774-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="1f774-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1f774-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1f774-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1f774-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="1f774-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1f774-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="1f774-133">In the search box, type **Cezanne HR Software**, select **Cezanne HR Software** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1f774-133">In the search box, type **Cezanne HR Software**, select **Cezanne HR Software** from result panel then click **Add** button to add the application.</span></span>

    ![Cezanne HR Software in the results list](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1f774-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1f774-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1f774-136">In this section, you configure and test Azure AD single sign-on with Cezanne HR Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1f774-136">In this section, you configure and test Azure AD single sign-on with Cezanne HR Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1f774-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Cezanne HR Software is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f774-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Cezanne HR Software is to a user in Azure AD.</span></span> <span data-ttu-id="1f774-138">In other words, a link relationship between an Azure AD user and the related user in Cezanne HR Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1f774-138">In other words, a link relationship between an Azure AD user and the related user in Cezanne HR Software needs to be established.</span></span>

<span data-ttu-id="1f774-139">In Cezanne HR Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="1f774-139">In Cezanne HR Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1f774-140">To configure and test Azure AD single sign-on with Cezanne HR Software, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1f774-140">To configure and test Azure AD single sign-on with Cezanne HR Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1f774-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1f774-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="1f774-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f774-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="1f774-143">**[Create a Cezanne HR Software test user](#create-a-cezannehrsoftware-test-user)** - to have a counterpart of Britta Simon in Cezanne HR Software that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1f774-143">**[Create a Cezanne HR Software test user](#create-a-cezannehrsoftware-test-user)** - to have a counterpart of Britta Simon in Cezanne HR Software that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="1f774-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1f774-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="1f774-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1f774-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1f774-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1f774-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1f774-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cezanne HR Software application.</span><span class="sxs-lookup"><span data-stu-id="1f774-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cezanne HR Software application.</span></span>

<span data-ttu-id="1f774-148">**To configure Azure AD single sign-on with Cezanne HR Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1f774-148">**To configure Azure AD single sign-on with Cezanne HR Software, perform the following steps:**</span></span>

1. <span data-ttu-id="1f774-149">In the Azure portal, on the **Cezanne HR Software** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1f774-149">In the Azure portal, on the **Cezanne HR Software** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="1f774-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1f774-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

1. <span data-ttu-id="1f774-153">On the **Cezanne HR Software Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f774-153">On the **Cezanne HR Software Domain and URLs** section, perform the following steps:</span></span>

    ![Cezanne HR Software Domain and URLs single sign-on information](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="1f774-155">a.</span><span class="sxs-lookup"><span data-stu-id="1f774-155">a.</span></span> <span data-ttu-id="1f774-156">In the **Sign-on URL** textbox, type the URL: `https://w3.cezanneondemand.com/CezanneOnDemand/-/<tenantidentifier>`</span><span class="sxs-lookup"><span data-stu-id="1f774-156">In the **Sign-on URL** textbox, type the URL: `https://w3.cezanneondemand.com/CezanneOnDemand/-/<tenantidentifier>`</span></span>

    <span data-ttu-id="1f774-157">b.</span><span class="sxs-lookup"><span data-stu-id="1f774-157">b.</span></span> <span data-ttu-id="1f774-158">In the **Identifier** textbox, type the URL: `https://w3.cezanneondemand.com/CezanneOnDemand/`</span><span class="sxs-lookup"><span data-stu-id="1f774-158">In the **Identifier** textbox, type the URL: `https://w3.cezanneondemand.com/CezanneOnDemand/`</span></span>

    <span data-ttu-id="1f774-159">c.</span><span class="sxs-lookup"><span data-stu-id="1f774-159">c.</span></span> <span data-ttu-id="1f774-160">In the **Reply URL** textbox, type the URL: `https://w3.cezanneondemand.com:443/cezanneondemand/-/<tenantidentifier>/Saml/samlp`</span><span class="sxs-lookup"><span data-stu-id="1f774-160">In the **Reply URL** textbox, type the URL: `https://w3.cezanneondemand.com:443/cezanneondemand/-/<tenantidentifier>/Saml/samlp`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="1f774-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1f774-161">These values are not real.</span></span> <span data-ttu-id="1f774-162">Update these values with the actual Sign-On URL and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="1f774-162">Update these values with the actual Sign-On URL and Reply URL.</span></span> <span data-ttu-id="1f774-163">Contact [Cezanne HR Software Client support team](https://cezannehr.com/services/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1f774-163">Contact [Cezanne HR Software Client support team](https://cezannehr.com/services/support/) to get these values.</span></span>

1. <span data-ttu-id="1f774-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1f774-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

1. <span data-ttu-id="1f774-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1f774-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/cezannehrsoftware-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="1f774-168">On the **Cezanne HR Software Configuration** section, click **Configure Cezanne HR Software** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="1f774-168">On the **Cezanne HR Software Configuration** section, click **Configure Cezanne HR Software** to open **Configure sign-on** window.</span></span>

    ![Cezanne HR Software Configuration](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png)

1. <span data-ttu-id="1f774-170">Scroll down to the **Quick Reference** section.</span><span class="sxs-lookup"><span data-stu-id="1f774-170">Scroll down to the **Quick Reference** section.</span></span> <span data-ttu-id="1f774-171">Copy the **SAML Single Sign-On Service URL and SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="1f774-171">Copy the **SAML Single Sign-On Service URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Cezanne HR Software Configuration](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure1.png)

1. <span data-ttu-id="1f774-173">In a different web browser window, sign-on to your Cezanne HR Software tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1f774-173">In a different web browser window, sign-on to your Cezanne HR Software tenant as an administrator.</span></span>

1. <span data-ttu-id="1f774-174">On the left navigation pane, click **System Setup**.</span><span class="sxs-lookup"><span data-stu-id="1f774-174">On the left navigation pane, click **System Setup**.</span></span> <span data-ttu-id="1f774-175">Go to **Security Settings**.</span><span class="sxs-lookup"><span data-stu-id="1f774-175">Go to **Security Settings**.</span></span> <span data-ttu-id="1f774-176">Then navigate to **Single Sign-On Configuration**.</span><span class="sxs-lookup"><span data-stu-id="1f774-176">Then navigate to **Single Sign-On Configuration**.</span></span>

    ![Configure Single Sign-On On App side](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

1. <span data-ttu-id="1f774-178">In the **Allow users to log in using the following Single Sign-On (SSO) Service** panel, check the **SAML 2.0** box and select the **Advanced Configuration** option.</span><span class="sxs-lookup"><span data-stu-id="1f774-178">In the **Allow users to log in using the following Single Sign-On (SSO) Service** panel, check the **SAML 2.0** box and select the **Advanced Configuration** option.</span></span>

    ![Configure Single Sign-On On App side](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

1. <span data-ttu-id="1f774-180">Click **Add New** button.</span><span class="sxs-lookup"><span data-stu-id="1f774-180">Click **Add New** button.</span></span>

    ![Configure Single Sign-On On App side](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

1. <span data-ttu-id="1f774-182">Perform the following steps on **SAML 2.0 IDENTITY PROVIDERS** section.</span><span class="sxs-lookup"><span data-stu-id="1f774-182">Perform the following steps on **SAML 2.0 IDENTITY PROVIDERS** section.</span></span>

    ![Configure Single Sign-On On App side](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="1f774-184">a.</span><span class="sxs-lookup"><span data-stu-id="1f774-184">a.</span></span> <span data-ttu-id="1f774-185">Enter the name of your Identity Provider as the **Display Name**.</span><span class="sxs-lookup"><span data-stu-id="1f774-185">Enter the name of your Identity Provider as the **Display Name**.</span></span>

    <span data-ttu-id="1f774-186">b.</span><span class="sxs-lookup"><span data-stu-id="1f774-186">b.</span></span> <span data-ttu-id="1f774-187">In the **Entity Identifier** textbox, paste the value of **SAML Entity ID** which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1f774-187">In the **Entity Identifier** textbox, paste the value of **SAML Entity ID** which you have copied from the Azure portal.</span></span> 

    <span data-ttu-id="1f774-188">c.</span><span class="sxs-lookup"><span data-stu-id="1f774-188">c.</span></span> <span data-ttu-id="1f774-189">Change the **SAML Binding** to 'POST'.</span><span class="sxs-lookup"><span data-stu-id="1f774-189">Change the **SAML Binding** to 'POST'.</span></span>

    <span data-ttu-id="1f774-190">d.</span><span class="sxs-lookup"><span data-stu-id="1f774-190">d.</span></span> <span data-ttu-id="1f774-191">In the **Security Token Service Endpoint** textbox, paste the value of **SAML Single Sign-on Service URL** which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1f774-191">In the **Security Token Service Endpoint** textbox, paste the value of **SAML Single Sign-on Service URL** which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="1f774-192">e.</span><span class="sxs-lookup"><span data-stu-id="1f774-192">e.</span></span> <span data-ttu-id="1f774-193">In the User ID Attribute Name textbox, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="1f774-193">In the User ID Attribute Name textbox, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="1f774-194">f.</span><span class="sxs-lookup"><span data-stu-id="1f774-194">f.</span></span> <span data-ttu-id="1f774-195">Click **Upload** icon to upload the downloaded certificate from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1f774-195">Click **Upload** icon to upload the downloaded certificate from Azure portal.</span></span>
    
    <span data-ttu-id="1f774-196">g.</span><span class="sxs-lookup"><span data-stu-id="1f774-196">g.</span></span> <span data-ttu-id="1f774-197">Click the **Ok** button.</span><span class="sxs-lookup"><span data-stu-id="1f774-197">Click the **Ok** button.</span></span> 

1. <span data-ttu-id="1f774-198">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1f774-198">Click **Save** button.</span></span>

    ![Configure Single Sign-On On App side](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="1f774-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="1f774-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1f774-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="1f774-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1f774-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f774-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1f774-203">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1f774-203">Create an Azure AD test user</span></span>

<span data-ttu-id="1f774-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f774-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="1f774-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1f774-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1f774-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="1f774-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/cezannehrsoftware-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="1f774-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1f774-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/cezannehrsoftware-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="1f774-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="1f774-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/cezannehrsoftware-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="1f774-213">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f774-213">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/cezannehrsoftware-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1f774-215">a.</span><span class="sxs-lookup"><span data-stu-id="1f774-215">a.</span></span> <span data-ttu-id="1f774-216">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f774-216">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f774-217">b.</span><span class="sxs-lookup"><span data-stu-id="1f774-217">b.</span></span> <span data-ttu-id="1f774-218">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f774-218">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1f774-219">c.</span><span class="sxs-lookup"><span data-stu-id="1f774-219">c.</span></span> <span data-ttu-id="1f774-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="1f774-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1f774-221">d.</span><span class="sxs-lookup"><span data-stu-id="1f774-221">d.</span></span> <span data-ttu-id="1f774-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1f774-222">Click **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="1f774-223">Create a Cezanne HR Software test user</span><span class="sxs-lookup"><span data-stu-id="1f774-223">Create a Cezanne HR Software test user</span></span>

<span data-ttu-id="1f774-224">In order to enable Azure AD users to log into Cezanne HR Software, they must be provisioned into Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="1f774-224">In order to enable Azure AD users to log into Cezanne HR Software, they must be provisioned into Cezanne HR Software.</span></span> <span data-ttu-id="1f774-225">In the case of Cezanne HR Software, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="1f774-225">In the case of Cezanne HR Software, provisioning is a manual task.</span></span>

<span data-ttu-id="1f774-226">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1f774-226">**To provision a user account, perform the following steps:**</span></span>

1.  <span data-ttu-id="1f774-227">Log into your Cezanne HR Software company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1f774-227">Log into your Cezanne HR Software company site as an administrator.</span></span>

1.  <span data-ttu-id="1f774-228">On the left navigation pane, click **System Setup**.</span><span class="sxs-lookup"><span data-stu-id="1f774-228">On the left navigation pane, click **System Setup**.</span></span> <span data-ttu-id="1f774-229">Go to **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="1f774-229">Go to **Manage Users**.</span></span> <span data-ttu-id="1f774-230">Then navigate to **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="1f774-230">Then navigate to **Add New User**.</span></span>

    <span data-ttu-id="1f774-231">![New User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span><span class="sxs-lookup"><span data-stu-id="1f774-231">![New User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

1.  <span data-ttu-id="1f774-232">On **Person Details** section, perform below steps:</span><span class="sxs-lookup"><span data-stu-id="1f774-232">On **Person Details** section, perform below steps:</span></span>

    <span data-ttu-id="1f774-233">![New User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span><span class="sxs-lookup"><span data-stu-id="1f774-233">![New User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="1f774-234">a.</span><span class="sxs-lookup"><span data-stu-id="1f774-234">a.</span></span> <span data-ttu-id="1f774-235">Set **Internal User** as OFF.</span><span class="sxs-lookup"><span data-stu-id="1f774-235">Set **Internal User** as OFF.</span></span>
    
    <span data-ttu-id="1f774-236">b.</span><span class="sxs-lookup"><span data-stu-id="1f774-236">b.</span></span> <span data-ttu-id="1f774-237">In the **First Name** textbox, type the First Name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1f774-237">In the **First Name** textbox, type the First Name of user like **Britta**.</span></span>  
 
    <span data-ttu-id="1f774-238">c.</span><span class="sxs-lookup"><span data-stu-id="1f774-238">c.</span></span> <span data-ttu-id="1f774-239">In the **Last Name** textbox, type the last Name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1f774-239">In the **Last Name** textbox, type the last Name of user like **Simon**.</span></span>
    
    <span data-ttu-id="1f774-240">d.</span><span class="sxs-lookup"><span data-stu-id="1f774-240">d.</span></span> <span data-ttu-id="1f774-241">In the **E-mail** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1f774-241">In the **E-mail** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

1.  <span data-ttu-id="1f774-242">On **Account Information** section, perform below steps:</span><span class="sxs-lookup"><span data-stu-id="1f774-242">On **Account Information** section, perform below steps:</span></span>

    <span data-ttu-id="1f774-243">![New User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span><span class="sxs-lookup"><span data-stu-id="1f774-243">![New User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="1f774-244">a.</span><span class="sxs-lookup"><span data-stu-id="1f774-244">a.</span></span> <span data-ttu-id="1f774-245">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1f774-245">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="1f774-246">b.</span><span class="sxs-lookup"><span data-stu-id="1f774-246">b.</span></span> <span data-ttu-id="1f774-247">In the **Password** textbox, type the password of user.</span><span class="sxs-lookup"><span data-stu-id="1f774-247">In the **Password** textbox, type the password of user.</span></span>
    
    <span data-ttu-id="1f774-248">c.</span><span class="sxs-lookup"><span data-stu-id="1f774-248">c.</span></span> <span data-ttu-id="1f774-249">Select **HR Professional** as **Security Role**.</span><span class="sxs-lookup"><span data-stu-id="1f774-249">Select **HR Professional** as **Security Role**.</span></span>
    
    <span data-ttu-id="1f774-250">d.</span><span class="sxs-lookup"><span data-stu-id="1f774-250">d.</span></span> <span data-ttu-id="1f774-251">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f774-251">Click **OK**.</span></span>

1. <span data-ttu-id="1f774-252">Navigate to **Single Sign-On** tab and select **Add New** in the **SAML 2.0 Identifiers** area.</span><span class="sxs-lookup"><span data-stu-id="1f774-252">Navigate to **Single Sign-On** tab and select **Add New** in the **SAML 2.0 Identifiers** area.</span></span>

    <span data-ttu-id="1f774-253">![User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span><span class="sxs-lookup"><span data-stu-id="1f774-253">![User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

1. <span data-ttu-id="1f774-254">Choose your Identity Provider for the **Identity Provider** and in the text box of **User Identifier**, enter the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="1f774-254">Choose your Identity Provider for the **Identity Provider** and in the text box of **User Identifier**, enter the email address of Britta Simon account.</span></span>

    <span data-ttu-id="1f774-255">![User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span><span class="sxs-lookup"><span data-stu-id="1f774-255">![User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
1. <span data-ttu-id="1f774-256">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1f774-256">Click **Save** button.</span></span>

    <span data-ttu-id="1f774-257">![User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span><span class="sxs-lookup"><span data-stu-id="1f774-257">![User](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1f774-258">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1f774-258">Assign the Azure AD test user</span></span>

<span data-ttu-id="1f774-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="1f774-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cezanne HR Software.</span></span>

![Assign the user role][200] 

<span data-ttu-id="1f774-261">**To assign Britta Simon to Cezanne HR Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1f774-261">**To assign Britta Simon to Cezanne HR Software, perform the following steps:**</span></span>

1. <span data-ttu-id="1f774-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1f774-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="1f774-264">In the applications list, select **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="1f774-264">In the applications list, select **Cezanne HR Software**.</span></span>

    ![The Cezanne HR Software link in the Applications list](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png)  

1. <span data-ttu-id="1f774-266">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1f774-266">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="1f774-268">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1f774-268">Click **Add** button.</span></span> <span data-ttu-id="1f774-269">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1f774-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="1f774-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1f774-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="1f774-272">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1f774-272">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="1f774-273">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1f774-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1f774-274">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1f774-274">Test single sign-on</span></span>

<span data-ttu-id="1f774-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1f774-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1f774-276">When you click the Cezanne HR Software tile in the Access Panel, you should get automatically signed-on to your Cezanne HR Software application.</span><span class="sxs-lookup"><span data-stu-id="1f774-276">When you click the Cezanne HR Software tile in the Access Panel, you should get automatically signed-on to your Cezanne HR Software application.</span></span>
<span data-ttu-id="1f774-277">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f774-277">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1f774-278">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1f774-278">Additional resources</span></span>

* [<span data-ttu-id="1f774-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f774-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1f774-280">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f774-280">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/cezannehrsoftware-tutorial/tutorial_general_203.png

