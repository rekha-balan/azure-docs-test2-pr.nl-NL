---
title: 'Tutorial: Azure Active Directory integration with Yardi eLearning | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Yardi eLearning.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 7ea58b54-ec5b-4576-8586-814b11d0f4fb
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 9a6bbb716957621daf4667a7e819c31eeedaa53a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967733"
---
# <a name="tutorial-azure-active-directory-integration-with-yardi-elearning"></a><span data-ttu-id="06b05-103">Tutorial: Azure Active Directory integration with Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="06b05-103">Tutorial: Azure Active Directory integration with Yardi eLearning</span></span>

<span data-ttu-id="06b05-104">In this tutorial, you learn how to integrate Yardi eLearning with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="06b05-104">In this tutorial, you learn how to integrate Yardi eLearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06b05-105">Integrating Yardi eLearning with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="06b05-105">Integrating Yardi eLearning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="06b05-106">You can control in Azure AD who has access to Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="06b05-106">You can control in Azure AD who has access to Yardi eLearning</span></span>
- <span data-ttu-id="06b05-107">You can enable your users to automatically get signed-on to Yardi eLearning (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="06b05-107">You can enable your users to automatically get signed-on to Yardi eLearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="06b05-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="06b05-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="06b05-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="06b05-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06b05-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="06b05-110">Prerequisites</span></span>

<span data-ttu-id="06b05-111">To configure Azure AD integration with Yardi eLearning, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="06b05-111">To configure Azure AD integration with Yardi eLearning, you need the following items:</span></span>

- <span data-ttu-id="06b05-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="06b05-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06b05-113">A Yardi eLearning single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="06b05-113">A Yardi eLearning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06b05-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="06b05-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06b05-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="06b05-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06b05-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="06b05-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06b05-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06b05-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06b05-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="06b05-118">Scenario description</span></span>
<span data-ttu-id="06b05-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="06b05-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06b05-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="06b05-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06b05-121">Adding Yardi eLearning from the gallery</span><span class="sxs-lookup"><span data-stu-id="06b05-121">Adding Yardi eLearning from the gallery</span></span>
1. <span data-ttu-id="06b05-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="06b05-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yardi-elearning-from-the-gallery"></a><span data-ttu-id="06b05-123">Adding Yardi eLearning from the gallery</span><span class="sxs-lookup"><span data-stu-id="06b05-123">Adding Yardi eLearning from the gallery</span></span>
<span data-ttu-id="06b05-124">To configure the integration of Yardi eLearning into Azure AD, you need to add Yardi eLearning from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="06b05-124">To configure the integration of Yardi eLearning into Azure AD, you need to add Yardi eLearning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="06b05-125">**To add Yardi eLearning from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06b05-125">**To add Yardi eLearning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="06b05-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="06b05-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="06b05-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="06b05-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="06b05-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="06b05-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="06b05-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="06b05-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="06b05-133">In the search box, type **Yardi eLearning**.</span><span class="sxs-lookup"><span data-stu-id="06b05-133">In the search box, type **Yardi eLearning**.</span></span>

    ![Creating an Azure AD test user](./media/yardielearning-tutorial/tutorial_yardielearning_search.png)

1. <span data-ttu-id="06b05-135">In the results panel, select **Yardi eLearning**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="06b05-135">In the results panel, select **Yardi eLearning**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/yardielearning-tutorial/tutorial_yardielearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="06b05-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="06b05-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="06b05-138">In this section, you configure and test Azure AD single sign-on with Yardi eLearning based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="06b05-138">In this section, you configure and test Azure AD single sign-on with Yardi eLearning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="06b05-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Yardi eLearning is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06b05-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Yardi eLearning is to a user in Azure AD.</span></span> <span data-ttu-id="06b05-140">In other words, a link relationship between an Azure AD user and the related user in Yardi eLearning needs to be established.</span><span class="sxs-lookup"><span data-stu-id="06b05-140">In other words, a link relationship between an Azure AD user and the related user in Yardi eLearning needs to be established.</span></span>

<span data-ttu-id="06b05-141">In Yardi eLearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="06b05-141">In Yardi eLearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="06b05-142">To configure and test Azure AD single sign-on with Yardi eLearning, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="06b05-142">To configure and test Azure AD single sign-on with Yardi eLearning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="06b05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="06b05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="06b05-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06b05-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="06b05-145">**[Creating a Yardi eLearning test user](#creating-a-yardi-elearning-test-user)** - to have a counterpart of Britta Simon in Yardi eLearning that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="06b05-145">**[Creating a Yardi eLearning test user](#creating-a-yardi-elearning-test-user)** - to have a counterpart of Britta Simon in Yardi eLearning that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="06b05-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="06b05-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="06b05-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="06b05-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="06b05-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="06b05-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="06b05-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yardi eLearning application.</span><span class="sxs-lookup"><span data-stu-id="06b05-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yardi eLearning application.</span></span>

<span data-ttu-id="06b05-150">**To configure Azure AD single sign-on with Yardi eLearning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06b05-150">**To configure Azure AD single sign-on with Yardi eLearning, perform the following steps:**</span></span>

1. <span data-ttu-id="06b05-151">In the Azure portal, on the **Yardi eLearning** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="06b05-151">In the Azure portal, on the **Yardi eLearning** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="06b05-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="06b05-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/yardielearning-tutorial/tutorial_yardielearning_samlbase.png)

