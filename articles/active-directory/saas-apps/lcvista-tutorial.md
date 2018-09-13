---
title: 'Tutorial: Azure Active Directory integration with LCVista | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LCVista.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 1ec1783e6c9caabfbc5e03849b6d4c04b1f33d23
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871703"
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="79672-103">Tutorial: Azure Active Directory integration with LCVista</span><span class="sxs-lookup"><span data-stu-id="79672-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="79672-104">In this tutorial, you learn how to integrate LCVista with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79672-104">In this tutorial, you learn how to integrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79672-105">Integrating LCVista with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="79672-105">Integrating LCVista with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79672-106">You can control in Azure AD who has access to LCVista</span><span class="sxs-lookup"><span data-stu-id="79672-106">You can control in Azure AD who has access to LCVista</span></span>
- <span data-ttu-id="79672-107">You can enable your users to automatically get signed-on to LCVista (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="79672-107">You can enable your users to automatically get signed-on to LCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79672-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="79672-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="79672-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="79672-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79672-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="79672-110">Prerequisites</span></span>

<span data-ttu-id="79672-111">To configure Azure AD integration with LCVista, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="79672-111">To configure Azure AD integration with LCVista, you need the following items:</span></span>

- <span data-ttu-id="79672-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="79672-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79672-113">A LCVista single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="79672-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79672-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="79672-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79672-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="79672-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79672-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="79672-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79672-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79672-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79672-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="79672-118">Scenario description</span></span>
<span data-ttu-id="79672-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="79672-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79672-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="79672-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79672-121">Adding LCVista from the gallery</span><span class="sxs-lookup"><span data-stu-id="79672-121">Adding LCVista from the gallery</span></span>
1. <span data-ttu-id="79672-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="79672-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-the-gallery"></a><span data-ttu-id="79672-123">Adding LCVista from the gallery</span><span class="sxs-lookup"><span data-stu-id="79672-123">Adding LCVista from the gallery</span></span>
<span data-ttu-id="79672-124">To configure the integration of LCVista into Azure AD, you need to add LCVista from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="79672-124">To configure the integration of LCVista into Azure AD, you need to add LCVista from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79672-125">**To add LCVista from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="79672-125">**To add LCVista from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79672-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="79672-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="79672-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="79672-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79672-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="79672-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="79672-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="79672-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="79672-133">In the search box, type **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="79672-133">In the search box, type **LCVista**.</span></span>

    ![Creating an Azure AD test user](./media/lcvista-tutorial/tutorial_lcvista_search.png)

1. <span data-ttu-id="79672-135">In the results panel, select **LCVista**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="79672-135">In the results panel, select **LCVista**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79672-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="79672-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79672-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="79672-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79672-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LCVista is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79672-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LCVista is to a user in Azure AD.</span></span> <span data-ttu-id="79672-140">In other words, a link relationship between an Azure AD user and the related user in LCVista needs to be established.</span><span class="sxs-lookup"><span data-stu-id="79672-140">In other words, a link relationship between an Azure AD user and the related user in LCVista needs to be established.</span></span>

<span data-ttu-id="79672-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LCVista.</span><span class="sxs-lookup"><span data-stu-id="79672-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LCVista.</span></span>

<span data-ttu-id="79672-142">To configure and test Azure AD single sign-on with LCVista, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="79672-142">To configure and test Azure AD single sign-on with LCVista, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79672-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="79672-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="79672-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79672-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="79672-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - to have a counterpart of Britta Simon in LCVista that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="79672-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - to have a counterpart of Britta Simon in LCVista that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="79672-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="79672-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="79672-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="79672-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79672-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="79672-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79672-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LCVista application.</span><span class="sxs-lookup"><span data-stu-id="79672-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="79672-150">**To configure Azure AD single sign-on with LCVista, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="79672-150">**To configure Azure AD single sign-on with LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="79672-151">In the Azure portal, on the **LCVista** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="79672-151">In the Azure portal, on the **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="79672-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="79672-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/lcvista-tutorial/tutorial_lcvista_samlbase.png)

