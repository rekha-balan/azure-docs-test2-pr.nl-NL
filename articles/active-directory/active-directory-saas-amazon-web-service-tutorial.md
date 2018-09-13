---
title: 'Tutorial: Azure Active Directory integration with Amazon Web Services (AWS) | Microsoft Docs'
description: Learn how to use Amazon Web Services (AWS) with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 2aafe870e60a091f4f4687bd8e12edabda4d869e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556698"
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="281e0-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="281e0-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>
<span data-ttu-id="281e0-104">The objective of this tutorial is to show you how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="281e0-104">The objective of this tutorial is to show you how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="281e0-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="281e0-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="281e0-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="281e0-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span></span> 
* <span data-ttu-id="281e0-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="281e0-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="281e0-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="281e0-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="281e0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="281e0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="281e0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="281e0-110">Prerequisites</span></span>
<span data-ttu-id="281e0-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="281e0-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

* <span data-ttu-id="281e0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="281e0-112">An Azure AD subscription</span></span>
* <span data-ttu-id="281e0-113">An Amazon Web Services (AWS) SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="281e0-113">An Amazon Web Services (AWS) SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="281e0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="281e0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="281e0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="281e0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="281e0-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="281e0-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="281e0-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="281e0-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="281e0-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="281e0-118">Scenario Description</span></span>
<span data-ttu-id="281e0-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="281e0-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="281e0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="281e0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="281e0-121">Adding Amazon Web Services (AWS) from the gallery</span><span class="sxs-lookup"><span data-stu-id="281e0-121">Adding Amazon Web Services (AWS) from the gallery</span></span> 
2. <span data-ttu-id="281e0-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="281e0-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="281e0-123">Add Amazon Web Services (AWS) from the gallery</span><span class="sxs-lookup"><span data-stu-id="281e0-123">Add Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="281e0-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="281e0-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="281e0-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="281e0-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="281e0-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="281e0-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 

2. <span data-ttu-id="281e0-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="281e0-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="281e0-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="281e0-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span> 
   
    ![Applications][2]

4. <span data-ttu-id="281e0-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="281e0-131">Click **Add** at the bottom of the page.</span></span> 
   
    ![Applications][3]

5. <span data-ttu-id="281e0-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="281e0-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span> 
   
    ![Applications][4]

6. <span data-ttu-id="281e0-135">In the search box, type **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="281e0-135">In the search box, type **Amazon Web Services (AWS)**.</span></span>
   
    ![Applications][5]

7. <span data-ttu-id="281e0-137">In the results pane, select **Amazon Web Services (AWS)**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="281e0-137">In the results pane, select **Amazon Web Services (AWS)**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][6]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="281e0-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="281e0-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="281e0-140">The objective of this section is to show you how to configure and test Azure AD SSO with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="281e0-140">The objective of this section is to show you how to configure and test Azure AD SSO with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="281e0-141">For SSO to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="281e0-141">For SSO to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) to an user in Azure AD is.</span></span> <span data-ttu-id="281e0-142">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="281e0-142">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>  

<span data-ttu-id="281e0-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="281e0-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="281e0-144">To configure and test Azure AD SSO with Amazon Web Services (AWS), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="281e0-144">To configure and test Azure AD SSO with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="281e0-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="281e0-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="281e0-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="281e0-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="281e0-147">**[Creating a Amazon Web Services (AWS) test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="281e0-147">**[Creating a Amazon Web Services (AWS) test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="281e0-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="281e0-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="281e0-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="281e0-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="281e0-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="281e0-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="281e0-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your Amazon Web Services (AWS) application.</span><span class="sxs-lookup"><span data-stu-id="281e0-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your Amazon Web Services (AWS) application.</span></span>  

<span data-ttu-id="281e0-152">Your Amazon Web Services (AWS) application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="281e0-152">Your Amazon Web Services (AWS) application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="281e0-153">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="281e0-153">The following screenshot shows an example for this.</span></span>

![Configure Single Sign-On][27]

<span data-ttu-id="281e0-155">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="281e0-155">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="281e0-156">In the Azure classic portal, on the **Amazon Web Services (AWS)** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="281e0-156">In the Azure classic portal, on the **Amazon Web Services (AWS)** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7]

2. <span data-ttu-id="281e0-158">On the **How would you like users to sign on to Amazon Web Services (AWS)** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="281e0-158">On the **How would you like users to sign on to Amazon Web Services (AWS)** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On][8]

