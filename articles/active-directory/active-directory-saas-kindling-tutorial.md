---
title: 'Tutorial: Azure Active Directory integration with Kindling | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kindling.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 46bc1fe3fcb3d54dd03a7f797e5edd239b57776f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549971"
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="05ddb-103">Tutorial: Azure Active Directory integration with Kindling</span><span class="sxs-lookup"><span data-stu-id="05ddb-103">Tutorial: Azure Active Directory integration with Kindling</span></span>
<span data-ttu-id="05ddb-104">The objective of this tutorial is to show you how to integrate Kindling with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05ddb-104">The objective of this tutorial is to show you how to integrate Kindling with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="05ddb-105">Integrating Kindling with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="05ddb-105">Integrating Kindling with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="05ddb-106">You can control in Azure AD who has access to Kindling</span><span class="sxs-lookup"><span data-stu-id="05ddb-106">You can control in Azure AD who has access to Kindling</span></span> 
* <span data-ttu-id="05ddb-107">You can enable your users to automatically get signed-on to Kindling (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="05ddb-107">You can enable your users to automatically get signed-on to Kindling (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="05ddb-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="05ddb-108">You can manage your accounts in one central location - the Azure classic portal</span></span> 

<span data-ttu-id="05ddb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05ddb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05ddb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="05ddb-110">Prerequisites</span></span>
<span data-ttu-id="05ddb-111">To configure Azure AD integration with Kindling, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="05ddb-111">To configure Azure AD integration with Kindling, you need the following items:</span></span>

* <span data-ttu-id="05ddb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="05ddb-112">An Azure AD subscription</span></span>
* <span data-ttu-id="05ddb-113">A Kindling subscription</span><span class="sxs-lookup"><span data-stu-id="05ddb-113">A Kindling subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05ddb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="05ddb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="05ddb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="05ddb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="05ddb-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="05ddb-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="05ddb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05ddb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="05ddb-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="05ddb-118">Scenario Description</span></span>
<span data-ttu-id="05ddb-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="05ddb-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="05ddb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="05ddb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05ddb-121">Adding Kindling from the gallery</span><span class="sxs-lookup"><span data-stu-id="05ddb-121">Adding Kindling from the gallery</span></span> 
2. <span data-ttu-id="05ddb-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="05ddb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-the-gallery"></a><span data-ttu-id="05ddb-123">Adding Kindling from the gallery</span><span class="sxs-lookup"><span data-stu-id="05ddb-123">Adding Kindling from the gallery</span></span>
<span data-ttu-id="05ddb-124">To configure the integration of Kindling into Azure AD, you need to add Kindling from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="05ddb-124">To configure the integration of Kindling into Azure AD, you need to add Kindling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="05ddb-125">**To add Kindling from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05ddb-125">**To add Kindling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="05ddb-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]

2. <span data-ttu-id="05ddb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="05ddb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="05ddb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="05ddb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="05ddb-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="05ddb-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="05ddb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="05ddb-135">In the search box, type **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-135">In the search box, type **Kindling**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_kindling_01.png)

7. <span data-ttu-id="05ddb-137">In the results pane, select **Kindling**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="05ddb-137">In the results pane, select **Kindling**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_kindling_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05ddb-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="05ddb-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05ddb-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="05ddb-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="05ddb-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Kindling to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="05ddb-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Kindling to an user in Azure AD is.</span></span> <span data-ttu-id="05ddb-142">In other words, a link relationship between an Azure AD user and the related user in Kindling needs to be established.</span><span class="sxs-lookup"><span data-stu-id="05ddb-142">In other words, a link relationship between an Azure AD user and the related user in Kindling needs to be established.</span></span>  
<span data-ttu-id="05ddb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kindling.</span><span class="sxs-lookup"><span data-stu-id="05ddb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kindling.</span></span>

<span data-ttu-id="05ddb-144">To configure and test Azure AD single sign-on with Kindling, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="05ddb-144">To configure and test Azure AD single sign-on with Kindling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="05ddb-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="05ddb-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="05ddb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05ddb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05ddb-147">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - to have a counterpart of Britta Simon in Kindling that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="05ddb-147">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - to have a counterpart of Britta Simon in Kindling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="05ddb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="05ddb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05ddb-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="05ddb-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05ddb-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="05ddb-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="05ddb-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Kindling application.</span><span class="sxs-lookup"><span data-stu-id="05ddb-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Kindling application.</span></span> <span data-ttu-id="05ddb-152">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="05ddb-152">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="05ddb-153">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="05ddb-153">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="05ddb-154">To configure single sign-on for Kindling, you need a registered domain.</span><span class="sxs-lookup"><span data-stu-id="05ddb-154">To configure single sign-on for Kindling, you need a registered domain.</span></span> <span data-ttu-id="05ddb-155">If you don't have a registered domain yet, contact your Kindling support team via [support@kindlingapp.com](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="05ddb-155">If you don't have a registered domain yet, contact your Kindling support team via [support@kindlingapp.com](mailto:support@kindlingapp.com).</span></span>  

