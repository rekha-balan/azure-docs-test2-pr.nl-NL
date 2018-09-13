---
title: 'Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and IBM Kenexa Survey Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 6828617e0ae61a3784e4db3d1c2ecf4ce9862ce2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866329"
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="37845-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="37845-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="37845-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37845-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37845-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="37845-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37845-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="37845-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="37845-107">You can enable your users to automatically sign in to IBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="37845-107">You can enable your users to automatically sign in to IBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="37845-108">You can manage your accounts in one central location: the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="37845-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="37845-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="37845-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37845-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="37845-110">Prerequisites</span></span>

<span data-ttu-id="37845-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="37845-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span></span>

- <span data-ttu-id="37845-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="37845-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37845-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span><span class="sxs-lookup"><span data-stu-id="37845-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37845-114">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span><span class="sxs-lookup"><span data-stu-id="37845-114">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="37845-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="37845-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="37845-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="37845-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37845-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37845-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37845-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="37845-118">Scenario description</span></span>
<span data-ttu-id="37845-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="37845-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="37845-120">The scenario outlined in the tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="37845-120">The scenario outlined in the tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="37845-121">Adding IBM Kenexa Survey Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="37845-121">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
* <span data-ttu-id="37845-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="37845-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a><span data-ttu-id="37845-123">Add IBM Kenexa Survey Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="37845-123">Add IBM Kenexa Survey Enterprise from the gallery</span></span>
<span data-ttu-id="37845-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="37845-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37845-125">To add IBM Kenexa Survey Enterprise from the gallery, do the following:</span><span class="sxs-lookup"><span data-stu-id="37845-125">To add IBM Kenexa Survey Enterprise from the gallery, do the following:</span></span>

1. <span data-ttu-id="37845-126">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="37845-126">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** button.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="37845-128">Select **Enterprise applications**, and then select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="37845-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="37845-130">To add an application, click the **New application** button.</span><span class="sxs-lookup"><span data-stu-id="37845-130">To add an application, click the **New application** button.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="37845-132">In the search box, type **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="37845-132">In the search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Creating an Azure AD test user](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