1. <span data-ttu-id="79672-155">On the **LCVista Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="79672-155">On the **LCVista Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="79672-157">a.</span><span class="sxs-lookup"><span data-stu-id="79672-157">a.</span></span> <span data-ttu-id="79672-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="79672-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="79672-159">b.</span><span class="sxs-lookup"><span data-stu-id="79672-159">b.</span></span> <span data-ttu-id="79672-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="79672-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="79672-161">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="79672-161">These values are not the real.</span></span> <span data-ttu-id="79672-162">Update these values with the actual Identifier and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="79672-162">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="79672-163">Contact [LCVista Client support team](https://lcvista.com/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="79672-163">Contact [LCVista Client support team](https://lcvista.com/contact) to get these values.</span></span> 

1. <span data-ttu-id="79672-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="79672-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/lcvista-tutorial/tutorial_lcvista_certificate.png) 

1. <span data-ttu-id="79672-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="79672-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/lcvista-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="79672-168">On the **LCVista Configuration** section, click **Configure LCVista** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="79672-168">On the **LCVista Configuration** section, click **Configure LCVista** to open **Configure sign-on** window.</span></span> <span data-ttu-id="79672-169">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="79672-169">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/lcvista-tutorial/tutorial_lcvista_configure.png) 

1.  <span data-ttu-id="79672-171">Sign on to your LCVista application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="79672-171">Sign on to your LCVista application as an administrator.</span></span>

