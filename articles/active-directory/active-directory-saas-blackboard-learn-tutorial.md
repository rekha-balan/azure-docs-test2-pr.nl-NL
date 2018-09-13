---
title: 'Tutorial: Azure Active Directory integration with Blackboard Learn | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Blackboard Learn.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 7aa08085056b389aab234b24fd7a45a06d7c9a15
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550588"
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="99f88-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="99f88-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>
<span data-ttu-id="99f88-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99f88-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99f88-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="99f88-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="99f88-106">You can control in Azure AD who has access to Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="99f88-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
* <span data-ttu-id="99f88-107">You can enable your users to automatically get signed-on to Blackboard Learn single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="99f88-107">You can enable your users to automatically get signed-on to Blackboard Learn single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="99f88-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="99f88-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="99f88-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99f88-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99f88-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99f88-110">Prerequisites</span></span>
<span data-ttu-id="99f88-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="99f88-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

* <span data-ttu-id="99f88-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="99f88-112">An Azure AD subscription</span></span>
* <span data-ttu-id="99f88-113">A Blackboard Learn Cloud Platform single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="99f88-113">A Blackboard Learn Cloud Platform single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="99f88-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="99f88-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="99f88-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="99f88-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="99f88-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="99f88-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="99f88-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99f88-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="99f88-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="99f88-118">Scenario Description</span></span>
<span data-ttu-id="99f88-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="99f88-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="99f88-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="99f88-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="99f88-121">Adding Blackboard Learn from the gallery</span><span class="sxs-lookup"><span data-stu-id="99f88-121">Adding Blackboard Learn from the gallery</span></span>
* <span data-ttu-id="99f88-122">Configuring and testing Azure AD single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="99f88-122">Configuring and testing Azure AD single sign-on (SSO)</span></span>

## <a name="add-blackboard-learn-from-the-gallery"></a><span data-ttu-id="99f88-123">Add Blackboard Learn from the gallery</span><span class="sxs-lookup"><span data-stu-id="99f88-123">Add Blackboard Learn from the gallery</span></span>
<span data-ttu-id="99f88-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="99f88-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="99f88-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99f88-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="99f88-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99f88-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="99f88-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="99f88-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="99f88-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="99f88-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="99f88-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="99f88-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="99f88-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="99f88-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="99f88-135">In the search box, type **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="99f88-135">In the search box, type **Blackboard Learn**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_01.png)
7. <span data-ttu-id="99f88-137">In the results pane, select **Blackboard Learn**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="99f88-137">In the results pane, select **Blackboard Learn**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_06.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="99f88-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99f88-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="99f88-140">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="99f88-140">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99f88-141">For SSO to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99f88-141">For SSO to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="99f88-142">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span><span class="sxs-lookup"><span data-stu-id="99f88-142">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="99f88-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="99f88-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="99f88-144">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="99f88-144">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="99f88-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="99f88-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="99f88-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99f88-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99f88-147">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="99f88-147">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="99f88-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="99f88-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99f88-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="99f88-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="99f88-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99f88-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="99f88-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Blackboard Learn application.</span><span class="sxs-lookup"><span data-stu-id="99f88-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="99f88-152">Blackboard Learn application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="99f88-152">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="99f88-153">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="99f88-153">Please configure the following claims for this application.</span></span> <span data-ttu-id="99f88-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="99f88-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="99f88-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="99f88-155">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_51.png) 

<span data-ttu-id="99f88-157">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99f88-157">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="99f88-158">In the Azure classic portal, on the **Blackboard Learn** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="99f88-158">In the Azure classic portal, on the **Blackboard Learn** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_80.png) 
2. <span data-ttu-id="99f88-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps: We have map the Userprincipalname as the unique user attribute here but you can map it to the appropriate value which uniquely distinguish the user in the organization and that maps to Blackboard learn username field.</span><span class="sxs-lookup"><span data-stu-id="99f88-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps: We have map the Userprincipalname as the unique user attribute here but you can map it to the appropriate value which uniquely distinguish the user in the organization and that maps to Blackboard learn username field.</span></span>
   
   | <span data-ttu-id="99f88-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="99f88-161">Attribute Name</span></span> | <span data-ttu-id="99f88-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="99f88-162">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="99f88-163">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="99f88-163">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="99f88-164">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="99f88-164">user.userprincipalname</span></span> |

    1. <span data-ttu-id="99f88-165">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="99f88-165">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_81.png) 
    2. <span data-ttu-id="99f88-167">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="99f88-167">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span></span>
    3. <span data-ttu-id="99f88-168">From the **Attribute Value** list, selsect the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="99f88-168">From the **Attribute Value** list, selsect the attribute value shown for that row.</span></span>
    4. <span data-ttu-id="99f88-169">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="99f88-169">Click **Complete**.</span></span>    

