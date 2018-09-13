---
title: 'Tutorial: Azure Active Directory integration with Syncplicity | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Syncplicity.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3b74ca178d3bf380dc759ce0325d4047891a39d3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869214"
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="eabb6-103">Tutorial: Azure Active Directory integration with Syncplicity</span><span class="sxs-lookup"><span data-stu-id="eabb6-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="eabb6-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eabb6-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eabb6-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="eabb6-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eabb6-106">You can control in Azure AD who has access to Syncplicity</span><span class="sxs-lookup"><span data-stu-id="eabb6-106">You can control in Azure AD who has access to Syncplicity</span></span>
- <span data-ttu-id="eabb6-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="eabb6-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eabb6-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="eabb6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="eabb6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="eabb6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eabb6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eabb6-110">Prerequisites</span></span>

<span data-ttu-id="eabb6-111">To configure Azure AD integration with Syncplicity, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="eabb6-111">To configure Azure AD integration with Syncplicity, you need the following items:</span></span>

- <span data-ttu-id="eabb6-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="eabb6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eabb6-113">A Syncplicity single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="eabb6-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eabb6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="eabb6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eabb6-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="eabb6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eabb6-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="eabb6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eabb6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eabb6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eabb6-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="eabb6-118">Scenario description</span></span>
<span data-ttu-id="eabb6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="eabb6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eabb6-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="eabb6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eabb6-121">Adding Syncplicity from the gallery</span><span class="sxs-lookup"><span data-stu-id="eabb6-121">Adding Syncplicity from the gallery</span></span>
1. <span data-ttu-id="eabb6-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="eabb6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-the-gallery"></a><span data-ttu-id="eabb6-123">Adding Syncplicity from the gallery</span><span class="sxs-lookup"><span data-stu-id="eabb6-123">Adding Syncplicity from the gallery</span></span>
<span data-ttu-id="eabb6-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="eabb6-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eabb6-125">**To add Syncplicity from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="eabb6-125">**To add Syncplicity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eabb6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="eabb6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="eabb6-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eabb6-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="eabb6-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="eabb6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="eabb6-133">In the search box, type **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-133">In the search box, type **Syncplicity**.</span></span>

    ![Creating an Azure AD test user](./media/syncplicity-tutorial/tutorial_syncplicity_search.png)

1. <span data-ttu-id="eabb6-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="eabb6-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eabb6-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="eabb6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eabb6-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="eabb6-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eabb6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eabb6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span></span> <span data-ttu-id="eabb6-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span><span class="sxs-lookup"><span data-stu-id="eabb6-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span></span>

<span data-ttu-id="eabb6-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="eabb6-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eabb6-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="eabb6-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eabb6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="eabb6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="eabb6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eabb6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="eabb6-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="eabb6-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="eabb6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="eabb6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="eabb6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="eabb6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eabb6-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="eabb6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eabb6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span><span class="sxs-lookup"><span data-stu-id="eabb6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="eabb6-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="eabb6-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="eabb6-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="eabb6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="eabb6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

1. <span data-ttu-id="eabb6-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="eabb6-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="eabb6-157">a.</span><span class="sxs-lookup"><span data-stu-id="eabb6-157">a.</span></span> <span data-ttu-id="eabb6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="eabb6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="eabb6-159">b.</span><span class="sxs-lookup"><span data-stu-id="eabb6-159">b.</span></span> <span data-ttu-id="eabb6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="eabb6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eabb6-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="eabb6-161">These values are not real.</span></span> <span data-ttu-id="eabb6-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="eabb6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eabb6-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span><span class="sxs-lookup"><span data-stu-id="eabb6-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span></span> 
 

1. <span data-ttu-id="eabb6-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="eabb6-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
1. <span data-ttu-id="eabb6-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="eabb6-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/syncplicity-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="eabb6-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="eabb6-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="eabb6-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="eabb6-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/syncplicity-tutorial/tutorial_syncplicity_configure.png) 

1. <span data-ttu-id="eabb6-171">Sign in to your **Syncplicity** tenant.</span><span class="sxs-lookup"><span data-stu-id="eabb6-171">Sign in to your **Syncplicity** tenant.</span></span>

1. <span data-ttu-id="eabb6-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="eabb6-173">![Syncplicity](./media/syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="eabb6-173">![Syncplicity](./media/syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

