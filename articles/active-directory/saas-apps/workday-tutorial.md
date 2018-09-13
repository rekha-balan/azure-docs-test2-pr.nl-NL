---
title: 'Tutorial: Azure Active Directory integration with Workday | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Workday.
services: active-directory
documentationCenter: na
author: cmmdesai
manager: mtillman
ms.reviewer: jeedes
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/11/2018
ms.author: chmutali
ms.openlocfilehash: 78b9fe704c5c8a1f81da480787f1791e88bf4f72
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867101"
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="394a0-103">Tutorial: Azure Active Directory integration with Workday</span><span class="sxs-lookup"><span data-stu-id="394a0-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="394a0-104">In this tutorial, you learn how to integrate Workday with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="394a0-104">In this tutorial, you learn how to integrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="394a0-105">Integrating Workday with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="394a0-105">Integrating Workday with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="394a0-106">You can control in Azure AD who has access to Workday.</span><span class="sxs-lookup"><span data-stu-id="394a0-106">You can control in Azure AD who has access to Workday.</span></span>
- <span data-ttu-id="394a0-107">You can enable your users to automatically get signed-on to Workday (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="394a0-107">You can enable your users to automatically get signed-on to Workday (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="394a0-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="394a0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="394a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="394a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="394a0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="394a0-110">Prerequisites</span></span>

<span data-ttu-id="394a0-111">To configure Azure AD integration with Workday, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="394a0-111">To configure Azure AD integration with Workday, you need the following items:</span></span>

- <span data-ttu-id="394a0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="394a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="394a0-113">A Workday single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="394a0-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="394a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="394a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="394a0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="394a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="394a0-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="394a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="394a0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="394a0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="394a0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="394a0-118">Scenario description</span></span>

<span data-ttu-id="394a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="394a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="394a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="394a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="394a0-121">Adding Workday from the gallery</span><span class="sxs-lookup"><span data-stu-id="394a0-121">Adding Workday from the gallery</span></span>
2. <span data-ttu-id="394a0-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="394a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-the-gallery"></a><span data-ttu-id="394a0-123">Adding Workday from the gallery</span><span class="sxs-lookup"><span data-stu-id="394a0-123">Adding Workday from the gallery</span></span>

<span data-ttu-id="394a0-124">To configure the integration of Workday into Azure AD, you need to add Workday from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="394a0-124">To configure the integration of Workday into Azure AD, you need to add Workday from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="394a0-125">**To add Workday from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="394a0-125">**To add Workday from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="394a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="394a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="394a0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="394a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="394a0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="394a0-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="394a0-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="394a0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="394a0-133">In the search box, type **Workday**, select **Workday** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="394a0-133">In the search box, type **Workday**, select **Workday** from result panel then click **Add** button to add the application.</span></span>

    ![Workday in the results list](./media/workday-tutorial/tutorial_workday_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="394a0-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="394a0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="394a0-136">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="394a0-136">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="394a0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workday is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="394a0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workday is to a user in Azure AD.</span></span> <span data-ttu-id="394a0-138">In other words, a link relationship between an Azure AD user and the related user in Workday needs to be established.</span><span class="sxs-lookup"><span data-stu-id="394a0-138">In other words, a link relationship between an Azure AD user and the related user in Workday needs to be established.</span></span>

<span data-ttu-id="394a0-139">In Workday, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="394a0-139">In Workday, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="394a0-140">To configure and test Azure AD single sign-on with Workday, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="394a0-140">To configure and test Azure AD single sign-on with Workday, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="394a0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="394a0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="394a0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="394a0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="394a0-143">**[Create a Workday test user](#create-a-workday-test-user)** - to have a counterpart of Britta Simon in Workday that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="394a0-143">**[Create a Workday test user](#create-a-workday-test-user)** - to have a counterpart of Britta Simon in Workday that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="394a0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="394a0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="394a0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="394a0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="394a0-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="394a0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="394a0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workday application.</span><span class="sxs-lookup"><span data-stu-id="394a0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="394a0-148">**To configure Azure AD single sign-on with Workday, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="394a0-148">**To configure Azure AD single sign-on with Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="394a0-149">In the Azure portal, on the **Workday** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="394a0-149">In the Azure portal, on the **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="394a0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="394a0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="394a0-153">On the **Workday Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="394a0-153">On the **Workday Domain and URLs** section, perform the following steps:</span></span>

    ![Workday Domain and URLs single sign-on information](./media/workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="394a0-155">a.</span><span class="sxs-lookup"><span data-stu-id="394a0-155">a.</span></span> <span data-ttu-id="394a0-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="394a0-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="394a0-157">b.</span><span class="sxs-lookup"><span data-stu-id="394a0-157">b.</span></span> <span data-ttu-id="394a0-158">In the **Identifier** textbox, type a URL: `http://www.workday.com`</span><span class="sxs-lookup"><span data-stu-id="394a0-158">In the **Identifier** textbox, type a URL: `http://www.workday.com`</span></span>

4. <span data-ttu-id="394a0-159">Check **Show advanced URL settings** and perform the following step:</span><span class="sxs-lookup"><span data-stu-id="394a0-159">Check **Show advanced URL settings** and perform the following step:</span></span>

    ![Workday Domain and URLs single sign-on information](./media/workday-tutorial/tutorial_workday_url1.png)

    <span data-ttu-id="394a0-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="394a0-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE]
    > <span data-ttu-id="394a0-162">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="394a0-162">These values are not the real.</span></span> <span data-ttu-id="394a0-163">Update these values with the actual Sign-on URL and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="394a0-163">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="394a0-164">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span><span class="sxs-lookup"><span data-stu-id="394a0-164">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span>
    > <span data-ttu-id="394a0-165">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span><span class="sxs-lookup"><span data-stu-id="394a0-165">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="394a0-166">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="394a0-166">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get these values.</span></span>

5. <span data-ttu-id="394a0-167">Workday application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="394a0-167">Workday application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="394a0-168">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="394a0-168">Configure the following claims for this application.</span></span> <span data-ttu-id="394a0-169">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="394a0-169">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="394a0-170">The following screenshot shows an example for this configuration.</span><span class="sxs-lookup"><span data-stu-id="394a0-170">The following screenshot shows an example for this configuration.</span></span>

    ![Configure Single Sign-On](./media/Workday-tutorial/tutorial_workday_attributes.png)

    > [!NOTE]
    > <span data-ttu-id="394a0-172">Here we have mapped the Name ID with UPN (user.userprincipalname) as default.</span><span class="sxs-lookup"><span data-stu-id="394a0-172">Here we have mapped the Name ID with UPN (user.userprincipalname) as default.</span></span> <span data-ttu-id="394a0-173">You need to map the Name ID with actual User ID in your Workday account (your email, UPN etc.) for successful working of SSO.</span><span class="sxs-lookup"><span data-stu-id="394a0-173">You need to map the Name ID with actual User ID in your Workday account (your email, UPN etc.) for successful working of SSO.</span></span>

6. <span data-ttu-id="394a0-174">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="394a0-174">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/workday-tutorial/tutorial_workday_certificate.png)

7. <span data-ttu-id="394a0-176">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="394a0-176">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/workday-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="394a0-178">On the **Workday Configuration** section, click **Configure Workday** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="394a0-178">On the **Workday Configuration** section, click **Configure Workday** to open **Configure sign-on** window.</span></span> <span data-ttu-id="394a0-179">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="394a0-179">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Workday Configuration](./media/workday-tutorial/tutorial_workday_configure.png)

9. <span data-ttu-id="394a0-181">In a different web browser window, log in to your Workday company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="394a0-181">In a different web browser window, log in to your Workday company site as an administrator.</span></span>

10. <span data-ttu-id="394a0-182">In the **Search box** search with the name **Edit Tenant Setup – Security** on the top left side of the home page.</span><span class="sxs-lookup"><span data-stu-id="394a0-182">In the **Search box** search with the name **Edit Tenant Setup – Security** on the top left side of the home page.</span></span>

    <span data-ttu-id="394a0-183">![Edit Tenant Security](./media/workday-tutorial/IC782925.png "Edit Tenant Security")</span><span class="sxs-lookup"><span data-stu-id="394a0-183">![Edit Tenant Security](./media/workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="394a0-184">In the **Redirection URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="394a0-184">In the **Redirection URLs** section, perform the following steps:</span></span>

    <span data-ttu-id="394a0-185">![Redirection URLs](./media/workday-tutorial/IC7829581.png "Redirection URLs")</span><span class="sxs-lookup"><span data-stu-id="394a0-185">![Redirection URLs](./media/workday-tutorial/IC7829581.png "Redirection URLs")</span></span>

    <span data-ttu-id="394a0-186">a.</span><span class="sxs-lookup"><span data-stu-id="394a0-186">a.</span></span> <span data-ttu-id="394a0-187">Click **Add Row**.</span><span class="sxs-lookup"><span data-stu-id="394a0-187">Click **Add Row**.</span></span>

    <span data-ttu-id="394a0-188">b.</span><span class="sxs-lookup"><span data-stu-id="394a0-188">b.</span></span> <span data-ttu-id="394a0-189">In the **Login Redirect URL** textbox and the **Mobile Redirect URL** textbox, type the **Sign-on URL** you have entered on the **Workday Domain and URLs** section of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="394a0-189">In the **Login Redirect URL** textbox and the **Mobile Redirect URL** textbox, type the **Sign-on URL** you have entered on the **Workday Domain and URLs** section of the Azure portal.</span></span>

    <span data-ttu-id="394a0-190">c.</span><span class="sxs-lookup"><span data-stu-id="394a0-190">c.</span></span> <span data-ttu-id="394a0-191">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL**, and then paste it into the **Logout Redirect URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="394a0-191">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL**, and then paste it into the **Logout Redirect URL** textbox.</span></span>

    <span data-ttu-id="394a0-192">d.</span><span class="sxs-lookup"><span data-stu-id="394a0-192">d.</span></span> <span data-ttu-id="394a0-193">In **Used for Environments** textbox, select the environment name.</span><span class="sxs-lookup"><span data-stu-id="394a0-193">In **Used for Environments** textbox, select the environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="394a0-194">The value of the Environment attribute is tied to the value of the tenant URL:</span><span class="sxs-lookup"><span data-stu-id="394a0-194">The value of the Environment attribute is tied to the value of the tenant URL:</span></span>  
    ><span data-ttu-id="394a0-195">-If the domain name of the Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), the **Environment** attribute must be set to Implementation.</span><span class="sxs-lookup"><span data-stu-id="394a0-195">-If the domain name of the Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), the **Environment** attribute must be set to Implementation.</span></span>  
    ><span data-ttu-id="394a0-196">-If the domain name starts with something else, you need to contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get the matching **Environment** value.</span><span class="sxs-lookup"><span data-stu-id="394a0-196">-If the domain name starts with something else, you need to contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get the matching **Environment** value.</span></span>

12. <span data-ttu-id="394a0-197">In the **SAML Setup** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="394a0-197">In the **SAML Setup** section, perform the following steps:</span></span>

    <span data-ttu-id="394a0-198">![SAML Setup](./media/workday-tutorial/IC782926.png "SAML Setup")</span><span class="sxs-lookup"><span data-stu-id="394a0-198">![SAML Setup](./media/workday-tutorial/IC782926.png "SAML Setup")</span></span>

    <span data-ttu-id="394a0-199">a.</span><span class="sxs-lookup"><span data-stu-id="394a0-199">a.</span></span>  <span data-ttu-id="394a0-200">Select **Enable SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="394a0-200">Select **Enable SAML Authentication**.</span></span>

    <span data-ttu-id="394a0-201">b.</span><span class="sxs-lookup"><span data-stu-id="394a0-201">b.</span></span>  <span data-ttu-id="394a0-202">Click **Add Row**.</span><span class="sxs-lookup"><span data-stu-id="394a0-202">Click **Add Row**.</span></span>

13. <span data-ttu-id="394a0-203">In the **SAML Identity Providers** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="394a0-203">In the **SAML Identity Providers** section, perform the following steps:</span></span>

    <span data-ttu-id="394a0-204">![SAML Identity Providers](./media/workday-tutorial/IC7829271.png "SAML Identity Providers")</span><span class="sxs-lookup"><span data-stu-id="394a0-204">![SAML Identity Providers](./media/workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>

    <span data-ttu-id="394a0-205">a.</span><span class="sxs-lookup"><span data-stu-id="394a0-205">a.</span></span> <span data-ttu-id="394a0-206">In the **Identity Provider Name** textbox, type a provider name (for example: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="394a0-206">In the **Identity Provider Name** textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>

    <span data-ttu-id="394a0-207">b.</span><span class="sxs-lookup"><span data-stu-id="394a0-207">b.</span></span> <span data-ttu-id="394a0-208">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Entity ID** value, and then paste it into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="394a0-208">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Entity ID** value, and then paste it into the **Issuer** textbox.</span></span>

    <span data-ttu-id="394a0-209">![SAML Identity Providers](./media/workday-tutorial/IC7829272.png "SAML Identity Providers")</span><span class="sxs-lookup"><span data-stu-id="394a0-209">![SAML Identity Providers](./media/workday-tutorial/IC7829272.png "SAML Identity Providers")</span></span>

    <span data-ttu-id="394a0-210">c.</span><span class="sxs-lookup"><span data-stu-id="394a0-210">c.</span></span> <span data-ttu-id="394a0-211">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL** value, and then paste it into the **Logout Response URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="394a0-211">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL** value, and then paste it into the **Logout Response URL** textbox.</span></span>

    <span data-ttu-id="394a0-212">d.</span><span class="sxs-lookup"><span data-stu-id="394a0-212">d.</span></span> <span data-ttu-id="394a0-213">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **IdP SSO Service URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="394a0-213">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **IdP SSO Service URL** textbox.</span></span>

    <span data-ttu-id="394a0-214">e.</span><span class="sxs-lookup"><span data-stu-id="394a0-214">e.</span></span> <span data-ttu-id="394a0-215">In **Used for Environments** textbox, select the environment name.</span><span class="sxs-lookup"><span data-stu-id="394a0-215">In **Used for Environments** textbox, select the environment name.</span></span>

    <span data-ttu-id="394a0-216">f.</span><span class="sxs-lookup"><span data-stu-id="394a0-216">f.</span></span> <span data-ttu-id="394a0-217">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="394a0-217">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span>

    <span data-ttu-id="394a0-218">![Create](./media/workday-tutorial/IC782928.png "Create")</span><span class="sxs-lookup"><span data-stu-id="394a0-218">![Create](./media/workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="394a0-219">g.</span><span class="sxs-lookup"><span data-stu-id="394a0-219">g.</span></span> <span data-ttu-id="394a0-220">Click **Create x509 Public Key**.</span><span class="sxs-lookup"><span data-stu-id="394a0-220">Click **Create x509 Public Key**.</span></span>

    <span data-ttu-id="394a0-221">![Create](./media/workday-tutorial/IC782929.png "Create")</span><span class="sxs-lookup"><span data-stu-id="394a0-221">![Create](./media/workday-tutorial/IC782929.png "Create")</span></span>

14. <span data-ttu-id="394a0-222">In the **View x509 Public Key** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="394a0-222">In the **View x509 Public Key** section, perform the following steps:</span></span>

    <span data-ttu-id="394a0-223">![View x509 Public Key](./media/workday-tutorial/IC782930.png "View x509 Public Key")</span><span class="sxs-lookup"><span data-stu-id="394a0-223">![View x509 Public Key](./media/workday-tutorial/IC782930.png "View x509 Public Key")</span></span>

    <span data-ttu-id="394a0-224">a.</span><span class="sxs-lookup"><span data-stu-id="394a0-224">a.</span></span> <span data-ttu-id="394a0-225">In the **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span><span class="sxs-lookup"><span data-stu-id="394a0-225">In the **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>

    <span data-ttu-id="394a0-226">b.</span><span class="sxs-lookup"><span data-stu-id="394a0-226">b.</span></span> <span data-ttu-id="394a0-227">In the **Valid From** textbox, type the valid from attribute value of your certificate.</span><span class="sxs-lookup"><span data-stu-id="394a0-227">In the **Valid From** textbox, type the valid from attribute value of your certificate.</span></span>

    <span data-ttu-id="394a0-228">c.</span><span class="sxs-lookup"><span data-stu-id="394a0-228">c.</span></span>  <span data-ttu-id="394a0-229">In the **Valid To** textbox, type the valid to attribute value of your certificate.</span><span class="sxs-lookup"><span data-stu-id="394a0-229">In the **Valid To** textbox, type the valid to attribute value of your certificate.</span></span>

    > [!NOTE]
    > <span data-ttu-id="394a0-230">You can get the valid from date and the valid to date from the downloaded certificate by double-clicking it.</span><span class="sxs-lookup"><span data-stu-id="394a0-230">You can get the valid from date and the valid to date from the downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="394a0-231">The dates are listed under the **Details** tab.</span><span class="sxs-lookup"><span data-stu-id="394a0-231">The dates are listed under the **Details** tab.</span></span>
    >
    >

    <span data-ttu-id="394a0-232">d.</span><span class="sxs-lookup"><span data-stu-id="394a0-232">d.</span></span>  <span data-ttu-id="394a0-233">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span><span class="sxs-lookup"><span data-stu-id="394a0-233">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>

    <span data-ttu-id="394a0-234">e.</span><span class="sxs-lookup"><span data-stu-id="394a0-234">e.</span></span>  <span data-ttu-id="394a0-235">In the **Certificate** textbox, paste the content of your clipboard.</span><span class="sxs-lookup"><span data-stu-id="394a0-235">In the **Certificate** textbox, paste the content of your clipboard.</span></span>

    <span data-ttu-id="394a0-236">f.</span><span class="sxs-lookup"><span data-stu-id="394a0-236">f.</span></span>  <span data-ttu-id="394a0-237">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="394a0-237">Click **OK**.</span></span>

15. <span data-ttu-id="394a0-238">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="394a0-238">Perform the following steps:</span></span>

    <span data-ttu-id="394a0-239">![SSO configuration](./media/workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span><span class="sxs-lookup"><span data-stu-id="394a0-239">![SSO configuration](./media/workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>

    <span data-ttu-id="394a0-240">a.</span><span class="sxs-lookup"><span data-stu-id="394a0-240">a.</span></span>  <span data-ttu-id="394a0-241">In the **Service Provider ID** textbox, type **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="394a0-241">In the **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>

    <span data-ttu-id="394a0-242">b.</span><span class="sxs-lookup"><span data-stu-id="394a0-242">b.</span></span> <span data-ttu-id="394a0-243">Select **Do Not Deflate SP-initiated Authentication Request**.</span><span class="sxs-lookup"><span data-stu-id="394a0-243">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>

    <span data-ttu-id="394a0-244">c.</span><span class="sxs-lookup"><span data-stu-id="394a0-244">c.</span></span> <span data-ttu-id="394a0-245">As **Authentication Request Signature Method**, select **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="394a0-245">As **Authentication Request Signature Method**, select **SHA256**.</span></span>

    <span data-ttu-id="394a0-246">![Authentication Request Signature Method](./media/workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span><span class="sxs-lookup"><span data-stu-id="394a0-246">![Authentication Request Signature Method](./media/workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 

    <span data-ttu-id="394a0-247">d.</span><span class="sxs-lookup"><span data-stu-id="394a0-247">d.</span></span> <span data-ttu-id="394a0-248">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="394a0-248">Click **OK**.</span></span>

    <span data-ttu-id="394a0-249">![OK](./media/workday-tutorial/IC782933.png "OK")</span><span class="sxs-lookup"><span data-stu-id="394a0-249">![OK](./media/workday-tutorial/IC782933.png "OK")</span></span>

    > [!NOTE]
    > <span data-ttu-id="394a0-250">Please ensure you set up single sign-on correctly.</span><span class="sxs-lookup"><span data-stu-id="394a0-250">Please ensure you set up single sign-on correctly.</span></span> <span data-ttu-id="394a0-251">In case you enable single sign-on with incorrect setup, you may not be able to enter the application with your credentials and get locked out. In this situation, Workday provides a backup log-in url where users can sign-in using their normal username and password in the following format:[Your Workday URL]/login.flex?redirect=n</span><span class="sxs-lookup"><span data-stu-id="394a0-251">In case you enable single sign-on with incorrect setup, you may not be able to enter the application with your credentials and get locked out. In this situation, Workday provides a backup log-in url where users can sign-in using their normal username and password in the following format:[Your Workday URL]/login.flex?redirect=n</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="394a0-252">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="394a0-252">Create an Azure AD test user</span></span>

<span data-ttu-id="394a0-253">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="394a0-253">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="394a0-255">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="394a0-255">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="394a0-256">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="394a0-256">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/workday-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="394a0-258">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="394a0-258">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/workday-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="394a0-260">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="394a0-260">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/workday-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="394a0-262">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="394a0-262">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/workday-tutorial/create_aaduser_04.png)

    <span data-ttu-id="394a0-264">a.</span><span class="sxs-lookup"><span data-stu-id="394a0-264">a.</span></span> <span data-ttu-id="394a0-265">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="394a0-265">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="394a0-266">b.</span><span class="sxs-lookup"><span data-stu-id="394a0-266">b.</span></span> <span data-ttu-id="394a0-267">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="394a0-267">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="394a0-268">c.</span><span class="sxs-lookup"><span data-stu-id="394a0-268">c.</span></span> <span data-ttu-id="394a0-269">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="394a0-269">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="394a0-270">d.</span><span class="sxs-lookup"><span data-stu-id="394a0-270">d.</span></span> <span data-ttu-id="394a0-271">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="394a0-271">Click **Create**.</span></span>
 
### <a name="create-a-workday-test-user"></a><span data-ttu-id="394a0-272">Create a Workday test user</span><span class="sxs-lookup"><span data-stu-id="394a0-272">Create a Workday test user</span></span>

<span data-ttu-id="394a0-273">In this section, you create a user called Britta Simon in Workday.</span><span class="sxs-lookup"><span data-stu-id="394a0-273">In this section, you create a user called Britta Simon in Workday.</span></span> <span data-ttu-id="394a0-274">Work with [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to add the users in the Workday platform.</span><span class="sxs-lookup"><span data-stu-id="394a0-274">Work with [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to add the users in the Workday platform.</span></span> <span data-ttu-id="394a0-275">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="394a0-275">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="394a0-276">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="394a0-276">Assign the Azure AD test user</span></span>

<span data-ttu-id="394a0-277">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workday.</span><span class="sxs-lookup"><span data-stu-id="394a0-277">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workday.</span></span>

![Assign the user role][200] 

<span data-ttu-id="394a0-279">**To assign Britta Simon to Workday, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="394a0-279">**To assign Britta Simon to Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="394a0-280">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="394a0-280">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="394a0-282">In the applications list, select **Workday**.</span><span class="sxs-lookup"><span data-stu-id="394a0-282">In the applications list, select **Workday**.</span></span>

    ![The Workday link in the Applications list](./media/workday-tutorial/tutorial_workday_app.png)  

3. <span data-ttu-id="394a0-284">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="394a0-284">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="394a0-286">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="394a0-286">Click **Add** button.</span></span> <span data-ttu-id="394a0-287">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="394a0-287">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="394a0-289">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="394a0-289">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="394a0-290">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="394a0-290">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="394a0-291">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="394a0-291">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="394a0-292">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="394a0-292">Test single sign-on</span></span>

<span data-ttu-id="394a0-293">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="394a0-293">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="394a0-294">When you click the Workday tile in the Access Panel, you should get automatically signed-on to your Workday application.</span><span class="sxs-lookup"><span data-stu-id="394a0-294">When you click the Workday tile in the Access Panel, you should get automatically signed-on to your Workday application.</span></span>
<span data-ttu-id="394a0-295">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="394a0-295">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="394a0-296">Additional resources</span><span class="sxs-lookup"><span data-stu-id="394a0-296">Additional resources</span></span>

* [<span data-ttu-id="394a0-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="394a0-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="394a0-298">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="394a0-298">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/workday-tutorial/tutorial_general_01.png
[2]: ./media/workday-tutorial/tutorial_general_02.png
[3]: ./media/workday-tutorial/tutorial_general_03.png
[4]: ./media/workday-tutorial/tutorial_general_04.png

[100]: ./media/workday-tutorial/tutorial_general_100.png

[200]: ./media/workday-tutorial/tutorial_general_200.png
[201]: ./media/workday-tutorial/tutorial_general_201.png
[202]: ./media/workday-tutorial/tutorial_general_202.png
[203]: ./media/workday-tutorial/tutorial_general_203.png
