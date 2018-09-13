---
title: 'Tutorial: Azure Active Directory integration with Synergi | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Synergi.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 73c970e1-f1ba-420b-b225-414fdf93b140
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 8c8475e373977194d18fb24a44f385492bb55499
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564312"
---
# <a name="tutorial-azure-active-directory-integration-with-synergi"></a><span data-ttu-id="4d8f3-103">Tutorial: Azure Active Directory integration with Synergi</span><span class="sxs-lookup"><span data-stu-id="4d8f3-103">Tutorial: Azure Active Directory integration with Synergi</span></span>
<span data-ttu-id="4d8f3-104">In this tutorial, you learn how to integrate Synergi with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d8f3-104">In this tutorial, you learn how to integrate Synergi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d8f3-105">Integrating Synergi with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-105">Integrating Synergi with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="4d8f3-106">You can control in Azure AD who has access to Synergi</span><span class="sxs-lookup"><span data-stu-id="4d8f3-106">You can control in Azure AD who has access to Synergi</span></span>
* <span data-ttu-id="4d8f3-107">You can enable your users to automatically get signed-on to Synergi single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4d8f3-107">You can enable your users to automatically get signed-on to Synergi single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="4d8f3-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="4d8f3-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="4d8f3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d8f3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d8f3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4d8f3-110">Prerequisites</span></span>
<span data-ttu-id="4d8f3-111">To configure Azure AD integration with Synergi, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-111">To configure Azure AD integration with Synergi, you need the following items:</span></span>

* <span data-ttu-id="4d8f3-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4d8f3-112">An Azure AD subscription</span></span>
* <span data-ttu-id="4d8f3-113">A Synergi SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4d8f3-113">A Synergi SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="4d8f3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="4d8f3-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="4d8f3-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="4d8f3-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d8f3-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d8f3-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4d8f3-118">Scenario description</span></span>
<span data-ttu-id="4d8f3-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="4d8f3-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d8f3-121">Adding Synergi from the gallery</span><span class="sxs-lookup"><span data-stu-id="4d8f3-121">Adding Synergi from the gallery</span></span>
2. <span data-ttu-id="4d8f3-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="4d8f3-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-synergi-from-the-gallery"></a><span data-ttu-id="4d8f3-123">Add Synergi from the gallery</span><span class="sxs-lookup"><span data-stu-id="4d8f3-123">Add Synergi from the gallery</span></span>
<span data-ttu-id="4d8f3-124">To configure the integration of Synergi into Azure AD, you need to add Synergi from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-124">To configure the integration of Synergi into Azure AD, you need to add Synergi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4d8f3-125">**To add Synergi from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4d8f3-125">**To add Synergi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4d8f3-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]

2. <span data-ttu-id="4d8f3-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="4d8f3-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="4d8f3-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="4d8f3-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="4d8f3-135">In the search box, type **Synergi**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-135">In the search box, type **Synergi**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_synergi_01.png)

7. <span data-ttu-id="4d8f3-137">In the results pane, select **Synergi**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-137">In the results pane, select **Synergi**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_synergi_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4d8f3-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4d8f3-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4d8f3-140">In this section, you configure and test Azure AD SSO with Synergi based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4d8f3-140">In this section, you configure and test Azure AD SSO with Synergi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4d8f3-141">For SSO to work, Azure AD needs to know what the counterpart user in Synergi is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-141">For SSO to work, Azure AD needs to know what the counterpart user in Synergi is to a user in Azure AD.</span></span> <span data-ttu-id="4d8f3-142">In other words, a link relationship between an Azure AD user and the related user in Synergi needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-142">In other words, a link relationship between an Azure AD user and the related user in Synergi needs to be established.</span></span>

<span data-ttu-id="4d8f3-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Synergi.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Synergi.</span></span>

