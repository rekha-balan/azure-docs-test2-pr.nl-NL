---
title: 'Tutorial: Azure Active Directory integration with Freshservice | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Freshservice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: eb848ede258d8d25d4734664bd500235f34359e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867860"
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="f7944-103">Tutorial: Azure Active Directory integration with Freshservice</span><span class="sxs-lookup"><span data-stu-id="f7944-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="f7944-104">In this tutorial, you learn how to integrate Freshservice with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7944-104">In this tutorial, you learn how to integrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7944-105">Integrating Freshservice with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f7944-105">Integrating Freshservice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f7944-106">You can control in Azure AD who has access to Freshservice</span><span class="sxs-lookup"><span data-stu-id="f7944-106">You can control in Azure AD who has access to Freshservice</span></span>
- <span data-ttu-id="f7944-107">You can enable your users to automatically get signed-on to Freshservice (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f7944-107">You can enable your users to automatically get signed-on to Freshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f7944-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f7944-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f7944-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f7944-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7944-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f7944-110">Prerequisites</span></span>

<span data-ttu-id="f7944-111">To configure Azure AD integration with Freshservice, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f7944-111">To configure Azure AD integration with Freshservice, you need the following items:</span></span>

- <span data-ttu-id="f7944-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f7944-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7944-113">A Freshservice single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f7944-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7944-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f7944-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7944-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f7944-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7944-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f7944-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7944-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7944-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7944-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f7944-118">Scenario description</span></span>
<span data-ttu-id="f7944-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f7944-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7944-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f7944-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7944-121">Adding Freshservice from the gallery</span><span class="sxs-lookup"><span data-stu-id="f7944-121">Adding Freshservice from the gallery</span></span>
1. <span data-ttu-id="f7944-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f7944-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-the-gallery"></a><span data-ttu-id="f7944-123">Adding Freshservice from the gallery</span><span class="sxs-lookup"><span data-stu-id="f7944-123">Adding Freshservice from the gallery</span></span>
<span data-ttu-id="f7944-124">To configure the integration of Freshservice into Azure AD, you need to add Freshservice from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f7944-124">To configure the integration of Freshservice into Azure AD, you need to add Freshservice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f7944-125">**To add Freshservice from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f7944-125">**To add Freshservice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f7944-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f7944-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="f7944-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f7944-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f7944-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f7944-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="f7944-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f7944-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="f7944-133">In the search box, type **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="f7944-133">In the search box, type **Freshservice**.</span></span>

    ![Creating an Azure AD test user](./media/freshservice-tutorial/tutorial_freshservice_search.png)

1. <span data-ttu-id="f7944-135">In the results panel, select **Freshservice**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f7944-135">In the results panel, select **Freshservice**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f7944-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f7944-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f7944-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f7944-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7944-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Freshservice is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7944-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Freshservice is to a user in Azure AD.</span></span> <span data-ttu-id="f7944-140">In other words, a link relationship between an Azure AD user and the related user in Freshservice needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f7944-140">In other words, a link relationship between an Azure AD user and the related user in Freshservice needs to be established.</span></span>

<span data-ttu-id="f7944-141">In Freshservice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="f7944-141">In Freshservice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f7944-142">To configure and test Azure AD single sign-on with Freshservice, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f7944-142">To configure and test Azure AD single sign-on with Freshservice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f7944-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f7944-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f7944-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7944-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f7944-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - to have a counterpart of Britta Simon in Freshservice that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f7944-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - to have a counterpart of Britta Simon in Freshservice that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f7944-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f7944-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f7944-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f7944-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f7944-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f7944-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f7944-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Freshservice application.</span><span class="sxs-lookup"><span data-stu-id="f7944-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="f7944-150">**To configure Azure AD single sign-on with Freshservice, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f7944-150">**To configure Azure AD single sign-on with Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="f7944-151">In the Azure portal, on the **Freshservice** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f7944-151">In the Azure portal, on the **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="f7944-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f7944-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/freshservice-tutorial/tutorial_freshservice_samlbase.png)

