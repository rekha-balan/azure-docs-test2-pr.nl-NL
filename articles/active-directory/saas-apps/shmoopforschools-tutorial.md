---
title: 'Tutorial: Azure Active Directory integration with Shmoop For Schools | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Shmoop For Schools.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 1d75560a-55b3-42e9-bda1-92b01c572d8e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/23/2018
ms.author: jeedes
ms.openlocfilehash: b5826fd3067ac337808b9e27040dee808cd6a01c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867504"
---
# <a name="tutorial-azure-active-directory-integration-with-shmoop-for-schools"></a><span data-ttu-id="d240a-103">Tutorial: Azure Active Directory integration with Shmoop For Schools</span><span class="sxs-lookup"><span data-stu-id="d240a-103">Tutorial: Azure Active Directory integration with Shmoop For Schools</span></span>

<span data-ttu-id="d240a-104">In this tutorial, you learn how to integrate Shmoop For Schools with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d240a-104">In this tutorial, you learn how to integrate Shmoop For Schools with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d240a-105">Integrating Shmoop For Schools with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d240a-105">Integrating Shmoop For Schools with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d240a-106">You can control in Azure AD who has access to Shmoop For Schools.</span><span class="sxs-lookup"><span data-stu-id="d240a-106">You can control in Azure AD who has access to Shmoop For Schools.</span></span>
- <span data-ttu-id="d240a-107">You can enable your users to automatically get signed in to Shmoop For Schools with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="d240a-107">You can enable your users to automatically get signed in to Shmoop For Schools with their Azure AD accounts.</span></span>
- <span data-ttu-id="d240a-108">You can manage your accounts in one central location--the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d240a-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="d240a-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d240a-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d240a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d240a-110">Prerequisites</span></span>

<span data-ttu-id="d240a-111">To configure Azure AD integration with Shmoop For Schools, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d240a-111">To configure Azure AD integration with Shmoop For Schools, you need the following items:</span></span>

- <span data-ttu-id="d240a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d240a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d240a-113">A Shmoop For Schools single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d240a-113">A Shmoop For Schools single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d240a-114">We don't recommend using a production environment to test the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d240a-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="d240a-115">To test the steps in this tutorial, we recommend:</span><span class="sxs-lookup"><span data-stu-id="d240a-115">To test the steps in this tutorial, we recommend:</span></span>

