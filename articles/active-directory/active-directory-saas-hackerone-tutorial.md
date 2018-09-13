---
title: 'Tutorial: Azure Active Directory integration with HackerOne | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HackerOne.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: jeedes
ms.openlocfilehash: 4f6c7b09a7fcdf450163ac7ecd3113d4c4aac806
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660523"
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="362a9-103">Tutorial: Azure Active Directory integration with HackerOne</span><span class="sxs-lookup"><span data-stu-id="362a9-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>
<span data-ttu-id="362a9-104">In this tutorial, you integrate HackerOne with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="362a9-104">In this tutorial, you integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="362a9-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="362a9-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="362a9-106">You can control in Azure AD who has access to HackerOne</span><span class="sxs-lookup"><span data-stu-id="362a9-106">You can control in Azure AD who has access to HackerOne</span></span>
* <span data-ttu-id="362a9-107">You can enable your users to automatically get signed-on to HackerOne single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="362a9-107">You can enable your users to automatically get signed-on to HackerOne single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="362a9-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="362a9-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="362a9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="362a9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="362a9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="362a9-110">Prerequisites</span></span>
<span data-ttu-id="362a9-111">To configure Azure AD integration with HackerOne, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="362a9-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

* <span data-ttu-id="362a9-112">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="362a9-112">An Azure subscription</span></span>
* <span data-ttu-id="362a9-113">A HackerOne SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="362a9-113">A HackerOne SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="362a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="362a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="362a9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="362a9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="362a9-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="362a9-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="362a9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="362a9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="362a9-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="362a9-118">Scenario Description</span></span>
<span data-ttu-id="362a9-119">In this tutorial, you configure and test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="362a9-119">In this tutorial, you configure and test Azure AD single sign-on in a test environment.</span></span>  

<span data-ttu-id="362a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="362a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

*  <span data-ttu-id="362a9-121">Adding HackerOne from the gallery</span><span class="sxs-lookup"><span data-stu-id="362a9-121">Adding HackerOne from the gallery</span></span>
*  <span data-ttu-id="362a9-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="362a9-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-hackerone-from-the-gallery"></a><span data-ttu-id="362a9-123">Add HackerOne from the gallery</span><span class="sxs-lookup"><span data-stu-id="362a9-123">Add HackerOne from the gallery</span></span>
<span data-ttu-id="362a9-124">To integrate HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="362a9-124">To integrate HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="362a9-125">**To add HackerOne from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="362a9-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="362a9-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="362a9-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="362a9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="362a9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="362a9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="362a9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="362a9-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="362a9-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="362a9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="362a9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

  ![Applications][4]
6. <span data-ttu-id="362a9-135">In the search box, type **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="362a9-135">In the search box, type **HackerOne**.</span></span>

  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_01.png)

7. <span data-ttu-id="362a9-137">In the results pane, select **HackerOne**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="362a9-137">In the results pane, select **HackerOne**, and then click **Complete** to add the application.</span></span>

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="362a9-138">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="362a9-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="362a9-139">Next, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="362a9-139">Next, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="362a9-140">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="362a9-140">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne to an user in Azure AD is.</span></span> <span data-ttu-id="362a9-141">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span><span class="sxs-lookup"><span data-stu-id="362a9-141">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>  
<span data-ttu-id="362a9-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in HackerOne.</span><span class="sxs-lookup"><span data-stu-id="362a9-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in HackerOne.</span></span>