1. <span data-ttu-id="f7944-155">On the **Freshservice Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f7944-155">On the **Freshservice Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="f7944-157">a.</span><span class="sxs-lookup"><span data-stu-id="f7944-157">a.</span></span> <span data-ttu-id="f7944-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="f7944-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="f7944-159">b.</span><span class="sxs-lookup"><span data-stu-id="f7944-159">b.</span></span> <span data-ttu-id="f7944-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="f7944-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f7944-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="f7944-161">These values are not real.</span></span> <span data-ttu-id="f7944-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="f7944-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f7944-163">Contact [Freshservice Client support team](https://support.freshservice.com/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="f7944-163">Contact [Freshservice Client support team](https://support.freshservice.com/) to get these values.</span></span> 
 
1. <span data-ttu-id="f7944-164">On the **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span><span class="sxs-lookup"><span data-stu-id="f7944-164">On the **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Configure Single Sign-On](./media/freshservice-tutorial/tutorial_freshservice_certificate.png)

1. <span data-ttu-id="f7944-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f7944-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/freshservice-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f7944-168">On the **Freshservice Configuration** section, click **Configure Freshservice** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="f7944-168">On the **Freshservice Configuration** section, click **Configure Freshservice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f7944-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="f7944-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/freshservice-tutorial/tutorial_freshservice_configure.png) 

1. <span data-ttu-id="f7944-171">In a different web browser window, log in to your Freshservice company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f7944-171">In a different web browser window, log in to your Freshservice company site as an administrator.</span></span>

1. <span data-ttu-id="f7944-172">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="f7944-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="f7944-173">![Admin](./media/freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="f7944-173">![Admin](./media/freshservice-tutorial/ic790814.png "Admin")</span></span>

1. <span data-ttu-id="f7944-174">In the **Customer Portal**, click **Security**.</span><span class="sxs-lookup"><span data-stu-id="f7944-174">In the **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="f7944-175">![Security](./media/freshservice-tutorial/ic790815.png "Security")</span><span class="sxs-lookup"><span data-stu-id="f7944-175">![Security](./media/freshservice-tutorial/ic790815.png "Security")</span></span>