3. <span data-ttu-id="281e0-160">On the **Configure App Settings** dialog page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="281e0-160">On the **Configure App Settings** dialog page, click **Next**.</span></span> 
   
    ![Configure App Settings][9]

4. <span data-ttu-id="281e0-162">On the **Configure single sign-on at Amazon Web Services (AWS)** page, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="281e0-162">On the **Configure single sign-on at Amazon Web Services (AWS)** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![Configure Single Sign-On][10]

5. <span data-ttu-id="281e0-164">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="281e0-164">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

6. <span data-ttu-id="281e0-165">Click **Console Home**.</span><span class="sxs-lookup"><span data-stu-id="281e0-165">Click **Console Home**.</span></span>
   
    ![Configure Single Sign-On][11]

7. <span data-ttu-id="281e0-167">Click **Identity and Access Management**.</span><span class="sxs-lookup"><span data-stu-id="281e0-167">Click **Identity and Access Management**.</span></span> 
   
    ![Configure Single Sign-On][12]

8. <span data-ttu-id="281e0-169">Click **Identity Providers**, and then click **Create Provider**.</span><span class="sxs-lookup"><span data-stu-id="281e0-169">Click **Identity Providers**, and then click **Create Provider**.</span></span> 
   
    ![Configure Single Sign-On][13]

9. <span data-ttu-id="281e0-171">On the **Configure Provider** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="281e0-171">On the **Configure Provider** dialog page, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On][14]   
  1. <span data-ttu-id="281e0-173">As **Provider Type**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="281e0-173">As **Provider Type**, select **SAML**.</span></span>
  2. <span data-ttu-id="281e0-174">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="281e0-174">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>
  3. <span data-ttu-id="281e0-175">To upload your downloaded metadata file, click **Choose File**.</span><span class="sxs-lookup"><span data-stu-id="281e0-175">To upload your downloaded metadata file, click **Choose File**.</span></span>
  4. <span data-ttu-id="281e0-176">Click **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="281e0-176">Click **Next Step**.</span></span>

10. <span data-ttu-id="281e0-177">On the **Verify Provider Information** dialog page, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="281e0-177">On the **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Configure Single Sign-On][15]

11. <span data-ttu-id="281e0-179">Click **Roles**, and then click **Create New Role**.</span><span class="sxs-lookup"><span data-stu-id="281e0-179">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Configure Single Sign-On][16]

12. <span data-ttu-id="281e0-181">On the **Set Role Name** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="281e0-181">On the **Set Role Name** dialog, perform the following steps:</span></span> 
    
    ![Configure Single Sign-On][17] 
  1. <span data-ttu-id="281e0-183">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="281e0-183">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 
  2. <span data-ttu-id="281e0-184">Click **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="281e0-184">Click **Next Step**.</span></span>

13. <span data-ttu-id="281e0-185">On the **Select Role Type** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="281e0-185">On the **Select Role Type** dialog, perform the following steps:</span></span> 
    
    ![Configure Single Sign-On][18] 
  1. <span data-ttu-id="281e0-187">Select **Role For Identity Provider Access**.</span><span class="sxs-lookup"><span data-stu-id="281e0-187">Select **Role For Identity Provider Access**.</span></span> 
  2. <span data-ttu-id="281e0-188">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span><span class="sxs-lookup"><span data-stu-id="281e0-188">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span></span>

