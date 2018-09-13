---
title: 'Tutorial: Azure Active Directory integration with SimpleNexus | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SimpleNexus.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 89821a05-88e2-4579-b144-0123b2b9cb95
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 25379fd5ecc4c3aa129e9ae7e6cd8049be794150
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868212"
---
# <a name="tutorial-azure-active-directory-integration-with-simplenexus"></a><span data-ttu-id="7a42e-103">Tutorial: Azure Active Directory integration with SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="7a42e-103">Tutorial: Azure Active Directory integration with SimpleNexus</span></span>

<span data-ttu-id="7a42e-104">In this tutorial, you learn how to integrate SimpleNexus with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a42e-104">In this tutorial, you learn how to integrate SimpleNexus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a42e-105">Integrating SimpleNexus with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7a42e-105">Integrating SimpleNexus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7a42e-106">You can control in Azure AD who has access to SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="7a42e-106">You can control in Azure AD who has access to SimpleNexus</span></span>
- <span data-ttu-id="7a42e-107">You can enable your users to automatically get signed-on to SimpleNexus (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7a42e-107">You can enable your users to automatically get signed-on to SimpleNexus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a42e-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7a42e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7a42e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7a42e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a42e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a42e-110">Prerequisites</span></span>

<span data-ttu-id="7a42e-111">To configure Azure AD integration with SimpleNexus, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7a42e-111">To configure Azure AD integration with SimpleNexus, you need the following items:</span></span>

- <span data-ttu-id="7a42e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7a42e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a42e-113">A SimpleNexus single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7a42e-113">A SimpleNexus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a42e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7a42e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a42e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7a42e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a42e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7a42e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7a42e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a42e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a42e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7a42e-118">Scenario description</span></span>
<span data-ttu-id="7a42e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7a42e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a42e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7a42e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a42e-121">Adding SimpleNexus from the gallery</span><span class="sxs-lookup"><span data-stu-id="7a42e-121">Adding SimpleNexus from the gallery</span></span>
1. <span data-ttu-id="7a42e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a42e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-simplenexus-from-the-gallery"></a><span data-ttu-id="7a42e-123">Adding SimpleNexus from the gallery</span><span class="sxs-lookup"><span data-stu-id="7a42e-123">Adding SimpleNexus from the gallery</span></span>
<span data-ttu-id="7a42e-124">To configure the integration of SimpleNexus into Azure AD, you need to add SimpleNexus from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7a42e-124">To configure the integration of SimpleNexus into Azure AD, you need to add SimpleNexus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7a42e-125">**To add SimpleNexus from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a42e-125">**To add SimpleNexus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7a42e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7a42e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="7a42e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7a42e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="7a42e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7a42e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="7a42e-133">In the search box, type **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-133">In the search box, type **SimpleNexus**.</span></span>

    ![Creating an Azure AD test user](./media/simplenexus-tutorial/tutorial_simplenexus_search.png)

1. <span data-ttu-id="7a42e-135">In the results panel, select **SimpleNexus**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7a42e-135">In the results panel, select **SimpleNexus**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/simplenexus-tutorial/tutorial_simplenexus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a42e-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a42e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a42e-138">In this section, you configure and test Azure AD single sign-on with SimpleNexus based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7a42e-138">In this section, you configure and test Azure AD single sign-on with SimpleNexus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a42e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SimpleNexus is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a42e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SimpleNexus is to a user in Azure AD.</span></span> <span data-ttu-id="7a42e-140">In other words, a link relationship between an Azure AD user and the related user in SimpleNexus needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7a42e-140">In other words, a link relationship between an Azure AD user and the related user in SimpleNexus needs to be established.</span></span>

<span data-ttu-id="7a42e-141">In SimpleNexus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="7a42e-141">In SimpleNexus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7a42e-142">To configure and test Azure AD single sign-on with SimpleNexus, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7a42e-142">To configure and test Azure AD single sign-on with SimpleNexus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7a42e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7a42e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7a42e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a42e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7a42e-145">**[Creating a SimpleNexus test user](#creating-a-simplenexus-test-user)** - to have a counterpart of Britta Simon in SimpleNexus that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7a42e-145">**[Creating a SimpleNexus test user](#creating-a-simplenexus-test-user)** - to have a counterpart of Britta Simon in SimpleNexus that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7a42e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7a42e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7a42e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7a42e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a42e-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a42e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a42e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SimpleNexus application.</span><span class="sxs-lookup"><span data-stu-id="7a42e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SimpleNexus application.</span></span>

<span data-ttu-id="7a42e-150">**To configure Azure AD single sign-on with SimpleNexus, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a42e-150">**To configure Azure AD single sign-on with SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="7a42e-151">In the Azure portal, on the **SimpleNexus** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-151">In the Azure portal, on the **SimpleNexus** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="7a42e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7a42e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/simplenexus-tutorial/tutorial_simplenexus_samlbase.png)

1. <span data-ttu-id="7a42e-155">On the **SimpleNexus Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7a42e-155">On the **SimpleNexus Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/simplenexus-tutorial/tutorial_simplenexus_url.png)

    <span data-ttu-id="7a42e-157">a.</span><span class="sxs-lookup"><span data-stu-id="7a42e-157">a.</span></span> <span data-ttu-id="7a42e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>_login`</span><span class="sxs-lookup"><span data-stu-id="7a42e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>_login`</span></span>

    <span data-ttu-id="7a42e-159">b.</span><span class="sxs-lookup"><span data-stu-id="7a42e-159">b.</span></span> <span data-ttu-id="7a42e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="7a42e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7a42e-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7a42e-161">These values are not real.</span></span> <span data-ttu-id="7a42e-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="7a42e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7a42e-163">Contact [SimpleNexus Client support team](https://simplenexus.com/sn/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7a42e-163">Contact [SimpleNexus Client support team](https://simplenexus.com/sn/contact-us/) to get these values.</span></span> 
 
1. <span data-ttu-id="7a42e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7a42e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/simplenexus-tutorial/tutorial_simplenexus_certificate.png) 

1. <span data-ttu-id="7a42e-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7a42e-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/simplenexus-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="7a42e-168">To configure single sign-on on **SimpleNexus** side, you need to send the downloaded **Metadata XML** to [SimpleNexus support team](https://simplenexus.com/sn/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="7a42e-168">To configure single sign-on on **SimpleNexus** side, you need to send the downloaded **Metadata XML** to [SimpleNexus support team](https://simplenexus.com/sn/contact-us/).</span></span> <span data-ttu-id="7a42e-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="7a42e-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7a42e-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="7a42e-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7a42e-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="7a42e-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7a42e-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7a42e-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a42e-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7a42e-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a42e-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a42e-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="7a42e-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a42e-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7a42e-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7a42e-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/simplenexus-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="7a42e-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/simplenexus-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="7a42e-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="7a42e-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/simplenexus-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="7a42e-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7a42e-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/simplenexus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a42e-185">a.</span><span class="sxs-lookup"><span data-stu-id="7a42e-185">a.</span></span> <span data-ttu-id="7a42e-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a42e-187">b.</span><span class="sxs-lookup"><span data-stu-id="7a42e-187">b.</span></span> <span data-ttu-id="7a42e-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7a42e-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a42e-189">c.</span><span class="sxs-lookup"><span data-stu-id="7a42e-189">c.</span></span> <span data-ttu-id="7a42e-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7a42e-191">d.</span><span class="sxs-lookup"><span data-stu-id="7a42e-191">d.</span></span> <span data-ttu-id="7a42e-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-192">Click **Create**.</span></span>
 
### <a name="creating-a-simplenexus-test-user"></a><span data-ttu-id="7a42e-193">Creating a SimpleNexus test user</span><span class="sxs-lookup"><span data-stu-id="7a42e-193">Creating a SimpleNexus test user</span></span>

<span data-ttu-id="7a42e-194">In order to enable Azure AD users to log in to SimpleNexus, they must be provisioned into SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="7a42e-194">In order to enable Azure AD users to log in to SimpleNexus, they must be provisioned into SimpleNexus.</span></span>

<span data-ttu-id="7a42e-195">In the case of SimpleNexus, provisioning is a manual task performed by the tenant administrator.</span><span class="sxs-lookup"><span data-stu-id="7a42e-195">In the case of SimpleNexus, provisioning is a manual task performed by the tenant administrator.</span></span>

>[!NOTE]
><span data-ttu-id="7a42e-196">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="7a42e-196">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7a42e-197">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7a42e-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7a42e-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="7a42e-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SimpleNexus.</span></span>

![Assign User][200] 

<span data-ttu-id="7a42e-200">**To assign Britta Simon to SimpleNexus, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a42e-200">**To assign Britta Simon to SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="7a42e-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7a42e-203">In the applications list, select **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-203">In the applications list, select **SimpleNexus**.</span></span>

    ![Configure Single Sign-On](./media/simplenexus-tutorial/tutorial_simplenexus_app.png) 

1. <span data-ttu-id="7a42e-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7a42e-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="7a42e-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7a42e-207">Click **Add** button.</span></span> <span data-ttu-id="7a42e-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a42e-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="7a42e-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7a42e-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7a42e-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a42e-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7a42e-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a42e-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a42e-213">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a42e-213">Testing single sign-on</span></span>

<span data-ttu-id="7a42e-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7a42e-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7a42e-215">When you click the SimpleNexus tile in the Access Panel, you should get automatically signed-on to your SimpleNexus application.</span><span class="sxs-lookup"><span data-stu-id="7a42e-215">When you click the SimpleNexus tile in the Access Panel, you should get automatically signed-on to your SimpleNexus application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a42e-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7a42e-216">Additional resources</span></span>

* [<span data-ttu-id="7a42e-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a42e-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7a42e-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7a42e-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/simplenexus-tutorial/tutorial_general_01.png
[2]: ./media/simplenexus-tutorial/tutorial_general_02.png
[3]: ./media/simplenexus-tutorial/tutorial_general_03.png
[4]: ./media/simplenexus-tutorial/tutorial_general_04.png

[100]: ./media/simplenexus-tutorial/tutorial_general_100.png

[200]: ./media/simplenexus-tutorial/tutorial_general_200.png
[201]: ./media/simplenexus-tutorial/tutorial_general_201.png
[202]: ./media/simplenexus-tutorial/tutorial_general_202.png
[203]: ./media/simplenexus-tutorial/tutorial_general_203.png

