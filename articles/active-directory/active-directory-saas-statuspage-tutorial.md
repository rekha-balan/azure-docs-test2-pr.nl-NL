---
title: 'Tutorial: Azure Active Directory integration with StatusPage | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and StatusPage.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: jeedes
ms.openlocfilehash: b0df0bc6d9a04bd000e506064054f00c141d8d3f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553399"
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="0ecea-103">Tutorial: Azure Active Directory integration with StatusPage</span><span class="sxs-lookup"><span data-stu-id="0ecea-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>
<span data-ttu-id="0ecea-104">The objective of this tutorial is to show you how to integrate StatusPage with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ecea-104">The objective of this tutorial is to show you how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ecea-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0ecea-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="0ecea-106">You can control in Azure AD who has access to StatusPage</span><span class="sxs-lookup"><span data-stu-id="0ecea-106">You can control in Azure AD who has access to StatusPage</span></span> 
* <span data-ttu-id="0ecea-107">You can enable your users to automatically get signed-on to StatusPage single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="0ecea-107">You can enable your users to automatically get signed-on to StatusPage single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="0ecea-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="0ecea-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="0ecea-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ecea-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ecea-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0ecea-110">Prerequisites</span></span>
<span data-ttu-id="0ecea-111">To configure Azure AD integration with StatusPage, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0ecea-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

* <span data-ttu-id="0ecea-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0ecea-112">An Azure AD subscription</span></span>
* <span data-ttu-id="0ecea-113">A StatusPage single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0ecea-113">A StatusPage single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="0ecea-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0ecea-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="0ecea-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0ecea-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="0ecea-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="0ecea-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="0ecea-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ecea-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="0ecea-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="0ecea-118">Scenario Description</span></span>
<span data-ttu-id="0ecea-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0ecea-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="0ecea-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0ecea-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="0ecea-121">Adding StatusPage from the gallery</span><span class="sxs-lookup"><span data-stu-id="0ecea-121">Adding StatusPage from the gallery</span></span> 
* <span data-ttu-id="0ecea-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="0ecea-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-statuspage-from-the-gallery"></a><span data-ttu-id="0ecea-123">Add StatusPage from the gallery</span><span class="sxs-lookup"><span data-stu-id="0ecea-123">Add StatusPage from the gallery</span></span>
<span data-ttu-id="0ecea-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0ecea-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0ecea-125">**To add StatusPage from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0ecea-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0ecea-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="0ecea-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="0ecea-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="0ecea-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="0ecea-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="0ecea-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="0ecea-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="0ecea-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="0ecea-135">In the search box, type **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-135">In the search box, type **StatusPage**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_01.png)
7. <span data-ttu-id="0ecea-137">In the results pane, select **StatusPage**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="0ecea-137">In the results pane, select **StatusPage**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="0ecea-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="0ecea-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="0ecea-140">The objective of this section is to show you how to configure and test Azure AD SSO with StatusPage based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0ecea-140">The objective of this section is to show you how to configure and test Azure AD SSO with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ecea-141">For SSO to work, Azure AD needs to know what the counterpart user in StatusPage to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="0ecea-141">For SSO to work, Azure AD needs to know what the counterpart user in StatusPage to an user in Azure AD is.</span></span> <span data-ttu-id="0ecea-142">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0ecea-142">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="0ecea-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in StatusPage.</span><span class="sxs-lookup"><span data-stu-id="0ecea-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in StatusPage.</span></span>

<span data-ttu-id="0ecea-144">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0ecea-144">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0ecea-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0ecea-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0ecea-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0ecea-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ecea-147">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="0ecea-147">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="0ecea-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0ecea-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ecea-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0ecea-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0ecea-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0ecea-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="0ecea-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your StatusPage application.</span><span class="sxs-lookup"><span data-stu-id="0ecea-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your StatusPage application.</span></span> 

<span data-ttu-id="0ecea-152">**To configure Azure AD SSO with StatusPage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0ecea-152">**To configure Azure AD SSO with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="0ecea-153">In the Azure classic portal, on the **StatusPage** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="0ecea-153">In the Azure classic portal, on the **StatusPage** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="0ecea-155">On the **How would you like users to sign on to StatusPage** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-155">On the **How would you like users to sign on to StatusPage** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_03.png) 
3. <span data-ttu-id="0ecea-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0ecea-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_04.png) 
   
   >[!NOTE]
   ><span data-ttu-id="0ecea-159">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0ecea-159">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
   > 
  1. <span data-ttu-id="0ecea-160">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span><span class="sxs-lookup"><span data-stu-id="0ecea-160">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
  2. <span data-ttu-id="0ecea-161">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0ecea-161">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>
  3. <span data-ttu-id="0ecea-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-162">Click **Next**.</span></span>

4. <span data-ttu-id="0ecea-163">On the **Configure single sign-on at StatusPage** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0ecea-163">On the **Configure single sign-on at StatusPage** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_05.png)   
  1. <span data-ttu-id="0ecea-165">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0ecea-165">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="0ecea-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-166">Click **Next**.</span></span>
