---
title: 'Tutorial: Azure Active Directory integration with Gigya | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Gigya.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 3759cfdb30620622912c5866e43f81699ac37eb7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855780"
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="7bffa-103">Tutorial: Azure Active Directory integration with Gigya</span><span class="sxs-lookup"><span data-stu-id="7bffa-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="7bffa-104">In this tutorial, you learn how to integrate Gigya with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7bffa-104">In this tutorial, you learn how to integrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7bffa-105">Integrating Gigya with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7bffa-105">Integrating Gigya with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7bffa-106">You can control in Azure AD who has access to Gigya</span><span class="sxs-lookup"><span data-stu-id="7bffa-106">You can control in Azure AD who has access to Gigya</span></span>
- <span data-ttu-id="7bffa-107">You can enable your users to automatically get signed-on to Gigya (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7bffa-107">You can enable your users to automatically get signed-on to Gigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7bffa-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7bffa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7bffa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7bffa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bffa-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7bffa-110">Prerequisites</span></span>

<span data-ttu-id="7bffa-111">To configure Azure AD integration with Gigya, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7bffa-111">To configure Azure AD integration with Gigya, you need the following items:</span></span>

- <span data-ttu-id="7bffa-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7bffa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7bffa-113">A Gigya single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7bffa-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7bffa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7bffa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7bffa-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7bffa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7bffa-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7bffa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7bffa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7bffa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7bffa-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7bffa-118">Scenario description</span></span>
<span data-ttu-id="7bffa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7bffa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7bffa-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7bffa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7bffa-121">Adding Gigya from the gallery</span><span class="sxs-lookup"><span data-stu-id="7bffa-121">Adding Gigya from the gallery</span></span>
1. <span data-ttu-id="7bffa-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7bffa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-the-gallery"></a><span data-ttu-id="7bffa-123">Adding Gigya from the gallery</span><span class="sxs-lookup"><span data-stu-id="7bffa-123">Adding Gigya from the gallery</span></span>
<span data-ttu-id="7bffa-124">To configure the integration of Gigya into Azure AD, you need to add Gigya from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7bffa-124">To configure the integration of Gigya into Azure AD, you need to add Gigya from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7bffa-125">**To add Gigya from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7bffa-125">**To add Gigya from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7bffa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7bffa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="7bffa-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7bffa-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="7bffa-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7bffa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="7bffa-133">In the search box, type **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-133">In the search box, type **Gigya**.</span></span>

    ![Creating an Azure AD test user](./media/gigya-tutorial/tutorial_gigya_search.png)

1. <span data-ttu-id="7bffa-135">In the results panel, select **Gigya**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7bffa-135">In the results panel, select **Gigya**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7bffa-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7bffa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7bffa-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7bffa-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7bffa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Gigya is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bffa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Gigya is to a user in Azure AD.</span></span> <span data-ttu-id="7bffa-140">In other words, a link relationship between an Azure AD user and the related user in Gigya needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7bffa-140">In other words, a link relationship between an Azure AD user and the related user in Gigya needs to be established.</span></span>

<span data-ttu-id="7bffa-141">In Gigya, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="7bffa-141">In Gigya, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7bffa-142">To configure and test Azure AD single sign-on with Gigya, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7bffa-142">To configure and test Azure AD single sign-on with Gigya, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7bffa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7bffa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7bffa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bffa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7bffa-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - to have a counterpart of Britta Simon in Gigya that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7bffa-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - to have a counterpart of Britta Simon in Gigya that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7bffa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7bffa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7bffa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7bffa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7bffa-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7bffa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7bffa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Gigya application.</span><span class="sxs-lookup"><span data-stu-id="7bffa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="7bffa-150">**To configure Azure AD single sign-on with Gigya, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7bffa-150">**To configure Azure AD single sign-on with Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="7bffa-151">In the Azure portal, on the **Gigya** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-151">In the Azure portal, on the **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="7bffa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7bffa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/gigya-tutorial/tutorial_gigya_samlbase.png)

