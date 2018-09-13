---
title: 'Tutorial: Azure Active Directory integration with LinkedIn Learning | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LinkedIn Learning.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 4683970df351dfc08f8a372f4c55479fd1af5675
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555956"
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="39ac2-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="39ac2-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="39ac2-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39ac2-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39ac2-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="39ac2-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="39ac2-106">You can control in Azure AD who has access to LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="39ac2-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="39ac2-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="39ac2-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="39ac2-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="39ac2-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="39ac2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39ac2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39ac2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="39ac2-110">Prerequisites</span></span>

<span data-ttu-id="39ac2-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="39ac2-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="39ac2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="39ac2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39ac2-113">A LinkedIn Learning single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="39ac2-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39ac2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="39ac2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39ac2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="39ac2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39ac2-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="39ac2-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="39ac2-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39ac2-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39ac2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="39ac2-118">Scenario description</span></span>
<span data-ttu-id="39ac2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="39ac2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39ac2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="39ac2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39ac2-121">Adding LinkedIn Learning from the gallery</span><span class="sxs-lookup"><span data-stu-id="39ac2-121">Adding LinkedIn Learning from the gallery</span></span>
2. <span data-ttu-id="39ac2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="39ac2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="39ac2-123">Adding LinkedIn Learning from the gallery</span><span class="sxs-lookup"><span data-stu-id="39ac2-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="39ac2-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="39ac2-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="39ac2-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39ac2-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="39ac2-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="39ac2-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="39ac2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="39ac2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="39ac2-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="39ac2-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="39ac2-133">In the search box, type **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="39ac2-134">From results panel, click **LinkedIn Learning** to add the application.</span><span class="sxs-lookup"><span data-stu-id="39ac2-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="39ac2-136">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="39ac2-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="39ac2-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="39ac2-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="39ac2-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39ac2-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="39ac2-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span><span class="sxs-lookup"><span data-stu-id="39ac2-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="39ac2-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="39ac2-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="39ac2-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="39ac2-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="39ac2-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="39ac2-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="39ac2-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39ac2-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39ac2-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39ac2-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="39ac2-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="39ac2-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39ac2-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="39ac2-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="39ac2-147">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="39ac2-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="39ac2-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Learning application.</span><span class="sxs-lookup"><span data-stu-id="39ac2-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="39ac2-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39ac2-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="39ac2-150">In the Azure Management portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-150">In the Azure Management portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="39ac2-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="39ac2-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="39ac2-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="39ac2-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="39ac2-155">In **Account Center**, click **Global Settings** under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="39ac2-156">Also, select **Learning - Default** from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="39ac2-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="39ac2-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span><span class="sxs-lookup"><span data-stu-id="39ac2-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="39ac2-160">On Azure Portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span><span class="sxs-lookup"><span data-stu-id="39ac2-160">On Azure Portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="39ac2-162">a.</span><span class="sxs-lookup"><span data-stu-id="39ac2-162">a.</span></span> <span data-ttu-id="39ac2-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="39ac2-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="39ac2-164">b.</span><span class="sxs-lookup"><span data-stu-id="39ac2-164">b.</span></span> <span data-ttu-id="39ac2-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="39ac2-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="39ac2-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span><span class="sxs-lookup"><span data-stu-id="39ac2-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="39ac2-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="39ac2-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="39ac2-169">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="39ac2-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="39ac2-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span><span class="sxs-lookup"><span data-stu-id="39ac2-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="39ac2-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span><span class="sxs-lookup"><span data-stu-id="39ac2-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="39ac2-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span><span class="sxs-lookup"><span data-stu-id="39ac2-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="39ac2-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span></span>

    | <span data-ttu-id="39ac2-175">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="39ac2-175">Attribute Name</span></span> | <span data-ttu-id="39ac2-176">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="39ac2-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="39ac2-177">department</span><span class="sxs-lookup"><span data-stu-id="39ac2-177">department</span></span>| <span data-ttu-id="39ac2-178">user.department</span><span class="sxs-lookup"><span data-stu-id="39ac2-178">user.department</span></span> |

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)

    <span data-ttu-id="39ac2-180">a.</span><span class="sxs-lookup"><span data-stu-id="39ac2-180">a.</span></span> <span data-ttu-id="39ac2-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span><span class="sxs-lookup"><span data-stu-id="39ac2-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/adduserattribute.png)
   
    <span data-ttu-id="39ac2-183">b.</span><span class="sxs-lookup"><span data-stu-id="39ac2-183">b.</span></span> <span data-ttu-id="39ac2-184">Click on **Ok** to save the attribute.</span><span class="sxs-lookup"><span data-stu-id="39ac2-184">Click on **Ok** to save the attribute.</span></span>

