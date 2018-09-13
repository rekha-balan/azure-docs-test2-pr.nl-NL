---
title: 'Tutorial: Azure Active Directory integration with iLMS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and iLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 0e67e97a68ca333dff366dd5e0222c96a1022557
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870502"
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="f1732-103">Tutorial: Azure Active Directory integration with iLMS</span><span class="sxs-lookup"><span data-stu-id="f1732-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="f1732-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1732-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1732-105">Integrating iLMS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f1732-105">Integrating iLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f1732-106">You can control in Azure AD who has access to iLMS</span><span class="sxs-lookup"><span data-stu-id="f1732-106">You can control in Azure AD who has access to iLMS</span></span>
- <span data-ttu-id="f1732-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f1732-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1732-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f1732-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f1732-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f1732-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1732-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f1732-110">Prerequisites</span></span>

<span data-ttu-id="f1732-111">To configure Azure AD integration with iLMS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f1732-111">To configure Azure AD integration with iLMS, you need the following items:</span></span>

- <span data-ttu-id="f1732-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f1732-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1732-113">An iLMS single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f1732-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1732-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f1732-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1732-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f1732-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1732-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="f1732-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f1732-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1732-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1732-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f1732-118">Scenario description</span></span>
<span data-ttu-id="f1732-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f1732-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1732-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f1732-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1732-121">Adding iLMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="f1732-121">Adding iLMS from the gallery</span></span>
1. <span data-ttu-id="f1732-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f1732-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-the-gallery"></a><span data-ttu-id="f1732-123">Adding iLMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="f1732-123">Adding iLMS from the gallery</span></span>
<span data-ttu-id="f1732-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f1732-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f1732-125">**To add iLMS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f1732-125">**To add iLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f1732-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f1732-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="f1732-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f1732-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f1732-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f1732-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="f1732-131">To add new application, click **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f1732-131">To add new application, click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="f1732-133">In the search box, type **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="f1732-133">In the search box, type **iLMS**.</span></span>

    ![Creating an Azure AD test user](./media/ilms-tutorial/tutorial_ilms_search.png)

1. <span data-ttu-id="f1732-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f1732-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1732-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f1732-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1732-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f1732-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1732-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1732-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span></span> <span data-ttu-id="f1732-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f1732-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span></span>

<span data-ttu-id="f1732-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span><span class="sxs-lookup"><span data-stu-id="f1732-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span></span>

<span data-ttu-id="f1732-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f1732-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f1732-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f1732-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f1732-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1732-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f1732-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="f1732-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span></span>
1. <span data-ttu-id="f1732-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1732-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f1732-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f1732-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1732-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f1732-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1732-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span><span class="sxs-lookup"><span data-stu-id="f1732-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="f1732-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f1732-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="f1732-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f1732-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="f1732-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1732-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_ilms_samlbase.png)

1. <span data-ttu-id="f1732-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f1732-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="f1732-157">a.</span><span class="sxs-lookup"><span data-stu-id="f1732-157">a.</span></span> <span data-ttu-id="f1732-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span><span class="sxs-lookup"><span data-stu-id="f1732-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="f1732-159">b.</span><span class="sxs-lookup"><span data-stu-id="f1732-159">b.</span></span> <span data-ttu-id="f1732-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="f1732-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="f1732-161">This '123456' is an example value of identifier.</span><span class="sxs-lookup"><span data-stu-id="f1732-161">This '123456' is an example value of identifier.</span></span>

1. <span data-ttu-id="f1732-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f1732-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="f1732-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="f1732-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

1. <span data-ttu-id="f1732-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="f1732-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="f1732-166">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="f1732-166">Configure the following claims for this application.</span></span> <span data-ttu-id="f1732-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="f1732-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="f1732-168">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="f1732-168">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/ilms-tutorial/4.png)
    
    <span data-ttu-id="f1732-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span><span class="sxs-lookup"><span data-stu-id="f1732-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span></span> <span data-ttu-id="f1732-171">All these attributes shown above are required.</span><span class="sxs-lookup"><span data-stu-id="f1732-171">All these attributes shown above are required.</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="f1732-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span><span class="sxs-lookup"><span data-stu-id="f1732-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span></span> <span data-ttu-id="f1732-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="f1732-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span></span>