1. <span data-ttu-id="f7944-176">In the **Security** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f7944-176">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f7944-177">![Single Sign On](./media/freshservice-tutorial/ic790816.png "Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="f7944-177">![Single Sign On](./media/freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="f7944-178">a.</span><span class="sxs-lookup"><span data-stu-id="f7944-178">a.</span></span> <span data-ttu-id="f7944-179">Switch **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="f7944-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="f7944-180">b.</span><span class="sxs-lookup"><span data-stu-id="f7944-180">b.</span></span> <span data-ttu-id="f7944-181">Select **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="f7944-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="f7944-182">c.</span><span class="sxs-lookup"><span data-stu-id="f7944-182">c.</span></span> <span data-ttu-id="f7944-183">In the **SAML Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f7944-183">In the **SAML Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f7944-184">d.</span><span class="sxs-lookup"><span data-stu-id="f7944-184">d.</span></span> <span data-ttu-id="f7944-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f7944-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f7944-186">e.</span><span class="sxs-lookup"><span data-stu-id="f7944-186">e.</span></span> <span data-ttu-id="f7944-187">In **Security Certificate Fingerprint** textbox, paste the **THUMBPRINT** value of certificate, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f7944-187">In **Security Certificate Fingerprint** textbox, paste the **THUMBPRINT** value of certificate, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f7944-188">f.</span><span class="sxs-lookup"><span data-stu-id="f7944-188">f.</span></span> <span data-ttu-id="f7944-189">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="f7944-189">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f7944-190">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f7944-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="f7944-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7944-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="f7944-193">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f7944-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f7944-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f7944-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/freshservice-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="f7944-196">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f7944-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/freshservice-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="f7944-198">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f7944-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/freshservice-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="f7944-200">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f7944-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f7944-202">a.</span><span class="sxs-lookup"><span data-stu-id="f7944-202">a.</span></span> <span data-ttu-id="f7944-203">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7944-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7944-204">b.</span><span class="sxs-lookup"><span data-stu-id="f7944-204">b.</span></span> <span data-ttu-id="f7944-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f7944-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f7944-206">c.</span><span class="sxs-lookup"><span data-stu-id="f7944-206">c.</span></span> <span data-ttu-id="f7944-207">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f7944-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f7944-208">d.</span><span class="sxs-lookup"><span data-stu-id="f7944-208">d.</span></span> <span data-ttu-id="f7944-209">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f7944-209">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="f7944-210">Creating a Freshservice test user</span><span class="sxs-lookup"><span data-stu-id="f7944-210">Creating a Freshservice test user</span></span>

<span data-ttu-id="f7944-211">To enable Azure AD users to log in to FreshService, they must be provisioned into FreshService.</span><span class="sxs-lookup"><span data-stu-id="f7944-211">To enable Azure AD users to log in to FreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="f7944-212">In the case of FreshService, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="f7944-212">In the case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="f7944-213">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f7944-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f7944-214">Log in to your **FreshService** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f7944-214">Log in to your **FreshService** company site as an administrator.</span></span>

1. <span data-ttu-id="f7944-215">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="f7944-215">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="f7944-216">![Admin](./media/freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="f7944-216">![Admin](./media/freshservice-tutorial/ic790814.png "Admin")</span></span>

1. <span data-ttu-id="f7944-217">In the **User Management** section, click **Requesters**.</span><span class="sxs-lookup"><span data-stu-id="f7944-217">In the **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="f7944-218">![Requesters](./media/freshservice-tutorial/ic790818.png "Requesters")</span><span class="sxs-lookup"><span data-stu-id="f7944-218">![Requesters](./media/freshservice-tutorial/ic790818.png "Requesters")</span></span>

1. <span data-ttu-id="f7944-219">Click **New Requester**.</span><span class="sxs-lookup"><span data-stu-id="f7944-219">Click **New Requester**.</span></span>
   
    <span data-ttu-id="f7944-220">![New Requesters](./media/freshservice-tutorial/ic790819.png "New Requesters")</span><span class="sxs-lookup"><span data-stu-id="f7944-220">![New Requesters](./media/freshservice-tutorial/ic790819.png "New Requesters")</span></span>

1. <span data-ttu-id="f7944-221">In the **New Requester** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f7944-221">In the **New Requester** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f7944-222">![New Requester](./media/freshservice-tutorial/ic790820.png "New Requester")</span><span class="sxs-lookup"><span data-stu-id="f7944-222">![New Requester](./media/freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="f7944-223">a.</span><span class="sxs-lookup"><span data-stu-id="f7944-223">a.</span></span> <span data-ttu-id="f7944-224">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="f7944-224">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="f7944-225">b.</span><span class="sxs-lookup"><span data-stu-id="f7944-225">b.</span></span> <span data-ttu-id="f7944-226">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f7944-226">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="f7944-227">The Azure Active Directory account holder gets an email including a link to confirm the account before it becomes active</span><span class="sxs-lookup"><span data-stu-id="f7944-227">The Azure Active Directory account holder gets an email including a link to confirm the account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="f7944-228">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="f7944-228">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span></span>
>  

![Assign User][200] 

<span data-ttu-id="f7944-230">**To assign Britta Simon to Freshservice, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f7944-230">**To assign Britta Simon to Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="f7944-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f7944-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f7944-233">In the applications list, select **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="f7944-233">In the applications list, select **Freshservice**.</span></span>

    ![Configure Single Sign-On](./media/freshservice-tutorial/tutorial_freshservice_app.png) 

1. <span data-ttu-id="f7944-235">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f7944-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="f7944-237">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f7944-237">Click **Add** button.</span></span> <span data-ttu-id="f7944-238">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f7944-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="f7944-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f7944-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f7944-241">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f7944-241">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f7944-242">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f7944-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f7944-243">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f7944-243">Testing single sign-on</span></span>

<span data-ttu-id="f7944-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f7944-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f7944-245">When you click the Freshservice tile in the Access Panel, you should get automatically signed-on to your Freshservice application.</span><span class="sxs-lookup"><span data-stu-id="f7944-245">When you click the Freshservice tile in the Access Panel, you should get automatically signed-on to your Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7944-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f7944-246">Additional resources</span></span>

* [<span data-ttu-id="f7944-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7944-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f7944-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f7944-248">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/freshservice-tutorial/tutorial_general_01.png
[2]: ./media/freshservice-tutorial/tutorial_general_02.png
[3]: ./media/freshservice-tutorial/tutorial_general_03.png
[4]: ./media/freshservice-tutorial/tutorial_general_04.png

[100]: ./media/freshservice-tutorial/tutorial_general_100.png

[200]: ./media/freshservice-tutorial/tutorial_general_200.png
[201]: ./media/freshservice-tutorial/tutorial_general_201.png
[202]: ./media/freshservice-tutorial/tutorial_general_202.png
[203]: ./media/freshservice-tutorial/tutorial_general_203.png