14. <span data-ttu-id="281e0-189">On the **Establish Trust** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="281e0-189">On the **Establish Trust** dialog, perform the following steps:</span></span>  
    
    ![Configure Single Sign-On][19] 
  1. <span data-ttu-id="281e0-191">As SAML provider, select the SAML provider you have created previousley (e.g.: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="281e0-191">As SAML provider, select the SAML provider you have created previousley (e.g.: *WAAD*)</span></span>   
  2. <span data-ttu-id="281e0-192">Click **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="281e0-192">Click **Next Step**.</span></span>

15. <span data-ttu-id="281e0-193">On the **Verify Role Trust** dialog, click **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="281e0-193">On the **Verify Role Trust** dialog, click **Next Step**.</span></span> 
    
    ![Configure Single Sign-On][32]

16. <span data-ttu-id="281e0-195">On the **Attach Policy** dialog, click **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="281e0-195">On the **Attach Policy** dialog, click **Next Step**.</span></span>  
    
    ![Configure Single Sign-On][33]

17. <span data-ttu-id="281e0-197">On the **Review** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="281e0-197">On the **Review** dialog, perform the following steps:</span></span>   
    
    ![Configure Single Sign-On][34] 
  1. <span data-ttu-id="281e0-199">Copy the **Role ARN** value.</span><span class="sxs-lookup"><span data-stu-id="281e0-199">Copy the **Role ARN** value.</span></span>  
  2. <span data-ttu-id="281e0-200">Copy the **Trusted Entities** ARN value.</span><span class="sxs-lookup"><span data-stu-id="281e0-200">Copy the **Trusted Entities** ARN value.</span></span> 
  3. <span data-ttu-id="281e0-201">Click **Create Role**.</span><span class="sxs-lookup"><span data-stu-id="281e0-201">Click **Create Role**.</span></span> 

18. <span data-ttu-id="281e0-202">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="281e0-202">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![What is Azure AD Connect][20]

19. <span data-ttu-id="281e0-204">On the **Single sign-on confirmation** page, click **Complete** to close the **Configure single sign-on** dialog.</span><span class="sxs-lookup"><span data-stu-id="281e0-204">On the **Single sign-on confirmation** page, click **Complete** to close the **Configure single sign-on** dialog.</span></span>
    
    ![What is Azure AD Connect][22]

20. <span data-ttu-id="281e0-206">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="281e0-206">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span> 
    
    ![Configure Single Sign-On][21]

21. <span data-ttu-id="281e0-208">Click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="281e0-208">Click **add user attribute**.</span></span> 
    
    ![Configure Single Sign-On][23]

22. <span data-ttu-id="281e0-210">On the Add User Attribute dialog, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="281e0-210">On the Add User Attribute dialog, perform the following steps.</span></span> 
    
    ![Configure Single Sign-On][24]  
  1. <span data-ttu-id="281e0-212">In the **Attribute Name** textbox, type **https://aws.amazon.com/SAML/Attributes/Role**.</span><span class="sxs-lookup"><span data-stu-id="281e0-212">In the **Attribute Name** textbox, type **https://aws.amazon.com/SAML/Attributes/Role**.</span></span>  
  2. <span data-ttu-id="281e0-213">In the **Attribute Value** textbox, type **[the Role ARN value],[the Trusted Entity ARN value]**.</span><span class="sxs-lookup"><span data-stu-id="281e0-213">In the **Attribute Value** textbox, type **[the Role ARN value],[the Trusted Entity ARN value]**.</span></span>
    
     >[!TIP]
     ><span data-ttu-id="281e0-214">These are the values you have copied from the Review dialog when you have created your role.</span><span class="sxs-lookup"><span data-stu-id="281e0-214">These are the values you have copied from the Review dialog when you have created your role.</span></span> 
     > 
     
  3. <span data-ttu-id="281e0-215">Click **Complete** to close the **Add User Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="281e0-215">Click **Complete** to close the **Add User Attribute** dialog.</span></span>

23. <span data-ttu-id="281e0-216">Click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="281e0-216">Click **add user attribute**.</span></span> 
    
    ![Configure Single Sign-On][23]

24. <span data-ttu-id="281e0-218">On the Add User Attribute dialog, perform the following steps, and then click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="281e0-218">On the Add User Attribute dialog, perform the following steps, and then click **Apply Changes**.</span></span> 
    
    ![Configure Single Sign-On][25]
 1. <span data-ttu-id="281e0-220">In the **Attribute Name** textbox, type **https://aws.amazon.com/SAML/Attributes/RoleSessionName**.</span><span class="sxs-lookup"><span data-stu-id="281e0-220">In the **Attribute Name** textbox, type **https://aws.amazon.com/SAML/Attributes/RoleSessionName**.</span></span>
 2. <span data-ttu-id="281e0-221">In the **Attribute Value** textbox, type or select **user.userprincipalname** from the drop down list.</span><span class="sxs-lookup"><span data-stu-id="281e0-221">In the **Attribute Value** textbox, type or select **user.userprincipalname** from the drop down list.</span></span>

     ![Configure Single Sign-On][35]
 3. <span data-ttu-id="281e0-223">Click **Complete** to close the **Add User Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="281e0-223">Click **Complete** to close the **Add User Attribute** dialog.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="281e0-224">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="281e0-224">Create an Azure AD test user</span></span>
<span data-ttu-id="281e0-225">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="281e0-225">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png)

