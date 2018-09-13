---
title: 'Tutorial: Azure Active Directory integration with Asset Bank | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Asset Bank.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 345d071e61d1173d9567b20ce086d2ea71b5876a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660530"
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="ff94b-103">Tutorial: Azure Active Directory integration with Asset Bank</span><span class="sxs-lookup"><span data-stu-id="ff94b-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>
<span data-ttu-id="ff94b-104">The objective of this tutorial is to show you how to integrate Asset Bank with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff94b-104">The objective of this tutorial is to show you how to integrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff94b-105">Integrating Asset Bank with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ff94b-105">Integrating Asset Bank with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="ff94b-106">You can control in Azure AD who has access to Asset Bank</span><span class="sxs-lookup"><span data-stu-id="ff94b-106">You can control in Azure AD who has access to Asset Bank</span></span>
* <span data-ttu-id="ff94b-107">You can enable your users to automatically get signed-on to Asset Bank single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ff94b-107">You can enable your users to automatically get signed-on to Asset Bank single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="ff94b-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="ff94b-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="ff94b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff94b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff94b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff94b-110">Prerequisites</span></span>
<span data-ttu-id="ff94b-111">To configure Azure AD integration with Asset Bank, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ff94b-111">To configure Azure AD integration with Asset Bank, you need the following items:</span></span>

* <span data-ttu-id="ff94b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ff94b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ff94b-113">A Asset Bank single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ff94b-113">A Asset Bank single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="ff94b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ff94b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>  

<span data-ttu-id="ff94b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ff94b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ff94b-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="ff94b-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ff94b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff94b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff94b-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="ff94b-118">Scenario Description</span></span>
<span data-ttu-id="ff94b-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ff94b-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="ff94b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ff94b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="ff94b-121">Adding Asset Bank from the gallery</span><span class="sxs-lookup"><span data-stu-id="ff94b-121">Adding Asset Bank from the gallery</span></span>
* <span data-ttu-id="ff94b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff94b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-asset-bank-from-the-gallery"></a><span data-ttu-id="ff94b-123">Add Asset Bank from the gallery</span><span class="sxs-lookup"><span data-stu-id="ff94b-123">Add Asset Bank from the gallery</span></span>
<span data-ttu-id="ff94b-124">To configure the integration of Asset Bank into Azure AD, you need to add Asset Bank from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ff94b-124">To configure the integration of Asset Bank into Azure AD, you need to add Asset Bank from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff94b-125">**To add Asset Bank from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff94b-125">**To add Asset Bank from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff94b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="ff94b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ff94b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ff94b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ff94b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="ff94b-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ff94b-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="ff94b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="ff94b-135">In the search box, type **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-135">In the search box, type **Asset Bank**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_01.png)
7. <span data-ttu-id="ff94b-137">In the results pane, select **Asset Bank**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ff94b-137">In the results pane, select **Asset Bank**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ff94b-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff94b-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ff94b-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ff94b-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff94b-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Asset Bank to a user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="ff94b-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Asset Bank to a user in Azure AD is.</span></span> <span data-ttu-id="ff94b-142">In other words, a link relationship between an Azure AD user and the related user in Asset Bank needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ff94b-142">In other words, a link relationship between an Azure AD user and the related user in Asset Bank needs to be established.</span></span>

<span data-ttu-id="ff94b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="ff94b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Asset Bank.</span></span>

