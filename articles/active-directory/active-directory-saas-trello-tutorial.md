---
title: 'Tutorial: Azure Active Directory integration with Trello | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Trello.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: jeedes
ms.openlocfilehash: 0d6b955c035e028c1ab1bedaf9312900458cecc7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563918"
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="1bf39-103">Tutorial: Azure Active Directory integration with Trello</span><span class="sxs-lookup"><span data-stu-id="1bf39-103">Tutorial: Azure Active Directory integration with Trello</span></span>
<span data-ttu-id="1bf39-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1bf39-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1bf39-105">Integrating Trello with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1bf39-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1bf39-106">You can control in Azure AD who has access to Trello</span><span class="sxs-lookup"><span data-stu-id="1bf39-106">You can control in Azure AD who has access to Trello</span></span>
* <span data-ttu-id="1bf39-107">You can enable your users to automatically get signed-on to Trello single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1bf39-107">You can enable your users to automatically get signed-on to Trello single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="1bf39-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="1bf39-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1bf39-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1bf39-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bf39-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1bf39-110">Prerequisites</span></span>
<span data-ttu-id="1bf39-111">To configure Azure AD integration with Trello, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1bf39-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

* <span data-ttu-id="1bf39-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1bf39-112">An Azure AD subscription</span></span>
* <span data-ttu-id="1bf39-113">A **Trello** single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1bf39-113">A **Trello** single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1bf39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1bf39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="1bf39-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1bf39-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1bf39-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="1bf39-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1bf39-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1bf39-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1bf39-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1bf39-118">Scenario description</span></span>
<span data-ttu-id="1bf39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1bf39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1bf39-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1bf39-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1bf39-121">Adding Trello from the gallery</span><span class="sxs-lookup"><span data-stu-id="1bf39-121">Adding Trello from the gallery</span></span>
2. <span data-ttu-id="1bf39-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1bf39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-trello-from-the-gallery"></a><span data-ttu-id="1bf39-123">Add Trello from the gallery</span><span class="sxs-lookup"><span data-stu-id="1bf39-123">Add Trello from the gallery</span></span>
<span data-ttu-id="1bf39-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1bf39-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1bf39-125">**To add Trello from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1bf39-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1bf39-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="1bf39-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1bf39-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1bf39-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1bf39-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="1bf39-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1bf39-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="1bf39-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="1bf39-135">In the search box, type **Trello**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-135">In the search box, type **Trello**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_01.png)

7. <span data-ttu-id="1bf39-137">In the results pane, select **Trello**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1bf39-137">In the results pane, select **Trello**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="1bf39-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1bf39-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="1bf39-140">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1bf39-140">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1bf39-141">For SSO to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bf39-141">For SSO to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="1bf39-142">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1bf39-142">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="1bf39-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Trello.</span><span class="sxs-lookup"><span data-stu-id="1bf39-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Trello.</span></span> <span data-ttu-id="1bf39-144">To configure and test Azure AD SSO with Trello, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1bf39-144">To configure and test Azure AD SSO with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1bf39-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1bf39-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1bf39-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1bf39-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1bf39-147">**[Creating a Trello test user](#creating-a-the-funding-portal-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="1bf39-147">**[Creating a Trello test user](#creating-a-the-funding-portal-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1bf39-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1bf39-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1bf39-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1bf39-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1bf39-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1bf39-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="1bf39-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Trello application.</span><span class="sxs-lookup"><span data-stu-id="1bf39-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="1bf39-152">Trello application expects the SAML assertions to contain specific attributes.</span><span class="sxs-lookup"><span data-stu-id="1bf39-152">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="1bf39-153">Please configure the following attributes  for this application.</span><span class="sxs-lookup"><span data-stu-id="1bf39-153">Please configure the following attributes  for this application.</span></span> <span data-ttu-id="1bf39-154">You can manage the values of these attributes from the **"Atrributes"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="1bf39-154">You can manage the values of these attributes from the **"Atrributes"** tab of the application.</span></span> <span data-ttu-id="1bf39-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="1bf39-155">The following screenshot shows an example for this.</span></span>

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_03.png) 

<span data-ttu-id="1bf39-157">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1bf39-157">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="1bf39-158">In the Azure classic portal, on the **Trello** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-158">In the Azure classic portal, on the **Trello** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On][5]

2. <span data-ttu-id="1bf39-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1bf39-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>

    | <span data-ttu-id="1bf39-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="1bf39-161">Attribute Name</span></span> | <span data-ttu-id="1bf39-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="1bf39-162">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="1bf39-163">User.Email</span><span class="sxs-lookup"><span data-stu-id="1bf39-163">User.Email</span></span> | <span data-ttu-id="1bf39-164">user.mail</span><span class="sxs-lookup"><span data-stu-id="1bf39-164">user.mail</span></span> |
    | <span data-ttu-id="1bf39-165">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="1bf39-165">User.FirstName</span></span> | <span data-ttu-id="1bf39-166">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1bf39-166">user.givenname</span></span> |
    | <span data-ttu-id="1bf39-167">User.LastName</span><span class="sxs-lookup"><span data-stu-id="1bf39-167">User.LastName</span></span> | <span data-ttu-id="1bf39-168">user.surname</span><span class="sxs-lookup"><span data-stu-id="1bf39-168">user.surname</span></span> |

   1. <span data-ttu-id="1bf39-169">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="1bf39-169">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_05.png)
   2. <span data-ttu-id="1bf39-171">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="1bf39-171">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="1bf39-172">From the **Attribute Value** list, select the value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="1bf39-172">From the **Attribute Value** list, select the value shown for that row.</span></span>
   4. <span data-ttu-id="1bf39-173">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-173">Click **Complete**.</span></span> <span data-ttu-id="1bf39-174">Then, **Apply Changes** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1bf39-174">Then, **Apply Changes** at the bottom of the page.</span></span>

