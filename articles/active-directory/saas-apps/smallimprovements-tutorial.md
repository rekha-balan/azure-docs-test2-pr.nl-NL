---
title: 'Tutorial: Azure Active Directory integration with Small Improvements | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Small Improvements.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 48b1e47befa647a9d221e5cdf5bf0485c3b66028
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866906"
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="19864-103">Tutorial: Azure Active Directory integration with Small Improvements</span><span class="sxs-lookup"><span data-stu-id="19864-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="19864-104">In this tutorial, you learn how to integrate Small Improvements with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19864-104">In this tutorial, you learn how to integrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19864-105">Integrating Small Improvements with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="19864-105">Integrating Small Improvements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="19864-106">You can control in Azure AD who has access to Small Improvements</span><span class="sxs-lookup"><span data-stu-id="19864-106">You can control in Azure AD who has access to Small Improvements</span></span>
- <span data-ttu-id="19864-107">You can enable your users to automatically get signed-on to Small Improvements (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="19864-107">You can enable your users to automatically get signed-on to Small Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19864-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="19864-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="19864-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="19864-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19864-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="19864-110">Prerequisites</span></span>

<span data-ttu-id="19864-111">To configure Azure AD integration with Small Improvements, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="19864-111">To configure Azure AD integration with Small Improvements, you need the following items:</span></span>

- <span data-ttu-id="19864-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="19864-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19864-113">A Small Improvements single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="19864-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19864-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="19864-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19864-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="19864-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19864-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="19864-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="19864-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19864-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19864-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="19864-118">Scenario description</span></span>
<span data-ttu-id="19864-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="19864-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19864-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="19864-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19864-121">Adding Small Improvements from the gallery</span><span class="sxs-lookup"><span data-stu-id="19864-121">Adding Small Improvements from the gallery</span></span>
1. <span data-ttu-id="19864-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="19864-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-the-gallery"></a><span data-ttu-id="19864-123">Adding Small Improvements from the gallery</span><span class="sxs-lookup"><span data-stu-id="19864-123">Adding Small Improvements from the gallery</span></span>
<span data-ttu-id="19864-124">To configure the integration of Small Improvements into Azure AD, you need to add Small Improvements from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="19864-124">To configure the integration of Small Improvements into Azure AD, you need to add Small Improvements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="19864-125">**To add Small Improvements from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19864-125">**To add Small Improvements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="19864-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="19864-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="19864-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="19864-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="19864-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="19864-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="19864-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="19864-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="19864-133">In the search box, type **Small Improvements**.</span><span class="sxs-lookup"><span data-stu-id="19864-133">In the search box, type **Small Improvements**.</span></span>

    ![Creating an Azure AD test user](./media/smallimprovements-tutorial/tutorial_smallimprovements_search.png)

1. <span data-ttu-id="19864-135">In the results panel, select **Small Improvements**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="19864-135">In the results panel, select **Small Improvements**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="19864-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="19864-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="19864-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="19864-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="19864-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Small Improvements is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19864-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Small Improvements is to a user in Azure AD.</span></span> <span data-ttu-id="19864-140">In other words, a link relationship between an Azure AD user and the related user in Small Improvements needs to be established.</span><span class="sxs-lookup"><span data-stu-id="19864-140">In other words, a link relationship between an Azure AD user and the related user in Small Improvements needs to be established.</span></span>

<span data-ttu-id="19864-141">In Small Improvements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="19864-141">In Small Improvements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="19864-142">To configure and test Azure AD single sign-on with Small Improvements, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="19864-142">To configure and test Azure AD single sign-on with Small Improvements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="19864-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="19864-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="19864-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19864-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="19864-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - to have a counterpart of Britta Simon in Small Improvements that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="19864-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - to have a counterpart of Britta Simon in Small Improvements that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="19864-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="19864-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="19864-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="19864-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="19864-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="19864-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="19864-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Small Improvements application.</span><span class="sxs-lookup"><span data-stu-id="19864-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="19864-150">**To configure Azure AD single sign-on with Small Improvements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19864-150">**To configure Azure AD single sign-on with Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="19864-151">In the Azure portal, on the **Small Improvements** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="19864-151">In the Azure portal, on the **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="19864-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="19864-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

1. <span data-ttu-id="19864-155">On the **Small Improvements Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19864-155">On the **Small Improvements Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="19864-157">a.</span><span class="sxs-lookup"><span data-stu-id="19864-157">a.</span></span> <span data-ttu-id="19864-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="19864-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="19864-159">b.</span><span class="sxs-lookup"><span data-stu-id="19864-159">b.</span></span> <span data-ttu-id="19864-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="19864-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="19864-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="19864-161">These values are not real.</span></span> <span data-ttu-id="19864-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="19864-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="19864-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="19864-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) to get these values.</span></span> 
 
