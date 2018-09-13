---
title: 'Tutorial: Azure Active Directory integration with Halogen Software'
description: Learn how to configure single sign-on between Azure Active Directory and Halogen Software.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 9c86fe24bef880eedc7e5d9f7a38feae980fe84d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550945"
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="ffdaa-103">Tutorial: Azure Active Directory integration with Halogen Software</span><span class="sxs-lookup"><span data-stu-id="ffdaa-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>
<span data-ttu-id="ffdaa-104">The objective of this tutorial is to show you how to integrate Halogen Software with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ffdaa-104">The objective of this tutorial is to show you how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ffdaa-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="ffdaa-106">You can control in Azure AD who has access to Halogen Software</span><span class="sxs-lookup"><span data-stu-id="ffdaa-106">You can control in Azure AD who has access to Halogen Software</span></span> 
* <span data-ttu-id="ffdaa-107">You can enable your users to automatically get signed-on to Halogen Software single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ffdaa-107">You can enable your users to automatically get signed-on to Halogen Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="ffdaa-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="ffdaa-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="ffdaa-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ffdaa-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffdaa-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ffdaa-110">Prerequisites</span></span>
<span data-ttu-id="ffdaa-111">To configure Azure AD integration with Halogen Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

* <span data-ttu-id="ffdaa-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ffdaa-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ffdaa-113">A Halogen Software SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ffdaa-113">A Halogen Software SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ffdaa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="ffdaa-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ffdaa-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ffdaa-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ffdaa-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="ffdaa-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="ffdaa-118">Scenario Description</span></span>
<span data-ttu-id="ffdaa-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="ffdaa-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ffdaa-121">Adding Halogen Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="ffdaa-121">Adding Halogen Software from the gallery</span></span> 
2. <span data-ttu-id="ffdaa-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ffdaa-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="ffdaa-123">Adding Halogen Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="ffdaa-123">Adding Halogen Software from the gallery</span></span>
<span data-ttu-id="ffdaa-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ffdaa-125">**To add Halogen Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ffdaa-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ffdaa-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="ffdaa-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ffdaa-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="ffdaa-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-131">Click **Add** at the bottom of the page.</span></span>    
   
    ![Applications][3]
5. <span data-ttu-id="ffdaa-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="ffdaa-135">In the search box, type **halogen software**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-135">In the search box, type **halogen software**.</span></span>
   
    ![Applications][5]
7. <span data-ttu-id="ffdaa-137">In the results pane, select **Halogen Software**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-137">In the results pane, select **Halogen Software**, and then click **Complete** to add the application.</span></span>

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="ffdaa-138">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ffdaa-138">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="ffdaa-139">The objective of this section is to show you how to configure and test Azure AD SSO with Halogen Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ffdaa-139">The objective of this section is to show you how to configure and test Azure AD SSO with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ffdaa-140">For SSO to work, Azure AD needs to know what the counterpart user in Halogen Software to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-140">For SSO to work, Azure AD needs to know what the counterpart user in Halogen Software to an user in Azure AD is.</span></span> <span data-ttu-id="ffdaa-141">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-141">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="ffdaa-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Halogen Software.</span></span>

<span data-ttu-id="ffdaa-143">To configure and test Azure AD SSO with Halogen Software, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-143">To configure and test Azure AD SSO with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ffdaa-144">**[Configuring Azure AD Single single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-144">**[Configuring Azure AD Single single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ffdaa-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ffdaa-146">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-146">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ffdaa-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ffdaa-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="ffdaa-149">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ffdaa-149">Configure Azure AD SSO</span></span>
<span data-ttu-id="ffdaa-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Halogen Software application.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Halogen Software application.</span></span>

<span data-ttu-id="ffdaa-151">**To configure Azure AD SSO with Halogen Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ffdaa-151">**To configure Azure AD SSO with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="ffdaa-152">In the Azure classic portal, on the **Halogen Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-152">In the Azure classic portal, on the **Halogen Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][8]
2. <span data-ttu-id="ffdaa-154">On the **How would you like users to sign on to Halogen Software** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-154">On the **How would you like users to sign on to Halogen Software** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][9]
3. <span data-ttu-id="ffdaa-156">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-156">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure App Settings][10]
   1. <span data-ttu-id="ffdaa-158">in the **Sign On URL** textbox, type your URL used by your users to sign on to your Halogen Software application using the following pattern: *https://global.hgncloud.com/fabrikam/welcome.jsp*</span><span class="sxs-lookup"><span data-stu-id="ffdaa-158">in the **Sign On URL** textbox, type your URL used by your users to sign on to your Halogen Software application using the following pattern: *https://global.hgncloud.com/fabrikam/welcome.jsp*</span></span>
   2. <span data-ttu-id="ffdaa-159">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-159">Click **Next**.</span></span>
