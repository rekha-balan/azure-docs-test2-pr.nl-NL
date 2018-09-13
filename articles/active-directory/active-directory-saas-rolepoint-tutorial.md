---
title: 'Tutorial: Azure Active Directory integration with RolePoint | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and RolePoint.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 2bc11444d858c6c2f5130bc5869313afaa77ae50
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553881"
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="19bfb-103">Tutorial: Azure Active Directory integration with RolePoint</span><span class="sxs-lookup"><span data-stu-id="19bfb-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="19bfb-104">In this tutorial, you learn how to integrate RolePoint with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19bfb-104">In this tutorial, you learn how to integrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19bfb-105">Integrating RolePoint with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="19bfb-105">Integrating RolePoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="19bfb-106">You can control in Azure AD who has access to RolePoint</span><span class="sxs-lookup"><span data-stu-id="19bfb-106">You can control in Azure AD who has access to RolePoint</span></span>
- <span data-ttu-id="19bfb-107">You can enable your users to automatically get signed-on to RolePoint single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="19bfb-107">You can enable your users to automatically get signed-on to RolePoint single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="19bfb-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="19bfb-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="19bfb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19bfb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19bfb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="19bfb-110">Prerequisites</span></span>

<span data-ttu-id="19bfb-111">To configure Azure AD integration with RolePoint, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="19bfb-111">To configure Azure AD integration with RolePoint, you need the following items:</span></span>

- <span data-ttu-id="19bfb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="19bfb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19bfb-113">A RolePoint SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="19bfb-113">A RolePoint SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="19bfb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="19bfb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="19bfb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="19bfb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19bfb-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="19bfb-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="19bfb-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19bfb-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19bfb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="19bfb-118">Scenario description</span></span>
<span data-ttu-id="19bfb-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="19bfb-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="19bfb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="19bfb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19bfb-121">Adding RolePoint from the gallery</span><span class="sxs-lookup"><span data-stu-id="19bfb-121">Adding RolePoint from the gallery</span></span>
2. <span data-ttu-id="19bfb-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="19bfb-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-rolepoint-from-the-gallery"></a><span data-ttu-id="19bfb-123">Add RolePoint from the gallery</span><span class="sxs-lookup"><span data-stu-id="19bfb-123">Add RolePoint from the gallery</span></span>
<span data-ttu-id="19bfb-124">To configure the integration of RolePoint into Azure AD, you need to add RolePoint from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="19bfb-124">To configure the integration of RolePoint into Azure AD, you need to add RolePoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="19bfb-125">**To add RolePoint from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19bfb-125">**To add RolePoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="19bfb-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="19bfb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="19bfb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="19bfb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="19bfb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="19bfb-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="19bfb-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="19bfb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="19bfb-135">In the search box, type **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-135">In the search box, type **RolePoint**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_001.png)

7. <span data-ttu-id="19bfb-137">In the results pane, select **RolePoint**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="19bfb-137">In the results pane, select **RolePoint**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="19bfb-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="19bfb-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="19bfb-140">In this section, you configure and test Azure AD SSO with RolePoint based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="19bfb-140">In this section, you configure and test Azure AD SSO with RolePoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="19bfb-141">For SSO to work, Azure AD needs to know what the counterpart user in RolePoint is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19bfb-141">For SSO to work, Azure AD needs to know what the counterpart user in RolePoint is to a user in Azure AD.</span></span> <span data-ttu-id="19bfb-142">In other words, a link relationship between an Azure AD user and the related user in RolePoint needs to be established.</span><span class="sxs-lookup"><span data-stu-id="19bfb-142">In other words, a link relationship between an Azure AD user and the related user in RolePoint needs to be established.</span></span>

<span data-ttu-id="19bfb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RolePoint.</span><span class="sxs-lookup"><span data-stu-id="19bfb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RolePoint.</span></span>

