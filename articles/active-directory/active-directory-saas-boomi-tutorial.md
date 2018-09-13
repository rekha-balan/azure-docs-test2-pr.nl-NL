---
title: 'Tutorial: Azure Active Directory integration with Boomi | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Boomi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 4f594d921811180fb3b02560d2cb8f50b90ec114
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553464"
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="71e5d-103">Tutorial: Azure Active Directory integration with Boomi</span><span class="sxs-lookup"><span data-stu-id="71e5d-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="71e5d-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71e5d-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71e5d-105">Integrating Boomi with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="71e5d-105">Integrating Boomi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="71e5d-106">You can control in Azure AD who has access to Boomi</span><span class="sxs-lookup"><span data-stu-id="71e5d-106">You can control in Azure AD who has access to Boomi</span></span>
- <span data-ttu-id="71e5d-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="71e5d-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="71e5d-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="71e5d-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="71e5d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="71e5d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71e5d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="71e5d-110">Prerequisites</span></span>

<span data-ttu-id="71e5d-111">To configure Azure AD integration with Boomi, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="71e5d-111">To configure Azure AD integration with Boomi, you need the following items:</span></span>

- <span data-ttu-id="71e5d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="71e5d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71e5d-113">A Boomi single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="71e5d-113">A Boomi single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="71e5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="71e5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="71e5d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="71e5d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71e5d-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="71e5d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="71e5d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71e5d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="71e5d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="71e5d-118">Scenario description</span></span>
<span data-ttu-id="71e5d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="71e5d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71e5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="71e5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71e5d-121">Adding Boomi from the gallery</span><span class="sxs-lookup"><span data-stu-id="71e5d-121">Adding Boomi from the gallery</span></span>
2. <span data-ttu-id="71e5d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="71e5d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-boomi-from-the-gallery"></a><span data-ttu-id="71e5d-123">Adding Boomi from the gallery</span><span class="sxs-lookup"><span data-stu-id="71e5d-123">Adding Boomi from the gallery</span></span>
<span data-ttu-id="71e5d-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="71e5d-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="71e5d-125">**To add Boomi from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71e5d-125">**To add Boomi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="71e5d-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="71e5d-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="71e5d-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="71e5d-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="71e5d-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="71e5d-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="71e5d-133">In the search box, type **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-133">In the search box, type **Boomi**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_000.png)

5. <span data-ttu-id="71e5d-135">In the results panel, select **Boomi**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="71e5d-135">In the results panel, select **Boomi**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="71e5d-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="71e5d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="71e5d-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="71e5d-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="71e5d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71e5d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span></span> <span data-ttu-id="71e5d-140">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span><span class="sxs-lookup"><span data-stu-id="71e5d-140">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span></span>

<span data-ttu-id="71e5d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Boomi.</span><span class="sxs-lookup"><span data-stu-id="71e5d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Boomi.</span></span>

<span data-ttu-id="71e5d-142">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="71e5d-142">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="71e5d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="71e5d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="71e5d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71e5d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="71e5d-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="71e5d-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="71e5d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="71e5d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="71e5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="71e5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="71e5d-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="71e5d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="71e5d-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Boomi application.</span><span class="sxs-lookup"><span data-stu-id="71e5d-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="71e5d-150">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71e5d-150">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="71e5d-151">In the Azure Management portal, on the **Boomi** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-151">In the Azure Management portal, on the **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="71e5d-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="71e5d-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_01.png)

3. <span data-ttu-id="71e5d-155">On the **Boomi Domain and URLs** section, in the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<account name>/saml`</span><span class="sxs-lookup"><span data-stu-id="71e5d-155">On the **Boomi Domain and URLs** section, in the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<account name>/saml`</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_02.png)

    > [!NOTE] 
    > <span data-ttu-id="71e5d-157">Please note that this is not the real value.</span><span class="sxs-lookup"><span data-stu-id="71e5d-157">Please note that this is not the real value.</span></span> <span data-ttu-id="71e5d-158">You have to update this value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="71e5d-158">You have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="71e5d-159">Contact Boomi support team to get this value.</span><span class="sxs-lookup"><span data-stu-id="71e5d-159">Contact Boomi support team to get this value.</span></span> 