5. <span data-ttu-id="0ecea-167">In another browser window, sign on to your StatusPage company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0ecea-167">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>
6. <span data-ttu-id="0ecea-168">In the main toolbar, click **Manage Account**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-168">In the main toolbar, click **Manage Account**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 
7. <span data-ttu-id="0ecea-170">Click the **Single Sign-on** tab.</span><span class="sxs-lookup"><span data-stu-id="0ecea-170">Click the **Single Sign-on** tab.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 
8. <span data-ttu-id="0ecea-172">On the SSO Setup page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0ecea-172">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png)  
  1. <span data-ttu-id="0ecea-174">In the Azure classic portal, on the **Configure single sign-on at StatusPage** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **SSO Target URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0ecea-174">In the Azure classic portal, on the **Configure single sign-on at StatusPage** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **SSO Target URL** textbox.</span></span> 
  2. <span data-ttu-id="0ecea-175">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="0ecea-175">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 
  3. <span data-ttu-id="0ecea-176">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-176">Click **Save**.</span></span>
9. <span data-ttu-id="0ecea-177">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-177">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Single Sign-On][10]
10. <span data-ttu-id="0ecea-179">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-179">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0ecea-181">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0ecea-181">Create an Azure AD test user</span></span>
<span data-ttu-id="0ecea-182">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0ecea-182">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="0ecea-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0ecea-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0ecea-185">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-185">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="0ecea-187">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="0ecea-187">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="0ecea-188">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-188">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="0ecea-190">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-190">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="0ecea-192">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0ecea-192">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="0ecea-194">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="0ecea-194">As Type Of User, select New user in your organization.</span></span>  
  2. <span data-ttu-id="0ecea-195">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-195">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="0ecea-196">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-196">Click **Next**.</span></span>
6. <span data-ttu-id="0ecea-197">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0ecea-197">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/create_aaduser_06.png)  
  1. <span data-ttu-id="0ecea-199">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-199">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="0ecea-200">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-200">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="0ecea-201">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-201">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="0ecea-202">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-202">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="0ecea-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-203">Click **Next**.</span></span>
7. <span data-ttu-id="0ecea-204">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-204">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="0ecea-206">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0ecea-206">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="0ecea-208">Write down the value of the **New Password**</span><span class="sxs-lookup"><span data-stu-id="0ecea-208">Write down the value of the **New Password**</span></span>  
  2. <span data-ttu-id="0ecea-209">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-209">Click **Complete**.</span></span>   

### <a name="create-a-statuspage-test-user"></a><span data-ttu-id="0ecea-210">Create a StatusPage test user</span><span class="sxs-lookup"><span data-stu-id="0ecea-210">Create a StatusPage test user</span></span>
<span data-ttu-id="0ecea-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span><span class="sxs-lookup"><span data-stu-id="0ecea-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="0ecea-212">StatusPage supports just-in-time provisioning.</span><span class="sxs-lookup"><span data-stu-id="0ecea-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="0ecea-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="0ecea-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

<span data-ttu-id="0ecea-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0ecea-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="0ecea-215">Sign-on to your StatusPage company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0ecea-215">Sign-on to your StatusPage company site as an administrator.</span></span>
2. <span data-ttu-id="0ecea-216">In the menu on the top, click **Manage Account**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-216">In the menu on the top, click **Manage Account**.</span></span>
3. <span data-ttu-id="0ecea-217">Click the Team Members tab.</span><span class="sxs-lookup"><span data-stu-id="0ecea-217">Click the Team Members tab.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 
4. <span data-ttu-id="0ecea-219">Click **Add Team Member**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-219">Click **Add Team Member**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 
5. <span data-ttu-id="0ecea-221">Type the **Email Address**, **First Name** and **Sur Name** of a valid user you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="0ecea-221">Type the **Email Address**, **First Name** and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 
6. <span data-ttu-id="0ecea-223">As **Role**, choose **Client Administrator**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-223">As **Role**, choose **Client Administrator**.</span></span>
7. <span data-ttu-id="0ecea-224">Click **Create Account**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-224">Click **Create Account**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0ecea-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0ecea-225">Assign the Azure AD test user</span></span>
<span data-ttu-id="0ecea-226">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to StatusPage.</span><span class="sxs-lookup"><span data-stu-id="0ecea-226">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to StatusPage.</span></span>

![Assign User][200] 

<span data-ttu-id="0ecea-228">**To assign Britta Simon to StatusPage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0ecea-228">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="0ecea-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="0ecea-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="0ecea-231">In the applications list, select **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-231">In the applications list, select **StatusPage**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_50.png) 
3. <span data-ttu-id="0ecea-233">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-233">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="0ecea-235">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-235">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="0ecea-236">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="0ecea-236">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="0ecea-238">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="0ecea-238">Test single sign-on</span></span>
<span data-ttu-id="0ecea-239">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0ecea-239">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0ecea-240">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span><span class="sxs-lookup"><span data-stu-id="0ecea-240">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ecea-241">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="0ecea-241">Additional Resources</span></span>
* [<span data-ttu-id="0ecea-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ecea-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ecea-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0ecea-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-statuspage-tutorial/tutorial_general_205.png




