<span data-ttu-id="362a9-143">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="362a9-143">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="362a9-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="362a9-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="362a9-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="362a9-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="362a9-146">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="362a9-146">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="362a9-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="362a9-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="362a9-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="362a9-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="362a9-149">Configure Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="362a9-149">Configure Azure AD Single Sign-On</span></span>
<span data-ttu-id="362a9-150">Next, you enable Azure AD single sign-on in the classic portal and to configure single sign-on in your HackerOne application.</span><span class="sxs-lookup"><span data-stu-id="362a9-150">Next, you enable Azure AD single sign-on in the classic portal and to configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="362a9-151">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="362a9-151">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="362a9-152">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="362a9-152">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="362a9-153">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="362a9-153">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="362a9-154">In the Azure classic portal, on the **HackerOne** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="362a9-154">In the Azure classic portal, on the **HackerOne** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="362a9-156">On the **How would you like users to sign on to HackerOne** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="362a9-156">On the **How would you like users to sign on to HackerOne** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_03.png) 
3. <span data-ttu-id="362a9-158">On the **Configure App Settings** dialog page, perform the following steps and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="362a9-158">On the **Configure App Settings** dialog page, perform the following steps and then click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_04.png) 
    1. <span data-ttu-id="362a9-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your HackerOne application using the following pattern: **“https://hackerone.com/\<company name\>/authentication”**.</span><span class="sxs-lookup"><span data-stu-id="362a9-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your HackerOne application using the following pattern: **“https://hackerone.com/\<company name\>/authentication”**.</span></span> 
    2. <span data-ttu-id="362a9-161">Contact the HackerOne support team via [support@hackerone.com](mailto:support@hackerone.com) to get your tenant URL if you don't know it.</span><span class="sxs-lookup"><span data-stu-id="362a9-161">Contact the HackerOne support team via [support@hackerone.com](mailto:support@hackerone.com) to get your tenant URL if you don't know it.</span></span>
    3. <span data-ttu-id="362a9-162">In the **Identifier** textbox, type the tenant URL.</span><span class="sxs-lookup"><span data-stu-id="362a9-162">In the **Identifier** textbox, type the tenant URL.</span></span> 
    4. <span data-ttu-id="362a9-163">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="362a9-163">Click **Next**.</span></span>

4. <span data-ttu-id="362a9-164">On the **Configure single sign-on at HackerOne** page, perform the following steps and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="362a9-164">On the **Configure single sign-on at HackerOne** page, perform the following steps and then click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_05.png) 
    1. <span data-ttu-id="362a9-166">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="362a9-166">Click **Download certificate**, and then save the file on your computer.</span></span>
    2. <span data-ttu-id="362a9-167">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="362a9-167">Click **Next**.</span></span>
5. <span data-ttu-id="362a9-168">Sign-on to your HackerOne tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="362a9-168">Sign-on to your HackerOne tenant as an administrator.</span></span>
6. <span data-ttu-id="362a9-169">In the menu on the top, click the **Settings**.</span><span class="sxs-lookup"><span data-stu-id="362a9-169">In the menu on the top, click the **Settings**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 
7. <span data-ttu-id="362a9-171">Navigate to "**Authentication**" and click "**Add SAML settings**".</span><span class="sxs-lookup"><span data-stu-id="362a9-171">Navigate to "**Authentication**" and click "**Add SAML settings**".</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 
8. <span data-ttu-id="362a9-173">On the **SAML Settings** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="362a9-173">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 
    1. <span data-ttu-id="362a9-175">In the **Email Domain** textbox, type a registered domain.</span><span class="sxs-lookup"><span data-stu-id="362a9-175">In the **Email Domain** textbox, type a registered domain.</span></span>
    2. <span data-ttu-id="362a9-176">On the Azure classic portal, copy the **Single Sign-On Service URL**, and then paste it into the Single Sign On URL textbox.</span><span class="sxs-lookup"><span data-stu-id="362a9-176">On the Azure classic portal, copy the **Single Sign-On Service URL**, and then paste it into the Single Sign On URL textbox.</span></span>
    3. <span data-ttu-id="362a9-177">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="362a9-177">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
    
       >[!TIP] 
       ><span data-ttu-id="362a9-178">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="362a9-178">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
       >
    4. <span data-ttu-id="362a9-179">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="362a9-179">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X509 Certificate** textbox.</span></span>
    5. <span data-ttu-id="362a9-180">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="362a9-180">Click **Save**.</span></span>
