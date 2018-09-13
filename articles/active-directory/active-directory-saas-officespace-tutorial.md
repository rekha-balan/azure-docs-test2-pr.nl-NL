---
title: 'Tutorial: Azure Active Directory integration with OfficeSpace Software | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and OfficeSpace Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jeedes
ms.openlocfilehash: 1b748eec9d04910d7c33ad4f14b41dcc8efe5a3f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564444"
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="49018-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="49018-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="49018-104">In this tutorial, you learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49018-104">In this tutorial, you learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49018-105">Integrating OfficeSpace Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="49018-105">Integrating OfficeSpace Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="49018-106">You can control in Azure AD who has access to OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="49018-106">You can control in Azure AD who has access to OfficeSpace Software</span></span>
- <span data-ttu-id="49018-107">You can enable your users to automatically get signed-on to OfficeSpace Software (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="49018-107">You can enable your users to automatically get signed-on to OfficeSpace Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49018-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="49018-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="49018-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49018-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49018-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="49018-110">Prerequisites</span></span>

<span data-ttu-id="49018-111">To configure Azure AD integration with OfficeSpace Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="49018-111">To configure Azure AD integration with OfficeSpace Software, you need the following items:</span></span>

- <span data-ttu-id="49018-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="49018-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49018-113">An OfficeSpace Software single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="49018-113">An OfficeSpace Software single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="49018-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="49018-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="49018-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="49018-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49018-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="49018-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="49018-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49018-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="49018-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="49018-118">Scenario description</span></span>
<span data-ttu-id="49018-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="49018-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49018-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="49018-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49018-121">Adding OfficeSpace Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="49018-121">Adding OfficeSpace Software from the gallery</span></span>
2. <span data-ttu-id="49018-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="49018-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-officespace-software-from-the-gallery"></a><span data-ttu-id="49018-123">Adding OfficeSpace Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="49018-123">Adding OfficeSpace Software from the gallery</span></span>
<span data-ttu-id="49018-124">To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="49018-124">To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="49018-125">**To add OfficeSpace Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="49018-125">**To add OfficeSpace Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="49018-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="49018-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="49018-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="49018-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="49018-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="49018-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="49018-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="49018-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="49018-133">In the search box, type **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="49018-133">In the search box, type **OfficeSpace Software**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_001.png)

5. <span data-ttu-id="49018-135">In the results panel, select **OfficeSpace Software**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="49018-135">In the results panel, select **OfficeSpace Software**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="49018-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="49018-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="49018-138">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="49018-138">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="49018-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OfficeSpace Software is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49018-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OfficeSpace Software is to a user in Azure AD.</span></span> <span data-ttu-id="49018-140">In other words, a link relationship between an Azure AD user and the related user in OfficeSpace Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="49018-140">In other words, a link relationship between an Azure AD user and the related user in OfficeSpace Software needs to be established.</span></span>

<span data-ttu-id="49018-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="49018-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in OfficeSpace Software.</span></span>