- <span data-ttu-id="d240a-116">Using your production evironment only if it's necessary.</span><span class="sxs-lookup"><span data-stu-id="d240a-116">Using your production evironment only if it's necessary.</span></span>
- <span data-ttu-id="d240a-117">Getting a [free one-month trial](https://azure.microsoft.com/pricing/free-trial/) if you don't already have an Azure AD trial environment.</span><span class="sxs-lookup"><span data-stu-id="d240a-117">Getting a [free one-month trial](https://azure.microsoft.com/pricing/free-trial/) if you don't already have an Azure AD trial environment.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d240a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d240a-118">Scenario description</span></span>
<span data-ttu-id="d240a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d240a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d240a-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d240a-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d240a-121">Adding Shmoop For Schools from the gallery</span><span class="sxs-lookup"><span data-stu-id="d240a-121">Adding Shmoop For Schools from the gallery</span></span>
2. <span data-ttu-id="d240a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d240a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-shmoop-for-schools-from-the-gallery"></a><span data-ttu-id="d240a-123">Add Shmoop For Schools from the gallery</span><span class="sxs-lookup"><span data-stu-id="d240a-123">Add Shmoop For Schools from the gallery</span></span>
<span data-ttu-id="d240a-124">To configure the integration of Shmoop For Schools into Azure AD, you need to add Shmoop For Schools from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d240a-124">To configure the integration of Shmoop For Schools into Azure AD, you need to add Shmoop For Schools from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d240a-125">**To add Shmoop For Schools from the gallery, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d240a-125">**To add Shmoop For Schools from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="d240a-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d240a-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="d240a-128">Go to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d240a-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="d240a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d240a-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="d240a-131">To add a new application, select the **New application** button on the top of dialog box.</span><span class="sxs-lookup"><span data-stu-id="d240a-131">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="d240a-133">In the search box, type **Shmoop For Schools**.</span><span class="sxs-lookup"><span data-stu-id="d240a-133">In the search box, type **Shmoop For Schools**.</span></span> <span data-ttu-id="d240a-134">Select **Shmoop For Schools** from the results, then select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d240a-134">Select **Shmoop For Schools** from the results, then select the **Add** button to add the application.</span></span>

    ![Shmoop For Schools in the results list](./media/shmoopforschools-tutorial/tutorial_shmoopforschools_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d240a-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d240a-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d240a-137">In this section, you configure and test Azure AD single sign-on with Shmoop For Schools based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d240a-137">In this section, you configure and test Azure AD single sign-on with Shmoop For Schools based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d240a-138">For single sign-on to work, Azure AD needs to know who the counterpart user in Shmoop For Schools is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d240a-138">For single sign-on to work, Azure AD needs to know who the counterpart user in Shmoop For Schools is to a user in Azure AD.</span></span> <span data-ttu-id="d240a-139">In other words, you need to establish a link between an Azure AD user and the related user in Shmoop For Schools.</span><span class="sxs-lookup"><span data-stu-id="d240a-139">In other words, you need to establish a link between an Azure AD user and the related user in Shmoop For Schools.</span></span>

<span data-ttu-id="d240a-140">To configure and test Azure AD single sign-on with Shmoop For Schools, complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d240a-140">To configure and test Azure AD single sign-on with Shmoop For Schools, complete the following building blocks:</span></span>

1. <span data-ttu-id="d240a-141">[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d240a-141">[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d240a-142">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d240a-142">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d240a-143">[Create a Shmoop For Schools test user](#create-a-shmoop-for-schools-test-user) to have a counterpart of Britta Simon in Shmoop For Schools that is linked to the Azure AD representation of the user.</span><span class="sxs-lookup"><span data-stu-id="d240a-143">[Create a Shmoop For Schools test user](#create-a-shmoop-for-schools-test-user) to have a counterpart of Britta Simon in Shmoop For Schools that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="d240a-144">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d240a-144">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d240a-145">[Test single sign-on](#test-single-sign-on) to verify that the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d240a-145">[Test single sign-on](#test-single-sign-on) to verify that the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d240a-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d240a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d240a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Shmoop For Schools application.</span><span class="sxs-lookup"><span data-stu-id="d240a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Shmoop For Schools application.</span></span>

<span data-ttu-id="d240a-148">**To configure Azure AD single sign-on with Shmoop For Schools, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d240a-148">**To configure Azure AD single sign-on with Shmoop For Schools, perform the following steps:**</span></span>

1. <span data-ttu-id="d240a-149">In the Azure portal, on the **Shmoop For Schools** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d240a-149">In the Azure portal, on the **Shmoop For Schools** application integration page, select **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="d240a-151">In the **Single sign-on** dialog box, in the drop-down menu under **Single Sign-on Mode**, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d240a-151">In the **Single sign-on** dialog box, in the drop-down menu under **Single Sign-on Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Single sign-on dialog box](./media/shmoopforschools-tutorial/tutorial_shmoopforschools_samlbase.png)

3. <span data-ttu-id="d240a-153">In the **Shmoop For Schools Domain and URLs** section, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="d240a-153">In the **Shmoop For Schools Domain and URLs** section, take the following steps:</span></span>

    ![Configure single sign-on](./media/shmoopforschools-tutorial/tutorial_shmoopforschools_url.png)

    <span data-ttu-id="d240a-155">a.</span><span class="sxs-lookup"><span data-stu-id="d240a-155">a.</span></span> <span data-ttu-id="d240a-156">In the **Sign-on URL** box, type a URL with the following pattern: `https://schools.shmoop.com/public-api/saml2/start/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="d240a-156">In the **Sign-on URL** box, type a URL with the following pattern: `https://schools.shmoop.com/public-api/saml2/start/<uniqueid>`</span></span>

    <span data-ttu-id="d240a-157">b.</span><span class="sxs-lookup"><span data-stu-id="d240a-157">b.</span></span> <span data-ttu-id="d240a-158">In the **Identifier** box, type a URL with the following pattern: `https://schools.shmoop.com/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="d240a-158">In the **Identifier** box, type a URL with the following pattern: `https://schools.shmoop.com/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d240a-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="d240a-159">These values are not real.</span></span> <span data-ttu-id="d240a-160">Update these values with the actual sign-on URL and identifier.</span><span class="sxs-lookup"><span data-stu-id="d240a-160">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="d240a-161">Contact the [Shmoop For Schools Client support team](mailto:support@shmoop.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="d240a-161">Contact the [Shmoop For Schools Client support team](mailto:support@shmoop.com) to get these values.</span></span> 
 
4. <span data-ttu-id="d240a-162">The Shmoop For Schools application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="d240a-162">The Shmoop For Schools application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d240a-163">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="d240a-163">Configure the following claims for this application.</span></span> <span data-ttu-id="d240a-164">You can manage the values of these attributes from the **User Attributes** section on the application integration page.</span><span class="sxs-lookup"><span data-stu-id="d240a-164">You can manage the values of these attributes from the **User Attributes** section on the application integration page.</span></span> <span data-ttu-id="d240a-165">The following screenshot shows how to configure the assertions:</span><span class="sxs-lookup"><span data-stu-id="d240a-165">The following screenshot shows how to configure the assertions:</span></span>

    ![Configure single sign-on](./media/shmoopforschools-tutorial/tutorial_attribute.png)

    > [!NOTE]
    > <span data-ttu-id="d240a-167">Shmoop for School supports two roles for users: **Teacher** and **Student**.</span><span class="sxs-lookup"><span data-stu-id="d240a-167">Shmoop for School supports two roles for users: **Teacher** and **Student**.</span></span> <span data-ttu-id="d240a-168">Set up these roles in Azure AD so that users can be assigned the appropriate roles.</span><span class="sxs-lookup"><span data-stu-id="d240a-168">Set up these roles in Azure AD so that users can be assigned the appropriate roles.</span></span> <span data-ttu-id="d240a-169">To understand how to configure roles in Azure AD, see [Manage access using RBAC and the Azure portal](../../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d240a-169">To understand how to configure roles in Azure AD, see [Manage access using RBAC and the Azure portal](../../role-based-access-control/role-assignments-portal.md).</span></span>
    
5. <span data-ttu-id="d240a-170">In the **User Attributes** section in the **Single sign-on** dialog box, configure the SAML token attribute as shown in the previous image.</span><span class="sxs-lookup"><span data-stu-id="d240a-170">In the **User Attributes** section in the **Single sign-on** dialog box, configure the SAML token attribute as shown in the previous image.</span></span>  <span data-ttu-id="d240a-171">Then take the following steps:</span><span class="sxs-lookup"><span data-stu-id="d240a-171">Then take the following steps:</span></span>

    | <span data-ttu-id="d240a-172">Attribute name</span><span class="sxs-lookup"><span data-stu-id="d240a-172">Attribute name</span></span> | <span data-ttu-id="d240a-173">Attribute value</span><span class="sxs-lookup"><span data-stu-id="d240a-173">Attribute value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="d240a-174">role</span><span class="sxs-lookup"><span data-stu-id="d240a-174">role</span></span>           | <span data-ttu-id="d240a-175">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="d240a-175">user.assignedroles</span></span> |

    <span data-ttu-id="d240a-176">a.</span><span class="sxs-lookup"><span data-stu-id="d240a-176">a.</span></span> <span data-ttu-id="d240a-177">To open the **Add Attribute** dialog box, select **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="d240a-177">To open the **Add Attribute** dialog box, select **Add attribute**.</span></span>
    
    ![<span data-ttu-id="d240a-178">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="d240a-178">Configure single sign-on</span></span> ](./media/shmoopforschools-tutorial/tutorial_attribute_04.png)
    
    ![Configure single sign-on](./media/shmoopforschools-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="d240a-180">b.</span><span class="sxs-lookup"><span data-stu-id="d240a-180">b.</span></span> <span data-ttu-id="d240a-181">In the **Name** box, type the attribute name that's shown for that row.</span><span class="sxs-lookup"><span data-stu-id="d240a-181">In the **Name** box, type the attribute name that's shown for that row.</span></span>
    
    <span data-ttu-id="d240a-182">c.</span><span class="sxs-lookup"><span data-stu-id="d240a-182">c.</span></span> <span data-ttu-id="d240a-183">From the **Value** list, select the attribute value that's shown for that row.</span><span class="sxs-lookup"><span data-stu-id="d240a-183">From the **Value** list, select the attribute value that's shown for that row.</span></span>

    <span data-ttu-id="d240a-184">d.</span><span class="sxs-lookup"><span data-stu-id="d240a-184">d.</span></span> <span data-ttu-id="d240a-185">Leave the **Namespace** box empty.</span><span class="sxs-lookup"><span data-stu-id="d240a-185">Leave the **Namespace** box empty.</span></span>
    
    <span data-ttu-id="d240a-186">e.</span><span class="sxs-lookup"><span data-stu-id="d240a-186">e.</span></span> <span data-ttu-id="d240a-187">Select **Ok**.</span><span class="sxs-lookup"><span data-stu-id="d240a-187">Select **Ok**.</span></span>

6. <span data-ttu-id="d240a-188">Select the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d240a-188">Select the **Save** button.</span></span>

    ![Configure single sign-on](./media/shmoopforschools-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d240a-190">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="d240a-190">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/shmoopforschools-tutorial/tutorial_shmoopforschools_certificate.png)

8. <span data-ttu-id="d240a-192">To configure single sign-on on the **Shmoop For Schools** side, you need to send the **App Federation Metadata Url** to the [Shmoop For Schools support team](mailto:support@shmoop.com).</span><span class="sxs-lookup"><span data-stu-id="d240a-192">To configure single sign-on on the **Shmoop For Schools** side, you need to send the **App Federation Metadata Url** to the [Shmoop For Schools support team](mailto:support@shmoop.com).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d240a-193">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d240a-193">Create an Azure AD test user</span></span>

<span data-ttu-id="d240a-194">The objective of this section is to create a test user called Britta Simon in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d240a-194">The objective of this section is to create a test user called Britta Simon in the Azure portal.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="d240a-196">**To create a test user in Azure AD, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d240a-196">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="d240a-197">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="d240a-197">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/shmoopforschools-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d240a-199">To display the list of users, go to **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d240a-199">To display the list of users, go to **Users and groups**.</span></span> <span data-ttu-id="d240a-200">Then select **All users**.</span><span class="sxs-lookup"><span data-stu-id="d240a-200">Then select **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/shmoopforschools-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d240a-202">To open the **User** dialog box, select **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d240a-202">To open the **User** dialog box, select **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/shmoopforschools-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d240a-204">In the **User** dialog box, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="d240a-204">In the **User** dialog box, take the following steps:</span></span>

    ![The User dialog box](./media/shmoopforschools-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d240a-206">a.</span><span class="sxs-lookup"><span data-stu-id="d240a-206">a.</span></span> <span data-ttu-id="d240a-207">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d240a-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d240a-208">b.</span><span class="sxs-lookup"><span data-stu-id="d240a-208">b.</span></span> <span data-ttu-id="d240a-209">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d240a-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d240a-210">c.</span><span class="sxs-lookup"><span data-stu-id="d240a-210">c.</span></span> <span data-ttu-id="d240a-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="d240a-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d240a-212">d.</span><span class="sxs-lookup"><span data-stu-id="d240a-212">d.</span></span> <span data-ttu-id="d240a-213">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d240a-213">Select **Create**.</span></span>
 
### <a name="create-a-shmoop-for-schools-test-user"></a><span data-ttu-id="d240a-214">Create a Shmoop For Schools test user</span><span class="sxs-lookup"><span data-stu-id="d240a-214">Create a Shmoop For Schools test user</span></span>

<span data-ttu-id="d240a-215">The objective of this section is to create a user called Britta Simon in Shmoop For Schools.</span><span class="sxs-lookup"><span data-stu-id="d240a-215">The objective of this section is to create a user called Britta Simon in Shmoop For Schools.</span></span> <span data-ttu-id="d240a-216">Shmoop For Schools supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="d240a-216">Shmoop For Schools supports just-in-time provisioning, which is enabled by default.</span></span> <span data-ttu-id="d240a-217">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="d240a-217">There is no action item for you in this section.</span></span> <span data-ttu-id="d240a-218">If a new user doesn't yet exist, it is created during the attempt to access Shmoop For Schools.</span><span class="sxs-lookup"><span data-stu-id="d240a-218">If a new user doesn't yet exist, it is created during the attempt to access Shmoop For Schools.</span></span>

>[!NOTE]
><span data-ttu-id="d240a-219">If you need to create a user manually, contact the [Shmoop For Schools support team](mailto:support@shmoop.com).</span><span class="sxs-lookup"><span data-stu-id="d240a-219">If you need to create a user manually, contact the [Shmoop For Schools support team](mailto:support@shmoop.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d240a-220">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d240a-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="d240a-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Shmoop For Schools.</span><span class="sxs-lookup"><span data-stu-id="d240a-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Shmoop For Schools.</span></span>

![Assign the user role][200] 

<span data-ttu-id="d240a-223">**To assign Britta Simon to Shmoop For Schools, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d240a-223">**To assign Britta Simon to Shmoop For Schools, take the following steps:**</span></span>

1. <span data-ttu-id="d240a-224">In the Azure portal, open the applications view.</span><span class="sxs-lookup"><span data-stu-id="d240a-224">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="d240a-225">Then go to **Enterprise applications** in the directory view.</span><span class="sxs-lookup"><span data-stu-id="d240a-225">Then go to **Enterprise applications** in the directory view.</span></span>  <span data-ttu-id="d240a-226">Next, select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d240a-226">Next, select **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="d240a-228">In the applications list, select **Shmoop For Schools**.</span><span class="sxs-lookup"><span data-stu-id="d240a-228">In the applications list, select **Shmoop For Schools**.</span></span>

    ![The Shmoop For Schools link in the applications list](./media/shmoopforschools-tutorial/tutorial_shmoopforschools_app.png)  

3. <span data-ttu-id="d240a-230">In the menu on the left, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d240a-230">In the menu on the left, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="d240a-232">Select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d240a-232">Select the **Add** button.</span></span> <span data-ttu-id="d240a-233">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d240a-233">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="d240a-235">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span><span class="sxs-lookup"><span data-stu-id="d240a-235">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="d240a-236">In the **Users and groups** dialog box, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="d240a-236">In the **Users and groups** dialog box, click the **Select** button.</span></span> 

7. <span data-ttu-id="d240a-237">In the **Add Assignment** dialog box, select the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="d240a-237">In the **Add Assignment** dialog box, select the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d240a-238">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d240a-238">Test single sign-on</span></span>

<span data-ttu-id="d240a-239">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d240a-239">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="d240a-240">When you select the **Shmoop For Schools** tile in the Access Panel, you should get automatically signed in to your Shmoop For Schools application.</span><span class="sxs-lookup"><span data-stu-id="d240a-240">When you select the **Shmoop For Schools** tile in the Access Panel, you should get automatically signed in to your Shmoop For Schools application.</span></span>

<span data-ttu-id="d240a-241">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d240a-241">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d240a-242">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d240a-242">Additional resources</span></span>

* [<span data-ttu-id="d240a-243">List of tutorials for how to integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d240a-243">List of tutorials for how to integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d240a-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d240a-244">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/shmoopforschools-tutorial/tutorial_general_01.png
[2]: ./media/shmoopforschools-tutorial/tutorial_general_02.png
[3]: ./media/shmoopforschools-tutorial/tutorial_general_03.png
[4]: ./media/shmoopforschools-tutorial/tutorial_general_04.png

[100]: ./media/shmoopforschools-tutorial/tutorial_general_100.png

[200]: ./media/shmoopforschools-tutorial/tutorial_general_200.png
[201]: ./media/shmoopforschools-tutorial/tutorial_general_201.png
[202]: ./media/shmoopforschools-tutorial/tutorial_general_202.png
[203]: ./media/shmoopforschools-tutorial/tutorial_general_203.png

