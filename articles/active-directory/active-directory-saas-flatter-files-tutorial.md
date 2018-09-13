---
title: 'Tutorial: Azure Active Directory integration with Flatter Files | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Flatter Files.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: fc6fb3dd66d21ec40e5ff57245be418060906272
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554510"
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="9a9dc-103">Tutorial: Azure Active Directory integration with Flatter Files</span><span class="sxs-lookup"><span data-stu-id="9a9dc-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>
<span data-ttu-id="9a9dc-104">The objective of this tutorial is to show you how to integrate Flatter Files with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a9dc-104">The objective of this tutorial is to show you how to integrate Flatter Files with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="9a9dc-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="9a9dc-106">You can control in Azure AD who has access to Flatter Files</span><span class="sxs-lookup"><span data-stu-id="9a9dc-106">You can control in Azure AD who has access to Flatter Files</span></span> 
* <span data-ttu-id="9a9dc-107">You can enable your users to automatically get signed-on to Flatter Files single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="9a9dc-107">You can enable your users to automatically get signed-on to Flatter Files single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="9a9dc-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span><span class="sxs-lookup"><span data-stu-id="9a9dc-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span></span>

<span data-ttu-id="9a9dc-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a9dc-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a9dc-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9a9dc-110">Prerequisites</span></span>
<span data-ttu-id="9a9dc-111">To configure Azure AD integration with Flatter Files, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-111">To configure Azure AD integration with Flatter Files, you need the following items:</span></span>

* <span data-ttu-id="9a9dc-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9a9dc-112">An Azure AD subscription</span></span>
* <span data-ttu-id="9a9dc-113">A Flatter Files single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9a9dc-113">A Flatter Files single-sign on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="9a9dc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="9a9dc-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="9a9dc-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="9a9dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a9dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="9a9dc-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9a9dc-118">Scenario description</span></span>
<span data-ttu-id="9a9dc-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  

<span data-ttu-id="9a9dc-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a9dc-121">Adding Flatter Files from the gallery</span><span class="sxs-lookup"><span data-stu-id="9a9dc-121">Adding Flatter Files from the gallery</span></span> 
2. <span data-ttu-id="9a9dc-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9a9dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-flatter-files-from-the-gallery"></a><span data-ttu-id="9a9dc-123">Add Flatter Files from the gallery</span><span class="sxs-lookup"><span data-stu-id="9a9dc-123">Add Flatter Files from the gallery</span></span>
<span data-ttu-id="9a9dc-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a9dc-125">**To add Flatter Files from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9a9dc-125">**To add Flatter Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a9dc-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="9a9dc-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="9a9dc-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="9a9dc-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="9a9dc-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="9a9dc-135">In the search box, type **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-135">In the search box, type **Flatter Files**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_01.png)

7. <span data-ttu-id="9a9dc-137">In the results pane, select **Flatter Files**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-137">In the results pane, select **Flatter Files**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_500.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a9dc-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9a9dc-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9a9dc-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9a9dc-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a9dc-141">For SSO to work, Azure AD needs to know what the counterpart user in Flatter Files to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-141">For SSO to work, Azure AD needs to know what the counterpart user in Flatter Files to an user in Azure AD is.</span></span> <span data-ttu-id="9a9dc-142">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-142">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span></span>  

<span data-ttu-id="9a9dc-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Flatter Files.</span></span>