1. <span data-ttu-id="99f88-170">In the classic portal, on the **Blackboard Learn** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="99f88-170">In the classic portal, on the **Blackboard Learn** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="99f88-172">On the **How would you like users to sign on to Blackboard Learn** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99f88-172">On the **How would you like users to sign on to Blackboard Learn** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_03.png) 
3. <span data-ttu-id="99f88-174">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99f88-174">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_04.png) 
    1. <span data-ttu-id="99f88-176">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Blackboard Learn application using the following pattern: **https://\<company name-pricing\>.blackboard.com/**.</span><span class="sxs-lookup"><span data-stu-id="99f88-176">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Blackboard Learn application using the following pattern: **https://\<company name-pricing\>.blackboard.com/**.</span></span>
    2. <span data-ttu-id="99f88-177">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99f88-177">click **Next**.</span></span>
4. <span data-ttu-id="99f88-178">On the **Configure single sign-on at Blackboard Learn** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99f88-178">On the **Configure single sign-on at Blackboard Learn** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_05.png)
    1. <span data-ttu-id="99f88-180">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="99f88-180">Click **Download metadata**, and then save the file on your computer.</span></span>
    2. <span data-ttu-id="99f88-181">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99f88-181">Click **Next**.</span></span>
5. <span data-ttu-id="99f88-182">To get SSO configured for your application, contact Blackboard Learn support team and provide them with the downloaded metadata.</span><span class="sxs-lookup"><span data-stu-id="99f88-182">To get SSO configured for your application, contact Blackboard Learn support team and provide them with the downloaded metadata.</span></span>
6. <span data-ttu-id="99f88-183">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99f88-183">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="99f88-185">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="99f88-185">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="99f88-187">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99f88-187">Create an Azure AD test user</span></span>
<span data-ttu-id="99f88-188">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99f88-188">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="99f88-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99f88-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="99f88-191">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99f88-191">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="99f88-193">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="99f88-193">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="99f88-194">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="99f88-194">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="99f88-196">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="99f88-196">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png)   
5. <span data-ttu-id="99f88-198">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99f88-198">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_05.png) 
    1. <span data-ttu-id="99f88-200">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="99f88-200">As Type Of User, select New user in your organization.</span></span>
    2. <span data-ttu-id="99f88-201">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99f88-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
    3. <span data-ttu-id="99f88-202">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99f88-202">Click **Next**.</span></span>
6. <span data-ttu-id="99f88-203">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99f88-203">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_06.png) 
   1. <span data-ttu-id="99f88-205">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="99f88-205">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="99f88-206">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="99f88-206">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="99f88-207">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99f88-207">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="99f88-208">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="99f88-208">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="99f88-209">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99f88-209">Click **Next**.</span></span>
7. <span data-ttu-id="99f88-210">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="99f88-210">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="99f88-212">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99f88-212">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_08.png) 
    1. <span data-ttu-id="99f88-214">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="99f88-214">Write down the value of the **New Password**.</span></span>
    2. <span data-ttu-id="99f88-215">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="99f88-215">Click **Complete**.</span></span>   

### <a name="create-an-blackboard-learn-test-user"></a><span data-ttu-id="99f88-216">Create an Blackboard Learn test user</span><span class="sxs-lookup"><span data-stu-id="99f88-216">Create an Blackboard Learn test user</span></span>
<span data-ttu-id="99f88-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="99f88-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="99f88-218">Blackboard Learn application support  just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="99f88-218">Blackboard Learn application support  just in time user provisioning.</span></span> <span data-ttu-id="99f88-219">Please make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="99f88-219">Please make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="99f88-220">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99f88-220">Assign the Azure AD test user</span></span>
<span data-ttu-id="99f88-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="99f88-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Blackboard Learn.</span></span>

![Assign User][200] 

<span data-ttu-id="99f88-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99f88-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="99f88-224">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="99f88-224">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="99f88-226">In the applications list, select **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="99f88-226">In the applications list, select **Blackboard Learn**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_50.png) 
3. <span data-ttu-id="99f88-228">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="99f88-228">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="99f88-230">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99f88-230">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="99f88-231">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="99f88-231">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="99f88-233">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="99f88-233">Test single sign-on</span></span>
<span data-ttu-id="99f88-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="99f88-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="99f88-235">Blackboard Learn application support When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span><span class="sxs-lookup"><span data-stu-id="99f88-235">Blackboard Learn application support When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99f88-236">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="99f88-236">Additional Resources</span></span>
* [<span data-ttu-id="99f88-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99f88-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99f88-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99f88-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_205.png




























