---
title: 'Tutorial: Azure Active Directory integration with Showpad | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Showpad.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d78276fad3da1b0ef4a860f147b17bc715932971
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855708"
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="b8878-103">Tutorial: Azure Active Directory integration with Showpad</span><span class="sxs-lookup"><span data-stu-id="b8878-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="b8878-104">In this tutorial, you learn how to integrate Showpad with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b8878-104">In this tutorial, you learn how to integrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b8878-105">Integrating Showpad with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b8878-105">Integrating Showpad with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b8878-106">You can control in Azure AD who has access to Showpad</span><span class="sxs-lookup"><span data-stu-id="b8878-106">You can control in Azure AD who has access to Showpad</span></span>
- <span data-ttu-id="b8878-107">You can enable your users to automatically get signed-on to Showpad (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="b8878-107">You can enable your users to automatically get signed-on to Showpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b8878-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b8878-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b8878-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b8878-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8878-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b8878-110">Prerequisites</span></span>

<span data-ttu-id="b8878-111">To configure Azure AD integration with Showpad, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b8878-111">To configure Azure AD integration with Showpad, you need the following items:</span></span>

- <span data-ttu-id="b8878-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b8878-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b8878-113">A Showpad single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b8878-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b8878-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b8878-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b8878-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b8878-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b8878-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b8878-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b8878-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8878-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b8878-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b8878-118">Scenario description</span></span>
<span data-ttu-id="b8878-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b8878-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b8878-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b8878-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b8878-121">Adding Showpad from the gallery</span><span class="sxs-lookup"><span data-stu-id="b8878-121">Adding Showpad from the gallery</span></span>
1. <span data-ttu-id="b8878-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b8878-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-the-gallery"></a><span data-ttu-id="b8878-123">Adding Showpad from the gallery</span><span class="sxs-lookup"><span data-stu-id="b8878-123">Adding Showpad from the gallery</span></span>

<span data-ttu-id="b8878-124">To configure the integration of Showpad into Azure AD, you need to add Showpad from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b8878-124">To configure the integration of Showpad into Azure AD, you need to add Showpad from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b8878-125">**To add Showpad from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b8878-125">**To add Showpad from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b8878-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b8878-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="b8878-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b8878-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b8878-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b8878-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="b8878-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b8878-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="b8878-133">In the search box, type **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="b8878-133">In the search box, type **Showpad**.</span></span>

    ![Creating an Azure AD test user](./media/showpad-tutorial/tutorial_showpad_search.png)

1. <span data-ttu-id="b8878-135">In the results panel, select **Showpad**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b8878-135">In the results panel, select **Showpad**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b8878-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b8878-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="b8878-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="b8878-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b8878-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Showpad is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8878-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Showpad is to a user in Azure AD.</span></span> <span data-ttu-id="b8878-140">In other words, a link relationship between an Azure AD user and the related user in Showpad needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b8878-140">In other words, a link relationship between an Azure AD user and the related user in Showpad needs to be established.</span></span>

<span data-ttu-id="b8878-141">In Showpad, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="b8878-141">In Showpad, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b8878-142">To configure and test Azure AD single sign-on with Showpad, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b8878-142">To configure and test Azure AD single sign-on with Showpad, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b8878-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b8878-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="b8878-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8878-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="b8878-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - to have a counterpart of Britta Simon in Showpad that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b8878-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - to have a counterpart of Britta Simon in Showpad that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="b8878-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b8878-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="b8878-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b8878-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b8878-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b8878-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b8878-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Showpad application.</span><span class="sxs-lookup"><span data-stu-id="b8878-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="b8878-150">**To configure Azure AD single sign-on with Showpad, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b8878-150">**To configure Azure AD single sign-on with Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="b8878-151">In the Azure portal, on the **Showpad** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b8878-151">In the Azure portal, on the **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="b8878-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b8878-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/showpad-tutorial/tutorial_showpad_samlbase.png)

