---
title: 'Tutorial: Azure Active Directory integration with O. C. Tanner - AppreciateHub | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and O. C. Tanner - AppreciateHub.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 002049d2baee1e38375b110a6993fdfc53fd52f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554677"
---
# <a name="tutorial-azure-active-directory-integration-with-o-c-tanner---appreciatehub"></a><span data-ttu-id="aa870-105">Tutorial: Azure Active Directory integration with O. C.</span><span class="sxs-lookup"><span data-stu-id="aa870-105">Tutorial: Azure Active Directory integration with O. C.</span></span> <span data-ttu-id="aa870-106">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="aa870-106">Tanner - AppreciateHub</span></span>
<span data-ttu-id="aa870-107">The objective of this tutorial is to show you how to integrate O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-107">The objective of this tutorial is to show you how to integrate O.C.</span></span> <span data-ttu-id="aa870-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa870-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="aa870-109">Integrating O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-109">Integrating O.C.</span></span> <span data-ttu-id="aa870-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="aa870-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="aa870-111">You can control in Azure AD who has access to O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="aa870-112">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="aa870-112">Tanner - AppreciateHub</span></span> 
* <span data-ttu-id="aa870-113">You can enable your users to automatically get signed-on to O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="aa870-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="aa870-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="aa870-115">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="aa870-115">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="aa870-116">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa870-116">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa870-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aa870-117">Prerequisites</span></span>
<span data-ttu-id="aa870-118">To configure Azure AD integration with O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="aa870-119">Tanner - AppreciateHub, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="aa870-119">Tanner - AppreciateHub, you need the following items:</span></span>

* <span data-ttu-id="aa870-120">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="aa870-120">An Azure AD subscription</span></span>
* <span data-ttu-id="aa870-121">A O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-121">A O.C.</span></span> <span data-ttu-id="aa870-122">Tanner - AppreciateHub single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="aa870-122">Tanner - AppreciateHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa870-123">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="aa870-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="aa870-124">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="aa870-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="aa870-125">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="aa870-125">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="aa870-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa870-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="aa870-127">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="aa870-127">Scenario Description</span></span>
<span data-ttu-id="aa870-128">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="aa870-128">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="aa870-129">The scenario outlined in this tutorial consists of three main building blocks:</span><span class="sxs-lookup"><span data-stu-id="aa870-129">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="aa870-130">Adding O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-130">Adding O.C.</span></span> <span data-ttu-id="aa870-131">Tanner - AppreciateHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="aa870-131">Tanner - AppreciateHub from the gallery</span></span> 
2. <span data-ttu-id="aa870-132">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="aa870-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="aa870-133">Adding O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-133">Adding O.C.</span></span> <span data-ttu-id="aa870-134">Tanner - AppreciateHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="aa870-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="aa870-135">To configure the integration of O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-135">To configure the integration of O.C.</span></span> <span data-ttu-id="aa870-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="aa870-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="aa870-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aa870-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="aa870-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aa870-139">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa870-139">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="aa870-141">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="aa870-141">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="aa870-142">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="aa870-142">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2] 
4. <span data-ttu-id="aa870-144">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="aa870-144">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3] 
5. <span data-ttu-id="aa870-146">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="aa870-146">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4] 
6. <span data-ttu-id="aa870-148">In the search box, type **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="aa870-148">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>
   
    ![Applications][5] 
