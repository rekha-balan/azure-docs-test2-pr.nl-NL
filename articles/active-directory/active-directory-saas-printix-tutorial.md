---
title: 'Tutorial: Azure Active Directory integration with Printix | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Printix.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: d4892f5c7e22a52439b73423f5aedecd345f3b76
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554818"
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="bd41e-103">Tutorial: Azure Active Directory integration with Printix</span><span class="sxs-lookup"><span data-stu-id="bd41e-103">Tutorial: Azure Active Directory integration with Printix</span></span>
<span data-ttu-id="bd41e-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd41e-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd41e-105">Integrating Printix with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="bd41e-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="bd41e-106">You can control in Azure AD who has access to Printix</span><span class="sxs-lookup"><span data-stu-id="bd41e-106">You can control in Azure AD who has access to Printix</span></span>
* <span data-ttu-id="bd41e-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="bd41e-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="bd41e-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="bd41e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="bd41e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd41e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd41e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bd41e-110">Prerequisites</span></span>
<span data-ttu-id="bd41e-111">To configure Azure AD integration with Printix, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="bd41e-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

* <span data-ttu-id="bd41e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="bd41e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="bd41e-113">A Printix single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="bd41e-113">A Printix single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd41e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="bd41e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="bd41e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="bd41e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="bd41e-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="bd41e-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="bd41e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd41e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd41e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="bd41e-118">Scenario description</span></span>
<span data-ttu-id="bd41e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="bd41e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="bd41e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="bd41e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd41e-121">Adding Printix from the gallery</span><span class="sxs-lookup"><span data-stu-id="bd41e-121">Adding Printix from the gallery</span></span>
2. <span data-ttu-id="bd41e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bd41e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="bd41e-123">Adding Printix from the gallery</span><span class="sxs-lookup"><span data-stu-id="bd41e-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="bd41e-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="bd41e-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bd41e-125">**To add Printix from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bd41e-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bd41e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]

2. <span data-ttu-id="bd41e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="bd41e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="bd41e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="bd41e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="bd41e-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="bd41e-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="bd41e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="bd41e-135">In the search box, type **Printix**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-135">In the search box, type **Printix**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_printix_01.png)

7. <span data-ttu-id="bd41e-137">In the results pane, select **Printix**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="bd41e-137">In the results pane, select **Printix**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd41e-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bd41e-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd41e-139">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bd41e-139">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bd41e-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd41e-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="bd41e-141">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span><span class="sxs-lookup"><span data-stu-id="bd41e-141">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="bd41e-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Printix.</span><span class="sxs-lookup"><span data-stu-id="bd41e-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Printix.</span></span>

<span data-ttu-id="bd41e-143">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="bd41e-143">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bd41e-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="bd41e-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bd41e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd41e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd41e-146">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="bd41e-146">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="bd41e-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bd41e-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd41e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="bd41e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd41e-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bd41e-149">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="bd41e-150">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Printix application.</span><span class="sxs-lookup"><span data-stu-id="bd41e-150">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="bd41e-151">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bd41e-151">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="bd41e-152">In the classic portal, on the **Printix** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="bd41e-152">In the classic portal, on the **Printix** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="bd41e-154">On the **How would you like users to sign on to Printix** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-154">On the **How would you like users to sign on to Printix** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_printix_03.png) 

3. <span data-ttu-id="bd41e-156">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bd41e-156">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_printix_04.png) 
   
    <span data-ttu-id="bd41e-158">a.</span><span class="sxs-lookup"><span data-stu-id="bd41e-158">a.</span></span> <span data-ttu-id="bd41e-159">In the **Reply URL** textbox,  type `https://auth.printix.net/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="bd41e-159">In the **Reply URL** textbox,  type `https://auth.printix.net/saml/SSO`.</span></span>
   
    <span data-ttu-id="bd41e-160">b.</span><span class="sxs-lookup"><span data-stu-id="bd41e-160">b.</span></span> <span data-ttu-id="bd41e-161">click **Next**</span><span class="sxs-lookup"><span data-stu-id="bd41e-161">click **Next**</span></span>

4. <span data-ttu-id="bd41e-162">On the **Configure single sign-on at Printix** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bd41e-162">On the **Configure single sign-on at Printix** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_printix_05.png)
   
    <span data-ttu-id="bd41e-164">a.</span><span class="sxs-lookup"><span data-stu-id="bd41e-164">a.</span></span> <span data-ttu-id="bd41e-165">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="bd41e-165">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="bd41e-166">b.</span><span class="sxs-lookup"><span data-stu-id="bd41e-166">b.</span></span> <span data-ttu-id="bd41e-167">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-167">Click **Next**.</span></span>

5. <span data-ttu-id="bd41e-168">Sign-on to your Printix tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="bd41e-168">Sign-on to your Printix tenant as an administrator.</span></span>

6. <span data-ttu-id="bd41e-169">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span><span class="sxs-lookup"><span data-stu-id="bd41e-169">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

7. <span data-ttu-id="bd41e-171">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span><span class="sxs-lookup"><span data-stu-id="bd41e-171">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

8. <span data-ttu-id="bd41e-173">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span><span class="sxs-lookup"><span data-stu-id="bd41e-173">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
    <span data-ttu-id="bd41e-175">a.</span><span class="sxs-lookup"><span data-stu-id="bd41e-175">a.</span></span> <span data-ttu-id="bd41e-176">Attached the metadata xml file which you downloaded in step 4 to Printix support team via "**support@printix.net**".</span><span class="sxs-lookup"><span data-stu-id="bd41e-176">Attached the metadata xml file which you downloaded in step 4 to Printix support team via "**support@printix.net**".</span></span> <span data-ttu-id="bd41e-177">Then they will upload the xml file and provide a federation metadata URL with you.</span><span class="sxs-lookup"><span data-stu-id="bd41e-177">Then they will upload the xml file and provide a federation metadata URL with you.</span></span>

