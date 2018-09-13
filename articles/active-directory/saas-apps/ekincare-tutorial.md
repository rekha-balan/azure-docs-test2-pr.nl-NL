---
title: 'Tutorial: Azure Active Directory integration with eKincare | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and eKincare.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: e6cf860f161015fa0698effcd4ecaead263b29f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868999"
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="48448-103">Tutorial: Azure Active Directory integration with eKincare</span><span class="sxs-lookup"><span data-stu-id="48448-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="48448-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48448-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48448-105">Integrating eKincare with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="48448-105">Integrating eKincare with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48448-106">You can control in Azure AD who has access to eKincare</span><span class="sxs-lookup"><span data-stu-id="48448-106">You can control in Azure AD who has access to eKincare</span></span>
- <span data-ttu-id="48448-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="48448-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48448-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="48448-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="48448-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="48448-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48448-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="48448-110">Prerequisites</span></span>

<span data-ttu-id="48448-111">To configure Azure AD integration with eKincare, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="48448-111">To configure Azure AD integration with eKincare, you need the following items:</span></span>

- <span data-ttu-id="48448-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="48448-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48448-113">A eKincare single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="48448-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48448-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="48448-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48448-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="48448-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48448-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="48448-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48448-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48448-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48448-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="48448-118">Scenario description</span></span>
<span data-ttu-id="48448-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="48448-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48448-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="48448-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48448-121">Adding eKincare from the gallery</span><span class="sxs-lookup"><span data-stu-id="48448-121">Adding eKincare from the gallery</span></span>
1. <span data-ttu-id="48448-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48448-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-the-gallery"></a><span data-ttu-id="48448-123">Adding eKincare from the gallery</span><span class="sxs-lookup"><span data-stu-id="48448-123">Adding eKincare from the gallery</span></span>
<span data-ttu-id="48448-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="48448-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48448-125">**To add eKincare from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48448-125">**To add eKincare from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48448-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="48448-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="48448-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="48448-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48448-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="48448-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="48448-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="48448-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="48448-133">In the search box, type **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="48448-133">In the search box, type **eKincare**.</span></span>

    ![Creating an Azure AD test user](./media/ekincare-tutorial/tutorial_ekincare_search.png)

1. <span data-ttu-id="48448-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="48448-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48448-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48448-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48448-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="48448-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="48448-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48448-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span></span> <span data-ttu-id="48448-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span><span class="sxs-lookup"><span data-stu-id="48448-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span></span>

<span data-ttu-id="48448-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="48448-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48448-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="48448-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48448-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="48448-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="48448-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48448-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="48448-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="48448-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="48448-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48448-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="48448-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="48448-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48448-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48448-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48448-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span><span class="sxs-lookup"><span data-stu-id="48448-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="48448-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48448-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="48448-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="48448-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="48448-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48448-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/ekincare-tutorial/tutorial_ekincare_samlbase.png)

1. <span data-ttu-id="48448-155">On the **eKincare Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48448-155">On the **eKincare Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="48448-157">a.</span><span class="sxs-lookup"><span data-stu-id="48448-157">a.</span></span> <span data-ttu-id="48448-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="48448-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="48448-159">b.</span><span class="sxs-lookup"><span data-stu-id="48448-159">b.</span></span> <span data-ttu-id="48448-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="48448-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48448-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="48448-161">These values are not real.</span></span> <span data-ttu-id="48448-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="48448-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="48448-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="48448-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span></span>
 
1. <span data-ttu-id="48448-164">eKincare application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="48448-164">eKincare application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="48448-165">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="48448-165">Configure the following claims for this application.</span></span> <span data-ttu-id="48448-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="48448-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="48448-167">The following screenshot shows an example for this configuration.</span><span class="sxs-lookup"><span data-stu-id="48448-167">The following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="48448-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span><span class="sxs-lookup"><span data-stu-id="48448-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span></span> <span data-ttu-id="48448-169">The other two claims' name i.e</span><span class="sxs-lookup"><span data-stu-id="48448-169">The other two claims' name i.e</span></span> <span data-ttu-id="48448-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span><span class="sxs-lookup"><span data-stu-id="48448-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span></span>
    
    ![Configure Single Sign-On](./media/ekincare-tutorial/attribute.png)
    
