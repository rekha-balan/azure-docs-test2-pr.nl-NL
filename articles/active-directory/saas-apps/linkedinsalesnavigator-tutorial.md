---
title: 'Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LinkedInSalesNavigator.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2018
ms.author: jeedes
ms.openlocfilehash: f0e34a614251cf11c9547d749fef58dfa8ca623a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868514"
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="edc3a-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="edc3a-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="edc3a-104">In this tutorial, you learn how to integrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="edc3a-104">In this tutorial, you learn how to integrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="edc3a-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="edc3a-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="edc3a-106">You can control in Azure AD who has access to LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="edc3a-106">You can control in Azure AD who has access to LinkedIn Sales Navigator</span></span>
- <span data-ttu-id="edc3a-107">You can enable your users to automatically get signed-on to LinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="edc3a-107">You can enable your users to automatically get signed-on to LinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="edc3a-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="edc3a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="edc3a-109">If you want to know more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="edc3a-109">If you want to know more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edc3a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="edc3a-110">Prerequisites</span></span>

<span data-ttu-id="edc3a-111">To configure Azure AD integration with LinkedIn Sales Navigator, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="edc3a-111">To configure Azure AD integration with LinkedIn Sales Navigator, you need the following items:</span></span>

- <span data-ttu-id="edc3a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="edc3a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="edc3a-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="edc3a-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="edc3a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="edc3a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="edc3a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="edc3a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edc3a-116">Avoid using your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="edc3a-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="edc3a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="edc3a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="edc3a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="edc3a-118">Scenario description</span></span>
<span data-ttu-id="edc3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="edc3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="edc3a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="edc3a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edc3a-121">Adding LinkedIn Sales Navigator from the gallery</span><span class="sxs-lookup"><span data-stu-id="edc3a-121">Adding LinkedIn Sales Navigator from the gallery</span></span>
1. <span data-ttu-id="edc3a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="edc3a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-the-gallery"></a><span data-ttu-id="edc3a-123">Adding LinkedIn Sales Navigator from the gallery</span><span class="sxs-lookup"><span data-stu-id="edc3a-123">Adding LinkedIn Sales Navigator from the gallery</span></span>
<span data-ttu-id="edc3a-124">To configure the integration of LinkedIn Sales Navigator into Azure AD, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="edc3a-124">To configure the integration of LinkedIn Sales Navigator into Azure AD, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="edc3a-125">**To add LinkedIn Sales Navigator from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edc3a-125">**To add LinkedIn Sales Navigator from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="edc3a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="edc3a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="edc3a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="edc3a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="edc3a-131">Click **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="edc3a-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="edc3a-133">In the search box, type **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-133">In the search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Creating an Azure AD test user](./media/linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

1. <span data-ttu-id="edc3a-135">In the results panel, select **LinkedIn Sales Navigator**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="edc3a-135">In the results panel, select **LinkedIn Sales Navigator**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="edc3a-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="edc3a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="edc3a-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="edc3a-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="edc3a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Sales Navigator is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edc3a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Sales Navigator is to a user in Azure AD.</span></span> <span data-ttu-id="edc3a-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Sales Navigator needs to be established.</span><span class="sxs-lookup"><span data-stu-id="edc3a-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Sales Navigator needs to be established.</span></span>

<span data-ttu-id="edc3a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="edc3a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="edc3a-142">To configure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="edc3a-142">To configure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="edc3a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="edc3a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="edc3a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edc3a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="edc3a-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - to have a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked to the Azure AD representation of the user.</span><span class="sxs-lookup"><span data-stu-id="edc3a-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - to have a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked to the Azure AD representation of the user.</span></span>
1. <span data-ttu-id="edc3a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="edc3a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="edc3a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="edc3a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="edc3a-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="edc3a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="edc3a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span><span class="sxs-lookup"><span data-stu-id="edc3a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="edc3a-150">**To configure Azure AD single sign-on with LinkedIn Sales Navigator, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edc3a-150">**To configure Azure AD single sign-on with LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="edc3a-151">In the Azure portal, on the **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-151">In the Azure portal, on the **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="edc3a-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="edc3a-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

1. <span data-ttu-id="edc3a-155">In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.</span><span class="sxs-lookup"><span data-stu-id="edc3a-155">In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.</span></span>

1. <span data-ttu-id="edc3a-156">In **Account Center**, click **Global Settings** under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="edc3a-157">Also, select **Sales Navigator** from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="edc3a-157">Also, select **Sales Navigator** from the dropdown list.</span></span>

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

