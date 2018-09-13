---
title: 'Tutorial: Azure Active Directory integration with Igloo Software | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Igloo Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: d49a08c6f57f5248f17539cd9d0467d132f7a63d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869398"
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="2441c-103">Tutorial: Azure Active Directory integration with Igloo Software</span><span class="sxs-lookup"><span data-stu-id="2441c-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="2441c-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2441c-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2441c-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2441c-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2441c-106">You can control in Azure AD who has access to Igloo Software</span><span class="sxs-lookup"><span data-stu-id="2441c-106">You can control in Azure AD who has access to Igloo Software</span></span>
- <span data-ttu-id="2441c-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="2441c-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2441c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2441c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2441c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2441c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2441c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2441c-110">Prerequisites</span></span>

<span data-ttu-id="2441c-111">To configure Azure AD integration with Igloo Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2441c-111">To configure Azure AD integration with Igloo Software, you need the following items:</span></span>

- <span data-ttu-id="2441c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2441c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2441c-113">An Igloo Software single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2441c-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2441c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2441c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2441c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2441c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2441c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="2441c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2441c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2441c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2441c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2441c-118">Scenario description</span></span>
<span data-ttu-id="2441c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2441c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2441c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2441c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2441c-121">Adding Igloo Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="2441c-121">Adding Igloo Software from the gallery</span></span>
1. <span data-ttu-id="2441c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2441c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-the-gallery"></a><span data-ttu-id="2441c-123">Adding Igloo Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="2441c-123">Adding Igloo Software from the gallery</span></span>
<span data-ttu-id="2441c-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2441c-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2441c-125">**To add Igloo Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2441c-125">**To add Igloo Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2441c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2441c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="2441c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2441c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2441c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2441c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="2441c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="2441c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="2441c-133">In the search box, type **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="2441c-133">In the search box, type **Igloo Software**.</span></span>

    ![Creating an Azure AD test user](./media/igloo-software-tutorial/tutorial_igloosoftware_search.png)

1. <span data-ttu-id="2441c-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2441c-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2441c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2441c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2441c-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2441c-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2441c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2441c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span></span> <span data-ttu-id="2441c-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2441c-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span></span>

<span data-ttu-id="2441c-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="2441c-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2441c-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2441c-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2441c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2441c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="2441c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2441c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="2441c-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="2441c-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="2441c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2441c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="2441c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2441c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2441c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2441c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2441c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span><span class="sxs-lookup"><span data-stu-id="2441c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="2441c-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2441c-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="2441c-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2441c-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="2441c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2441c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

1. <span data-ttu-id="2441c-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2441c-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="2441c-157">a.</span><span class="sxs-lookup"><span data-stu-id="2441c-157">a.</span></span> <span data-ttu-id="2441c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="2441c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="2441c-159">b.</span><span class="sxs-lookup"><span data-stu-id="2441c-159">b.</span></span> <span data-ttu-id="2441c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="2441c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="2441c-161">c.</span><span class="sxs-lookup"><span data-stu-id="2441c-161">c.</span></span> <span data-ttu-id="2441c-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="2441c-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2441c-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="2441c-163">These values are not real.</span></span> <span data-ttu-id="2441c-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="2441c-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2441c-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="2441c-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span></span> 

1. <span data-ttu-id="2441c-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2441c-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

1. <span data-ttu-id="2441c-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2441c-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/igloo-software-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="2441c-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="2441c-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2441c-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="2441c-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

1. <span data-ttu-id="2441c-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2441c-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span></span>

