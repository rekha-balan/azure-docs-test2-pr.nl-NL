---
title: 'Tutorial: Azure Active Directory integration with Procore SSO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Procore SSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 25f31b40defc3cfe9b80a71b4d7a5ac7caf600f8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550943"
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="13d5d-103">Tutorial: Azure Active Directory integration with Procore SSO</span><span class="sxs-lookup"><span data-stu-id="13d5d-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="13d5d-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="13d5d-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13d5d-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="13d5d-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="13d5d-106">You can control in Azure AD who has access to Procore SSO</span><span class="sxs-lookup"><span data-stu-id="13d5d-106">You can control in Azure AD who has access to Procore SSO</span></span>
- <span data-ttu-id="13d5d-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="13d5d-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="13d5d-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="13d5d-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="13d5d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="13d5d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Procore SSO, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="13d5d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="13d5d-110">Prerequisites</span></span>

<span data-ttu-id="13d5d-111">To configure Azure AD integration with Procore SSO, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="13d5d-111">To configure Azure AD integration with Procore SSO, you need the following items:</span></span>

- <span data-ttu-id="13d5d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="13d5d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="13d5d-113">A Procore SSO single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="13d5d-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="13d5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="13d5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="13d5d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="13d5d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="13d5d-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="13d5d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="13d5d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13d5d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="13d5d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="13d5d-118">Scenario description</span></span>
<span data-ttu-id="13d5d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="13d5d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="13d5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="13d5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="13d5d-121">Adding Procore SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="13d5d-121">Adding Procore SSO from the gallery</span></span>
2. <span data-ttu-id="13d5d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="13d5d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-the-gallery"></a><span data-ttu-id="13d5d-123">Adding Procore SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="13d5d-123">Adding Procore SSO from the gallery</span></span>
<span data-ttu-id="13d5d-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="13d5d-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="13d5d-125">**To add Procore SSO from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="13d5d-125">**To add Procore SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="13d5d-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="13d5d-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="13d5d-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="13d5d-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="13d5d-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="13d5d-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="13d5d-133">In the search box, type **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-133">In the search box, type **Procore SSO**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="13d5d-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="13d5d-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="13d5d-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="13d5d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="13d5d-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="13d5d-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="13d5d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13d5d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span></span> <span data-ttu-id="13d5d-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span><span class="sxs-lookup"><span data-stu-id="13d5d-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span></span>

<span data-ttu-id="13d5d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="13d5d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span></span>

<span data-ttu-id="13d5d-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="13d5d-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="13d5d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="13d5d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="13d5d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13d5d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="13d5d-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="13d5d-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="13d5d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="13d5d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="13d5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="13d5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="13d5d-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="13d5d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="13d5d-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span><span class="sxs-lookup"><span data-stu-id="13d5d-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="13d5d-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="13d5d-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="13d5d-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="13d5d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="13d5d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="13d5d-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="13d5d-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="13d5d-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="13d5d-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="13d5d-159">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="13d5d-159">Click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="13d5d-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="13d5d-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="13d5d-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="13d5d-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="13d5d-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="13d5d-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span></span>

8. <span data-ttu-id="13d5d-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span><span class="sxs-lookup"><span data-stu-id="13d5d-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="13d5d-167">Paste the values in the boxes as described below-</span><span class="sxs-lookup"><span data-stu-id="13d5d-167">Paste the values in the boxes as described below-</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)   

    <span data-ttu-id="13d5d-169">a.</span><span class="sxs-lookup"><span data-stu-id="13d5d-169">a.</span></span> <span data-ttu-id="13d5d-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="13d5d-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span></span>

    <span data-ttu-id="13d5d-171">b.</span><span class="sxs-lookup"><span data-stu-id="13d5d-171">b.</span></span> <span data-ttu-id="13d5d-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="13d5d-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span></span>

    <span data-ttu-id="13d5d-173">c.</span><span class="sxs-lookup"><span data-stu-id="13d5d-173">c.</span></span> <span data-ttu-id="13d5d-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span></span> <span data-ttu-id="13d5d-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="13d5d-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="13d5d-176">Click on **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="13d5d-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span><span class="sxs-lookup"><span data-stu-id="13d5d-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