<span data-ttu-id="19bfb-144">To configure and test Azure AD SSO with RolePoint, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="19bfb-144">To configure and test Azure AD SSO with RolePoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="19bfb-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="19bfb-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="19bfb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19bfb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19bfb-147">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - to have a counterpart of Britta Simon in RolePoint that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="19bfb-147">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - to have a counterpart of Britta Simon in RolePoint that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="19bfb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="19bfb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19bfb-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="19bfb-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="19bfb-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="19bfb-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="19bfb-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your RolePoint application.</span><span class="sxs-lookup"><span data-stu-id="19bfb-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="19bfb-152">RolePoint application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="19bfb-152">RolePoint application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="19bfb-153">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="19bfb-153">Please configure the following claims for this application.</span></span> <span data-ttu-id="19bfb-154">You can manage the values of these attributes from the "**Atrribute**" tab of the application.</span><span class="sxs-lookup"><span data-stu-id="19bfb-154">You can manage the values of these attributes from the "**Atrribute**" tab of the application.</span></span> <span data-ttu-id="19bfb-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="19bfb-155">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_01.png)

<span data-ttu-id="19bfb-157">**To configure Azure AD single sign-on with RolePoint, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19bfb-157">**To configure Azure AD single sign-on with RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="19bfb-158">In the Azure classic portal, on the **RolePoint** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-158">In the Azure classic portal, on the **RolePoint** application integration page, in the menu on the top, click **Attributes**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_02.png)

2. <span data-ttu-id="19bfb-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19bfb-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>    

    | <span data-ttu-id="19bfb-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="19bfb-161">Attribute Name</span></span> | <span data-ttu-id="19bfb-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="19bfb-162">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="19bfb-163">FirstName</span><span class="sxs-lookup"><span data-stu-id="19bfb-163">FirstName</span></span> | <span data-ttu-id="19bfb-164">user.givenname</span><span class="sxs-lookup"><span data-stu-id="19bfb-164">user.givenname</span></span> |
    | <span data-ttu-id="19bfb-165">LastName</span><span class="sxs-lookup"><span data-stu-id="19bfb-165">LastName</span></span> | <span data-ttu-id="19bfb-166">user.surname</span><span class="sxs-lookup"><span data-stu-id="19bfb-166">user.surname</span></span> |
    | <span data-ttu-id="19bfb-167">Email</span><span class="sxs-lookup"><span data-stu-id="19bfb-167">Email</span></span> | <span data-ttu-id="19bfb-168">user.mail</span><span class="sxs-lookup"><span data-stu-id="19bfb-168">user.mail</span></span> |
 
  1. <span data-ttu-id="19bfb-169">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="19bfb-169">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_03.png)
  2. <span data-ttu-id="19bfb-171">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="19bfb-171">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  3. <span data-ttu-id="19bfb-172">From the **Attribute Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="19bfb-172">From the **Attribute Value** list, type the attribute value shown for that row.</span></span>
  4. <span data-ttu-id="19bfb-173">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-173">Click **Complete**.</span></span>

3. <span data-ttu-id="19bfb-174">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-174">In the menu on the top, click **Quick Start**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_04.png) 

4. <span data-ttu-id="19bfb-176">On the **How would you like users to sign on to RolePoint** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-176">On the **How would you like users to sign on to RolePoint** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_05.png)

