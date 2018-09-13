---
title: 'Tutorial: Azure Active Directory integration with BGS Online | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BGS Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 3e0da76410c00b8ec0865b094d15237f4f932fb5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968962"
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="a336c-103">Tutorial: Azure Active Directory integration with BGS Online</span><span class="sxs-lookup"><span data-stu-id="a336c-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="a336c-104">In this tutorial, you learn how to integrate BGS Online with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a336c-104">In this tutorial, you learn how to integrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a336c-105">Integrating BGS Online with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a336c-105">Integrating BGS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a336c-106">You can control in Azure AD who has access to BGS Online</span><span class="sxs-lookup"><span data-stu-id="a336c-106">You can control in Azure AD who has access to BGS Online</span></span>
- <span data-ttu-id="a336c-107">You can enable your users to automatically get signed-on to BGS Online (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a336c-107">You can enable your users to automatically get signed-on to BGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a336c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a336c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a336c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a336c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a336c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a336c-110">Prerequisites</span></span>

<span data-ttu-id="a336c-111">To configure Azure AD integration with BGS Online, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a336c-111">To configure Azure AD integration with BGS Online, you need the following items:</span></span>

- <span data-ttu-id="a336c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a336c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a336c-113">A BGS Online single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a336c-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a336c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a336c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a336c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a336c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a336c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a336c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a336c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a336c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a336c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a336c-118">Scenario description</span></span>
<span data-ttu-id="a336c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a336c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a336c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a336c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a336c-121">Adding BGS Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="a336c-121">Adding BGS Online from the gallery</span></span>
1. <span data-ttu-id="a336c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a336c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-the-gallery"></a><span data-ttu-id="a336c-123">Adding BGS Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="a336c-123">Adding BGS Online from the gallery</span></span>
<span data-ttu-id="a336c-124">To configure the integration of BGS Online into Azure AD, you need to add BGS Online from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a336c-124">To configure the integration of BGS Online into Azure AD, you need to add BGS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a336c-125">**To add BGS Online from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a336c-125">**To add BGS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a336c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a336c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="a336c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a336c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a336c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a336c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a336c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a336c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a336c-133">In the search box, type **BGS Online**.</span><span class="sxs-lookup"><span data-stu-id="a336c-133">In the search box, type **BGS Online**.</span></span>

    ![Creating an Azure AD test user](./media/bgsonline-tutorial/tutorial_bgsonline_search.png)

1. <span data-ttu-id="a336c-135">In the results panel, select **BGS Online**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a336c-135">In the results panel, select **BGS Online**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a336c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a336c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a336c-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a336c-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a336c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BGS Online is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a336c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BGS Online is to a user in Azure AD.</span></span> <span data-ttu-id="a336c-140">In other words, a link relationship between an Azure AD user and the related user in BGS Online needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a336c-140">In other words, a link relationship between an Azure AD user and the related user in BGS Online needs to be established.</span></span>

<span data-ttu-id="a336c-141">In BGS Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a336c-141">In BGS Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a336c-142">To configure and test Azure AD single sign-on with BGS Online, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a336c-142">To configure and test Azure AD single sign-on with BGS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a336c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a336c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a336c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a336c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a336c-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - to have a counterpart of Britta Simon in BGS Online that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a336c-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - to have a counterpart of Britta Simon in BGS Online that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a336c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a336c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a336c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a336c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a336c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a336c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a336c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BGS Online application.</span><span class="sxs-lookup"><span data-stu-id="a336c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="a336c-150">**To configure Azure AD single sign-on with BGS Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a336c-150">**To configure Azure AD single sign-on with BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="a336c-151">In the Azure portal, on the **BGS Online** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a336c-151">In the Azure portal, on the **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a336c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a336c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

1. <span data-ttu-id="a336c-155">On the **BGS Online Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a336c-155">On the **BGS Online Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="a336c-157">a.</span><span class="sxs-lookup"><span data-stu-id="a336c-157">a.</span></span> <span data-ttu-id="a336c-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a336c-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="a336c-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="a336c-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="a336c-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="a336c-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="a336c-161">b.</span><span class="sxs-lookup"><span data-stu-id="a336c-161">b.</span></span> <span data-ttu-id="a336c-162">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a336c-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    
    <span data-ttu-id="a336c-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="a336c-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="a336c-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="a336c-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a336c-165">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a336c-165">These values are not real.</span></span> <span data-ttu-id="a336c-166">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="a336c-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a336c-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a336c-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) to get these values.</span></span>
 

1. <span data-ttu-id="a336c-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a336c-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

1. <span data-ttu-id="a336c-170">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a336c-170">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a336c-172">On the **BGS Online Configuration** section, click **Configure BGS Online** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a336c-172">On the **BGS Online Configuration** section, click **Configure BGS Online** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a336c-173">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a336c-173">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_bgsonline_configure.png) 

1. <span data-ttu-id="a336c-175">To configure single sign-on on **BGS Online** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="a336c-175">To configure single sign-on on **BGS Online** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="a336c-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a336c-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a336c-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a336c-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a336c-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a336c-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a336c-179">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a336c-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="a336c-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a336c-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a336c-182">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a336c-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a336c-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a336c-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/bgsonline-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a336c-185">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a336c-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/bgsonline-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a336c-187">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a336c-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/bgsonline-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="a336c-189">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a336c-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a336c-191">a.</span><span class="sxs-lookup"><span data-stu-id="a336c-191">a.</span></span> <span data-ttu-id="a336c-192">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a336c-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a336c-193">b.</span><span class="sxs-lookup"><span data-stu-id="a336c-193">b.</span></span> <span data-ttu-id="a336c-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a336c-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a336c-195">c.</span><span class="sxs-lookup"><span data-stu-id="a336c-195">c.</span></span> <span data-ttu-id="a336c-196">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a336c-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a336c-197">d.</span><span class="sxs-lookup"><span data-stu-id="a336c-197">d.</span></span> <span data-ttu-id="a336c-198">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a336c-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="a336c-199">Creating a BGS Online test user</span><span class="sxs-lookup"><span data-stu-id="a336c-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="a336c-200">In this section, you create a user called Britta Simon in BGS Online.</span><span class="sxs-lookup"><span data-stu-id="a336c-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="a336c-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) to add the users in the BGS Online platform.</span><span class="sxs-lookup"><span data-stu-id="a336c-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) to add the users in the BGS Online platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a336c-202">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a336c-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a336c-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BGS Online.</span><span class="sxs-lookup"><span data-stu-id="a336c-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BGS Online.</span></span>

![Assign User][200] 

<span data-ttu-id="a336c-205">**To assign Britta Simon to BGS Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a336c-205">**To assign Britta Simon to BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="a336c-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a336c-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a336c-208">In the applications list, select **BGS Online**.</span><span class="sxs-lookup"><span data-stu-id="a336c-208">In the applications list, select **BGS Online**.</span></span>

    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_bgsonline_app.png) 

1. <span data-ttu-id="a336c-210">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a336c-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="a336c-212">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a336c-212">Click **Add** button.</span></span> <span data-ttu-id="a336c-213">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a336c-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a336c-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a336c-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a336c-216">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a336c-216">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a336c-217">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a336c-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a336c-218">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a336c-218">Testing single sign-on</span></span>

<span data-ttu-id="a336c-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a336c-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a336c-220">When you click the BGS Online tile in the Access Panel, you should get automatically signed-on to your BGS Online application.</span><span class="sxs-lookup"><span data-stu-id="a336c-220">When you click the BGS Online tile in the Access Panel, you should get automatically signed-on to your BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a336c-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a336c-221">Additional resources</span></span>

* [<span data-ttu-id="a336c-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a336c-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a336c-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a336c-223">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/bgsonline-tutorial/tutorial_general_203.png