4. <span data-ttu-id="71e5d-160">Boomi application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="71e5d-160">Boomi application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="71e5d-161">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="71e5d-161">Please configure the following claims for this application.</span></span> <span data-ttu-id="71e5d-162">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="71e5d-162">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="71e5d-163">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="71e5d-163">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_03.png)

5. <span data-ttu-id="71e5d-165">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="71e5d-165">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="71e5d-166">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="71e5d-166">Attribute Name</span></span> | <span data-ttu-id="71e5d-167">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="71e5d-167">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="71e5d-168">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="71e5d-168">FEDERATION_ID</span></span> | <span data-ttu-id="71e5d-169">user.mail</span><span class="sxs-lookup"><span data-stu-id="71e5d-169">user.mail</span></span> |

    <span data-ttu-id="71e5d-170">a.</span><span class="sxs-lookup"><span data-stu-id="71e5d-170">a.</span></span> <span data-ttu-id="71e5d-171">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="71e5d-171">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_04.png)

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_05.png)
    
    <span data-ttu-id="71e5d-174">b.</span><span class="sxs-lookup"><span data-stu-id="71e5d-174">b.</span></span> <span data-ttu-id="71e5d-175">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="71e5d-175">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="71e5d-176">c.</span><span class="sxs-lookup"><span data-stu-id="71e5d-176">c.</span></span> <span data-ttu-id="71e5d-177">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="71e5d-177">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="71e5d-178">d.</span><span class="sxs-lookup"><span data-stu-id="71e5d-178">d.</span></span> <span data-ttu-id="71e5d-179">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="71e5d-179">Click **OK**</span></span>

6. <span data-ttu-id="71e5d-180">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-180">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_06.png)    

7. <span data-ttu-id="71e5d-182">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-182">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="71e5d-183">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="71e5d-183">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_300.png)

8. <span data-ttu-id="71e5d-185">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="71e5d-185">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_07.png)

9. <span data-ttu-id="71e5d-187">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-187">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="71e5d-189">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="71e5d-189">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_08.png) 

11. <span data-ttu-id="71e5d-191">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="71e5d-191">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_09.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_10.png)

12. <span data-ttu-id="71e5d-194">In a different web browser window, log into your Boomi company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="71e5d-194">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

13. <span data-ttu-id="71e5d-195">Navigate to **Company Name** and go to **Set up**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-195">Navigate to **Company Name** and go to **Set up**.</span></span>

14. <span data-ttu-id="71e5d-196">Click the **SSO options** tab and perform below steps.</span><span class="sxs-lookup"><span data-stu-id="71e5d-196">Click the **SSO options** tab and perform below steps.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="71e5d-198">a.</span><span class="sxs-lookup"><span data-stu-id="71e5d-198">a.</span></span> <span data-ttu-id="71e5d-199">Check **Enable SAML Single Sign-On** checkbox.</span><span class="sxs-lookup"><span data-stu-id="71e5d-199">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="71e5d-200">b.</span><span class="sxs-lookup"><span data-stu-id="71e5d-200">b.</span></span> <span data-ttu-id="71e5d-201">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-201">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="71e5d-202">c.</span><span class="sxs-lookup"><span data-stu-id="71e5d-202">c.</span></span> <span data-ttu-id="71e5d-203">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="71e5d-203">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="71e5d-204">d.</span><span class="sxs-lookup"><span data-stu-id="71e5d-204">d.</span></span> <span data-ttu-id="71e5d-205">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span><span class="sxs-lookup"><span data-stu-id="71e5d-205">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="71e5d-206">e.</span><span class="sxs-lookup"><span data-stu-id="71e5d-206">e.</span></span> <span data-ttu-id="71e5d-207">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="71e5d-207">Click **Save** button.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="71e5d-208">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="71e5d-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="71e5d-209">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71e5d-209">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="71e5d-211">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71e5d-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="71e5d-212">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="71e5d-212">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="71e5d-214">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="71e5d-214">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="71e5d-216">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="71e5d-216">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="71e5d-218">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="71e5d-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="71e5d-220">a.</span><span class="sxs-lookup"><span data-stu-id="71e5d-220">a.</span></span> <span data-ttu-id="71e5d-221">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71e5d-222">b.</span><span class="sxs-lookup"><span data-stu-id="71e5d-222">b.</span></span> <span data-ttu-id="71e5d-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="71e5d-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="71e5d-224">c.</span><span class="sxs-lookup"><span data-stu-id="71e5d-224">c.</span></span> <span data-ttu-id="71e5d-225">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="71e5d-226">d.</span><span class="sxs-lookup"><span data-stu-id="71e5d-226">d.</span></span> <span data-ttu-id="71e5d-227">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-227">Click **Create**.</span></span> 



### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="71e5d-228">Creating a Boomi test user</span><span class="sxs-lookup"><span data-stu-id="71e5d-228">Creating a Boomi test user</span></span>

<span data-ttu-id="71e5d-229">In order to enable Azure AD users to log into Boomi, they must be provisioned into Boomi.</span><span class="sxs-lookup"><span data-stu-id="71e5d-229">In order to enable Azure AD users to log into Boomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="71e5d-230">In the case of Boomi, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="71e5d-230">In the case of Boomi, provisioning is a manual task.</span></span>

####<a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="71e5d-231">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="71e5d-231">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="71e5d-232">Log into your Boomi company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="71e5d-232">Log into your Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="71e5d-233">After logging in, navigate to **User Management** and go to **Users**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-233">After logging in, navigate to **User Management** and go to **Users**.</span></span>

    <span data-ttu-id="71e5d-234">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span><span class="sxs-lookup"><span data-stu-id="71e5d-234">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="71e5d-235">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span><span class="sxs-lookup"><span data-stu-id="71e5d-235">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="71e5d-236">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span><span class="sxs-lookup"><span data-stu-id="71e5d-236">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="71e5d-237">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span><span class="sxs-lookup"><span data-stu-id="71e5d-237">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

4. <span data-ttu-id="71e5d-238">Enter the user's **User e-mail address**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-238">Enter the user's **User e-mail address**.</span></span>

5. <span data-ttu-id="71e5d-239">Enter the user's **First name** and **Last name**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-239">Enter the user's **First name** and **Last name**.</span></span>

6. <span data-ttu-id="71e5d-240">Enter the user's **Federation ID**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-240">Enter the user's **Federation ID**.</span></span> <span data-ttu-id="71e5d-241">Each user must have a Federation ID that uniquely identifies the user within the account.</span><span class="sxs-lookup"><span data-stu-id="71e5d-241">Each user must have a Federation ID that uniquely identifies the user within the account.</span></span> 

7. <span data-ttu-id="71e5d-242">Assign the **Standard User** role to the user.</span><span class="sxs-lookup"><span data-stu-id="71e5d-242">Assign the **Standard User** role to the user.</span></span> <span data-ttu-id="71e5d-243">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span><span class="sxs-lookup"><span data-stu-id="71e5d-243">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>

8. <span data-ttu-id="71e5d-244">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-244">Click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71e5d-245">The user will not receive a welcome notification email containing a password that can be used to log into the AtomSphere account because his password will be managed through the identity provider.</span><span class="sxs-lookup"><span data-stu-id="71e5d-245">The user will not receive a welcome notification email containing a password that can be used to log into the AtomSphere account because his password will be managed through the identity provider.</span></span> <span data-ttu-id="71e5d-246">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="71e5d-246">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="71e5d-247">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="71e5d-247">Assigning the Azure AD test user</span></span>

<span data-ttu-id="71e5d-248">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Boomi.</span><span class="sxs-lookup"><span data-stu-id="71e5d-248">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Boomi.</span></span>

![Assign User][200] 

<span data-ttu-id="71e5d-250">**To assign Britta Simon to Boomi, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71e5d-250">**To assign Britta Simon to Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="71e5d-251">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-251">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="71e5d-253">In the applications list, select **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-253">In the applications list, select **Boomi**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_50.png) 

3. <span data-ttu-id="71e5d-255">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="71e5d-255">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="71e5d-257">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="71e5d-257">Click **Add** button.</span></span> <span data-ttu-id="71e5d-258">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="71e5d-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="71e5d-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="71e5d-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="71e5d-261">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="71e5d-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="71e5d-262">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="71e5d-262">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="71e5d-263">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="71e5d-263">Testing single sign-on</span></span>

<span data-ttu-id="71e5d-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="71e5d-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="71e5d-265">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span><span class="sxs-lookup"><span data-stu-id="71e5d-265">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="71e5d-266">Additional resources</span><span class="sxs-lookup"><span data-stu-id="71e5d-266">Additional resources</span></span>

* [<span data-ttu-id="71e5d-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71e5d-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71e5d-268">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="71e5d-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_203.png































