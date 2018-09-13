---
title: 'Tutorial: Azure Active Directory integration with GaggleAMP | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and GaggleAMP.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2018
ms.author: jeedes
ms.openlocfilehash: 828dd1e1dcef900a7105143088f6782032b4f22e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968574"
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="1699d-103">Tutorial: Azure Active Directory integration with GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="1699d-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="1699d-104">In this tutorial, you learn how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1699d-104">In this tutorial, you learn how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1699d-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1699d-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1699d-106">You can control in Azure AD who has access to GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="1699d-106">You can control in Azure AD who has access to GaggleAMP</span></span>
- <span data-ttu-id="1699d-107">You can enable your users to automatically get signed-on to GaggleAMP (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1699d-107">You can enable your users to automatically get signed-on to GaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1699d-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1699d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1699d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1699d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1699d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1699d-110">Prerequisites</span></span>

<span data-ttu-id="1699d-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1699d-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span></span>

- <span data-ttu-id="1699d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1699d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1699d-113">A GaggleAMP single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1699d-113">A GaggleAMP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1699d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1699d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1699d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1699d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1699d-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1699d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1699d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1699d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1699d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1699d-118">Scenario description</span></span>
<span data-ttu-id="1699d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1699d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1699d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1699d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1699d-121">Adding GaggleAMP from the gallery</span><span class="sxs-lookup"><span data-stu-id="1699d-121">Adding GaggleAMP from the gallery</span></span>
1. <span data-ttu-id="1699d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1699d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-the-gallery"></a><span data-ttu-id="1699d-123">Adding GaggleAMP from the gallery</span><span class="sxs-lookup"><span data-stu-id="1699d-123">Adding GaggleAMP from the gallery</span></span>
<span data-ttu-id="1699d-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1699d-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1699d-125">**To add GaggleAMP from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1699d-125">**To add GaggleAMP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1699d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1699d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="1699d-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1699d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1699d-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1699d-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="1699d-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1699d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="1699d-133">In the search box, type **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="1699d-133">In the search box, type **GaggleAMP**.</span></span>

    ![Creating an Azure AD test user](./media/gaggleamp-tutorial/tutorial_gaggleamp_search.png)

1. <span data-ttu-id="1699d-135">In the results panel, select **GaggleAMP**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1699d-135">In the results panel, select **GaggleAMP**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1699d-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1699d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1699d-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1699d-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1699d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GaggleAMP is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1699d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GaggleAMP is to a user in Azure AD.</span></span> <span data-ttu-id="1699d-140">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1699d-140">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span></span>

<span data-ttu-id="1699d-141">In GaggleAMP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="1699d-141">In GaggleAMP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1699d-142">To configure and test Azure AD single sign-on with GaggleAMP, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1699d-142">To configure and test Azure AD single sign-on with GaggleAMP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1699d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1699d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="1699d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1699d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="1699d-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1699d-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="1699d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1699d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="1699d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1699d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1699d-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1699d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1699d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GaggleAMP application.</span><span class="sxs-lookup"><span data-stu-id="1699d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="1699d-150">**To configure Azure AD single sign-on with GaggleAMP, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1699d-150">**To configure Azure AD single sign-on with GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="1699d-151">In the Azure portal, on the **GaggleAMP** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1699d-151">In the Azure portal, on the **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="1699d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1699d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

1. <span data-ttu-id="1699d-155">On the **GaggleAMP Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="1699d-155">On the **GaggleAMP Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="1699d-157">In the **Identifier** textbox, type the URL: `https://accounts.gaggleamp.com/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="1699d-157">In the **Identifier** textbox, type the URL: `https://accounts.gaggleamp.com/auth/saml/callback`</span></span>

1. <span data-ttu-id="1699d-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="1699d-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/gaggleamp-tutorial/tutorial_gaggleamp_url1.png)

     <span data-ttu-id="1699d-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://gaggleamp.com/i/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="1699d-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://gaggleamp.com/i/<customerid>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="1699d-161">The Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="1699d-161">The Sign-on URL value is not real.</span></span> <span data-ttu-id="1699d-162">Update this value with the actual Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="1699d-162">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="1699d-163">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="1699d-163">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) to get this value.</span></span>
 
1. <span data-ttu-id="1699d-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1699d-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

