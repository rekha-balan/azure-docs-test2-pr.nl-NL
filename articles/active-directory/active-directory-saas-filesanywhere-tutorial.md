---
title: 'Tutorial: Azure Active Directory integration with FilesAnywhere | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and FilesAnywhere.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: a0af0b70e011d3d4cc28b03527058d6b0beb5588
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551984"
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="3e34f-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="3e34f-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="3e34f-104">In this tutorial, you learn how to integrate FilesAnywhere with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e34f-104">In this tutorial, you learn how to integrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e34f-105">Integrating FilesAnywhere with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3e34f-105">Integrating FilesAnywhere with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3e34f-106">You can control in Azure AD who has access to FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="3e34f-106">You can control in Azure AD who has access to FilesAnywhere</span></span>
- <span data-ttu-id="3e34f-107">You can enable your users to automatically get signed-on to FilesAnywhere (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="3e34f-107">You can enable your users to automatically get signed-on to FilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e34f-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="3e34f-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="3e34f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e34f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e34f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3e34f-110">Prerequisites</span></span>

<span data-ttu-id="3e34f-111">To configure Azure AD integration with FilesAnywhere, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3e34f-111">To configure Azure AD integration with FilesAnywhere, you need the following items:</span></span>

- <span data-ttu-id="3e34f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3e34f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e34f-113">A FilesAnywhere single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3e34f-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="3e34f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3e34f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="3e34f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3e34f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e34f-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="3e34f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3e34f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e34f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3e34f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3e34f-118">Scenario description</span></span>
<span data-ttu-id="3e34f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3e34f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e34f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3e34f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e34f-121">Adding FilesAnywhere from the gallery</span><span class="sxs-lookup"><span data-stu-id="3e34f-121">Adding FilesAnywhere from the gallery</span></span>
2. <span data-ttu-id="3e34f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3e34f-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-the-gallery"></a><span data-ttu-id="3e34f-123">Adding FilesAnywhere from the gallery</span><span class="sxs-lookup"><span data-stu-id="3e34f-123">Adding FilesAnywhere from the gallery</span></span>
<span data-ttu-id="3e34f-124">To configure the integration of FilesAnywhere into Azure AD, you need to add FilesAnywhere from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3e34f-124">To configure the integration of FilesAnywhere into Azure AD, you need to add FilesAnywhere from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3e34f-125">**To add FilesAnywhere from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3e34f-125">**To add FilesAnywhere from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e34f-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3e34f-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e34f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3e34f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3e34f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3e34f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3e34f-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="3e34f-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3e34f-133">In the search box, type **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="3e34f-133">In the search box, type **FilesAnywhere**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_filesanywhere_search.png)

5. <span data-ttu-id="3e34f-135">In the results panel, select **FilesAnywhere**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3e34f-135">In the results panel, select **FilesAnywhere**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_filesanywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e34f-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3e34f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e34f-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3e34f-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e34f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FilesAnywhere is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e34f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FilesAnywhere is to a user in Azure AD.</span></span> <span data-ttu-id="3e34f-140">In other words, a link relationship between an Azure AD user and the related user in FilesAnywhere needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3e34f-140">In other words, a link relationship between an Azure AD user and the related user in FilesAnywhere needs to be established.</span></span>

<span data-ttu-id="3e34f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3e34f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="3e34f-142">To configure and test Azure AD single sign-on with FilesAnywhere, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3e34f-142">To configure and test Azure AD single sign-on with FilesAnywhere, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e34f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3e34f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e34f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e34f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e34f-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - to have a counterpart of Britta Simon in FilesAnywhere that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="3e34f-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - to have a counterpart of Britta Simon in FilesAnywhere that is linked to the Azure AD representation of her.</span></span>
3. <span data-ttu-id="3e34f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e34f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="3e34f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3e34f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e34f-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3e34f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e34f-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FilesAnywhere application.</span><span class="sxs-lookup"><span data-stu-id="3e34f-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="3e34f-150">**To configure Azure AD single sign-on with FilesAnywhere, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3e34f-150">**To configure Azure AD single sign-on with FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="3e34f-151">In the Azure Management portal, on the **FilesAnywhere** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3e34f-151">In the Azure Management portal, on the **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="3e34f-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="3e34f-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_filesanywhere_samlbase.png)

3. <span data-ttu-id="3e34f-155">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span><span class="sxs-lookup"><span data-stu-id="3e34f-155">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="3e34f-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e34f-157">a.</span></span> <span data-ttu-id="3e34f-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="3e34f-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>

4. <span data-ttu-id="3e34f-159">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3e34f-159">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="3e34f-161">a.</span><span class="sxs-lookup"><span data-stu-id="3e34f-161">a.</span></span> <span data-ttu-id="3e34f-162">Click on the **Show advanced URL settings** option</span><span class="sxs-lookup"><span data-stu-id="3e34f-162">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="3e34f-163">b.</span><span class="sxs-lookup"><span data-stu-id="3e34f-163">b.</span></span> <span data-ttu-id="3e34f-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="3e34f-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e34f-165">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="3e34f-165">Please note that these are not the real values.</span></span> <span data-ttu-id="3e34f-166">You have to update these values with the actual Sign On URL and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="3e34f-166">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="3e34f-167">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="3e34f-167">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) to get these values.</span></span> 

