---
title: 'Tutorial: Azure Active Directory integration with CS Stars | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and CS Stars.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 5704d151-afb8-40a4-b286-8bacd4f279ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: d107d0811bd2c2b8f732528eba159160c9839fab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554261"
---
# <a name="tutorial-azure-active-directory-integration-with-cs-stars"></a><span data-ttu-id="fb56b-103">Tutorial: Azure Active Directory integration with CS Stars</span><span class="sxs-lookup"><span data-stu-id="fb56b-103">Tutorial: Azure Active Directory integration with CS Stars</span></span>
<span data-ttu-id="fb56b-104">The objective of this tutorial is to show you how to integrate CS Stars with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb56b-104">The objective of this tutorial is to show you how to integrate CS Stars with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="fb56b-105">Integrating CS Stars with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fb56b-105">Integrating CS Stars with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="fb56b-106">You can control in Azure AD who has access to CS Stars</span><span class="sxs-lookup"><span data-stu-id="fb56b-106">You can control in Azure AD who has access to CS Stars</span></span>
* <span data-ttu-id="fb56b-107">You can enable your users to automatically get signed-on to CS Stars (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="fb56b-107">You can enable your users to automatically get signed-on to CS Stars (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="fb56b-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="fb56b-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="fb56b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb56b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb56b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fb56b-110">Prerequisites</span></span>
<span data-ttu-id="fb56b-111">To configure Azure AD integration with CS Stars, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fb56b-111">To configure Azure AD integration with CS Stars, you need the following items:</span></span>

* <span data-ttu-id="fb56b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fb56b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="fb56b-113">A CS Stars single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="fb56b-113">A CS Stars single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb56b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="fb56b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>
>

<span data-ttu-id="fb56b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="fb56b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="fb56b-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="fb56b-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="fb56b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb56b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb56b-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="fb56b-118">Scenario Description</span></span>
<span data-ttu-id="fb56b-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="fb56b-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="fb56b-120">The scenario outlined in this tutorial consists of three main building blocks:</span><span class="sxs-lookup"><span data-stu-id="fb56b-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="fb56b-121">Adding CS Stars from the gallery</span><span class="sxs-lookup"><span data-stu-id="fb56b-121">Adding CS Stars from the gallery</span></span>
2. <span data-ttu-id="fb56b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fb56b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cs-stars-from-the-gallery"></a><span data-ttu-id="fb56b-123">Adding CS Stars from the gallery</span><span class="sxs-lookup"><span data-stu-id="fb56b-123">Adding CS Stars from the gallery</span></span>
<span data-ttu-id="fb56b-124">To configure the integration of CS Stars into Azure AD, you need to add CS Stars from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="fb56b-124">To configure the integration of CS Stars into Azure AD, you need to add CS Stars from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fb56b-125">**To add CS Stars from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fb56b-125">**To add CS Stars from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fb56b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="fb56b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="fb56b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="fb56b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="fb56b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]
4. <span data-ttu-id="fb56b-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="fb56b-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]
5. <span data-ttu-id="fb56b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]
6. <span data-ttu-id="fb56b-135">In the search box, type **CS Stars**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-135">In the search box, type **CS Stars**.</span></span>

    ![Applications][5]
7. <span data-ttu-id="fb56b-137">In the results pane, select **CS Stars**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="fb56b-137">In the results pane, select **CS Stars**, and then click **Complete** to add the application.</span></span>

    ![Applications][400]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fb56b-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fb56b-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fb56b-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with CS Stars based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fb56b-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with CS Stars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fb56b-141">For single sign-on to work, Azure AD needs to know what the counterpart user in CS Stars to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="fb56b-141">For single sign-on to work, Azure AD needs to know what the counterpart user in CS Stars to an user in Azure AD is.</span></span> <span data-ttu-id="fb56b-142">In other words, a link relationship between an Azure AD user and the related user in CS Stars needs to be established.</span><span class="sxs-lookup"><span data-stu-id="fb56b-142">In other words, a link relationship between an Azure AD user and the related user in CS Stars needs to be established.</span></span>  
<span data-ttu-id="fb56b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in CS Stars.</span><span class="sxs-lookup"><span data-stu-id="fb56b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in CS Stars.</span></span>

