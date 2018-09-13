---
title: 'Tutorial: Azure Active Directory integration with SECURE DELIVER | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SECURE DELIVER.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: fccd5668-fe6f-4e6d-a9ce-ba4f321c33d1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 3c3d06d3b44b837af8da3c638dd6f1428c5086cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965940"
---
# <a name="tutorial-azure-active-directory-integration-with-secure-deliver"></a><span data-ttu-id="36432-103">Tutorial: Azure Active Directory integration with SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="36432-103">Tutorial: Azure Active Directory integration with SECURE DELIVER</span></span>

<span data-ttu-id="36432-104">In this tutorial, you learn how to integrate SECURE DELIVER with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36432-104">In this tutorial, you learn how to integrate SECURE DELIVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36432-105">Integrating SECURE DELIVER with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="36432-105">Integrating SECURE DELIVER with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="36432-106">You can control in Azure AD who has access to SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="36432-106">You can control in Azure AD who has access to SECURE DELIVER</span></span>
- <span data-ttu-id="36432-107">You can enable your users to automatically get signed-on to SECURE DELIVER (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="36432-107">You can enable your users to automatically get signed-on to SECURE DELIVER (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36432-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="36432-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="36432-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="36432-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36432-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="36432-110">Prerequisites</span></span>

<span data-ttu-id="36432-111">To configure Azure AD integration with SECURE DELIVER, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="36432-111">To configure Azure AD integration with SECURE DELIVER, you need the following items:</span></span>

- <span data-ttu-id="36432-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="36432-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36432-113">A SECURE DELIVER single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="36432-113">A SECURE DELIVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36432-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="36432-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36432-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="36432-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36432-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="36432-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36432-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36432-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36432-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="36432-118">Scenario description</span></span>
<span data-ttu-id="36432-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="36432-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36432-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="36432-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36432-121">Adding SECURE DELIVER from the gallery</span><span class="sxs-lookup"><span data-stu-id="36432-121">Adding SECURE DELIVER from the gallery</span></span>
1. <span data-ttu-id="36432-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="36432-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-secure-deliver-from-the-gallery"></a><span data-ttu-id="36432-123">Adding SECURE DELIVER from the gallery</span><span class="sxs-lookup"><span data-stu-id="36432-123">Adding SECURE DELIVER from the gallery</span></span>
<span data-ttu-id="36432-124">To configure the integration of SECURE DELIVER into Azure AD, you need to add SECURE DELIVER from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="36432-124">To configure the integration of SECURE DELIVER into Azure AD, you need to add SECURE DELIVER from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="36432-125">**To add SECURE DELIVER from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36432-125">**To add SECURE DELIVER from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="36432-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="36432-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="36432-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="36432-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="36432-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="36432-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="36432-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="36432-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="36432-133">In the search box, type **SECURE DELIVER**.</span><span class="sxs-lookup"><span data-stu-id="36432-133">In the search box, type **SECURE DELIVER**.</span></span>

    ![Creating an Azure AD test user](./media/securedeliver-tutorial/tutorial_securedeliver_search.png)

1. <span data-ttu-id="36432-135">In the results panel, select **SECURE DELIVER**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="36432-135">In the results panel, select **SECURE DELIVER**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/securedeliver-tutorial/tutorial_securedeliver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36432-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="36432-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36432-138">In this section, you configure and test Azure AD single sign-on with SECURE DELIVER based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="36432-138">In this section, you configure and test Azure AD single sign-on with SECURE DELIVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="36432-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SECURE DELIVER is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36432-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SECURE DELIVER is to a user in Azure AD.</span></span> <span data-ttu-id="36432-140">In other words, a link relationship between an Azure AD user and the related user in SECURE DELIVER needs to be established.</span><span class="sxs-lookup"><span data-stu-id="36432-140">In other words, a link relationship between an Azure AD user and the related user in SECURE DELIVER needs to be established.</span></span>

<span data-ttu-id="36432-141">In SECURE DELIVER, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="36432-141">In SECURE DELIVER, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="36432-142">To configure and test Azure AD single sign-on with SECURE DELIVER, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="36432-142">To configure and test Azure AD single sign-on with SECURE DELIVER, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="36432-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="36432-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="36432-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36432-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="36432-145">**[Creating a SECURE DELIVER test user](#creating-a-secure-deliver-test-user)** - to have a counterpart of Britta Simon in SECURE DELIVER that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="36432-145">**[Creating a SECURE DELIVER test user](#creating-a-secure-deliver-test-user)** - to have a counterpart of Britta Simon in SECURE DELIVER that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="36432-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="36432-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="36432-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="36432-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36432-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="36432-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36432-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SECURE DELIVER application.</span><span class="sxs-lookup"><span data-stu-id="36432-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SECURE DELIVER application.</span></span>

<span data-ttu-id="36432-150">**To configure Azure AD single sign-on with SECURE DELIVER, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36432-150">**To configure Azure AD single sign-on with SECURE DELIVER, perform the following steps:**</span></span>

1. <span data-ttu-id="36432-151">In the Azure portal, on the **SECURE DELIVER** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="36432-151">In the Azure portal, on the **SECURE DELIVER** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="36432-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="36432-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/securedeliver-tutorial/tutorial_securedeliver_samlbase.png)

1. <span data-ttu-id="36432-155">On the **SECURE DELIVER Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="36432-155">On the **SECURE DELIVER Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/securedeliver-tutorial/tutorial_securedeliver_url.png)

    <span data-ttu-id="36432-157">a.</span><span class="sxs-lookup"><span data-stu-id="36432-157">a.</span></span> <span data-ttu-id="36432-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span><span class="sxs-lookup"><span data-stu-id="36432-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span></span>

    <span data-ttu-id="36432-159">b.</span><span class="sxs-lookup"><span data-stu-id="36432-159">b.</span></span> <span data-ttu-id="36432-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span><span class="sxs-lookup"><span data-stu-id="36432-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36432-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="36432-161">These values are not real.</span></span> <span data-ttu-id="36432-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="36432-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="36432-163">Contact [SECURE DELIVER Client support team](mailto:iw-sd-support@fujifilm.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="36432-163">Contact [SECURE DELIVER Client support team](mailto:iw-sd-support@fujifilm.com) to get these values.</span></span> 
 
1. <span data-ttu-id="36432-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="36432-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/securedeliver-tutorial/tutorial_securedeliver_certificate.png) 

