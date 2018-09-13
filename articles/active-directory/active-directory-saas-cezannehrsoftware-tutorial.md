---
title: 'Tutorial: Azure Active Directory integration with Cezanne HR Software | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cezanne HR Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: ec979de3823c25e42a64da27bcbb8a25e4e68d40
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554299"
---
# <a name="tutorial-azure-active-directory-integration-with-cezanne-hr-software"></a><span data-ttu-id="ecd27-103">Tutorial: Azure Active Directory integration with Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="ecd27-103">Tutorial: Azure Active Directory integration with Cezanne HR Software</span></span>

<span data-ttu-id="ecd27-104">In this tutorial, you learn how to integrate Cezanne HR Software with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ecd27-104">In this tutorial, you learn how to integrate Cezanne HR Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ecd27-105">Integrating Cezanne HR Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ecd27-105">Integrating Cezanne HR Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ecd27-106">You can control in Azure AD who has access to Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="ecd27-106">You can control in Azure AD who has access to Cezanne HR Software</span></span>
- <span data-ttu-id="ecd27-107">You can enable your users to automatically get signed-on to Cezanne HR Software single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ecd27-107">You can enable your users to automatically get signed-on to Cezanne HR Software single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="ecd27-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="ecd27-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="ecd27-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ecd27-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecd27-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ecd27-110">Prerequisites</span></span>

<span data-ttu-id="ecd27-111">To configure Azure AD integration with Cezanne HR Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ecd27-111">To configure Azure AD integration with Cezanne HR Software, you need the following items:</span></span>

- <span data-ttu-id="ecd27-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ecd27-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ecd27-113">A Cezanne HR Software SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ecd27-113">A Cezanne HR Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="ecd27-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ecd27-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>
>

<span data-ttu-id="ecd27-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ecd27-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ecd27-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="ecd27-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ecd27-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ecd27-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="ecd27-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ecd27-118">Scenario description</span></span>
<span data-ttu-id="ecd27-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ecd27-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ecd27-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ecd27-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ecd27-121">Adding Cezanne HR Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="ecd27-121">Adding Cezanne HR Software from the gallery</span></span>
2. <span data-ttu-id="ecd27-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ecd27-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-cezanne-hr-software-from-the-gallery"></a><span data-ttu-id="ecd27-123">Add Cezanne HR Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="ecd27-123">Add Cezanne HR Software from the gallery</span></span>
<span data-ttu-id="ecd27-124">To configure the integration of Cezanne HR Software into Azure AD, you need to add Cezanne HR Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ecd27-124">To configure the integration of Cezanne HR Software into Azure AD, you need to add Cezanne HR Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ecd27-125">**To add Cezanne HR Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ecd27-125">**To add Cezanne HR Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ecd27-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ecd27-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ecd27-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ecd27-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ecd27-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ecd27-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ecd27-133">In the search box, type **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-133">In the search box, type **Cezanne HR Software**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_00001.png)

5. <span data-ttu-id="ecd27-135">In the results panel, select **Cezanne HR Software**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ecd27-135">In the results panel, select **Cezanne HR Software**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ecd27-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ecd27-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ecd27-138">In this section, you configure and test Azure AD SSO with Cezanne HR Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ecd27-138">In this section, you configure and test Azure AD SSO with Cezanne HR Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ecd27-139">For SSO to work, Azure AD needs to know what the counterpart user in Cezanne HR Software is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecd27-139">For SSO to work, Azure AD needs to know what the counterpart user in Cezanne HR Software is to a user in Azure AD.</span></span> <span data-ttu-id="ecd27-140">In other words, a link relationship between an Azure AD user and the related user in Cezanne HR Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ecd27-140">In other words, a link relationship between an Azure AD user and the related user in Cezanne HR Software needs to be established.</span></span>

<span data-ttu-id="ecd27-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="ecd27-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Cezanne HR Software.</span></span>