7. <span data-ttu-id="aa870-150">In the results pane, select **O.C. Tanner - AppreciateHub**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="aa870-150">In the results pane, select **O.C. Tanner - AppreciateHub**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][25] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa870-152">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="aa870-152">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aa870-153">The objective of this section is to show you how to configure and test Azure AD single sign-on with O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-153">The objective of this section is to show you how to configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="aa870-154">Tanner - AppreciateHub based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aa870-154">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aa870-155">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-155">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="aa870-156">Tanner - AppreciateHub to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="aa870-156">Tanner - AppreciateHub to an user in Azure AD is.</span></span> <span data-ttu-id="aa870-157">In other words, a link relationship between an Azure AD user and the related user in O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-157">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="aa870-158">Tanner - AppreciateHub needs to be established.</span><span class="sxs-lookup"><span data-stu-id="aa870-158">Tanner - AppreciateHub needs to be established.</span></span>  
<span data-ttu-id="aa870-159">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-159">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in O.C.</span></span> <span data-ttu-id="aa870-160">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="aa870-160">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="aa870-161">To configure and test Azure AD single sign-on with O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-161">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="aa870-162">Tanner - AppreciateHub, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="aa870-162">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aa870-163">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="aa870-163">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aa870-164">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa870-164">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa870-165">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-165">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="aa870-166">Tanner - AppreciateHub that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="aa870-166">Tanner - AppreciateHub that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="aa870-167">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="aa870-167">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa870-168">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="aa870-168">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa870-169">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="aa870-169">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="aa870-170">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-170">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your O.C.</span></span> <span data-ttu-id="aa870-171">Tanner - AppreciateHub application.</span><span class="sxs-lookup"><span data-stu-id="aa870-171">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="aa870-172">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="aa870-172">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="aa870-173">In the Azure classic portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="aa870-173">In the Azure classic portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6]
2. <span data-ttu-id="aa870-175">On the **How would you like users to sign on to O.C. Tanner - AppreciateHub** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aa870-175">On the **How would you like users to sign on to O.C. Tanner - AppreciateHub** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7]
3. <span data-ttu-id="aa870-177">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="aa870-177">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure App Settings][8]
   
     <span data-ttu-id="aa870-179">a.</span><span class="sxs-lookup"><span data-stu-id="aa870-179">a.</span></span> <span data-ttu-id="aa870-180">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="aa870-180">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
     <span data-ttu-id="aa870-181">b.</span><span class="sxs-lookup"><span data-stu-id="aa870-181">b.</span></span> <span data-ttu-id="aa870-182">Locate the **md:AssertionConsumerService** node.</span><span class="sxs-lookup"><span data-stu-id="aa870-182">Locate the **md:AssertionConsumerService** node.</span></span> 
   
     <span data-ttu-id="aa870-183">c.</span><span class="sxs-lookup"><span data-stu-id="aa870-183">c.</span></span> <span data-ttu-id="aa870-184">Copy the value of the **Location** attribute.</span><span class="sxs-lookup"><span data-stu-id="aa870-184">Copy the value of the **Location** attribute.</span></span> 
   
     ![Configure App Settings][12]
   
     <span data-ttu-id="aa870-186">d.</span><span class="sxs-lookup"><span data-stu-id="aa870-186">d.</span></span> <span data-ttu-id="aa870-187">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="aa870-187">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="aa870-188">If you are expiriencing issues getting the Reply URL from the metadata file, contact the O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-188">If you are expiriencing issues getting the Reply URL from the metadata file, contact the O.C.</span></span> <span data-ttu-id="aa870-189">Tanner - AppreciateHub support team via [sso@octanner.com](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="aa870-189">Tanner - AppreciateHub support team via [sso@octanner.com](mailto:sso@octanner.com).</span></span>
    > 
    > 
   
    <span data-ttu-id="aa870-190">e.</span><span class="sxs-lookup"><span data-stu-id="aa870-190">e.</span></span> <span data-ttu-id="aa870-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aa870-191">Click **Next**.</span></span>

