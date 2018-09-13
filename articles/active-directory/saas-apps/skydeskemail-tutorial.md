---
title: 'Tutorial: Azure Active Directory integration with SkyDesk Email | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SkyDesk Email.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 058aad72ea8e5741bc632b3c27c032613683ae78
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865903"
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="fe096-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="fe096-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="fe096-104">In this tutorial, you learn how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe096-104">In this tutorial, you learn how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fe096-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fe096-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fe096-106">You can control in Azure AD who has access to SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="fe096-106">You can control in Azure AD who has access to SkyDesk Email</span></span>
- <span data-ttu-id="fe096-107">You can enable your users to automatically get signed-on to SkyDesk Email (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="fe096-107">You can enable your users to automatically get signed-on to SkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fe096-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="fe096-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fe096-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="fe096-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe096-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fe096-110">Prerequisites</span></span>

<span data-ttu-id="fe096-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fe096-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span></span>

- <span data-ttu-id="fe096-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fe096-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fe096-113">A SkyDesk Email single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="fe096-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fe096-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="fe096-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fe096-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="fe096-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fe096-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="fe096-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fe096-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe096-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fe096-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="fe096-118">Scenario description</span></span>
<span data-ttu-id="fe096-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="fe096-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fe096-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="fe096-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fe096-121">Adding SkyDesk Email from the gallery</span><span class="sxs-lookup"><span data-stu-id="fe096-121">Adding SkyDesk Email from the gallery</span></span>
1. <span data-ttu-id="fe096-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fe096-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-the-gallery"></a><span data-ttu-id="fe096-123">Adding SkyDesk Email from the gallery</span><span class="sxs-lookup"><span data-stu-id="fe096-123">Adding SkyDesk Email from the gallery</span></span>
<span data-ttu-id="fe096-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="fe096-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fe096-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fe096-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fe096-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="fe096-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="fe096-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="fe096-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fe096-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fe096-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="fe096-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="fe096-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="fe096-133">In the search box, type **SkyDesk Email**.</span><span class="sxs-lookup"><span data-stu-id="fe096-133">In the search box, type **SkyDesk Email**.</span></span>

    ![Creating an Azure AD test user](./media/skydeskemail-tutorial/tutorial_skydeskemail_search.png)

1. <span data-ttu-id="fe096-135">In the results panel, select **SkyDesk Email**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="fe096-135">In the results panel, select **SkyDesk Email**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fe096-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fe096-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fe096-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fe096-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fe096-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SkyDesk Email is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe096-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SkyDesk Email is to a user in Azure AD.</span></span> <span data-ttu-id="fe096-140">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span><span class="sxs-lookup"><span data-stu-id="fe096-140">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span></span>

<span data-ttu-id="fe096-141">In SkyDesk Email, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="fe096-141">In SkyDesk Email, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fe096-142">To configure and test Azure AD single sign-on with SkyDesk Email, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="fe096-142">To configure and test Azure AD single sign-on with SkyDesk Email, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fe096-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="fe096-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="fe096-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe096-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="fe096-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="fe096-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="fe096-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fe096-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="fe096-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="fe096-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fe096-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fe096-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fe096-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SkyDesk Email application.</span><span class="sxs-lookup"><span data-stu-id="fe096-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="fe096-150">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fe096-150">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="fe096-151">In the Azure portal, on the **SkyDesk Email** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fe096-151">In the Azure portal, on the **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="fe096-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fe096-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

1. <span data-ttu-id="fe096-155">On the **SkyDesk Email Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe096-155">On the **SkyDesk Email Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="fe096-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="fe096-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fe096-158">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="fe096-158">The value is not real.</span></span> <span data-ttu-id="fe096-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="fe096-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="fe096-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) to get the value.</span><span class="sxs-lookup"><span data-stu-id="fe096-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) to get the value.</span></span> 
 
1. <span data-ttu-id="fe096-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="fe096-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

1. <span data-ttu-id="fe096-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="fe096-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="fe096-165">On the **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="fe096-165">On the **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fe096-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="fe096-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

1. <span data-ttu-id="fe096-168">To enable SSO in **SkyDesk Email**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe096-168">To enable SSO in **SkyDesk Email**, perform the following steps:</span></span>

    <span data-ttu-id="fe096-169">a.</span><span class="sxs-lookup"><span data-stu-id="fe096-169">a.</span></span> <span data-ttu-id="fe096-170">Sign-on to your SkyDesk Email account as administrator.</span><span class="sxs-lookup"><span data-stu-id="fe096-170">Sign-on to your SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="fe096-171">b.</span><span class="sxs-lookup"><span data-stu-id="fe096-171">b.</span></span> <span data-ttu-id="fe096-172">In the menu on the top, click **Setup**, and select **Org**.</span><span class="sxs-lookup"><span data-stu-id="fe096-172">In the menu on the top, click **Setup**, and select **Org**.</span></span> 
    
      ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="fe096-174">c.</span><span class="sxs-lookup"><span data-stu-id="fe096-174">c.</span></span> <span data-ttu-id="fe096-175">Click on **Domains** from the left panel.</span><span class="sxs-lookup"><span data-stu-id="fe096-175">Click on **Domains** from the left panel.</span></span>
    
      ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="fe096-177">d.</span><span class="sxs-lookup"><span data-stu-id="fe096-177">d.</span></span> <span data-ttu-id="fe096-178">Click on **Add Domain**.</span><span class="sxs-lookup"><span data-stu-id="fe096-178">Click on **Add Domain**.</span></span>
    
      ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="fe096-180">e.</span><span class="sxs-lookup"><span data-stu-id="fe096-180">e.</span></span> <span data-ttu-id="fe096-181">Enter your Domain name, and then verify the Domain.</span><span class="sxs-lookup"><span data-stu-id="fe096-181">Enter your Domain name, and then verify the Domain.</span></span>
    
      ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="fe096-183">f.</span><span class="sxs-lookup"><span data-stu-id="fe096-183">f.</span></span> <span data-ttu-id="fe096-184">Click on **SAML Authentication** from the left panel.</span><span class="sxs-lookup"><span data-stu-id="fe096-184">Click on **SAML Authentication** from the left panel.</span></span>
    
      ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_52.png)