To ensure users can sign-in to Procore SSO after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Procore SSO in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="13d5d-178">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="13d5d-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="13d5d-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13d5d-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="13d5d-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="13d5d-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="13d5d-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="13d5d-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13d5d-184">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="13d5d-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="13d5d-186">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="13d5d-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13d5d-188">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="13d5d-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13d5d-190">a.</span><span class="sxs-lookup"><span data-stu-id="13d5d-190">a.</span></span> <span data-ttu-id="13d5d-191">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13d5d-192">b.</span><span class="sxs-lookup"><span data-stu-id="13d5d-192">b.</span></span> <span data-ttu-id="13d5d-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="13d5d-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="13d5d-194">c.</span><span class="sxs-lookup"><span data-stu-id="13d5d-194">c.</span></span> <span data-ttu-id="13d5d-195">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="13d5d-196">d.</span><span class="sxs-lookup"><span data-stu-id="13d5d-196">d.</span></span> <span data-ttu-id="13d5d-197">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="13d5d-198">Creating a Procore SSO test user</span><span class="sxs-lookup"><span data-stu-id="13d5d-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="13d5d-199">Please follow the below steps to create a Procore test user on their side.</span><span class="sxs-lookup"><span data-stu-id="13d5d-199">Please follow the below steps to create a Procore test user on their side.</span></span>

1. <span data-ttu-id="13d5d-200">Login to your procore company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="13d5d-200">Login to your procore company site as an administrator.</span></span>  

2. <span data-ttu-id="13d5d-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span><span class="sxs-lookup"><span data-stu-id="13d5d-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/procore_sso_directory.png)

3. <span data-ttu-id="13d5d-203">Click on **Add a Person** option to open the form and enter perform following options -</span><span class="sxs-lookup"><span data-stu-id="13d5d-203">Click on **Add a Person** option to open the form and enter perform following options -</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/procore_user_add.png)

    <span data-ttu-id="13d5d-205">a.</span><span class="sxs-lookup"><span data-stu-id="13d5d-205">a.</span></span> <span data-ttu-id="13d5d-206">In the **First Name** textbox, type user's first name like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-206">In the **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="13d5d-207">b.</span><span class="sxs-lookup"><span data-stu-id="13d5d-207">b.</span></span> <span data-ttu-id="13d5d-208">In the **Last name** textbox, type user's last name like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-208">In the **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="13d5d-209">c.</span><span class="sxs-lookup"><span data-stu-id="13d5d-209">c.</span></span> <span data-ttu-id="13d5d-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="13d5d-211">d.</span><span class="sxs-lookup"><span data-stu-id="13d5d-211">d.</span></span> <span data-ttu-id="13d5d-212">Select **Permission Template** as **Apply Permission Template Later**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="13d5d-213">e.</span><span class="sxs-lookup"><span data-stu-id="13d5d-213">e.</span></span> <span data-ttu-id="13d5d-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-214">Click **Create**.</span></span>

4. <span data-ttu-id="13d5d-215">Check and update the details for the newly added contact.</span><span class="sxs-lookup"><span data-stu-id="13d5d-215">Check and update the details for the newly added contact.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/procore_user_check.png)

5. <span data-ttu-id="13d5d-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span><span class="sxs-lookup"><span data-stu-id="13d5d-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/procore_user_save.png)   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="13d5d-219">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="13d5d-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="13d5d-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="13d5d-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span></span>

![Assign User][200] 

<span data-ttu-id="13d5d-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="13d5d-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="13d5d-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="13d5d-225">In the applications list, select **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-225">In the applications list, select **Procore SSO**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="13d5d-227">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="13d5d-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="13d5d-229">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="13d5d-229">Click **Add** button.</span></span> <span data-ttu-id="13d5d-230">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="13d5d-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="13d5d-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="13d5d-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="13d5d-233">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="13d5d-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="13d5d-234">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="13d5d-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="13d5d-235">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="13d5d-235">Testing single sign-on</span></span>

<span data-ttu-id="13d5d-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="13d5d-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="13d5d-237">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="13d5d-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="13d5d-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="13d5d-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="13d5d-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span><span class="sxs-lookup"><span data-stu-id="13d5d-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="13d5d-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="13d5d-240">Additional resources</span></span>

* [<span data-ttu-id="13d5d-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13d5d-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13d5d-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="13d5d-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png




