<span data-ttu-id="49018-142">To configure and test Azure AD single sign-on with OfficeSpace Software, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="49018-142">To configure and test Azure AD single sign-on with OfficeSpace Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="49018-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="49018-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="49018-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49018-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49018-145">**[Creating an OfficeSpace Software test user](#creating-an-officespace-software-test-user)** - to have a counterpart of Britta Simon in OfficeSpace Software that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="49018-145">**[Creating an OfficeSpace Software test user](#creating-an-officespace-software-test-user)** - to have a counterpart of Britta Simon in OfficeSpace Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="49018-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="49018-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49018-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="49018-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="49018-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="49018-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="49018-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your OfficeSpace Software application.</span><span class="sxs-lookup"><span data-stu-id="49018-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="49018-150">**To configure Azure AD single sign-on with OfficeSpace Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="49018-150">**To configure Azure AD single sign-on with OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="49018-151">In the Azure Management portal, on the **OfficeSpace Software** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="49018-151">In the Azure Management portal, on the **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="49018-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="49018-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_01.png)

3. <span data-ttu-id="49018-155">On the **OfficeSpace Software Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="49018-155">On the **OfficeSpace Software Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_02.png)

    <span data-ttu-id="49018-157">a.</span><span class="sxs-lookup"><span data-stu-id="49018-157">a.</span></span> <span data-ttu-id="49018-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="49018-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="49018-159">b.</span><span class="sxs-lookup"><span data-stu-id="49018-159">b.</span></span> <span data-ttu-id="49018-160">In the **Identifier** textbox, type a value using the following pattern: `<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="49018-160">In the **Identifier** textbox, type a value using the following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="49018-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="49018-161">Please note that these are not the real values.</span></span> <span data-ttu-id="49018-162">You have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="49018-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="49018-163">Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="49018-163">Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com) to get these values.</span></span> 

4. <span data-ttu-id="49018-164">OfficeSpace Software application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="49018-164">OfficeSpace Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="49018-165">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="49018-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="49018-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="49018-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="49018-167">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="49018-167">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_03.png)

5. <span data-ttu-id="49018-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="49018-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="49018-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="49018-170">Attribute Name</span></span> | <span data-ttu-id="49018-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="49018-171">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="49018-172">email</span><span class="sxs-lookup"><span data-stu-id="49018-172">email</span></span> | <span data-ttu-id="49018-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="49018-173">user.mail</span></span> |
    | <span data-ttu-id="49018-174">name</span><span class="sxs-lookup"><span data-stu-id="49018-174">name</span></span> | <span data-ttu-id="49018-175">user.displayname</span><span class="sxs-lookup"><span data-stu-id="49018-175">user.displayname</span></span> |
    | <span data-ttu-id="49018-176">first_name</span><span class="sxs-lookup"><span data-stu-id="49018-176">first_name</span></span> | <span data-ttu-id="49018-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="49018-177">user.givenname</span></span> |
    | <span data-ttu-id="49018-178">last_name</span><span class="sxs-lookup"><span data-stu-id="49018-178">last_name</span></span> | <span data-ttu-id="49018-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="49018-179">user.surname</span></span> |

    <span data-ttu-id="49018-180">a.</span><span class="sxs-lookup"><span data-stu-id="49018-180">a.</span></span> <span data-ttu-id="49018-181">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="49018-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_04.png)

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="49018-184">b.</span><span class="sxs-lookup"><span data-stu-id="49018-184">b.</span></span> <span data-ttu-id="49018-185">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="49018-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="49018-186">c.</span><span class="sxs-lookup"><span data-stu-id="49018-186">c.</span></span> <span data-ttu-id="49018-187">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="49018-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="49018-188">d.</span><span class="sxs-lookup"><span data-stu-id="49018-188">d.</span></span> <span data-ttu-id="49018-189">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="49018-189">Click **Ok**</span></span>

6. <span data-ttu-id="49018-190">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="49018-190">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_08.png) 

7. <span data-ttu-id="49018-192">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="49018-192">Click **Save**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="49018-194">On the **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="49018-194">On the **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_09.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_10.png)

9. <span data-ttu-id="49018-197">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="49018-197">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="49018-198">Go to **Settings** and click **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="49018-198">Go to **Settings** and click **Connectors**.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="49018-200">Click **SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="49018-200">Click **SAML Authentication**.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="49018-202">In the **SAML Authentication** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="49018-202">In the **SAML Authentication** section, perform the following steps:</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="49018-204">a.</span><span class="sxs-lookup"><span data-stu-id="49018-204">a.</span></span> <span data-ttu-id="49018-205">In the **Logout provider url** textbox put the value of **Sign-Out URL** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="49018-205">In the **Logout provider url** textbox put the value of **Sign-Out URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="49018-206">b.</span><span class="sxs-lookup"><span data-stu-id="49018-206">b.</span></span> <span data-ttu-id="49018-207">In the **Client idp target url** textbox put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="49018-207">In the **Client idp target url** textbox put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="49018-208">c.</span><span class="sxs-lookup"><span data-stu-id="49018-208">c.</span></span> <span data-ttu-id="49018-209">Copy the **Thumbprint** value from the downloaded certificate, and then paste it into the **Client idp cert fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="49018-209">Copy the **Thumbprint** value from the downloaded certificate, and then paste it into the **Client idp cert fingerprint** textbox.</span></span> 

    <span data-ttu-id="49018-210">d.</span><span class="sxs-lookup"><span data-stu-id="49018-210">d.</span></span> <span data-ttu-id="49018-211">Click **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="49018-211">Click **Save Settings**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="49018-212">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span><span class="sxs-lookup"><span data-stu-id="49018-212">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)</span></span> 
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="49018-213">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="49018-213">Creating an Azure AD test user</span></span>
<span data-ttu-id="49018-214">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49018-214">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="49018-216">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="49018-216">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="49018-217">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="49018-217">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49018-219">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="49018-219">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49018-221">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="49018-221">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49018-223">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="49018-223">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49018-225">a.</span><span class="sxs-lookup"><span data-stu-id="49018-225">a.</span></span> <span data-ttu-id="49018-226">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49018-226">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49018-227">b.</span><span class="sxs-lookup"><span data-stu-id="49018-227">b.</span></span> <span data-ttu-id="49018-228">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="49018-228">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49018-229">c.</span><span class="sxs-lookup"><span data-stu-id="49018-229">c.</span></span> <span data-ttu-id="49018-230">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="49018-230">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="49018-231">d.</span><span class="sxs-lookup"><span data-stu-id="49018-231">d.</span></span> <span data-ttu-id="49018-232">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="49018-232">Click **Create**.</span></span> 



### <a name="creating-an-officespace-software-test-user"></a><span data-ttu-id="49018-233">Creating an OfficeSpace Software test user</span><span class="sxs-lookup"><span data-stu-id="49018-233">Creating an OfficeSpace Software test user</span></span>

<span data-ttu-id="49018-234">The objective of this section is to create a user called Britta Simon in OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="49018-234">The objective of this section is to create a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="49018-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="49018-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="49018-236">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="49018-236">There is no action item for you in this section.</span></span> <span data-ttu-id="49018-237">A new user will be created during an attempt to access OfficeSpace Software if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="49018-237">A new user will be created during an attempt to access OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="49018-238">If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="49018-238">If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="49018-239">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="49018-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="49018-240">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="49018-240">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to OfficeSpace Software.</span></span>

![Assign User][200] 

<span data-ttu-id="49018-242">**To assign Britta Simon to OfficeSpace Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="49018-242">**To assign Britta Simon to OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="49018-243">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="49018-243">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="49018-245">In the applications list, select **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="49018-245">In the applications list, select **OfficeSpace Software**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_officespace_50.png) 

3. <span data-ttu-id="49018-247">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="49018-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="49018-249">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="49018-249">Click **Add** button.</span></span> <span data-ttu-id="49018-250">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="49018-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="49018-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="49018-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="49018-253">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="49018-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49018-254">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="49018-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="49018-255">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="49018-255">Testing single sign-on</span></span>

<span data-ttu-id="49018-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="49018-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="49018-257">When you click the OfficeSpace Software tile in the Access Panel, you should get automatically signed-on to your OfficeSpace Software application.</span><span class="sxs-lookup"><span data-stu-id="49018-257">When you click the OfficeSpace Software tile in the Access Panel, you should get automatically signed-on to your OfficeSpace Software application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="49018-258">Additional resources</span><span class="sxs-lookup"><span data-stu-id="49018-258">Additional resources</span></span>

* [<span data-ttu-id="49018-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49018-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49018-260">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49018-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-officespace-tutorial/tutorial_general_203.png



























