---
title: 'Tutorial: Azure Active Directory integration with JobScore | Microsoft Docs'
description: Learn how to use JobScore with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0122a7dc9a7d509af77291794d4be6f4153ca2de
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550746"
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="8669d-103">Tutorial: Azure Active Directory integration with JobScore</span><span class="sxs-lookup"><span data-stu-id="8669d-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="8669d-104">In this tutorial, you learn how to integrate JobScore with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8669d-104">In this tutorial, you learn how to integrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8669d-105">Integrating JobScore with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8669d-105">Integrating JobScore with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8669d-106">You can control in Azure AD who has access to JobScore</span><span class="sxs-lookup"><span data-stu-id="8669d-106">You can control in Azure AD who has access to JobScore</span></span>
- <span data-ttu-id="8669d-107">You can enable your users to automatically get signed-on to JobScore (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8669d-107">You can enable your users to automatically get signed-on to JobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8669d-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="8669d-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8669d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8669d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8669d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8669d-110">Prerequisites</span></span>

<span data-ttu-id="8669d-111">To configure Azure AD integration with JobScore, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8669d-111">To configure Azure AD integration with JobScore, you need the following items:</span></span>

- <span data-ttu-id="8669d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8669d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8669d-113">A JobScore single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8669d-113">A JobScore single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="8669d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8669d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="8669d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8669d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8669d-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="8669d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8669d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8669d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="8669d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8669d-118">Scenario description</span></span>
<span data-ttu-id="8669d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8669d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8669d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8669d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8669d-121">Adding JobScore from the gallery</span><span class="sxs-lookup"><span data-stu-id="8669d-121">Adding JobScore from the gallery</span></span>
2. <span data-ttu-id="8669d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8669d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-jobscore-from-the-gallery"></a><span data-ttu-id="8669d-123">Adding JobScore from the gallery</span><span class="sxs-lookup"><span data-stu-id="8669d-123">Adding JobScore from the gallery</span></span>
<span data-ttu-id="8669d-124">To configure the integration of JobScore into Azure AD, you need to add JobScore from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8669d-124">To configure the integration of JobScore into Azure AD, you need to add JobScore from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8669d-125">**To add JobScore from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8669d-125">**To add JobScore from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8669d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8669d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8669d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8669d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8669d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8669d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="8669d-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="8669d-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="8669d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="8669d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="8669d-135">In the search box, type **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="8669d-135">In the search box, type **JobScore**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_001.png)

7. <span data-ttu-id="8669d-137">In the results pane, select **JobScore**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="8669d-137">In the results pane, select **JobScore**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8669d-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8669d-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8669d-140">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8669d-140">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8669d-141">For single sign-on to work, Azure AD needs to know what the counterpart user in JobScore is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8669d-141">For single sign-on to work, Azure AD needs to know what the counterpart user in JobScore is to a user in Azure AD.</span></span> <span data-ttu-id="8669d-142">In other words, a link relationship between an Azure AD user and the related user in JobScore needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8669d-142">In other words, a link relationship between an Azure AD user and the related user in JobScore needs to be established.</span></span>

<span data-ttu-id="8669d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in JobScore.</span><span class="sxs-lookup"><span data-stu-id="8669d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in JobScore.</span></span>

<span data-ttu-id="8669d-144">To configure and test Azure AD single sign-on with JobScore, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8669d-144">To configure and test Azure AD single sign-on with JobScore, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8669d-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8669d-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8669d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8669d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8669d-147">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - to have a counterpart of Britta Simon in JobScore that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="8669d-147">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - to have a counterpart of Britta Simon in JobScore that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8669d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8669d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8669d-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8669d-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8669d-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8669d-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8669d-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your JobScore application.</span><span class="sxs-lookup"><span data-stu-id="8669d-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your JobScore application.</span></span>


<span data-ttu-id="8669d-152">**To configure Azure AD single sign-on with JobScore, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8669d-152">**To configure Azure AD single sign-on with JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="8669d-153">In the classic portal, on the **JobScore** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span><span class="sxs-lookup"><span data-stu-id="8669d-153">In the classic portal, on the **JobScore** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span></span>

    ![Configure Single Sign-On][6]

2. <span data-ttu-id="8669d-155">On the **How would you like users to sign on to JobScore** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8669d-155">On the **How would you like users to sign on to JobScore** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_02.png)

3. <span data-ttu-id="8669d-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8669d-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_03.png)

    <span data-ttu-id="8669d-159">a.</span><span class="sxs-lookup"><span data-stu-id="8669d-159">a.</span></span> <span data-ttu-id="8669d-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="8669d-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    <span data-ttu-id="8669d-161">b.</span><span class="sxs-lookup"><span data-stu-id="8669d-161">b.</span></span> <span data-ttu-id="8669d-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8669d-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8669d-163">Please note that this is not the real value.</span><span class="sxs-lookup"><span data-stu-id="8669d-163">Please note that this is not the real value.</span></span> <span data-ttu-id="8669d-164">You have to update this value with the actual Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="8669d-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="8669d-165">Contact [JobScore support team](emaiLto:support@jobscore.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="8669d-165">Contact [JobScore support team](emaiLto:support@jobscore.com) to get this value.</span></span>

4. <span data-ttu-id="8669d-166">On the **Configure single sign-on at JobScore** page, click **Download metadata** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="8669d-166">On the **Configure single sign-on at JobScore** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_04.png) 

