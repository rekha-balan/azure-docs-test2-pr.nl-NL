---
title: 'Tutorial: Azure Active Directory integration with Cimpl | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cimpl.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 58ee5481-ae40-4e4a-a3c9-86343851fc9a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 8668b1c355e7d19943596fb94d6a7d260c0bca43
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865617"
---
# <a name="tutorial-azure-active-directory-integration-with-cimpl"></a><span data-ttu-id="66534-103">Tutorial: Azure Active Directory integration with Cimpl</span><span class="sxs-lookup"><span data-stu-id="66534-103">Tutorial: Azure Active Directory integration with Cimpl</span></span>

<span data-ttu-id="66534-104">In this tutorial, you learn how to integrate Cimpl with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="66534-104">In this tutorial, you learn how to integrate Cimpl with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66534-105">Integrating Cimpl with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="66534-105">Integrating Cimpl with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="66534-106">You can control in Azure AD who has access to Cimpl</span><span class="sxs-lookup"><span data-stu-id="66534-106">You can control in Azure AD who has access to Cimpl</span></span>
- <span data-ttu-id="66534-107">You can enable your users to automatically get signed-on to Cimpl (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="66534-107">You can enable your users to automatically get signed-on to Cimpl (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66534-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="66534-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="66534-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="66534-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66534-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="66534-110">Prerequisites</span></span>

<span data-ttu-id="66534-111">To configure Azure AD integration with Cimpl, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="66534-111">To configure Azure AD integration with Cimpl, you need the following items:</span></span>

- <span data-ttu-id="66534-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="66534-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66534-113">A Cimpl single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="66534-113">A Cimpl single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66534-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="66534-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66534-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="66534-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66534-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="66534-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66534-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66534-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66534-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="66534-118">Scenario description</span></span>
<span data-ttu-id="66534-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="66534-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66534-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="66534-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66534-121">Adding Cimpl from the gallery</span><span class="sxs-lookup"><span data-stu-id="66534-121">Adding Cimpl from the gallery</span></span>
1. <span data-ttu-id="66534-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="66534-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cimpl-from-the-gallery"></a><span data-ttu-id="66534-123">Adding Cimpl from the gallery</span><span class="sxs-lookup"><span data-stu-id="66534-123">Adding Cimpl from the gallery</span></span>
<span data-ttu-id="66534-124">To configure the integration of Cimpl into Azure AD, you need to add Cimpl from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="66534-124">To configure the integration of Cimpl into Azure AD, you need to add Cimpl from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="66534-125">**To add Cimpl from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="66534-125">**To add Cimpl from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="66534-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="66534-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="66534-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="66534-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="66534-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="66534-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="66534-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="66534-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="66534-133">In the search box, type **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="66534-133">In the search box, type **Cimpl**.</span></span>

    ![Creating an Azure AD test user](./media/cimpl-tutorial/tutorial_cimpl_search.png)

1. <span data-ttu-id="66534-135">In the results panel, select **Cimpl**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="66534-135">In the results panel, select **Cimpl**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/cimpl-tutorial/tutorial_cimpl_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66534-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="66534-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66534-138">In this section, you configure and test Azure AD single sign-on with Cimpl based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="66534-138">In this section, you configure and test Azure AD single sign-on with Cimpl based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="66534-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cimpl is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66534-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cimpl is to a user in Azure AD.</span></span> <span data-ttu-id="66534-140">In other words, a link relationship between an Azure AD user and the related user in Cimpl needs to be established.</span><span class="sxs-lookup"><span data-stu-id="66534-140">In other words, a link relationship between an Azure AD user and the related user in Cimpl needs to be established.</span></span>

<span data-ttu-id="66534-141">In Cimpl, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="66534-141">In Cimpl, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="66534-142">To configure and test Azure AD single sign-on with Cimpl, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="66534-142">To configure and test Azure AD single sign-on with Cimpl, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="66534-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="66534-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="66534-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66534-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="66534-145">**[Creating a Cimpl test user](#creating-a-cimpl-test-user)** - to have a counterpart of Britta Simon in Cimpl that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="66534-145">**[Creating a Cimpl test user](#creating-a-cimpl-test-user)** - to have a counterpart of Britta Simon in Cimpl that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="66534-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="66534-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="66534-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="66534-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66534-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="66534-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66534-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cimpl application.</span><span class="sxs-lookup"><span data-stu-id="66534-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cimpl application.</span></span>

<span data-ttu-id="66534-150">**To configure Azure AD single sign-on with Cimpl, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="66534-150">**To configure Azure AD single sign-on with Cimpl, perform the following steps:**</span></span>

1. <span data-ttu-id="66534-151">In the Azure portal, on the **Cimpl** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="66534-151">In the Azure portal, on the **Cimpl** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="66534-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="66534-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/cimpl-tutorial/tutorial_cimpl_samlbase.png)

1. <span data-ttu-id="66534-155">On the **Cimpl Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="66534-155">On the **Cimpl Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/cimpl-tutorial/tutorial_cimpl_url.png)

    <span data-ttu-id="66534-157">a.</span><span class="sxs-lookup"><span data-stu-id="66534-157">a.</span></span> <span data-ttu-id="66534-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="66534-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    <span data-ttu-id="66534-159">b.</span><span class="sxs-lookup"><span data-stu-id="66534-159">b.</span></span> <span data-ttu-id="66534-160">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="66534-160">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66534-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="66534-161">These values are not real.</span></span> <span data-ttu-id="66534-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="66534-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="66534-163">Contact Cimpl team at **+1 866-982-8250** to get these values.</span><span class="sxs-lookup"><span data-stu-id="66534-163">Contact Cimpl team at **+1 866-982-8250** to get these values.</span></span> 
 