1. <span data-ttu-id="7bffa-155">On the **Gigya Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bffa-155">On the **Gigya Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="7bffa-157">a.</span><span class="sxs-lookup"><span data-stu-id="7bffa-157">a.</span></span> <span data-ttu-id="7bffa-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="7bffa-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="7bffa-159">b.</span><span class="sxs-lookup"><span data-stu-id="7bffa-159">b.</span></span> <span data-ttu-id="7bffa-160">In the **Identifier** textbox, type a URL using the following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="7bffa-160">In the **Identifier** textbox, type a URL using the following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7bffa-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7bffa-161">These values are not real.</span></span> <span data-ttu-id="7bffa-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="7bffa-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7bffa-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7bffa-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) to get these values.</span></span> 
 
1. <span data-ttu-id="7bffa-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7bffa-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/gigya-tutorial/tutorial_gigya_certificate.png) 

1. <span data-ttu-id="7bffa-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7bffa-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/gigya-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="7bffa-168">On the **Gigya Configuration** section, click **Configure Gigya** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="7bffa-168">On the **Gigya Configuration** section, click **Configure Gigya** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7bffa-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="7bffa-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/gigya-tutorial/tutorial_gigya_configure.png) 

1. <span data-ttu-id="7bffa-171">In a different web browser window, log into your Gigya company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7bffa-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

1. <span data-ttu-id="7bffa-172">Go to **Settings \> SAML Login**, and then click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7bffa-172">Go to **Settings \> SAML Login**, and then click the **Add** button.</span></span>
   
    <span data-ttu-id="7bffa-173">![SAML Login](./media/gigya-tutorial/ic789532.png "SAML Login")</span><span class="sxs-lookup"><span data-stu-id="7bffa-173">![SAML Login](./media/gigya-tutorial/ic789532.png "SAML Login")</span></span>