5. <span data-ttu-id="8669d-168">To get SSO configured for your application, contact [JobScore support team](emaiLto:support@jobscore.com) and provide them with the downloaded **Metadata**.</span><span class="sxs-lookup"><span data-stu-id="8669d-168">To get SSO configured for your application, contact [JobScore support team](emaiLto:support@jobscore.com) and provide them with the downloaded **Metadata**.</span></span>

6. <span data-ttu-id="8669d-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8669d-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="8669d-171">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8669d-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD Single Sign-On][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8669d-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8669d-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="8669d-174">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8669d-174">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="8669d-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8669d-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8669d-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8669d-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="8669d-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8669d-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8669d-180">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8669d-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8669d-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="8669d-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="8669d-184">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8669d-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="8669d-186">a.</span><span class="sxs-lookup"><span data-stu-id="8669d-186">a.</span></span> <span data-ttu-id="8669d-187">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="8669d-187">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="8669d-188">b.</span><span class="sxs-lookup"><span data-stu-id="8669d-188">b.</span></span> <span data-ttu-id="8669d-189">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8669d-189">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8669d-190">c.</span><span class="sxs-lookup"><span data-stu-id="8669d-190">c.</span></span> <span data-ttu-id="8669d-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8669d-191">Click **Next**.</span></span>

6.  <span data-ttu-id="8669d-192">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8669d-192">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="8669d-194">a.</span><span class="sxs-lookup"><span data-stu-id="8669d-194">a.</span></span> <span data-ttu-id="8669d-195">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8669d-195">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="8669d-196">b.</span><span class="sxs-lookup"><span data-stu-id="8669d-196">b.</span></span> <span data-ttu-id="8669d-197">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8669d-197">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="8669d-198">c.</span><span class="sxs-lookup"><span data-stu-id="8669d-198">c.</span></span> <span data-ttu-id="8669d-199">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8669d-199">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="8669d-200">d.</span><span class="sxs-lookup"><span data-stu-id="8669d-200">d.</span></span> <span data-ttu-id="8669d-201">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="8669d-201">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="8669d-202">e.</span><span class="sxs-lookup"><span data-stu-id="8669d-202">e.</span></span> <span data-ttu-id="8669d-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8669d-203">Click **Next**.</span></span>

7. <span data-ttu-id="8669d-204">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="8669d-204">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="8669d-206">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8669d-206">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="8669d-208">a.</span><span class="sxs-lookup"><span data-stu-id="8669d-208">a.</span></span> <span data-ttu-id="8669d-209">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="8669d-209">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="8669d-210">b.</span><span class="sxs-lookup"><span data-stu-id="8669d-210">b.</span></span> <span data-ttu-id="8669d-211">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8669d-211">Click **Complete**.</span></span>   



### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="8669d-212">Creating a JobScore test user</span><span class="sxs-lookup"><span data-stu-id="8669d-212">Creating a JobScore test user</span></span>

<span data-ttu-id="8669d-213">In this section, you create a user called Britta Simon in JobScore.</span><span class="sxs-lookup"><span data-stu-id="8669d-213">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="8669d-214">Please work with [JobScore support team](emaiLto:support@jobscore.com) to add the users in the JobScore platform.</span><span class="sxs-lookup"><span data-stu-id="8669d-214">Please work with [JobScore support team](emaiLto:support@jobscore.com) to add the users in the JobScore platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8669d-215">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8669d-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8669d-216">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to JobScore.</span><span class="sxs-lookup"><span data-stu-id="8669d-216">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to JobScore.</span></span>

![Assign User][200] 

<span data-ttu-id="8669d-218">**To assign Britta Simon to JobScore, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8669d-218">**To assign Britta Simon to JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="8669d-219">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8669d-219">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="8669d-221">In the applications list, select **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="8669d-221">In the applications list, select **JobScore**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_50.png) 

3. <span data-ttu-id="8669d-223">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8669d-223">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203] 

4. <span data-ttu-id="8669d-225">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8669d-225">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="8669d-226">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="8669d-226">In the toolbar on the bottom, click **Assign**.</span></span>
    
    ![Assign User][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="8669d-228">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="8669d-228">Testing single sign-on</span></span>

<span data-ttu-id="8669d-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8669d-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8669d-230">When you click the JobScore tile in the Access Panel, you should get automatically signed-on to your JobScore application.</span><span class="sxs-lookup"><span data-stu-id="8669d-230">When you click the JobScore tile in the Access Panel, you should get automatically signed-on to your JobScore application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8669d-231">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8669d-231">Additional resources</span></span>

* [<span data-ttu-id="8669d-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8669d-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8669d-233">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8669d-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jobscore-tutorial/tutorial_general_205.png

























