---
title: 'Tutorial: Azure Active Directory integration with Samanage | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Samanage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 118ab72c9afc13c5792f229f9c7bc61d226553d5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865185"
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="15de5-103">Tutorial: Azure Active Directory integration with Samanage</span><span class="sxs-lookup"><span data-stu-id="15de5-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="15de5-104">In this tutorial, you learn how to integrate Samanage with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15de5-104">In this tutorial, you learn how to integrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="15de5-105">Integrating Samanage with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="15de5-105">Integrating Samanage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="15de5-106">You can control in Azure AD who has access to Samanage</span><span class="sxs-lookup"><span data-stu-id="15de5-106">You can control in Azure AD who has access to Samanage</span></span>
- <span data-ttu-id="15de5-107">You can enable your users to automatically get signed-on to Samanage (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="15de5-107">You can enable your users to automatically get signed-on to Samanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="15de5-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="15de5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="15de5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="15de5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15de5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15de5-110">Prerequisites</span></span>

<span data-ttu-id="15de5-111">To configure Azure AD integration with Samanage, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="15de5-111">To configure Azure AD integration with Samanage, you need the following items:</span></span>

- <span data-ttu-id="15de5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="15de5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="15de5-113">A Samanage single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="15de5-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="15de5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="15de5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="15de5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="15de5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="15de5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="15de5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="15de5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15de5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="15de5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="15de5-118">Scenario description</span></span>
<span data-ttu-id="15de5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="15de5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="15de5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="15de5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="15de5-121">Adding Samanage from the gallery</span><span class="sxs-lookup"><span data-stu-id="15de5-121">Adding Samanage from the gallery</span></span>
1. <span data-ttu-id="15de5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="15de5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-the-gallery"></a><span data-ttu-id="15de5-123">Adding Samanage from the gallery</span><span class="sxs-lookup"><span data-stu-id="15de5-123">Adding Samanage from the gallery</span></span>
<span data-ttu-id="15de5-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="15de5-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="15de5-125">**To add Samanage from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15de5-125">**To add Samanage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="15de5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="15de5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="15de5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="15de5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="15de5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="15de5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="15de5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="15de5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="15de5-133">In the search box, type **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="15de5-133">In the search box, type **Samanage**.</span></span>

    ![Creating an Azure AD test user](./media/samanage-tutorial/tutorial_samanage_search.png)

1. <span data-ttu-id="15de5-135">In the results panel, select **Samanage**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="15de5-135">In the results panel, select **Samanage**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="15de5-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="15de5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="15de5-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="15de5-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="15de5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Samanage is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15de5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Samanage is to a user in Azure AD.</span></span> <span data-ttu-id="15de5-140">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span><span class="sxs-lookup"><span data-stu-id="15de5-140">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span></span>

<span data-ttu-id="15de5-141">In Samanage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="15de5-141">In Samanage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="15de5-142">To configure and test Azure AD single sign-on with Samanage, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="15de5-142">To configure and test Azure AD single sign-on with Samanage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="15de5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="15de5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="15de5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15de5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="15de5-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="15de5-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="15de5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="15de5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="15de5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="15de5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="15de5-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="15de5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="15de5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Samanage application.</span><span class="sxs-lookup"><span data-stu-id="15de5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="15de5-150">**To configure Azure AD single sign-on with Samanage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15de5-150">**To configure Azure AD single sign-on with Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="15de5-151">In the Azure portal, on the **Samanage** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="15de5-151">In the Azure portal, on the **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="15de5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="15de5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/samanage-tutorial/tutorial_samanage_samlbase.png)

1. <span data-ttu-id="15de5-155">On the **Samanage Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="15de5-155">On the **Samanage Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="15de5-157">a.</span><span class="sxs-lookup"><span data-stu-id="15de5-157">a.</span></span> <span data-ttu-id="15de5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="15de5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="15de5-159">b.</span><span class="sxs-lookup"><span data-stu-id="15de5-159">b.</span></span> <span data-ttu-id="15de5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="15de5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="15de5-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="15de5-161">These values are not real.</span></span> <span data-ttu-id="15de5-162">Update these values with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="15de5-162">Update these values with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> <span data-ttu-id="15de5-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="15de5-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
1. <span data-ttu-id="15de5-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="15de5-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/samanage-tutorial/tutorial_samanage_certificate.png) 