9. <span data-ttu-id="bd41e-178">Click the "**Test**" button and click "**OK**" button if the test was successful.</span><span class="sxs-lookup"><span data-stu-id="bd41e-178">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
    <span data-ttu-id="bd41e-179">a.</span><span class="sxs-lookup"><span data-stu-id="bd41e-179">a.</span></span> <span data-ttu-id="bd41e-180">Azure active directory page will show after clicking the **test** button.</span><span class="sxs-lookup"><span data-stu-id="bd41e-180">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="bd41e-181">"The test was successful" here means after entering the credentials of your Azure test account it will popo up a message "Settings tested OK".Then click the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="bd41e-181">"The test was successful" here means after entering the credentials of your Azure test account it will popo up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

10. <span data-ttu-id="bd41e-183">Click the **Save** button on "**Authentication**" page.</span><span class="sxs-lookup"><span data-stu-id="bd41e-183">Click the **Save** button on "**Authentication**" page.</span></span>

11. <span data-ttu-id="bd41e-184">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-184">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

12. <span data-ttu-id="bd41e-186">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-186">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd41e-188">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bd41e-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd41e-189">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd41e-189">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="bd41e-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bd41e-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bd41e-192">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-192">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="bd41e-194">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="bd41e-194">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="bd41e-195">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-195">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd41e-197">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-197">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="bd41e-199">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bd41e-199">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="bd41e-201">a.</span><span class="sxs-lookup"><span data-stu-id="bd41e-201">a.</span></span> <span data-ttu-id="bd41e-202">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="bd41e-202">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="bd41e-203">b.</span><span class="sxs-lookup"><span data-stu-id="bd41e-203">b.</span></span> <span data-ttu-id="bd41e-204">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-204">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="bd41e-205">c.</span><span class="sxs-lookup"><span data-stu-id="bd41e-205">c.</span></span> <span data-ttu-id="bd41e-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-206">Click **Next**.</span></span>

6. <span data-ttu-id="bd41e-207">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bd41e-207">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="bd41e-209">a.</span><span class="sxs-lookup"><span data-stu-id="bd41e-209">a.</span></span> <span data-ttu-id="bd41e-210">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-210">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="bd41e-211">b.</span><span class="sxs-lookup"><span data-stu-id="bd41e-211">b.</span></span> <span data-ttu-id="bd41e-212">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-212">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="bd41e-213">c.</span><span class="sxs-lookup"><span data-stu-id="bd41e-213">c.</span></span> <span data-ttu-id="bd41e-214">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-214">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="bd41e-215">d.</span><span class="sxs-lookup"><span data-stu-id="bd41e-215">d.</span></span> <span data-ttu-id="bd41e-216">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-216">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="bd41e-217">e.</span><span class="sxs-lookup"><span data-stu-id="bd41e-217">e.</span></span> <span data-ttu-id="bd41e-218">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-218">Click **Next**.</span></span>

7. <span data-ttu-id="bd41e-219">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="bd41e-221">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bd41e-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="bd41e-223">a.</span><span class="sxs-lookup"><span data-stu-id="bd41e-223">a.</span></span> <span data-ttu-id="bd41e-224">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-224">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="bd41e-225">b.</span><span class="sxs-lookup"><span data-stu-id="bd41e-225">b.</span></span> <span data-ttu-id="bd41e-226">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-226">Click **Complete**.</span></span>   

### <a name="creating-an-printix-test-user"></a><span data-ttu-id="bd41e-227">Creating an Printix test user</span><span class="sxs-lookup"><span data-stu-id="bd41e-227">Creating an Printix test user</span></span>
<span data-ttu-id="bd41e-228">The objective of this section is to create a user called Britta Simon in Printix.</span><span class="sxs-lookup"><span data-stu-id="bd41e-228">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="bd41e-229">Printix supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="bd41e-229">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="bd41e-230">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="bd41e-230">There is no action item for you in this section.</span></span> <span data-ttu-id="bd41e-231">A new user will be created during an attempt to access Printix if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="bd41e-231">A new user will be created during an attempt to access Printix if it doesn't exist yet.</span></span> <span data-ttu-id="bd41e-232">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="bd41e-232">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

> [!NOTE]
> <span data-ttu-id="bd41e-233">If you need to create an user manually, you need to contact the Printix support team.</span><span class="sxs-lookup"><span data-stu-id="bd41e-233">If you need to create an user manually, you need to contact the Printix support team.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bd41e-234">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bd41e-234">Assigning the Azure AD test user</span></span>
<span data-ttu-id="bd41e-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Printix.</span><span class="sxs-lookup"><span data-stu-id="bd41e-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Printix.</span></span>

![Assign User][200] 

<span data-ttu-id="bd41e-237">**To assign Britta Simon to Printix, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bd41e-237">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="bd41e-238">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="bd41e-238">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="bd41e-240">In the applications list, select **Printix**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-240">In the applications list, select **Printix**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_printix_50.png) 

3. <span data-ttu-id="bd41e-242">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-242">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]

4. <span data-ttu-id="bd41e-244">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-244">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="bd41e-245">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="bd41e-245">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="bd41e-247">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="bd41e-247">Testing single sign-on</span></span>
<span data-ttu-id="bd41e-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bd41e-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bd41e-249">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span><span class="sxs-lookup"><span data-stu-id="bd41e-249">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd41e-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="bd41e-250">Additional resources</span></span>
* [<span data-ttu-id="bd41e-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd41e-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd41e-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bd41e-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-printix-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-printix-tutorial/tutorial_general_205.png




