<span data-ttu-id="9a9dc-144">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-144">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a9dc-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9a9dc-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a9dc-147">**[Creating a Flatter Files test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-147">**[Creating a Flatter Files test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9a9dc-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a9dc-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a9dc-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9a9dc-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="9a9dc-151">The objective of this section is to enable Azure AD single sign-on in the Azure AD classic portal and to configure single sign-on in your Flatter Files application.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-151">The objective of this section is to enable Azure AD single sign-on in the Azure AD classic portal and to configure single sign-on in your Flatter Files application.</span></span> <span data-ttu-id="9a9dc-152">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-152">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="9a9dc-153">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="9a9dc-153">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
<span data-ttu-id="9a9dc-154">To configure single sign-on for Flatter Files, you need a registered domain.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-154">To configure single sign-on for Flatter Files, you need a registered domain.</span></span> <span data-ttu-id="9a9dc-155">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="9a9dc-155">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span>  

<span data-ttu-id="9a9dc-156">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9a9dc-156">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="9a9dc-157">In the Azure AD classic portal, on the **Flatter Files** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-157">In the Azure AD classic portal, on the **Flatter Files** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="9a9dc-159">On the **How would you like users to sign on to Flatter Files** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-159">On the **How would you like users to sign on to Flatter Files** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
       <span data-ttu-id="9a9dc-160">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_02.png)</span><span class="sxs-lookup"><span data-stu-id="9a9dc-160">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_02.png)</span></span> 
3. <span data-ttu-id="9a9dc-161">On the **Configure App Settings** dialog page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-161">On the **Configure App Settings** dialog page, click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_03.png) 
   >[!NOTE]
   ><span data-ttu-id="9a9dc-163">Flatter Files uses the same SSO login URL for all the customers: [https://www.flatterfiles.com/site/login/sso/](https://www.flatterfiles.com/site/login/sso/).</span><span class="sxs-lookup"><span data-stu-id="9a9dc-163">Flatter Files uses the same SSO login URL for all the customers: [https://www.flatterfiles.com/site/login/sso/](https://www.flatterfiles.com/site/login/sso/).</span></span>
   > 
   
4. <span data-ttu-id="9a9dc-164">On the **Configure single sign-on at Flatter Files** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-164">On the **Configure single sign-on at Flatter Files** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_04.png)  
    1. <span data-ttu-id="9a9dc-166">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-166">Click **Download certificate**, and then save the file on your computer.</span></span>
    2. <span data-ttu-id="9a9dc-167">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-167">Click **Next**.</span></span>
5. <span data-ttu-id="9a9dc-168">Sign-on to your Flatter Files application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-168">Sign-on to your Flatter Files application as an administrator.</span></span>
6. <span data-ttu-id="9a9dc-169">Click Dashboard.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-169">Click Dashboard.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  
7. <span data-ttu-id="9a9dc-171">Click **Settings**, and then perform the following steps on the **Company** tab:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-171">Click **Settings**, and then perform the following steps on the **Company** tab:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    1. <span data-ttu-id="9a9dc-173">Select **Use SAML 2.0 for Authentication**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-173">Select **Use SAML 2.0 for Authentication**.</span></span>
    2. <span data-ttu-id="9a9dc-174">Click **Configure SAML**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-174">Click **Configure SAML**.</span></span>
8. <span data-ttu-id="9a9dc-175">On the **SAML Configuration** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-175">On the **SAML Configuration** dialog, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   1. <span data-ttu-id="9a9dc-177">In the Domain textbox, type your registered domain.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-177">In the Domain textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="9a9dc-178">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com] (mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="9a9dc-178">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com] (mailto:support@flatterfiles.com).</span></span> 
    >    
   2. <span data-ttu-id="9a9dc-179">In the Azure classic portal, on the Configure single sign-on at Flatter Files dialog, copt the Single Sign-On Service URL, and then paste it into the Identity Provider URL textbox.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-179">In the Azure classic portal, on the Configure single sign-on at Flatter Files dialog, copt the Single Sign-On Service URL, and then paste it into the Identity Provider URL textbox.</span></span>
   3.  <span data-ttu-id="9a9dc-180">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-180">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
 
   >[!TIP]
   ><span data-ttu-id="9a9dc-181">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="9a9dc-181">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
   >  
   4.  <span data-ttu-id="9a9dc-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **FlatterFiles Identity Provider Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **FlatterFiles Identity Provider Certificate** textbox.</span></span>
   5. <span data-ttu-id="9a9dc-183">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-183">Click **Update**.</span></span>
