---
title: 'Tutorial: Azure Active Directory integration with 23 Video | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 23 Video.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 8b4b41551a1679948518846a63eee87bbd1bbfd9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870542"
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="c958a-103">Tutorial: Azure Active Directory integration with 23 Video</span><span class="sxs-lookup"><span data-stu-id="c958a-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="c958a-104">In this tutorial, you learn how to integrate 23 Video with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c958a-104">In this tutorial, you learn how to integrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c958a-105">Integrating 23 Video with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c958a-105">Integrating 23 Video with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c958a-106">You can control in Azure AD who has access to 23 Video</span><span class="sxs-lookup"><span data-stu-id="c958a-106">You can control in Azure AD who has access to 23 Video</span></span>
- <span data-ttu-id="c958a-107">You can enable your users to automatically get signed-on to 23 Video (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c958a-107">You can enable your users to automatically get signed-on to 23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c958a-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c958a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c958a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c958a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c958a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c958a-110">Prerequisites</span></span>

<span data-ttu-id="c958a-111">To configure Azure AD integration with 23 Video, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c958a-111">To configure Azure AD integration with 23 Video, you need the following items:</span></span>

- <span data-ttu-id="c958a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c958a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c958a-113">A 23 Video single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c958a-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c958a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c958a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c958a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c958a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c958a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c958a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c958a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c958a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c958a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c958a-118">Scenario description</span></span>
<span data-ttu-id="c958a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c958a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c958a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c958a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c958a-121">Adding 23 Video from the gallery</span><span class="sxs-lookup"><span data-stu-id="c958a-121">Adding 23 Video from the gallery</span></span>
2. <span data-ttu-id="c958a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c958a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-the-gallery"></a><span data-ttu-id="c958a-123">Adding 23 Video from the gallery</span><span class="sxs-lookup"><span data-stu-id="c958a-123">Adding 23 Video from the gallery</span></span>
<span data-ttu-id="c958a-124">To configure the integration of 23 Video into Azure AD, you need to add 23 Video from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c958a-124">To configure the integration of 23 Video into Azure AD, you need to add 23 Video from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c958a-125">**To add 23 Video from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c958a-125">**To add 23 Video from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c958a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c958a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c958a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c958a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c958a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c958a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c958a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c958a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c958a-133">In the search box, type **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="c958a-133">In the search box, type **23 Video**.</span></span>

    ![Creating an Azure AD test user](./media/23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="c958a-135">In the results panel, select **23 Video**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c958a-135">In the results panel, select **23 Video**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c958a-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c958a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c958a-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c958a-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c958a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 23 Video is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c958a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 23 Video is to a user in Azure AD.</span></span> <span data-ttu-id="c958a-140">In other words, a link relationship between an Azure AD user and the related user in 23 Video needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c958a-140">In other words, a link relationship between an Azure AD user and the related user in 23 Video needs to be established.</span></span>

<span data-ttu-id="c958a-141">In 23 Video, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c958a-141">In 23 Video, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c958a-142">To configure and test Azure AD single sign-on with 23 Video, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c958a-142">To configure and test Azure AD single sign-on with 23 Video, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c958a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c958a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c958a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c958a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c958a-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - to have a counterpart of Britta Simon in 23 Video that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c958a-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - to have a counterpart of Britta Simon in 23 Video that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c958a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c958a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c958a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c958a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c958a-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c958a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c958a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 23 Video application.</span><span class="sxs-lookup"><span data-stu-id="c958a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="c958a-150">**To configure Azure AD single sign-on with 23 Video, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c958a-150">**To configure Azure AD single sign-on with 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="c958a-151">In the Azure portal, on the **23 Video** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c958a-151">In the Azure portal, on the **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="c958a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c958a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="c958a-155">On the **23 Video Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c958a-155">On the **23 Video Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="c958a-157">a.</span><span class="sxs-lookup"><span data-stu-id="c958a-157">a.</span></span> <span data-ttu-id="c958a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="c958a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="c958a-159">b.</span><span class="sxs-lookup"><span data-stu-id="c958a-159">b.</span></span> <span data-ttu-id="c958a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="c958a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c958a-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="c958a-161">These values are not real.</span></span> <span data-ttu-id="c958a-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="c958a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c958a-163">Contact [23 Video Client support team](mailto:support@23company.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="c958a-163">Contact [23 Video Client support team](mailto:support@23company.com) to get these values.</span></span> 
 
4. <span data-ttu-id="c958a-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c958a-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="c958a-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c958a-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c958a-168">On the **23 Video Configuration** section, click **Configure 23 Video** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="c958a-168">On the **23 Video Configuration** section, click **Configure 23 Video** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c958a-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="c958a-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="c958a-171">To configure single sign-on on **23 Video** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [23 Video support team](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="c958a-171">To configure single sign-on on **23 Video** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="c958a-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="c958a-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c958a-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="c958a-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c958a-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c958a-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c958a-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c958a-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="c958a-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c958a-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="c958a-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c958a-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c958a-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c958a-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c958a-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c958a-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c958a-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="c958a-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c958a-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c958a-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c958a-187">a.</span><span class="sxs-lookup"><span data-stu-id="c958a-187">a.</span></span> <span data-ttu-id="c958a-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c958a-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c958a-189">b.</span><span class="sxs-lookup"><span data-stu-id="c958a-189">b.</span></span> <span data-ttu-id="c958a-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c958a-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c958a-191">c.</span><span class="sxs-lookup"><span data-stu-id="c958a-191">c.</span></span> <span data-ttu-id="c958a-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="c958a-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c958a-193">d.</span><span class="sxs-lookup"><span data-stu-id="c958a-193">d.</span></span> <span data-ttu-id="c958a-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c958a-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="c958a-195">Creating a 23 Video test user</span><span class="sxs-lookup"><span data-stu-id="c958a-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="c958a-196">The objective of this section is to create a user called Britta Simon in 23 Video.</span><span class="sxs-lookup"><span data-stu-id="c958a-196">The objective of this section is to create a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="c958a-197">**To create a user called Britta Simon in 23 Video, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c958a-197">**To create a user called Britta Simon in 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="c958a-198">Sign on to your 23 Video company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="c958a-198">Sign on to your 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="c958a-199">Go to **Settings**.</span><span class="sxs-lookup"><span data-stu-id="c958a-199">Go to **Settings**.</span></span>
 
3. <span data-ttu-id="c958a-200">In **Users** section, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="c958a-200">In **Users** section, click **Configure**.</span></span>
   
    ![Assign User][400]

4. <span data-ttu-id="c958a-202">Click **Add a new user**.</span><span class="sxs-lookup"><span data-stu-id="c958a-202">Click **Add a new user**.</span></span> 
   
    ![Assign User][401]

5. <span data-ttu-id="c958a-204">In the **Invite someone to join this site** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c958a-204">In the **Invite someone to join this site** section, perform the following steps:</span></span>
   
    ![Assign User][402]

    <span data-ttu-id="c958a-206">a.</span><span class="sxs-lookup"><span data-stu-id="c958a-206">a.</span></span> <span data-ttu-id="c958a-207">In the **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c958a-207">In the **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="c958a-208">b.</span><span class="sxs-lookup"><span data-stu-id="c958a-208">b.</span></span> <span data-ttu-id="c958a-209">Click **Add the user**.</span><span class="sxs-lookup"><span data-stu-id="c958a-209">Click **Add the user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c958a-210">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c958a-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c958a-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 23 Video.</span><span class="sxs-lookup"><span data-stu-id="c958a-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 23 Video.</span></span>

![Assign User][200] 

<span data-ttu-id="c958a-213">**To assign Britta Simon to 23 Video, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c958a-213">**To assign Britta Simon to 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="c958a-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c958a-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="c958a-216">In the applications list, select **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="c958a-216">In the applications list, select **23 Video**.</span></span>

    ![Configure Single Sign-On](./media/23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="c958a-218">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c958a-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="c958a-220">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c958a-220">Click **Add** button.</span></span> <span data-ttu-id="c958a-221">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c958a-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="c958a-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c958a-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c958a-224">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c958a-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c958a-225">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c958a-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c958a-226">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="c958a-226">Testing single sign-on</span></span>

<span data-ttu-id="c958a-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c958a-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c958a-228">When you click the 23 Video tile in the Access Panel, you should get automatically signed-on to your 23 Video application.</span><span class="sxs-lookup"><span data-stu-id="c958a-228">When you click the 23 Video tile in the Access Panel, you should get automatically signed-on to your 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c958a-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c958a-229">Additional resources</span></span>

* [<span data-ttu-id="c958a-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c958a-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c958a-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c958a-231">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/23video-tutorial/tutorial_general_01.png
[2]: ./media/23video-tutorial/tutorial_general_02.png
[3]: ./media/23video-tutorial/tutorial_general_03.png
[4]: ./media/23video-tutorial/tutorial_general_04.png

[100]: ./media/23video-tutorial/tutorial_general_100.png

[200]: ./media/23video-tutorial/tutorial_general_200.png
[201]: ./media/23video-tutorial/tutorial_general_201.png
[202]: ./media/23video-tutorial/tutorial_general_202.png
[203]: ./media/23video-tutorial/tutorial_general_203.png

[400]: ./media/23video-tutorial/tutorial_23video_10.png
[401]: ./media/23video-tutorial/tutorial_23video_11.png
[402]: ./media/23video-tutorial/tutorial_23video_12.png