<span data-ttu-id="4d8f3-144">To configure and test Azure AD SSO with Synergi, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-144">To configure and test Azure AD SSO with Synergi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4d8f3-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4d8f3-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d8f3-147">**[Creating a Synergi test user](#creating-a-synergi-test-user)** - to have a counterpart of Britta Simon in Synergi that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-147">**[Creating a Synergi test user](#creating-a-synergi-test-user)** - to have a counterpart of Britta Simon in Synergi that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4d8f3-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d8f3-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4d8f3-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4d8f3-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="4d8f3-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Synergi application.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Synergi application.</span></span>

<span data-ttu-id="4d8f3-152">**To configure Azure AD single sign-on with Synergi, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4d8f3-152">**To configure Azure AD single sign-on with Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="4d8f3-153">In the classic portal, on the **Synergi** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-153">In the classic portal, on the **Synergi** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="4d8f3-155">On the **How would you like users to sign on to Synergi** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-155">On the **How would you like users to sign on to Synergi** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_synergi_03.png) 

3. <span data-ttu-id="4d8f3-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_synergi_04.png) 
  1. <span data-ttu-id="4d8f3-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Synergi application using the following pattern: **https://\<company name\>.irmsecurity.com/sso/\<organization id\>**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Synergi application using the following pattern: **https://\<company name\>.irmsecurity.com/sso/\<organization id\>**.</span></span> 
  2. <span data-ttu-id="4d8f3-160">click **Next**</span><span class="sxs-lookup"><span data-stu-id="4d8f3-160">click **Next**</span></span>

4. <span data-ttu-id="4d8f3-161">On the **Configure single sign-on at Synergi** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-161">On the **Configure single sign-on at Synergi** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_synergi_05.png)
  1. <span data-ttu-id="4d8f3-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-163">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="4d8f3-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-164">Click **Next**.</span></span>

5. <span data-ttu-id="4d8f3-165">To get SSO configured for your application, contact Synergi support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-165">To get SSO configured for your application, contact Synergi support team and provide them with the following:</span></span>
   
  * <span data-ttu-id="4d8f3-166">The downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="4d8f3-166">The downloaded certificate</span></span>
  * <span data-ttu-id="4d8f3-167">The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="4d8f3-167">The **Entity ID**</span></span> 
  * <span data-ttu-id="4d8f3-168">The **Single Sign Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="4d8f3-168">The **Single Sign Out Service URL**</span></span>

6. <span data-ttu-id="4d8f3-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="4d8f3-171">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4d8f3-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4d8f3-173">Create an Azure AD test user</span></span>
<span data-ttu-id="4d8f3-174">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="4d8f3-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4d8f3-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4d8f3-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="4d8f3-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="4d8f3-180">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-180">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d8f3-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="4d8f3-184">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="4d8f3-186">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="4d8f3-187">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="4d8f3-188">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-188">Click **Next**.</span></span>

6. <span data-ttu-id="4d8f3-189">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-189">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="4d8f3-191">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="4d8f3-192">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="4d8f3-193">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="4d8f3-194">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="4d8f3-195">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-195">Click **Next**.</span></span>

7. <span data-ttu-id="4d8f3-196">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-196">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="4d8f3-198">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4d8f3-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="4d8f3-200">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="4d8f3-201">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-201">Click **Complete**.</span></span>   

### <a name="create-an-synergi-test-user"></a><span data-ttu-id="4d8f3-202">Create an Synergi test user</span><span class="sxs-lookup"><span data-stu-id="4d8f3-202">Create an Synergi test user</span></span>
<span data-ttu-id="4d8f3-203">In this section, you create a user called Britta Simon in Synergi.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-203">In this section, you create a user called Britta Simon in Synergi.</span></span> <span data-ttu-id="4d8f3-204">Please work with Synergi support team to add the users in the Synergi platform.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-204">Please work with Synergi support team to add the users in the Synergi platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4d8f3-205">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4d8f3-205">Assign the Azure AD test user</span></span>
<span data-ttu-id="4d8f3-206">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Synergi.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-206">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Synergi.</span></span>

![Assign User][200] 

<span data-ttu-id="4d8f3-208">**To assign Britta Simon to Synergi, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4d8f3-208">**To assign Britta Simon to Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="4d8f3-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="4d8f3-211">In the applications list, select **Synergi**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-211">In the applications list, select **Synergi**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_synergi_50.png) 

3. <span data-ttu-id="4d8f3-213">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-213">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]

4. <span data-ttu-id="4d8f3-215">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="4d8f3-216">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-216">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="4d8f3-218">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="4d8f3-218">Test single sign-on</span></span>
<span data-ttu-id="4d8f3-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4d8f3-220">When you click the Synergi tile in the Access Panel, you should get automatically signed-on to your Synergi application.</span><span class="sxs-lookup"><span data-stu-id="4d8f3-220">When you click the Synergi tile in the Access Panel, you should get automatically signed-on to your Synergi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4d8f3-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4d8f3-221">Additional resources</span></span>
* [<span data-ttu-id="4d8f3-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d8f3-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d8f3-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d8f3-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-synergi-tutorial/tutorial_general_205.png
