1. <span data-ttu-id="1bf39-175">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-175">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On][6]

2. <span data-ttu-id="1bf39-177">In the classic portal, on the **Trello** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="1bf39-177">In the classic portal, on the **Trello** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7] 

3. <span data-ttu-id="1bf39-179">On the **How would you like users to sign on to Trello** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-179">On the **How would you like users to sign on to Trello** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_06.png)

4. <span data-ttu-id="1bf39-181">On the **Configure App Settings** dialog page, if you wish to configure the application in **IDP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1bf39-181">On the **Configure App Settings** dialog page, if you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_07.png)

   1. <span data-ttu-id="1bf39-183">In the Reply URL text box, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="1bf39-183">In the Reply URL text box, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>
   2. <span data-ttu-id="1bf39-184">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-184">Click **Next**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="1bf39-185">You should get the **\<enterprise\>** slug from Trello.</span><span class="sxs-lookup"><span data-stu-id="1bf39-185">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="1bf39-186">If you don't have the slug value, please contact Trello support team at <mailto:support@trello.com> to get the slug for you enterprise.</span><span class="sxs-lookup"><span data-stu-id="1bf39-186">If you don't have the slug value, please contact Trello support team at <mailto:support@trello.com> to get the slug for you enterprise.</span></span>
    > 
    > 

5. <span data-ttu-id="1bf39-187">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL**:</span><span class="sxs-lookup"><span data-stu-id="1bf39-187">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_08.png)
   
   1. <span data-ttu-id="1bf39-189">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="1bf39-189">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>
   2. <span data-ttu-id="1bf39-190">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-190">Click **Next**.</span></span>

6. <span data-ttu-id="1bf39-191">On the **Configure single sign-on at Trello** page, Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1bf39-191">On the **Configure single sign-on at Trello** page, Click **Download certificate**, and then save the file on your computer.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_09.png)

7. <span data-ttu-id="1bf39-193">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send Trello team the Sign On URL and attach downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="1bf39-193">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send Trello team the Sign On URL and attach downloaded certificate.</span></span>
8. <span data-ttu-id="1bf39-194">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-194">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

9. <span data-ttu-id="1bf39-196">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-196">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1bf39-198">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1bf39-198">Create an Azure AD test user</span></span>
<span data-ttu-id="1bf39-199">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1bf39-199">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="1bf39-201">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1bf39-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1bf39-202">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-202">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="1bf39-204">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1bf39-204">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1bf39-205">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-205">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1bf39-207">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-207">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="1bf39-209">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1bf39-209">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_05.png) 
   
   1. <span data-ttu-id="1bf39-211">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="1bf39-211">As Type Of User, select New user in your organization.</span></span>
   2. <span data-ttu-id="1bf39-212">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-212">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="1bf39-213">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-213">Click **Next**.</span></span>

6. <span data-ttu-id="1bf39-214">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1bf39-214">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="1bf39-216">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-216">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="1bf39-217">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-217">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="1bf39-218">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-218">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="1bf39-219">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-219">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="1bf39-220">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-220">Click **Next**.</span></span>

7. <span data-ttu-id="1bf39-221">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-221">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="1bf39-223">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1bf39-223">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_08.png) 
   
   1. <span data-ttu-id="1bf39-225">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-225">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="1bf39-226">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-226">Click **Complete**.</span></span>   

### <a name="create-a-trello-test-user"></a><span data-ttu-id="1bf39-227">Create a Trello test user</span><span class="sxs-lookup"><span data-stu-id="1bf39-227">Create a Trello test user</span></span>
<span data-ttu-id="1bf39-228">In this section, you create a user called Britta Simon in Trello.</span><span class="sxs-lookup"><span data-stu-id="1bf39-228">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="1bf39-229">In this section, you create a user called Britta Simon in Trello.</span><span class="sxs-lookup"><span data-stu-id="1bf39-229">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="1bf39-230">Trello supports just-in-time provisioning and a new account will be created the first time you sign in from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bf39-230">Trello supports just-in-time provisioning and a new account will be created the first time you sign in from Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1bf39-231">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1bf39-231">Assign the Azure AD test user</span></span>
<span data-ttu-id="1bf39-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Trello.</span><span class="sxs-lookup"><span data-stu-id="1bf39-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Trello.</span></span>

![Assign User][200] 

<span data-ttu-id="1bf39-234">**To assign Britta Simon to Trello, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1bf39-234">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="1bf39-235">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1bf39-235">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="1bf39-237">In the applications list, select **Trello**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-237">In the applications list, select **Trello**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_10.png) 

3. <span data-ttu-id="1bf39-239">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-239">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 

4. <span data-ttu-id="1bf39-241">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-241">In the All Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1bf39-242">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1bf39-242">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="1bf39-244">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1bf39-244">Test single sign-on</span></span>
<span data-ttu-id="1bf39-245">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1bf39-245">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1bf39-246">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span><span class="sxs-lookup"><span data-stu-id="1bf39-246">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1bf39-247">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1bf39-247">Additional resources</span></span>
* [<span data-ttu-id="1bf39-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1bf39-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1bf39-249">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1bf39-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-trello-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_205.png






























