---
title: 'Tutorial: Azure Active Directory integration with Intralinks | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Intralinks.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jeedes
ms.openlocfilehash: 9cd04043263697e1f2e3446907533589bbeef019
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550938"
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="1eb41-103">Tutorial: Azure Active Directory integration with Intralinks</span><span class="sxs-lookup"><span data-stu-id="1eb41-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>
<span data-ttu-id="1eb41-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1eb41-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1eb41-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1eb41-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1eb41-106">You can control in Azure AD who has access to Intralinks</span><span class="sxs-lookup"><span data-stu-id="1eb41-106">You can control in Azure AD who has access to Intralinks</span></span>
* <span data-ttu-id="1eb41-107">You can enable your users to automatically get signed-on to Intralinks single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1eb41-107">You can enable your users to automatically get signed-on to Intralinks single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="1eb41-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="1eb41-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1eb41-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1eb41-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1eb41-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1eb41-110">Prerequisites</span></span>
<span data-ttu-id="1eb41-111">To configure Azure AD integration with Intralinks, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1eb41-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

* <span data-ttu-id="1eb41-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1eb41-112">An Azure AD subscription</span></span>
* <span data-ttu-id="1eb41-113">A Intralinks single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1eb41-113">A Intralinks single-sign on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="1eb41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1eb41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="1eb41-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1eb41-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1eb41-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="1eb41-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1eb41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1eb41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1eb41-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="1eb41-118">Scenario Description</span></span>
<span data-ttu-id="1eb41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1eb41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="1eb41-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1eb41-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1eb41-121">Adding Intralinks from the gallery</span><span class="sxs-lookup"><span data-stu-id="1eb41-121">Adding Intralinks from the gallery</span></span>
2. <span data-ttu-id="1eb41-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1eb41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-intralinks-from-the-gallery"></a><span data-ttu-id="1eb41-123">Add Intralinks from the gallery</span><span class="sxs-lookup"><span data-stu-id="1eb41-123">Add Intralinks from the gallery</span></span>
<span data-ttu-id="1eb41-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1eb41-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1eb41-125">**To add Intralinks from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eb41-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb41-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="1eb41-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1eb41-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1eb41-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1eb41-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="1eb41-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1eb41-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="1eb41-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="1eb41-135">In the search box, type **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-135">In the search box, type **Intralinks**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_01.png)
7. <span data-ttu-id="1eb41-137">In the results pane, select **Intralinks**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1eb41-137">In the results pane, select **Intralinks**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_02.png)

## <a name="configure-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1eb41-139">Configure and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1eb41-139">Configure and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1eb41-140">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1eb41-140">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1eb41-141">For SSO to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1eb41-141">For SSO to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="1eb41-142">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1eb41-142">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

>[!NOTE]
><span data-ttu-id="1eb41-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Intralinks.</span><span class="sxs-lookup"><span data-stu-id="1eb41-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Intralinks.</span></span>
>

<span data-ttu-id="1eb41-144">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1eb41-144">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1eb41-145">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1eb41-145">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1eb41-146">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1eb41-146">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1eb41-147">**[Create an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="1eb41-147">**[Create an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1eb41-148">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1eb41-148">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1eb41-149">**[Test Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1eb41-149">**[Test Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1eb41-150">Configure Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1eb41-150">Configure Azure AD Single Sign-On</span></span>
<span data-ttu-id="1eb41-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Intralinks application.</span><span class="sxs-lookup"><span data-stu-id="1eb41-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="1eb41-152">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eb41-152">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb41-153">In the classic portal, on the **Intralinks** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="1eb41-153">In the classic portal, on the **Intralinks** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="1eb41-155">On the **How would you like users to sign on to Intralinks** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-155">On the **How would you like users to sign on to Intralinks** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_03.png) 
3. <span data-ttu-id="1eb41-157">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="1eb41-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_04.png) 
   
    1. <span data-ttu-id="1eb41-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern: **https://\<company name\>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/\<Azure AD Tenant ID\>/**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern: **https://\<company name\>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/\<Azure AD Tenant ID\>/**.</span></span>
    2. <span data-ttu-id="1eb41-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-160">Click **Next**.</span></span>
4. <span data-ttu-id="1eb41-161">On the **Configure single sign-on at Intralinks** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1eb41-161">On the **Configure single sign-on at Intralinks** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_05.png)
   
    1. <span data-ttu-id="1eb41-163">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1eb41-163">Click **Download metadata**, and then save the file on your computer.</span></span>
    2. <span data-ttu-id="1eb41-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-164">Click **Next**.</span></span>
5. <span data-ttu-id="1eb41-165">To get SSO configured for your application, contact Intralinks support team and email the attach downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="1eb41-165">To get SSO configured for your application, contact Intralinks support team and email the attach downloaded metadata file.</span></span>
6. <span data-ttu-id="1eb41-166">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-166">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="1eb41-168">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-168">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1eb41-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1eb41-170">Create an Azure AD test user</span></span>
<span data-ttu-id="1eb41-171">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1eb41-171">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

* <span data-ttu-id="1eb41-172">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-172">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="1eb41-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eb41-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb41-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="1eb41-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1eb41-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1eb41-178">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-178">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="1eb41-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="1eb41-182">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="1eb41-182">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/create_aaduser_05.png)</span></span> 
   
    1. <span data-ttu-id="1eb41-183">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="1eb41-183">As Type Of User, select New user in your organization.</span></span> 
    2. <span data-ttu-id="1eb41-184">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-184">In the User Name **textbox**, type **BrittaSimon**.</span></span>
    3. <span data-ttu-id="1eb41-185">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-185">Click **Next**.</span></span>
6. <span data-ttu-id="1eb41-186">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="1eb41-186">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/create_aaduser_06.png)</span></span> 
   
   1. <span data-ttu-id="1eb41-187">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-187">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="1eb41-188">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-188">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="1eb41-189">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-189">In the **Display Name** textbox, type **Britta Simon**.</span></span>   
   4. <span data-ttu-id="1eb41-190">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-190">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="1eb41-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-191">Click **Next**.</span></span>
7. <span data-ttu-id="1eb41-192">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-192">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="1eb41-194">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1eb41-194">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/create_aaduser_08.png) 
   
    1. <span data-ttu-id="1eb41-196">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-196">Write down the value of the **New Password**.</span></span>
    2. <span data-ttu-id="1eb41-197">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-197">Click **Complete**.</span></span>   

