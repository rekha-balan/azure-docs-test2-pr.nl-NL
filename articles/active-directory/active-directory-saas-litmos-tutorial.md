---
title: 'Tutorial: Azure Active Directory integration with Litmos | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Litmos.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jeedes
ms.openlocfilehash: e3de24f24aa4cb4838adabf1b00e9762edc064f1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556618"
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="7bfc0-103">Tutorial: Azure Active Directory integration with Litmos</span><span class="sxs-lookup"><span data-stu-id="7bfc0-103">Tutorial: Azure Active Directory integration with Litmos</span></span>
<span data-ttu-id="7bfc0-104">The objective of this tutorial is to show you how to integrate Litmos with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7bfc0-104">The objective of this tutorial is to show you how to integrate Litmos with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="7bfc0-105">Integrating Litmos with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-105">Integrating Litmos with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="7bfc0-106">You can control in Azure AD who has access to Litmos</span><span class="sxs-lookup"><span data-stu-id="7bfc0-106">You can control in Azure AD who has access to Litmos</span></span> 
* <span data-ttu-id="7bfc0-107">You can enable your users to automatically get signed-on to Litmos single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7bfc0-107">You can enable your users to automatically get signed-on to Litmos single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="7bfc0-108">You can manage your accounts in one central location - the Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bfc0-108">You can manage your accounts in one central location - the Azure Active Directory</span></span> 

<span data-ttu-id="7bfc0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7bfc0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bfc0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7bfc0-110">Prerequisites</span></span>
<span data-ttu-id="7bfc0-111">To configure Azure AD integration with Litmos, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-111">To configure Azure AD integration with Litmos, you need the following items:</span></span>

* <span data-ttu-id="7bfc0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7bfc0-112">An Azure AD subscription</span></span>
* <span data-ttu-id="7bfc0-113">A Litmos single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7bfc0-113">A Litmos single-sign on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="7bfc0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 

<span data-ttu-id="7bfc0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7bfc0-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7bfc0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7bfc0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="7bfc0-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="7bfc0-118">Scenario Description</span></span>
<span data-ttu-id="7bfc0-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  

<span data-ttu-id="7bfc0-120">The scenario outlined in this tutorial consists of three main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="7bfc0-121">Adding Litmos from the gallery</span><span class="sxs-lookup"><span data-stu-id="7bfc0-121">Adding Litmos from the gallery</span></span> 
2. <span data-ttu-id="7bfc0-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7bfc0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-litmos-from-the-gallery"></a><span data-ttu-id="7bfc0-123">Add Litmos from the gallery</span><span class="sxs-lookup"><span data-stu-id="7bfc0-123">Add Litmos from the gallery</span></span>
<span data-ttu-id="7bfc0-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7bfc0-125">**To add Litmos from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7bfc0-125">**To add Litmos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7bfc0-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="7bfc0-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7bfc0-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="7bfc0-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="7bfc0-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="7bfc0-135">In the search box, type **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-135">In the search box, type **Litmos**.</span></span>
   
    ![Applications][5]
7. <span data-ttu-id="7bfc0-137">In the results pane, select **Litmos**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-137">In the results pane, select **Litmos**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][500]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7bfc0-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7bfc0-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7bfc0-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7bfc0-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7bfc0-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos to an user in Azure AD is.</span></span> <span data-ttu-id="7bfc0-142">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-142">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span></span>  

<span data-ttu-id="7bfc0-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Litmos.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Litmos.</span></span>