1. <span data-ttu-id="06b05-155">On the **Yardi eLearning Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="06b05-155">On the **Yardi eLearning Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/yardielearning-tutorial/tutorial_yardielearning_url.png)

    <span data-ttu-id="06b05-157">a.</span><span class="sxs-lookup"><span data-stu-id="06b05-157">a.</span></span> <span data-ttu-id="06b05-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.yardielearning.com/login`</span><span class="sxs-lookup"><span data-stu-id="06b05-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.yardielearning.com/login`</span></span>

    <span data-ttu-id="06b05-159">b.</span><span class="sxs-lookup"><span data-stu-id="06b05-159">b.</span></span> <span data-ttu-id="06b05-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.yardielearning.com/trust`</span><span class="sxs-lookup"><span data-stu-id="06b05-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.yardielearning.com/trust`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="06b05-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="06b05-161">These values are not real.</span></span> <span data-ttu-id="06b05-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="06b05-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="06b05-163">Contact [Yardi eLearning Client support team](mailto:elearning@yardi.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="06b05-163">Contact [Yardi eLearning Client support team](mailto:elearning@yardi.com) to get these values.</span></span> 
 
1. <span data-ttu-id="06b05-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="06b05-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/yardielearning-tutorial/tutorial_yardielearning_certificate.png) 

1. <span data-ttu-id="06b05-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="06b05-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/yardielearning-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="06b05-168">To configure single sign-on on **Yardi eLearning** side, you need to send the downloaded **Metadata XML** to [Yardi eLearning support team](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="06b05-168">To configure single sign-on on **Yardi eLearning** side, you need to send the downloaded **Metadata XML** to [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span> 

> [!TIP]
> <span data-ttu-id="06b05-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="06b05-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="06b05-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="06b05-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="06b05-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06b05-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="06b05-172">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="06b05-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="06b05-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06b05-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="06b05-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06b05-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="06b05-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="06b05-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/yardielearning-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="06b05-178">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="06b05-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/yardielearning-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="06b05-180">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="06b05-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/yardielearning-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="06b05-182">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="06b05-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/yardielearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="06b05-184">a.</span><span class="sxs-lookup"><span data-stu-id="06b05-184">a.</span></span> <span data-ttu-id="06b05-185">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="06b05-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06b05-186">b.</span><span class="sxs-lookup"><span data-stu-id="06b05-186">b.</span></span> <span data-ttu-id="06b05-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="06b05-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="06b05-188">c.</span><span class="sxs-lookup"><span data-stu-id="06b05-188">c.</span></span> <span data-ttu-id="06b05-189">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="06b05-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="06b05-190">d.</span><span class="sxs-lookup"><span data-stu-id="06b05-190">d.</span></span> <span data-ttu-id="06b05-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="06b05-191">Click **Create**.</span></span>
 
### <a name="creating-a-yardi-elearning-test-user"></a><span data-ttu-id="06b05-192">Creating a Yardi eLearning test user</span><span class="sxs-lookup"><span data-stu-id="06b05-192">Creating a Yardi eLearning test user</span></span>

<span data-ttu-id="06b05-193">The objective of this section is to create a user called Britta Simon in Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="06b05-193">The objective of this section is to create a user called Britta Simon in Yardi eLearning.</span></span> <span data-ttu-id="06b05-194">Yardi eLearning supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="06b05-194">Yardi eLearning supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="06b05-195">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="06b05-195">There is no action item for you in this section.</span></span> <span data-ttu-id="06b05-196">A new user is created during an attempt to access Yardi eLearning if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="06b05-196">A new user is created during an attempt to access Yardi eLearning if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="06b05-197">If you need to create a user manually, you need to contact the [Yardi eLearning support team](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="06b05-197">If you need to create a user manually, you need to contact the [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="06b05-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="06b05-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="06b05-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="06b05-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yardi eLearning.</span></span>

![Assign User][200] 

<span data-ttu-id="06b05-201">**To assign Britta Simon to Yardi eLearning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06b05-201">**To assign Britta Simon to Yardi eLearning, perform the following steps:**</span></span>

1. <span data-ttu-id="06b05-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="06b05-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="06b05-204">In the applications list, select **Yardi eLearning**.</span><span class="sxs-lookup"><span data-stu-id="06b05-204">In the applications list, select **Yardi eLearning**.</span></span>

    ![Configure Single Sign-On](./media/yardielearning-tutorial/tutorial_yardielearning_app.png) 

1. <span data-ttu-id="06b05-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="06b05-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="06b05-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="06b05-208">Click **Add** button.</span></span> <span data-ttu-id="06b05-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="06b05-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="06b05-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="06b05-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="06b05-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="06b05-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="06b05-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="06b05-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="06b05-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="06b05-214">Testing single sign-on</span></span>

<span data-ttu-id="06b05-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="06b05-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="06b05-216">When you click the Yardi eLearning tile in the Access Panel, you should get automatically signed-on to your Yardi eLearning application.</span><span class="sxs-lookup"><span data-stu-id="06b05-216">When you click the Yardi eLearning tile in the Access Panel, you should get automatically signed-on to your Yardi eLearning application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="06b05-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="06b05-217">Additional resources</span></span>

* [<span data-ttu-id="06b05-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06b05-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="06b05-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="06b05-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/yardielearning-tutorial/tutorial_general_01.png
[2]: ./media/yardielearning-tutorial/tutorial_general_02.png
[3]: ./media/yardielearning-tutorial/tutorial_general_03.png
[4]: ./media/yardielearning-tutorial/tutorial_general_04.png

[100]: ./media/yardielearning-tutorial/tutorial_general_100.png

[200]: ./media/yardielearning-tutorial/tutorial_general_200.png
[201]: ./media/yardielearning-tutorial/tutorial_general_201.png
[202]: ./media/yardielearning-tutorial/tutorial_general_202.png
[203]: ./media/yardielearning-tutorial/tutorial_general_203.png