1. <span data-ttu-id="37845-134">In the results list, select **IBM Kenexa Survey Enterprise**, and then click the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="37845-134">In the results list, select **IBM Kenexa Survey Enterprise**, and then click the **Add** button to add the application.</span></span>

    ![IBM Kenexa Survey Enterprise in the results list](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="37845-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="37845-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="37845-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="37845-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="37845-138">For SSO to work, Azure AD needs to identify the IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37845-138">For SSO to work, Azure AD needs to identify the IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="37845-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="37845-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="37845-140">To establish the link relationship, assign the value of the **user name** in IBM Kenexa Survey Enterprise as the value of the **Username** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37845-140">To establish the link relationship, assign the value of the **user name** in IBM Kenexa Survey Enterprise as the value of the **Username** in Azure AD.</span></span>

<span data-ttu-id="37845-141">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete the building blocks in the next two sections.</span><span class="sxs-lookup"><span data-stu-id="37845-141">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete the building blocks in the next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="37845-142">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="37845-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="37845-143">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing the following:</span><span class="sxs-lookup"><span data-stu-id="37845-143">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing the following:</span></span>

1. <span data-ttu-id="37845-144">In the Azure portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="37845-144">In the Azure portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![IBM Kenexa Survey Enterprise Configure single sign-on link][4]

1. <span data-ttu-id="37845-146">In the **Single sign-on** dialog box, in the **Mode** box, select **SAML-based Sign-on** to enable SSO.</span><span class="sxs-lookup"><span data-stu-id="37845-146">In the **Single sign-on** dialog box, in the **Mode** box, select **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Single sign-on dialog box](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

1. <span data-ttu-id="37845-148">In the **IBM Kenexa Survey Enterprise Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="37845-148">In the **IBM Kenexa Survey Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![IBM Kenexa Survey Enterprise Domain and URLs single sign-on information](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="37845-150">a.</span><span class="sxs-lookup"><span data-stu-id="37845-150">a.</span></span> <span data-ttu-id="37845-151">In the **Identifier** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="37845-151">In the **Identifier** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="37845-152">b.</span><span class="sxs-lookup"><span data-stu-id="37845-152">b.</span></span> <span data-ttu-id="37845-153">In the **Reply URL** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="37845-153">In the **Reply URL** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37845-154">The preceding values are not real.</span><span class="sxs-lookup"><span data-stu-id="37845-154">The preceding values are not real.</span></span> <span data-ttu-id="37845-155">Update them with the actual identifier and reply URL.</span><span class="sxs-lookup"><span data-stu-id="37845-155">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="37845-156">To obtain the actual values, contact the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="37845-156">To obtain the actual values, contact the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

1. <span data-ttu-id="37845-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save the certificate file to your computer.</span><span class="sxs-lookup"><span data-stu-id="37845-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save the certificate file to your computer.</span></span>

    ![The Certificate (Base64) download link](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="37845-159">The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes.</span><span class="sxs-lookup"><span data-stu-id="37845-159">The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes.</span></span> <span data-ttu-id="37845-160">The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system.</span><span class="sxs-lookup"><span data-stu-id="37845-160">The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system.</span></span> <span data-ttu-id="37845-161">To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="37845-161">To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="37845-162">By default, Azure AD sets the user identifier as the user principal name (UPN) value.</span><span class="sxs-lookup"><span data-stu-id="37845-162">By default, Azure AD sets the user identifier as the user principal name (UPN) value.</span></span> <span data-ttu-id="37845-163">You can change this value on the **Attribute** tab, as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="37845-163">You can change this value on the **Attribute** tab, as shown in the following screenshot.</span></span> <span data-ttu-id="37845-164">The integration works only after you've completed the mapping correctly.</span><span class="sxs-lookup"><span data-stu-id="37845-164">The integration works only after you've completed the mapping correctly.</span></span>
    
    ![The User Attributes dialog box](./media/kenexasurvey-tutorial/tutorial_attribute.png) 

1. <span data-ttu-id="37845-166">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="37845-166">Click **Save**.</span></span>

    ![The configure single sign-on Save button](./media/kenexasurvey-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="37845-168">To open the **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="37845-168">To open the **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![The Configure IBM Kenexa Survey Enterprise link](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

1. <span data-ttu-id="37845-170">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from the **Quick Reference** section.</span><span class="sxs-lookup"><span data-stu-id="37845-170">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from the **Quick Reference** section.</span></span>

1. <span data-ttu-id="37845-171">In the **Configure sign-on** window, under **Quick Reference**, copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span><span class="sxs-lookup"><span data-stu-id="37845-171">In the **Configure sign-on** window, under **Quick Reference**, copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

1. <span data-ttu-id="37845-172">To configure SSO on the **IBM Kenexa Survey Enterprise** side, send the downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values to the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="37845-172">To configure SSO on the **IBM Kenexa Survey Enterprise** side, send the downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values to the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="37845-173">You can refer to a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span><span class="sxs-lookup"><span data-stu-id="37845-173">You can refer to a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="37845-174">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply click the **single sign-on** tab, and then access the embedded documentation through the **Configuration** section at the end.</span><span class="sxs-lookup"><span data-stu-id="37845-174">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply click the **single sign-on** tab, and then access the embedded documentation through the **Configuration** section at the end.</span></span> <span data-ttu-id="37845-175">To learn more about the embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="37845-175">To learn more about the embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="37845-176">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="37845-176">Create an Azure AD test user</span></span>
<span data-ttu-id="37845-177">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span><span class="sxs-lookup"><span data-stu-id="37845-177">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Create an Azure AD test user][100]

1. <span data-ttu-id="37845-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="37845-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/kenexasurvey-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="37845-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="37845-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/kenexasurvey-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="37845-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="37845-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![The Add button](./media/kenexasurvey-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="37845-185">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="37845-185">In the **User** dialog box, perform the following steps:</span></span>
 
    ![The User dialog box](./media/kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37845-187">a.</span><span class="sxs-lookup"><span data-stu-id="37845-187">a.</span></span> <span data-ttu-id="37845-188">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37845-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37845-189">b.</span><span class="sxs-lookup"><span data-stu-id="37845-189">b.</span></span> <span data-ttu-id="37845-190">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37845-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="37845-191">c.</span><span class="sxs-lookup"><span data-stu-id="37845-191">c.</span></span> <span data-ttu-id="37845-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="37845-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="37845-193">d.</span><span class="sxs-lookup"><span data-stu-id="37845-193">d.</span></span> <span data-ttu-id="37845-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="37845-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="37845-195">Create an IBM Kenexa Survey Enterprise test user</span><span class="sxs-lookup"><span data-stu-id="37845-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="37845-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="37845-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="37845-197">To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="37845-197">To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="37845-198">This SSO ID value should also be mapped to the user identifier value from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37845-198">This SSO ID value should also be mapped to the user identifier value from Azure AD.</span></span> <span data-ttu-id="37845-199">You can change this default setting on the **Attribute** tab.</span><span class="sxs-lookup"><span data-stu-id="37845-199">You can change this default setting on the **Attribute** tab.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="37845-200">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="37845-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="37845-201">In this section, you enable user Britta Simon to use Azure SSO by granting access to IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="37845-201">In this section, you enable user Britta Simon to use Azure SSO by granting access to IBM Kenexa Survey Enterprise.</span></span>

![Assign the user role][200] 

<span data-ttu-id="37845-203">To assign user Britta Simon to IBM Kenexa Survey Enterprise, do the following:</span><span class="sxs-lookup"><span data-stu-id="37845-203">To assign user Britta Simon to IBM Kenexa Survey Enterprise, do the following:</span></span>

1. <span data-ttu-id="37845-204">In the Azure portal, open the **Applications** view, go to the **Directory** view, select **Enterprise applications**, and then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="37845-204">In the Azure portal, open the **Applications** view, go to the **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![The "Enterprise applications" and "All applications" links][201] 

1. <span data-ttu-id="37845-206">In the **Applications** list, select **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="37845-206">In the **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![The IBM Kenexa Survey Enterprise link in the Applications list](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

1. <span data-ttu-id="37845-208">In the left pane, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="37845-208">In the left pane, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202] 

1. <span data-ttu-id="37845-210">Click the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="37845-210">Click the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="37845-212">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="37845-212">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

1. <span data-ttu-id="37845-213">In the **Users and groups** dialog box, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="37845-213">In the **Users and groups** dialog box, click the **Select** button.</span></span>

1. <span data-ttu-id="37845-214">In the **Add Assignment** dialog box, click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="37845-214">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="37845-215">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="37845-215">Test single sign-on</span></span>

<span data-ttu-id="37845-216">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="37845-216">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="37845-217">When you click the **IBM Kenexa Survey Enterprise** tile in the Access Panel, you should be automatically signed in to your IBM Kenexa Survey Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="37845-217">When you click the **IBM Kenexa Survey Enterprise** tile in the Access Panel, you should be automatically signed in to your IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37845-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="37845-218">Additional resources</span></span>

* [<span data-ttu-id="37845-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37845-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="37845-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37845-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/kenexasurvey-tutorial/tutorial_general_203.png

 
