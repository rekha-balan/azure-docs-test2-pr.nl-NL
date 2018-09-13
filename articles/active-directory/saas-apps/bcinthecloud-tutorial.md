---
title: 'Tutorial: Azure Active Directory integration with BC in the Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BC in the Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: 5d9d2bb0dc44eab0a419efce0c26a8f30135285e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969070"
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-the-cloud"></a><span data-ttu-id="4c8b2-103">Tutorial: Azure Active Directory integration with BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="4c8b2-103">Tutorial: Azure Active Directory integration with BC in the Cloud</span></span>

<span data-ttu-id="4c8b2-104">In this tutorial, you learn how to integrate BC in the Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c8b2-104">In this tutorial, you learn how to integrate BC in the Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c8b2-105">Integrating BC in the Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4c8b2-105">Integrating BC in the Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c8b2-106">You can control in Azure AD who has access to BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="4c8b2-106">You can control in Azure AD who has access to BC in the Cloud</span></span>
- <span data-ttu-id="4c8b2-107">You can enable your users to automatically get signed-on to BC in the Cloud (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4c8b2-107">You can enable your users to automatically get signed-on to BC in the Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c8b2-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4c8b2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4c8b2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4c8b2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c8b2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4c8b2-110">Prerequisites</span></span>

<span data-ttu-id="4c8b2-111">To configure Azure AD integration with BC in the Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4c8b2-111">To configure Azure AD integration with BC in the Cloud, you need the following items:</span></span>

- <span data-ttu-id="4c8b2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4c8b2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c8b2-113">A BC in the Cloud single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4c8b2-113">A BC in the Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c8b2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c8b2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4c8b2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c8b2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c8b2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c8b2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c8b2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4c8b2-118">Scenario description</span></span>
<span data-ttu-id="4c8b2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c8b2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4c8b2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c8b2-121">Adding BC in the Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="4c8b2-121">Adding BC in the Cloud from the gallery</span></span>
1. <span data-ttu-id="4c8b2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c8b2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-the-cloud-from-the-gallery"></a><span data-ttu-id="4c8b2-123">Adding BC in the Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="4c8b2-123">Adding BC in the Cloud from the gallery</span></span>
<span data-ttu-id="4c8b2-124">To configure the integration of BC in the Cloud into Azure AD, you need to add BC in the Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-124">To configure the integration of BC in the Cloud into Azure AD, you need to add BC in the Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c8b2-125">**To add BC in the Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c8b2-125">**To add BC in the Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c8b2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4c8b2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c8b2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="4c8b2-131">To add new application, click **Add** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-131">To add new application, click **Add** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4c8b2-133">In the search box, type **BC in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-133">In the search box, type **BC in the Cloud**.</span></span>

    ![Creating an Azure AD test user](./media/bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

1. <span data-ttu-id="4c8b2-135">In the results panel, select **BC in the Cloud**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-135">In the results panel, select **BC in the Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c8b2-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c8b2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c8b2-138">In this section, you configure and test Azure AD single sign-on with BC in the Cloud based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4c8b2-138">In this section, you configure and test Azure AD single sign-on with BC in the Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4c8b2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BC in the Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BC in the Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="4c8b2-140">In other words, a link relationship between an Azure AD user and the related user in BC in the Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-140">In other words, a link relationship between an Azure AD user and the related user in BC in the Cloud needs to be established.</span></span>

<span data-ttu-id="4c8b2-141">In BC in the Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-141">In BC in the Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4c8b2-142">To configure and test Azure AD single sign-on with BC in the Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4c8b2-142">To configure and test Azure AD single sign-on with BC in the Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c8b2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4c8b2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4c8b2-145">**[Creating a BC in the Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - to have a counterpart of Britta Simon in BC in the Cloud that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-145">**[Creating a BC in the Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - to have a counterpart of Britta Simon in BC in the Cloud that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4c8b2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4c8b2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c8b2-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c8b2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c8b2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BC in the Cloud application.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BC in the Cloud application.</span></span>

<span data-ttu-id="4c8b2-150">**To configure Azure AD single sign-on with BC in the Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c8b2-150">**To configure Azure AD single sign-on with BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4c8b2-151">In the Azure portal, on the **BC in the Cloud** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-151">In the Azure portal, on the **BC in the Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4c8b2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

1. <span data-ttu-id="4c8b2-155">On the **BC in the Cloud Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4c8b2-155">On the **BC in the Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="4c8b2-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-157">a.</span></span> <span data-ttu-id="4c8b2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="4c8b2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="4c8b2-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-159">b.</span></span> <span data-ttu-id="4c8b2-160">In the **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="4c8b2-160">In the **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c8b2-161">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-161">This value is not real.</span></span> <span data-ttu-id="4c8b2-162">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="4c8b2-163">Contact [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-163">Contact [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to get this value.</span></span> 
 
1. <span data-ttu-id="4c8b2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

1. <span data-ttu-id="4c8b2-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/bcinthecloud-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4c8b2-168">To configure single sign-on on **BC in the Cloud** side, you need to send the downloaded **Metadata XML** to [BC in the Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="4c8b2-168">To configure single sign-on on **BC in the Cloud** side, you need to send the downloaded **Metadata XML** to [BC in the Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="4c8b2-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4c8b2-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4c8b2-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4c8b2-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c8b2-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c8b2-172">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4c8b2-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c8b2-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4c8b2-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c8b2-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c8b2-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/bcinthecloud-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="4c8b2-178">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/bcinthecloud-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4c8b2-180">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/bcinthecloud-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4c8b2-182">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4c8b2-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c8b2-184">a.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-184">a.</span></span> <span data-ttu-id="4c8b2-185">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c8b2-186">b.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-186">b.</span></span> <span data-ttu-id="4c8b2-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c8b2-188">c.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-188">c.</span></span> <span data-ttu-id="4c8b2-189">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c8b2-190">d.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-190">d.</span></span> <span data-ttu-id="4c8b2-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-the-cloud-test-user"></a><span data-ttu-id="4c8b2-192">Creating a BC in the Cloud test user</span><span class="sxs-lookup"><span data-stu-id="4c8b2-192">Creating a BC in the Cloud test user</span></span>

<span data-ttu-id="4c8b2-193">In this section, you create a user called Britta Simon in BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-193">In this section, you create a user called Britta Simon in BC in the Cloud.</span></span> <span data-ttu-id="4c8b2-194">Work with [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add the users in the BC in the Cloud application.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-194">Work with [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add the users in the BC in the Cloud application.</span></span> <span data-ttu-id="4c8b2-195">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c8b2-196">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4c8b2-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c8b2-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BC in the Cloud.</span></span>

![Assign User][200] 

<span data-ttu-id="4c8b2-199">**To assign Britta Simon to BC in the Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c8b2-199">**To assign Britta Simon to BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4c8b2-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4c8b2-202">In the applications list, select **BC in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-202">In the applications list, select **BC in the Cloud**.</span></span>

    ![Configure Single Sign-On](./media/bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

1. <span data-ttu-id="4c8b2-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4c8b2-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-206">Click **Add** button.</span></span> <span data-ttu-id="4c8b2-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4c8b2-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4c8b2-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-210">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4c8b2-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c8b2-212">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c8b2-212">Testing single sign-on</span></span>

<span data-ttu-id="4c8b2-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

 <span data-ttu-id="4c8b2-214">When you click the BC in the Cloud tile in the Access Panel, you should get automatically signed-on to your BC in the Cloud application.</span><span class="sxs-lookup"><span data-stu-id="4c8b2-214">When you click the BC in the Cloud tile in the Access Panel, you should get automatically signed-on to your BC in the Cloud application.</span></span> <span data-ttu-id="4c8b2-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c8b2-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c8b2-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4c8b2-216">Additional resources</span></span>

* [<span data-ttu-id="4c8b2-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c8b2-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4c8b2-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c8b2-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/bcinthecloud-tutorial/tutorial_general_203.png