4. <span data-ttu-id="ffdaa-160">On the **Configure single sign-on at Halogen Software** page, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-160">On the **Configure single sign-on at Halogen Software** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![What is Azure AD Connect][11]
5. <span data-ttu-id="ffdaa-162">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-162">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>
6. <span data-ttu-id="ffdaa-163">Click the **Options** tab.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-163">Click the **Options** tab.</span></span> 
   
    ![What is Azure AD Connect][12]
7. <span data-ttu-id="ffdaa-165">In the left navigation pane, click **SAML Configuration**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-165">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![What is Azure AD Connect][13]
8. <span data-ttu-id="ffdaa-167">On the **SAML Configuration** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-167">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![What is Azure AD Connect][14]
  1. <span data-ttu-id="ffdaa-169">As **Unique Identifier**, select **NameID**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-169">As **Unique Identifier**, select **NameID**.</span></span>
  2. <span data-ttu-id="ffdaa-170">As **Unique Identifier Maps To**, select **Username**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-170">As **Unique Identifier Maps To**, select **Username**.</span></span>
  3. <span data-ttu-id="ffdaa-171">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-171">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
  4. <span data-ttu-id="ffdaa-172">To test the configuration, click **Run Test**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-172">To test the configuration, click **Run Test**.</span></span> 
    >[!NOTE]
    ><span data-ttu-id="ffdaa-173">You need to wait for the message "*The SAML test is complete. Please close this window*".</span><span class="sxs-lookup"><span data-stu-id="ffdaa-173">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="ffdaa-174">Then, close the opened browser window.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-174">Then, close the opened browser window.</span></span> <span data-ttu-id="ffdaa-175">The **Enable SAML** checkbox is only enabled if the test has been completed.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-175">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
    >
  5. <span data-ttu-id="ffdaa-176">Select **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-176">Select **Enable SAML**.</span></span>
  6. <span data-ttu-id="ffdaa-177">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-177">Click **Save Changes**.</span></span> 
9. <span data-ttu-id="ffdaa-178">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-178">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span> 
   
    ![What is Azure AD Connect][15]
10. <span data-ttu-id="ffdaa-180">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-180">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![What is Azure AD Connect][16]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ffdaa-182">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ffdaa-182">Create an Azure AD test user</span></span>
<span data-ttu-id="ffdaa-183">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-183">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="ffdaa-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ffdaa-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ffdaa-185">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-185">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![What is Azure AD Connect][100] 
2. <span data-ttu-id="ffdaa-187">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-187">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ffdaa-188">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-188">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![What is Azure AD Connect][101] 
4. <span data-ttu-id="ffdaa-190">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-190">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![What is Azure AD Connect][102] 
5. <span data-ttu-id="ffdaa-192">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-192">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![What is Azure AD Connect][103] 
  1. <span data-ttu-id="ffdaa-194">As **Type Of User**, select **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-194">As **Type Of User**, select **New user in your organization**.</span></span>
  2. <span data-ttu-id="ffdaa-195">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-195">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="ffdaa-196">Click Next.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-196">Click Next.</span></span>
