---
title: 'Tutorial: Azure Active Directory integration with Workplace by Facebook | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Workplace by Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2018
ms.author: jeedes
ms.openlocfilehash: 1f83dd64c7f6773ddb8956e6ebbc37b8c55aacec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867590"
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="f99be-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="f99be-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="f99be-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f99be-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f99be-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f99be-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f99be-106">You can control in Azure AD who has access to Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="f99be-106">You can control in Azure AD who has access to Workplace by Facebook</span></span>
- <span data-ttu-id="f99be-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f99be-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f99be-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f99be-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f99be-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f99be-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f99be-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f99be-110">Prerequisites</span></span>

<span data-ttu-id="f99be-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f99be-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="f99be-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f99be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f99be-113">A Workplace by Facebook single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f99be-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f99be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f99be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f99be-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f99be-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f99be-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f99be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f99be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f99be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

> [!NOTE]
> <span data-ttu-id="f99be-118">Facebook has two products, Workplace Standard (free) and Workplace Premium (paid).</span><span class="sxs-lookup"><span data-stu-id="f99be-118">Facebook has two products, Workplace Standard (free) and Workplace Premium (paid).</span></span> <span data-ttu-id="f99be-119">Any Workplace Premium tenant can configure SCIM and SSO integration with no other implications to cost or licenses required.</span><span class="sxs-lookup"><span data-stu-id="f99be-119">Any Workplace Premium tenant can configure SCIM and SSO integration with no other implications to cost or licenses required.</span></span> <span data-ttu-id="f99be-120">SSO and SCIM are not available in Workplace Standard instances.</span><span class="sxs-lookup"><span data-stu-id="f99be-120">SSO and SCIM are not available in Workplace Standard instances.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f99be-121">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f99be-121">Scenario description</span></span>
<span data-ttu-id="f99be-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f99be-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f99be-123">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f99be-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f99be-124">Adding Workplace by Facebook from the gallery</span><span class="sxs-lookup"><span data-stu-id="f99be-124">Adding Workplace by Facebook from the gallery</span></span>
1. <span data-ttu-id="f99be-125">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f99be-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="f99be-126">Adding Workplace by Facebook from the gallery</span><span class="sxs-lookup"><span data-stu-id="f99be-126">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="f99be-127">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f99be-127">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f99be-128">**To add Workplace by Facebook from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f99be-128">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f99be-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f99be-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="f99be-131">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f99be-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f99be-132">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f99be-132">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="f99be-134">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f99be-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="f99be-136">In the search box, type **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="f99be-136">In the search box, type **Workplace by Facebook**.</span></span>

    ![Creating an Azure AD test user](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

1. <span data-ttu-id="f99be-138">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f99be-138">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f99be-140">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f99be-140">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f99be-141">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f99be-141">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f99be-142">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f99be-142">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="f99be-143">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f99be-143">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span></span>

<span data-ttu-id="f99be-144">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="f99be-144">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="f99be-145">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f99be-145">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f99be-146">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f99be-146">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f99be-147">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span><span class="sxs-lookup"><span data-stu-id="f99be-147">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span></span>
1. <span data-ttu-id="f99be-148">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f99be-148">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f99be-149">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f99be-149">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f99be-150">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f99be-150">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f99be-151">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f99be-151">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f99be-152">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f99be-152">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f99be-153">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span><span class="sxs-lookup"><span data-stu-id="f99be-153">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="f99be-154">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f99be-154">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="f99be-155">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f99be-155">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="f99be-157">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f99be-157">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

1. <span data-ttu-id="f99be-159">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f99be-159">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="f99be-161">a.</span><span class="sxs-lookup"><span data-stu-id="f99be-161">a.</span></span> <span data-ttu-id="f99be-162">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="f99be-162">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="f99be-163">b.</span><span class="sxs-lookup"><span data-stu-id="f99be-163">b.</span></span> <span data-ttu-id="f99be-164">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instanceID>`</span><span class="sxs-lookup"><span data-stu-id="f99be-164">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instanceID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f99be-165">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="f99be-165">These values are not the real.</span></span> <span data-ttu-id="f99be-166">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="f99be-166">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f99be-167">See the Authentication page of the Workplace Company Dashboard for the correct values for your Workplace community.</span><span class="sxs-lookup"><span data-stu-id="f99be-167">See the Authentication page of the Workplace Company Dashboard for the correct values for your Workplace community.</span></span> 

1. <span data-ttu-id="f99be-168">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f99be-168">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

1. <span data-ttu-id="f99be-170">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f99be-170">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/workplacebyfacebook-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f99be-172">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="f99be-172">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f99be-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="f99be-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/workplacebyfacebook-tutorial/config.png) 

1. <span data-ttu-id="f99be-175">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f99be-175">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="f99be-176">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f99be-176">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

1. <span data-ttu-id="f99be-177">In the **Company Dashboard**, go to the **Authentication** tab.</span><span class="sxs-lookup"><span data-stu-id="f99be-177">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

1. <span data-ttu-id="f99be-178">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f99be-178">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

1. <span data-ttu-id="f99be-179">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span><span class="sxs-lookup"><span data-stu-id="f99be-179">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="f99be-180">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f99be-180">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="f99be-181">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f99be-181">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="f99be-182">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f99be-182">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="f99be-183">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="f99be-183">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

1. <span data-ttu-id="f99be-184">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="f99be-184">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span></span>

1. <span data-ttu-id="f99be-185">Scroll to the bottom of the section and click the **Test SSO** button.</span><span class="sxs-lookup"><span data-stu-id="f99be-185">Scroll to the bottom of the section and click the **Test SSO** button.</span></span> <span data-ttu-id="f99be-186">This results in a popup window appearing with Azure AD login page presented.</span><span class="sxs-lookup"><span data-stu-id="f99be-186">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="f99be-187">Enter your credentials in as normal to authenticate.</span><span class="sxs-lookup"><span data-stu-id="f99be-187">Enter your credentials in as normal to authenticate.</span></span> 

    <span data-ttu-id="f99be-188">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span><span class="sxs-lookup"><span data-stu-id="f99be-188">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

1. <span data-ttu-id="f99be-189">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f99be-189">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span></span>

1. <span data-ttu-id="f99be-190">All users using Workplace will now be presented with Azure AD login page for authentication.</span><span class="sxs-lookup"><span data-stu-id="f99be-190">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

1. <span data-ttu-id="f99be-191">**SAML Logout Redirect (optional)** -</span><span class="sxs-lookup"><span data-stu-id="f99be-191">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="f99be-192">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span><span class="sxs-lookup"><span data-stu-id="f99be-192">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span></span> <span data-ttu-id="f99be-193">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span><span class="sxs-lookup"><span data-stu-id="f99be-193">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span></span> <span data-ttu-id="f99be-194">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span><span class="sxs-lookup"><span data-stu-id="f99be-194">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="f99be-195">Configuring Reauthentication Frequency</span><span class="sxs-lookup"><span data-stu-id="f99be-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="f99be-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span><span class="sxs-lookup"><span data-stu-id="f99be-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="f99be-197">The minimum value for the SAML check on mobile applications is set to one week.</span><span class="sxs-lookup"><span data-stu-id="f99be-197">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="f99be-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span><span class="sxs-lookup"><span data-stu-id="f99be-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f99be-199">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f99be-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="f99be-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f99be-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="f99be-202">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f99be-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f99be-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f99be-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/workplacebyfacebook-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="f99be-205">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f99be-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/workplacebyfacebook-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="f99be-207">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f99be-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/workplacebyfacebook-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="f99be-209">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f99be-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f99be-211">a.</span><span class="sxs-lookup"><span data-stu-id="f99be-211">a.</span></span> <span data-ttu-id="f99be-212">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f99be-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f99be-213">b.</span><span class="sxs-lookup"><span data-stu-id="f99be-213">b.</span></span> <span data-ttu-id="f99be-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f99be-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f99be-215">c.</span><span class="sxs-lookup"><span data-stu-id="f99be-215">c.</span></span> <span data-ttu-id="f99be-216">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f99be-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f99be-217">d.</span><span class="sxs-lookup"><span data-stu-id="f99be-217">d.</span></span> <span data-ttu-id="f99be-218">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f99be-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="f99be-219">Creating a Workplace by Facebook test user</span><span class="sxs-lookup"><span data-stu-id="f99be-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="f99be-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="f99be-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="f99be-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="f99be-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="f99be-222">There is no action for you in this section.</span><span class="sxs-lookup"><span data-stu-id="f99be-222">There is no action for you in this section.</span></span> <span data-ttu-id="f99be-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="f99be-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="f99be-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="f99be-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f99be-225">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f99be-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f99be-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="f99be-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span></span>

![Assign User][200] 

<span data-ttu-id="f99be-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f99be-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="f99be-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f99be-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f99be-231">In the applications list, select **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="f99be-231">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Configure Single Sign-On](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

1. <span data-ttu-id="f99be-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f99be-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="f99be-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f99be-235">Click **Add** button.</span></span> <span data-ttu-id="f99be-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f99be-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="f99be-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f99be-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f99be-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f99be-239">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f99be-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f99be-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f99be-241">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f99be-241">Testing single sign-on</span></span>

<span data-ttu-id="f99be-242">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f99be-242">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="f99be-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f99be-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f99be-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f99be-244">Additional resources</span></span>

* [<span data-ttu-id="f99be-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f99be-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f99be-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f99be-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="f99be-247">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="f99be-247">Configure User Provisioning</span></span>](workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/workplacebyfacebook-tutorial/tutorial_general_203.png