1. <span data-ttu-id="edc3a-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

1. <span data-ttu-id="edc3a-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode.</span><span class="sxs-lookup"><span data-stu-id="edc3a-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode.</span></span>

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="edc3a-163">a.</span><span class="sxs-lookup"><span data-stu-id="edc3a-163">a.</span></span> <span data-ttu-id="edc3a-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="edc3a-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="edc3a-165">b.</span><span class="sxs-lookup"><span data-stu-id="edc3a-165">b.</span></span> <span data-ttu-id="edc3a-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="edc3a-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

1. <span data-ttu-id="edc3a-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode.</span><span class="sxs-lookup"><span data-stu-id="edc3a-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode.</span></span>

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="edc3a-169">In the **Sign-on URL** textbox, type the value using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="edc3a-169">In the **Sign-on URL** textbox, type the value using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

1. <span data-ttu-id="edc3a-170">Your **LinkedIn Sales Navigator** application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="edc3a-170">Your **LinkedIn Sales Navigator** application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="edc3a-171">The following screenshot shows an example.</span><span class="sxs-lookup"><span data-stu-id="edc3a-171">The following screenshot shows an example.</span></span> <span data-ttu-id="edc3a-172">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it to be mapped with the user's email address.</span><span class="sxs-lookup"><span data-stu-id="edc3a-172">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it to be mapped with the user's email address.</span></span> <span data-ttu-id="edc3a-173">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span><span class="sxs-lookup"><span data-stu-id="edc3a-173">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/updateusermail.png)
    
