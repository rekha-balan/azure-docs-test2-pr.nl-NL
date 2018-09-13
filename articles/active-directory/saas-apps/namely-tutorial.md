---
title: 'Tutorial: Azure Active Directory integration with Namely | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Namely.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 344de0d5f09d33146fd5065a7dc723038b492273
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864773"
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="7ec19-103">Tutorial: Azure Active Directory integration with Namely</span><span class="sxs-lookup"><span data-stu-id="7ec19-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="7ec19-104">In this tutorial, you learn how to integrate Namely with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ec19-104">In this tutorial, you learn how to integrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ec19-105">Integrating Namely with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7ec19-105">Integrating Namely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7ec19-106">You can control in Azure AD who has access to Namely</span><span class="sxs-lookup"><span data-stu-id="7ec19-106">You can control in Azure AD who has access to Namely</span></span>
- <span data-ttu-id="7ec19-107">You can enable your users to automatically get signed-on to Namely (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7ec19-107">You can enable your users to automatically get signed-on to Namely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ec19-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7ec19-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7ec19-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7ec19-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ec19-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7ec19-110">Prerequisites</span></span>

<span data-ttu-id="7ec19-111">To configure Azure AD integration with Namely, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7ec19-111">To configure Azure AD integration with Namely, you need the following items:</span></span>

- <span data-ttu-id="7ec19-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7ec19-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ec19-113">A Namely single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7ec19-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ec19-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7ec19-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ec19-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7ec19-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ec19-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7ec19-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ec19-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ec19-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ec19-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7ec19-118">Scenario description</span></span>
<span data-ttu-id="7ec19-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7ec19-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ec19-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7ec19-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ec19-121">Adding Namely from the gallery</span><span class="sxs-lookup"><span data-stu-id="7ec19-121">Adding Namely from the gallery</span></span>
1. <span data-ttu-id="7ec19-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7ec19-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-the-gallery"></a><span data-ttu-id="7ec19-123">Adding Namely from the gallery</span><span class="sxs-lookup"><span data-stu-id="7ec19-123">Adding Namely from the gallery</span></span>
<span data-ttu-id="7ec19-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7ec19-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7ec19-125">**To add Namely from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7ec19-125">**To add Namely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7ec19-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7ec19-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="7ec19-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7ec19-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="7ec19-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7ec19-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="7ec19-133">In the search box, type **Namely**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-133">In the search box, type **Namely**.</span></span>

    ![Creating an Azure AD test user](./media/namely-tutorial/tutorial_namely_search.png)

1. <span data-ttu-id="7ec19-135">In the results panel, select **Namely**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7ec19-135">In the results panel, select **Namely**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ec19-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7ec19-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ec19-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7ec19-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ec19-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Namely is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ec19-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Namely is to a user in Azure AD.</span></span> <span data-ttu-id="7ec19-140">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7ec19-140">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span></span>

<span data-ttu-id="7ec19-141">In Namely, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="7ec19-141">In Namely, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7ec19-142">To configure and test Azure AD single sign-on with Namely, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7ec19-142">To configure and test Azure AD single sign-on with Namely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7ec19-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7ec19-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7ec19-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ec19-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7ec19-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7ec19-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7ec19-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ec19-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7ec19-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7ec19-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ec19-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7ec19-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ec19-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Namely application.</span><span class="sxs-lookup"><span data-stu-id="7ec19-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="7ec19-150">**To configure Azure AD single sign-on with Namely, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7ec19-150">**To configure Azure AD single sign-on with Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="7ec19-151">In the Azure portal, on the **Namely** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-151">In the Azure portal, on the **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="7ec19-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ec19-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_samlbase.png)

1. <span data-ttu-id="7ec19-155">On the **Namely Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7ec19-155">On the **Namely Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="7ec19-157">a.</span><span class="sxs-lookup"><span data-stu-id="7ec19-157">a.</span></span> <span data-ttu-id="7ec19-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="7ec19-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="7ec19-159">b.</span><span class="sxs-lookup"><span data-stu-id="7ec19-159">b.</span></span> <span data-ttu-id="7ec19-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="7ec19-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ec19-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7ec19-161">These values are not real.</span></span> <span data-ttu-id="7ec19-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="7ec19-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7ec19-163">Contact [Namely Client support team](https://www.namely.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7ec19-163">Contact [Namely Client support team](https://www.namely.com/contact/) to get these values.</span></span> 
 
1. <span data-ttu-id="7ec19-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7ec19-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_certificate.png) 

1. <span data-ttu-id="7ec19-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7ec19-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="7ec19-168">On the **Namely Configuration** section, click **Configure Namely** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="7ec19-168">On the **Namely Configuration** section, click **Configure Namely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7ec19-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="7ec19-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_configure.png) 

1. <span data-ttu-id="7ec19-171">In another browser window, sign on to your Namely company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7ec19-171">In another browser window, sign on to your Namely company site as an administrator.</span></span>

1. <span data-ttu-id="7ec19-172">In the toolbar on the top, click **Company**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-172">In the toolbar on the top, click **Company**.</span></span>
   
    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_06.png) 

1. <span data-ttu-id="7ec19-174">Click the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="7ec19-174">Click the **Settings** tab.</span></span>
   
    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_07.png) 

1. <span data-ttu-id="7ec19-176">Click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-176">Click **SAML**.</span></span>
   
    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_08.png) 