1. <span data-ttu-id="15de5-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="15de5-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/samanage-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="15de5-168">On the **Samanage Configuration** section, click **Configure Samanage** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="15de5-168">On the **Samanage Configuration** section, click **Configure Samanage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="15de5-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="15de5-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/samanage-tutorial/tutorial_samanage_configure.png) 

1. <span data-ttu-id="15de5-171">In a different web browser window, log into your Samanage company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="15de5-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

1. <span data-ttu-id="15de5-172">Click **Dashboard** and select **Setup** in left navigation pane.</span><span class="sxs-lookup"><span data-stu-id="15de5-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="15de5-173">![Dashboard](./media/samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="15de5-173">![Dashboard](./media/samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

1. <span data-ttu-id="15de5-174">Click **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="15de5-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="15de5-175">![Single Sign-On](./media/samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="15de5-175">![Single Sign-On](./media/samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

1. <span data-ttu-id="15de5-176">Navigate to **Login using SAML** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="15de5-176">Navigate to **Login using SAML** section, perform the following steps:</span></span>
   
    <span data-ttu-id="15de5-177">![Login using SAML](./media/samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span><span class="sxs-lookup"><span data-stu-id="15de5-177">![Login using SAML](./media/samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="15de5-178">a.</span><span class="sxs-lookup"><span data-stu-id="15de5-178">a.</span></span> <span data-ttu-id="15de5-179">Click **Enable Single Sign-On with SAML**.</span><span class="sxs-lookup"><span data-stu-id="15de5-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="15de5-180">b.</span><span class="sxs-lookup"><span data-stu-id="15de5-180">b.</span></span> <span data-ttu-id="15de5-181">In the **Identity Provider URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15de5-181">In the **Identity Provider URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="15de5-182">c.</span><span class="sxs-lookup"><span data-stu-id="15de5-182">c.</span></span> <span data-ttu-id="15de5-183">Confirm the **Login URL** matches the **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15de5-183">Confirm the **Login URL** matches the **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="15de5-184">d.</span><span class="sxs-lookup"><span data-stu-id="15de5-184">d.</span></span> <span data-ttu-id="15de5-185">In the **Logout URL** textbox, enter the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15de5-185">In the **Logout URL** textbox, enter the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="15de5-186">e.</span><span class="sxs-lookup"><span data-stu-id="15de5-186">e.</span></span> <span data-ttu-id="15de5-187">In the **SAML Issuer** textbox, type the app id URI set in your identity provider.</span><span class="sxs-lookup"><span data-stu-id="15de5-187">In the **SAML Issuer** textbox, type the app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="15de5-188">f.</span><span class="sxs-lookup"><span data-stu-id="15de5-188">f.</span></span> <span data-ttu-id="15de5-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span><span class="sxs-lookup"><span data-stu-id="15de5-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="15de5-190">g.</span><span class="sxs-lookup"><span data-stu-id="15de5-190">g.</span></span> <span data-ttu-id="15de5-191">Click **Create users if they do not exist in Samanage**.</span><span class="sxs-lookup"><span data-stu-id="15de5-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="15de5-192">h.</span><span class="sxs-lookup"><span data-stu-id="15de5-192">h.</span></span> <span data-ttu-id="15de5-193">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="15de5-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="15de5-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="15de5-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="15de5-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="15de5-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="15de5-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="15de5-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="15de5-197">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="15de5-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="15de5-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15de5-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="15de5-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15de5-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="15de5-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="15de5-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/samanage-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="15de5-203">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="15de5-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/samanage-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="15de5-205">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="15de5-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/samanage-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="15de5-207">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="15de5-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="15de5-209">a.</span><span class="sxs-lookup"><span data-stu-id="15de5-209">a.</span></span> <span data-ttu-id="15de5-210">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="15de5-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="15de5-211">b.</span><span class="sxs-lookup"><span data-stu-id="15de5-211">b.</span></span> <span data-ttu-id="15de5-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="15de5-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="15de5-213">c.</span><span class="sxs-lookup"><span data-stu-id="15de5-213">c.</span></span> <span data-ttu-id="15de5-214">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="15de5-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="15de5-215">d.</span><span class="sxs-lookup"><span data-stu-id="15de5-215">d.</span></span> <span data-ttu-id="15de5-216">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="15de5-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="15de5-217">Creating a Samanage test user</span><span class="sxs-lookup"><span data-stu-id="15de5-217">Creating a Samanage test user</span></span>

<span data-ttu-id="15de5-218">To enable Azure AD users to log in to Samanage, they must be provisioned into Samanage.</span><span class="sxs-lookup"><span data-stu-id="15de5-218">To enable Azure AD users to log in to Samanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="15de5-219">In the case of Samanage, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="15de5-219">In the case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="15de5-220">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15de5-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="15de5-221">Log into your Samanage company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="15de5-221">Log into your Samanage company site as an administrator.</span></span>

1. <span data-ttu-id="15de5-222">Click **Dashboard** and select **Setup** in left navigation pan.</span><span class="sxs-lookup"><span data-stu-id="15de5-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="15de5-223">![Setup](./media/samanage-tutorial/tutorial_samanage_001.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="15de5-223">![Setup](./media/samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

1. <span data-ttu-id="15de5-224">Click the **Users** tab</span><span class="sxs-lookup"><span data-stu-id="15de5-224">Click the **Users** tab</span></span>
   
    <span data-ttu-id="15de5-225">![Users](./media/samanage-tutorial/tutorial_samanage_006.png "Users")</span><span class="sxs-lookup"><span data-stu-id="15de5-225">![Users](./media/samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

1. <span data-ttu-id="15de5-226">Click **New User**.</span><span class="sxs-lookup"><span data-stu-id="15de5-226">Click **New User**.</span></span>
   
    <span data-ttu-id="15de5-227">![New User](./media/samanage-tutorial/tutorial_samanage_007.png "New User")</span><span class="sxs-lookup"><span data-stu-id="15de5-227">![New User](./media/samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

1. <span data-ttu-id="15de5-228">Type the **Name** and the **Email Address** of an Azure Active Directory account you want to provision and click **Create user**.</span><span class="sxs-lookup"><span data-stu-id="15de5-228">Type the **Name** and the **Email Address** of an Azure Active Directory account you want to provision and click **Create user**.</span></span>
   
    <span data-ttu-id="15de5-229">![Create User](./media/samanage-tutorial/tutorial_samanage_008.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="15de5-229">![Create User](./media/samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="15de5-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="15de5-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="15de5-231">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="15de5-231">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="15de5-232">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="15de5-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="15de5-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Samanage.</span><span class="sxs-lookup"><span data-stu-id="15de5-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Samanage.</span></span>

![Assign User][200] 

<span data-ttu-id="15de5-235">**To assign Britta Simon to Samanage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15de5-235">**To assign Britta Simon to Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="15de5-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="15de5-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="15de5-238">In the applications list, select **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="15de5-238">In the applications list, select **Samanage**.</span></span>

    ![Configure Single Sign-On](./media/samanage-tutorial/tutorial_samanage_app.png) 

1. <span data-ttu-id="15de5-240">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="15de5-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="15de5-242">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="15de5-242">Click **Add** button.</span></span> <span data-ttu-id="15de5-243">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="15de5-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="15de5-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="15de5-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="15de5-246">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="15de5-246">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="15de5-247">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="15de5-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="15de5-248">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="15de5-248">Testing single sign-on</span></span>

<span data-ttu-id="15de5-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="15de5-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="15de5-250">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span><span class="sxs-lookup"><span data-stu-id="15de5-250">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span></span>
<span data-ttu-id="15de5-251">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="15de5-251">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="15de5-252">Additional resources</span><span class="sxs-lookup"><span data-stu-id="15de5-252">Additional resources</span></span>

* [<span data-ttu-id="15de5-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15de5-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="15de5-254">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="15de5-254">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/samanage-tutorial/tutorial_general_01.png
[2]: ./media/samanage-tutorial/tutorial_general_02.png
[3]: ./media/samanage-tutorial/tutorial_general_03.png
[4]: ./media/samanage-tutorial/tutorial_general_04.png

[100]: ./media/samanage-tutorial/tutorial_general_100.png

[200]: ./media/samanage-tutorial/tutorial_general_200.png
[201]: ./media/samanage-tutorial/tutorial_general_201.png
[202]: ./media/samanage-tutorial/tutorial_general_202.png
[203]: ./media/samanage-tutorial/tutorial_general_203.png

