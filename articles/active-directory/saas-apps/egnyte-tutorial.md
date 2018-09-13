---
title: 'Tutorial: Azure Active Directory integration with Egnyte | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Egnyte.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 4f6f6ef12f5a8dd8a9f210e9b1f1ca978ec5a1ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868939"
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="54ac6-103">Tutorial: Azure Active Directory integration with Egnyte</span><span class="sxs-lookup"><span data-stu-id="54ac6-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="54ac6-104">In this tutorial, you learn how to integrate Egnyte with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54ac6-104">In this tutorial, you learn how to integrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54ac6-105">Integrating Egnyte with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="54ac6-105">Integrating Egnyte with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54ac6-106">You can control in Azure AD who has access to Egnyte</span><span class="sxs-lookup"><span data-stu-id="54ac6-106">You can control in Azure AD who has access to Egnyte</span></span>
- <span data-ttu-id="54ac6-107">You can enable your users to automatically get signed-on to Egnyte (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="54ac6-107">You can enable your users to automatically get signed-on to Egnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="54ac6-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="54ac6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="54ac6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="54ac6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54ac6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="54ac6-110">Prerequisites</span></span>

<span data-ttu-id="54ac6-111">To configure Azure AD integration with Egnyte, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="54ac6-111">To configure Azure AD integration with Egnyte, you need the following items:</span></span>

- <span data-ttu-id="54ac6-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="54ac6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54ac6-113">An Egnyte single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="54ac6-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54ac6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="54ac6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54ac6-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="54ac6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54ac6-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="54ac6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54ac6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54ac6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54ac6-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="54ac6-118">Scenario description</span></span>
<span data-ttu-id="54ac6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="54ac6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54ac6-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="54ac6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54ac6-121">Adding Egnyte from the gallery</span><span class="sxs-lookup"><span data-stu-id="54ac6-121">Adding Egnyte from the gallery</span></span>
1. <span data-ttu-id="54ac6-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54ac6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-the-gallery"></a><span data-ttu-id="54ac6-123">Adding Egnyte from the gallery</span><span class="sxs-lookup"><span data-stu-id="54ac6-123">Adding Egnyte from the gallery</span></span>
<span data-ttu-id="54ac6-124">To configure the integration of Egnyte into Azure AD, you need to add Egnyte from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="54ac6-124">To configure the integration of Egnyte into Azure AD, you need to add Egnyte from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54ac6-125">**To add Egnyte from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54ac6-125">**To add Egnyte from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54ac6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="54ac6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="54ac6-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54ac6-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="54ac6-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="54ac6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="54ac6-133">In the search box, type **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-133">In the search box, type **Egnyte**.</span></span>

    ![Creating an Azure AD test user](./media/egnyte-tutorial/tutorial_egnyte_search.png)

1. <span data-ttu-id="54ac6-135">In the results panel, select **Egnyte**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="54ac6-135">In the results panel, select **Egnyte**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="54ac6-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54ac6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="54ac6-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="54ac6-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="54ac6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Egnyte is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54ac6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Egnyte is to a user in Azure AD.</span></span> <span data-ttu-id="54ac6-140">In other words, a link relationship between an Azure AD user and the related user in Egnyte needs to be established.</span><span class="sxs-lookup"><span data-stu-id="54ac6-140">In other words, a link relationship between an Azure AD user and the related user in Egnyte needs to be established.</span></span>

<span data-ttu-id="54ac6-141">In Egnyte, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="54ac6-141">In Egnyte, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54ac6-142">To configure and test Azure AD single sign-on with Egnyte, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="54ac6-142">To configure and test Azure AD single sign-on with Egnyte, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54ac6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="54ac6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="54ac6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54ac6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="54ac6-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - to have a counterpart of Britta Simon in Egnyte that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="54ac6-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - to have a counterpart of Britta Simon in Egnyte that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="54ac6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="54ac6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="54ac6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="54ac6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="54ac6-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54ac6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="54ac6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Egnyte application.</span><span class="sxs-lookup"><span data-stu-id="54ac6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="54ac6-150">**To configure Azure AD single sign-on with Egnyte, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54ac6-150">**To configure Azure AD single sign-on with Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="54ac6-151">In the Azure portal, on the **Egnyte** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-151">In the Azure portal, on the **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="54ac6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="54ac6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/egnyte-tutorial/tutorial_egnyte_samlbase.png)

1. <span data-ttu-id="54ac6-155">On the **Egnyte Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54ac6-155">On the **Egnyte Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="54ac6-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="54ac6-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54ac6-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="54ac6-158">This value is not real.</span></span> <span data-ttu-id="54ac6-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="54ac6-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="54ac6-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get this value.</span><span class="sxs-lookup"><span data-stu-id="54ac6-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get this value.</span></span> 
 