1. <span data-ttu-id="2441c-174">Go to the **Control Panel**.</span><span class="sxs-lookup"><span data-stu-id="2441c-174">Go to the **Control Panel**.</span></span>
   
     <span data-ttu-id="2441c-175">![Control Panel](./media/igloo-software-tutorial/ic799949.png "Control Panel")</span><span class="sxs-lookup"><span data-stu-id="2441c-175">![Control Panel](./media/igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

1. <span data-ttu-id="2441c-176">In the **Membership** tab, click **Sign In Settings**.</span><span class="sxs-lookup"><span data-stu-id="2441c-176">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="2441c-177">![Sign in Settings](./media/igloo-software-tutorial/ic783968.png "Sign in Settings")</span><span class="sxs-lookup"><span data-stu-id="2441c-177">![Sign in Settings](./media/igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

1. <span data-ttu-id="2441c-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="2441c-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="2441c-179">![SAML Configuration](./media/igloo-software-tutorial/ic783969.png "SAML Configuration")</span><span class="sxs-lookup"><span data-stu-id="2441c-179">![SAML Configuration](./media/igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
1. <span data-ttu-id="2441c-180">In the **General Configuration** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2441c-180">In the **General Configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="2441c-181">![General Configuration](./media/igloo-software-tutorial/ic783970.png "General Configuration")</span><span class="sxs-lookup"><span data-stu-id="2441c-181">![General Configuration](./media/igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="2441c-182">a.</span><span class="sxs-lookup"><span data-stu-id="2441c-182">a.</span></span> <span data-ttu-id="2441c-183">In the **Connection Name** textbox, type a custom name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="2441c-183">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="2441c-184">b.</span><span class="sxs-lookup"><span data-stu-id="2441c-184">b.</span></span> <span data-ttu-id="2441c-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2441c-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="2441c-186">c.</span><span class="sxs-lookup"><span data-stu-id="2441c-186">c.</span></span> <span data-ttu-id="2441c-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2441c-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="2441c-188">d.</span><span class="sxs-lookup"><span data-stu-id="2441c-188">d.</span></span> <span data-ttu-id="2441c-189">Select **Logout Response and Request HTTP Type** as **POST**.</span><span class="sxs-lookup"><span data-stu-id="2441c-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="2441c-190">e.</span><span class="sxs-lookup"><span data-stu-id="2441c-190">e.</span></span> <span data-ttu-id="2441c-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="2441c-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>
    
1. <span data-ttu-id="2441c-192">In the **Response and Authentication Configuration**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2441c-192">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="2441c-193">![Response and Authentication Configuration](./media/igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span><span class="sxs-lookup"><span data-stu-id="2441c-193">![Response and Authentication Configuration](./media/igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="2441c-194">a.</span><span class="sxs-lookup"><span data-stu-id="2441c-194">a.</span></span> <span data-ttu-id="2441c-195">As **Identity Provider**, select **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="2441c-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="2441c-196">b.</span><span class="sxs-lookup"><span data-stu-id="2441c-196">b.</span></span> <span data-ttu-id="2441c-197">As **Identifier Type**, select **Email Address**.</span><span class="sxs-lookup"><span data-stu-id="2441c-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="2441c-198">c.</span><span class="sxs-lookup"><span data-stu-id="2441c-198">c.</span></span> <span data-ttu-id="2441c-199">In the **Email Attribute** textbox, type **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="2441c-199">In the **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="2441c-200">d.</span><span class="sxs-lookup"><span data-stu-id="2441c-200">d.</span></span> <span data-ttu-id="2441c-201">In the **First Name Attribute** textbox, type **givenname**.</span><span class="sxs-lookup"><span data-stu-id="2441c-201">In the **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="2441c-202">e.</span><span class="sxs-lookup"><span data-stu-id="2441c-202">e.</span></span> <span data-ttu-id="2441c-203">In the **Last Name Attribute** textbox, type **surname**.</span><span class="sxs-lookup"><span data-stu-id="2441c-203">In the **Last Name Attribute** textbox, type **surname**.</span></span>

1. <span data-ttu-id="2441c-204">Perform the following steps to complete the configuration:</span><span class="sxs-lookup"><span data-stu-id="2441c-204">Perform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="2441c-205">![User creation on Sign in](./media/igloo-software-tutorial/IC783972.png "User creation on Sign in")</span><span class="sxs-lookup"><span data-stu-id="2441c-205">![User creation on Sign in](./media/igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="2441c-206">a.</span><span class="sxs-lookup"><span data-stu-id="2441c-206">a.</span></span> <span data-ttu-id="2441c-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span><span class="sxs-lookup"><span data-stu-id="2441c-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="2441c-208">b.</span><span class="sxs-lookup"><span data-stu-id="2441c-208">b.</span></span> <span data-ttu-id="2441c-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span><span class="sxs-lookup"><span data-stu-id="2441c-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="2441c-210">c.</span><span class="sxs-lookup"><span data-stu-id="2441c-210">c.</span></span> <span data-ttu-id="2441c-211">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2441c-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2441c-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="2441c-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2441c-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="2441c-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2441c-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2441c-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2441c-215">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2441c-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="2441c-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2441c-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="2441c-218">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2441c-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2441c-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2441c-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/igloo-software-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="2441c-221">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="2441c-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/igloo-software-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="2441c-223">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="2441c-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/igloo-software-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="2441c-225">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2441c-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2441c-227">a.</span><span class="sxs-lookup"><span data-stu-id="2441c-227">a.</span></span> <span data-ttu-id="2441c-228">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2441c-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2441c-229">b.</span><span class="sxs-lookup"><span data-stu-id="2441c-229">b.</span></span> <span data-ttu-id="2441c-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2441c-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2441c-231">c.</span><span class="sxs-lookup"><span data-stu-id="2441c-231">c.</span></span> <span data-ttu-id="2441c-232">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="2441c-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2441c-233">d.</span><span class="sxs-lookup"><span data-stu-id="2441c-233">d.</span></span> <span data-ttu-id="2441c-234">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2441c-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="2441c-235">Creating an Igloo Software test user</span><span class="sxs-lookup"><span data-stu-id="2441c-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="2441c-236">There is no action item for you to configure user provisioning to Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="2441c-236">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="2441c-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="2441c-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="2441c-238">If there is no user account available yet, it is automatically created by Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="2441c-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2441c-239">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2441c-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2441c-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="2441c-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span></span>

![Assign User][200] 

<span data-ttu-id="2441c-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2441c-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="2441c-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2441c-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="2441c-245">In the applications list, select **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="2441c-245">In the applications list, select **Igloo Software**.</span></span>

    ![Configure Single Sign-On](./media/igloo-software-tutorial/tutorial_igloosoftware_app.png) 

1. <span data-ttu-id="2441c-247">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2441c-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="2441c-249">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2441c-249">Click **Add** button.</span></span> <span data-ttu-id="2441c-250">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2441c-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="2441c-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2441c-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="2441c-253">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2441c-253">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="2441c-254">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2441c-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2441c-255">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="2441c-255">Testing single sign-on</span></span>

<span data-ttu-id="2441c-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2441c-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2441c-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span><span class="sxs-lookup"><span data-stu-id="2441c-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span></span>
<span data-ttu-id="2441c-258">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2441c-258">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2441c-259">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2441c-259">Additional resources</span></span>

* [<span data-ttu-id="2441c-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2441c-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="2441c-261">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2441c-261">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/igloo-software-tutorial/tutorial_general_203.png