10. <span data-ttu-id="39ac2-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="39ac2-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

11. <span data-ttu-id="39ac2-187">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-187">Click **Save**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="39ac2-189">Go to **LinkedIn Admin Settings** section.</span><span class="sxs-lookup"><span data-stu-id="39ac2-189">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="39ac2-190">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span><span class="sxs-lookup"><span data-stu-id="39ac2-190">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="39ac2-192">Click **On** to enable SSO.</span><span class="sxs-lookup"><span data-stu-id="39ac2-192">Click **On** to enable SSO.</span></span> <span data-ttu-id="39ac2-193">SSO status will change from **Not Connected** to **Connected**</span><span class="sxs-lookup"><span data-stu-id="39ac2-193">SSO status will change from **Not Connected** to **Connected**</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="39ac2-195">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="39ac2-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="39ac2-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39ac2-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="39ac2-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39ac2-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="39ac2-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="39ac2-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="39ac2-201">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="39ac2-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="39ac2-203">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="39ac2-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="39ac2-205">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="39ac2-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="39ac2-207">a.</span><span class="sxs-lookup"><span data-stu-id="39ac2-207">a.</span></span> <span data-ttu-id="39ac2-208">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39ac2-209">b.</span><span class="sxs-lookup"><span data-stu-id="39ac2-209">b.</span></span> <span data-ttu-id="39ac2-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="39ac2-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="39ac2-211">c.</span><span class="sxs-lookup"><span data-stu-id="39ac2-211">c.</span></span> <span data-ttu-id="39ac2-212">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="39ac2-213">d.</span><span class="sxs-lookup"><span data-stu-id="39ac2-213">d.</span></span> <span data-ttu-id="39ac2-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-214">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="39ac2-215">Creating a LinkedIn Learning test user</span><span class="sxs-lookup"><span data-stu-id="39ac2-215">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="39ac2-216">Linked Learning Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="39ac2-216">Linked Learning Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="39ac2-217">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span><span class="sxs-lookup"><span data-stu-id="39ac2-217">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/linkedinuserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="39ac2-219">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="39ac2-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="39ac2-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="39ac2-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Learning.</span></span>

![Assign User][200] 

<span data-ttu-id="39ac2-222">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39ac2-222">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="39ac2-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="39ac2-225">In the applications list, select **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-225">In the applications list, select **LinkedIn Learning**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="39ac2-227">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="39ac2-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="39ac2-229">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="39ac2-229">Click **Add** button.</span></span> <span data-ttu-id="39ac2-230">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="39ac2-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="39ac2-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="39ac2-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="39ac2-233">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="39ac2-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39ac2-234">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="39ac2-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="39ac2-235">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="39ac2-235">Testing single sign-on</span></span>

<span data-ttu-id="39ac2-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="39ac2-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="39ac2-237">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span><span class="sxs-lookup"><span data-stu-id="39ac2-237">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39ac2-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="39ac2-238">Additional resources</span></span>

* [<span data-ttu-id="39ac2-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39ac2-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39ac2-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39ac2-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png


