1. <span data-ttu-id="f1732-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f1732-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="f1732-175">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="f1732-175">Attribute Name</span></span> | <span data-ttu-id="f1732-176">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="f1732-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="f1732-177">division</span><span class="sxs-lookup"><span data-stu-id="f1732-177">division</span></span> | <span data-ttu-id="f1732-178">user.department</span><span class="sxs-lookup"><span data-stu-id="f1732-178">user.department</span></span> |
    | <span data-ttu-id="f1732-179">region</span><span class="sxs-lookup"><span data-stu-id="f1732-179">region</span></span> | <span data-ttu-id="f1732-180">user.state</span><span class="sxs-lookup"><span data-stu-id="f1732-180">user.state</span></span> |
    | <span data-ttu-id="f1732-181">department</span><span class="sxs-lookup"><span data-stu-id="f1732-181">department</span></span> | <span data-ttu-id="f1732-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="f1732-182">user.jobtitle</span></span> |

    <span data-ttu-id="f1732-183">a.</span><span class="sxs-lookup"><span data-stu-id="f1732-183">a.</span></span> <span data-ttu-id="f1732-184">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="f1732-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_ilms_04.png)

    ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="f1732-187">b.</span><span class="sxs-lookup"><span data-stu-id="f1732-187">b.</span></span> <span data-ttu-id="f1732-188">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="f1732-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f1732-189">c.</span><span class="sxs-lookup"><span data-stu-id="f1732-189">c.</span></span> <span data-ttu-id="f1732-190">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="f1732-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f1732-191">d.</span><span class="sxs-lookup"><span data-stu-id="f1732-191">d.</span></span> <span data-ttu-id="f1732-192">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="f1732-192">Click **Ok**</span></span>

1. <span data-ttu-id="f1732-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f1732-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_ilms_certificate.png) 

1. <span data-ttu-id="f1732-195">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f1732-195">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f1732-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f1732-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span></span>

1. <span data-ttu-id="f1732-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f1732-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span></span>
    
    ![Configure Single Sign-On](./media/ilms-tutorial/1.png) 

    <span data-ttu-id="f1732-200">a.</span><span class="sxs-lookup"><span data-stu-id="f1732-200">a.</span></span> <span data-ttu-id="f1732-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span><span class="sxs-lookup"><span data-stu-id="f1732-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Configure Single Sign-On](./media/ilms-tutorial/2.png) 

    <span data-ttu-id="f1732-203">b.</span><span class="sxs-lookup"><span data-stu-id="f1732-203">b.</span></span> <span data-ttu-id="f1732-204">Under **Identity Provider** section, click **Import Metadata**.</span><span class="sxs-lookup"><span data-stu-id="f1732-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="f1732-205">c.</span><span class="sxs-lookup"><span data-stu-id="f1732-205">c.</span></span> <span data-ttu-id="f1732-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="f1732-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="f1732-208">d.</span><span class="sxs-lookup"><span data-stu-id="f1732-208">d.</span></span> <span data-ttu-id="f1732-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span><span class="sxs-lookup"><span data-stu-id="f1732-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="f1732-210">Check **Create Un-recognized User Account**.</span><span class="sxs-lookup"><span data-stu-id="f1732-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="f1732-211">Map the attributes in Azure AD with the attributes in iLMS.</span><span class="sxs-lookup"><span data-stu-id="f1732-211">Map the attributes in Azure AD with the attributes in iLMS.</span></span> <span data-ttu-id="f1732-212">In the attribute column, specify the attributes name or the default value.</span><span class="sxs-lookup"><span data-stu-id="f1732-212">In the attribute column, specify the attributes name or the default value.</span></span>

    <span data-ttu-id="f1732-213">e.</span><span class="sxs-lookup"><span data-stu-id="f1732-213">e.</span></span> <span data-ttu-id="f1732-214">Go to **Business Rules** tab and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f1732-214">Go to **Business Rules** tab and perform the following steps:</span></span> 
        
       ![Configure Single Sign-On](./media/ilms-tutorial/5.png)

       - <span data-ttu-id="f1732-215">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1732-215">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="f1732-216">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1732-216">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="f1732-217">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span><span class="sxs-lookup"><span data-stu-id="f1732-217">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span></span>
        
       - <span data-ttu-id="f1732-218">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span><span class="sxs-lookup"><span data-stu-id="f1732-218">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span></span>