4. <span data-ttu-id="aa870-192">On the **Configure single sign-on at O.C. Tanner - AppreciateHub** page, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="aa870-192">On the **Configure single sign-on at O.C. Tanner - AppreciateHub** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![What is Azure AD Connect][9]
5. <span data-ttu-id="aa870-194">Contact the O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-194">Contact the O.C.</span></span> <span data-ttu-id="aa870-195">Tanner - AppreciateHub support team via xyz, provide them with the metadata file, and them let them know that they should enable SSO for you.</span><span class="sxs-lookup"><span data-stu-id="aa870-195">Tanner - AppreciateHub support team via xyz, provide them with the metadata file, and them let them know that they should enable SSO for you.</span></span>
6. <span data-ttu-id="aa870-196">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aa870-196">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![What is Azure AD Connect][10]
7. <span data-ttu-id="aa870-198">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="aa870-198">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![What is Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa870-200">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="aa870-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa870-201">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa870-201">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="aa870-203">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="aa870-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aa870-204">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa870-204">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="aa870-206">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="aa870-206">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="aa870-207">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="aa870-207">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="aa870-209">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="aa870-209">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="aa870-211">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="aa870-211">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="aa870-213">a.</span><span class="sxs-lookup"><span data-stu-id="aa870-213">a.</span></span> <span data-ttu-id="aa870-214">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="aa870-214">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="aa870-215">b.</span><span class="sxs-lookup"><span data-stu-id="aa870-215">b.</span></span> <span data-ttu-id="aa870-216">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa870-216">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="aa870-217">c.</span><span class="sxs-lookup"><span data-stu-id="aa870-217">c.</span></span> <span data-ttu-id="aa870-218">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aa870-218">Click **Next**.</span></span>
6. <span data-ttu-id="aa870-219">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="aa870-219">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_06.png)
   
    <span data-ttu-id="aa870-221">a.</span><span class="sxs-lookup"><span data-stu-id="aa870-221">a.</span></span> <span data-ttu-id="aa870-222">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="aa870-222">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="aa870-223">b.</span><span class="sxs-lookup"><span data-stu-id="aa870-223">b.</span></span> <span data-ttu-id="aa870-224">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="aa870-224">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="aa870-225">c.</span><span class="sxs-lookup"><span data-stu-id="aa870-225">c.</span></span> <span data-ttu-id="aa870-226">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="aa870-226">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="aa870-227">d.</span><span class="sxs-lookup"><span data-stu-id="aa870-227">d.</span></span> <span data-ttu-id="aa870-228">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="aa870-228">In the **Role** list, select **User**.</span></span>
    <span data-ttu-id="aa870-229">e.</span><span class="sxs-lookup"><span data-stu-id="aa870-229">e.</span></span> <span data-ttu-id="aa870-230">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aa870-230">Click **Next**.</span></span>

7. <span data-ttu-id="aa870-231">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="aa870-231">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="aa870-233">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="aa870-233">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="aa870-235">a.</span><span class="sxs-lookup"><span data-stu-id="aa870-235">a.</span></span> <span data-ttu-id="aa870-236">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="aa870-236">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="aa870-237">b.</span><span class="sxs-lookup"><span data-stu-id="aa870-237">b.</span></span> <span data-ttu-id="aa870-238">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="aa870-238">Click **Complete**.</span></span>   

### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="aa870-239">Creating a O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-239">Creating a O.C.</span></span> <span data-ttu-id="aa870-240">Tanner - AppreciateHub test user</span><span class="sxs-lookup"><span data-stu-id="aa870-240">Tanner - AppreciateHub test user</span></span>
<span data-ttu-id="aa870-241">The objective of this section is to create a user called Britta Simon in O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-241">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="aa870-242">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="aa870-242">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="aa870-243">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="aa870-243">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="aa870-244">Ask your OC Tanner support team to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa870-244">Ask your OC Tanner support team to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="aa870-245">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="aa870-245">Assigning the Azure AD test user</span></span>
<span data-ttu-id="aa870-246">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-246">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to O.C.</span></span> <span data-ttu-id="aa870-247">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="aa870-247">Tanner - AppreciateHub.</span></span>

![Assign User][200]

<span data-ttu-id="aa870-249">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="aa870-249">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="aa870-250">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="aa870-250">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="aa870-252">In the applications list, select **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="aa870-252">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>
   
    ![Assign User][202]
3. <span data-ttu-id="aa870-254">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="aa870-254">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="aa870-256">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="aa870-256">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="aa870-257">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="aa870-257">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="aa870-259">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="aa870-259">Testing Single Sign-On</span></span>
<span data-ttu-id="aa870-260">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="aa870-260">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="aa870-261">When you click the O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-261">When you click the O.C.</span></span> <span data-ttu-id="aa870-262">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span><span class="sxs-lookup"><span data-stu-id="aa870-262">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="aa870-263">Tanner - AppreciateHub application.</span><span class="sxs-lookup"><span data-stu-id="aa870-263">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa870-264">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="aa870-264">Additional Resources</span></span>
* [<span data-ttu-id="aa870-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa870-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa870-266">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa870-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_01.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_25.png


[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_02.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_03.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_04.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_05.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_06.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_07.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_205.png
