<span data-ttu-id="7bfc0-144">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-144">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7bfc0-145">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-145">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7bfc0-146">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-146">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7bfc0-147">**[Create a Litmos test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-147">**[Create a Litmos test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7bfc0-148">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-148">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7bfc0-149">**[Test Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-149">**[Test Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7bfc0-150">Configure Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7bfc0-150">Configure Azure AD Single Sign-On</span></span>
<span data-ttu-id="7bfc0-151">The objective of this section is to enable Azure AD single sign-on in the Azure AD classic portal and to configure single sign-on in your Litmos application.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-151">The objective of this section is to enable Azure AD single sign-on in the Azure AD classic portal and to configure single sign-on in your Litmos application.</span></span>  

<span data-ttu-id="7bfc0-152">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-152">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span>  

<span data-ttu-id="7bfc0-153">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="7bfc0-153">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="7bfc0-154">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-154">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span></span>  

![Azure AD Single Sign-On][17] 

<span data-ttu-id="7bfc0-156">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7bfc0-156">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="7bfc0-157">In the Azure AD classic portal, on the **Litmos** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-157">In the Azure AD classic portal, on the **Litmos** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="7bfc0-159">On the **How would you like users to sign on to Litmos** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-159">On the **How would you like users to sign on to Litmos** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 
3. <span data-ttu-id="7bfc0-161">Sign-on to your Litmos company site (e.g.: *https://azureapptest.litmos.com/account/Login*) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-161">Sign-on to your Litmos company site (e.g.: *https://azureapptest.litmos.com/account/Login*) as an administrator.</span></span>
   
    ![Azure AD Single Sign-On][21] 
4. <span data-ttu-id="7bfc0-163">In the navigation bar on the left side, click **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-163">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Azure AD Single Sign-On][22] 
5. <span data-ttu-id="7bfc0-165">Click the **Integrations** tab.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-165">Click the **Integrations** tab.</span></span>
   
    ![Azure AD Single Sign-On][23] 
6. <span data-ttu-id="7bfc0-167">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-167">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![Azure AD Single Sign-On][24] 
7. <span data-ttu-id="7bfc0-169">Copy the value under **The SAML endoiint for litmos is:**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-169">Copy the value under **The SAML endoiint for litmos is:**.</span></span>
   
    ![Azure AD Single Sign-On][26] 
8. <span data-ttu-id="7bfc0-171">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-171">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][8] 
   
    1. <span data-ttu-id="7bfc0-173">In the **Identifier** textbox, type the URL used by your users to sign-on to your Litmos application (e.g.: *https://azureapptest.litmos.com/account/Login*).</span><span class="sxs-lookup"><span data-stu-id="7bfc0-173">In the **Identifier** textbox, type the URL used by your users to sign-on to your Litmos application (e.g.: *https://azureapptest.litmos.com/account/Login*).</span></span>
   
    2. <span data-ttu-id="7bfc0-174">In the **Reply URL** textbox, paste the value you have copied from the Litmos application in the previous step.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-174">In the **Reply URL** textbox, paste the value you have copied from the Litmos application in the previous step.</span></span>
   
    3. <span data-ttu-id="7bfc0-175">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-175">Click **Next**.</span></span>
9. <span data-ttu-id="7bfc0-176">On the **Configure single sign-on at Litmos** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-176">On the **Configure single sign-on at Litmos** page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][2] 
   
    * <span data-ttu-id="7bfc0-178">Click Download certificate, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-178">Click Download certificate, and then save the file on your computer.</span></span>
10. <span data-ttu-id="7bfc0-179">In your **Litmos** application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-179">In your **Litmos** application, perform the following steps:</span></span>
    
     ![Azure AD Single Sign-On][25] 
    
     1. <span data-ttu-id="7bfc0-181">Click **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-181">Click **Enable SAML**.</span></span>
    
     2. <span data-ttu-id="7bfc0-182">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-182">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="7bfc0-183">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="7bfc0-183">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
     >

     3. <span data-ttu-id="7bfc0-184">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-184">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span></span>
    
     4. <span data-ttu-id="7bfc0-185">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-185">Click **Save Changes**.</span></span>
11. <span data-ttu-id="7bfc0-186">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-186">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
    
     ![Azure AD Single Sign-On][10]
12. <span data-ttu-id="7bfc0-188">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-188">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
     ![Azure AD Single Sign-On][11]
13. <span data-ttu-id="7bfc0-190">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-190">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span> 
    
    ![Configure Single Sign-On][12]
14. <span data-ttu-id="7bfc0-192">On the **Add User Attribute** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-192">On the **Add User Attribute** dialog, perform the following steps:</span></span> 
    
    ![Configure Single Sign-On][14]
    
    | <span data-ttu-id="7bfc0-194">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="7bfc0-194">Attribute Name</span></span> | <span data-ttu-id="7bfc0-195">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="7bfc0-195">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="7bfc0-196">Email</span><span class="sxs-lookup"><span data-stu-id="7bfc0-196">Email</span></span> |<span data-ttu-id="7bfc0-197">user.mail</span><span class="sxs-lookup"><span data-stu-id="7bfc0-197">user.mail</span></span> |
    | <span data-ttu-id="7bfc0-198">FirstName</span><span class="sxs-lookup"><span data-stu-id="7bfc0-198">FirstName</span></span> |<span data-ttu-id="7bfc0-199">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7bfc0-199">user.givenname</span></span> |
    | <span data-ttu-id="7bfc0-200">Lastname</span><span class="sxs-lookup"><span data-stu-id="7bfc0-200">Lastname</span></span> |<span data-ttu-id="7bfc0-201">user.surname</span><span class="sxs-lookup"><span data-stu-id="7bfc0-201">user.surname</span></span> |
    
    <span data-ttu-id="7bfc0-202">For each data row in the table above, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-202">For each data row in the table above, perform the following steps:</span></span>
    
 1. <span data-ttu-id="7bfc0-203">Click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-203">Click **add user attribute**.</span></span>    
   <span data-ttu-id="7bfc0-204">![Configure Single Sign-On][15]</span><span class="sxs-lookup"><span data-stu-id="7bfc0-204">![Configure Single Sign-On][15]</span></span>
 2. <span data-ttu-id="7bfc0-205">In the **Attribute Name** textbox, type the **Attribute Name** shown for that row.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-205">In the **Attribute Name** textbox, type the **Attribute Name** shown for that row.</span></span>
 3. <span data-ttu-id="7bfc0-206">Select the **Attribute Value** shown for that row.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-206">Select the **Attribute Value** shown for that row.</span></span>
 4. <span data-ttu-id="7bfc0-207">Click **Complete** to close the **Add User Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-207">Click **Complete** to close the **Add User Attribute** dialog.</span></span>


1. <span data-ttu-id="7bfc0-208">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-208">Click **Apply Changes**.</span></span> 
   
   ![Configure Single Sign-On][16]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7bfc0-210">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7bfc0-210">Create an Azure AD test user</span></span>
<span data-ttu-id="7bfc0-211">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-211">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="7bfc0-213">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7bfc0-213">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7bfc0-214">In the **Azure clasic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-214">In the **Azure clasic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="7bfc0-216">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-216">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7bfc0-217">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-217">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="7bfc0-219">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-219">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="7bfc0-221">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-221">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/create_aaduser_05.png)  
   
    1. <span data-ttu-id="7bfc0-223">As **Type Of User**, select **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-223">As **Type Of User**, select **New user in your organization**.</span></span>
   
    2. <span data-ttu-id="7bfc0-224">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-224">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    3. <span data-ttu-id="7bfc0-225">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-225">Click **Next**.</span></span>
6. <span data-ttu-id="7bfc0-226">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-226">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="7bfc0-228">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-228">In the **First Name** textbox, type **Britta**.</span></span>  
   
   2. <span data-ttu-id="7bfc0-229">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-229">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   3. <span data-ttu-id="7bfc0-230">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-230">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   4. <span data-ttu-id="7bfc0-231">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-231">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="7bfc0-232">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-232">Click **Next**.</span></span>
7. <span data-ttu-id="7bfc0-233">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-233">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="7bfc0-235">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bfc0-235">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/create_aaduser_08.png) 
   
    1. <span data-ttu-id="7bfc0-237">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-237">Write down the value of the **New Password**.</span></span>
   
    2. <span data-ttu-id="7bfc0-238">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-238">Click **Complete**.</span></span>   

### <a name="create-a-litmos-test-user"></a><span data-ttu-id="7bfc0-239">Create a Litmos test user</span><span class="sxs-lookup"><span data-stu-id="7bfc0-239">Create a Litmos test user</span></span>
<span data-ttu-id="7bfc0-240">The objective of this section is to create a user called Britta Simon in Litmos.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-240">The objective of this section is to create a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="7bfc0-241">The Litmos application supports Just-in-Time provisioning.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-241">The Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="7bfc0-242">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-242">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

<span data-ttu-id="7bfc0-243">**To create a user called Britta Simon in Litmos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7bfc0-243">**To create a user called Britta Simon in Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="7bfc0-244">Sign-on to your Litmos company site (e.g.: *https://azureapptest.litmos.com/account/Login*) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-244">Sign-on to your Litmos company site (e.g.: *https://azureapptest.litmos.com/account/Login*) as an administrator.</span></span>
   
    ![Azure AD Single Sign-On][21] 
2. <span data-ttu-id="7bfc0-246">In the navigation bar on the left side, click **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-246">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Azure AD Single Sign-On][22] 
3. <span data-ttu-id="7bfc0-248">Click the **Integrations** tab.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-248">Click the **Integrations** tab.</span></span>
   
    ![Azure AD Single Sign-On][23] 
4. <span data-ttu-id="7bfc0-250">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-250">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![Azure AD Single Sign-On][24] 
5. <span data-ttu-id="7bfc0-252">Select **Autogenerate Users:**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-252">Select **Autogenerate Users:**.</span></span>
   
    ![Azure AD Single Sign-On][27] 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7bfc0-254">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7bfc0-254">Assign the Azure AD test user</span></span>
<span data-ttu-id="7bfc0-255">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Litmos.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-255">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Litmos.</span></span>

![Assign User][200] 

<span data-ttu-id="7bfc0-257">**To assign Britta Simon to Litmos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7bfc0-257">**To assign Britta Simon to Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="7bfc0-258">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-258">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="7bfc0-260">In the applications list, select **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-260">In the applications list, select **Litmos**.</span></span>
   
    ![Assign User][202] 
3. <span data-ttu-id="7bfc0-262">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-262">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="7bfc0-264">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-264">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="7bfc0-265">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-265">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="7bfc0-267">Test Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7bfc0-267">Test Single Sign-On</span></span>
<span data-ttu-id="7bfc0-268">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-268">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="7bfc0-269">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span><span class="sxs-lookup"><span data-stu-id="7bfc0-269">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7bfc0-270">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="7bfc0-270">Additional Resources</span></span>
* [<span data-ttu-id="7bfc0-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bfc0-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7bfc0-272">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7bfc0-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_01.png
[500]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_02.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_07.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_80.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_81.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_82.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_81.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_19.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_67.png


[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_100.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_litmos_68.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-litmos-tutorial/tutorial_general_205.png


[400]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_400.png
[401]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_401.png
[402]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_402.png










