1. <span data-ttu-id="f1732-219">Click **Save** button to save the settings.</span><span class="sxs-lookup"><span data-stu-id="f1732-219">Click **Save** button to save the settings.</span></span>

    ![Configure Single Sign-On](./media/ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="f1732-221">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f1732-221">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f1732-222">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f1732-222">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f1732-223">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1732-223">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1732-224">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f1732-224">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1732-225">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1732-225">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="f1732-227">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f1732-227">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f1732-228">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f1732-228">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/ilms-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="f1732-230">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="f1732-230">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](./media/ilms-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="f1732-232">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="f1732-232">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/ilms-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="f1732-234">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f1732-234">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1732-236">a.</span><span class="sxs-lookup"><span data-stu-id="f1732-236">a.</span></span> <span data-ttu-id="f1732-237">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1732-237">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1732-238">b.</span><span class="sxs-lookup"><span data-stu-id="f1732-238">b.</span></span> <span data-ttu-id="f1732-239">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1732-239">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1732-240">c.</span><span class="sxs-lookup"><span data-stu-id="f1732-240">c.</span></span> <span data-ttu-id="f1732-241">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f1732-241">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f1732-242">d.</span><span class="sxs-lookup"><span data-stu-id="f1732-242">d.</span></span> <span data-ttu-id="f1732-243">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f1732-243">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="f1732-244">Creating an iLMS test user</span><span class="sxs-lookup"><span data-stu-id="f1732-244">Creating an iLMS test user</span></span>

<span data-ttu-id="f1732-245">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="f1732-245">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="f1732-246">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span><span class="sxs-lookup"><span data-stu-id="f1732-246">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="f1732-247">If you need to create an user manually, then follow below steps :</span><span class="sxs-lookup"><span data-stu-id="f1732-247">If you need to create an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="f1732-248">Log in to your iLMS company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f1732-248">Log in to your iLMS company site as an administrator.</span></span>

1. <span data-ttu-id="f1732-249">Click **“Register User”** under **Users** tab to open **Register User** page.</span><span class="sxs-lookup"><span data-stu-id="f1732-249">Click **“Register User”** under **Users** tab to open **Register User** page.</span></span> 
   
   ![Add Employee](./media/ilms-tutorial/3.png)

1. <span data-ttu-id="f1732-251">On the **“Register User”** page, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="f1732-251">On the **“Register User”** page, perform the following steps.</span></span>

    ![Add Employee](./media/ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="f1732-253">a.</span><span class="sxs-lookup"><span data-stu-id="f1732-253">a.</span></span> <span data-ttu-id="f1732-254">In the **First Name** textbox, type the first name Britta.</span><span class="sxs-lookup"><span data-stu-id="f1732-254">In the **First Name** textbox, type the first name Britta.</span></span>
   
    <span data-ttu-id="f1732-255">b.</span><span class="sxs-lookup"><span data-stu-id="f1732-255">b.</span></span> <span data-ttu-id="f1732-256">In the **Last Name** textbox, type the last name Simon.</span><span class="sxs-lookup"><span data-stu-id="f1732-256">In the **Last Name** textbox, type the last name Simon.</span></span>

    <span data-ttu-id="f1732-257">c.</span><span class="sxs-lookup"><span data-stu-id="f1732-257">c.</span></span> <span data-ttu-id="f1732-258">In the **Email ID** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="f1732-258">In the **Email ID** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="f1732-259">d.</span><span class="sxs-lookup"><span data-stu-id="f1732-259">d.</span></span> <span data-ttu-id="f1732-260">In the **Region** dropdown, select the value for region.</span><span class="sxs-lookup"><span data-stu-id="f1732-260">In the **Region** dropdown, select the value for region.</span></span>

    <span data-ttu-id="f1732-261">e.</span><span class="sxs-lookup"><span data-stu-id="f1732-261">e.</span></span> <span data-ttu-id="f1732-262">In the **Division** dropdown, select the value for division.</span><span class="sxs-lookup"><span data-stu-id="f1732-262">In the **Division** dropdown, select the value for division.</span></span>

    <span data-ttu-id="f1732-263">f.</span><span class="sxs-lookup"><span data-stu-id="f1732-263">f.</span></span> <span data-ttu-id="f1732-264">In the **Department** dropdown, select the value for department.</span><span class="sxs-lookup"><span data-stu-id="f1732-264">In the **Department** dropdown, select the value for department.</span></span>

    <span data-ttu-id="f1732-265">g.</span><span class="sxs-lookup"><span data-stu-id="f1732-265">g.</span></span> <span data-ttu-id="f1732-266">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f1732-266">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1732-267">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span><span class="sxs-lookup"><span data-stu-id="f1732-267">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f1732-268">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f1732-268">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f1732-269">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span><span class="sxs-lookup"><span data-stu-id="f1732-269">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span></span>

![Assign User][200] 

<span data-ttu-id="f1732-271">**To assign Britta Simon to iLMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f1732-271">**To assign Britta Simon to iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="f1732-272">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f1732-272">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f1732-274">In the applications list, select **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="f1732-274">In the applications list, select **iLMS**.</span></span>

    ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_ilms_app.png) 

1. <span data-ttu-id="f1732-276">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f1732-276">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="f1732-278">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f1732-278">Click **Add** button.</span></span> <span data-ttu-id="f1732-279">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f1732-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="f1732-281">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f1732-281">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f1732-282">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f1732-282">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f1732-283">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f1732-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1732-284">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f1732-284">Testing single sign-on</span></span>

<span data-ttu-id="f1732-285">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f1732-285">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f1732-286">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span><span class="sxs-lookup"><span data-stu-id="f1732-286">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1732-287">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f1732-287">Additional resources</span></span>

* [<span data-ttu-id="f1732-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1732-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f1732-289">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1732-289">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/ilms-tutorial/tutorial_general_01.png
[2]: ./media/ilms-tutorial/tutorial_general_02.png
[3]: ./media/ilms-tutorial/tutorial_general_03.png
[4]: ./media/ilms-tutorial/tutorial_general_04.png

[100]: ./media/ilms-tutorial/tutorial_general_100.png

[200]: ./media/ilms-tutorial/tutorial_general_200.png
[201]: ./media/ilms-tutorial/tutorial_general_201.png
[202]: ./media/ilms-tutorial/tutorial_general_202.png
[203]: ./media/ilms-tutorial/tutorial_general_203.png