1. <span data-ttu-id="edc3a-175">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span><span class="sxs-lookup"><span data-stu-id="edc3a-175">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="edc3a-176">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span><span class="sxs-lookup"><span data-stu-id="edc3a-176">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="edc3a-177">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="edc3a-177">Attribute Name</span></span> | <span data-ttu-id="edc3a-178">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="edc3a-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="edc3a-179">email</span><span class="sxs-lookup"><span data-stu-id="edc3a-179">email</span></span>| <span data-ttu-id="edc3a-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="edc3a-180">user.mail</span></span> |
    | <span data-ttu-id="edc3a-181">department</span><span class="sxs-lookup"><span data-stu-id="edc3a-181">department</span></span>| <span data-ttu-id="edc3a-182">user.department</span><span class="sxs-lookup"><span data-stu-id="edc3a-182">user.department</span></span> |
    | <span data-ttu-id="edc3a-183">firstname</span><span class="sxs-lookup"><span data-stu-id="edc3a-183">firstname</span></span>| <span data-ttu-id="edc3a-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="edc3a-184">user.givenname</span></span> |
    | <span data-ttu-id="edc3a-185">lastname</span><span class="sxs-lookup"><span data-stu-id="edc3a-185">lastname</span></span>| <span data-ttu-id="edc3a-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="edc3a-186">user.surname</span></span> |
    
    ![Creating an Azure AD test user](./media/linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="edc3a-188">a.</span><span class="sxs-lookup"><span data-stu-id="edc3a-188">a.</span></span> <span data-ttu-id="edc3a-189">Click on **Add Attribute** to open the attribute dialog.</span><span class="sxs-lookup"><span data-stu-id="edc3a-189">Click on **Add Attribute** to open the attribute dialog.</span></span>
    
    ![Creating an Azure AD test user](./media/linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Creating an Azure AD test user](./media/linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="edc3a-192">b.</span><span class="sxs-lookup"><span data-stu-id="edc3a-192">b.</span></span> <span data-ttu-id="edc3a-193">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="edc3a-193">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="edc3a-194">c.</span><span class="sxs-lookup"><span data-stu-id="edc3a-194">c.</span></span> <span data-ttu-id="edc3a-195">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="edc3a-195">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="edc3a-196">d.</span><span class="sxs-lookup"><span data-stu-id="edc3a-196">d.</span></span> <span data-ttu-id="edc3a-197">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="edc3a-197">Click **Ok**</span></span>

1. <span data-ttu-id="edc3a-198">Perform the following steps on the **name** attribute-</span><span class="sxs-lookup"><span data-stu-id="edc3a-198">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="edc3a-199">a.</span><span class="sxs-lookup"><span data-stu-id="edc3a-199">a.</span></span> <span data-ttu-id="edc3a-200">Click on the attribute to open the **Edit Attribute** window.</span><span class="sxs-lookup"><span data-stu-id="edc3a-200">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="edc3a-202">b.</span><span class="sxs-lookup"><span data-stu-id="edc3a-202">b.</span></span> <span data-ttu-id="edc3a-203">Delete the URL value from the **namespace**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-203">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="edc3a-204">c.</span><span class="sxs-lookup"><span data-stu-id="edc3a-204">c.</span></span> <span data-ttu-id="edc3a-205">Click **Ok** to save the setting.</span><span class="sxs-lookup"><span data-stu-id="edc3a-205">Click **Ok** to save the setting.</span></span>

1. <span data-ttu-id="edc3a-206">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="edc3a-206">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

1. <span data-ttu-id="edc3a-208">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="edc3a-208">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="edc3a-210">Go to **LinkedIn Admin Settings** section.</span><span class="sxs-lookup"><span data-stu-id="edc3a-210">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="edc3a-211">Click **Upload XML file** to upload the Metadata XML file that you have downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="edc3a-211">Click **Upload XML file** to upload the Metadata XML file that you have downloaded from the Azure portal.</span></span>

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

1. <span data-ttu-id="edc3a-213">Click **On** to enable SSO.</span><span class="sxs-lookup"><span data-stu-id="edc3a-213">Click **On** to enable SSO.</span></span> <span data-ttu-id="edc3a-214">SSO status changes from **Not Connected** to **Connected**</span><span class="sxs-lookup"><span data-stu-id="edc3a-214">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="edc3a-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="edc3a-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="edc3a-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="edc3a-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="edc3a-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="edc3a-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="edc3a-219">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="edc3a-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="edc3a-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edc3a-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="edc3a-222">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edc3a-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="edc3a-223">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="edc3a-223">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="edc3a-225">Go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-225">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="edc3a-227">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="edc3a-227">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="edc3a-229">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="edc3a-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="edc3a-231">a.</span><span class="sxs-lookup"><span data-stu-id="edc3a-231">a.</span></span> <span data-ttu-id="edc3a-232">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="edc3a-233">b.</span><span class="sxs-lookup"><span data-stu-id="edc3a-233">b.</span></span> <span data-ttu-id="edc3a-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="edc3a-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="edc3a-235">c.</span><span class="sxs-lookup"><span data-stu-id="edc3a-235">c.</span></span> <span data-ttu-id="edc3a-236">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="edc3a-237">d.</span><span class="sxs-lookup"><span data-stu-id="edc3a-237">d.</span></span> <span data-ttu-id="edc3a-238">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="edc3a-239">Creating a LinkedIn Sales Navigator test user</span><span class="sxs-lookup"><span data-stu-id="edc3a-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="edc3a-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="edc3a-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="edc3a-241">Activate **Automatically assign licenses** to assign a license to the user.</span><span class="sxs-lookup"><span data-stu-id="edc3a-241">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Creating an Azure AD test user](./media/linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="edc3a-243">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="edc3a-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="edc3a-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="edc3a-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Sales Navigator.</span></span>

![Assign User][200] 

<span data-ttu-id="edc3a-246">**To assign Britta Simon to LinkedIn Sales Navigator, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edc3a-246">**To assign Britta Simon to LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="edc3a-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="edc3a-249">In the applications list, select **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-249">In the applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Configure Single Sign-On](./media/linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

1. <span data-ttu-id="edc3a-251">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="edc3a-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="edc3a-253">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="edc3a-253">Click **Add** button.</span></span> <span data-ttu-id="edc3a-254">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="edc3a-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="edc3a-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="edc3a-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="edc3a-257">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="edc3a-257">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="edc3a-258">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="edc3a-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="edc3a-259">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="edc3a-259">Testing single sign-on</span></span>

<span data-ttu-id="edc3a-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="edc3a-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="edc3a-261">When you click the LinkedIn Sales Navigator tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span><span class="sxs-lookup"><span data-stu-id="edc3a-261">When you click the LinkedIn Sales Navigator tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="edc3a-262">It links your personal account with your LinkedIn business account.</span><span class="sxs-lookup"><span data-stu-id="edc3a-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="edc3a-263">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="edc3a-263">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="edc3a-264">Additional resources</span><span class="sxs-lookup"><span data-stu-id="edc3a-264">Additional resources</span></span>

* [<span data-ttu-id="edc3a-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="edc3a-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="edc3a-266">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="edc3a-266">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/linkedinsalesnavigator-tutorial/tutorial_general_203.png