1. <span data-ttu-id="7bffa-174">In the **SAML Login** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bffa-174">In the **SAML Login** section, perform the following steps:</span></span>
   
    <span data-ttu-id="7bffa-175">![SAML Configuration](./media/gigya-tutorial/ic789533.png "SAML Configuration")</span><span class="sxs-lookup"><span data-stu-id="7bffa-175">![SAML Configuration](./media/gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="7bffa-176">a.</span><span class="sxs-lookup"><span data-stu-id="7bffa-176">a.</span></span> <span data-ttu-id="7bffa-177">In the **Name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="7bffa-177">In the **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="7bffa-178">b.</span><span class="sxs-lookup"><span data-stu-id="7bffa-178">b.</span></span> <span data-ttu-id="7bffa-179">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7bffa-179">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="7bffa-180">c.</span><span class="sxs-lookup"><span data-stu-id="7bffa-180">c.</span></span> <span data-ttu-id="7bffa-181">In **Single Sign-On Service URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7bffa-181">In **Single Sign-On Service URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="7bffa-182">d.</span><span class="sxs-lookup"><span data-stu-id="7bffa-182">d.</span></span> <span data-ttu-id="7bffa-183">In **Name ID Format** textbox, paste the value of **Name Identifier Format** which you have copied from Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7bffa-183">In **Name ID Format** textbox, paste the value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="7bffa-184">e.</span><span class="sxs-lookup"><span data-stu-id="7bffa-184">e.</span></span> <span data-ttu-id="7bffa-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="7bffa-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="7bffa-186">f.</span><span class="sxs-lookup"><span data-stu-id="7bffa-186">f.</span></span> <span data-ttu-id="7bffa-187">Click **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="7bffa-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="7bffa-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7bffa-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="7bffa-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7bffa-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7bffa-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7bffa-191">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7bffa-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="7bffa-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bffa-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="7bffa-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7bffa-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7bffa-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7bffa-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/gigya-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="7bffa-197">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/gigya-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="7bffa-199">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="7bffa-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/gigya-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="7bffa-201">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bffa-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7bffa-203">a.</span><span class="sxs-lookup"><span data-stu-id="7bffa-203">a.</span></span> <span data-ttu-id="7bffa-204">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7bffa-205">b.</span><span class="sxs-lookup"><span data-stu-id="7bffa-205">b.</span></span> <span data-ttu-id="7bffa-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7bffa-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7bffa-207">c.</span><span class="sxs-lookup"><span data-stu-id="7bffa-207">c.</span></span> <span data-ttu-id="7bffa-208">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7bffa-209">d.</span><span class="sxs-lookup"><span data-stu-id="7bffa-209">d.</span></span> <span data-ttu-id="7bffa-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="7bffa-211">Creating a Gigya test user</span><span class="sxs-lookup"><span data-stu-id="7bffa-211">Creating a Gigya test user</span></span>

<span data-ttu-id="7bffa-212">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span><span class="sxs-lookup"><span data-stu-id="7bffa-212">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="7bffa-213">In the case of Gigya, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="7bffa-213">In the case of Gigya, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="7bffa-214">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bffa-214">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="7bffa-215">Log in to your **Gigya** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7bffa-215">Log in to your **Gigya** company site as an administrator.</span></span>

1. <span data-ttu-id="7bffa-216">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-216">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="7bffa-217">![Manage Users](./media/gigya-tutorial/ic789535.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="7bffa-217">![Manage Users](./media/gigya-tutorial/ic789535.png "Manage Users")</span></span>

1. <span data-ttu-id="7bffa-218">On the Invite Users dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bffa-218">On the Invite Users dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="7bffa-219">![Invite Users](./media/gigya-tutorial/ic789536.png "Invite Users")</span><span class="sxs-lookup"><span data-stu-id="7bffa-219">![Invite Users](./media/gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="7bffa-220">a.</span><span class="sxs-lookup"><span data-stu-id="7bffa-220">a.</span></span> <span data-ttu-id="7bffa-221">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="7bffa-221">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span></span>
    
    <span data-ttu-id="7bffa-222">b.</span><span class="sxs-lookup"><span data-stu-id="7bffa-222">b.</span></span> <span data-ttu-id="7bffa-223">Click **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="7bffa-224">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="7bffa-224">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span>
    > 
    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7bffa-225">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7bffa-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7bffa-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Gigya.</span><span class="sxs-lookup"><span data-stu-id="7bffa-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Gigya.</span></span>

![Assign User][200] 

<span data-ttu-id="7bffa-228">**To assign Britta Simon to Gigya, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7bffa-228">**To assign Britta Simon to Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="7bffa-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7bffa-231">In the applications list, select **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-231">In the applications list, select **Gigya**.</span></span>

    ![Configure Single Sign-On](./media/gigya-tutorial/tutorial_gigya_app.png) 

1. <span data-ttu-id="7bffa-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7bffa-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="7bffa-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7bffa-235">Click **Add** button.</span></span> <span data-ttu-id="7bffa-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7bffa-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="7bffa-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7bffa-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7bffa-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7bffa-239">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7bffa-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7bffa-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7bffa-241">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="7bffa-241">Testing single sign-on</span></span>

<span data-ttu-id="7bffa-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7bffa-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7bffa-243">When you click the Gigya tile in the Access Panel, you should get automatically signed-on to your Gigya application.</span><span class="sxs-lookup"><span data-stu-id="7bffa-243">When you click the Gigya tile in the Access Panel, you should get automatically signed-on to your Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7bffa-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7bffa-244">Additional resources</span></span>

* [<span data-ttu-id="7bffa-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bffa-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7bffa-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7bffa-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/gigya-tutorial/tutorial_general_01.png
[2]: ./media/gigya-tutorial/tutorial_general_02.png
[3]: ./media/gigya-tutorial/tutorial_general_03.png
[4]: ./media/gigya-tutorial/tutorial_general_04.png

[100]: ./media/gigya-tutorial/tutorial_general_100.png

[200]: ./media/gigya-tutorial/tutorial_general_200.png
[201]: ./media/gigya-tutorial/tutorial_general_201.png
[202]: ./media/gigya-tutorial/tutorial_general_202.png
[203]: ./media/gigya-tutorial/tutorial_general_203.png