9. <span data-ttu-id="9a9dc-184">In the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-184">In the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Single Sign-On][10]
10. <span data-ttu-id="9a9dc-186">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-186">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
     ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a9dc-188">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9a9dc-188">Create an Azure AD test user</span></span>
<span data-ttu-id="9a9dc-189">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-189">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="9a9dc-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9a9dc-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a9dc-192">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-192">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="9a9dc-194">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-194">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="9a9dc-195">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-195">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="9a9dc-197">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-197">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="9a9dc-199">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-199">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_05.png)  
   1. <span data-ttu-id="9a9dc-201">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-201">As Type Of User, select New user in your organization.</span></span>
   2. <span data-ttu-id="9a9dc-202">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-202">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="9a9dc-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-203">Click **Next**.</span></span>
6. <span data-ttu-id="9a9dc-204">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-204">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_06.png) 
   1. <span data-ttu-id="9a9dc-206">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-206">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="9a9dc-207">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-207">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="9a9dc-208">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-208">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="9a9dc-209">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-209">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="9a9dc-210">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-210">Click **Next**.</span></span>
7. <span data-ttu-id="9a9dc-211">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-211">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="9a9dc-213">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-213">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_08.png) 
   1. <span data-ttu-id="9a9dc-215">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-215">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="9a9dc-216">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-216">Click **Complete**.</span></span>   

### <a name="create-a-flatter-files-test-user"></a><span data-ttu-id="9a9dc-217">Create a Flatter Files test user</span><span class="sxs-lookup"><span data-stu-id="9a9dc-217">Create a Flatter Files test user</span></span>
<span data-ttu-id="9a9dc-218">The objective of this section is to create a user called Britta Simon in Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-218">The objective of this section is to create a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="9a9dc-219">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9a9dc-219">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="9a9dc-220">Sign on to your **Flatter Files** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-220">Sign on to your **Flatter Files** company site as administrator.</span></span>
2. <span data-ttu-id="9a9dc-221">In the navigation pane on the left, click **Settings**, and then click the Users **tab**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-221">In the navigation pane on the left, click **Settings**, and then click the Users **tab**.</span></span>
   
    ![Cfreate a Flatter Files User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)
3. <span data-ttu-id="9a9dc-223">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-223">Click **Add User**.</span></span> 
4. <span data-ttu-id="9a9dc-224">On the **Add User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-224">On the **Add User** dialog, perform the following steps:</span></span>
   
    ![Cfreate a Flatter Files User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)
   1. <span data-ttu-id="9a9dc-226">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-226">In the **First Name** textbox, type **Britta**.</span></span>
   2. <span data-ttu-id="9a9dc-227">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-227">In the **Last Name** textbox, type **Simon**.</span></span> 
   3. <span data-ttu-id="9a9dc-228">In the **Email Address** textbox, type Britta's email address in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-228">In the **Email Address** textbox, type Britta's email address in the Azure classic portal.</span></span>
   4. <span data-ttu-id="9a9dc-229">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-229">Click **Submit**.</span></span>   

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9a9dc-230">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9a9dc-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="9a9dc-231">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-231">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Flatter Files.</span></span>

![Assign User][200] 

<span data-ttu-id="9a9dc-233">**To assign Britta Simon to Flatter Files, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9a9dc-233">**To assign Britta Simon to Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="9a9dc-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="9a9dc-236">In the applications list, select **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-236">In the applications list, select **Flatter Files**.</span></span>
   
    ![Assign User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_11.png) 
3. <span data-ttu-id="9a9dc-238">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-238">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="9a9dc-240">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-240">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="9a9dc-241">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="9a9dc-243">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="9a9dc-243">Test single sign-on</span></span>
<span data-ttu-id="9a9dc-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="9a9dc-245">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-245">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a9dc-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9a9dc-246">Additional resources</span></span>
* [<span data-ttu-id="9a9dc-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a9dc-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a9dc-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a9dc-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/tutorial_general_205.png




