1. <span data-ttu-id="b8878-155">On the **Showpad Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b8878-155">On the **Showpad Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="b8878-157">a.</span><span class="sxs-lookup"><span data-stu-id="b8878-157">a.</span></span> <span data-ttu-id="b8878-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="b8878-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="b8878-159">b.</span><span class="sxs-lookup"><span data-stu-id="b8878-159">b.</span></span> <span data-ttu-id="b8878-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="b8878-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b8878-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="b8878-161">These values are not real.</span></span> <span data-ttu-id="b8878-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="b8878-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b8878-163">Contact [Showpad support team](https://help.showpad.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="b8878-163">Contact [Showpad support team](https://help.showpad.com) to get these values.</span></span> 
 


1. <span data-ttu-id="b8878-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b8878-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/showpad-tutorial/tutorial_showpad_certificate.png) 

1. <span data-ttu-id="b8878-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b8878-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/showpad-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="b8878-168">Sign-on to your Showpad tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b8878-168">Sign-on to your Showpad tenant as an administrator.</span></span>

1. <span data-ttu-id="b8878-169">In the menu on the top, click the **Settings**.</span><span class="sxs-lookup"><span data-stu-id="b8878-169">In the menu on the top, click the **Settings**.</span></span>
   
    ![Configure Single Sign-On On App Side](./media/showpad-tutorial/tutorial_showpad_001.png) 

1. <span data-ttu-id="b8878-171">Navigate to "**Single Sign-On**" and click "**Enable**."</span><span class="sxs-lookup"><span data-stu-id="b8878-171">Navigate to "**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Configure Single Sign-On On App Side](./media/showpad-tutorial/tutorial_showpad_002.png)

1. <span data-ttu-id="b8878-173">On the **Add a SAML 2.0 Service** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b8878-173">On the **Add a SAML 2.0 Service** dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On On App Side](./media/showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="b8878-175">a.</span><span class="sxs-lookup"><span data-stu-id="b8878-175">a.</span></span> <span data-ttu-id="b8878-176">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span><span class="sxs-lookup"><span data-stu-id="b8878-176">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="b8878-177">b.</span><span class="sxs-lookup"><span data-stu-id="b8878-177">b.</span></span> <span data-ttu-id="b8878-178">As **Metadata Source**, select **XML**.</span><span class="sxs-lookup"><span data-stu-id="b8878-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="b8878-179">c.</span><span class="sxs-lookup"><span data-stu-id="b8878-179">c.</span></span> <span data-ttu-id="b8878-180">Copy the content of metadata XML file, which you have downloaded from the Azure portal, and then paste it into the **Metadata XML** textbox.</span><span class="sxs-lookup"><span data-stu-id="b8878-180">Copy the content of metadata XML file, which you have downloaded from the Azure portal, and then paste it into the **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="b8878-181">d.</span><span class="sxs-lookup"><span data-stu-id="b8878-181">d.</span></span> <span data-ttu-id="b8878-182">Select **Auto-provision accounts for new users when they log in**.</span><span class="sxs-lookup"><span data-stu-id="b8878-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="b8878-183">e.</span><span class="sxs-lookup"><span data-stu-id="b8878-183">e.</span></span> <span data-ttu-id="b8878-184">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="b8878-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="b8878-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="b8878-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b8878-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="b8878-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b8878-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b8878-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b8878-188">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b8878-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="b8878-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8878-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="b8878-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b8878-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b8878-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b8878-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/showpad-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="b8878-194">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b8878-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/showpad-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="b8878-196">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="b8878-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/showpad-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="b8878-198">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b8878-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b8878-200">a.</span><span class="sxs-lookup"><span data-stu-id="b8878-200">a.</span></span> <span data-ttu-id="b8878-201">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b8878-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b8878-202">b.</span><span class="sxs-lookup"><span data-stu-id="b8878-202">b.</span></span> <span data-ttu-id="b8878-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b8878-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b8878-204">c.</span><span class="sxs-lookup"><span data-stu-id="b8878-204">c.</span></span> <span data-ttu-id="b8878-205">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="b8878-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b8878-206">d.</span><span class="sxs-lookup"><span data-stu-id="b8878-206">d.</span></span> <span data-ttu-id="b8878-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b8878-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="b8878-208">Creating a Showpad test user</span><span class="sxs-lookup"><span data-stu-id="b8878-208">Creating a Showpad test user</span></span>

<span data-ttu-id="b8878-209">The objective of this section is to create a user called Britta Simon in Showpad.</span><span class="sxs-lookup"><span data-stu-id="b8878-209">The objective of this section is to create a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="b8878-210">Showpad supports just-in-time provisioning.</span><span class="sxs-lookup"><span data-stu-id="b8878-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="b8878-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="b8878-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="b8878-212">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="b8878-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b8878-213">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b8878-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b8878-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Showpad.</span><span class="sxs-lookup"><span data-stu-id="b8878-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Showpad.</span></span>

![Assign User][200] 

<span data-ttu-id="b8878-216">**To assign Britta Simon to Showpad, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b8878-216">**To assign Britta Simon to Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="b8878-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b8878-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="b8878-219">In the applications list, select **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="b8878-219">In the applications list, select **Showpad**.</span></span>

    ![Configure Single Sign-On](./media/showpad-tutorial/tutorial_showpad_app.png) 

1. <span data-ttu-id="b8878-221">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b8878-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="b8878-223">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b8878-223">Click **Add** button.</span></span> <span data-ttu-id="b8878-224">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b8878-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="b8878-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b8878-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="b8878-227">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b8878-227">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="b8878-228">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b8878-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b8878-229">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="b8878-229">Testing single sign-on</span></span>

<span data-ttu-id="b8878-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b8878-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b8878-231">When you click the Showpad tile in the Access Panel, you should get automatically signed-on to Showpad application.</span><span class="sxs-lookup"><span data-stu-id="b8878-231">When you click the Showpad tile in the Access Panel, you should get automatically signed-on to Showpad application.</span></span>
<span data-ttu-id="b8878-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b8878-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b8878-233">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b8878-233">Additional resources</span></span>

* [<span data-ttu-id="b8878-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8878-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b8878-235">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b8878-235">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/showpad-tutorial/tutorial_general_01.png
[2]: ./media/showpad-tutorial/tutorial_general_02.png
[3]: ./media/showpad-tutorial/tutorial_general_03.png
[4]: ./media/showpad-tutorial/tutorial_general_04.png

[100]: ./media/showpad-tutorial/tutorial_general_100.png

[200]: ./media/showpad-tutorial/tutorial_general_200.png
[201]: ./media/showpad-tutorial/tutorial_general_201.png
[202]: ./media/showpad-tutorial/tutorial_general_202.png
[203]: ./media/showpad-tutorial/tutorial_general_203.png