<span data-ttu-id="fb56b-144">To configure and test Azure AD single sign-on with CS Stars, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="fb56b-144">To configure and test Azure AD single sign-on with CS Stars, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fb56b-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="fb56b-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fb56b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb56b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb56b-147">**[Creating a CS Stars test user](#creating-a-cs-stars-test-user)** - to have a counterpart of Britta Simon in CS Stars that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="fb56b-147">**[Creating a CS Stars test user](#creating-a-cs-stars-test-user)** - to have a counterpart of Britta Simon in CS Stars that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="fb56b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fb56b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb56b-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="fb56b-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fb56b-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fb56b-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="fb56b-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your CS Stars application.</span><span class="sxs-lookup"><span data-stu-id="fb56b-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your CS Stars application.</span></span>

<span data-ttu-id="fb56b-152">**To configure Azure AD single sign-on with CS Stars, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fb56b-152">**To configure Azure AD single sign-on with CS Stars, perform the following steps:**</span></span>

1. <span data-ttu-id="fb56b-153">In the Azure classic portal, on the **CS Stars** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="fb56b-153">In the Azure classic portal, on the **CS Stars** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Configure Single Sign-On][6]
2. <span data-ttu-id="fb56b-155">On the **How would you like users to sign on to CS Stars** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-155">On the **How would you like users to sign on to CS Stars** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Azure AD Single Sign-On][7]
3. <span data-ttu-id="fb56b-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fb56b-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure App Settings][8]

    <span data-ttu-id="fb56b-159">a.</span><span class="sxs-lookup"><span data-stu-id="fb56b-159">a.</span></span> <span data-ttu-id="fb56b-160">in the **Sign On URL** textbox, type your URL used by your users to sign on to your CS Stars application (e.g.: `https://uat.csstars.com/enterprise/default.cmdx?ssoclient=C234UAT2`).</span><span class="sxs-lookup"><span data-stu-id="fb56b-160">in the **Sign On URL** textbox, type your URL used by your users to sign on to your CS Stars application (e.g.: `https://uat.csstars.com/enterprise/default.cmdx?ssoclient=C234UAT2`).</span></span>

    > [!NOTE]
    > <span data-ttu-id="fb56b-161">If you don't know what the right value is, contact your Marsh ClearSight representative.</span><span class="sxs-lookup"><span data-stu-id="fb56b-161">If you don't know what the right value is, contact your Marsh ClearSight representative.</span></span>

    <span data-ttu-id="fb56b-162">b.</span><span class="sxs-lookup"><span data-stu-id="fb56b-162">b.</span></span> <span data-ttu-id="fb56b-163">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-163">Click **Next**.</span></span>
4. <span data-ttu-id="fb56b-164">On the **Configure single sign-on at CS Stars** page, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="fb56b-164">On the **Configure single sign-on at CS Stars** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>

    ![What is Azure AD Connect][9]
