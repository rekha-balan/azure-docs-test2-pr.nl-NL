---
title: 'Tutorial: Azure Active Directory integration with Oneteam | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Oneteam.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: d0dc7dc75e22f0129988883056216abbd3421acc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563244"
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="816bf-103">Tutorial: Azure Active Directory integration with Oneteam</span><span class="sxs-lookup"><span data-stu-id="816bf-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="816bf-104">In this tutorial, you learn how to integrate Oneteam with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="816bf-104">In this tutorial, you learn how to integrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="816bf-105">Integrating Oneteam with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="816bf-105">Integrating Oneteam with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="816bf-106">You can control in Azure AD who has access to Oneteam</span><span class="sxs-lookup"><span data-stu-id="816bf-106">You can control in Azure AD who has access to Oneteam</span></span>
- <span data-ttu-id="816bf-107">You can enable your users to automatically get signed-on to Oneteam single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="816bf-107">You can enable your users to automatically get signed-on to Oneteam single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="816bf-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="816bf-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="816bf-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="816bf-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="816bf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="816bf-110">Prerequisites</span></span>

<span data-ttu-id="816bf-111">To configure Azure AD integration with Oneteam, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="816bf-111">To configure Azure AD integration with Oneteam, you need the following items:</span></span>

- <span data-ttu-id="816bf-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="816bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="816bf-113">A Oneteam SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="816bf-113">A Oneteam SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="816bf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="816bf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="816bf-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="816bf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="816bf-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="816bf-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="816bf-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="816bf-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="816bf-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="816bf-118">Scenario description</span></span>
<span data-ttu-id="816bf-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="816bf-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="816bf-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="816bf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="816bf-121">Adding Oneteam from the gallery</span><span class="sxs-lookup"><span data-stu-id="816bf-121">Adding Oneteam from the gallery</span></span>
2. <span data-ttu-id="816bf-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="816bf-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-oneteam-from-the-gallery"></a><span data-ttu-id="816bf-123">Add Oneteam from the gallery</span><span class="sxs-lookup"><span data-stu-id="816bf-123">Add Oneteam from the gallery</span></span>
<span data-ttu-id="816bf-124">To configure the integration of Oneteam into Azure AD, you need to add Oneteam from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="816bf-124">To configure the integration of Oneteam into Azure AD, you need to add Oneteam from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="816bf-125">**To add Oneteam from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="816bf-125">**To add Oneteam from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="816bf-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="816bf-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="816bf-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="816bf-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="816bf-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="816bf-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="816bf-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="816bf-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="816bf-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="816bf-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="816bf-135">In the search box, type **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="816bf-135">In the search box, type **Oneteam**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_001.png)

7. <span data-ttu-id="816bf-137">In the results pane, select **Oneteam**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="816bf-137">In the results pane, select **Oneteam**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="816bf-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="816bf-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="816bf-140">In this section, you configure and test Azure AD SSO with Oneteam based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="816bf-140">In this section, you configure and test Azure AD SSO with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="816bf-141">For SSO to work, Azure AD needs to know what the counterpart user in Oneteam is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="816bf-141">For SSO to work, Azure AD needs to know what the counterpart user in Oneteam is to a user in Azure AD.</span></span> <span data-ttu-id="816bf-142">In other words, a link relationship between an Azure AD user and the related user in Oneteam needs to be established.</span><span class="sxs-lookup"><span data-stu-id="816bf-142">In other words, a link relationship between an Azure AD user and the related user in Oneteam needs to be established.</span></span>

<span data-ttu-id="816bf-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Oneteam.</span><span class="sxs-lookup"><span data-stu-id="816bf-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Oneteam.</span></span>

<span data-ttu-id="816bf-144">To configure and test Azure AD SSO with Oneteam, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="816bf-144">To configure and test Azure AD SSO with Oneteam, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="816bf-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="816bf-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="816bf-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="816bf-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="816bf-147">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - to have a counterpart of Britta Simon in Oneteam that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="816bf-147">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - to have a counterpart of Britta Simon in Oneteam that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="816bf-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="816bf-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="816bf-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="816bf-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="816bf-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="816bf-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="816bf-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Oneteam application.</span><span class="sxs-lookup"><span data-stu-id="816bf-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Oneteam application.</span></span>


<span data-ttu-id="816bf-152">**To configure Azure AD single sign-on with Oneteam, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="816bf-152">**To configure Azure AD single sign-on with Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="816bf-153">In the classic portal, on the **Oneteam** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span><span class="sxs-lookup"><span data-stu-id="816bf-153">In the classic portal, on the **Oneteam** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span></span>

    ![Configure Single Sign-On][6]

2. <span data-ttu-id="816bf-155">On the **How would you like users to sign on to Oneteam** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="816bf-155">On the **How would you like users to sign on to Oneteam** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_02.png)

3. <span data-ttu-id="816bf-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="816bf-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_03.png)
  1. <span data-ttu-id="816bf-159">In the **Identifier** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/issuer`.</span><span class="sxs-lookup"><span data-stu-id="816bf-159">In the **Identifier** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/issuer`.</span></span>
  2. <span data-ttu-id="816bf-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`.</span><span class="sxs-lookup"><span data-stu-id="816bf-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`.</span></span>
  3. <span data-ttu-id="816bf-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="816bf-161">Click **Next**.</span></span>

4. <span data-ttu-id="816bf-162">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="816bf-162">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_04.png)
  1. <span data-ttu-id="816bf-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<team name>.one-team.io/`.</span><span class="sxs-lookup"><span data-stu-id="816bf-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<team name>.one-team.io/`.</span></span>
  2. <span data-ttu-id="816bf-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="816bf-165">Click **Next**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="816bf-166">Please note that you have to update these values with the actual Sign On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="816bf-166">Please note that you have to update these values with the actual Sign On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="816bf-167">You can raise the support ticket with Oneteam from <a href="https://support.one-team.com/hc/en-us/requests/new">here</a> to get these values.</span><span class="sxs-lookup"><span data-stu-id="816bf-167">You can raise the support ticket with Oneteam from <a href="https://support.one-team.com/hc/en-us/requests/new">here</a> to get these values.</span></span>
    >

