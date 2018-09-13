---
title: 'Tutorial: Azure Active Directory integration with ServiceChannel | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ServiceChannel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 1449dc365d318baff3084385b78b60533ac2c71a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869043"
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="4dd69-103">Tutorial: Azure Active Directory integration with ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="4dd69-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="4dd69-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4dd69-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4dd69-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4dd69-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4dd69-106">You can control in Azure AD who has access to ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="4dd69-106">You can control in Azure AD who has access to ServiceChannel</span></span>
- <span data-ttu-id="4dd69-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4dd69-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4dd69-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="4dd69-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="4dd69-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4dd69-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dd69-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4dd69-110">Prerequisites</span></span>

<span data-ttu-id="4dd69-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4dd69-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span></span>

- <span data-ttu-id="4dd69-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4dd69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4dd69-113">A ServiceChannel single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4dd69-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4dd69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4dd69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4dd69-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4dd69-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4dd69-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="4dd69-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4dd69-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4dd69-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4dd69-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4dd69-118">Scenario description</span></span>
<span data-ttu-id="4dd69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4dd69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4dd69-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4dd69-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4dd69-121">Adding ServiceChannel from the gallery</span><span class="sxs-lookup"><span data-stu-id="4dd69-121">Adding ServiceChannel from the gallery</span></span>
1. <span data-ttu-id="4dd69-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dd69-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-the-gallery"></a><span data-ttu-id="4dd69-123">Adding ServiceChannel from the gallery</span><span class="sxs-lookup"><span data-stu-id="4dd69-123">Adding ServiceChannel from the gallery</span></span>
<span data-ttu-id="4dd69-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4dd69-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4dd69-125">**To add ServiceChannel from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd69-125">**To add ServiceChannel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd69-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4dd69-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4dd69-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4dd69-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="4dd69-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd69-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4dd69-133">In the search box, type **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-133">In the search box, type **ServiceChannel**.</span></span>

    ![Creating an Azure AD test user](./media/servicechannel-tutorial/tutorial-servicechannel_000.png)

1. <span data-ttu-id="4dd69-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4dd69-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4dd69-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dd69-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4dd69-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4dd69-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4dd69-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4dd69-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span></span> <span data-ttu-id="4dd69-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4dd69-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span></span>

<span data-ttu-id="4dd69-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="4dd69-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span></span>

<span data-ttu-id="4dd69-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4dd69-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4dd69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4dd69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4dd69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dd69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4dd69-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dd69-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4dd69-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4dd69-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4dd69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4dd69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4dd69-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dd69-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4dd69-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span><span class="sxs-lookup"><span data-stu-id="4dd69-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="4dd69-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd69-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd69-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4dd69-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="4dd69-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](./media/servicechannel-tutorial/tutorial-servicechannel_01.png)

1. <span data-ttu-id="4dd69-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dd69-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="4dd69-157">a.</span><span class="sxs-lookup"><span data-stu-id="4dd69-157">a.</span></span> <span data-ttu-id="4dd69-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="4dd69-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="4dd69-159">b.</span><span class="sxs-lookup"><span data-stu-id="4dd69-159">b.</span></span> <span data-ttu-id="4dd69-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="4dd69-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4dd69-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="4dd69-161">Please note that these are not the real values.</span></span> <span data-ttu-id="4dd69-162">You have to update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="4dd69-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="4dd69-163">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="4dd69-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="4dd69-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span><span class="sxs-lookup"><span data-stu-id="4dd69-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span></span>