1. <span data-ttu-id="79672-172">In the **SAML Config** section, check the **Enable SAML login** and enter the details as mentioned in below image.</span><span class="sxs-lookup"><span data-stu-id="79672-172">In the **SAML Config** section, check the **Enable SAML login** and enter the details as mentioned in below image.</span></span> 

    ![Configure Single Sign-On](./media/lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="79672-174">a.</span><span class="sxs-lookup"><span data-stu-id="79672-174">a.</span></span> <span data-ttu-id="79672-175">Paste the **Issuer URL** which you have copied from Azure AD in the **Entity ID** section.</span><span class="sxs-lookup"><span data-stu-id="79672-175">Paste the **Issuer URL** which you have copied from Azure AD in the **Entity ID** section.</span></span> 

    <span data-ttu-id="79672-176">b.</span><span class="sxs-lookup"><span data-stu-id="79672-176">b.</span></span> <span data-ttu-id="79672-177">Paste the **Single Sign-On Service URL** which you have copied from Azure AD in the **URL** section.</span><span class="sxs-lookup"><span data-stu-id="79672-177">Paste the **Single Sign-On Service URL** which you have copied from Azure AD in the **URL** section.</span></span>

    <span data-ttu-id="79672-178">c.</span><span class="sxs-lookup"><span data-stu-id="79672-178">c.</span></span> <span data-ttu-id="79672-179">From Metadata (XML) which you have downloaded from Azure portal, copy the value **X509Certificate** and paste it in the **x509 Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="79672-179">From Metadata (XML) which you have downloaded from Azure portal, copy the value **X509Certificate** and paste it in the **x509 Certificate** section.</span></span>

    <span data-ttu-id="79672-180">d.</span><span class="sxs-lookup"><span data-stu-id="79672-180">d.</span></span> <span data-ttu-id="79672-181">In the **First name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="79672-181">In the **First name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="79672-182">e.</span><span class="sxs-lookup"><span data-stu-id="79672-182">e.</span></span> <span data-ttu-id="79672-183">In the **Last name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="79672-183">In the **Last name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="79672-184">f.</span><span class="sxs-lookup"><span data-stu-id="79672-184">f.</span></span> <span data-ttu-id="79672-185">In the **Email attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="79672-185">In the **Email attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="79672-186">g.</span><span class="sxs-lookup"><span data-stu-id="79672-186">g.</span></span> <span data-ttu-id="79672-187">In the **Username attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="79672-187">In the **Username attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="79672-188">e.</span><span class="sxs-lookup"><span data-stu-id="79672-188">e.</span></span> <span data-ttu-id="79672-189">Click **Save** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="79672-189">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="79672-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="79672-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79672-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="79672-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79672-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79672-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79672-193">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="79672-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="79672-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79672-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="79672-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="79672-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79672-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="79672-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/lcvista-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="79672-199">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="79672-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/lcvista-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="79672-201">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="79672-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/lcvista-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="79672-203">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="79672-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79672-205">a.</span><span class="sxs-lookup"><span data-stu-id="79672-205">a.</span></span> <span data-ttu-id="79672-206">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79672-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79672-207">b.</span><span class="sxs-lookup"><span data-stu-id="79672-207">b.</span></span> <span data-ttu-id="79672-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="79672-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79672-209">c.</span><span class="sxs-lookup"><span data-stu-id="79672-209">c.</span></span> <span data-ttu-id="79672-210">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="79672-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="79672-211">d.</span><span class="sxs-lookup"><span data-stu-id="79672-211">d.</span></span> <span data-ttu-id="79672-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="79672-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="79672-213">Creating a LCVista test user</span><span class="sxs-lookup"><span data-stu-id="79672-213">Creating a LCVista test user</span></span>

<span data-ttu-id="79672-214">In this section, you create a user called Britta Simon in LCVista.</span><span class="sxs-lookup"><span data-stu-id="79672-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="79672-215">You need to contact [LCVista Client support team](https://lcvista.com/contact) to add the users in the LCVista application.</span><span class="sxs-lookup"><span data-stu-id="79672-215">You need to contact [LCVista Client support team](https://lcvista.com/contact) to add the users in the LCVista application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="79672-216">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="79672-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="79672-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LCVista.</span><span class="sxs-lookup"><span data-stu-id="79672-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LCVista.</span></span>

![Assign User][200] 

<span data-ttu-id="79672-219">**To assign Britta Simon to LCVista, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="79672-219">**To assign Britta Simon to LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="79672-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="79672-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="79672-222">In the applications list, select **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="79672-222">In the applications list, select **LCVista**.</span></span>

    ![Configure Single Sign-On](./media/lcvista-tutorial/tutorial_lcvista_app.png) 

1. <span data-ttu-id="79672-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="79672-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="79672-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="79672-226">Click **Add** button.</span></span> <span data-ttu-id="79672-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="79672-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="79672-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="79672-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="79672-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="79672-230">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="79672-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="79672-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79672-232">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="79672-232">Testing single sign-on</span></span>

<span data-ttu-id="79672-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="79672-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="79672-234">Click the LCVista tile in the Access Panel, you will be redirected to Organization sign on page.</span><span class="sxs-lookup"><span data-stu-id="79672-234">Click the LCVista tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="79672-235">After successful login, you will be signed-on to your LCVista application.</span><span class="sxs-lookup"><span data-stu-id="79672-235">After successful login, you will be signed-on to your LCVista application.</span></span> <span data-ttu-id="79672-236">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79672-236">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79672-237">Additional resources</span><span class="sxs-lookup"><span data-stu-id="79672-237">Additional resources</span></span>

* [<span data-ttu-id="79672-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79672-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="79672-239">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79672-239">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/lcvista-tutorial/tutorial_general_01.png
[2]: ./media/lcvista-tutorial/tutorial_general_02.png
[3]: ./media/lcvista-tutorial/tutorial_general_03.png
[4]: ./media/lcvista-tutorial/tutorial_general_04.png

[100]: ./media/lcvista-tutorial/tutorial_general_100.png

[200]: ./media/lcvista-tutorial/tutorial_general_200.png
[201]: ./media/lcvista-tutorial/tutorial_general_201.png
[202]: ./media/lcvista-tutorial/tutorial_general_202.png
[203]: ./media/lcvista-tutorial/tutorial_general_203.png