5. <span data-ttu-id="816bf-168">On the **Configure single sign-on at Oneteam** page, click **Download metadata** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="816bf-168">On the **Configure single sign-on at Oneteam** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_05.png) 

6. <span data-ttu-id="816bf-170">To get SSO configured for your application, you can raise the support ticket with Oneteam  support team from <a href="https://support.one-team.com/hc/en-us/requests/new">here</a> and provide them with the downloaded **Metadata**.</span><span class="sxs-lookup"><span data-stu-id="816bf-170">To get SSO configured for your application, you can raise the support ticket with Oneteam  support team from <a href="https://support.one-team.com/hc/en-us/requests/new">here</a> and provide them with the downloaded **Metadata**.</span></span>

7. <span data-ttu-id="816bf-171">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="816bf-171">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD Single Sign-On][10]

8. <span data-ttu-id="816bf-173">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="816bf-173">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="816bf-175">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="816bf-175">Create an Azure AD test user</span></span>
<span data-ttu-id="816bf-176">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="816bf-176">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="816bf-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="816bf-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="816bf-179">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="816bf-179">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="816bf-181">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="816bf-181">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="816bf-182">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="816bf-182">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="816bf-184">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="816bf-184">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="816bf-186">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="816bf-186">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="816bf-188">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="816bf-188">As Type Of User, select New user in your organization.</span></span>
 2. <span data-ttu-id="816bf-189">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="816bf-189">In the User Name **textbox**, type **BrittaSimon**.</span></span>
 3. <span data-ttu-id="816bf-190">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="816bf-190">Click **Next**.</span></span>

6.  <span data-ttu-id="816bf-191">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="816bf-191">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/create_aaduser_06.png) 
 1. <span data-ttu-id="816bf-193">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="816bf-193">In the **First Name** textbox, type **Britta**.</span></span>  
 2. <span data-ttu-id="816bf-194">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="816bf-194">In the **Last Name** textbox, type, **Simon**.</span></span>
 3. <span data-ttu-id="816bf-195">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="816bf-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>
 4. <span data-ttu-id="816bf-196">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="816bf-196">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="816bf-197">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="816bf-197">Click **Next**.</span></span>

7. <span data-ttu-id="816bf-198">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="816bf-198">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="816bf-200">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="816bf-200">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="816bf-202">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="816bf-202">Write down the value of the **New Password**.</span></span>
 2. <span data-ttu-id="816bf-203">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="816bf-203">Click **Complete**.</span></span>   

### <a name="create-a-oneteam-test-user"></a><span data-ttu-id="816bf-204">Create a Oneteam test user</span><span class="sxs-lookup"><span data-stu-id="816bf-204">Create a Oneteam test user</span></span>

<span data-ttu-id="816bf-205">The objective of this section is to create a user called Britta Simon in Oneteam.</span><span class="sxs-lookup"><span data-stu-id="816bf-205">The objective of this section is to create a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="816bf-206">Oneteam supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="816bf-206">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="816bf-207">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="816bf-207">There is no action item for you in this section.</span></span> <span data-ttu-id="816bf-208">A new user will be created during an attempt to access Oneteam if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="816bf-208">A new user will be created during an attempt to access Oneteam if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="816bf-209">If you need to create an user manually, you can raise the support ticket with Oneteam  support team from <a href="https://support.one-team.com/hc/en-us/requests/new">here</a>.</span><span class="sxs-lookup"><span data-stu-id="816bf-209">If you need to create an user manually, you can raise the support ticket with Oneteam  support team from <a href="https://support.one-team.com/hc/en-us/requests/new">here</a>.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="816bf-210">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="816bf-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="816bf-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Oneteam.</span><span class="sxs-lookup"><span data-stu-id="816bf-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Oneteam.</span></span>

![Assign User][200] 

<span data-ttu-id="816bf-213">**To assign Britta Simon to Oneteam, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="816bf-213">**To assign Britta Simon to Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="816bf-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="816bf-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="816bf-216">In the applications list, select **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="816bf-216">In the applications list, select **Oneteam**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_50.png) 

3. <span data-ttu-id="816bf-218">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="816bf-218">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203] 

4. <span data-ttu-id="816bf-220">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="816bf-220">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="816bf-221">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="816bf-221">In the toolbar on the bottom, click **Assign**.</span></span>
    
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="816bf-223">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="816bf-223">Test single sign-on</span></span>

<span data-ttu-id="816bf-224">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="816bf-224">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="816bf-225">When you click the Oneteam tile in the Access Panel, you should get automatically signed-on to your Oneteam application.</span><span class="sxs-lookup"><span data-stu-id="816bf-225">When you click the Oneteam tile in the Access Panel, you should get automatically signed-on to your Oneteam application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="816bf-226">Additional resources</span><span class="sxs-lookup"><span data-stu-id="816bf-226">Additional resources</span></span>

* [<span data-ttu-id="816bf-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="816bf-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="816bf-228">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="816bf-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oneteam-tutorial/tutorial_general_205.png


























