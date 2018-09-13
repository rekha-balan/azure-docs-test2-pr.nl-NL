---
title: 'Tutorial: Azure Active Directory integration with Palo Alto Networks - GlobalProtect | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Palo Alto Networks - GlobalProtect.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 03bef6f2-3ea2-4eaa-a828-79c5f1346ce5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2017
ms.author: jeedes
ms.openlocfilehash: d3fdf52d07faa4242a0267ebc929946bbc95418a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868461"
---
# <a name="tutorial-azure-active-directory-integration-with-palo-alto-networks---globalprotect"></a><span data-ttu-id="98f17-103">Tutorial: Azure Active Directory integration with Palo Alto Networks - GlobalProtect</span><span class="sxs-lookup"><span data-stu-id="98f17-103">Tutorial: Azure Active Directory integration with Palo Alto Networks - GlobalProtect</span></span>

<span data-ttu-id="98f17-104">In this tutorial, you learn how to integrate Palo Alto Networks - GlobalProtect with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="98f17-104">In this tutorial, you learn how to integrate Palo Alto Networks - GlobalProtect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98f17-105">Integrating Palo Alto Networks - GlobalProtect with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="98f17-105">Integrating Palo Alto Networks - GlobalProtect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="98f17-106">You can control in Azure AD who has access to Palo Alto Networks - GlobalProtect.</span><span class="sxs-lookup"><span data-stu-id="98f17-106">You can control in Azure AD who has access to Palo Alto Networks - GlobalProtect.</span></span>
- <span data-ttu-id="98f17-107">You can enable your users to automatically get signed-on to Palo Alto Networks - GlobalProtect (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="98f17-107">You can enable your users to automatically get signed-on to Palo Alto Networks - GlobalProtect (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="98f17-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="98f17-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="98f17-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="98f17-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98f17-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="98f17-110">Prerequisites</span></span>

<span data-ttu-id="98f17-111">To configure Azure AD integration with Palo Alto Networks - GlobalProtect, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="98f17-111">To configure Azure AD integration with Palo Alto Networks - GlobalProtect, you need the following items:</span></span>

- <span data-ttu-id="98f17-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="98f17-112">An Azure AD subscription</span></span>
- <span data-ttu-id="98f17-113">A Palo Alto Networks - GlobalProtect single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="98f17-113">A Palo Alto Networks - GlobalProtect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="98f17-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="98f17-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="98f17-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="98f17-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="98f17-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="98f17-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="98f17-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98f17-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98f17-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="98f17-118">Scenario description</span></span>
<span data-ttu-id="98f17-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="98f17-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="98f17-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="98f17-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="98f17-121">Adding Palo Alto Networks - GlobalProtect from the gallery</span><span class="sxs-lookup"><span data-stu-id="98f17-121">Adding Palo Alto Networks - GlobalProtect from the gallery</span></span>
1. <span data-ttu-id="98f17-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="98f17-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-palo-alto-networks---globalprotect-from-the-gallery"></a><span data-ttu-id="98f17-123">Adding Palo Alto Networks - GlobalProtect from the gallery</span><span class="sxs-lookup"><span data-stu-id="98f17-123">Adding Palo Alto Networks - GlobalProtect from the gallery</span></span>
<span data-ttu-id="98f17-124">To configure the integration of Palo Alto Networks - GlobalProtect into Azure AD, you need to add Palo Alto Networks - GlobalProtect from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="98f17-124">To configure the integration of Palo Alto Networks - GlobalProtect into Azure AD, you need to add Palo Alto Networks - GlobalProtect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="98f17-125">**To add Palo Alto Networks - GlobalProtect from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="98f17-125">**To add Palo Alto Networks - GlobalProtect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="98f17-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="98f17-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="98f17-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="98f17-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="98f17-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="98f17-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="98f17-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="98f17-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="98f17-133">In the search box, type **Palo Alto Networks - GlobalProtect**, select **Palo Alto Networks - GlobalProtect** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="98f17-133">In the search box, type **Palo Alto Networks - GlobalProtect**, select **Palo Alto Networks - GlobalProtect** from result panel then click **Add** button to add the application.</span></span>

    ![Palo Alto Networks - GlobalProtect in the results list](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoglobal_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="98f17-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="98f17-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="98f17-136">In this section, you configure and test Azure AD single sign-on with Palo Alto Networks - GlobalProtect based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="98f17-136">In this section, you configure and test Azure AD single sign-on with Palo Alto Networks - GlobalProtect based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="98f17-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Palo Alto Networks - GlobalProtect is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98f17-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Palo Alto Networks - GlobalProtect is to a user in Azure AD.</span></span> <span data-ttu-id="98f17-138">In other words, a link relationship between an Azure AD user and the related user in Palo Alto Networks - GlobalProtect needs to be established.</span><span class="sxs-lookup"><span data-stu-id="98f17-138">In other words, a link relationship between an Azure AD user and the related user in Palo Alto Networks - GlobalProtect needs to be established.</span></span>

<span data-ttu-id="98f17-139">In Palo Alto Networks - GlobalProtect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="98f17-139">In Palo Alto Networks - GlobalProtect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="98f17-140">To configure and test Azure AD single sign-on with Palo Alto Networks - GlobalProtect, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="98f17-140">To configure and test Azure AD single sign-on with Palo Alto Networks - GlobalProtect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="98f17-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="98f17-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="98f17-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98f17-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="98f17-143">**[Create a Palo Alto Networks - GlobalProtect test user](#create-a-palo-alto-networks---globalprotect-test-user)** - to have a counterpart of Britta Simon in Palo Alto Networks - GlobalProtect that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="98f17-143">**[Create a Palo Alto Networks - GlobalProtect test user](#create-a-palo-alto-networks---globalprotect-test-user)** - to have a counterpart of Britta Simon in Palo Alto Networks - GlobalProtect that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="98f17-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="98f17-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="98f17-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="98f17-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="98f17-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="98f17-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="98f17-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Palo Alto Networks - GlobalProtect application.</span><span class="sxs-lookup"><span data-stu-id="98f17-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Palo Alto Networks - GlobalProtect application.</span></span>

<span data-ttu-id="98f17-148">**To configure Azure AD single sign-on with Palo Alto Networks - GlobalProtect, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="98f17-148">**To configure Azure AD single sign-on with Palo Alto Networks - GlobalProtect, perform the following steps:**</span></span>

1. <span data-ttu-id="98f17-149">In the Azure portal, on the **Palo Alto Networks - GlobalProtect** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="98f17-149">In the Azure portal, on the **Palo Alto Networks - GlobalProtect** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="98f17-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="98f17-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoglobal_samlbase.png)

1. <span data-ttu-id="98f17-153">On the **Palo Alto Networks - GlobalProtect Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="98f17-153">On the **Palo Alto Networks - GlobalProtect Domain and URLs** section, perform the following steps:</span></span>

    ![Palo Alto Networks - GlobalProtect Domain and URLs single sign-on information](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoglobal_url.png)

    <span data-ttu-id="98f17-155">a.</span><span class="sxs-lookup"><span data-stu-id="98f17-155">a.</span></span> <span data-ttu-id="98f17-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Customer Firewall URL>`</span><span class="sxs-lookup"><span data-stu-id="98f17-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Customer Firewall URL>`</span></span>

    <span data-ttu-id="98f17-157">b.</span><span class="sxs-lookup"><span data-stu-id="98f17-157">b.</span></span> <span data-ttu-id="98f17-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<Customer Firewall URL>/SAML20/SP`</span><span class="sxs-lookup"><span data-stu-id="98f17-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<Customer Firewall URL>/SAML20/SP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="98f17-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="98f17-159">These values are not real.</span></span> <span data-ttu-id="98f17-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="98f17-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="98f17-161">Contact [Palo Alto Networks - GlobalProtect Client support team](https://support.paloaltonetworks.com/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="98f17-161">Contact [Palo Alto Networks - GlobalProtect Client support team](https://support.paloaltonetworks.com/support) to get these values.</span></span> 
 
1. <span data-ttu-id="98f17-162">Palo Alto Networks - GlobalProtect application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="98f17-162">Palo Alto Networks - GlobalProtect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="98f17-163">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="98f17-163">Please configure the following claims for this application.</span></span> <span data-ttu-id="98f17-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="98f17-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="98f17-165">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="98f17-165">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoglobal_attribute.png)
    
1. <span data-ttu-id="98f17-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="98f17-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="98f17-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="98f17-168">Attribute Name</span></span> | <span data-ttu-id="98f17-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="98f17-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="98f17-170">username</span><span class="sxs-lookup"><span data-stu-id="98f17-170">username</span></span> | <span data-ttu-id="98f17-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="98f17-171">user.userprincipalname</span></span> |

    <span data-ttu-id="98f17-172">a.</span><span class="sxs-lookup"><span data-stu-id="98f17-172">a.</span></span> <span data-ttu-id="98f17-173">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="98f17-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/paloaltoglobalprotect-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/paloaltoglobalprotect-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="98f17-176">b.</span><span class="sxs-lookup"><span data-stu-id="98f17-176">b.</span></span> <span data-ttu-id="98f17-177">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="98f17-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="98f17-178">c.</span><span class="sxs-lookup"><span data-stu-id="98f17-178">c.</span></span> <span data-ttu-id="98f17-179">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="98f17-179">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="98f17-180">We have mapped the value with user.userprincipalname as an example but you can map with your appropriate value.</span><span class="sxs-lookup"><span data-stu-id="98f17-180">We have mapped the value with user.userprincipalname as an example but you can map with your appropriate value.</span></span> 
    
    <span data-ttu-id="98f17-181">d.</span><span class="sxs-lookup"><span data-stu-id="98f17-181">d.</span></span> <span data-ttu-id="98f17-182">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="98f17-182">Click **Ok**</span></span>


1. <span data-ttu-id="98f17-183">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="98f17-183">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoglobal_certificate.png) 

1. <span data-ttu-id="98f17-185">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="98f17-185">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/paloaltoglobalprotect-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="98f17-187">Open the Palo Alto Networks Firewall Admin UI as an administrator in another browser window.</span><span class="sxs-lookup"><span data-stu-id="98f17-187">Open the Palo Alto Networks Firewall Admin UI as an administrator in another browser window.</span></span>

1. <span data-ttu-id="98f17-188">Click on **Device**.</span><span class="sxs-lookup"><span data-stu-id="98f17-188">Click on **Device**.</span></span>

    ![Configure Palo Alto Single Sign-on](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoadmin_admin1.png)

1. <span data-ttu-id="98f17-190">Select **SAML Identity Provider** from the left navigation bar and click "Import" to import the metadata file.</span><span class="sxs-lookup"><span data-stu-id="98f17-190">Select **SAML Identity Provider** from the left navigation bar and click "Import" to import the metadata file.</span></span>

    ![Configure Palo Alto Single Sign-on](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoadmin_admin2.png)

1. <span data-ttu-id="98f17-192">Perform following actions on the Import window</span><span class="sxs-lookup"><span data-stu-id="98f17-192">Perform following actions on the Import window</span></span>

    ![Configure Palo Alto Single Sign-on](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoadmin_admin3.png)

    <span data-ttu-id="98f17-194">a.</span><span class="sxs-lookup"><span data-stu-id="98f17-194">a.</span></span> <span data-ttu-id="98f17-195">In the **Profile Name** textbox, provide a name e.g Azure AD GlobalProtect.</span><span class="sxs-lookup"><span data-stu-id="98f17-195">In the **Profile Name** textbox, provide a name e.g Azure AD GlobalProtect.</span></span>
    
    <span data-ttu-id="98f17-196">b.</span><span class="sxs-lookup"><span data-stu-id="98f17-196">b.</span></span> <span data-ttu-id="98f17-197">In **Identity Provider Metadata**, click **Browse** and select the metadata.xml file which you have downloaded from Azure portal</span><span class="sxs-lookup"><span data-stu-id="98f17-197">In **Identity Provider Metadata**, click **Browse** and select the metadata.xml file which you have downloaded from Azure portal</span></span>
    
    <span data-ttu-id="98f17-198">c.</span><span class="sxs-lookup"><span data-stu-id="98f17-198">c.</span></span> <span data-ttu-id="98f17-199">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="98f17-199">Click **OK**</span></span>

> [!TIP]
> <span data-ttu-id="98f17-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="98f17-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="98f17-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="98f17-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="98f17-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="98f17-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="98f17-203">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="98f17-203">Create an Azure AD test user</span></span>

<span data-ttu-id="98f17-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98f17-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="98f17-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="98f17-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="98f17-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="98f17-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/paloaltoglobalprotect-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="98f17-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="98f17-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/paloaltoglobalprotect-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="98f17-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="98f17-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/paloaltoglobalprotect-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="98f17-213">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="98f17-213">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/paloaltoglobalprotect-tutorial/create_aaduser_04.png)

    <span data-ttu-id="98f17-215">a.</span><span class="sxs-lookup"><span data-stu-id="98f17-215">a.</span></span> <span data-ttu-id="98f17-216">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="98f17-216">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98f17-217">b.</span><span class="sxs-lookup"><span data-stu-id="98f17-217">b.</span></span> <span data-ttu-id="98f17-218">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98f17-218">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="98f17-219">c.</span><span class="sxs-lookup"><span data-stu-id="98f17-219">c.</span></span> <span data-ttu-id="98f17-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="98f17-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="98f17-221">d.</span><span class="sxs-lookup"><span data-stu-id="98f17-221">d.</span></span> <span data-ttu-id="98f17-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="98f17-222">Click **Create**.</span></span>
 
### <a name="create-a-palo-alto-networks---globalprotect-test-user"></a><span data-ttu-id="98f17-223">Create a Palo Alto Networks - GlobalProtect test user</span><span class="sxs-lookup"><span data-stu-id="98f17-223">Create a Palo Alto Networks - GlobalProtect test user</span></span>

<span data-ttu-id="98f17-224">Palo Alto Networks - GlobalProtect supports Just-in-time user provisioning so a user will be automatically created in the system after the successful authentication if it doesn't already exists.</span><span class="sxs-lookup"><span data-stu-id="98f17-224">Palo Alto Networks - GlobalProtect supports Just-in-time user provisioning so a user will be automatically created in the system after the successful authentication if it doesn't already exists.</span></span> <span data-ttu-id="98f17-225">You don't need to perform any action here.</span><span class="sxs-lookup"><span data-stu-id="98f17-225">You don't need to perform any action here.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="98f17-226">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="98f17-226">Assign the Azure AD test user</span></span>

<span data-ttu-id="98f17-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Palo Alto Networks - GlobalProtect.</span><span class="sxs-lookup"><span data-stu-id="98f17-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Palo Alto Networks - GlobalProtect.</span></span>

![Assign the user role][200] 

<span data-ttu-id="98f17-229">**To assign Britta Simon to Palo Alto Networks - GlobalProtect, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="98f17-229">**To assign Britta Simon to Palo Alto Networks - GlobalProtect, perform the following steps:**</span></span>

1. <span data-ttu-id="98f17-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="98f17-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="98f17-232">In the applications list, select **Palo Alto Networks - GlobalProtect**.</span><span class="sxs-lookup"><span data-stu-id="98f17-232">In the applications list, select **Palo Alto Networks - GlobalProtect**.</span></span>

    ![The Palo Alto Networks - GlobalProtect link in the Applications list](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoglobal_app.png)  

1. <span data-ttu-id="98f17-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="98f17-234">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="98f17-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="98f17-236">Click **Add** button.</span></span> <span data-ttu-id="98f17-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="98f17-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="98f17-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="98f17-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="98f17-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="98f17-240">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="98f17-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="98f17-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="98f17-242">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="98f17-242">Test single sign-on</span></span>

<span data-ttu-id="98f17-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="98f17-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="98f17-244">When you click the Palo Alto Networks - GlobalProtect tile in the Access Panel, you should get automatically signed-on to your Palo Alto Networks - GlobalProtect application.</span><span class="sxs-lookup"><span data-stu-id="98f17-244">When you click the Palo Alto Networks - GlobalProtect tile in the Access Panel, you should get automatically signed-on to your Palo Alto Networks - GlobalProtect application.</span></span>
<span data-ttu-id="98f17-245">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="98f17-245">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="98f17-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="98f17-246">Additional resources</span></span>

* [<span data-ttu-id="98f17-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98f17-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="98f17-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="98f17-248">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/paloaltoglobalprotect-tutorial/tutorial_general_01.png
[2]: ./media/paloaltoglobalprotect-tutorial/tutorial_general_02.png
[3]: ./media/paloaltoglobalprotect-tutorial/tutorial_general_03.png
[4]: ./media/paloaltoglobalprotect-tutorial/tutorial_general_04.png

[100]: ./media/paloaltoglobalprotect-tutorial/tutorial_general_100.png

[200]: ./media/paloaltoglobalprotect-tutorial/tutorial_general_200.png
[201]: ./media/paloaltoglobalprotect-tutorial/tutorial_general_201.png
[202]: ./media/paloaltoglobalprotect-tutorial/tutorial_general_202.png
[203]: ./media/paloaltoglobalprotect-tutorial/tutorial_general_203.png