<span data-ttu-id="05ddb-156">**To configure Azure AD single sign-on with Kindling, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05ddb-156">**To configure Azure AD single sign-on with Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="05ddb-157">In the Azure classic portal, on the **Kindling** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="05ddb-157">In the Azure classic portal, on the **Kindling** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="05ddb-159">On the **How would you like users to sign on to Kindling** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-159">On the **How would you like users to sign on to Kindling** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_kindling_03.png) 

3. <span data-ttu-id="05ddb-161">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="05ddb-161">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_kindling_04.png) 

    <span data-ttu-id="05ddb-163">a.</span><span class="sxs-lookup"><span data-stu-id="05ddb-163">a.</span></span> <span data-ttu-id="05ddb-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Kindling application  using the following pattern: `https://<company name>.kindlingapp.com/`</span><span class="sxs-lookup"><span data-stu-id="05ddb-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Kindling application  using the following pattern: `https://<company name>.kindlingapp.com/`</span></span>

    <span data-ttu-id="05ddb-165">b.</span><span class="sxs-lookup"><span data-stu-id="05ddb-165">b.</span></span> <span data-ttu-id="05ddb-166">Contact yout Kindling support team via [support@kindlingapp.com](mailto:support@kindlingapp.com) to get the **Issuer** and the **Reply URL** value.</span><span class="sxs-lookup"><span data-stu-id="05ddb-166">Contact yout Kindling support team via [support@kindlingapp.com](mailto:support@kindlingapp.com) to get the **Issuer** and the **Reply URL** value.</span></span>   

    <span data-ttu-id="05ddb-167">c.</span><span class="sxs-lookup"><span data-stu-id="05ddb-167">c.</span></span> <span data-ttu-id="05ddb-168">In the **Issuer** textbox, type your Issuer URL.</span><span class="sxs-lookup"><span data-stu-id="05ddb-168">In the **Issuer** textbox, type your Issuer URL.</span></span>

    <span data-ttu-id="05ddb-169">d.</span><span class="sxs-lookup"><span data-stu-id="05ddb-169">d.</span></span> <span data-ttu-id="05ddb-170">In the **Reply URL** textbox, type your Reply URL.</span><span class="sxs-lookup"><span data-stu-id="05ddb-170">In the **Reply URL** textbox, type your Reply URL.</span></span>   

    <span data-ttu-id="05ddb-171">e.</span><span class="sxs-lookup"><span data-stu-id="05ddb-171">e.</span></span> <span data-ttu-id="05ddb-172">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-172">Click **Next**.</span></span>


1. <span data-ttu-id="05ddb-173">On the **Configure single sign-on at Kindling** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="05ddb-173">On the **Configure single sign-on at Kindling** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_kindling_05.png) 
   
    <span data-ttu-id="05ddb-175">a.</span><span class="sxs-lookup"><span data-stu-id="05ddb-175">a.</span></span> <span data-ttu-id="05ddb-176">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="05ddb-176">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="05ddb-177">b.</span><span class="sxs-lookup"><span data-stu-id="05ddb-177">b.</span></span> <span data-ttu-id="05ddb-178">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-178">Click **Next**.</span></span>