<span data-ttu-id="281e0-227">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="281e0-227">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="281e0-228">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="281e0-228">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

2. <span data-ttu-id="281e0-230">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="281e0-230">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="281e0-231">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="281e0-231">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="281e0-233">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="281e0-233">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="281e0-235">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="281e0-235">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="281e0-237">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="281e0-237">As Type Of User, select New user in your organization.</span></span>
 2. <span data-ttu-id="281e0-238">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="281e0-238">In the User Name **textbox**, type **BrittaSimon**.</span></span>
 3. <span data-ttu-id="281e0-239">Click Next.</span><span class="sxs-lookup"><span data-stu-id="281e0-239">Click Next.</span></span>

6. <span data-ttu-id="281e0-240">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="281e0-240">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="281e0-242">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="281e0-242">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="281e0-243">In the **Last Name** txtbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="281e0-243">In the **Last Name** txtbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="281e0-244">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="281e0-244">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="281e0-245">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="281e0-245">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="281e0-246">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="281e0-246">Click **Next**.</span></span>

7. <span data-ttu-id="281e0-247">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="281e0-247">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="281e0-249">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="281e0-249">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="281e0-251">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="281e0-251">Write down the value of the **New Password**.</span></span>  
 2. <span data-ttu-id="281e0-252">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="281e0-252">Click **Complete**.</span></span>   

### <a name="create-a-amazon-web-services-aws-test-user"></a><span data-ttu-id="281e0-253">Create a Amazon Web Services (AWS) test user</span><span class="sxs-lookup"><span data-stu-id="281e0-253">Create a Amazon Web Services (AWS) test user</span></span>
<span data-ttu-id="281e0-254">The objective of this section is to create a user called Britta Simon in Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="281e0-254">The objective of this section is to create a user called Britta Simon in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="281e0-255">**To create a user called Britta Simon in Amazon Web Services (AWS), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="281e0-255">**To create a user called Britta Simon in Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="281e0-256">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="281e0-256">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="281e0-257">Click the **Console Home** icon.</span><span class="sxs-lookup"><span data-stu-id="281e0-257">Click the **Console Home** icon.</span></span> 
   
    ![Configure Single Sign-On][11]

3. <span data-ttu-id="281e0-259">Click Identity and Access Management.</span><span class="sxs-lookup"><span data-stu-id="281e0-259">Click Identity and Access Management.</span></span> 
   
    ![Configure Single Sign-On][28]

4. <span data-ttu-id="281e0-261">In the Dashboard, click Users, and then click Create New Users.</span><span class="sxs-lookup"><span data-stu-id="281e0-261">In the Dashboard, click Users, and then click Create New Users.</span></span> 
   
    ![Configure Single Sign-On][29]

5. <span data-ttu-id="281e0-263">On the Create User dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="281e0-263">On the Create User dialog, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On][30]   
 1. <span data-ttu-id="281e0-265">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="281e0-265">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span> 
 2. <span data-ttu-id="281e0-266">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="281e0-266">Click **Create**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="281e0-267">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="281e0-267">Assign the Azure AD test user</span></span>
<span data-ttu-id="281e0-268">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="281e0-268">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Amazon Web Services (AWS).</span></span>

![Assign User][31]

<span data-ttu-id="281e0-270">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="281e0-270">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="281e0-271">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="281e0-271">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][26]

2. <span data-ttu-id="281e0-273">In the applications list, select **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="281e0-273">In the applications list, select **Amazon Web Services (AWS)**.</span></span>
   
    ![Assign User][27]

3. <span data-ttu-id="281e0-275">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="281e0-275">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][25]

4. <span data-ttu-id="281e0-277">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="281e0-277">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="281e0-278">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="281e0-278">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][29]

### <a name="test-single-sign-on"></a><span data-ttu-id="281e0-280">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="281e0-280">Test single sign-on</span></span>
<span data-ttu-id="281e0-281">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="281e0-281">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="281e0-282">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span><span class="sxs-lookup"><span data-stu-id="281e0-282">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="281e0-283">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="281e0-283">Additional Resources</span></span>
* [<span data-ttu-id="281e0-284">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="281e0-284">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="281e0-285">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="281e0-285">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795019.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795020.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795027.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795028.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/capture23.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/capture24.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_18.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950357.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_16.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_17.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/user_attributes_01.png

































































