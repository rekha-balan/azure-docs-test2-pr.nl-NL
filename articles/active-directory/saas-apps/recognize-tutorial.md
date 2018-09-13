---
title: 'Tutorial: Azure Active Directory integration with Recognize | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Recognize.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: b2d5acfcb722845d7f346668597c073319f273f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857914"
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="645c4-103">Tutorial: Azure Active Directory integration with Recognize</span><span class="sxs-lookup"><span data-stu-id="645c4-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="645c4-104">In this tutorial, you learn how to integrate Recognize with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="645c4-104">In this tutorial, you learn how to integrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="645c4-105">Integrating Recognize with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="645c4-105">Integrating Recognize with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="645c4-106">You can control in Azure AD who has access to Recognize</span><span class="sxs-lookup"><span data-stu-id="645c4-106">You can control in Azure AD who has access to Recognize</span></span>
- <span data-ttu-id="645c4-107">You can enable your users to automatically get signed-on to Recognize (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="645c4-107">You can enable your users to automatically get signed-on to Recognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="645c4-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="645c4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="645c4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="645c4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="645c4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="645c4-110">Prerequisites</span></span>

<span data-ttu-id="645c4-111">To configure Azure AD integration with Recognize, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="645c4-111">To configure Azure AD integration with Recognize, you need the following items:</span></span>

- <span data-ttu-id="645c4-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="645c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="645c4-113">A Recognize single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="645c4-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="645c4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="645c4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="645c4-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="645c4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="645c4-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="645c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="645c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="645c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="645c4-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="645c4-118">Scenario description</span></span>
<span data-ttu-id="645c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="645c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="645c4-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="645c4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="645c4-121">Adding Recognize from the gallery</span><span class="sxs-lookup"><span data-stu-id="645c4-121">Adding Recognize from the gallery</span></span>
1. <span data-ttu-id="645c4-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="645c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-the-gallery"></a><span data-ttu-id="645c4-123">Adding Recognize from the gallery</span><span class="sxs-lookup"><span data-stu-id="645c4-123">Adding Recognize from the gallery</span></span>
<span data-ttu-id="645c4-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="645c4-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="645c4-125">**To add Recognize from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="645c4-125">**To add Recognize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="645c4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="645c4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="645c4-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="645c4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="645c4-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="645c4-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="645c4-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="645c4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="645c4-133">In the search box, type **Recognize**.</span><span class="sxs-lookup"><span data-stu-id="645c4-133">In the search box, type **Recognize**.</span></span>

    ![Creating an Azure AD test user](./media/recognize-tutorial/tutorial_recognize_search.png)

1. <span data-ttu-id="645c4-135">In the results panel, select **Recognize**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="645c4-135">In the results panel, select **Recognize**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="645c4-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="645c4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="645c4-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="645c4-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="645c4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Recognize is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="645c4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Recognize is to a user in Azure AD.</span></span> <span data-ttu-id="645c4-140">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span><span class="sxs-lookup"><span data-stu-id="645c4-140">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span></span>

<span data-ttu-id="645c4-141">In Recognize, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="645c4-141">In Recognize, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="645c4-142">To configure and test Azure AD single sign-on with Recognize, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="645c4-142">To configure and test Azure AD single sign-on with Recognize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="645c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="645c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="645c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="645c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="645c4-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="645c4-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="645c4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="645c4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="645c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="645c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="645c4-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="645c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="645c4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Recognize application.</span><span class="sxs-lookup"><span data-stu-id="645c4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="645c4-150">**To configure Azure AD single sign-on with Recognize, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="645c4-150">**To configure Azure AD single sign-on with Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="645c4-151">In the Azure portal, on the **Recognize** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="645c4-151">In the Azure portal, on the **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="645c4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="645c4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/recognize-tutorial/tutorial_recognize_samlbase.png)

1. <span data-ttu-id="645c4-155">On the **Recognize Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="645c4-155">On the **Recognize Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="645c4-157">a.</span><span class="sxs-lookup"><span data-stu-id="645c4-157">a.</span></span> <span data-ttu-id="645c4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="645c4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="645c4-159">b.</span><span class="sxs-lookup"><span data-stu-id="645c4-159">b.</span></span> <span data-ttu-id="645c4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="645c4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="645c4-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="645c4-161">These values are not real.</span></span> <span data-ttu-id="645c4-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="645c4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="645c4-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="645c4-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that is explained later in the tutorial.</span></span> <span data-ttu-id="645c4-164">.</span><span class="sxs-lookup"><span data-stu-id="645c4-164">.</span></span> 
 
