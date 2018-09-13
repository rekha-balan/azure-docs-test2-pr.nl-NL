---
title: 'Tutorial: Azure Active Directory integration with Soonr Workplace | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Soonr Workplace.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 74450ce100c036f8ee7681edda43bcc063ba1ffb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550910"
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="f9c13-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="f9c13-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="f9c13-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f9c13-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="f9c13-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f9c13-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f9c13-106">You can control in Azure AD who has access to Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="f9c13-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="f9c13-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f9c13-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f9c13-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="f9c13-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="f9c13-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f9c13-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9c13-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f9c13-110">Prerequisites</span></span>

<span data-ttu-id="f9c13-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f9c13-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="f9c13-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f9c13-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9c13-113">A Soonr Workplace single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f9c13-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="f9c13-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f9c13-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="f9c13-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f9c13-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9c13-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="f9c13-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f9c13-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9c13-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f9c13-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f9c13-118">Scenario description</span></span>
<span data-ttu-id="f9c13-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f9c13-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="f9c13-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f9c13-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9c13-121">Adding Soonr Workplace from the gallery</span><span class="sxs-lookup"><span data-stu-id="f9c13-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="f9c13-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f9c13-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="f9c13-123">Adding Soonr Workplace from the gallery</span><span class="sxs-lookup"><span data-stu-id="f9c13-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="f9c13-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f9c13-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f9c13-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f9c13-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f9c13-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f9c13-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f9c13-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f9c13-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f9c13-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="f9c13-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="f9c13-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="f9c13-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![Applications][4]

6. <span data-ttu-id="f9c13-135">In the search box, type **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="f9c13-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="f9c13-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f9c13-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f9c13-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f9c13-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f9c13-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f9c13-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="f9c13-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="f9c13-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f9c13-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="f9c13-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="f9c13-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="f9c13-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f9c13-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f9c13-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f9c13-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f9c13-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9c13-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9c13-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="f9c13-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f9c13-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f9c13-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9c13-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f9c13-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f9c13-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f9c13-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f9c13-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span><span class="sxs-lookup"><span data-stu-id="f9c13-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="f9c13-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f9c13-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="f9c13-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="f9c13-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="f9c13-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="f9c13-157">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="f9c13-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="f9c13-159">a.</span><span class="sxs-lookup"><span data-stu-id="f9c13-159">a.</span></span> <span data-ttu-id="f9c13-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="f9c13-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="f9c13-161">b.</span><span class="sxs-lookup"><span data-stu-id="f9c13-161">b.</span></span> <span data-ttu-id="f9c13-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f9c13-163">Please note that this is not the real value.</span><span class="sxs-lookup"><span data-stu-id="f9c13-163">Please note that this is not the real value.</span></span> <span data-ttu-id="f9c13-164">You have to update this value with the actual Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="f9c13-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="f9c13-165">Contact Soonr Workplace support team to get this value.</span><span class="sxs-lookup"><span data-stu-id="f9c13-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="f9c13-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="f9c13-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="f9c13-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="f9c13-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="f9c13-169">•  The downloaded **Metadata** file</span><span class="sxs-lookup"><span data-stu-id="f9c13-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="f9c13-170">•  The **Issuer URL**</span><span class="sxs-lookup"><span data-stu-id="f9c13-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="f9c13-171">•  The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="f9c13-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="f9c13-172">•  The **Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="f9c13-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="f9c13-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9c13-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="f9c13-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="f9c13-176">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD Single Sign-On][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f9c13-178">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f9c13-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="f9c13-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9c13-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="f9c13-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f9c13-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f9c13-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="f9c13-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f9c13-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f9c13-185">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f9c13-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="f9c13-189">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f9c13-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="f9c13-191">a.</span><span class="sxs-lookup"><span data-stu-id="f9c13-191">a.</span></span> <span data-ttu-id="f9c13-192">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="f9c13-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="f9c13-193">b.</span><span class="sxs-lookup"><span data-stu-id="f9c13-193">b.</span></span> <span data-ttu-id="f9c13-194">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9c13-195">c.</span><span class="sxs-lookup"><span data-stu-id="f9c13-195">c.</span></span> <span data-ttu-id="f9c13-196">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-196">Click **Next**.</span></span>

6.  <span data-ttu-id="f9c13-197">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f9c13-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="f9c13-199">a.</span><span class="sxs-lookup"><span data-stu-id="f9c13-199">a.</span></span> <span data-ttu-id="f9c13-200">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="f9c13-201">b.</span><span class="sxs-lookup"><span data-stu-id="f9c13-201">b.</span></span> <span data-ttu-id="f9c13-202">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="f9c13-203">c.</span><span class="sxs-lookup"><span data-stu-id="f9c13-203">c.</span></span> <span data-ttu-id="f9c13-204">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="f9c13-205">d.</span><span class="sxs-lookup"><span data-stu-id="f9c13-205">d.</span></span> <span data-ttu-id="f9c13-206">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="f9c13-207">e.</span><span class="sxs-lookup"><span data-stu-id="f9c13-207">e.</span></span> <span data-ttu-id="f9c13-208">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-208">Click **Next**.</span></span>

7. <span data-ttu-id="f9c13-209">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="f9c13-211">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f9c13-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="f9c13-213">a.</span><span class="sxs-lookup"><span data-stu-id="f9c13-213">a.</span></span> <span data-ttu-id="f9c13-214">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="f9c13-215">b.</span><span class="sxs-lookup"><span data-stu-id="f9c13-215">b.</span></span> <span data-ttu-id="f9c13-216">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="f9c13-217">Creating a Soonr Workplace test user</span><span class="sxs-lookup"><span data-stu-id="f9c13-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="f9c13-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="f9c13-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="f9c13-219">Please work with Soonr Workplace support team to create a user in the platform.</span><span class="sxs-lookup"><span data-stu-id="f9c13-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="f9c13-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span><span class="sxs-lookup"><span data-stu-id="f9c13-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f9c13-221">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f9c13-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f9c13-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="f9c13-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![Assign User][200] 

<span data-ttu-id="f9c13-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f9c13-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="f9c13-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f9c13-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="f9c13-227">In the applications list, select **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="f9c13-229">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-229">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203] 

1. <span data-ttu-id="f9c13-231">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="f9c13-232">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="f9c13-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assign User][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="f9c13-234">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f9c13-234">Testing single sign-on</span></span>

<span data-ttu-id="f9c13-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f9c13-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f9c13-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span><span class="sxs-lookup"><span data-stu-id="f9c13-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f9c13-237">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f9c13-237">Additional resources</span></span>

* [<span data-ttu-id="f9c13-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9c13-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9c13-239">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f9c13-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-soonr-tutorial/tutorial_general_205.png

