1. <span data-ttu-id="eabb6-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="eabb6-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="eabb6-175">![Single Sign-On \(SSO\)](./media/syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="eabb6-175">![Single Sign-On \(SSO\)](./media/syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="eabb6-176">a.</span><span class="sxs-lookup"><span data-stu-id="eabb6-176">a.</span></span> <span data-ttu-id="eabb6-177">In the **Custom Domain** textbox, type the name of your domain.</span><span class="sxs-lookup"><span data-stu-id="eabb6-177">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  
    <span data-ttu-id="eabb6-178">b.</span><span class="sxs-lookup"><span data-stu-id="eabb6-178">b.</span></span> <span data-ttu-id="eabb6-179">Select **Enabled** as **Single Sign-On Status**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="eabb6-180">c.</span><span class="sxs-lookup"><span data-stu-id="eabb6-180">c.</span></span> <span data-ttu-id="eabb6-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eabb6-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="eabb6-182">d.</span><span class="sxs-lookup"><span data-stu-id="eabb6-182">d.</span></span> <span data-ttu-id="eabb6-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eabb6-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="eabb6-184">e.</span><span class="sxs-lookup"><span data-stu-id="eabb6-184">e.</span></span> <span data-ttu-id="eabb6-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eabb6-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="eabb6-186">f.</span><span class="sxs-lookup"><span data-stu-id="eabb6-186">f.</span></span> <span data-ttu-id="eabb6-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eabb6-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span></span> 

    <span data-ttu-id="eabb6-188">g.</span><span class="sxs-lookup"><span data-stu-id="eabb6-188">g.</span></span> <span data-ttu-id="eabb6-189">Click **SAVE CHANGES**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="eabb6-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="eabb6-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eabb6-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="eabb6-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eabb6-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eabb6-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eabb6-193">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="eabb6-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="eabb6-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eabb6-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="eabb6-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="eabb6-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eabb6-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="eabb6-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/syncplicity-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="eabb6-199">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/syncplicity-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="eabb6-201">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="eabb6-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/syncplicity-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="eabb6-203">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="eabb6-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eabb6-205">a.</span><span class="sxs-lookup"><span data-stu-id="eabb6-205">a.</span></span> <span data-ttu-id="eabb6-206">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eabb6-207">b.</span><span class="sxs-lookup"><span data-stu-id="eabb6-207">b.</span></span> <span data-ttu-id="eabb6-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eabb6-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eabb6-209">c.</span><span class="sxs-lookup"><span data-stu-id="eabb6-209">c.</span></span> <span data-ttu-id="eabb6-210">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="eabb6-211">d.</span><span class="sxs-lookup"><span data-stu-id="eabb6-211">d.</span></span> <span data-ttu-id="eabb6-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="eabb6-213">Creating a Syncplicity test user</span><span class="sxs-lookup"><span data-stu-id="eabb6-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="eabb6-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span><span class="sxs-lookup"><span data-stu-id="eabb6-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="eabb6-215">This section describes how to create AAD user accounts in Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="eabb6-215">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="eabb6-216">**To provision a user account to Syncplicity, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="eabb6-216">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="eabb6-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="eabb6-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

1. <span data-ttu-id="eabb6-218">Click **admin** and select **user accounts**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-218">Click **admin** and select **user accounts**.</span></span>

1. <span data-ttu-id="eabb6-219">Click **ADD A USER**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="eabb6-220">![Manage Users](./media/syncplicity-tutorial/ic769764.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="eabb6-220">![Manage Users](./media/syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

1. <span data-ttu-id="eabb6-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="eabb6-222">![Account Information](./media/syncplicity-tutorial/ic769765.png "Account Information")</span><span class="sxs-lookup"><span data-stu-id="eabb6-222">![Account Information](./media/syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="eabb6-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span><span class="sxs-lookup"><span data-stu-id="eabb6-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span></span> 
    > 

1. <span data-ttu-id="eabb6-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="eabb6-225">![Group Membership](./media/syncplicity-tutorial/ic769772.png "Group Membership")</span><span class="sxs-lookup"><span data-stu-id="eabb6-225">![Group Membership](./media/syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="eabb6-226">If there are no groups listed, click **NEXT**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

1. <span data-ttu-id="eabb6-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="eabb6-228">![Syncplicity Folders](./media/syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span><span class="sxs-lookup"><span data-stu-id="eabb6-228">![Syncplicity Folders](./media/syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="eabb6-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="eabb6-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="eabb6-230">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="eabb6-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="eabb6-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="eabb6-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span></span>

![Assign User][200] 

<span data-ttu-id="eabb6-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="eabb6-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="eabb6-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="eabb6-236">In the applications list, select **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-236">In the applications list, select **Syncplicity**.</span></span>

    ![Configure Single Sign-On](./media/syncplicity-tutorial/tutorial_syncplicity_app.png) 

1. <span data-ttu-id="eabb6-238">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="eabb6-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="eabb6-240">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="eabb6-240">Click **Add** button.</span></span> <span data-ttu-id="eabb6-241">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="eabb6-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="eabb6-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="eabb6-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="eabb6-244">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="eabb6-244">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="eabb6-245">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="eabb6-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eabb6-246">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="eabb6-246">Testing single sign-on</span></span>

<span data-ttu-id="eabb6-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="eabb6-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="eabb6-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span><span class="sxs-lookup"><span data-stu-id="eabb6-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="eabb6-249">Additional resources</span><span class="sxs-lookup"><span data-stu-id="eabb6-249">Additional resources</span></span>

* [<span data-ttu-id="eabb6-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eabb6-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="eabb6-251">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eabb6-251">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/syncplicity-tutorial/tutorial_general_203.png