1. <span data-ttu-id="fe096-186">On the **SAML Authentication** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe096-186">On the **SAML Authentication** dialog page, perform the following steps:</span></span>
   
      ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="fe096-188">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span><span class="sxs-lookup"><span data-stu-id="fe096-188">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="fe096-189">You can set the portal URL with the unique name.</span><span class="sxs-lookup"><span data-stu-id="fe096-189">You can set the portal URL with the unique name.</span></span>
    > 
    > 
   
    ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="fe096-191">a.</span><span class="sxs-lookup"><span data-stu-id="fe096-191">a.</span></span> <span data-ttu-id="fe096-192">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fe096-192">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fe096-193">b.</span><span class="sxs-lookup"><span data-stu-id="fe096-193">b.</span></span> <span data-ttu-id="fe096-194">In the **Logout** URL textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fe096-194">In the **Logout** URL textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fe096-195">c.</span><span class="sxs-lookup"><span data-stu-id="fe096-195">c.</span></span> <span data-ttu-id="fe096-196">**Change Password URL** is optional so leave it blank.</span><span class="sxs-lookup"><span data-stu-id="fe096-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="fe096-197">d.</span><span class="sxs-lookup"><span data-stu-id="fe096-197">d.</span></span> <span data-ttu-id="fe096-198">Click on **Get Key From File** to select your downloaded certificate from Azure portal, and then click **Open** to upload the certificate.</span><span class="sxs-lookup"><span data-stu-id="fe096-198">Click on **Get Key From File** to select your downloaded certificate from Azure portal, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="fe096-199">e.</span><span class="sxs-lookup"><span data-stu-id="fe096-199">e.</span></span> <span data-ttu-id="fe096-200">As **Algorithm**, select **RSA**.</span><span class="sxs-lookup"><span data-stu-id="fe096-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="fe096-201">f.</span><span class="sxs-lookup"><span data-stu-id="fe096-201">f.</span></span> <span data-ttu-id="fe096-202">Click **Ok** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="fe096-202">Click **Ok** to save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="fe096-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="fe096-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fe096-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="fe096-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fe096-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fe096-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fe096-206">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fe096-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="fe096-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe096-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="fe096-209">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fe096-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fe096-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="fe096-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/skydeskemail-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="fe096-212">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="fe096-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/skydeskemail-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="fe096-214">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="fe096-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/skydeskemail-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="fe096-216">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe096-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fe096-218">a.</span><span class="sxs-lookup"><span data-stu-id="fe096-218">a.</span></span> <span data-ttu-id="fe096-219">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fe096-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fe096-220">b.</span><span class="sxs-lookup"><span data-stu-id="fe096-220">b.</span></span> <span data-ttu-id="fe096-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fe096-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fe096-222">c.</span><span class="sxs-lookup"><span data-stu-id="fe096-222">c.</span></span> <span data-ttu-id="fe096-223">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="fe096-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fe096-224">d.</span><span class="sxs-lookup"><span data-stu-id="fe096-224">d.</span></span> <span data-ttu-id="fe096-225">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fe096-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="fe096-226">Creating a SkyDesk Email test user</span><span class="sxs-lookup"><span data-stu-id="fe096-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="fe096-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="fe096-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="fe096-228">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span><span class="sxs-lookup"><span data-stu-id="fe096-228">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="fe096-230">If you need to create bulk users, you need to contact the [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="fe096-230">If you need to create bulk users, you need to contact the [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fe096-231">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fe096-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fe096-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="fe096-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SkyDesk Email.</span></span>

![Assign User][200] 

<span data-ttu-id="fe096-234">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fe096-234">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="fe096-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fe096-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="fe096-237">In the applications list, select **SkyDesk Email**.</span><span class="sxs-lookup"><span data-stu-id="fe096-237">In the applications list, select **SkyDesk Email**.</span></span>

    ![Configure Single Sign-On](./media/skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

1. <span data-ttu-id="fe096-239">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="fe096-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="fe096-241">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="fe096-241">Click **Add** button.</span></span> <span data-ttu-id="fe096-242">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fe096-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="fe096-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="fe096-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="fe096-245">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="fe096-245">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="fe096-246">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fe096-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fe096-247">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="fe096-247">Testing single sign-on</span></span>

<span data-ttu-id="fe096-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="fe096-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="fe096-249">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span><span class="sxs-lookup"><span data-stu-id="fe096-249">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe096-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="fe096-250">Additional resources</span></span>

* [<span data-ttu-id="fe096-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe096-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="fe096-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fe096-252">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/skydeskemail-tutorial/tutorial_general_203.png