5. <span data-ttu-id="3e34f-168">FilesAnywhere Software application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="3e34f-168">FilesAnywhere Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3e34f-169">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="3e34f-169">Please configure the following claims for this application.</span></span> <span data-ttu-id="3e34f-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="3e34f-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="3e34f-171">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="3e34f-171">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="3e34f-173">When the users signs up with FilesAnywhere they get the value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="3e34f-173">When the users signs up with FilesAnywhere they get the value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="3e34f-174">You have to add the "Client Id" attribute with the unique value provided by FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3e34f-174">You have to add the "Client Id" attribute with the unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="3e34f-175">All these attributes shown above are required.</span><span class="sxs-lookup"><span data-stu-id="3e34f-175">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="3e34f-176">Please note that the value **2331** of **clientid** is just an example.</span><span class="sxs-lookup"><span data-stu-id="3e34f-176">Please note that the value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="3e34f-177">You need to provide the actual value.</span><span class="sxs-lookup"><span data-stu-id="3e34f-177">You need to provide the actual value.</span></span>


6. <span data-ttu-id="3e34f-178">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3e34f-178">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="3e34f-179">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="3e34f-179">Attribute Name</span></span> | <span data-ttu-id="3e34f-180">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="3e34f-180">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="3e34f-181">clientid</span><span class="sxs-lookup"><span data-stu-id="3e34f-181">clientid</span></span> | <span data-ttu-id="3e34f-182">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="3e34f-182">*"uniquevalue"*</span></span> |

    <span data-ttu-id="3e34f-183">a.</span><span class="sxs-lookup"><span data-stu-id="3e34f-183">a.</span></span> <span data-ttu-id="3e34f-184">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="3e34f-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="3e34f-187">b.</span><span class="sxs-lookup"><span data-stu-id="3e34f-187">b.</span></span> <span data-ttu-id="3e34f-188">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="3e34f-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="3e34f-189">c.</span><span class="sxs-lookup"><span data-stu-id="3e34f-189">c.</span></span> <span data-ttu-id="3e34f-190">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="3e34f-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="3e34f-191">d.</span><span class="sxs-lookup"><span data-stu-id="3e34f-191">d.</span></span> <span data-ttu-id="3e34f-192">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="3e34f-192">Click **Ok**</span></span>

7. <span data-ttu-id="3e34f-193">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3e34f-193">Click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3e34f-195">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3e34f-195">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_filesanywhere_certificate.png) 

9. <span data-ttu-id="3e34f-197">On the **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3e34f-197">On the **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_filesanywhere_configure.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_filesanywhere_configuresignon.png)

10. <span data-ttu-id="3e34f-200">To get SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them the downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span><span class="sxs-lookup"><span data-stu-id="3e34f-200">To get SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them the downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e34f-201">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3e34f-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e34f-202">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e34f-202">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="3e34f-204">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3e34f-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e34f-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3e34f-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e34f-207">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="3e34f-207">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e34f-209">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="3e34f-209">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e34f-211">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3e34f-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e34f-213">a.</span><span class="sxs-lookup"><span data-stu-id="3e34f-213">a.</span></span> <span data-ttu-id="3e34f-214">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e34f-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e34f-215">b.</span><span class="sxs-lookup"><span data-stu-id="3e34f-215">b.</span></span> <span data-ttu-id="3e34f-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e34f-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e34f-217">c.</span><span class="sxs-lookup"><span data-stu-id="3e34f-217">c.</span></span> <span data-ttu-id="3e34f-218">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="3e34f-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3e34f-219">d.</span><span class="sxs-lookup"><span data-stu-id="3e34f-219">d.</span></span> <span data-ttu-id="3e34f-220">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3e34f-220">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="3e34f-221">Creating a FilesAnywhere test user</span><span class="sxs-lookup"><span data-stu-id="3e34f-221">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="3e34f-222">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="3e34f-222">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3e34f-223">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3e34f-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3e34f-224">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3e34f-224">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FilesAnywhere.</span></span>

![Assign User][200] 

<span data-ttu-id="3e34f-226">**To assign Britta Simon to FilesAnywhere, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3e34f-226">**To assign Britta Simon to FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="3e34f-227">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3e34f-227">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="3e34f-229">In the applications list, select **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="3e34f-229">In the applications list, select **FilesAnywhere**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_filesanywhere_app.png) 

3. <span data-ttu-id="3e34f-231">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3e34f-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="3e34f-233">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3e34f-233">Click **Add** button.</span></span> <span data-ttu-id="3e34f-234">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3e34f-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="3e34f-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3e34f-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3e34f-237">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3e34f-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e34f-238">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3e34f-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="3e34f-239">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="3e34f-239">Testing single sign-on</span></span>

<span data-ttu-id="3e34f-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3e34f-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3e34f-241">When you click the FilesAnywhere tile in the Access Panel, you should get automatically signed-on to your FilesAnywhere application.</span><span class="sxs-lookup"><span data-stu-id="3e34f-241">When you click the FilesAnywhere tile in the Access Panel, you should get automatically signed-on to your FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3e34f-242">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3e34f-242">Additional resources</span></span>

* [<span data-ttu-id="3e34f-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e34f-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e34f-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3e34f-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filesanywhere-tutorial/tutorial_general_203.png


