9. <span data-ttu-id="362a9-181">On the Authentication Settings dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="362a9-181">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 
    1. <span data-ttu-id="362a9-183">Click **Run test**.</span><span class="sxs-lookup"><span data-stu-id="362a9-183">Click **Run test**.</span></span>
    2. <span data-ttu-id="362a9-184">If the value of the **Status** field equals **Last test status: created**, contact your HackerOne support team via [support@hackerone.com](mailto:support@hackerone.com) to request a review of your configuration.</span><span class="sxs-lookup"><span data-stu-id="362a9-184">If the value of the **Status** field equals **Last test status: created**, contact your HackerOne support team via [support@hackerone.com](mailto:support@hackerone.com) to request a review of your configuration.</span></span>
10. <span data-ttu-id="362a9-185">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="362a9-185">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
11. <span data-ttu-id="362a9-187">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="362a9-187">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="362a9-189">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="362a9-189">Create an Azure AD test user</span></span>
<span data-ttu-id="362a9-190">Next, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="362a9-190">Next, you create a test user in the classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="362a9-192">**To create a SECURE DELIVER test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="362a9-192">**To create a SECURE DELIVER test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="362a9-193">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="362a9-193">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="362a9-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="362a9-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="362a9-196">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="362a9-196">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="362a9-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="362a9-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="362a9-200">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="362a9-200">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_05.png) 
    1. <span data-ttu-id="362a9-202">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="362a9-202">As Type Of User, select New user in your organization.</span></span>
    2. <span data-ttu-id="362a9-203">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="362a9-203">In the User Name **textbox**, type **BrittaSimon**.</span></span>
    3. <span data-ttu-id="362a9-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="362a9-204">Click **Next**.</span></span>
6. <span data-ttu-id="362a9-205">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="362a9-205">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_06.png) 
   1. <span data-ttu-id="362a9-207">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="362a9-207">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="362a9-208">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="362a9-208">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="362a9-209">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="362a9-209">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="362a9-210">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="362a9-210">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="362a9-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="362a9-211">Click **Next**.</span></span>
7. <span data-ttu-id="362a9-212">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="362a9-212">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="362a9-214">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="362a9-214">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_08.png) 
    1. <span data-ttu-id="362a9-216">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="362a9-216">Write down the value of the **New Password**.</span></span>
    2. <span data-ttu-id="362a9-217">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="362a9-217">Click **Complete**.</span></span>   

### <a name="create-a-hackerone-test-user"></a><span data-ttu-id="362a9-218">Create a HackerOne test user</span><span class="sxs-lookup"><span data-stu-id="362a9-218">Create a HackerOne test user</span></span>
<span data-ttu-id="362a9-219">Next, you create a user called Britta Simon in HackerOne.</span><span class="sxs-lookup"><span data-stu-id="362a9-219">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="362a9-220">HackerOne supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="362a9-220">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="362a9-221">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="362a9-221">There is no action item for you in this section.</span></span> <span data-ttu-id="362a9-222">When you access HackerOne, a new user is created if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="362a9-222">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span> <span data-ttu-id="362a9-223">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="362a9-223">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="362a9-224">If you need to create a user manually, you need to contact the Certify support team.</span><span class="sxs-lookup"><span data-stu-id="362a9-224">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="362a9-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="362a9-225">Assign the Azure AD test user</span></span>
<span data-ttu-id="362a9-226">Next, you enable Britta Simon to use Azure single sign-on by granting her access to HackerOne.</span><span class="sxs-lookup"><span data-stu-id="362a9-226">Next, you enable Britta Simon to use Azure single sign-on by granting her access to HackerOne.</span></span>

![Assign User][200] 

<span data-ttu-id="362a9-228">**To assign Britta Simon to HackerOne, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="362a9-228">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="362a9-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="362a9-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="362a9-231">In the applications list, select **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="362a9-231">In the applications list, select **HackerOne**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_50.png) 
3. <span data-ttu-id="362a9-233">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="362a9-233">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="362a9-235">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="362a9-235">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="362a9-236">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="362a9-236">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="362a9-238">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="362a9-238">Test single sign-on</span></span>
<span data-ttu-id="362a9-239">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="362a9-239">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="362a9-240">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span><span class="sxs-lookup"><span data-stu-id="362a9-240">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="362a9-241">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="362a9-241">Additional Resources</span></span>
* [<span data-ttu-id="362a9-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="362a9-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="362a9-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="362a9-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_205.png




























