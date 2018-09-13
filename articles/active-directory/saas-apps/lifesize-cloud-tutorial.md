---
title: 'Tutorial: Azure Active Directory integration with Lifesize Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Lifesize Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c03456dcda2b3ee44686b070cdebb5fc81c3968c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866641"
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="bf292-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="bf292-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="bf292-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf292-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf292-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="bf292-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bf292-106">You can control in Azure AD who has access to Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="bf292-106">You can control in Azure AD who has access to Lifesize Cloud</span></span>
- <span data-ttu-id="bf292-107">You can enable your users to automatically get signed-on to Lifesize Cloud (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="bf292-107">You can enable your users to automatically get signed-on to Lifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf292-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bf292-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bf292-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="bf292-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf292-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bf292-110">Prerequisites</span></span>

<span data-ttu-id="bf292-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="bf292-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span></span>

- <span data-ttu-id="bf292-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="bf292-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf292-113">A Lifesize Cloud single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="bf292-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf292-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="bf292-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf292-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="bf292-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf292-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="bf292-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf292-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf292-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf292-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="bf292-118">Scenario description</span></span>
<span data-ttu-id="bf292-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="bf292-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf292-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="bf292-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf292-121">Adding Lifesize Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="bf292-121">Adding Lifesize Cloud from the gallery</span></span>
1. <span data-ttu-id="bf292-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bf292-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-the-gallery"></a><span data-ttu-id="bf292-123">Adding Lifesize Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="bf292-123">Adding Lifesize Cloud from the gallery</span></span>
<span data-ttu-id="bf292-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="bf292-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bf292-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bf292-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bf292-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bf292-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="bf292-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="bf292-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bf292-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bf292-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="bf292-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="bf292-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="bf292-133">In the search box, type **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="bf292-133">In the search box, type **Lifesize Cloud**.</span></span>

    ![Creating an Azure AD test user](./media/lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

1. <span data-ttu-id="bf292-135">In the results panel, select **Lifesize Cloud**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="bf292-135">In the results panel, select **Lifesize Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf292-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bf292-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf292-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bf292-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bf292-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf292-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="bf292-140">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="bf292-140">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span></span>

<span data-ttu-id="bf292-141">In Lifesize Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="bf292-141">In Lifesize Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bf292-142">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="bf292-142">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bf292-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="bf292-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="bf292-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf292-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="bf292-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="bf292-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="bf292-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bf292-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="bf292-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="bf292-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf292-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bf292-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf292-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lifesize Cloud application.</span><span class="sxs-lookup"><span data-stu-id="bf292-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="bf292-150">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bf292-150">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="bf292-151">In the Azure portal, on the **Lifesize Cloud** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bf292-151">In the Azure portal, on the **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="bf292-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bf292-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

1. <span data-ttu-id="bf292-155">On the **Lifesize Cloud Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bf292-155">On the **Lifesize Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="bf292-157">a.</span><span class="sxs-lookup"><span data-stu-id="bf292-157">a.</span></span> <span data-ttu-id="bf292-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="bf292-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="bf292-159">b.</span><span class="sxs-lookup"><span data-stu-id="bf292-159">b.</span></span> <span data-ttu-id="bf292-160">In the **Identifier** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="bf292-160">In the **Identifier** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
1. <span data-ttu-id="bf292-161">Check **Show advanced URL settings**, perform the following step:</span><span class="sxs-lookup"><span data-stu-id="bf292-161">Check **Show advanced URL settings**, perform the following step:</span></span>    
   
    ![Configure Single Sign-On](./media/lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="bf292-163">In the **Relay state** textbox, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="bf292-163">In the **Relay state** textbox, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="bf292-164">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="bf292-164">Please note that these are not the real values.</span></span> <span data-ttu-id="bf292-165">you have to update these values with the actual Sign-On URL, Relay State, and Identifier.</span><span class="sxs-lookup"><span data-stu-id="bf292-165">you have to update these values with the actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="bf292-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) to get Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="bf292-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) to get Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in the tutorial.</span></span>

1. <span data-ttu-id="bf292-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="bf292-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

1. <span data-ttu-id="bf292-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="bf292-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/lifesize-cloud-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="bf292-171">On the **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="bf292-171">On the **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bf292-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="bf292-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

1. <span data-ttu-id="bf292-174">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span><span class="sxs-lookup"><span data-stu-id="bf292-174">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span></span>

1. <span data-ttu-id="bf292-175">In the top right corner click on your name and then click on the **Advance Settings**.</span><span class="sxs-lookup"><span data-stu-id="bf292-175">In the top right corner click on your name and then click on the **Advance Settings**.</span></span>
   
    ![Configure Single Sign-On](./media/lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

1. <span data-ttu-id="bf292-177">In the Advance Settings now click on the **SSO Configuration** link.</span><span class="sxs-lookup"><span data-stu-id="bf292-177">In the Advance Settings now click on the **SSO Configuration** link.</span></span> <span data-ttu-id="bf292-178">It will open the SSO Configuration page for your instance.</span><span class="sxs-lookup"><span data-stu-id="bf292-178">It will open the SSO Configuration page for your instance.</span></span>
   
    ![Configure Single Sign-On](./media/lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

1. <span data-ttu-id="bf292-180">Now configure the following values in the SSO configuration UI.</span><span class="sxs-lookup"><span data-stu-id="bf292-180">Now configure the following values in the SSO configuration UI.</span></span>    
   
    ![Configure Single Sign-On](./media/lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="bf292-182">a.</span><span class="sxs-lookup"><span data-stu-id="bf292-182">a.</span></span> <span data-ttu-id="bf292-183">In **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bf292-183">In **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bf292-184">b.</span><span class="sxs-lookup"><span data-stu-id="bf292-184">b.</span></span>  <span data-ttu-id="bf292-185">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bf292-185">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bf292-186">c.</span><span class="sxs-lookup"><span data-stu-id="bf292-186">c.</span></span> <span data-ttu-id="bf292-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="bf292-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="bf292-188">d.</span><span class="sxs-lookup"><span data-stu-id="bf292-188">d.</span></span> <span data-ttu-id="bf292-189">In the SAML Attribute mappings for the First Name text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="bf292-189">In the SAML Attribute mappings for the First Name text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="bf292-190">e.</span><span class="sxs-lookup"><span data-stu-id="bf292-190">e.</span></span> <span data-ttu-id="bf292-191">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="bf292-191">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="bf292-192">f.</span><span class="sxs-lookup"><span data-stu-id="bf292-192">f.</span></span> <span data-ttu-id="bf292-193">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="bf292-193">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

1. <span data-ttu-id="bf292-194">To check the configuration you can click on the **Test** button.</span><span class="sxs-lookup"><span data-stu-id="bf292-194">To check the configuration you can click on the **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="bf292-195">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span><span class="sxs-lookup"><span data-stu-id="bf292-195">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span></span>

1. <span data-ttu-id="bf292-196">Enable the SSO by checking on the **Enable SSO** button.</span><span class="sxs-lookup"><span data-stu-id="bf292-196">Enable the SSO by checking on the **Enable SSO** button.</span></span>

1. <span data-ttu-id="bf292-197">Now click on the **Update** button so that all the settings are saved.</span><span class="sxs-lookup"><span data-stu-id="bf292-197">Now click on the **Update** button so that all the settings are saved.</span></span> <span data-ttu-id="bf292-198">This will generate the RelayState value.</span><span class="sxs-lookup"><span data-stu-id="bf292-198">This will generate the RelayState value.</span></span> <span data-ttu-id="bf292-199">Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="bf292-199">Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="bf292-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="bf292-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bf292-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="bf292-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bf292-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf292-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf292-203">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bf292-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="bf292-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf292-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="bf292-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bf292-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bf292-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bf292-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/lifesize-cloud-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="bf292-209">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="bf292-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/lifesize-cloud-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="bf292-211">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="bf292-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/lifesize-cloud-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="bf292-213">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bf292-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf292-215">a.</span><span class="sxs-lookup"><span data-stu-id="bf292-215">a.</span></span> <span data-ttu-id="bf292-216">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf292-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf292-217">b.</span><span class="sxs-lookup"><span data-stu-id="bf292-217">b.</span></span> <span data-ttu-id="bf292-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf292-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf292-219">c.</span><span class="sxs-lookup"><span data-stu-id="bf292-219">c.</span></span> <span data-ttu-id="bf292-220">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="bf292-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bf292-221">d.</span><span class="sxs-lookup"><span data-stu-id="bf292-221">d.</span></span> <span data-ttu-id="bf292-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bf292-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="bf292-223">Creating a Lifesize Cloud test user</span><span class="sxs-lookup"><span data-stu-id="bf292-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="bf292-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="bf292-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="bf292-225">Lifesize cloud does support automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="bf292-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="bf292-226">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span><span class="sxs-lookup"><span data-stu-id="bf292-226">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bf292-227">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bf292-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bf292-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="bf292-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lifesize Cloud.</span></span>

![Assign User][200] 

<span data-ttu-id="bf292-230">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bf292-230">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="bf292-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bf292-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="bf292-233">In the applications list, select **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="bf292-233">In the applications list, select **Lifesize Cloud**.</span></span>

    ![Configure Single Sign-On](./media/lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

1. <span data-ttu-id="bf292-235">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="bf292-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="bf292-237">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="bf292-237">Click **Add** button.</span></span> <span data-ttu-id="bf292-238">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bf292-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="bf292-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="bf292-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="bf292-241">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="bf292-241">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="bf292-242">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bf292-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf292-243">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="bf292-243">Testing single sign-on</span></span>

<span data-ttu-id="bf292-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bf292-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bf292-245">When you click the Lifesize Cloud tile in the Access Panel, you should get login page of Lifesize Cloud application.</span><span class="sxs-lookup"><span data-stu-id="bf292-245">When you click the Lifesize Cloud tile in the Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="bf292-246">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bf292-246">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf292-247">Additional resources</span><span class="sxs-lookup"><span data-stu-id="bf292-247">Additional resources</span></span>

* [<span data-ttu-id="bf292-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf292-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="bf292-249">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf292-249">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/lifesize-cloud-tutorial/tutorial_general_203.png