1. <span data-ttu-id="1699d-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1699d-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/gaggleamp-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="1699d-168">On the **GaggleAMP Configuration** section, click **Configure GaggleAMP** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="1699d-168">On the **GaggleAMP Configuration** section, click **Configure GaggleAMP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1699d-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="1699d-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

1. <span data-ttu-id="1699d-171">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="1699d-171">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

1. <span data-ttu-id="1699d-172">On your **SAML SSO** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1699d-172">On your **SAML SSO** page, perform the following steps:</span></span>  
   
    ![GaggleAMP Single Sign-On](./media/gaggleamp-tutorial/tutorial_gaggleamp_06.png)

    <span data-ttu-id="1699d-174">a.</span><span class="sxs-lookup"><span data-stu-id="1699d-174">a.</span></span> <span data-ttu-id="1699d-175">Select **Other** form the **Identity provider** dropdown menu.</span><span class="sxs-lookup"><span data-stu-id="1699d-175">Select **Other** form the **Identity provider** dropdown menu.</span></span>
    
    <span data-ttu-id="1699d-176">b.</span><span class="sxs-lookup"><span data-stu-id="1699d-176">b.</span></span> <span data-ttu-id="1699d-177">In the **Identity Provider Issuer** textbox, paste the value of **Issuer URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1699d-177">In the **Identity Provider Issuer** textbox, paste the value of **Issuer URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1699d-178">c.</span><span class="sxs-lookup"><span data-stu-id="1699d-178">c.</span></span> <span data-ttu-id="1699d-179">In the **Identity Provider Single Sign-On URL** textbox, paste the  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1699d-179">In the **Identity Provider Single Sign-On URL** textbox, paste the  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1699d-180">d.</span><span class="sxs-lookup"><span data-stu-id="1699d-180">d.</span></span> <span data-ttu-id="1699d-181">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="1699d-181">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="1699d-182">e.</span><span class="sxs-lookup"><span data-stu-id="1699d-182">e.</span></span> <span data-ttu-id="1699d-183">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1699d-183">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1699d-184">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1699d-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="1699d-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1699d-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="1699d-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1699d-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1699d-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1699d-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/gaggleamp-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="1699d-190">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1699d-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/gaggleamp-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="1699d-192">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="1699d-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/gaggleamp-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="1699d-194">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1699d-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1699d-196">a.</span><span class="sxs-lookup"><span data-stu-id="1699d-196">a.</span></span> <span data-ttu-id="1699d-197">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1699d-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1699d-198">b.</span><span class="sxs-lookup"><span data-stu-id="1699d-198">b.</span></span> <span data-ttu-id="1699d-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1699d-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1699d-200">c.</span><span class="sxs-lookup"><span data-stu-id="1699d-200">c.</span></span> <span data-ttu-id="1699d-201">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="1699d-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1699d-202">d.</span><span class="sxs-lookup"><span data-stu-id="1699d-202">d.</span></span> <span data-ttu-id="1699d-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1699d-203">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="1699d-204">Creating a GaggleAMP test user</span><span class="sxs-lookup"><span data-stu-id="1699d-204">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="1699d-205">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="1699d-205">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="1699d-206">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="1699d-206">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1699d-207">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="1699d-207">There is no action item for you in this section.</span></span> <span data-ttu-id="1699d-208">A new user is created during an attempt to access GaggleAMP if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="1699d-208">A new user is created during an attempt to access GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1699d-209">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1699d-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1699d-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="1699d-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GaggleAMP.</span></span>

![Assign User][200] 

<span data-ttu-id="1699d-212">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1699d-212">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="1699d-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1699d-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="1699d-215">In the applications list, select **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="1699d-215">In the applications list, select **GaggleAMP**.</span></span>

    ![Configure Single Sign-On](./media/gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

1. <span data-ttu-id="1699d-217">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1699d-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="1699d-219">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1699d-219">Click **Add** button.</span></span> <span data-ttu-id="1699d-220">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1699d-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="1699d-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1699d-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="1699d-223">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1699d-223">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="1699d-224">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1699d-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1699d-225">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="1699d-225">Testing single sign-on</span></span>

<span data-ttu-id="1699d-226">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1699d-226">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1699d-227">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span><span class="sxs-lookup"><span data-stu-id="1699d-227">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1699d-228">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1699d-228">Additional resources</span></span>

* [<span data-ttu-id="1699d-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1699d-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1699d-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1699d-230">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/gaggleamp-tutorial/tutorial_general_203.png
