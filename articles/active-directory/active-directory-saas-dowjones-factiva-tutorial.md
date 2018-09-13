---
title: 'Tutorial: Azure Active Directory integration with Dow Jones Factiva | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Dow Jones Factiva.
services: active-directory
documentationCenter: na
authors: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/17/2016
ms.author: jeedes
ms.openlocfilehash: 9e5a5481ba331074e4702c1691c1e1f976fb4899
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554506"
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="01db7-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="01db7-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="01db7-104">In this tutorial, you learn how to integrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="01db7-104">In this tutorial, you learn how to integrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01db7-105">Integrating Dow Jones Factiva with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="01db7-105">Integrating Dow Jones Factiva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="01db7-106">You can control in Azure AD who has access to Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="01db7-106">You can control in Azure AD who has access to Dow Jones Factiva</span></span>
- <span data-ttu-id="01db7-107">You can enable your users to automatically get signed-on to Dow Jones Factiva (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="01db7-107">You can enable your users to automatically get signed-on to Dow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="01db7-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="01db7-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="01db7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="01db7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01db7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="01db7-110">Prerequisites</span></span>

<span data-ttu-id="01db7-111">To configure Azure AD integration with Dow Jones Factiva, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="01db7-111">To configure Azure AD integration with Dow Jones Factiva, you need the following items:</span></span>

- <span data-ttu-id="01db7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="01db7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="01db7-113">A Dow Jones Factiva single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="01db7-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="01db7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="01db7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="01db7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="01db7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="01db7-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="01db7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="01db7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="01db7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="01db7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="01db7-118">Scenario description</span></span>
<span data-ttu-id="01db7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="01db7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="01db7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="01db7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01db7-121">Adding Dow Jones Factiva from the gallery</span><span class="sxs-lookup"><span data-stu-id="01db7-121">Adding Dow Jones Factiva from the gallery</span></span>
2. <span data-ttu-id="01db7-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="01db7-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-dow-jones-factiva-from-the-gallery"></a><span data-ttu-id="01db7-123">Adding Dow Jones Factiva from the gallery</span><span class="sxs-lookup"><span data-stu-id="01db7-123">Adding Dow Jones Factiva from the gallery</span></span>
<span data-ttu-id="01db7-124">To configure the integration of Dow Jones Factiva into Azure AD, you need to add Dow Jones Factiva from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="01db7-124">To configure the integration of Dow Jones Factiva into Azure AD, you need to add Dow Jones Factiva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="01db7-125">**To add Dow Jones Factiva from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="01db7-125">**To add Dow Jones Factiva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="01db7-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01db7-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="01db7-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="01db7-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="01db7-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="01db7-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="01db7-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="01db7-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="01db7-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="01db7-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="01db7-135">In the search box, type **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="01db7-135">In the search box, type **Dow Jones Factiva**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_01.png)

7. <span data-ttu-id="01db7-137">In the results pane, select **Dow Jones Factiva**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="01db7-137">In the results pane, select **Dow Jones Factiva**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="01db7-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="01db7-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="01db7-140">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="01db7-140">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="01db7-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Dow Jones Factiva is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01db7-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Dow Jones Factiva is to a user in Azure AD.</span></span> <span data-ttu-id="01db7-142">In other words, a link relationship between an Azure AD user and the related user in Dow Jones Factiva needs to be established.</span><span class="sxs-lookup"><span data-stu-id="01db7-142">In other words, a link relationship between an Azure AD user and the related user in Dow Jones Factiva needs to be established.</span></span>

<span data-ttu-id="01db7-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="01db7-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dow Jones Factiva.</span></span>

<span data-ttu-id="01db7-144">To configure and test Azure AD single sign-on with Dow Jones Factiva, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="01db7-144">To configure and test Azure AD single sign-on with Dow Jones Factiva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="01db7-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="01db7-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="01db7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01db7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="01db7-147">**[Creating a Dow Jones Factiva test user](#creating-a-dowjones-factiva-test-user)** - to have a counterpart of Britta Simon in Dow Jones Factiva that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="01db7-147">**[Creating a Dow Jones Factiva test user](#creating-a-dowjones-factiva-test-user)** - to have a counterpart of Britta Simon in Dow Jones Factiva that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="01db7-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="01db7-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="01db7-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="01db7-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="01db7-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="01db7-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="01db7-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Dow Jones Factiva application.</span><span class="sxs-lookup"><span data-stu-id="01db7-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Dow Jones Factiva application.</span></span>


<span data-ttu-id="01db7-152">**To configure Azure AD single sign-on with Dow Jones Factiva, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="01db7-152">**To configure Azure AD single sign-on with Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="01db7-153">In the classic portal, on the **Dow Jones Factiva** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="01db7-153">In the classic portal, on the **Dow Jones Factiva** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="01db7-155">On the **How would you like users to sign on to Dow Jones Factiva** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01db7-155">On the **How would you like users to sign on to Dow Jones Factiva** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_03.png) 

3. <span data-ttu-id="01db7-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="01db7-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="01db7-158">a.</span><span class="sxs-lookup"><span data-stu-id="01db7-158">a.</span></span> <span data-ttu-id="01db7-159">click **Next**</span><span class="sxs-lookup"><span data-stu-id="01db7-159">click **Next**</span></span>
 
4. <span data-ttu-id="01db7-160">On the **Configure single sign-on at Dow Jones Factiva** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="01db7-160">On the **Configure single sign-on at Dow Jones Factiva** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_05.png)

    <span data-ttu-id="01db7-162">a.</span><span class="sxs-lookup"><span data-stu-id="01db7-162">a.</span></span> <span data-ttu-id="01db7-163">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="01db7-163">Click **Download metadata**, and then save the file on your computer.</span></span>

    <span data-ttu-id="01db7-164">b.</span><span class="sxs-lookup"><span data-stu-id="01db7-164">b.</span></span> <span data-ttu-id="01db7-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01db7-165">Click **Next**.</span></span>