1. <span data-ttu-id="645c4-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="645c4-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/recognize-tutorial/tutorial_recognize_certificate.png) 

1. <span data-ttu-id="645c4-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="645c4-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/recognize-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="645c4-169">On the **Recognize Configuration** section, click **Configure Recognize** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="645c4-169">On the **Recognize Configuration** section, click **Configure Recognize** to open **Configure sign-on** window.</span></span> <span data-ttu-id="645c4-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="645c4-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/recognize-tutorial/tutorial_recognize_configure.png) 

1. <span data-ttu-id="645c4-172">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="645c4-172">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span></span>

1. <span data-ttu-id="645c4-173">On the upper right corner, click **Menu**.</span><span class="sxs-lookup"><span data-stu-id="645c4-173">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="645c4-174">Go to **Company Admin**.</span><span class="sxs-lookup"><span data-stu-id="645c4-174">Go to **Company Admin**.</span></span>
   
    ![Configure Single Sign-On On App side](./media/recognize-tutorial/tutorial_recognize_000.png)

1. <span data-ttu-id="645c4-176">On the left navigation pane, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="645c4-176">On the left navigation pane, click **Settings**.</span></span>
   
    ![Configure Single Sign-On On App side](./media/recognize-tutorial/tutorial_recognize_001.png)