1. <span data-ttu-id="66534-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="66534-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/cimpl-tutorial/tutorial_cimpl_certificate.png) 

1. <span data-ttu-id="66534-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="66534-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/cimpl-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="66534-168">On the **Cimpl Configuration** section, click **Configure Cimpl** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="66534-168">On the **Cimpl Configuration** section, click **Configure Cimpl** to open **Configure sign-on** window.</span></span> <span data-ttu-id="66534-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="66534-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/cimpl-tutorial/tutorial_cimpl_configure.png) 

1. <span data-ttu-id="66534-171">To configure single sign-on on **Cimpl** side, you need to send the downloaded **Certificate (Base64)**, **SAML Entity ID, and SAML Single Sign-On Service URL** to Cimpl support at **+1 866-982-8250**.</span><span class="sxs-lookup"><span data-stu-id="66534-171">To configure single sign-on on **Cimpl** side, you need to send the downloaded **Certificate (Base64)**, **SAML Entity ID, and SAML Single Sign-On Service URL** to Cimpl support at **+1 866-982-8250**.</span></span>


> [!TIP]
> <span data-ttu-id="66534-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="66534-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="66534-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="66534-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="66534-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66534-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66534-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="66534-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="66534-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66534-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="66534-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="66534-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="66534-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="66534-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/cimpl-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="66534-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="66534-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/cimpl-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="66534-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="66534-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/cimpl-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="66534-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="66534-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/cimpl-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66534-187">a.</span><span class="sxs-lookup"><span data-stu-id="66534-187">a.</span></span> <span data-ttu-id="66534-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66534-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66534-189">b.</span><span class="sxs-lookup"><span data-stu-id="66534-189">b.</span></span> <span data-ttu-id="66534-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="66534-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66534-191">c.</span><span class="sxs-lookup"><span data-stu-id="66534-191">c.</span></span> <span data-ttu-id="66534-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="66534-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="66534-193">d.</span><span class="sxs-lookup"><span data-stu-id="66534-193">d.</span></span> <span data-ttu-id="66534-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="66534-194">Click **Create**.</span></span>
 
### <a name="creating-a-cimpl-test-user"></a><span data-ttu-id="66534-195">Creating a Cimpl test user</span><span class="sxs-lookup"><span data-stu-id="66534-195">Creating a Cimpl test user</span></span>

<span data-ttu-id="66534-196">The objective of this section is to create a user called Britta Simon in Cimpl.</span><span class="sxs-lookup"><span data-stu-id="66534-196">The objective of this section is to create a user called Britta Simon in Cimpl.</span></span> <span data-ttu-id="66534-197">Work with Cimpl support at **+1 866-982-8250** to add the users in the Cimpl account.</span><span class="sxs-lookup"><span data-stu-id="66534-197">Work with Cimpl support at **+1 866-982-8250** to add the users in the Cimpl account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="66534-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="66534-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="66534-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cimpl.</span><span class="sxs-lookup"><span data-stu-id="66534-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cimpl.</span></span>

![Assign User][200] 

<span data-ttu-id="66534-201">**To assign Britta Simon to Cimpl, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="66534-201">**To assign Britta Simon to Cimpl, perform the following steps:**</span></span>

1. <span data-ttu-id="66534-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="66534-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="66534-204">In the applications list, select **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="66534-204">In the applications list, select **Cimpl**.</span></span>

    ![Configure Single Sign-On](./media/cimpl-tutorial/tutorial_cimpl_app.png) 

1. <span data-ttu-id="66534-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="66534-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="66534-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="66534-208">Click **Add** button.</span></span> <span data-ttu-id="66534-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="66534-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="66534-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="66534-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="66534-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="66534-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="66534-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="66534-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66534-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="66534-214">Testing single sign-on</span></span>

<span data-ttu-id="66534-215">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="66534-215">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  <span data-ttu-id="66534-216">When you click the Cimpl tile in the Access Panel, you should get automatically signed-on to your Cimpl application.</span><span class="sxs-lookup"><span data-stu-id="66534-216">When you click the Cimpl tile in the Access Panel, you should get automatically signed-on to your Cimpl application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="66534-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="66534-217">Additional resources</span></span>

* [<span data-ttu-id="66534-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66534-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="66534-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="66534-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/cimpl-tutorial/tutorial_general_01.png
[2]: ./media/cimpl-tutorial/tutorial_general_02.png
[3]: ./media/cimpl-tutorial/tutorial_general_03.png
[4]: ./media/cimpl-tutorial/tutorial_general_04.png

[100]: ./media/cimpl-tutorial/tutorial_general_100.png

[200]: ./media/cimpl-tutorial/tutorial_general_200.png
[201]: ./media/cimpl-tutorial/tutorial_general_201.png
[202]: ./media/cimpl-tutorial/tutorial_general_202.png
[203]: ./media/cimpl-tutorial/tutorial_general_203.png