<span data-ttu-id="ecd27-142">To configure and test Azure AD SSO with Cezanne HR Software, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ecd27-142">To configure and test Azure AD SSO with Cezanne HR Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ecd27-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ecd27-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ecd27-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ecd27-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ecd27-145">**[Creating a Cezanne HR Software test user](#creating-a-cezanne-hr-software-test-user)** - to have a counterpart of Britta Simon in Cezanne HR Software that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="ecd27-145">**[Creating a Cezanne HR Software test user](#creating-a-cezanne-hr-software-test-user)** - to have a counterpart of Britta Simon in Cezanne HR Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ecd27-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ecd27-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ecd27-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ecd27-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ecd27-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ecd27-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ecd27-149">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your Cezanne HR Software application.</span><span class="sxs-lookup"><span data-stu-id="ecd27-149">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your Cezanne HR Software application.</span></span>

<span data-ttu-id="ecd27-150">**To configure Azure AD SSO with Cezanne HR Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ecd27-150">**To configure Azure AD SSO with Cezanne HR Software, perform the following steps:**</span></span>

1. <span data-ttu-id="ecd27-151">In the Azure Management portal, on the **Cezanne HR Software** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-151">In the Azure Management portal, on the **Cezanne HR Software** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="ecd27-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="ecd27-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_01.png)

3. <span data-ttu-id="ecd27-155">On the **Cezanne HR Software Domain and URLs** section perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ecd27-155">On the **Cezanne HR Software Domain and URLs** section perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_02.png)
  1. <span data-ttu-id="ecd27-157">In the **Sign On URL** textbox, type a URL using the following pattern: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="ecd27-157">In the **Sign On URL** textbox, type a URL using the following pattern: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>
  2. <span data-ttu-id="ecd27-158">In the **Identifer** textbox, type: `https://w3.cezanneondemand.com/CezanneOnDemand/`</span><span class="sxs-lookup"><span data-stu-id="ecd27-158">In the **Identifer** textbox, type: `https://w3.cezanneondemand.com/CezanneOnDemand/`</span></span>

     >[!NOTE] 
     > <span data-ttu-id="ecd27-159">These are not the real values.</span><span class="sxs-lookup"><span data-stu-id="ecd27-159">These are not the real values.</span></span> <span data-ttu-id="ecd27-160">You have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="ecd27-160">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="ecd27-161">Here we suggest you to use the unique value of URL in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="ecd27-161">Here we suggest you to use the unique value of URL in the Identifier.</span></span> <span data-ttu-id="ecd27-162">Contact [Cezanne HR Software support team](mailto:info@cezannehr.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="ecd27-162">Contact [Cezanne HR Software support team](mailto:info@cezannehr.com) to get these values.</span></span>

4. <span data-ttu-id="ecd27-163">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-163">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_03.png)    

5. <span data-ttu-id="ecd27-165">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-165">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="ecd27-166">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ecd27-166">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="ecd27-168">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ecd27-168">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_04.png)

7. <span data-ttu-id="ecd27-170">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-170">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ecd27-172">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ecd27-172">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_05.png) 

9. <span data-ttu-id="ecd27-174">On the **Cezanne HR Software Configuration** section, click **Configure Cezanne HR Software** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="ecd27-174">On the **Cezanne HR Software Configuration** section, click **Configure Cezanne HR Software** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_06.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_07.png)

10. <span data-ttu-id="ecd27-177">In a different web browser window, sign-on to your Cezanne HR Software tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ecd27-177">In a different web browser window, sign-on to your Cezanne HR Software tenant as an administrator.</span></span>

11. <span data-ttu-id="ecd27-178">On the left navigation pane, click **System Setup**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-178">On the left navigation pane, click **System Setup**.</span></span> <span data-ttu-id="ecd27-179">Go to **Security Settings**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-179">Go to **Security Settings**.</span></span> <span data-ttu-id="ecd27-180">Then navigate to **Single Sign-On Configuration**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-180">Then navigate to **Single Sign-On Configuration**.</span></span>

    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

12. <span data-ttu-id="ecd27-182">In the **Allow users to log in using the following Single Sign-On (SSO) Service** panel, check the **SAML 2.0** box and select the **Advanced Configuration** option.</span><span class="sxs-lookup"><span data-stu-id="ecd27-182">In the **Allow users to log in using the following Single Sign-On (SSO) Service** panel, check the **SAML 2.0** box and select the **Advanced Configuration** option.</span></span>

    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

13. <span data-ttu-id="ecd27-184">Click **Add New** button.</span><span class="sxs-lookup"><span data-stu-id="ecd27-184">Click **Add New** button.</span></span>

    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

14. <span data-ttu-id="ecd27-186">Perform the following steps on **SAML 2.0 IDENTITY PROVIDERS** section.</span><span class="sxs-lookup"><span data-stu-id="ecd27-186">Perform the following steps on **SAML 2.0 IDENTITY PROVIDERS** section.</span></span>

    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
 1. <span data-ttu-id="ecd27-188">Enter the name of your Identity Provider as the **Display Name**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-188">Enter the name of your Identity Provider as the **Display Name**.</span></span>
 2. <span data-ttu-id="ecd27-189">In the **Entity Identifier** textbox put the value of **SAML Entity ID** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="ecd27-189">In the **Entity Identifier** textbox put the value of **SAML Entity ID** from Azure AD application configuration window.</span></span>
 3. <span data-ttu-id="ecd27-190">Change the **SAML Binding** to 'POST'.</span><span class="sxs-lookup"><span data-stu-id="ecd27-190">Change the **SAML Binding** to 'POST'.</span></span>
 4. <span data-ttu-id="ecd27-191">In the **Security Token Service Endpoint** textbox put the value of **SAML Single Sign-on Service URL** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="ecd27-191">In the **Security Token Service Endpoint** textbox put the value of **SAML Single Sign-on Service URL** from Azure AD application configuration window.</span></span>
 5. <span data-ttu-id="ecd27-192">In the **User ID Attribute Name** textbox enter 'http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name'.</span><span class="sxs-lookup"><span data-stu-id="ecd27-192">In the **User ID Attribute Name** textbox enter 'http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name'.</span></span>
 6. <span data-ttu-id="ecd27-193">Click **Upload** icon to upload the downloaded certificate from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecd27-193">Click **Upload** icon to upload the downloaded certificate from Azure AD.</span></span>
 7. <span data-ttu-id="ecd27-194">Click the **Ok** button.</span><span class="sxs-lookup"><span data-stu-id="ecd27-194">Click the **Ok** button.</span></span> 

15. <span data-ttu-id="ecd27-195">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ecd27-195">Click **Save** button.</span></span>

    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ecd27-197">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ecd27-197">Create an Azure AD test user</span></span>
<span data-ttu-id="ecd27-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ecd27-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="ecd27-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ecd27-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ecd27-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ecd27-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ecd27-203">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="ecd27-203">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ecd27-205">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="ecd27-205">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ecd27-207">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ecd27-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 
 1. <span data-ttu-id="ecd27-209">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-209">In the **Name** textbox, type **BrittaSimon**.</span></span>
 2. <span data-ttu-id="ecd27-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ecd27-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
 3. <span data-ttu-id="ecd27-211">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-211">Select **Show Password** and write down the value of the **Password**.</span></span>
 4. <span data-ttu-id="ecd27-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-212">Click **Create**.</span></span> 

### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="ecd27-213">Create a Cezanne HR Software test user</span><span class="sxs-lookup"><span data-stu-id="ecd27-213">Create a Cezanne HR Software test user</span></span>

<span data-ttu-id="ecd27-214">In order to enable Azure AD users to log into Cezanne HR Software, they must be provisioned into Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="ecd27-214">In order to enable Azure AD users to log into Cezanne HR Software, they must be provisioned into Cezanne HR Software.</span></span> <span data-ttu-id="ecd27-215">In the case of Cezanne HR Software, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="ecd27-215">In the case of Cezanne HR Software, provisioning is a manual task.</span></span>

<span data-ttu-id="ecd27-216">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ecd27-216">**To provision a user account, perform the following steps:**</span></span>

1.  <span data-ttu-id="ecd27-217">Log into your Cezanne HR Software company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ecd27-217">Log into your Cezanne HR Software company site as an administrator.</span></span>

2.  <span data-ttu-id="ecd27-218">On the left navigation pane, click **System Setup**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-218">On the left navigation pane, click **System Setup**.</span></span> <span data-ttu-id="ecd27-219">Go to **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-219">Go to **Manage Users**.</span></span> <span data-ttu-id="ecd27-220">Then navigate to **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-220">Then navigate to **Add New User**.</span></span>

    <span data-ttu-id="ecd27-221">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span><span class="sxs-lookup"><span data-stu-id="ecd27-221">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="ecd27-222">On **Person Details** section, perform below steps:</span><span class="sxs-lookup"><span data-stu-id="ecd27-222">On **Person Details** section, perform below steps:</span></span>

    <span data-ttu-id="ecd27-223">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span><span class="sxs-lookup"><span data-stu-id="ecd27-223">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
 1. <span data-ttu-id="ecd27-224">Set **Internal User** as OFF.</span><span class="sxs-lookup"><span data-stu-id="ecd27-224">Set **Internal User** as OFF.</span></span>
 2. <span data-ttu-id="ecd27-225">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-225">In the **First Name** textbox, type **Britta**.</span></span>  
 3. <span data-ttu-id="ecd27-226">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-226">In the **Last Name** textbox, type **Simon**.</span></span>
 4. <span data-ttu-id="ecd27-227">In the **E-mail** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="ecd27-227">In the **E-mail** textbox, type the email address of Britta Simon account.</span></span>

4.  <span data-ttu-id="ecd27-228">On **Account Information** section, perform below steps:</span><span class="sxs-lookup"><span data-stu-id="ecd27-228">On **Account Information** section, perform below steps:</span></span>

    <span data-ttu-id="ecd27-229">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span><span class="sxs-lookup"><span data-stu-id="ecd27-229">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
 1. <span data-ttu-id="ecd27-230">In the **Username** textbox, type the email address of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ecd27-230">In the **Username** textbox, type the email address of Britta Simon.</span></span>
 2. <span data-ttu-id="ecd27-231">In the **Password** textbox, type the password of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="ecd27-231">In the **Password** textbox, type the password of Britta Simon account.</span></span>
 3. <span data-ttu-id="ecd27-232">Select **HR Professional** as **Security Role**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-232">Select **HR Professional** as **Security Role**.</span></span>
 4. <span data-ttu-id="ecd27-233">click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-233">click **OK**.</span></span>

5. <span data-ttu-id="ecd27-234">Navigate to **Single Sign-On** tab and select **Add New** in the **SAML 2.0 Identifiers** area.</span><span class="sxs-lookup"><span data-stu-id="ecd27-234">Navigate to **Single Sign-On** tab and select **Add New** in the **SAML 2.0 Identifiers** area.</span></span>

    <span data-ttu-id="ecd27-235">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span><span class="sxs-lookup"><span data-stu-id="ecd27-235">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="ecd27-236">Choose your Identity Provider for the **Identity Provider** and in the text box of **User Identifier**, enter the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="ecd27-236">Choose your Identity Provider for the **Identity Provider** and in the text box of **User Identifier**, enter the email address of Britta Simon account.</span></span>

    <span data-ttu-id="ecd27-237">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span><span class="sxs-lookup"><span data-stu-id="ecd27-237">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="ecd27-238">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ecd27-238">Click **Save** button.</span></span>

    <span data-ttu-id="ecd27-239">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span><span class="sxs-lookup"><span data-stu-id="ecd27-239">![User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ecd27-240">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ecd27-240">Assign the Azure AD test user</span></span>

<span data-ttu-id="ecd27-241">In this section, you enable Britta Simon to use Azure SSO by granting her access to Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="ecd27-241">In this section, you enable Britta Simon to use Azure SSO by granting her access to Cezanne HR Software.</span></span>

![Assign User][200] 

<span data-ttu-id="ecd27-243">**To assign Britta Simon to Cezanne HR Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ecd27-243">**To assign Britta Simon to Cezanne HR Software, perform the following steps:**</span></span>

1. <span data-ttu-id="ecd27-244">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-244">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="ecd27-246">In the applications list, select **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-246">In the applications list, select **Cezanne HR Software**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_50.png) 

3. <span data-ttu-id="ecd27-248">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ecd27-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="ecd27-250">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ecd27-250">Click **Add** button.</span></span> <span data-ttu-id="ecd27-251">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ecd27-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="ecd27-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ecd27-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ecd27-254">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ecd27-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ecd27-255">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ecd27-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="ecd27-256">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ecd27-256">Test single sign-on</span></span>

<span data-ttu-id="ecd27-257">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ecd27-257">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ecd27-258">When you click the Cezanne HR Software tile in the Access Panel, you should get automatically signed-on to your Cezanne HR Software application.</span><span class="sxs-lookup"><span data-stu-id="ecd27-258">When you click the Cezanne HR Software tile in the Access Panel, you should get automatically signed-on to your Cezanne HR Software application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ecd27-259">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ecd27-259">Additional resources</span></span>

* [<span data-ttu-id="ecd27-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecd27-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ecd27-261">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ecd27-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png



