2. <span data-ttu-id="05ddb-179">Contact your Kindling support team via [support@kindlingapp.com](mailto:support@kindlingapp.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="05ddb-179">Contact your Kindling support team via [support@kindlingapp.com](mailto:support@kindlingapp.com) and provide them with the following:</span></span>
   
    - <span data-ttu-id="05ddb-180">The downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="05ddb-180">The downloaded certificate</span></span>
    - <span data-ttu-id="05ddb-181">The **Issuer URL** value that maps to Kindling's **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="05ddb-181">The **Issuer URL** value that maps to Kindling's **Entity ID**</span></span>
    - <span data-ttu-id="05ddb-182">The **Single Sign-On Service URL** that maps to Kindling's **SSO Sign On URL**</span><span class="sxs-lookup"><span data-stu-id="05ddb-182">The **Single Sign-On Service URL** that maps to Kindling's **SSO Sign On URL**</span></span> 
    - <span data-ttu-id="05ddb-183">The **Single Sign-Out Service URL** that maps to Kindling's **SSO Sign Out URL**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-183">The **Single Sign-Out Service URL** that maps to Kindling's **SSO Sign Out URL**.</span></span> 

3. <span data-ttu-id="05ddb-184">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-184">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Single Sign-On][10]

4. <span data-ttu-id="05ddb-186">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-186">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05ddb-188">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="05ddb-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="05ddb-189">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05ddb-189">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="05ddb-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05ddb-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="05ddb-192">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-192">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="05ddb-194">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="05ddb-194">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="05ddb-195">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-195">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05ddb-197">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-197">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="05ddb-199">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="05ddb-199">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/create_aaduser_05.png)  
   
    <span data-ttu-id="05ddb-201">a.</span><span class="sxs-lookup"><span data-stu-id="05ddb-201">a.</span></span> <span data-ttu-id="05ddb-202">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="05ddb-202">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="05ddb-203">b.</span><span class="sxs-lookup"><span data-stu-id="05ddb-203">b.</span></span> <span data-ttu-id="05ddb-204">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-204">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="05ddb-205">c.</span><span class="sxs-lookup"><span data-stu-id="05ddb-205">c.</span></span> <span data-ttu-id="05ddb-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-206">Click **Next**.</span></span>

6. <span data-ttu-id="05ddb-207">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="05ddb-207">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="05ddb-209">a.</span><span class="sxs-lookup"><span data-stu-id="05ddb-209">a.</span></span> <span data-ttu-id="05ddb-210">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-210">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="05ddb-211">b.</span><span class="sxs-lookup"><span data-stu-id="05ddb-211">b.</span></span> <span data-ttu-id="05ddb-212">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-212">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="05ddb-213">c.</span><span class="sxs-lookup"><span data-stu-id="05ddb-213">c.</span></span> <span data-ttu-id="05ddb-214">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-214">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="05ddb-215">d.</span><span class="sxs-lookup"><span data-stu-id="05ddb-215">d.</span></span> <span data-ttu-id="05ddb-216">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-216">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="05ddb-217">e.</span><span class="sxs-lookup"><span data-stu-id="05ddb-217">e.</span></span> <span data-ttu-id="05ddb-218">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-218">Click **Next**.</span></span>

7. <span data-ttu-id="05ddb-219">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="05ddb-221">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="05ddb-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="05ddb-223">a.</span><span class="sxs-lookup"><span data-stu-id="05ddb-223">a.</span></span> <span data-ttu-id="05ddb-224">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-224">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="05ddb-225">b.</span><span class="sxs-lookup"><span data-stu-id="05ddb-225">b.</span></span> <span data-ttu-id="05ddb-226">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-226">Click **Complete**.</span></span>   

### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="05ddb-227">Creating a Kindling test user</span><span class="sxs-lookup"><span data-stu-id="05ddb-227">Creating a Kindling test user</span></span>
<span data-ttu-id="05ddb-228">The objective of this section is to create a user called Britta Simon in Kindling.</span><span class="sxs-lookup"><span data-stu-id="05ddb-228">The objective of this section is to create a user called Britta Simon in Kindling.</span></span>
<span data-ttu-id="05ddb-229">Kindling supports just-in-time provisioning.</span><span class="sxs-lookup"><span data-stu-id="05ddb-229">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="05ddb-230">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="05ddb-230">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

<span data-ttu-id="05ddb-231">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="05ddb-231">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="05ddb-232">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="05ddb-232">Assigning the Azure AD test user</span></span>
<span data-ttu-id="05ddb-233">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Kindling.</span><span class="sxs-lookup"><span data-stu-id="05ddb-233">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Kindling.</span></span>

![Assign User][200] 

<span data-ttu-id="05ddb-235">**To assign Britta Simon to Kindling, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05ddb-235">**To assign Britta Simon to Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="05ddb-236">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="05ddb-236">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="05ddb-238">In the applications list, select **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-238">In the applications list, select **Kindling**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_kindling_50.png) 

3. <span data-ttu-id="05ddb-240">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-240">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 

4. <span data-ttu-id="05ddb-242">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-242">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="05ddb-243">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="05ddb-243">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="05ddb-245">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="05ddb-245">Testing Single Sign-On</span></span>
<span data-ttu-id="05ddb-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="05ddb-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="05ddb-247">When you click the Kindling tile in the Access Panel, you should get automatically signed-on to your Kindling application.</span><span class="sxs-lookup"><span data-stu-id="05ddb-247">When you click the Kindling tile in the Access Panel, you should get automatically signed-on to your Kindling application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05ddb-248">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="05ddb-248">Additional Resources</span></span>
* [<span data-ttu-id="05ddb-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05ddb-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05ddb-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05ddb-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kindling-tutorial/tutorial_general_205.png