6. <span data-ttu-id="ffdaa-197">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-197">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![What is Azure AD Connect][104] 
  1. <span data-ttu-id="ffdaa-199">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-199">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="ffdaa-200">In the **Last Name** txtbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-200">In the **Last Name** txtbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="ffdaa-201">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-201">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="ffdaa-202">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-202">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="ffdaa-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-203">Click **Next**.</span></span>
7. <span data-ttu-id="ffdaa-204">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-204">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![What is Azure AD Connect][105]  
8. <span data-ttu-id="ffdaa-206">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-206">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![What is Azure AD Connect][106]   
  1. <span data-ttu-id="ffdaa-208">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-208">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="ffdaa-209">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-209">Click **Complete**.</span></span>   

### <a name="create-a-halogen-software-test-user"></a><span data-ttu-id="ffdaa-210">Create a Halogen Software test user</span><span class="sxs-lookup"><span data-stu-id="ffdaa-210">Create a Halogen Software test user</span></span>
<span data-ttu-id="ffdaa-211">The objective of this section is to create a user called Britta Simon in Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-211">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="ffdaa-212">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ffdaa-212">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="ffdaa-213">Sign on to your **Halogen Software** application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-213">Sign on to your **Halogen Software** application as an administrator.</span></span>
2. <span data-ttu-id="ffdaa-214">Click the **User Center** tab, and then click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-214">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![What is Azure AD Connect][300]  
3. <span data-ttu-id="ffdaa-216">On the **New User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ffdaa-216">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![What is Azure AD Connect][301]
  1. <span data-ttu-id="ffdaa-218">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-218">In the **First Name** textbox, type **Britta**.</span></span> 
  2. <span data-ttu-id="ffdaa-219">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-219">In the **Last Name** textbox, type **Simon**.</span></span> 
  3. <span data-ttu-id="ffdaa-220">In the **Username** textbox, type **Brita Simon's user name in the Azure classic portal**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-220">In the **Username** textbox, type **Brita Simon's user name in the Azure classic portal**.</span></span>
  4. <span data-ttu-id="ffdaa-221">In the **Password** textbox, type a password for Britta.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-221">In the **Password** textbox, type a password for Britta.</span></span>
  5. <span data-ttu-id="ffdaa-222">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-222">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ffdaa-223">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ffdaa-223">Assign the Azure AD test user</span></span>
<span data-ttu-id="ffdaa-224">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-224">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Halogen Software.</span></span>

![What is Azure AD Connect][200]

<span data-ttu-id="ffdaa-226">**To assign Britta Simon to Halogen Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ffdaa-226">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="ffdaa-227">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-227">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![What is Azure AD Connect][201]
2. <span data-ttu-id="ffdaa-229">In the applications list, select **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-229">In the applications list, select **Halogen Software**.</span></span>
   
    ![What is Azure AD Connect][202]
3. <span data-ttu-id="ffdaa-231">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-231">In the menu on the top, click **Users**.</span></span>
   
    ![What is Azure AD Connect][203]
4. <span data-ttu-id="ffdaa-233">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-233">In the Users list, select **Britta Simon**.</span></span>
   
    ![What is Azure AD Connect][204]
5. <span data-ttu-id="ffdaa-235">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-235">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![What is Azure AD Connect][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="ffdaa-237">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ffdaa-237">Test single sign-on</span></span>
<span data-ttu-id="ffdaa-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ffdaa-239">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span><span class="sxs-lookup"><span data-stu-id="ffdaa-239">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ffdaa-240">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="ffdaa-240">Additional Resources</span></span>
* [<span data-ttu-id="ffdaa-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffdaa-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ffdaa-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ffdaa-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_05.png
[6]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_06.png
[7]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_07.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_08.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_09.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_10.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_11.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_15.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_16.png
[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_100.png 
[101]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_101.png 
[102]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_102.png 
[103]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_103.png 
[104]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_104.png 
[105]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_105.png 
[106]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_106.png 
[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_200.png 
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_201.png 
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_203.png
[204]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_205.png
[300]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png
[301]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png





























