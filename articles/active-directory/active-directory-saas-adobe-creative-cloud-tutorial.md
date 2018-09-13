---
title: 'Tutorial: Azure Active Directory integration with Adobe Creative Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Adobe Creative Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 99dd101d2fdfddc0b6cd03c009661f6902158615
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662766"
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="35f5c-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="35f5c-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="35f5c-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35f5c-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35f5c-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="35f5c-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="35f5c-106">You can control in Azure AD who has access to Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="35f5c-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="35f5c-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="35f5c-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35f5c-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="35f5c-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="35f5c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35f5c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35f5c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="35f5c-110">Prerequisites</span></span>

<span data-ttu-id="35f5c-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="35f5c-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="35f5c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="35f5c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35f5c-113">A Adobe Creative Cloud single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="35f5c-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35f5c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="35f5c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35f5c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="35f5c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35f5c-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="35f5c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="35f5c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35f5c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35f5c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="35f5c-118">Scenario description</span></span>
<span data-ttu-id="35f5c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="35f5c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35f5c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="35f5c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35f5c-121">Adding Adobe Creative Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="35f5c-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="35f5c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="35f5c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="35f5c-123">Adding Adobe Creative Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="35f5c-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="35f5c-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="35f5c-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="35f5c-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="35f5c-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="35f5c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="35f5c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="35f5c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="35f5c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="35f5c-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="35f5c-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="35f5c-133">In the search box, type **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="35f5c-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="35f5c-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35f5c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="35f5c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35f5c-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="35f5c-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35f5c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35f5c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="35f5c-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="35f5c-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="35f5c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="35f5c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="35f5c-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="35f5c-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="35f5c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="35f5c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="35f5c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35f5c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35f5c-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="35f5c-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="35f5c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="35f5c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35f5c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="35f5c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35f5c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="35f5c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35f5c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span><span class="sxs-lookup"><span data-stu-id="35f5c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="35f5c-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="35f5c-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="35f5c-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="35f5c-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="35f5c-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="35f5c-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="35f5c-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="35f5c-157">a.</span><span class="sxs-lookup"><span data-stu-id="35f5c-157">a.</span></span> <span data-ttu-id="35f5c-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="35f5c-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="35f5c-159">b.</span><span class="sxs-lookup"><span data-stu-id="35f5c-159">b.</span></span> <span data-ttu-id="35f5c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="35f5c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35f5c-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="35f5c-161">Please note that these are not the real values.</span></span> <span data-ttu-id="35f5c-162">You have to update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="35f5c-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="35f5c-163">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="35f5c-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="35f5c-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span><span class="sxs-lookup"><span data-stu-id="35f5c-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="35f5c-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="35f5c-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="35f5c-167">a.</span><span class="sxs-lookup"><span data-stu-id="35f5c-167">a.</span></span> <span data-ttu-id="35f5c-168">Click on the **Show advanced URL settings** option</span><span class="sxs-lookup"><span data-stu-id="35f5c-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="35f5c-169">b.</span><span class="sxs-lookup"><span data-stu-id="35f5c-169">b.</span></span> <span data-ttu-id="35f5c-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="35f5c-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="35f5c-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="35f5c-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="35f5c-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="35f5c-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="35f5c-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span><span class="sxs-lookup"><span data-stu-id="35f5c-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="35f5c-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="35f5c-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="35f5c-177">Go to **Identity** on the left navigation pane and click your domain.</span><span class="sxs-lookup"><span data-stu-id="35f5c-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="35f5c-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span><span class="sxs-lookup"><span data-stu-id="35f5c-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="35f5c-179">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="35f5c-179">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="35f5c-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="35f5c-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="35f5c-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="35f5c-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="35f5c-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="35f5c-183">Select **HTTP - Redirect** as **IDP Binding**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="35f5c-184">Select **Email Address** as **User Login Setting**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="35f5c-185">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="35f5c-185">Click **Save** button.</span></span>

15. <span data-ttu-id="35f5c-186">The dashboard will now present the XML **"Download Metadata"** file.</span><span class="sxs-lookup"><span data-stu-id="35f5c-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="35f5c-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span><span class="sxs-lookup"><span data-stu-id="35f5c-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="35f5c-188">Please open the file and configure them in the Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="35f5c-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="35f5c-191">a.</span><span class="sxs-lookup"><span data-stu-id="35f5c-191">a.</span></span> <span data-ttu-id="35f5c-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="35f5c-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="35f5c-193">b.</span><span class="sxs-lookup"><span data-stu-id="35f5c-193">b.</span></span> <span data-ttu-id="35f5c-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="35f5c-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35f5c-195">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="35f5c-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="35f5c-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35f5c-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="35f5c-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="35f5c-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="35f5c-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="35f5c-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="35f5c-201">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="35f5c-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="35f5c-203">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="35f5c-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="35f5c-205">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="35f5c-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35f5c-207">a.</span><span class="sxs-lookup"><span data-stu-id="35f5c-207">a.</span></span> <span data-ttu-id="35f5c-208">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35f5c-209">b.</span><span class="sxs-lookup"><span data-stu-id="35f5c-209">b.</span></span> <span data-ttu-id="35f5c-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="35f5c-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35f5c-211">c.</span><span class="sxs-lookup"><span data-stu-id="35f5c-211">c.</span></span> <span data-ttu-id="35f5c-212">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="35f5c-213">d.</span><span class="sxs-lookup"><span data-stu-id="35f5c-213">d.</span></span> <span data-ttu-id="35f5c-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="35f5c-215">Creating an Adobe Creative Cloud test user</span><span class="sxs-lookup"><span data-stu-id="35f5c-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="35f5c-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="35f5c-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="35f5c-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="35f5c-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="35f5c-218">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="35f5c-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="35f5c-219">Log in to your Adobe Creative Cloud company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="35f5c-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="35f5c-220">Click **People**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-220">Click **People**.</span></span>

    <span data-ttu-id="35f5c-221">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span><span class="sxs-lookup"><span data-stu-id="35f5c-221">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="35f5c-222">Click **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-222">Click **Invite User**.</span></span>

    <span data-ttu-id="35f5c-223">![Invite Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span><span class="sxs-lookup"><span data-stu-id="35f5c-223">![Invite Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="35f5c-224">On the **Invite People** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="35f5c-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="35f5c-225">![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="35f5c-225">![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="35f5c-226">a.</span><span class="sxs-lookup"><span data-stu-id="35f5c-226">a.</span></span> <span data-ttu-id="35f5c-227">In the **Email** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="35f5c-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="35f5c-228">b.</span><span class="sxs-lookup"><span data-stu-id="35f5c-228">b.</span></span> <span data-ttu-id="35f5c-229">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="35f5c-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="35f5c-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="35f5c-231">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="35f5c-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="35f5c-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="35f5c-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![Assign User][200] 

<span data-ttu-id="35f5c-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="35f5c-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="35f5c-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="35f5c-237">In the applications list, select **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="35f5c-239">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="35f5c-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="35f5c-241">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="35f5c-241">Click **Add** button.</span></span> <span data-ttu-id="35f5c-242">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="35f5c-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="35f5c-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="35f5c-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="35f5c-245">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="35f5c-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35f5c-246">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="35f5c-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35f5c-247">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="35f5c-247">Testing single sign-on</span></span>

<span data-ttu-id="35f5c-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="35f5c-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="35f5c-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span><span class="sxs-lookup"><span data-stu-id="35f5c-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="35f5c-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="35f5c-250">Additional resources</span></span>

* [<span data-ttu-id="35f5c-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35f5c-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35f5c-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="35f5c-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png


























