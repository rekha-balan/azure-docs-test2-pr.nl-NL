---
title: 'Tutorial: Azure Active Directory integration with Humanity | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Humanity.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 5858300027d77b6057e059960f1c997b4bfc1e56
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870497"
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="37e4e-103">Tutorial: Azure Active Directory integration with Humanity</span><span class="sxs-lookup"><span data-stu-id="37e4e-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="37e4e-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37e4e-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37e4e-105">Integrating Humanity with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="37e4e-105">Integrating Humanity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37e4e-106">You can control in Azure AD who has access to Humanity</span><span class="sxs-lookup"><span data-stu-id="37e4e-106">You can control in Azure AD who has access to Humanity</span></span>
- <span data-ttu-id="37e4e-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="37e4e-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37e4e-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="37e4e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="37e4e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="37e4e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37e4e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="37e4e-110">Prerequisites</span></span>

<span data-ttu-id="37e4e-111">To configure Azure AD integration with Humanity, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="37e4e-111">To configure Azure AD integration with Humanity, you need the following items:</span></span>

- <span data-ttu-id="37e4e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="37e4e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37e4e-113">A Humanity single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="37e4e-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37e4e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="37e4e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37e4e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="37e4e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37e4e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="37e4e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37e4e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37e4e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37e4e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="37e4e-118">Scenario description</span></span>
<span data-ttu-id="37e4e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="37e4e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37e4e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="37e4e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37e4e-121">Adding Humanity from the gallery</span><span class="sxs-lookup"><span data-stu-id="37e4e-121">Adding Humanity from the gallery</span></span>
1. <span data-ttu-id="37e4e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="37e4e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-the-gallery"></a><span data-ttu-id="37e4e-123">Adding Humanity from the gallery</span><span class="sxs-lookup"><span data-stu-id="37e4e-123">Adding Humanity from the gallery</span></span>
<span data-ttu-id="37e4e-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="37e4e-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37e4e-125">**To add Humanity from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="37e4e-125">**To add Humanity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="37e4e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="37e4e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="37e4e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="37e4e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="37e4e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="37e4e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="37e4e-133">In the search box, type **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-133">In the search box, type **Humanity**.</span></span>

    ![Creating an Azure AD test user](./media/shiftplanning-tutorial/tutorial_humanity_search.png)

1. <span data-ttu-id="37e4e-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="37e4e-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37e4e-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="37e4e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37e4e-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="37e4e-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="37e4e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37e4e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span></span> <span data-ttu-id="37e4e-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span><span class="sxs-lookup"><span data-stu-id="37e4e-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span></span>

<span data-ttu-id="37e4e-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="37e4e-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="37e4e-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="37e4e-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="37e4e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="37e4e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="37e4e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37e4e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="37e4e-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="37e4e-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="37e4e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="37e4e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="37e4e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="37e4e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37e4e-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="37e4e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37e4e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span><span class="sxs-lookup"><span data-stu-id="37e4e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="37e4e-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="37e4e-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="37e4e-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="37e4e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="37e4e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/shiftplanning-tutorial/tutorial_humanity_samlbase.png)

1. <span data-ttu-id="37e4e-155">On the **Humanity Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="37e4e-155">On the **Humanity Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="37e4e-157">a.</span><span class="sxs-lookup"><span data-stu-id="37e4e-157">a.</span></span> <span data-ttu-id="37e4e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="37e4e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="37e4e-159">b.</span><span class="sxs-lookup"><span data-stu-id="37e4e-159">b.</span></span> <span data-ttu-id="37e4e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="37e4e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37e4e-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="37e4e-161">These values are not real.</span></span> <span data-ttu-id="37e4e-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="37e4e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="37e4e-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="37e4e-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span></span> 
 
1. <span data-ttu-id="37e4e-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="37e4e-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/shiftplanning-tutorial/tutorial_humanity_certificate.png) 

1. <span data-ttu-id="37e4e-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="37e4e-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/shiftplanning-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="37e4e-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="37e4e-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="37e4e-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="37e4e-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/shiftplanning-tutorial/tutorial_humanity_configure.png) 

1. <span data-ttu-id="37e4e-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="37e4e-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span></span>