<span data-ttu-id="ff94b-144">To configure and test Azure AD single sign-on with Asset Bank, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ff94b-144">To configure and test Azure AD single sign-on with Asset Bank, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff94b-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ff94b-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff94b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff94b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff94b-147">**[Creating a Asset Bank test user](#creating-a-asset-bank-test-user)** - to have a counterpart of Britta Simon in Asset Bank that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="ff94b-147">**[Creating a Asset Bank test user](#creating-a-asset-bank-test-user)** - to have a counterpart of Britta Simon in Asset Bank that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ff94b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ff94b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff94b-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ff94b-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ff94b-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff94b-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="ff94b-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Asset Bank application.</span><span class="sxs-lookup"><span data-stu-id="ff94b-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="ff94b-152">**To configure Azure AD single sign-on with Asset Bank, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff94b-152">**To configure Azure AD single sign-on with Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="ff94b-153">In the Azure classic portal, on the **Asset Bank** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="ff94b-153">In the Azure classic portal, on the **Asset Bank** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

![Configure Single Sign-On][6] 

1. <span data-ttu-id="ff94b-155">On the **How would you like users to sign on to Asset Bank** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-155">On the **How would you like users to sign on to Asset Bank** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_03.png) 
2. <span data-ttu-id="ff94b-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff94b-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_04.png) 
    1. <span data-ttu-id="ff94b-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Asset Bank application using the following pattern: **“https://\<company name\>.assetbank-server.com”**</span><span class="sxs-lookup"><span data-stu-id="ff94b-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Asset Bank application using the following pattern: **“https://\<company name\>.assetbank-server.com”**</span></span>
    2. <span data-ttu-id="ff94b-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-160">Click **Next**.</span></span>
1. <span data-ttu-id="ff94b-161">On the **Configure single sign-on at Asset Bank** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff94b-161">On the **Configure single sign-on at Asset Bank** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_05.png)    
    1. <span data-ttu-id="ff94b-163">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ff94b-163">Click **Download metadata**, and then save the file on your computer.</span></span>
    2. <span data-ttu-id="ff94b-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-164">Click **Next**.</span></span>
2. <span data-ttu-id="ff94b-165">To get SSO configured for your application, contact your Asset Bank support team via [support@assetbank.co.uk](mailto:support@assetbank.co.uk) and attach the metadata file to your email.</span><span class="sxs-lookup"><span data-stu-id="ff94b-165">To get SSO configured for your application, contact your Asset Bank support team via [support@assetbank.co.uk](mailto:support@assetbank.co.uk) and attach the metadata file to your email.</span></span>
3. <span data-ttu-id="ff94b-166">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-166">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="ff94b-168">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-168">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ff94b-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ff94b-170">Create an Azure AD test user</span></span>
<span data-ttu-id="ff94b-171">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff94b-171">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="ff94b-172">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-172">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="ff94b-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff94b-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff94b-175">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-175">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="ff94b-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ff94b-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ff94b-178">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-178">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="ff94b-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="ff94b-182">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff94b-182">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/create_aaduser_05.png) 
    1. <span data-ttu-id="ff94b-184">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="ff94b-184">As Type Of User, select New user in your organization.</span></span>
    2. <span data-ttu-id="ff94b-185">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-185">In the User Name **textbox**, type **BrittaSimon**.</span></span>
    3. <span data-ttu-id="ff94b-186">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-186">Click **Next**.</span></span>
6. <span data-ttu-id="ff94b-187">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff94b-187">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/create_aaduser_06.png) 
   1. <span data-ttu-id="ff94b-189">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-189">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="ff94b-190">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-190">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="ff94b-191">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-191">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="ff94b-192">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-192">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="ff94b-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-193">Click **Next**.</span></span>
7. <span data-ttu-id="ff94b-194">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-194">On the **Get temporary password** dialog page, click **create**.</span></span>
    <span data-ttu-id="ff94b-195">![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/create_aaduser_07.png)</span><span class="sxs-lookup"><span data-stu-id="ff94b-195">![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/create_aaduser_07.png)</span></span> 
8. <span data-ttu-id="ff94b-196">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff94b-196">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/create_aaduser_08.png) 
    1. <span data-ttu-id="ff94b-198">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-198">Write down the value of the **New Password**.</span></span>
    2. <span data-ttu-id="ff94b-199">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-199">Click **Complete**.</span></span>   

### <a name="create-a-asset-bank-test-user"></a><span data-ttu-id="ff94b-200">Create a Asset Bank test user</span><span class="sxs-lookup"><span data-stu-id="ff94b-200">Create a Asset Bank test user</span></span>
<span data-ttu-id="ff94b-201">The objective of this section is to create a user called Britta Simon in Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="ff94b-201">The objective of this section is to create a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="ff94b-202">Asset Bank supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="ff94b-202">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ff94b-203">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="ff94b-203">There is no action item for you in this section.</span></span> <span data-ttu-id="ff94b-204">A new user will be created during an attempt to access Asset Bank if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="ff94b-204">A new user will be created during an attempt to access Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="ff94b-205">If you need to create a user manually, you need to contact the Asset Bank support team.</span><span class="sxs-lookup"><span data-stu-id="ff94b-205">If you need to create a user manually, you need to contact the Asset Bank support team.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ff94b-206">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ff94b-206">Assign the Azure AD test user</span></span>
<span data-ttu-id="ff94b-207">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="ff94b-207">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Asset Bank.</span></span>

![Assign User][200] 

<span data-ttu-id="ff94b-209">**To assign Britta Simon to Asset Bank, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff94b-209">**To assign Britta Simon to Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="ff94b-210">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ff94b-210">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="ff94b-212">In the applications list, select **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-212">In the applications list, select **Asset Bank**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_50.png) 
3. <span data-ttu-id="ff94b-214">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-214">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="ff94b-216">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-216">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="ff94b-217">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="ff94b-217">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="ff94b-219">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff94b-219">Test single sign-on</span></span>
<span data-ttu-id="ff94b-220">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ff94b-220">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ff94b-221">When you click the Asset Bank tile in the Access Panel, you should get automatically signed-on to your Asset Bank application.</span><span class="sxs-lookup"><span data-stu-id="ff94b-221">When you click the Asset Bank tile in the Access Panel, you should get automatically signed-on to your Asset Bank application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff94b-222">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="ff94b-222">Additional Resources</span></span>
* [<span data-ttu-id="ff94b-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff94b-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff94b-224">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff94b-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-assetbank-tutorial/tutorial_general_205.png

