5. <span data-ttu-id="01db7-166">To get SSO configured for your application, contact Dow Jones Factiva support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="01db7-166">To get SSO configured for your application, contact Dow Jones Factiva support team and provide them with the following:</span></span>

    <span data-ttu-id="01db7-167">• The downloaded **metadata**</span><span class="sxs-lookup"><span data-stu-id="01db7-167">• The downloaded **metadata**</span></span>

6. <span data-ttu-id="01db7-168">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01db7-168">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="01db7-170">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="01db7-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="01db7-172">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="01db7-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="01db7-173">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01db7-173">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Create Azure AD User][20]

<span data-ttu-id="01db7-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="01db7-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="01db7-176">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01db7-176">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="01db7-178">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="01db7-178">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="01db7-179">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="01db7-179">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="01db7-181">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="01db7-181">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="01db7-183">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="01db7-183">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="01db7-184">a.</span><span class="sxs-lookup"><span data-stu-id="01db7-184">a.</span></span> <span data-ttu-id="01db7-185">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="01db7-185">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="01db7-186">b.</span><span class="sxs-lookup"><span data-stu-id="01db7-186">b.</span></span> <span data-ttu-id="01db7-187">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="01db7-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="01db7-188">c.</span><span class="sxs-lookup"><span data-stu-id="01db7-188">c.</span></span> <span data-ttu-id="01db7-189">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01db7-189">Click **Next**.</span></span>

6.  <span data-ttu-id="01db7-190">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="01db7-190">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="01db7-191">a.</span><span class="sxs-lookup"><span data-stu-id="01db7-191">a.</span></span> <span data-ttu-id="01db7-192">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="01db7-192">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="01db7-193">b.</span><span class="sxs-lookup"><span data-stu-id="01db7-193">b.</span></span> <span data-ttu-id="01db7-194">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="01db7-194">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="01db7-195">c.</span><span class="sxs-lookup"><span data-stu-id="01db7-195">c.</span></span> <span data-ttu-id="01db7-196">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="01db7-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="01db7-197">d.</span><span class="sxs-lookup"><span data-stu-id="01db7-197">d.</span></span> <span data-ttu-id="01db7-198">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="01db7-198">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="01db7-199">e.</span><span class="sxs-lookup"><span data-stu-id="01db7-199">e.</span></span> <span data-ttu-id="01db7-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01db7-200">Click **Next**.</span></span>

7. <span data-ttu-id="01db7-201">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="01db7-201">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="01db7-203">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="01db7-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="01db7-205">a.</span><span class="sxs-lookup"><span data-stu-id="01db7-205">a.</span></span> <span data-ttu-id="01db7-206">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="01db7-206">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="01db7-207">b.</span><span class="sxs-lookup"><span data-stu-id="01db7-207">b.</span></span> <span data-ttu-id="01db7-208">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="01db7-208">Click **Complete**.</span></span>   



### <a name="creating-an-dow-jones-factiva-test-user"></a><span data-ttu-id="01db7-209">Creating an Dow Jones Factiva test user</span><span class="sxs-lookup"><span data-stu-id="01db7-209">Creating an Dow Jones Factiva test user</span></span>

<span data-ttu-id="01db7-210">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="01db7-210">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="01db7-211">Please work with Dow Jones Factiva support team to add the users in the Dow Jones Factiva platform.</span><span class="sxs-lookup"><span data-stu-id="01db7-211">Please work with Dow Jones Factiva support team to add the users in the Dow Jones Factiva platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="01db7-212">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="01db7-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="01db7-213">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="01db7-213">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Dow Jones Factiva.</span></span>

![Assign User][200] 

<span data-ttu-id="01db7-215">**To assign Britta Simon to Dow Jones Factiva, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="01db7-215">**To assign Britta Simon to Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="01db7-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="01db7-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="01db7-218">In the applications list, select **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="01db7-218">In the applications list, select **Dow Jones Factiva**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_50.png) 

3. <span data-ttu-id="01db7-220">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="01db7-220">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203]

4. <span data-ttu-id="01db7-222">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="01db7-222">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="01db7-223">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="01db7-223">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assign User][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="01db7-225">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="01db7-225">Testing Single Sign-On</span></span>

<span data-ttu-id="01db7-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="01db7-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="01db7-227">When you click the Dow Jones Factiva tile in the Access Panel, you should get automatically signed-on to your Dow Jones Factiva application.</span><span class="sxs-lookup"><span data-stu-id="01db7-227">When you click the Dow Jones Factiva tile in the Access Panel, you should get automatically signed-on to your Dow Jones Factiva application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="01db7-228">Additional resources</span><span class="sxs-lookup"><span data-stu-id="01db7-228">Additional resources</span></span>

* [<span data-ttu-id="01db7-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01db7-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01db7-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="01db7-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_205.png
























