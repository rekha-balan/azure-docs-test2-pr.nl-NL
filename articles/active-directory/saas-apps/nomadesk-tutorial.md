---
title: 'Tutorial: Azure Active Directory integration with Nomadesk | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Nomadesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d261b776-b48e-45f0-9722-0297adefabb8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 705ea75665a5868d41b0887cdb11579db23ae076
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866391"
---
# <a name="tutorial-azure-active-directory-integration-with-nomadesk"></a><span data-ttu-id="a3220-103">Tutorial: Azure Active Directory integration with Nomadesk</span><span class="sxs-lookup"><span data-stu-id="a3220-103">Tutorial: Azure Active Directory integration with Nomadesk</span></span>

<span data-ttu-id="a3220-104">In this tutorial, you learn how to integrate Nomadesk with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a3220-104">In this tutorial, you learn how to integrate Nomadesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3220-105">Integrating Nomadesk with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a3220-105">Integrating Nomadesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a3220-106">You can control in Azure AD who has access to Nomadesk</span><span class="sxs-lookup"><span data-stu-id="a3220-106">You can control in Azure AD who has access to Nomadesk</span></span>
- <span data-ttu-id="a3220-107">You can enable your users to automatically get signed-on to Nomadesk (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a3220-107">You can enable your users to automatically get signed-on to Nomadesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a3220-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a3220-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a3220-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a3220-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3220-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a3220-110">Prerequisites</span></span>

<span data-ttu-id="a3220-111">To configure Azure AD integration with Nomadesk, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a3220-111">To configure Azure AD integration with Nomadesk, you need the following items:</span></span>

- <span data-ttu-id="a3220-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a3220-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3220-113">A Nomadesk single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a3220-113">A Nomadesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3220-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a3220-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3220-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a3220-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3220-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a3220-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3220-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3220-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3220-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a3220-118">Scenario description</span></span>
<span data-ttu-id="a3220-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a3220-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3220-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a3220-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3220-121">Adding Nomadesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="a3220-121">Adding Nomadesk from the gallery</span></span>
1. <span data-ttu-id="a3220-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a3220-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nomadesk-from-the-gallery"></a><span data-ttu-id="a3220-123">Adding Nomadesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="a3220-123">Adding Nomadesk from the gallery</span></span>
<span data-ttu-id="a3220-124">To configure the integration of Nomadesk into Azure AD, you need to add Nomadesk from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a3220-124">To configure the integration of Nomadesk into Azure AD, you need to add Nomadesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a3220-125">**To add Nomadesk from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3220-125">**To add Nomadesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a3220-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a3220-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="a3220-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a3220-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a3220-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a3220-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a3220-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a3220-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a3220-133">In the search box, type **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="a3220-133">In the search box, type **Nomadesk**.</span></span>

    ![Creating an Azure AD test user](./media/nomadesk-tutorial/tutorial_nomadesk_search.png)

1. <span data-ttu-id="a3220-135">In the results panel, select **Nomadesk**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a3220-135">In the results panel, select **Nomadesk**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/nomadesk-tutorial/tutorial_nomadesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a3220-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a3220-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a3220-138">In this section, you configure and test Azure AD single sign-on with Nomadesk based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a3220-138">In this section, you configure and test Azure AD single sign-on with Nomadesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a3220-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadesk is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3220-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadesk is to a user in Azure AD.</span></span> <span data-ttu-id="a3220-140">In other words, a link relationship between an Azure AD user and the related user in Nomadesk needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a3220-140">In other words, a link relationship between an Azure AD user and the related user in Nomadesk needs to be established.</span></span>

<span data-ttu-id="a3220-141">In Nomadesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a3220-141">In Nomadesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a3220-142">To configure and test Azure AD single sign-on with Nomadesk, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a3220-142">To configure and test Azure AD single sign-on with Nomadesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a3220-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a3220-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a3220-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3220-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a3220-145">**[Creating a Nomadesk test user](#creating-a-nomadesk-test-user)** - to have a counterpart of Britta Simon in Nomadesk that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a3220-145">**[Creating a Nomadesk test user](#creating-a-nomadesk-test-user)** - to have a counterpart of Britta Simon in Nomadesk that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a3220-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a3220-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a3220-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a3220-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a3220-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a3220-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a3220-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadesk application.</span><span class="sxs-lookup"><span data-stu-id="a3220-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadesk application.</span></span>

<span data-ttu-id="a3220-150">**To configure Azure AD single sign-on with Nomadesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3220-150">**To configure Azure AD single sign-on with Nomadesk, perform the following steps:**</span></span>

1. <span data-ttu-id="a3220-151">In the Azure portal, on the **Nomadesk** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a3220-151">In the Azure portal, on the **Nomadesk** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a3220-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a3220-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/nomadesk-tutorial/tutorial_nomadesk_samlbase.png)

1. <span data-ttu-id="a3220-155">On the **Nomadesk Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a3220-155">On the **Nomadesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/nomadesk-tutorial/tutorial_nomadesk_url.png)

    <span data-ttu-id="a3220-157">a.</span><span class="sxs-lookup"><span data-stu-id="a3220-157">a.</span></span> <span data-ttu-id="a3220-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mynomadesk.com/logon/saml/<TENANTID>`</span><span class="sxs-lookup"><span data-stu-id="a3220-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mynomadesk.com/logon/saml/<TENANTID>`</span></span>

    <span data-ttu-id="a3220-159">b.</span><span class="sxs-lookup"><span data-stu-id="a3220-159">b.</span></span> <span data-ttu-id="a3220-160">In the **Identifier** textbox, type a URL using the following pattern: `https://secure.nomadesk.com/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="a3220-160">In the **Identifier** textbox, type a URL using the following pattern: `https://secure.nomadesk.com/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a3220-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a3220-161">These values are not real.</span></span> <span data-ttu-id="a3220-162">Update these values with the actual Sign-on URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="a3220-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="a3220-163">Contact [Nomadesk Client support team](mailto:support@nomadesk.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a3220-163">Contact [Nomadesk Client support team](mailto:support@nomadesk.com) to get these values.</span></span> 
 
1. <span data-ttu-id="a3220-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a3220-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/nomadesk-tutorial/tutorial_nomadesk_certificate.png) 

1. <span data-ttu-id="a3220-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a3220-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/nomadesk-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a3220-168">On the **Nomadesk Configuration** section, click **Configure Nomadesk** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a3220-168">On the **Nomadesk Configuration** section, click **Configure Nomadesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a3220-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a3220-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/nomadesk-tutorial/tutorial_nomadesk_configure.png) 

1. <span data-ttu-id="a3220-171">To configure single sign-on on **Nomadesk** side, you need to send the downloaded **Certificate**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Nomadesk support team](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="a3220-171">To configure single sign-on on **Nomadesk** side, you need to send the downloaded **Certificate**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Nomadesk support team](mailto:support@nomadesk.com).</span></span> <span data-ttu-id="a3220-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a3220-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a3220-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a3220-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a3220-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a3220-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a3220-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a3220-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a3220-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a3220-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="a3220-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3220-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a3220-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3220-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a3220-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a3220-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/nomadesk-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a3220-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a3220-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/nomadesk-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a3220-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a3220-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/nomadesk-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="a3220-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a3220-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/nomadesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a3220-188">a.</span><span class="sxs-lookup"><span data-stu-id="a3220-188">a.</span></span> <span data-ttu-id="a3220-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a3220-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3220-190">b.</span><span class="sxs-lookup"><span data-stu-id="a3220-190">b.</span></span> <span data-ttu-id="a3220-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a3220-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a3220-192">c.</span><span class="sxs-lookup"><span data-stu-id="a3220-192">c.</span></span> <span data-ttu-id="a3220-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a3220-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a3220-194">d.</span><span class="sxs-lookup"><span data-stu-id="a3220-194">d.</span></span> <span data-ttu-id="a3220-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a3220-195">Click **Create**.</span></span>
 
### <a name="creating-a-nomadesk-test-user"></a><span data-ttu-id="a3220-196">Creating a Nomadesk test user</span><span class="sxs-lookup"><span data-stu-id="a3220-196">Creating a Nomadesk test user</span></span>

<span data-ttu-id="a3220-197">The objective of this section is to create a user called Britta Simon in Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="a3220-197">The objective of this section is to create a user called Britta Simon in Nomadesk.</span></span> <span data-ttu-id="a3220-198">Nomadesk supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="a3220-198">Nomadesk supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a3220-199">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="a3220-199">There is no action item for you in this section.</span></span> <span data-ttu-id="a3220-200">A new user is created during an attempt to access Nomadesk if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="a3220-200">A new user is created during an attempt to access Nomadesk if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a3220-201">If you need to create a user manually, you need to contact the [Nomadesk support team](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="a3220-201">If you need to create a user manually, you need to contact the [Nomadesk support team](mailto:support@nomadesk.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a3220-202">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a3220-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a3220-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="a3220-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadesk.</span></span>

![Assign User][200] 

<span data-ttu-id="a3220-205">**To assign Britta Simon to Nomadesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3220-205">**To assign Britta Simon to Nomadesk, perform the following steps:**</span></span>

1. <span data-ttu-id="a3220-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a3220-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a3220-208">In the applications list, select **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="a3220-208">In the applications list, select **Nomadesk**.</span></span>

    ![Configure Single Sign-On](./media/nomadesk-tutorial/tutorial_nomadesk_app.png) 

1. <span data-ttu-id="a3220-210">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a3220-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="a3220-212">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a3220-212">Click **Add** button.</span></span> <span data-ttu-id="a3220-213">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a3220-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a3220-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a3220-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a3220-216">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a3220-216">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a3220-217">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a3220-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a3220-218">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a3220-218">Testing single sign-on</span></span>

<span data-ttu-id="a3220-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a3220-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a3220-220">When you click the Nomadesk tile in the Access Panel,  you should get automatically signed-on to your Nomadesk application.</span><span class="sxs-lookup"><span data-stu-id="a3220-220">When you click the Nomadesk tile in the Access Panel,  you should get automatically signed-on to your Nomadesk application.</span></span>
<span data-ttu-id="a3220-221">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a3220-221">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3220-222">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a3220-222">Additional resources</span></span>

* [<span data-ttu-id="a3220-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3220-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a3220-224">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3220-224">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/nomadesk-tutorial/tutorial_general_01.png
[2]: ./media/nomadesk-tutorial/tutorial_general_02.png
[3]: ./media/nomadesk-tutorial/tutorial_general_03.png
[4]: ./media/nomadesk-tutorial/tutorial_general_04.png

[100]: ./media/nomadesk-tutorial/tutorial_general_100.png

[200]: ./media/nomadesk-tutorial/tutorial_general_200.png
[201]: ./media/nomadesk-tutorial/tutorial_general_201.png
[202]: ./media/nomadesk-tutorial/tutorial_general_202.png
[203]: ./media/nomadesk-tutorial/tutorial_general_203.png

