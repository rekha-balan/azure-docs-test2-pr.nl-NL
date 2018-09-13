---
title: 'Tutorial: Azure Active Directory integration with Capriza Platform | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Capriza Platform.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 78b459b3b2c3f29c0e8b93a1f20e21c125c53b97
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867398"
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="3cbf6-103">Tutorial: Azure Active Directory integration with Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="3cbf6-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="3cbf6-104">In this tutorial, you learn how to integrate Capriza Platform with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3cbf6-104">In this tutorial, you learn how to integrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cbf6-105">Integrating Capriza Platform with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3cbf6-105">Integrating Capriza Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3cbf6-106">You can control in Azure AD who has access to Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="3cbf6-106">You can control in Azure AD who has access to Capriza Platform</span></span>
- <span data-ttu-id="3cbf6-107">You can enable your users to automatically get signed-on to Capriza Platform (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="3cbf6-107">You can enable your users to automatically get signed-on to Capriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3cbf6-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3cbf6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3cbf6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3cbf6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cbf6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3cbf6-110">Prerequisites</span></span>

<span data-ttu-id="3cbf6-111">To configure Azure AD integration with Capriza Platform, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3cbf6-111">To configure Azure AD integration with Capriza Platform, you need the following items:</span></span>

- <span data-ttu-id="3cbf6-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3cbf6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3cbf6-113">A Capriza Platform single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3cbf6-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3cbf6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3cbf6-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3cbf6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3cbf6-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3cbf6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cbf6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cbf6-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3cbf6-118">Scenario description</span></span>
<span data-ttu-id="3cbf6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3cbf6-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3cbf6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3cbf6-121">Adding Capriza Platform from the gallery</span><span class="sxs-lookup"><span data-stu-id="3cbf6-121">Adding Capriza Platform from the gallery</span></span>
1. <span data-ttu-id="3cbf6-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cbf6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-the-gallery"></a><span data-ttu-id="3cbf6-123">Adding Capriza Platform from the gallery</span><span class="sxs-lookup"><span data-stu-id="3cbf6-123">Adding Capriza Platform from the gallery</span></span>
<span data-ttu-id="3cbf6-124">To configure the integration of Capriza Platform into Azure AD, you need to add Capriza Platform from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-124">To configure the integration of Capriza Platform into Azure AD, you need to add Capriza Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3cbf6-125">**To add Capriza Platform from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cbf6-125">**To add Capriza Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3cbf6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="3cbf6-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3cbf6-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="3cbf6-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="3cbf6-133">In the search box, type **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-133">In the search box, type **Capriza Platform**.</span></span>

    ![Creating an Azure AD test user](./media/capriza-tutorial/tutorial_caprizaplatform_search.png)

1. <span data-ttu-id="3cbf6-135">In the results panel, select **Capriza Platform**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-135">In the results panel, select **Capriza Platform**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3cbf6-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cbf6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3cbf6-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3cbf6-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3cbf6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Capriza Platform is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Capriza Platform is to a user in Azure AD.</span></span> <span data-ttu-id="3cbf6-140">In other words, a link relationship between an Azure AD user and the related user in Capriza Platform needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-140">In other words, a link relationship between an Azure AD user and the related user in Capriza Platform needs to be established.</span></span>

<span data-ttu-id="3cbf6-141">In Capriza Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-141">In Capriza Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3cbf6-142">To configure and test Azure AD single sign-on with Capriza Platform, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3cbf6-142">To configure and test Azure AD single sign-on with Capriza Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3cbf6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="3cbf6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="3cbf6-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - to have a counterpart of Britta Simon in Capriza Platform that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - to have a counterpart of Britta Simon in Capriza Platform that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="3cbf6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="3cbf6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3cbf6-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cbf6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3cbf6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Capriza Platform application.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="3cbf6-150">**To configure Azure AD single sign-on with Capriza Platform, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cbf6-150">**To configure Azure AD single sign-on with Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="3cbf6-151">In the Azure portal, on the **Capriza Platform** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-151">In the Azure portal, on the **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="3cbf6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

1. <span data-ttu-id="3cbf6-155">On the **Capriza Platform Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3cbf6-155">On the **Capriza Platform Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="3cbf6-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="3cbf6-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3cbf6-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-158">This value is not real.</span></span> <span data-ttu-id="3cbf6-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3cbf6-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) to get this value.</span></span> 

1. <span data-ttu-id="3cbf6-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

1. <span data-ttu-id="3cbf6-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/capriza-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="3cbf6-165">On the **Capriza Platform Configuration** section, click **Configure Capriza Platform** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-165">On the **Capriza Platform Configuration** section, click **Configure Capriza Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3cbf6-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="3cbf6-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/capriza-tutorial/tutorial_caprizaplatform_configure.png) 

1. <span data-ttu-id="3cbf6-168">To configure single sign-on on **Capriza Platform** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Capriza Platform support team](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="3cbf6-168">To configure single sign-on on **Capriza Platform** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="3cbf6-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3cbf6-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="3cbf6-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3cbf6-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3cbf6-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3cbf6-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3cbf6-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3cbf6-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="3cbf6-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="3cbf6-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cbf6-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3cbf6-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/capriza-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="3cbf6-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/capriza-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="3cbf6-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/capriza-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="3cbf6-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3cbf6-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3cbf6-185">a.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-185">a.</span></span> <span data-ttu-id="3cbf6-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3cbf6-187">b.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-187">b.</span></span> <span data-ttu-id="3cbf6-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3cbf6-189">c.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-189">c.</span></span> <span data-ttu-id="3cbf6-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3cbf6-191">d.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-191">d.</span></span> <span data-ttu-id="3cbf6-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="3cbf6-193">Creating a Capriza Platform test user</span><span class="sxs-lookup"><span data-stu-id="3cbf6-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="3cbf6-194">The objective of this section is to create a user called Britta Simon in Capriza.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-194">The objective of this section is to create a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="3cbf6-195">Capriza supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="3cbf6-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only the just-in-time user provisioning will work.**</span><span class="sxs-lookup"><span data-stu-id="3cbf6-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only the just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="3cbf6-197">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-197">There is no action item for you in this section.</span></span> <span data-ttu-id="3cbf6-198">A new user will be created during an attempt to access Capriza if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-198">A new user will be created during an attempt to access Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3cbf6-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3cbf6-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3cbf6-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Capriza Platform.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Capriza Platform.</span></span>

![Assign User][200] 

<span data-ttu-id="3cbf6-202">**To assign Britta Simon to Capriza Platform, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cbf6-202">**To assign Britta Simon to Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="3cbf6-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="3cbf6-205">In the applications list, select **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-205">In the applications list, select **Capriza Platform**.</span></span>

    ![Configure Single Sign-On](./media/capriza-tutorial/tutorial_caprizaplatform_app.png) 

1. <span data-ttu-id="3cbf6-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="3cbf6-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-209">Click **Add** button.</span></span> <span data-ttu-id="3cbf6-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="3cbf6-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="3cbf6-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="3cbf6-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3cbf6-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cbf6-215">Testing single sign-on</span></span>

<span data-ttu-id="3cbf6-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3cbf6-217">When you click the Capriza Platform tile in the Access Panel, you should get automatically signed-on to your Capriza application.</span><span class="sxs-lookup"><span data-stu-id="3cbf6-217">When you click the Capriza Platform tile in the Access Panel, you should get automatically signed-on to your Capriza application.</span></span> <span data-ttu-id="3cbf6-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3cbf6-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3cbf6-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3cbf6-219">Additional resources</span></span>

* [<span data-ttu-id="3cbf6-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3cbf6-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3cbf6-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3cbf6-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/capriza-tutorial/tutorial_general_01.png
[2]: ./media/capriza-tutorial/tutorial_general_02.png
[3]: ./media/capriza-tutorial/tutorial_general_03.png
[4]: ./media/capriza-tutorial/tutorial_general_04.png

[100]: ./media/capriza-tutorial/tutorial_general_100.png

[200]: ./media/capriza-tutorial/tutorial_general_200.png
[201]: ./media/capriza-tutorial/tutorial_general_201.png
[202]: ./media/capriza-tutorial/tutorial_general_202.png
[203]: ./media/capriza-tutorial/tutorial_general_203.png