1. <span data-ttu-id="48448-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48448-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="48448-173">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="48448-173">Attribute Name</span></span> | <span data-ttu-id="48448-174">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="48448-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="48448-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="48448-175">employeeid</span></span> | <span data-ttu-id="48448-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="48448-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="48448-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="48448-177">organizationid</span></span> | <span data-ttu-id="48448-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="48448-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="48448-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="48448-179">organizationname</span></span> | <span data-ttu-id="48448-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="48448-180">*user.companyname*</span></span> |

    <span data-ttu-id="48448-181">a.</span><span class="sxs-lookup"><span data-stu-id="48448-181">a.</span></span> <span data-ttu-id="48448-182">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="48448-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/ekincare-tutorial/04.png)

    ![Configure Single Sign-On](./media/ekincare-tutorial/05.png)
    
    <span data-ttu-id="48448-185">b.</span><span class="sxs-lookup"><span data-stu-id="48448-185">b.</span></span> <span data-ttu-id="48448-186">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="48448-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="48448-187">c.</span><span class="sxs-lookup"><span data-stu-id="48448-187">c.</span></span> <span data-ttu-id="48448-188">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="48448-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="48448-189">d.</span><span class="sxs-lookup"><span data-stu-id="48448-189">d.</span></span> <span data-ttu-id="48448-190">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="48448-190">Click **Ok**</span></span>

1. <span data-ttu-id="48448-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="48448-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/ekincare-tutorial/tutorial_ekincare_certificate.png) 

1. <span data-ttu-id="48448-193">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="48448-193">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/ekincare-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="48448-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="48448-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="48448-196">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="48448-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="48448-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="48448-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48448-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="48448-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48448-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48448-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48448-200">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="48448-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="48448-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48448-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="48448-203">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48448-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48448-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="48448-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/ekincare-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="48448-206">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="48448-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/ekincare-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="48448-208">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="48448-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/ekincare-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="48448-210">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48448-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48448-212">a.</span><span class="sxs-lookup"><span data-stu-id="48448-212">a.</span></span> <span data-ttu-id="48448-213">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48448-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48448-214">b.</span><span class="sxs-lookup"><span data-stu-id="48448-214">b.</span></span> <span data-ttu-id="48448-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="48448-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48448-216">c.</span><span class="sxs-lookup"><span data-stu-id="48448-216">c.</span></span> <span data-ttu-id="48448-217">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="48448-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="48448-218">d.</span><span class="sxs-lookup"><span data-stu-id="48448-218">d.</span></span> <span data-ttu-id="48448-219">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="48448-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="48448-220">Creating a eKincare test user</span><span class="sxs-lookup"><span data-stu-id="48448-220">Creating a eKincare test user</span></span>

<span data-ttu-id="48448-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="48448-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48448-222">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="48448-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="48448-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span><span class="sxs-lookup"><span data-stu-id="48448-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span></span>

![Assign User][200] 

<span data-ttu-id="48448-225">**To assign Britta Simon to eKincare, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48448-225">**To assign Britta Simon to eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="48448-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="48448-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="48448-228">In the applications list, select **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="48448-228">In the applications list, select **eKincare**.</span></span>

    ![Configure Single Sign-On](./media/ekincare-tutorial/tutorial_ekincare_app.png) 

1. <span data-ttu-id="48448-230">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="48448-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="48448-232">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="48448-232">Click **Add** button.</span></span> <span data-ttu-id="48448-233">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="48448-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="48448-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="48448-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="48448-236">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="48448-236">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="48448-237">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="48448-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48448-238">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="48448-238">Testing single sign-on</span></span>

<span data-ttu-id="48448-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="48448-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="48448-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span><span class="sxs-lookup"><span data-stu-id="48448-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span></span>
<span data-ttu-id="48448-241">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="48448-241">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48448-242">Additional resources</span><span class="sxs-lookup"><span data-stu-id="48448-242">Additional resources</span></span>

* [<span data-ttu-id="48448-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48448-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="48448-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48448-244">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/ekincare-tutorial/tutorial_general_01.png
[2]: ./media/ekincare-tutorial/tutorial_general_02.png
[3]: ./media/ekincare-tutorial/tutorial_general_03.png
[4]: ./media/ekincare-tutorial/tutorial_general_04.png

[100]: ./media/ekincare-tutorial/tutorial_general_100.png

[200]: ./media/ekincare-tutorial/tutorial_general_200.png
[201]: ./media/ekincare-tutorial/tutorial_general_201.png
[202]: ./media/ekincare-tutorial/tutorial_general_202.png
[203]: ./media/ekincare-tutorial/tutorial_general_203.png

