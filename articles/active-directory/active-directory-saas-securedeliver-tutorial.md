---
title: 'Tutorial: Azure Active Directory integration with Novatus | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SECURE DELIVER.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: fccd5668-fe6f-4e6d-a9ce-ba4f321c33d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: jeedes
ms.openlocfilehash: 81519aa7f60658ab35ca65f63ffcda2f9399cd42
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555965"
---
# <a name="tutorial-azure-active-directory-integration-with-secure-deliver"></a><span data-ttu-id="1df2f-103">Tutorial: Azure Active Directory integration with SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="1df2f-103">Tutorial: Azure Active Directory integration with SECURE DELIVER</span></span>
<span data-ttu-id="1df2f-104">The objective of this tutorial is to show you how to integrate SECURE DELIVER with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1df2f-104">The objective of this tutorial is to show you how to integrate SECURE DELIVER with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="1df2f-105">Integrating SECURE DELIVER with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1df2f-105">Integrating SECURE DELIVER with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1df2f-106">You can control in Azure AD who has access to SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="1df2f-106">You can control in Azure AD who has access to SECURE DELIVER</span></span>
* <span data-ttu-id="1df2f-107">You can enable your users to automatically get signed-on to SECURE DELIVER (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1df2f-107">You can enable your users to automatically get signed-on to SECURE DELIVER (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="1df2f-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="1df2f-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1df2f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1df2f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1df2f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1df2f-110">Prerequisites</span></span>
<span data-ttu-id="1df2f-111">To configure Azure AD integration with SECURE DELIVER, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1df2f-111">To configure Azure AD integration with SECURE DELIVER, you need the following items:</span></span>

* <span data-ttu-id="1df2f-112">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="1df2f-112">An Azure subscription</span></span>
* <span data-ttu-id="1df2f-113">A SECURE DELIVER single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1df2f-113">A SECURE DELIVER single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="1df2f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1df2f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="1df2f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1df2f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1df2f-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="1df2f-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1df2f-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1df2f-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1df2f-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="1df2f-118">Scenario Description</span></span>
<span data-ttu-id="1df2f-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1df2f-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="1df2f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1df2f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1df2f-121">Adding SECURE DELIVER from the gallery</span><span class="sxs-lookup"><span data-stu-id="1df2f-121">Adding SECURE DELIVER from the gallery</span></span>
2. <span data-ttu-id="1df2f-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1df2f-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-secure-deliver-from-the-gallery"></a><span data-ttu-id="1df2f-123">Add SECURE DELIVER from the gallery</span><span class="sxs-lookup"><span data-stu-id="1df2f-123">Add SECURE DELIVER from the gallery</span></span>
<span data-ttu-id="1df2f-124">To configure the integration of SECURE DELIVER into Azure AD, you need to add SECURE DELIVER from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1df2f-124">To configure the integration of SECURE DELIVER into Azure AD, you need to add SECURE DELIVER from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1df2f-125">**To add SECURE DELIVER from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1df2f-125">**To add SECURE DELIVER from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1df2f-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="1df2f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1df2f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1df2f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1df2f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="1df2f-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1df2f-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="1df2f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="1df2f-135">In the search box, type **SECURE DELIVER**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-135">In the search box, type **SECURE DELIVER**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_01.png)

7. <span data-ttu-id="1df2f-137">In the results pane, select **SECURE DELIVER**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1df2f-137">In the results pane, select **SECURE DELIVER**, and then click **Complete** to add the application.</span></span>
   
    ![App logo and Name in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_06.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1df2f-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1df2f-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1df2f-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SECURE DELIVER based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1df2f-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SECURE DELIVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1df2f-141">For SSO to work, Azure AD needs to know what the counterpart user in SECURE DELIVER to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="1df2f-141">For SSO to work, Azure AD needs to know what the counterpart user in SECURE DELIVER to an user in Azure AD is.</span></span> <span data-ttu-id="1df2f-142">In other words, a link relationship between an Azure AD user and the related user in SECURE DELIVER needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1df2f-142">In other words, a link relationship between an Azure AD user and the related user in SECURE DELIVER needs to be established.</span></span>  

<span data-ttu-id="1df2f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="1df2f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SECURE DELIVER.</span></span>

<span data-ttu-id="1df2f-144">To configure and test Azure AD SSO with SECURE DELIVER, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1df2f-144">To configure and test Azure AD SSO with SECURE DELIVER, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1df2f-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1df2f-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1df2f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1df2f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1df2f-147">**[Creating a SECURE DELIVER test user](#creating-a-secure-deliver-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="1df2f-147">**[Creating a SECURE DELIVER test user](#creating-a-secure-deliver-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1df2f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1df2f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1df2f-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1df2f-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1df2f-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1df2f-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="1df2f-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your SECURE DELIVER application.</span><span class="sxs-lookup"><span data-stu-id="1df2f-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your SECURE DELIVER application.</span></span>

<span data-ttu-id="1df2f-152">**To configure Azure AD single sign-on with SECURE DELIVER, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1df2f-152">**To configure Azure AD single sign-on with SECURE DELIVER, perform the following steps:**</span></span>

1. <span data-ttu-id="1df2f-153">In the Azure classic portal, on the **SECURE DELIVER** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="1df2f-153">In the Azure classic portal, on the **SECURE DELIVER** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="1df2f-155">On the **How would you like users to sign on to SECURE DELIVER** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-155">On the **How would you like users to sign on to SECURE DELIVER** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_03.png) 

3. <span data-ttu-id="1df2f-157">On the **Configure App Settings** dialog page, perform the following steps and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="1df2f-157">On the **Configure App Settings** dialog page, perform the following steps and then click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_04.png) 
   1. <span data-ttu-id="1df2f-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SECURE DELIVER application using the following pattern: **“https://i-securedeliver.jp/sd/\<company name\>/jsf/login/sso”**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SECURE DELIVER application using the following pattern: **“https://i-securedeliver.jp/sd/\<company name\>/jsf/login/sso”**.</span></span>
   2. <span data-ttu-id="1df2f-160">Contact the SECURE DELIVER Support Team via [iw-sd-support@fujifilm.com](mailto:iw-sd-support@fujifilm.com) to get your tenant URL if you don't know the value.</span><span class="sxs-lookup"><span data-stu-id="1df2f-160">Contact the SECURE DELIVER Support Team via [iw-sd-support@fujifilm.com](mailto:iw-sd-support@fujifilm.com) to get your tenant URL if you don't know the value.</span></span>
   3. <span data-ttu-id="1df2f-161">In the **Identifier** textbox, type the tenant URL.</span><span class="sxs-lookup"><span data-stu-id="1df2f-161">In the **Identifier** textbox, type the tenant URL.</span></span> 
   4. <span data-ttu-id="1df2f-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-162">Click **Next**.</span></span>

4. <span data-ttu-id="1df2f-163">On the **Configure single sign-on at SECURE DELIVER** page, perform the following steps and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="1df2f-163">On the **Configure single sign-on at SECURE DELIVER** page, perform the following steps and then click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_05.png) 
   1. <span data-ttu-id="1df2f-165">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1df2f-165">Click **Download certificate**, and then save the file on your computer.</span></span>
   2. <span data-ttu-id="1df2f-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-166">Click **Next**.</span></span>

5. <span data-ttu-id="1df2f-167">To get SSO configured for your application, contact your SECURE DELIVER support team via [iw-sd-support@fujifilm.com](mailto:iw-sd-support@fujifilm.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="1df2f-167">To get SSO configured for your application, contact your SECURE DELIVER support team via [iw-sd-support@fujifilm.com](mailto:iw-sd-support@fujifilm.com) and provide them with the following:</span></span>
   
   * <span data-ttu-id="1df2f-168">The downloaded certificate file</span><span class="sxs-lookup"><span data-stu-id="1df2f-168">The downloaded certificate file</span></span>
   * <span data-ttu-id="1df2f-169">The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="1df2f-169">The **Entity ID**</span></span>
   * <span data-ttu-id="1df2f-170">The **Single Sign-On Service URL**</span><span class="sxs-lookup"><span data-stu-id="1df2f-170">The **Single Sign-On Service URL**</span></span>
   * <span data-ttu-id="1df2f-171">The **Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="1df2f-171">The **Single Sign-Out Service URL**</span></span>

6. <span data-ttu-id="1df2f-172">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-172">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="1df2f-174">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-174">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

###<a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1df2f-176">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1df2f-176">Create an Azure AD test user</span></span>

<span data-ttu-id="1df2f-177">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1df2f-177">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="1df2f-179">**To create a SECURE DELIVER test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1df2f-179">**To create a SECURE DELIVER test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1df2f-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="1df2f-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1df2f-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1df2f-183">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-183">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1df2f-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="1df2f-187">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1df2f-187">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="1df2f-189">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="1df2f-189">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="1df2f-190">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-190">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="1df2f-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-191">Click **Next**.</span></span>

6. <span data-ttu-id="1df2f-192">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1df2f-192">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/create_aaduser_06.png)  
  1. <span data-ttu-id="1df2f-194">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-194">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="1df2f-195">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-195">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="1df2f-196">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>  
  4. <span data-ttu-id="1df2f-197">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-197">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="1df2f-198">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-198">Click **Next**.</span></span>

7. <span data-ttu-id="1df2f-199">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-199">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="1df2f-201">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1df2f-201">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="1df2f-203">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-203">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="1df2f-204">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-204">Click **Complete**.</span></span>   

### <a name="create-a-secure-deliver-test-user"></a><span data-ttu-id="1df2f-205">Create a SECURE DELIVER test user</span><span class="sxs-lookup"><span data-stu-id="1df2f-205">Create a SECURE DELIVER test user</span></span>
<span data-ttu-id="1df2f-206">The objective of this section is to create a user called Britta Simon in SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="1df2f-206">The objective of this section is to create a user called Britta Simon in SECURE DELIVER.</span></span> <span data-ttu-id="1df2f-207">Please work with SECURE DELIVER support team to add the users in the SECURE DELIVER account.</span><span class="sxs-lookup"><span data-stu-id="1df2f-207">Please work with SECURE DELIVER support team to add the users in the SECURE DELIVER account.</span></span>

>[!NOTE]
><span data-ttu-id="1df2f-208">If you need to create an user manually, you need to contact the SECURE DELIVER support team.</span><span class="sxs-lookup"><span data-stu-id="1df2f-208">If you need to create an user manually, you need to contact the SECURE DELIVER support team.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1df2f-209">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1df2f-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="1df2f-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="1df2f-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to SECURE DELIVER.</span></span>

![Assign User][200] 

<span data-ttu-id="1df2f-212">**To assign Britta Simon to SECURE DELIVER, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1df2f-212">**To assign Britta Simon to SECURE DELIVER, perform the following steps:**</span></span>

1. <span data-ttu-id="1df2f-213">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1df2f-213">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="1df2f-215">In the applications list, select **SECURE DELIVER**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-215">In the applications list, select **SECURE DELIVER**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_50.png) 
3. <span data-ttu-id="1df2f-217">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-217">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="1df2f-219">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1df2f-220">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="1df2f-222">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1df2f-222">Test single sign-on</span></span>
<span data-ttu-id="1df2f-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1df2f-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="1df2f-224">When you click the SECURE DELIVER tile in the Access Panel, you should get automatically signed-on to your SECURE DELIVER application.</span><span class="sxs-lookup"><span data-stu-id="1df2f-224">When you click the SECURE DELIVER tile in the Access Panel, you should get automatically signed-on to your SECURE DELIVER application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1df2f-225">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="1df2f-225">Additional Resources</span></span>
* [<span data-ttu-id="1df2f-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1df2f-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1df2f-227">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1df2f-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-securedeliver-tutorial/tutorial_general_205.png

