1. <span data-ttu-id="4dd69-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="4dd69-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="4dd69-166">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="4dd69-166">The following screenshot shows an example for this.</span></span> <span data-ttu-id="4dd69-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span></span> <span data-ttu-id="4dd69-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span><span class="sxs-lookup"><span data-stu-id="4dd69-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span></span> <span data-ttu-id="4dd69-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span><span class="sxs-lookup"><span data-stu-id="4dd69-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span></span>  

    <span data-ttu-id="4dd69-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span><span class="sxs-lookup"><span data-stu-id="4dd69-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Configure Single Sign-On](./media/servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="4dd69-172">See [Manage access using RBAC and the Azure portal](../../role-based-access-control/role-assignments-portal.md) to learn how to configure **Role** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4dd69-172">See [Manage access using RBAC and the Azure portal](../../role-based-access-control/role-assignments-portal.md) to learn how to configure **Role** in Azure AD.</span></span>

1. <span data-ttu-id="4dd69-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span><span class="sxs-lookup"><span data-stu-id="4dd69-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span>

    | <span data-ttu-id="4dd69-174">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="4dd69-174">Attribute Name</span></span> | <span data-ttu-id="4dd69-175">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="4dd69-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="4dd69-176">Role</span><span class="sxs-lookup"><span data-stu-id="4dd69-176">Role</span></span>| <span data-ttu-id="4dd69-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="4dd69-177">user.assignedroles</span></span> |

    <span data-ttu-id="4dd69-178">a.</span><span class="sxs-lookup"><span data-stu-id="4dd69-178">a.</span></span> <span data-ttu-id="4dd69-179">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd69-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Configure Single Sign-On](./media/servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="4dd69-182">b.</span><span class="sxs-lookup"><span data-stu-id="4dd69-182">b.</span></span> <span data-ttu-id="4dd69-183">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="4dd69-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="4dd69-184">c.</span><span class="sxs-lookup"><span data-stu-id="4dd69-184">c.</span></span> <span data-ttu-id="4dd69-185">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="4dd69-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4dd69-186">d.</span><span class="sxs-lookup"><span data-stu-id="4dd69-186">d.</span></span> <span data-ttu-id="4dd69-187">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="4dd69-187">Click **Ok**</span></span>
    
1. <span data-ttu-id="4dd69-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4dd69-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/servicechannel-tutorial/tutorial-servicechannel_05.png) 

1. <span data-ttu-id="4dd69-190">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-190">Click **Save**.</span></span>

    ![Configure Single Sign-On](./media/servicechannel-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4dd69-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4dd69-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4dd69-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span><span class="sxs-lookup"><span data-stu-id="4dd69-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span></span>

1. <span data-ttu-id="4dd69-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="4dd69-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="4dd69-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="4dd69-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4dd69-196">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4dd69-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="4dd69-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dd69-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4dd69-199">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd69-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd69-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4dd69-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/servicechannel-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="4dd69-202">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="4dd69-202">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](./media/servicechannel-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4dd69-204">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd69-204">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/servicechannel-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4dd69-206">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dd69-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4dd69-208">a.</span><span class="sxs-lookup"><span data-stu-id="4dd69-208">a.</span></span> <span data-ttu-id="4dd69-209">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4dd69-210">b.</span><span class="sxs-lookup"><span data-stu-id="4dd69-210">b.</span></span> <span data-ttu-id="4dd69-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4dd69-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4dd69-212">c.</span><span class="sxs-lookup"><span data-stu-id="4dd69-212">c.</span></span> <span data-ttu-id="4dd69-213">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4dd69-214">d.</span><span class="sxs-lookup"><span data-stu-id="4dd69-214">d.</span></span> <span data-ttu-id="4dd69-215">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="4dd69-216">Creating a ServiceChannel test user</span><span class="sxs-lookup"><span data-stu-id="4dd69-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="4dd69-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="4dd69-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="4dd69-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="4dd69-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4dd69-219">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4dd69-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4dd69-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="4dd69-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span></span>

![Assign User][200] 

<span data-ttu-id="4dd69-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd69-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd69-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4dd69-225">In the applications list, select **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-225">In the applications list, select **ServiceChannel**.</span></span>

    ![Configure Single Sign-On](./media/servicechannel-tutorial/tutorial-servicechannel_app01.png) 

1. <span data-ttu-id="4dd69-227">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4dd69-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4dd69-229">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4dd69-229">Click **Add** button.</span></span> <span data-ttu-id="4dd69-230">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd69-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4dd69-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4dd69-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4dd69-233">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd69-233">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4dd69-234">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd69-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4dd69-235">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dd69-235">Testing single sign-on</span></span>

<span data-ttu-id="4dd69-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4dd69-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4dd69-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span><span class="sxs-lookup"><span data-stu-id="4dd69-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4dd69-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4dd69-238">Additional resources</span></span>

* [<span data-ttu-id="4dd69-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4dd69-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4dd69-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4dd69-240">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/servicechannel-tutorial/tutorial_general_203.png