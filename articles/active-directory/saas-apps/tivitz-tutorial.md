---
title: 'Tutorial: Azure Active Directory integration with TiViTz | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TiViTz.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: b97ed88f-7888-4185-be22-41d1f62cbbf1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9b997b198c526aec5dfc64c33969008988c1abff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856882"
---
# <a name="tutorial-azure-active-directory-integration-with-tivitz"></a><span data-ttu-id="4b1c9-103">Tutorial: Azure Active Directory integration with TiViTz</span><span class="sxs-lookup"><span data-stu-id="4b1c9-103">Tutorial: Azure Active Directory integration with TiViTz</span></span>

<span data-ttu-id="4b1c9-104">In this tutorial, you learn how to integrate TiViTz with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b1c9-104">In this tutorial, you learn how to integrate TiViTz with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b1c9-105">Integrating TiViTz with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4b1c9-105">Integrating TiViTz with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b1c9-106">You can control in Azure AD who has access to TiViTz</span><span class="sxs-lookup"><span data-stu-id="4b1c9-106">You can control in Azure AD who has access to TiViTz</span></span>
- <span data-ttu-id="4b1c9-107">You can enable your users to automatically get signed-on to TiViTz (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4b1c9-107">You can enable your users to automatically get signed-on to TiViTz (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b1c9-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4b1c9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4b1c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4b1c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b1c9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4b1c9-110">Prerequisites</span></span>

<span data-ttu-id="4b1c9-111">To configure Azure AD integration with TiViTz, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4b1c9-111">To configure Azure AD integration with TiViTz, you need the following items:</span></span>

- <span data-ttu-id="4b1c9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4b1c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b1c9-113">A TiViTz single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4b1c9-113">A TiViTz single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b1c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b1c9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4b1c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b1c9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b1c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b1c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b1c9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4b1c9-118">Scenario description</span></span>
<span data-ttu-id="4b1c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b1c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4b1c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b1c9-121">Adding TiViTz from the gallery</span><span class="sxs-lookup"><span data-stu-id="4b1c9-121">Adding TiViTz from the gallery</span></span>
1. <span data-ttu-id="4b1c9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4b1c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tivitz-from-the-gallery"></a><span data-ttu-id="4b1c9-123">Adding TiViTz from the gallery</span><span class="sxs-lookup"><span data-stu-id="4b1c9-123">Adding TiViTz from the gallery</span></span>
<span data-ttu-id="4b1c9-124">To configure the integration of TiViTz into Azure AD, you need to add TiViTz from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-124">To configure the integration of TiViTz into Azure AD, you need to add TiViTz from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b1c9-125">**To add TiViTz from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4b1c9-125">**To add TiViTz from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4b1c9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4b1c9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="4b1c9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4b1c9-133">In the search box, type **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-133">In the search box, type **TiViTz**.</span></span>

    ![Creating an Azure AD test user](./media/tivitz-tutorial/tutorial_tivitz_search.png)

1. <span data-ttu-id="4b1c9-135">In the results panel, select **TiViTz**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-135">In the results panel, select **TiViTz**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/tivitz-tutorial/tutorial_tivitz_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b1c9-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4b1c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b1c9-138">In this section, you configure and test Azure AD single sign-on with TiViTz based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4b1c9-138">In this section, you configure and test Azure AD single sign-on with TiViTz based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b1c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TiViTz is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TiViTz is to a user in Azure AD.</span></span> <span data-ttu-id="4b1c9-140">In other words, a link relationship between an Azure AD user and the related user in TiViTz needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-140">In other words, a link relationship between an Azure AD user and the related user in TiViTz needs to be established.</span></span>

<span data-ttu-id="4b1c9-141">In TiViTz, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-141">In TiViTz, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4b1c9-142">To configure and test Azure AD single sign-on with TiViTz, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4b1c9-142">To configure and test Azure AD single sign-on with TiViTz, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b1c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4b1c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4b1c9-145">**[Creating a TiViTz test user](#creating-a-tivitz-test-user)** - to have a counterpart of Britta Simon in TiViTz that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-145">**[Creating a TiViTz test user](#creating-a-tivitz-test-user)** - to have a counterpart of Britta Simon in TiViTz that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4b1c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4b1c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b1c9-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4b1c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b1c9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TiViTz application.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TiViTz application.</span></span>

<span data-ttu-id="4b1c9-150">**To configure Azure AD single sign-on with TiViTz, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4b1c9-150">**To configure Azure AD single sign-on with TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1c9-151">In the Azure portal, on the **TiViTz** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-151">In the Azure portal, on the **TiViTz** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4b1c9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/tivitz-tutorial/tutorial_tivitz_samlbase.png)

1. <span data-ttu-id="4b1c9-155">On the **TiViTz Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b1c9-155">On the **TiViTz Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/tivitz-tutorial/tutorial_tivitz_url.png)

    <span data-ttu-id="4b1c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-157">a.</span></span> <span data-ttu-id="4b1c9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="4b1c9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    <span data-ttu-id="4b1c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-159">b.</span></span> <span data-ttu-id="4b1c9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="4b1c9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b1c9-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-161">These values are not real.</span></span> <span data-ttu-id="4b1c9-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4b1c9-163">Contact [TiViTz Client support team](mailto:info@tivitz.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-163">Contact [TiViTz Client support team](mailto:info@tivitz.com) to get these values.</span></span> 

1. <span data-ttu-id="4b1c9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/tivitz-tutorial/tutorial_tivitz_certificate.png) 

1. <span data-ttu-id="4b1c9-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/tivitz-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4b1c9-168">To configure single sign-on on **TiViTz** side, you need to send the downloaded **Metadata XML** to [TiViTz support team](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="4b1c9-168">To configure single sign-on on **TiViTz** side, you need to send the downloaded **Metadata XML** to [TiViTz support team](mailto:info@tivitz.com).</span></span>

> [!TIP]
> <span data-ttu-id="4b1c9-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4b1c9-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4b1c9-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4b1c9-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b1c9-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b1c9-172">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4b1c9-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b1c9-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4b1c9-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4b1c9-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1c9-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/tivitz-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="4b1c9-178">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/tivitz-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4b1c9-180">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/tivitz-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4b1c9-182">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b1c9-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/tivitz-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b1c9-184">a.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-184">a.</span></span> <span data-ttu-id="4b1c9-185">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b1c9-186">b.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-186">b.</span></span> <span data-ttu-id="4b1c9-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b1c9-188">c.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-188">c.</span></span> <span data-ttu-id="4b1c9-189">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4b1c9-190">d.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-190">d.</span></span> <span data-ttu-id="4b1c9-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-191">Click **Create**.</span></span>
 
### <a name="creating-a-tivitz-test-user"></a><span data-ttu-id="4b1c9-192">Creating a TiViTz test user</span><span class="sxs-lookup"><span data-stu-id="4b1c9-192">Creating a TiViTz test user</span></span>

<span data-ttu-id="4b1c9-193">The objective of this section is to create a user called Britta Simon in TiViTz.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-193">The objective of this section is to create a user called Britta Simon in TiViTz.</span></span> <span data-ttu-id="4b1c9-194">TiViTz supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-194">TiViTz supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="4b1c9-195">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-195">There is no action item for you in this section.</span></span> <span data-ttu-id="4b1c9-196">A new user is created during an attempt to access TiViTz if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-196">A new user is created during an attempt to access TiViTz if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="4b1c9-197">If you need to create an user manually, you need to contact [TiViTz support team](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="4b1c9-197">If you need to create an user manually, you need to contact [TiViTz support team](mailto:info@tivitz.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4b1c9-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4b1c9-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4b1c9-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TiViTz.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TiViTz.</span></span>

![Assign User][200] 

<span data-ttu-id="4b1c9-201">**To assign Britta Simon to TiViTz, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4b1c9-201">**To assign Britta Simon to TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1c9-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4b1c9-204">In the applications list, select **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-204">In the applications list, select **TiViTz**.</span></span>

    ![Configure Single Sign-On](./media/tivitz-tutorial/tutorial_tivitz_app.png) 

1. <span data-ttu-id="4b1c9-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4b1c9-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-208">Click **Add** button.</span></span> <span data-ttu-id="4b1c9-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4b1c9-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4b1c9-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4b1c9-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b1c9-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4b1c9-214">Testing single sign-on</span></span>

<span data-ttu-id="4b1c9-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4b1c9-216">When you click the TiViTz tile in the Access Panel, you should get automatically signed-on to your TiViTz application.</span><span class="sxs-lookup"><span data-stu-id="4b1c9-216">When you click the TiViTz tile in the Access Panel, you should get automatically signed-on to your TiViTz application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b1c9-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4b1c9-217">Additional resources</span></span>

* [<span data-ttu-id="4b1c9-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b1c9-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4b1c9-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b1c9-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/tivitz-tutorial/tutorial_general_01.png
[2]: ./media/tivitz-tutorial/tutorial_general_02.png
[3]: ./media/tivitz-tutorial/tutorial_general_03.png
[4]: ./media/tivitz-tutorial/tutorial_general_04.png

[100]: ./media/tivitz-tutorial/tutorial_general_100.png

[200]: ./media/tivitz-tutorial/tutorial_general_200.png
[201]: ./media/tivitz-tutorial/tutorial_general_201.png
[202]: ./media/tivitz-tutorial/tutorial_general_202.png
[203]: ./media/tivitz-tutorial/tutorial_general_203.png