1. <span data-ttu-id="37e4e-172">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="37e4e-173">![Admin](./media/shiftplanning-tutorial/iC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="37e4e-173">![Admin](./media/shiftplanning-tutorial/iC786619.png "Admin")</span></span>

1. <span data-ttu-id="37e4e-174">Under **Integration**, click **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="37e4e-175">![Single Sign-On](./media/shiftplanning-tutorial/iC786620.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="37e4e-175">![Single Sign-On](./media/shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

1. <span data-ttu-id="37e4e-176">In the **Single Sign-On** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="37e4e-176">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="37e4e-177">![Single Sign-On](./media/shiftplanning-tutorial/iC786905.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="37e4e-177">![Single Sign-On](./media/shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="37e4e-178">a.</span><span class="sxs-lookup"><span data-stu-id="37e4e-178">a.</span></span> <span data-ttu-id="37e4e-179">Select **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="37e4e-180">b.</span><span class="sxs-lookup"><span data-stu-id="37e4e-180">b.</span></span> <span data-ttu-id="37e4e-181">Select **Allow Password Login**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="37e4e-182">c.</span><span class="sxs-lookup"><span data-stu-id="37e4e-182">c.</span></span> <span data-ttu-id="37e4e-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="37e4e-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="37e4e-184">d.</span><span class="sxs-lookup"><span data-stu-id="37e4e-184">d.</span></span> <span data-ttu-id="37e4e-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="37e4e-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="37e4e-186">e.</span><span class="sxs-lookup"><span data-stu-id="37e4e-186">e.</span></span> <span data-ttu-id="37e4e-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="37e4e-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>

1. <span data-ttu-id="37e4e-188">Click **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="37e4e-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="37e4e-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="37e4e-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="37e4e-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="37e4e-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37e4e-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37e4e-192">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="37e4e-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="37e4e-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37e4e-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="37e4e-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="37e4e-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="37e4e-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="37e4e-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/shiftplanning-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="37e4e-198">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/shiftplanning-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="37e4e-200">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="37e4e-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/shiftplanning-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="37e4e-202">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="37e4e-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37e4e-204">a.</span><span class="sxs-lookup"><span data-stu-id="37e4e-204">a.</span></span> <span data-ttu-id="37e4e-205">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37e4e-206">b.</span><span class="sxs-lookup"><span data-stu-id="37e4e-206">b.</span></span> <span data-ttu-id="37e4e-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37e4e-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37e4e-208">c.</span><span class="sxs-lookup"><span data-stu-id="37e4e-208">c.</span></span> <span data-ttu-id="37e4e-209">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="37e4e-210">d.</span><span class="sxs-lookup"><span data-stu-id="37e4e-210">d.</span></span> <span data-ttu-id="37e4e-211">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="37e4e-212">Creating a Humanity test user</span><span class="sxs-lookup"><span data-stu-id="37e4e-212">Creating a Humanity test user</span></span>

<span data-ttu-id="37e4e-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span><span class="sxs-lookup"><span data-stu-id="37e4e-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="37e4e-214">In the case of Humanity, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="37e4e-214">In the case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="37e4e-215">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="37e4e-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="37e4e-216">Log in to your **Humanity** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="37e4e-216">Log in to your **Humanity** company site as an administrator.</span></span>

1. <span data-ttu-id="37e4e-217">Click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="37e4e-218">![Admin](./media/shiftplanning-tutorial/iC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="37e4e-218">![Admin](./media/shiftplanning-tutorial/iC786619.png "Admin")</span></span>

1. <span data-ttu-id="37e4e-219">Click **Staff**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="37e4e-220">![Staff](./media/shiftplanning-tutorial/ic786623.png "Staff")</span><span class="sxs-lookup"><span data-stu-id="37e4e-220">![Staff](./media/shiftplanning-tutorial/ic786623.png "Staff")</span></span>

1. <span data-ttu-id="37e4e-221">Under **Actions**, click **Add Employees**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="37e4e-222">![Add Employees](./media/shiftplanning-tutorial/iC786624.png "Add Employees")</span><span class="sxs-lookup"><span data-stu-id="37e4e-222">![Add Employees](./media/shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

1. <span data-ttu-id="37e4e-223">In the **Add Employees** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="37e4e-223">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="37e4e-224">![Save Employees](./media/shiftplanning-tutorial/iC786625.png "Save Employees")</span><span class="sxs-lookup"><span data-stu-id="37e4e-224">![Save Employees](./media/shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="37e4e-225">a.</span><span class="sxs-lookup"><span data-stu-id="37e4e-225">a.</span></span> <span data-ttu-id="37e4e-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="37e4e-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="37e4e-227">b.</span><span class="sxs-lookup"><span data-stu-id="37e4e-227">b.</span></span> <span data-ttu-id="37e4e-228">Click **Save Employees**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="37e4e-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="37e4e-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="37e4e-230">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="37e4e-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="37e4e-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span><span class="sxs-lookup"><span data-stu-id="37e4e-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span></span>

![Assign User][200] 

<span data-ttu-id="37e4e-233">**To assign Britta Simon to Humanity, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="37e4e-233">**To assign Britta Simon to Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="37e4e-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="37e4e-236">In the applications list, select **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-236">In the applications list, select **Humanity**.</span></span>

    ![Configure Single Sign-On](./media/shiftplanning-tutorial/tutorial_humanity_app.png) 

1. <span data-ttu-id="37e4e-238">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="37e4e-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="37e4e-240">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="37e4e-240">Click **Add** button.</span></span> <span data-ttu-id="37e4e-241">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="37e4e-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="37e4e-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="37e4e-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="37e4e-244">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="37e4e-244">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="37e4e-245">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="37e4e-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37e4e-246">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="37e4e-246">Testing single sign-on</span></span>

<span data-ttu-id="37e4e-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="37e4e-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="37e4e-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span><span class="sxs-lookup"><span data-stu-id="37e4e-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span></span>
<span data-ttu-id="37e4e-249">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="37e4e-249">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37e4e-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="37e4e-250">Additional resources</span></span>

* [<span data-ttu-id="37e4e-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37e4e-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="37e4e-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37e4e-252">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/shiftplanning-tutorial/tutorial_general_203.png

