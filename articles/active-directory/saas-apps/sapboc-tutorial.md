---
title: 'Tutorial: Azure Active Directory integration with SAP Business Object Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP Business Object Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: ffd4480a13549caba17becff27a43f51fcaa1988
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868352"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="fbace-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="fbace-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="fbace-104">In this tutorial, you learn how to integrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbace-104">In this tutorial, you learn how to integrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbace-105">You get the following benefits when you integrate SAP Business Object Cloud with Azure AD:</span><span class="sxs-lookup"><span data-stu-id="fbace-105">You get the following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="fbace-106">In Azure AD, you can control who has access to SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="fbace-106">In Azure AD, you can control who has access to SAP Business Object Cloud.</span></span>
- <span data-ttu-id="fbace-107">You can automatically sign in your users to SAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="fbace-107">You can automatically sign in your users to SAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="fbace-108">You can manage your accounts in one, central location, the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fbace-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="fbace-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="fbace-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbace-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fbace-110">Prerequisites</span></span>

<span data-ttu-id="fbace-111">To set up Azure AD integration with SAP Business Object Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fbace-111">To set up Azure AD integration with SAP Business Object Cloud, you need the following items:</span></span>

- <span data-ttu-id="fbace-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fbace-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbace-113">An SAP Business Object Cloud, with single sign-on turned on</span><span class="sxs-lookup"><span data-stu-id="fbace-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="fbace-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span><span class="sxs-lookup"><span data-stu-id="fbace-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="fbace-115">Recommendations for testing the steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="fbace-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="fbace-116">Do not use your production environment, unless it's necessary.</span><span class="sxs-lookup"><span data-stu-id="fbace-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="fbace-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbace-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbace-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="fbace-118">Scenario description</span></span>
<span data-ttu-id="fbace-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="fbace-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="fbace-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="fbace-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbace-121">Add SAP Business Object Cloud from the gallery.</span><span class="sxs-lookup"><span data-stu-id="fbace-121">Add SAP Business Object Cloud from the gallery.</span></span>
2. <span data-ttu-id="fbace-122">Set up and test Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fbace-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-the-gallery"></a><span data-ttu-id="fbace-123">Add SAP Business Object Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="fbace-123">Add SAP Business Object Cloud from the gallery</span></span>
<span data-ttu-id="fbace-124">To set up the integration of SAP Business Object Cloud with Azure AD, in the gallery, add SAP Business Object Cloud to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="fbace-124">To set up the integration of SAP Business Object Cloud with Azure AD, in the gallery, add SAP Business Object Cloud to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fbace-125">To add SAP Business Object Cloud from the gallery:</span><span class="sxs-lookup"><span data-stu-id="fbace-125">To add SAP Business Object Cloud from the gallery:</span></span>

1. <span data-ttu-id="fbace-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbace-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="fbace-128">Select **Enterprise applications**, and then select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fbace-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![The Enterprise applications page][2]
    
3. <span data-ttu-id="fbace-130">To add a new application, select **New application**.</span><span class="sxs-lookup"><span data-stu-id="fbace-130">To add a new application, select **New application**.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="fbace-132">In the search box, enter **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="fbace-132">In the search box, enter **SAP Business Object Cloud**.</span></span>

    ![The search box](./media/sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="fbace-134">In the results panel, select **SAP Business Object Cloud**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="fbace-134">In the results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business Object Cloud in the results list](./media/sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fbace-136">Set up and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fbace-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="fbace-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="fbace-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="fbace-138">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="fbace-138">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="fbace-139">A link relationship between an Azure AD user and the related user in SAP Business Object Cloud must be established.</span><span class="sxs-lookup"><span data-stu-id="fbace-139">A link relationship between an Azure AD user and the related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="fbace-140">To establish the link relationship, in SAP Business Object Cloud, for **Username**, assign the value of the **user name** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbace-140">To establish the link relationship, in SAP Business Object Cloud, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="fbace-141">To configure and test Azure AD single sign-on with SAP Business Object Cloud, complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="fbace-141">To configure and test Azure AD single sign-on with SAP Business Object Cloud, complete the following tasks:</span></span>

1. <span data-ttu-id="fbace-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="fbace-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="fbace-143">Sets up a user to use this feature.</span><span class="sxs-lookup"><span data-stu-id="fbace-143">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="fbace-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="fbace-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="fbace-145">Tests Azure AD single sign-on with the user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbace-145">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="fbace-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="fbace-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="fbace-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked to the Azure AD representation of the user.</span><span class="sxs-lookup"><span data-stu-id="fbace-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="fbace-148">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="fbace-148">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="fbace-149">Sets up Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fbace-149">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbace-150">[Test single sign-on](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="fbace-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="fbace-151">Verifies that the configuration works.</span><span class="sxs-lookup"><span data-stu-id="fbace-151">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="fbace-152">Set up Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fbace-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="fbace-153">In this section, you turn on Azure AD single sign-on in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fbace-153">In this section, you turn on Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="fbace-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span><span class="sxs-lookup"><span data-stu-id="fbace-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="fbace-155">To set up Azure AD single sign-on with SAP Business Object Cloud:</span><span class="sxs-lookup"><span data-stu-id="fbace-155">To set up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="fbace-156">In the Azure portal, on the **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fbace-156">In the Azure portal, on the **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Select Single Sign-On][4]

