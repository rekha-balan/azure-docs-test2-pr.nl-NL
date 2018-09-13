---
title: 'Tutorial: Azure Active Directory integration with 10,000ft Plans | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 10,000ft Plans.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: cc6b1036d98aca62360ed8a935d2d1719c7f4069
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867616"
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="3ca8c-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="3ca8c-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="3ca8c-104">In this tutorial, you learn how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ca8c-104">In this tutorial, you learn how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ca8c-105">Integrating 10,000ft Plans with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3ca8c-105">Integrating 10,000ft Plans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ca8c-106">You can control in Azure AD who has access to 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="3ca8c-106">You can control in Azure AD who has access to 10,000ft Plans</span></span>
- <span data-ttu-id="3ca8c-107">You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="3ca8c-107">You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ca8c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3ca8c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3ca8c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3ca8c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ca8c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3ca8c-110">Prerequisites</span></span>

<span data-ttu-id="3ca8c-111">To configure Azure AD integration with 10,000ft Plans, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3ca8c-111">To configure Azure AD integration with 10,000ft Plans, you need the following items:</span></span>

- <span data-ttu-id="3ca8c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3ca8c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ca8c-113">A 10,000ft Plans single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3ca8c-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ca8c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ca8c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3ca8c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ca8c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ca8c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ca8c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ca8c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3ca8c-118">Scenario description</span></span>
<span data-ttu-id="3ca8c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ca8c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3ca8c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ca8c-121">Adding 10,000ft Plans from the gallery</span><span class="sxs-lookup"><span data-stu-id="3ca8c-121">Adding 10,000ft Plans from the gallery</span></span>
2. <span data-ttu-id="3ca8c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ca8c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-the-gallery"></a><span data-ttu-id="3ca8c-123">Adding 10,000ft Plans from the gallery</span><span class="sxs-lookup"><span data-stu-id="3ca8c-123">Adding 10,000ft Plans from the gallery</span></span>
<span data-ttu-id="3ca8c-124">To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-124">To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ca8c-125">**To add 10,000ft Plans from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ca8c-125">**To add 10,000ft Plans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca8c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ca8c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ca8c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3ca8c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3ca8c-133">In the search box, type **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-133">In the search box, type **10,000ft Plans**.</span></span>

    ![Creating an Azure AD test user](./media/10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="3ca8c-135">In the results panel, select **10,000ft Plans**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-135">In the results panel, select **10,000ft Plans**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ca8c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ca8c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ca8c-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3ca8c-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3ca8c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans is to a user in Azure AD.</span></span> <span data-ttu-id="3ca8c-140">In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-140">In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.</span></span>

<span data-ttu-id="3ca8c-141">In 10,000ft Plans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-141">In 10,000ft Plans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3ca8c-142">To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3ca8c-142">To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ca8c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ca8c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ca8c-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in 10,000ft Plans that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in 10,000ft Plans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ca8c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ca8c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ca8c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ca8c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ca8c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 10,000ft Plans application.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="3ca8c-150">**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ca8c-150">**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca8c-151">In the Azure portal, on the **10,000ft Plans** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-151">In the Azure portal, on the **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="3ca8c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="3ca8c-155">On the **10,000ft Plans Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3ca8c-155">On the **10,000ft Plans Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="3ca8c-157">a.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-157">a.</span></span> <span data-ttu-id="3ca8c-158">In the **Sign-on URL** textbox, type the URL: `https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="3ca8c-158">In the **Sign-on URL** textbox, type the URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="3ca8c-159">b.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-159">b.</span></span> <span data-ttu-id="3ca8c-160">In the **Identifier** textbox, type the URL: `https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="3ca8c-160">In the **Identifier** textbox, type the URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3ca8c-161">The value for **Identifier** is different if you have a custom domain.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-161">The value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="3ca8c-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) to get this value.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) to get this value.</span></span> 
 
4. <span data-ttu-id="3ca8c-163">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-163">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="3ca8c-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3ca8c-167">On the **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-167">On the **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3ca8c-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="3ca8c-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="3ca8c-170">To configure single sign-on on **10,000ft Plans** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="3ca8c-170">To configure single sign-on on **10,000ft Plans** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="3ca8c-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="3ca8c-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ca8c-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ca8c-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3ca8c-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ca8c-174">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3ca8c-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ca8c-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="3ca8c-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ca8c-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca8c-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ca8c-180">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ca8c-182">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ca8c-184">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3ca8c-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ca8c-186">a.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-186">a.</span></span> <span data-ttu-id="3ca8c-187">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ca8c-188">b.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-188">b.</span></span> <span data-ttu-id="3ca8c-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ca8c-190">c.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-190">c.</span></span> <span data-ttu-id="3ca8c-191">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3ca8c-192">d.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-192">d.</span></span> <span data-ttu-id="3ca8c-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="3ca8c-194">Creating a 10,000ft Plans test user</span><span class="sxs-lookup"><span data-stu-id="3ca8c-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="3ca8c-195">The objective of this section is to create a user called Britta Simon in 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-195">The objective of this section is to create a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="3ca8c-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="3ca8c-197">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-197">There is no action item for you in this section.</span></span> <span data-ttu-id="3ca8c-198">A new user is created during an attempt to access 10,000ft Plans if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-198">A new user is created during an attempt to access 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="3ca8c-199">If you need to create a user manually, you need to contact the [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="3ca8c-199">If you need to create a user manually, you need to contact the [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3ca8c-200">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3ca8c-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3ca8c-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 10,000ft Plans.</span></span>

![Assign User][200] 

<span data-ttu-id="3ca8c-203">**To assign Britta Simon to 10,000ft Plans, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ca8c-203">**To assign Britta Simon to 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca8c-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="3ca8c-206">In the applications list, select **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-206">In the applications list, select **10,000ft Plans**.</span></span>

    ![Configure Single Sign-On](./media/10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="3ca8c-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="3ca8c-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-210">Click **Add** button.</span></span> <span data-ttu-id="3ca8c-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="3ca8c-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3ca8c-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ca8c-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ca8c-216">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ca8c-216">Testing single sign-on</span></span>

<span data-ttu-id="3ca8c-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="3ca8c-218">When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.</span><span class="sxs-lookup"><span data-stu-id="3ca8c-218">When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="3ca8c-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3ca8c-219">Additional resources</span></span>

* [<span data-ttu-id="3ca8c-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ca8c-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3ca8c-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3ca8c-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/10000ftplans-tutorial/tutorial_general_203.png