5. <span data-ttu-id="19bfb-178">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19bfb-178">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_06.png)
  1. <span data-ttu-id="19bfb-180">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="19bfb-180">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.rolepoint.com/login`</span></span>
  2. <span data-ttu-id="19bfb-181">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-181">Click **Next**.</span></span>
  
    >[!NOTE] 
    ><span data-ttu-id="19bfb-182">Please note that this is not the real value.</span><span class="sxs-lookup"><span data-stu-id="19bfb-182">Please note that this is not the real value.</span></span> <span data-ttu-id="19bfb-183">You have to update this value with the actual Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="19bfb-183">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="19bfb-184">Contact [RolePoint support team](emaiLto:info@rolepoint.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="19bfb-184">Contact [RolePoint support team](emaiLto:info@rolepoint.com) to get this value.</span></span>
    >

6. <span data-ttu-id="19bfb-185">On the **Configure single sign-on at RolePoint** page, click **Download metadata** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="19bfb-185">On the **Configure single sign-on at RolePoint** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_07.png) 

7. <span data-ttu-id="19bfb-187">To get SSO configured for your application, contact [RolePoint support team](emaiLto:info@rolepoint.com) and provide them with the downloaded **Metadata**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-187">To get SSO configured for your application, contact [RolePoint support team](emaiLto:info@rolepoint.com) and provide them with the downloaded **Metadata**.</span></span>

8. <span data-ttu-id="19bfb-188">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-188">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD Single Sign-On][10]

9. <span data-ttu-id="19bfb-190">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-190">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="19bfb-192">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="19bfb-192">Create an Azure AD test user</span></span>
<span data-ttu-id="19bfb-193">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19bfb-193">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="19bfb-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19bfb-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="19bfb-196">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-196">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="19bfb-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="19bfb-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="19bfb-199">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-199">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19bfb-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="19bfb-203">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19bfb-203">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="19bfb-205">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="19bfb-205">As Type Of User, select New user in your organization.</span></span>
 2. <span data-ttu-id="19bfb-206">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-206">In the User Name **textbox**, type **BrittaSimon**.</span></span>
 3. <span data-ttu-id="19bfb-207">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-207">Click **Next**.</span></span>

6.  <span data-ttu-id="19bfb-208">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19bfb-208">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/create_aaduser_06.png) 
 1. <span data-ttu-id="19bfb-210">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-210">In the **First Name** textbox, type **Britta**.</span></span> 
 2. <span data-ttu-id="19bfb-211">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-211">In the **Last Name** textbox, type, **Simon**.</span></span>
 3. <span data-ttu-id="19bfb-212">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-212">In the **Display Name** textbox, type **Britta Simon**.</span></span>
 4. <span data-ttu-id="19bfb-213">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-213">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="19bfb-214">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-214">Click **Next**.</span></span>

7. <span data-ttu-id="19bfb-215">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-215">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="19bfb-217">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19bfb-217">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="19bfb-219">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-219">Write down the value of the **New Password**.</span></span>
 2. <span data-ttu-id="19bfb-220">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-220">Click **Complete**.</span></span>   

### <a name="create-a-rolepoint-test-user"></a><span data-ttu-id="19bfb-221">Create a RolePoint test user</span><span class="sxs-lookup"><span data-stu-id="19bfb-221">Create a RolePoint test user</span></span>

<span data-ttu-id="19bfb-222">In this section, you create a user called Britta Simon in RolePoint.</span><span class="sxs-lookup"><span data-stu-id="19bfb-222">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="19bfb-223">Please work with [RolePoint support team](emaiLto:info@rolepoint.com) to add the users in the RolePoint platform.</span><span class="sxs-lookup"><span data-stu-id="19bfb-223">Please work with [RolePoint support team](emaiLto:info@rolepoint.com) to add the users in the RolePoint platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="19bfb-224">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="19bfb-224">Assign the Azure AD test user</span></span>

<span data-ttu-id="19bfb-225">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to RolePoint.</span><span class="sxs-lookup"><span data-stu-id="19bfb-225">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to RolePoint.</span></span>

![Assign User][200] 

<span data-ttu-id="19bfb-227">**To assign Britta Simon to RolePoint, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19bfb-227">**To assign Britta Simon to RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="19bfb-228">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="19bfb-228">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="19bfb-230">In the applications list, select **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-230">In the applications list, select **RolePoint**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_50.png) 

3. <span data-ttu-id="19bfb-232">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-232">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203] 

4. <span data-ttu-id="19bfb-234">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-234">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="19bfb-235">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="19bfb-235">In the toolbar on the bottom, click **Assign**.</span></span>
    
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="19bfb-237">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="19bfb-237">Test single sign-on</span></span>

<span data-ttu-id="19bfb-238">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="19bfb-238">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="19bfb-239">When you click the RolePoint tile in the Access Panel, you should get automatically signed-on to your RolePoint application.</span><span class="sxs-lookup"><span data-stu-id="19bfb-239">When you click the RolePoint tile in the Access Panel, you should get automatically signed-on to your RolePoint application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19bfb-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="19bfb-240">Additional resources</span></span>

* [<span data-ttu-id="19bfb-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19bfb-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19bfb-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="19bfb-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rolepoint-tutorial/tutorial_general_205.png





