5. <span data-ttu-id="fb56b-166">To get single sign-on enabled for CS Stars, contact your Marsh ClearSight representative and hand the metadata file over.</span><span class="sxs-lookup"><span data-stu-id="fb56b-166">To get single sign-on enabled for CS Stars, contact your Marsh ClearSight representative and hand the metadata file over.</span></span>
6. <span data-ttu-id="fb56b-167">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-167">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![What is Azure AD Connect][10]
7. <span data-ttu-id="fb56b-169">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  

    ![What is Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fb56b-171">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fb56b-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="fb56b-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb56b-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="fb56b-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fb56b-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fb56b-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png)
2. <span data-ttu-id="fb56b-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="fb56b-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="fb56b-178">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-178">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="fb56b-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="fb56b-182">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fb56b-182">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_05.png)

    <span data-ttu-id="fb56b-184">a.</span><span class="sxs-lookup"><span data-stu-id="fb56b-184">a.</span></span> <span data-ttu-id="fb56b-185">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="fb56b-185">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="fb56b-186">b.</span><span class="sxs-lookup"><span data-stu-id="fb56b-186">b.</span></span> <span data-ttu-id="fb56b-187">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb56b-188">c.</span><span class="sxs-lookup"><span data-stu-id="fb56b-188">c.</span></span> <span data-ttu-id="fb56b-189">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-189">Click **Next**.</span></span>
6. <span data-ttu-id="fb56b-190">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fb56b-190">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_06.png)

    <span data-ttu-id="fb56b-192">a.</span><span class="sxs-lookup"><span data-stu-id="fb56b-192">a.</span></span> <span data-ttu-id="fb56b-193">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-193">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="fb56b-194">b.</span><span class="sxs-lookup"><span data-stu-id="fb56b-194">b.</span></span> <span data-ttu-id="fb56b-195">In the **Last Name** txtbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-195">In the **Last Name** txtbox, type, **Simon**.</span></span>

    <span data-ttu-id="fb56b-196">c.</span><span class="sxs-lookup"><span data-stu-id="fb56b-196">c.</span></span> <span data-ttu-id="fb56b-197">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="fb56b-198">d.</span><span class="sxs-lookup"><span data-stu-id="fb56b-198">d.</span></span> <span data-ttu-id="fb56b-199">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-199">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="fb56b-200">e.</span><span class="sxs-lookup"><span data-stu-id="fb56b-200">e.</span></span> <span data-ttu-id="fb56b-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-201">Click **Next**.</span></span>
7. <span data-ttu-id="fb56b-202">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-202">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="fb56b-204">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fb56b-204">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_08.png)

    <span data-ttu-id="fb56b-206">a.</span><span class="sxs-lookup"><span data-stu-id="fb56b-206">a.</span></span> <span data-ttu-id="fb56b-207">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-207">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="fb56b-208">b.</span><span class="sxs-lookup"><span data-stu-id="fb56b-208">b.</span></span> <span data-ttu-id="fb56b-209">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-209">Click **Complete**.</span></span>   

### <a name="creating-a-cs-stars-test-user"></a><span data-ttu-id="fb56b-210">Creating a CS Stars test user</span><span class="sxs-lookup"><span data-stu-id="fb56b-210">Creating a CS Stars test user</span></span>
<span data-ttu-id="fb56b-211">The objective of this section is to create a user called Britta Simon in CS Stars.</span><span class="sxs-lookup"><span data-stu-id="fb56b-211">The objective of this section is to create a user called Britta Simon in CS Stars.</span></span>

<span data-ttu-id="fb56b-212">To get a user created in CS Stars, you need to contact your Marsh ClearSight representative.</span><span class="sxs-lookup"><span data-stu-id="fb56b-212">To get a user created in CS Stars, you need to contact your Marsh ClearSight representative.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fb56b-213">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fb56b-213">Assigning the Azure AD test user</span></span>
<span data-ttu-id="fb56b-214">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to CS Stars.</span><span class="sxs-lookup"><span data-stu-id="fb56b-214">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to CS Stars.</span></span>

![Assign User][200]

<span data-ttu-id="fb56b-216">**To assign Britta Simon to CS Stars, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fb56b-216">**To assign Britta Simon to CS Stars, perform the following steps:**</span></span>

1. <span data-ttu-id="fb56b-217">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="fb56b-217">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201]
2. <span data-ttu-id="fb56b-219">In the applications list, select **CS Stars**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-219">In the applications list, select **CS Stars**.</span></span>

    ![Assign User][202]
3. <span data-ttu-id="fb56b-221">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-221">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203]
4. <span data-ttu-id="fb56b-223">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-223">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="fb56b-224">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="fb56b-224">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="fb56b-226">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fb56b-226">Testing Single Sign-On</span></span>
<span data-ttu-id="fb56b-227">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="fb56b-227">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="fb56b-228">When you click the CS Stars tile in the Access Panel, you should get automatically signed-on to your CS Stars application.</span><span class="sxs-lookup"><span data-stu-id="fb56b-228">When you click the CS Stars tile in the Access Panel, you should get automatically signed-on to your CS Stars application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb56b-229">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="fb56b-229">Additional Resources</span></span>
* [<span data-ttu-id="fb56b-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb56b-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb56b-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb56b-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_01.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_02.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_general_205.png

[400]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_403.png

