1. <span data-ttu-id="54ac6-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="54ac6-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/egnyte-tutorial/tutorial_egnyte_certificate.png) 

1. <span data-ttu-id="54ac6-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="54ac6-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/egnyte-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="54ac6-165">On the **Egnyte Configuration** section, click **Configure Egnyte** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="54ac6-165">On the **Egnyte Configuration** section, click **Configure Egnyte** to open **Configure sign-on** window.</span></span> <span data-ttu-id="54ac6-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="54ac6-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/egnyte-tutorial/tutorial_egnyte_configure.png) 

1. <span data-ttu-id="54ac6-168">In a different web browser window, log in to your Egnyte company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="54ac6-168">In a different web browser window, log in to your Egnyte company site as an administrator.</span></span>

1. <span data-ttu-id="54ac6-169">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="54ac6-170">![Settings](./media/egnyte-tutorial/ic787819.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="54ac6-170">![Settings](./media/egnyte-tutorial/ic787819.png "Settings")</span></span>

1. <span data-ttu-id="54ac6-171">In the menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-171">In the menu, click **Settings**.</span></span>

   <span data-ttu-id="54ac6-172">![Settings](./media/egnyte-tutorial/ic787820.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="54ac6-172">![Settings](./media/egnyte-tutorial/ic787820.png "Settings")</span></span>

1. <span data-ttu-id="54ac6-173">Click the **Configuration** tab, and then click **Security**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-173">Click the **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="54ac6-174">![Security](./media/egnyte-tutorial/ic787821.png "Security")</span><span class="sxs-lookup"><span data-stu-id="54ac6-174">![Security](./media/egnyte-tutorial/ic787821.png "Security")</span></span>

1. <span data-ttu-id="54ac6-175">In the **Single Sign-On Authentication** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54ac6-175">In the **Single Sign-On Authentication** section, perform the following steps:</span></span>

    <span data-ttu-id="54ac6-176">![Single Sign On Authentication](./media/egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span><span class="sxs-lookup"><span data-stu-id="54ac6-176">![Single Sign On Authentication](./media/egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="54ac6-177">a.</span><span class="sxs-lookup"><span data-stu-id="54ac6-177">a.</span></span> <span data-ttu-id="54ac6-178">As **Single sign-on authentication**, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="54ac6-179">b.</span><span class="sxs-lookup"><span data-stu-id="54ac6-179">b.</span></span> <span data-ttu-id="54ac6-180">As **Identity provider**, select **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="54ac6-181">c.</span><span class="sxs-lookup"><span data-stu-id="54ac6-181">c.</span></span> <span data-ttu-id="54ac6-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into the **Identity provider login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="54ac6-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into the **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="54ac6-183">d.</span><span class="sxs-lookup"><span data-stu-id="54ac6-183">d.</span></span> <span data-ttu-id="54ac6-184">Paste **SAML Entity ID** which you have copied from Azure portal into the **Identity provider entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="54ac6-184">Paste **SAML Entity ID** which you have copied from Azure portal into the **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="54ac6-185">e.</span><span class="sxs-lookup"><span data-stu-id="54ac6-185">e.</span></span> <span data-ttu-id="54ac6-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="54ac6-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="54ac6-187">f.</span><span class="sxs-lookup"><span data-stu-id="54ac6-187">f.</span></span> <span data-ttu-id="54ac6-188">As **Default user mapping**, select **Email address**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="54ac6-189">g.</span><span class="sxs-lookup"><span data-stu-id="54ac6-189">g.</span></span> <span data-ttu-id="54ac6-190">As **Use domain-specific issuer value**, select **disabled**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="54ac6-191">h.</span><span class="sxs-lookup"><span data-stu-id="54ac6-191">h.</span></span> <span data-ttu-id="54ac6-192">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="54ac6-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="54ac6-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54ac6-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="54ac6-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54ac6-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="54ac6-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="54ac6-196">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="54ac6-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="54ac6-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54ac6-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="54ac6-199">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54ac6-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54ac6-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="54ac6-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/egnyte-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="54ac6-202">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/egnyte-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="54ac6-204">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="54ac6-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/egnyte-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="54ac6-206">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54ac6-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="54ac6-208">a.</span><span class="sxs-lookup"><span data-stu-id="54ac6-208">a.</span></span> <span data-ttu-id="54ac6-209">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54ac6-210">b.</span><span class="sxs-lookup"><span data-stu-id="54ac6-210">b.</span></span> <span data-ttu-id="54ac6-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="54ac6-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="54ac6-212">c.</span><span class="sxs-lookup"><span data-stu-id="54ac6-212">c.</span></span> <span data-ttu-id="54ac6-213">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="54ac6-214">d.</span><span class="sxs-lookup"><span data-stu-id="54ac6-214">d.</span></span> <span data-ttu-id="54ac6-215">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="54ac6-216">Creating an Egnyte test user</span><span class="sxs-lookup"><span data-stu-id="54ac6-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="54ac6-217">To enable Azure AD users to log in to Egnyte, they must be provisioned into Egnyte.</span><span class="sxs-lookup"><span data-stu-id="54ac6-217">To enable Azure AD users to log in to Egnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="54ac6-218">In the case of Egnyte, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="54ac6-218">In the case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="54ac6-219">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54ac6-219">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="54ac6-220">Log in to your **Egnyte** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="54ac6-220">Log in to your **Egnyte** company site as administrator.</span></span>

1. <span data-ttu-id="54ac6-221">Go to **Settings \> Users & Groups**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-221">Go to **Settings \> Users & Groups**.</span></span>

1. <span data-ttu-id="54ac6-222">Click **Add New User**, and then select the type of user you want to add.</span><span class="sxs-lookup"><span data-stu-id="54ac6-222">Click **Add New User**, and then select the type of user you want to add.</span></span>
   
   <span data-ttu-id="54ac6-223">![Users](./media/egnyte-tutorial/ic787824.png "Users")</span><span class="sxs-lookup"><span data-stu-id="54ac6-223">![Users](./media/egnyte-tutorial/ic787824.png "Users")</span></span>

1. <span data-ttu-id="54ac6-224">In the **New Standard User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54ac6-224">In the **New Standard User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="54ac6-225">![New Standard User](./media/egnyte-tutorial/ic787825.png "New Standard User")</span><span class="sxs-lookup"><span data-stu-id="54ac6-225">![New Standard User](./media/egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="54ac6-226">a.</span><span class="sxs-lookup"><span data-stu-id="54ac6-226">a.</span></span> <span data-ttu-id="54ac6-227">Type the **Email**, **Username**, and other details of a valid Azure Active Directory account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="54ac6-227">Type the **Email**, **Username**, and other details of a valid Azure Active Directory account you want to provision.</span></span>
   
   <span data-ttu-id="54ac6-228">b.</span><span class="sxs-lookup"><span data-stu-id="54ac6-228">b.</span></span> <span data-ttu-id="54ac6-229">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="54ac6-230">The Azure Active Directory account holder will receive a notification email.</span><span class="sxs-lookup"><span data-stu-id="54ac6-230">The Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="54ac6-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="54ac6-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="54ac6-232">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="54ac6-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="54ac6-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Egnyte.</span><span class="sxs-lookup"><span data-stu-id="54ac6-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Egnyte.</span></span>

![Assign User][200] 

<span data-ttu-id="54ac6-235">**To assign Britta Simon to Egnyte, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54ac6-235">**To assign Britta Simon to Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="54ac6-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="54ac6-238">In the applications list, select **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-238">In the applications list, select **Egnyte**.</span></span>

    ![Configure Single Sign-On](./media/egnyte-tutorial/tutorial_egnyte_app.png) 

1. <span data-ttu-id="54ac6-240">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="54ac6-242">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="54ac6-242">Click **Add** button.</span></span> <span data-ttu-id="54ac6-243">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="54ac6-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="54ac6-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="54ac6-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="54ac6-246">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="54ac6-246">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="54ac6-247">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="54ac6-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="54ac6-248">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="54ac6-248">Testing single sign-on</span></span>

<span data-ttu-id="54ac6-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="54ac6-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="54ac6-250">When you click the Egnyte tile in the Access Panel, you should get automatically signed-on to your Egnyte application.</span><span class="sxs-lookup"><span data-stu-id="54ac6-250">When you click the Egnyte tile in the Access Panel, you should get automatically signed-on to your Egnyte application.</span></span>
<span data-ttu-id="54ac6-251">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54ac6-251">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="54ac6-252">Additional resources</span><span class="sxs-lookup"><span data-stu-id="54ac6-252">Additional resources</span></span>

* [<span data-ttu-id="54ac6-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54ac6-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="54ac6-254">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54ac6-254">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/egnyte-tutorial/tutorial_general_01.png
[2]: ./media/egnyte-tutorial/tutorial_general_02.png
[3]: ./media/egnyte-tutorial/tutorial_general_03.png
[4]: ./media/egnyte-tutorial/tutorial_general_04.png

[100]: ./media/egnyte-tutorial/tutorial_general_100.png

[200]: ./media/egnyte-tutorial/tutorial_general_200.png
[201]: ./media/egnyte-tutorial/tutorial_general_201.png
[202]: ./media/egnyte-tutorial/tutorial_general_202.png
[203]: ./media/egnyte-tutorial/tutorial_general_203.png