### <a name="create-an-intralinks-test-user"></a><span data-ttu-id="1eb41-198">Create an Intralinks test user</span><span class="sxs-lookup"><span data-stu-id="1eb41-198">Create an Intralinks test user</span></span>
<span data-ttu-id="1eb41-199">In this section, you create a user called Britta Simon in Intralinks.</span><span class="sxs-lookup"><span data-stu-id="1eb41-199">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="1eb41-200">Please work with Intralinks support team to add the users in the Intralinks platform.</span><span class="sxs-lookup"><span data-stu-id="1eb41-200">Please work with Intralinks support team to add the users in the Intralinks platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1eb41-201">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1eb41-201">Assign the Azure AD test user</span></span>
<span data-ttu-id="1eb41-202">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Intralinks.</span><span class="sxs-lookup"><span data-stu-id="1eb41-202">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Intralinks.</span></span>

![Assign User][200] 

<span data-ttu-id="1eb41-204">**To assign Britta Simon to Intralinks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eb41-204">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb41-205">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1eb41-205">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="1eb41-207">In the applications list, select **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-207">In the applications list, select **Intralinks**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_50.png) 
3. <span data-ttu-id="1eb41-209">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-209">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="1eb41-211">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-211">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1eb41-212">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-212">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="1eb41-214">Add Intralinks VIA or Elite application</span><span class="sxs-lookup"><span data-stu-id="1eb41-214">Add Intralinks VIA or Elite application</span></span>
<span data-ttu-id="1eb41-215">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span><span class="sxs-lookup"><span data-stu-id="1eb41-215">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="1eb41-216">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span><span class="sxs-lookup"><span data-stu-id="1eb41-216">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="1eb41-217">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span><span class="sxs-lookup"><span data-stu-id="1eb41-217">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="1eb41-218">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span><span class="sxs-lookup"><span data-stu-id="1eb41-218">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>
> 

1. <span data-ttu-id="1eb41-219">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-219">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="1eb41-221">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1eb41-221">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1eb41-222">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1eb41-222">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="1eb41-224">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1eb41-224">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="1eb41-226">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-226">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="1eb41-228">From the left tab click on **Custom** tab.</span><span class="sxs-lookup"><span data-stu-id="1eb41-228">From the left tab click on **Custom** tab.</span></span>
   
    ![Adding Intralinks VIA or Elite application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_51.png)
7. <span data-ttu-id="1eb41-230">Give appropriate name to the application e.g. **Intralinks Elite** and click the Finish button.</span><span class="sxs-lookup"><span data-stu-id="1eb41-230">Give appropriate name to the application e.g. **Intralinks Elite** and click the Finish button.</span></span>
8. <span data-ttu-id="1eb41-231">Click **Configure Single Sign** button.</span><span class="sxs-lookup"><span data-stu-id="1eb41-231">Click **Configure Single Sign** button.</span></span>
9. <span data-ttu-id="1eb41-232">Select the **Existing Single Sign On** option.</span><span class="sxs-lookup"><span data-stu-id="1eb41-232">Select the **Existing Single Sign On** option.</span></span>
   
    ![Adding Intralinks VIA or Elite application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_52.png)
10. <span data-ttu-id="1eb41-234">Get the the SP Initiated SSO URL from Intralinks team for the other Intralinks application and enter it as shown below.</span><span class="sxs-lookup"><span data-stu-id="1eb41-234">Get the the SP Initiated SSO URL from Intralinks team for the other Intralinks application and enter it as shown below.</span></span> 
    
    ![Adding Intralinks VIA or Elite application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_53.png)
    
    * <span data-ttu-id="1eb41-236">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern: **https://\<CompanyName\>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/\<AzureADTenantID\>/**</span><span class="sxs-lookup"><span data-stu-id="1eb41-236">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern: **https://\<CompanyName\>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/\<AzureADTenantID\>/**</span></span>
11. <span data-ttu-id="1eb41-237">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-237">Click **Next**.</span></span>
12. <span data-ttu-id="1eb41-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="1eb41-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="1eb41-239">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1eb41-239">Test single sign-on</span></span>
<span data-ttu-id="1eb41-240">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1eb41-240">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1eb41-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span><span class="sxs-lookup"><span data-stu-id="1eb41-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1eb41-242">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="1eb41-242">Additional Resources</span></span>
* [<span data-ttu-id="1eb41-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eb41-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1eb41-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1eb41-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intralinks-tutorial/tutorial_general_205.png




