1. <span data-ttu-id="7ec19-178">On the **SAML Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7ec19-178">On the **SAML Settings** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="7ec19-180">a.</span><span class="sxs-lookup"><span data-stu-id="7ec19-180">a.</span></span> <span data-ttu-id="7ec19-181">Click **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="7ec19-182">b.</span><span class="sxs-lookup"><span data-stu-id="7ec19-182">b.</span></span> <span data-ttu-id="7ec19-183">In the **Identity provider SSO url** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7ec19-183">In the **Identity provider SSO url** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="7ec19-184">c.</span><span class="sxs-lookup"><span data-stu-id="7ec19-184">c.</span></span> <span data-ttu-id="7ec19-185">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="7ec19-185">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="7ec19-186">d.</span><span class="sxs-lookup"><span data-stu-id="7ec19-186">d.</span></span> <span data-ttu-id="7ec19-187">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7ec19-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="7ec19-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7ec19-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="7ec19-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7ec19-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ec19-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ec19-191">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7ec19-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ec19-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ec19-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="7ec19-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7ec19-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7ec19-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7ec19-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/namely-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="7ec19-197">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/namely-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="7ec19-199">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="7ec19-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/namely-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="7ec19-201">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7ec19-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ec19-203">a.</span><span class="sxs-lookup"><span data-stu-id="7ec19-203">a.</span></span> <span data-ttu-id="7ec19-204">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ec19-205">b.</span><span class="sxs-lookup"><span data-stu-id="7ec19-205">b.</span></span> <span data-ttu-id="7ec19-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7ec19-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ec19-207">c.</span><span class="sxs-lookup"><span data-stu-id="7ec19-207">c.</span></span> <span data-ttu-id="7ec19-208">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7ec19-209">d.</span><span class="sxs-lookup"><span data-stu-id="7ec19-209">d.</span></span> <span data-ttu-id="7ec19-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="7ec19-211">Creating a Namely test user</span><span class="sxs-lookup"><span data-stu-id="7ec19-211">Creating a Namely test user</span></span>

<span data-ttu-id="7ec19-212">The objective of this section is to create a user called Britta Simon in Namely.</span><span class="sxs-lookup"><span data-stu-id="7ec19-212">The objective of this section is to create a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="7ec19-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7ec19-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="7ec19-214">Sign-on to your Namely company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7ec19-214">Sign-on to your Namely company site as an administrator.</span></span>

1. <span data-ttu-id="7ec19-215">In the toolbar on the top, click **People**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-215">In the toolbar on the top, click **People**.</span></span>
   
    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_10.png) 

1. <span data-ttu-id="7ec19-217">Click the **Directory** tab.</span><span class="sxs-lookup"><span data-stu-id="7ec19-217">Click the **Directory** tab.</span></span>
   
    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_11.png) 

1. <span data-ttu-id="7ec19-219">Click **Add New Person**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-219">Click **Add New Person**.</span></span>

    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_12.png)

1. <span data-ttu-id="7ec19-221">On the **Add New Person** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7ec19-221">On the **Add New Person** dialog, perform the following steps:</span></span>

    <span data-ttu-id="7ec19-222">a.</span><span class="sxs-lookup"><span data-stu-id="7ec19-222">a.</span></span> <span data-ttu-id="7ec19-223">In the **First name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-223">In the **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="7ec19-224">b.</span><span class="sxs-lookup"><span data-stu-id="7ec19-224">b.</span></span> <span data-ttu-id="7ec19-225">In the **Last name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-225">In the **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="7ec19-226">c.</span><span class="sxs-lookup"><span data-stu-id="7ec19-226">c.</span></span> <span data-ttu-id="7ec19-227">In the **Email** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7ec19-227">In the **Email** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ec19-228">d.</span><span class="sxs-lookup"><span data-stu-id="7ec19-228">d.</span></span> <span data-ttu-id="7ec19-229">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-229">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7ec19-230">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7ec19-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7ec19-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Namely.</span><span class="sxs-lookup"><span data-stu-id="7ec19-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Namely.</span></span>

![Assign User][200] 

<span data-ttu-id="7ec19-233">**To assign Britta Simon to Namely, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7ec19-233">**To assign Britta Simon to Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="7ec19-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7ec19-236">In the applications list, select **Namely**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-236">In the applications list, select **Namely**.</span></span>

    ![Configure Single Sign-On](./media/namely-tutorial/tutorial_namely_app.png) 

1. <span data-ttu-id="7ec19-238">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7ec19-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="7ec19-240">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7ec19-240">Click **Add** button.</span></span> <span data-ttu-id="7ec19-241">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7ec19-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="7ec19-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7ec19-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7ec19-244">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7ec19-244">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7ec19-245">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7ec19-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ec19-246">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="7ec19-246">Testing single sign-on</span></span>

<span data-ttu-id="7ec19-247">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7ec19-247">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7ec19-248">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application</span><span class="sxs-lookup"><span data-stu-id="7ec19-248">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ec19-249">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7ec19-249">Additional resources</span></span>

* [<span data-ttu-id="7ec19-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ec19-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7ec19-251">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7ec19-251">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/namely-tutorial/tutorial_general_01.png
[2]: ./media/namely-tutorial/tutorial_general_02.png
[3]: ./media/namely-tutorial/tutorial_general_03.png
[4]: ./media/namely-tutorial/tutorial_general_04.png

[100]: ./media/namely-tutorial/tutorial_general_100.png

[200]: ./media/namely-tutorial/tutorial_general_200.png
[201]: ./media/namely-tutorial/tutorial_general_201.png
[202]: ./media/namely-tutorial/tutorial_general_202.png
[203]: ./media/namely-tutorial/tutorial_general_203.png