2. <span data-ttu-id="fbace-158">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fbace-158">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Select SAML-based Sign-on](./media/sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="fbace-160">Under **SAP Business Object Cloud Domain and URLs**, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="fbace-160">Under **SAP Business Object Cloud Domain and URLs**, complete the following steps:</span></span>

    1. <span data-ttu-id="fbace-161">In the **Sign-on URL** box, enter a URL that has the following pattern:</span><span class="sxs-lookup"><span data-stu-id="fbace-161">In the **Sign-on URL** box, enter a URL that has the following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="fbace-162">In the **Identifier** box, enter a URL that has the following pattern:</span><span class="sxs-lookup"><span data-stu-id="fbace-162">In the **Identifier** box, enter a URL that has the following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![SAP Business Object Cloud Domain and URLs page URLs](./media/sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="fbace-164">The values in these URLs are for demonstration only.</span><span class="sxs-lookup"><span data-stu-id="fbace-164">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="fbace-165">Update the values with the actual sign-on URL and identifier URL.</span><span class="sxs-lookup"><span data-stu-id="fbace-165">Update the values with the actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="fbace-166">To get the sign-on URL, contact the [SAP Business Object Cloud Client support team](https://help.sap.com/viewer/product/SAP_BusinessObjects_Cloud/release/en-US).</span><span class="sxs-lookup"><span data-stu-id="fbace-166">To get the sign-on URL, contact the [SAP Business Object Cloud Client support team](https://help.sap.com/viewer/product/SAP_BusinessObjects_Cloud/release/en-US).</span></span> <span data-ttu-id="fbace-167">You can get the identifier URL by downloading the SAP Business Object Cloud metadata from the admin console.</span><span class="sxs-lookup"><span data-stu-id="fbace-167">You can get the identifier URL by downloading the SAP Business Object Cloud metadata from the admin console.</span></span> <span data-ttu-id="fbace-168">This is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="fbace-168">This is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="fbace-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="fbace-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="fbace-170">Then, save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="fbace-170">Then, save the metadata file on your computer.</span></span>

    ![Select Metadata XML](./media/sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="fbace-172">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="fbace-172">Select **Save**.</span></span>

    ![Select Save](./media/sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbace-174">In a different web browser window, sign in to your SAP Business Object Cloud company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="fbace-174">In a different web browser window, sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="fbace-175">Select **Menu** > **System** > **Administration**.</span><span class="sxs-lookup"><span data-stu-id="fbace-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Select Menu, then System, and then Administration](./media/sapboc-tutorial/config1.png)

8. <span data-ttu-id="fbace-177">On the **Security** tab, select the **Edit** (pen) icon.</span><span class="sxs-lookup"><span data-stu-id="fbace-177">On the **Security** tab, select the **Edit** (pen) icon.</span></span>
    
    ![On the Security tab, select the Edit icon](./media/sapboc-tutorial/config2.png)  

9. <span data-ttu-id="fbace-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="fbace-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Select SAML Single Sign-On for the authentication method](./media/sapboc-tutorial/config3.png)  

10. <span data-ttu-id="fbace-181">To download the service provider metadata (Step 1), select **Download**.</span><span class="sxs-lookup"><span data-stu-id="fbace-181">To download the service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="fbace-182">In the metadata file, find and copy the **entityID** value.</span><span class="sxs-lookup"><span data-stu-id="fbace-182">In the metadata file, find and copy the **entityID** value.</span></span> <span data-ttu-id="fbace-183">In the Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste the value in the **Identifier** box.</span><span class="sxs-lookup"><span data-stu-id="fbace-183">In the Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste the value in the **Identifier** box.</span></span>

    ![Copy and paste the entityID value](./media/sapboc-tutorial/config4.png)  

11. <span data-ttu-id="fbace-185">To upload the service provider metadata (Step 2) in the file that you downloaded from the Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="fbace-185">To upload the service provider metadata (Step 2) in the file that you downloaded from the Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![Under Upload Identity Provider metadata, select Upload](./media/sapboc-tutorial/config5.png)

12. <span data-ttu-id="fbace-187">In the **User Attribute** list, select the user attribute (Step 3) that you want to use for your implementation.</span><span class="sxs-lookup"><span data-stu-id="fbace-187">In the **User Attribute** list, select the user attribute (Step 3) that you want to use for your implementation.</span></span> <span data-ttu-id="fbace-188">This user attribute maps to the identity provider.</span><span class="sxs-lookup"><span data-stu-id="fbace-188">This user attribute maps to the identity provider.</span></span> <span data-ttu-id="fbace-189">To enter a custom attribute on the user's page, use the **Custom SAML Mapping** option.</span><span class="sxs-lookup"><span data-stu-id="fbace-189">To enter a custom attribute on the user's page, use the **Custom SAML Mapping** option.</span></span> <span data-ttu-id="fbace-190">Or, you can select either **Email** or **USER ID** as the user attribute.</span><span class="sxs-lookup"><span data-stu-id="fbace-190">Or, you can select either **Email** or **USER ID** as the user attribute.</span></span> <span data-ttu-id="fbace-191">In our example, we selected **Email** because we mapped the user identifier claim with the **userprincipalname** attribute in the **User Attributes** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fbace-191">In our example, we selected **Email** because we mapped the user identifier claim with the **userprincipalname** attribute in the **User Attributes** section in the Azure portal.</span></span> <span data-ttu-id="fbace-192">This provides a unique user email, which is sent to the SAP Business Object Cloud application in every successful SAML response.</span><span class="sxs-lookup"><span data-stu-id="fbace-192">This provides a unique user email, which is sent to the SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Select User Attribute](./media/sapboc-tutorial/config6.png)

13. <span data-ttu-id="fbace-194">To verify the account with the identity provider (Step 4), in the **Login Credential (Email)** box, enter the user's email address.</span><span class="sxs-lookup"><span data-stu-id="fbace-194">To verify the account with the identity provider (Step 4), in the **Login Credential (Email)** box, enter the user's email address.</span></span> <span data-ttu-id="fbace-195">Then, select **Verify Account**.</span><span class="sxs-lookup"><span data-stu-id="fbace-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="fbace-196">The system adds sign-in credentials to the user account.</span><span class="sxs-lookup"><span data-stu-id="fbace-196">The system adds sign-in credentials to the user account.</span></span>

    ![Enter email, and select Verify Account](./media/sapboc-tutorial/config7.png)

14. <span data-ttu-id="fbace-198">Select the **Save** icon.</span><span class="sxs-lookup"><span data-stu-id="fbace-198">Select the **Save** icon.</span></span>

    ![Save icon](./media/sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="fbace-200">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span><span class="sxs-lookup"><span data-stu-id="fbace-200">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="fbace-201">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="fbace-201">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="fbace-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="fbace-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fbace-203">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fbace-203">Create an Azure AD test user</span></span>
<span data-ttu-id="fbace-204">In this section, you create a test user named Britta Simon in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fbace-204">In this section, you create a test user named Britta Simon in the Azure portal.</span></span>

<span data-ttu-id="fbace-205">To create a test user in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="fbace-205">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="fbace-206">In the Azure portal, in the left menu, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbace-206">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Creating an Azure AD test user](./media/sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbace-208">To display the list of users, select **Users and groups**, and then select **All users**.</span><span class="sxs-lookup"><span data-stu-id="fbace-208">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbace-210">To open the **User** dialog box, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="fbace-210">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Creating an Azure AD test user](./media/sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbace-212">In the **User** dialog box, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="fbace-212">In the **User** dialog box, complete the following steps:</span></span>
 
    1. <span data-ttu-id="fbace-213">In the **Name** box, enter **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbace-213">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="fbace-214">In the **User name** box, enter the email address of the user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbace-214">In the **User name** box, enter the email address of the user Britta Simon.</span></span>

    3. <span data-ttu-id="fbace-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="fbace-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="fbace-216">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="fbace-216">Select **Create**.</span></span>

        ![The User dialog box](./media/sapboc-tutorial/create_aaduser_04.png) 

    ![Create Azure AD User][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="fbace-219">Create an SAP Business Object Cloud test user</span><span class="sxs-lookup"><span data-stu-id="fbace-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="fbace-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in to SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="fbace-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in to SAP Business Object Cloud.</span></span> <span data-ttu-id="fbace-221">In SAP Business Object Cloud, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="fbace-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="fbace-222">To provision a user account:</span><span class="sxs-lookup"><span data-stu-id="fbace-222">To provision a user account:</span></span>

1. <span data-ttu-id="fbace-223">Sign in to your SAP Business Object Cloud company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="fbace-223">Sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="fbace-224">Select **Menu** > **Security** > **Users**.</span><span class="sxs-lookup"><span data-stu-id="fbace-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Add Employee](./media/sapboc-tutorial/user1.png)

3. <span data-ttu-id="fbace-226">On the **Users** page, to add new user details, select **+**.</span><span class="sxs-lookup"><span data-stu-id="fbace-226">On the **Users** page, to add new user details, select **+**.</span></span> 

    ![Add Users page](./media/sapboc-tutorial/user4.png)

    <span data-ttu-id="fbace-228">Then, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="fbace-228">Then, complete the following steps:</span></span>

    1. <span data-ttu-id="fbace-229">In the **USER ID** box, enter the user ID of the user, like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fbace-229">In the **USER ID** box, enter the user ID of the user, like **Britta**.</span></span>

    2. <span data-ttu-id="fbace-230">In the **FIRST NAME** box, enter the first name of the user, like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fbace-230">In the **FIRST NAME** box, enter the first name of the user, like **Britta**.</span></span>

    3. <span data-ttu-id="fbace-231">In the **LAST NAME** box, enter the last name of the user, like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fbace-231">In the **LAST NAME** box, enter the last name of the user, like **Simon**.</span></span>

    4. <span data-ttu-id="fbace-232">In the **DISPLAY NAME** box, enter the full name of the user, like **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fbace-232">In the **DISPLAY NAME** box, enter the full name of the user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="fbace-233">In the **E-MAIL** box, enter the email address of the user, like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="fbace-233">In the **E-MAIL** box, enter the email address of the user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="fbace-234">On the **Select Roles** page, select the appropriate role for the user, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="fbace-234">On the **Select Roles** page, select the appropriate role for the user, and then select **OK**.</span></span>

      ![Select role](./media/sapboc-tutorial/user3.png)

    7. <span data-ttu-id="fbace-236">Select the **Save** icon.</span><span class="sxs-lookup"><span data-stu-id="fbace-236">Select the **Save** icon.</span></span>    


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fbace-237">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fbace-237">Assign the Azure AD test user</span></span>

<span data-ttu-id="fbace-238">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="fbace-238">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to SAP Business Object Cloud.</span></span>

<span data-ttu-id="fbace-239">To assign Britta Simon to SAP Business Object Cloud:</span><span class="sxs-lookup"><span data-stu-id="fbace-239">To assign Britta Simon to SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="fbace-240">In the Azure portal, open the applications view, and then go to the directory view.</span><span class="sxs-lookup"><span data-stu-id="fbace-240">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="fbace-241">Select **Enterprise applications**, and then select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fbace-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="fbace-243">In the applications list, select **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="fbace-243">In the applications list, select **SAP Business Object Cloud**.</span></span>

    ![Configure Single Sign-On](./media/sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="fbace-245">In the left menu, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="fbace-245">In the left menu, select **Users and groups**.</span></span>

    ![Select Users and groups][202] 

4. <span data-ttu-id="fbace-247">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="fbace-247">Select **Add**.</span></span> <span data-ttu-id="fbace-248">Then, on the **Add Assignment** page, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="fbace-248">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![The Add Assignment page][203]

5. <span data-ttu-id="fbace-250">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fbace-250">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="fbace-251">On the **Users and groups** page, select **Select**.</span><span class="sxs-lookup"><span data-stu-id="fbace-251">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="fbace-252">On the **Add Assignment** page, select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="fbace-252">On the **Add Assignment** page, select **Assign**.</span></span>

![Assign the user role][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fbace-254">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="fbace-254">Test single sign-on</span></span>

<span data-ttu-id="fbace-255">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span><span class="sxs-lookup"><span data-stu-id="fbace-255">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="fbace-256">When you select the SAP Business Object Cloud tile in the access panel, you should be automatically signed in to your SAP Business Object Cloud application.</span><span class="sxs-lookup"><span data-stu-id="fbace-256">When you select the SAP Business Object Cloud tile in the access panel, you should be automatically signed in to your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="fbace-257">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbace-257">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fbace-258">Additional resources</span><span class="sxs-lookup"><span data-stu-id="fbace-258">Additional resources</span></span>

* [<span data-ttu-id="fbace-259">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbace-259">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="fbace-260">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fbace-260">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/sapboc-tutorial/tutorial_general_01.png
[2]: ./media/sapboc-tutorial/tutorial_general_02.png
[3]: ./media/sapboc-tutorial/tutorial_general_03.png
[4]: ./media/sapboc-tutorial/tutorial_general_04.png

[100]: ./media/sapboc-tutorial/tutorial_general_100.png

[200]: ./media/sapboc-tutorial/tutorial_general_200.png
[201]: ./media/sapboc-tutorial/tutorial_general_201.png
[202]: ./media/sapboc-tutorial/tutorial_general_202.png
[203]: ./media/sapboc-tutorial/tutorial_general_203.png