1. <span data-ttu-id="645c4-178">Perform the following steps on **SSO Settings** section.</span><span class="sxs-lookup"><span data-stu-id="645c4-178">Perform the following steps on **SSO Settings** section.</span></span>
   
    ![Configure Single Sign-On On App side](./media/recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="645c4-180">a.</span><span class="sxs-lookup"><span data-stu-id="645c4-180">a.</span></span> <span data-ttu-id="645c4-181">As **Enable SSO**, select **ON**.</span><span class="sxs-lookup"><span data-stu-id="645c4-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="645c4-182">b.</span><span class="sxs-lookup"><span data-stu-id="645c4-182">b.</span></span> <span data-ttu-id="645c4-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="645c4-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="645c4-184">c.</span><span class="sxs-lookup"><span data-stu-id="645c4-184">c.</span></span> <span data-ttu-id="645c4-185">In the **Sso target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="645c4-185">In the **Sso target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="645c4-186">d.</span><span class="sxs-lookup"><span data-stu-id="645c4-186">d.</span></span> <span data-ttu-id="645c4-187">In the **Slo target url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="645c4-187">In the **Slo target url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="645c4-188">e.</span><span class="sxs-lookup"><span data-stu-id="645c4-188">e.</span></span> <span data-ttu-id="645c4-189">Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="645c4-189">Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="645c4-190">f.</span><span class="sxs-lookup"><span data-stu-id="645c4-190">f.</span></span> <span data-ttu-id="645c4-191">Click the **Save settings** button.</span><span class="sxs-lookup"><span data-stu-id="645c4-191">Click the **Save settings** button.</span></span> 

1. <span data-ttu-id="645c4-192">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span><span class="sxs-lookup"><span data-stu-id="645c4-192">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span></span>
   
    ![Configure Single Sign-On On App side](./media/recognize-tutorial/tutorial_recognize_003.png)

1. <span data-ttu-id="645c4-194">Open the **Metadata URL link** under a blank browser to download the metadata document.</span><span class="sxs-lookup"><span data-stu-id="645c4-194">Open the **Metadata URL link** under a blank browser to download the metadata document.</span></span> <span data-ttu-id="645c4-195">Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="645c4-195">Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Configure Single Sign-On On App side](./media/recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="645c4-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="645c4-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="645c4-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="645c4-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="645c4-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="645c4-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="645c4-200">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="645c4-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="645c4-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="645c4-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="645c4-203">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="645c4-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="645c4-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="645c4-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/recognize-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="645c4-206">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="645c4-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/recognize-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="645c4-208">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="645c4-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/recognize-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="645c4-210">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="645c4-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="645c4-212">a.</span><span class="sxs-lookup"><span data-stu-id="645c4-212">a.</span></span> <span data-ttu-id="645c4-213">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="645c4-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="645c4-214">b.</span><span class="sxs-lookup"><span data-stu-id="645c4-214">b.</span></span> <span data-ttu-id="645c4-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="645c4-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="645c4-216">c.</span><span class="sxs-lookup"><span data-stu-id="645c4-216">c.</span></span> <span data-ttu-id="645c4-217">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="645c4-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="645c4-218">d.</span><span class="sxs-lookup"><span data-stu-id="645c4-218">d.</span></span> <span data-ttu-id="645c4-219">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="645c4-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="645c4-220">Creating a Recognize test user</span><span class="sxs-lookup"><span data-stu-id="645c4-220">Creating a Recognize test user</span></span>

<span data-ttu-id="645c4-221">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span><span class="sxs-lookup"><span data-stu-id="645c4-221">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="645c4-222">In the case of Recognize, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="645c4-222">In the case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="645c4-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span><span class="sxs-lookup"><span data-stu-id="645c4-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="645c4-224">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="645c4-224">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="645c4-225">Log into your Recognize company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="645c4-225">Log into your Recognize company site as an administrator.</span></span>

1. <span data-ttu-id="645c4-226">On the upper right corner, click **Menu**.</span><span class="sxs-lookup"><span data-stu-id="645c4-226">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="645c4-227">Go to **Company Admin**.</span><span class="sxs-lookup"><span data-stu-id="645c4-227">Go to **Company Admin**.</span></span>

1. <span data-ttu-id="645c4-228">On the left navigation pane, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="645c4-228">On the left navigation pane, click **Settings**.</span></span>

1. <span data-ttu-id="645c4-229">Perform the following steps on **User Sync** section.</span><span class="sxs-lookup"><span data-stu-id="645c4-229">Perform the following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="645c4-230">![New User](./media/recognize-tutorial/tutorial_recognize_005.png "New User")</span><span class="sxs-lookup"><span data-stu-id="645c4-230">![New User](./media/recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="645c4-231">a.</span><span class="sxs-lookup"><span data-stu-id="645c4-231">a.</span></span> <span data-ttu-id="645c4-232">As **Sync Enabled**, select **ON**.</span><span class="sxs-lookup"><span data-stu-id="645c4-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="645c4-233">b.</span><span class="sxs-lookup"><span data-stu-id="645c4-233">b.</span></span> <span data-ttu-id="645c4-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span><span class="sxs-lookup"><span data-stu-id="645c4-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="645c4-235">c.</span><span class="sxs-lookup"><span data-stu-id="645c4-235">c.</span></span> <span data-ttu-id="645c4-236">Click **Run User Sync**.</span><span class="sxs-lookup"><span data-stu-id="645c4-236">Click **Run User Sync**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="645c4-237">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="645c4-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="645c4-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Recognize.</span><span class="sxs-lookup"><span data-stu-id="645c4-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Recognize.</span></span>

![Assign User][200] 

<span data-ttu-id="645c4-240">**To assign Britta Simon to Recognize, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="645c4-240">**To assign Britta Simon to Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="645c4-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="645c4-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="645c4-243">In the applications list, select **Recognize**.</span><span class="sxs-lookup"><span data-stu-id="645c4-243">In the applications list, select **Recognize**.</span></span>

    ![Configure Single Sign-On](./media/recognize-tutorial/tutorial_recognize_app.png) 

1. <span data-ttu-id="645c4-245">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="645c4-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="645c4-247">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="645c4-247">Click **Add** button.</span></span> <span data-ttu-id="645c4-248">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="645c4-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="645c4-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="645c4-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="645c4-251">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="645c4-251">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="645c4-252">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="645c4-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="645c4-253">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="645c4-253">Testing single sign-on</span></span>

<span data-ttu-id="645c4-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="645c4-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="645c4-255">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span><span class="sxs-lookup"><span data-stu-id="645c4-255">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span></span> <span data-ttu-id="645c4-256">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="645c4-256">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="645c4-257">Additional resources</span><span class="sxs-lookup"><span data-stu-id="645c4-257">Additional resources</span></span>

* [<span data-ttu-id="645c4-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="645c4-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="645c4-259">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="645c4-259">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/recognize-tutorial/tutorial_general_01.png
[2]: ./media/recognize-tutorial/tutorial_general_02.png
[3]: ./media/recognize-tutorial/tutorial_general_03.png
[4]: ./media/recognize-tutorial/tutorial_general_04.png

[100]: ./media/recognize-tutorial/tutorial_general_100.png

[200]: ./media/recognize-tutorial/tutorial_general_200.png
[201]: ./media/recognize-tutorial/tutorial_general_201.png
[202]: ./media/recognize-tutorial/tutorial_general_202.png
[203]: ./media/recognize-tutorial/tutorial_general_203.png