1. <span data-ttu-id="19864-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="19864-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

1. <span data-ttu-id="19864-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="19864-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/smallimprovements-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="19864-168">On the **Small Improvements Configuration** section, click **Configure Small Improvements** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="19864-168">On the **Small Improvements Configuration** section, click **Configure Small Improvements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="19864-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="19864-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

1. <span data-ttu-id="19864-171">In another browser window, sign on to your Small Improvements company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="19864-171">In another browser window, sign on to your Small Improvements company site as an administrator.</span></span>

1. <span data-ttu-id="19864-172">From the main dashboard page, click **Administration** button on the left.</span><span class="sxs-lookup"><span data-stu-id="19864-172">From the main dashboard page, click **Administration** button on the left.</span></span>
   
    ![Configure Single Sign-On](./media/smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

1. <span data-ttu-id="19864-174">Click the **SAML SSO** button from **Integrations** section.</span><span class="sxs-lookup"><span data-stu-id="19864-174">Click the **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Configure Single Sign-On](./media/smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

1. <span data-ttu-id="19864-176">On the SSO Setup page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19864-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="19864-178">a.</span><span class="sxs-lookup"><span data-stu-id="19864-178">a.</span></span> <span data-ttu-id="19864-179">In the **HTTP Endpoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="19864-179">In the **HTTP Endpoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="19864-180">b.</span><span class="sxs-lookup"><span data-stu-id="19864-180">b.</span></span> <span data-ttu-id="19864-181">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **x509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="19864-181">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="19864-182">c.</span><span class="sxs-lookup"><span data-stu-id="19864-182">c.</span></span> <span data-ttu-id="19864-183">If you wish to have SSO and Login form authentication option available for users, then check the **Enable access via login/password too** option.</span><span class="sxs-lookup"><span data-stu-id="19864-183">If you wish to have SSO and Login form authentication option available for users, then check the **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="19864-184">d.</span><span class="sxs-lookup"><span data-stu-id="19864-184">d.</span></span> <span data-ttu-id="19864-185">Enter the appropriate value to Name the SSO Login button in the **SAML Prompt** textbox.</span><span class="sxs-lookup"><span data-stu-id="19864-185">Enter the appropriate value to Name the SSO Login button in the **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="19864-186">e.</span><span class="sxs-lookup"><span data-stu-id="19864-186">e.</span></span> <span data-ttu-id="19864-187">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="19864-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="19864-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="19864-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="19864-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="19864-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="19864-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="19864-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="19864-191">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="19864-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="19864-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19864-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="19864-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19864-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="19864-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="19864-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/smallimprovements-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="19864-197">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="19864-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/smallimprovements-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="19864-199">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="19864-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/smallimprovements-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="19864-201">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19864-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19864-203">a.</span><span class="sxs-lookup"><span data-stu-id="19864-203">a.</span></span> <span data-ttu-id="19864-204">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="19864-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19864-205">b.</span><span class="sxs-lookup"><span data-stu-id="19864-205">b.</span></span> <span data-ttu-id="19864-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="19864-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19864-207">c.</span><span class="sxs-lookup"><span data-stu-id="19864-207">c.</span></span> <span data-ttu-id="19864-208">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="19864-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="19864-209">d.</span><span class="sxs-lookup"><span data-stu-id="19864-209">d.</span></span> <span data-ttu-id="19864-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="19864-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="19864-211">Creating a Small Improvements test user</span><span class="sxs-lookup"><span data-stu-id="19864-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="19864-212">To enable Azure AD users to log in to Small Improvements, they must be provisioned into Small Improvements.</span><span class="sxs-lookup"><span data-stu-id="19864-212">To enable Azure AD users to log in to Small Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="19864-213">In the case of Small Improvements, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="19864-213">In the case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="19864-214">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19864-214">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="19864-215">Sign-on to your Small Improvements company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="19864-215">Sign-on to your Small Improvements company site as an administrator.</span></span>

1. <span data-ttu-id="19864-216">From the Home page, go to the menu on the left, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="19864-216">From the Home page, go to the menu on the left, click **Administration**.</span></span>

1. <span data-ttu-id="19864-217">Click the **User Directory** button from User Management section.</span><span class="sxs-lookup"><span data-stu-id="19864-217">Click the **User Directory** button from User Management section.</span></span> 
   
    ![Creating an Azure AD test user](./media/smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

1. <span data-ttu-id="19864-219">Click **Add users**.</span><span class="sxs-lookup"><span data-stu-id="19864-219">Click **Add users**.</span></span>

    ![Creating an Azure AD test user](./media/smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

1. <span data-ttu-id="19864-221">On the **Add Users** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19864-221">On the **Add Users** dialog, perform the following steps:</span></span> 

    ![Creating an Azure AD test user](./media/smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="19864-223">a.</span><span class="sxs-lookup"><span data-stu-id="19864-223">a.</span></span> <span data-ttu-id="19864-224">Enter the **first name** of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="19864-224">Enter the **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="19864-225">b.</span><span class="sxs-lookup"><span data-stu-id="19864-225">b.</span></span> <span data-ttu-id="19864-226">Enter the **Last name** of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="19864-226">Enter the **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="19864-227">c.</span><span class="sxs-lookup"><span data-stu-id="19864-227">c.</span></span> <span data-ttu-id="19864-228">Enter the **Email** of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="19864-228">Enter the **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="19864-229">d.</span><span class="sxs-lookup"><span data-stu-id="19864-229">d.</span></span> <span data-ttu-id="19864-230">You can also choose to enter the personal message in the **Send notification email** box.</span><span class="sxs-lookup"><span data-stu-id="19864-230">You can also choose to enter the personal message in the **Send notification email** box.</span></span> <span data-ttu-id="19864-231">If you do not wish to send the notification, then uncheck this checkbox.</span><span class="sxs-lookup"><span data-stu-id="19864-231">If you do not wish to send the notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="19864-232">e.</span><span class="sxs-lookup"><span data-stu-id="19864-232">e.</span></span> <span data-ttu-id="19864-233">Click **Create Users**.</span><span class="sxs-lookup"><span data-stu-id="19864-233">Click **Create Users**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="19864-234">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="19864-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="19864-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Small Improvements.</span><span class="sxs-lookup"><span data-stu-id="19864-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Small Improvements.</span></span>

![Assign User][200] 

<span data-ttu-id="19864-237">**To assign Britta Simon to Small Improvements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19864-237">**To assign Britta Simon to Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="19864-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="19864-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="19864-240">In the applications list, select **Small Improvements**.</span><span class="sxs-lookup"><span data-stu-id="19864-240">In the applications list, select **Small Improvements**.</span></span>

    ![Configure Single Sign-On](./media/smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

1. <span data-ttu-id="19864-242">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="19864-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="19864-244">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="19864-244">Click **Add** button.</span></span> <span data-ttu-id="19864-245">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="19864-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="19864-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="19864-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="19864-248">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="19864-248">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="19864-249">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="19864-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="19864-250">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="19864-250">Testing single sign-on</span></span>

<span data-ttu-id="19864-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="19864-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="19864-252">When you click the Small Improvements tile in the Access Panel, you should get automatically signed-on to your Small Improvements application.</span><span class="sxs-lookup"><span data-stu-id="19864-252">When you click the Small Improvements tile in the Access Panel, you should get automatically signed-on to your Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19864-253">Additional resources</span><span class="sxs-lookup"><span data-stu-id="19864-253">Additional resources</span></span>

* [<span data-ttu-id="19864-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19864-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="19864-255">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="19864-255">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/smallimprovements-tutorial/tutorial_general_203.png