1. <span data-ttu-id="36432-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="36432-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/securedeliver-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="36432-168">On the **SECURE DELIVER Configuration** section, click **Configure SECURE DELIVER** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="36432-168">On the **SECURE DELIVER Configuration** section, click **Configure SECURE DELIVER** to open **Configure sign-on** window.</span></span> <span data-ttu-id="36432-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="36432-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/securedeliver-tutorial/tutorial_securedeliver_configure.png) 

1. <span data-ttu-id="36432-171">To configure single sign-on on **SECURE DELIVER** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com).</span><span class="sxs-lookup"><span data-stu-id="36432-171">To configure single sign-on on **SECURE DELIVER** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com).</span></span> <span data-ttu-id="36432-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="36432-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="36432-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="36432-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="36432-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="36432-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="36432-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36432-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36432-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="36432-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="36432-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36432-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="36432-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36432-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="36432-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="36432-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/securedeliver-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="36432-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="36432-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/securedeliver-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="36432-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="36432-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/securedeliver-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="36432-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="36432-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/securedeliver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36432-188">a.</span><span class="sxs-lookup"><span data-stu-id="36432-188">a.</span></span> <span data-ttu-id="36432-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36432-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36432-190">b.</span><span class="sxs-lookup"><span data-stu-id="36432-190">b.</span></span> <span data-ttu-id="36432-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="36432-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36432-192">c.</span><span class="sxs-lookup"><span data-stu-id="36432-192">c.</span></span> <span data-ttu-id="36432-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="36432-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="36432-194">d.</span><span class="sxs-lookup"><span data-stu-id="36432-194">d.</span></span> <span data-ttu-id="36432-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="36432-195">Click **Create**.</span></span>
 
### <a name="creating-a-secure-deliver-test-user"></a><span data-ttu-id="36432-196">Creating a SECURE DELIVER test user</span><span class="sxs-lookup"><span data-stu-id="36432-196">Creating a SECURE DELIVER test user</span></span>

<span data-ttu-id="36432-197">The objective of this section is to create a user called Britta Simon in SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="36432-197">The objective of this section is to create a user called Britta Simon in SECURE DELIVER.</span></span> <span data-ttu-id="36432-198">Work with [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com) to add the users in the SECURE DELIVER account.</span><span class="sxs-lookup"><span data-stu-id="36432-198">Work with [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com) to add the users in the SECURE DELIVER account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="36432-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="36432-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="36432-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="36432-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SECURE DELIVER.</span></span>

![Assign User][200] 

<span data-ttu-id="36432-202">**To assign Britta Simon to SECURE DELIVER, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36432-202">**To assign Britta Simon to SECURE DELIVER, perform the following steps:**</span></span>

1. <span data-ttu-id="36432-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="36432-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="36432-205">In the applications list, select **SECURE DELIVER**.</span><span class="sxs-lookup"><span data-stu-id="36432-205">In the applications list, select **SECURE DELIVER**.</span></span>

    ![Configure Single Sign-On](./media/securedeliver-tutorial/tutorial_securedeliver_app.png) 

1. <span data-ttu-id="36432-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="36432-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="36432-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="36432-209">Click **Add** button.</span></span> <span data-ttu-id="36432-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="36432-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="36432-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="36432-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="36432-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="36432-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="36432-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="36432-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="36432-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="36432-215">Testing single sign-on</span></span>

<span data-ttu-id="36432-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="36432-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="36432-217">When you click the SECURE DELIVER tile in the Access Panel, you should get automatically signed-on to your SECURE DELIVER application.</span><span class="sxs-lookup"><span data-stu-id="36432-217">When you click the SECURE DELIVER tile in the Access Panel, you should get automatically signed-on to your SECURE DELIVER application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="36432-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="36432-218">Additional resources</span></span>

* [<span data-ttu-id="36432-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36432-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="36432-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="36432-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/securedeliver-tutorial/tutorial_general_01.png
[2]: ./media/securedeliver-tutorial/tutorial_general_02.png
[3]: ./media/securedeliver-tutorial/tutorial_general_03.png
[4]: ./media/securedeliver-tutorial/tutorial_general_04.png

[100]: ./media/securedeliver-tutorial/tutorial_general_100.png

[200]: ./media/securedeliver-tutorial/tutorial_general_200.png
[201]: ./media/securedeliver-tutorial/tutorial_general_201.png
[202]: ./media/securedeliver-tutorial/tutorial_general_202.png
[203]: ./media/securedeliver-tutorial/tutorial_general_203.png

