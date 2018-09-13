---
title: 'Tutorial: Azure Active Directory integration with SilkRoad Life Suite | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SilkRoad Life Suite.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d0b2675baf8d9d595585d8fc1a0116b416fbb9a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564178"
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="32ede-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="32ede-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="32ede-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32ede-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="32ede-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="32ede-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="32ede-106">You can control in Azure AD who has access to SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="32ede-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="32ede-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="32ede-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="32ede-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32ede-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32ede-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="32ede-109">Prerequisites</span></span>
<span data-ttu-id="32ede-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="32ede-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="32ede-111">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="32ede-111">An Azure AD subscription</span></span>
* <span data-ttu-id="32ede-112">A SilkRoad Life Suite SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="32ede-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="32ede-113">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="32ede-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="32ede-114">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="32ede-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="32ede-115">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="32ede-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="32ede-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32ede-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="32ede-117">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="32ede-117">Scenario Description</span></span>
<span data-ttu-id="32ede-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="32ede-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="32ede-119">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="32ede-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32ede-120">Adding SilkRoad Life Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="32ede-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="32ede-121">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="32ede-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="32ede-122">Add SilkRoad Life Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="32ede-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="32ede-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="32ede-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32ede-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="32ede-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32ede-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32ede-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="32ede-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="32ede-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="32ede-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="32ede-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="32ede-130">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="32ede-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="32ede-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="32ede-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="32ede-134">In the search box, type **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="32ede-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Applications][5]

7. <span data-ttu-id="32ede-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="32ede-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="32ede-138">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="32ede-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="32ede-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32ede-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32ede-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="32ede-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="32ede-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span><span class="sxs-lookup"><span data-stu-id="32ede-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="32ede-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="32ede-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="32ede-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="32ede-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32ede-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="32ede-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32ede-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32ede-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32ede-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="32ede-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="32ede-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="32ede-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32ede-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="32ede-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="32ede-149">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="32ede-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="32ede-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span><span class="sxs-lookup"><span data-stu-id="32ede-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="32ede-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="32ede-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="32ede-152">Sign-on to your SilkRoad company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="32ede-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="32ede-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span><span class="sxs-lookup"><span data-stu-id="32ede-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="32ede-154">Go to **Service Provider**, and then click **Federation Details**.</span><span class="sxs-lookup"><span data-stu-id="32ede-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD Single Sign-On][10] 

3. <span data-ttu-id="32ede-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="32ede-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Azure AD Single Sign-On][11] 

4. <span data-ttu-id="32ede-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="32ede-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

5. <span data-ttu-id="32ede-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="32ede-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 

6. <span data-ttu-id="32ede-162">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="32ede-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][8]   
 1. <span data-ttu-id="32ede-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="32ede-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="32ede-165">Open the downloaded **Silkroad** metadata file.</span><span class="sxs-lookup"><span data-stu-id="32ede-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="32ede-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span><span class="sxs-lookup"><span data-stu-id="32ede-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![Azure AD Single Sign-On][21] 
 4. <span data-ttu-id="32ede-168">Paste the value into the **Reply URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="32ede-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="32ede-169">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="32ede-169">Click **Next**.</span></span>

6. <span data-ttu-id="32ede-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="32ede-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][9]  
 1. <span data-ttu-id="32ede-172">Click Download certificate, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="32ede-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="32ede-173">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="32ede-173">Click **Next**.</span></span>

7. <span data-ttu-id="32ede-174">In your **SilkRoad** application, click **Authentication Sources**.</span><span class="sxs-lookup"><span data-stu-id="32ede-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD Single Sign-On][12] 

8. <span data-ttu-id="32ede-176">Click **Add Authentication Source**.</span><span class="sxs-lookup"><span data-stu-id="32ede-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD Single Sign-On][13] 

9. <span data-ttu-id="32ede-178">In the **Add Authentication Source** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="32ede-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Azure AD Single Sign-On][14]  
 1. <span data-ttu-id="32ede-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="32ede-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="32ede-181">Click **Create Identity Provider using File Data**.</span><span class="sxs-lookup"><span data-stu-id="32ede-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="32ede-182">In the **Authentication Sources** section, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="32ede-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD Single Sign-On][15] 

11. <span data-ttu-id="32ede-184">On the **Edit Authentication Source** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="32ede-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Azure AD Single Sign-On][16] 
 1. <span data-ttu-id="32ede-186">As **Enabled**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="32ede-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="32ede-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span><span class="sxs-lookup"><span data-stu-id="32ede-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="32ede-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="32ede-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="32ede-189">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="32ede-189">Click **Save**.</span></span>

12. <span data-ttu-id="32ede-190">Disable all other authentication sources.</span><span class="sxs-lookup"><span data-stu-id="32ede-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD Single Sign-On][17]

13. <span data-ttu-id="32ede-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="32ede-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD Single Sign-On][18]

14. <span data-ttu-id="32ede-194">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="32ede-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD Single Sign-On][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="32ede-196">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="32ede-196">Create an Azure AD test user</span></span>
<span data-ttu-id="32ede-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32ede-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="32ede-199">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="32ede-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32ede-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32ede-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="32ede-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="32ede-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="32ede-203">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="32ede-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32ede-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="32ede-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="32ede-207">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="32ede-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="32ede-209">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="32ede-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="32ede-210">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32ede-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="32ede-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="32ede-211">Click **Next**.</span></span>

6. <span data-ttu-id="32ede-212">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="32ede-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="32ede-214">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="32ede-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="32ede-215">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="32ede-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="32ede-216">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="32ede-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="32ede-217">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="32ede-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="32ede-218">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="32ede-218">Click **Next**.</span></span>

7. <span data-ttu-id="32ede-219">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="32ede-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="32ede-221">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="32ede-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="32ede-223">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="32ede-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="32ede-224">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="32ede-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="32ede-225">Create a SilkRoad Life Suite test user</span><span class="sxs-lookup"><span data-stu-id="32ede-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="32ede-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="32ede-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="32ede-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32ede-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="32ede-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="32ede-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="32ede-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32ede-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="32ede-230">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="32ede-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="32ede-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="32ede-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![Assign User][200] 

<span data-ttu-id="32ede-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="32ede-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="32ede-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="32ede-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="32ede-236">In the applications list, select **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="32ede-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Assign User][202] 

3. <span data-ttu-id="32ede-238">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="32ede-238">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 

4. <span data-ttu-id="32ede-240">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="32ede-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="32ede-241">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="32ede-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="32ede-243">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="32ede-243">Test single sign-on</span></span>
<span data-ttu-id="32ede-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="32ede-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="32ede-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span><span class="sxs-lookup"><span data-stu-id="32ede-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32ede-246">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="32ede-246">Additional Resources</span></span>
* [<span data-ttu-id="32ede-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32ede-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32ede-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32ede-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png







































