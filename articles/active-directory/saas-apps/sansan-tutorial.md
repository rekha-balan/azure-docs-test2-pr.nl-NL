---
title: 'Tutorial: Azure Active Directory integration with Sansan | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Sansan.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: cc070f7c4cb201e68c93b0b1337982325df74663
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871365"
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="935bc-103">Tutorial: Azure Active Directory integration with Sansan</span><span class="sxs-lookup"><span data-stu-id="935bc-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="935bc-104">In this tutorial, you learn how to integrate Sansan with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="935bc-104">In this tutorial, you learn how to integrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="935bc-105">Integrating Sansan with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="935bc-105">Integrating Sansan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="935bc-106">You can control in Azure AD who has access to Sansan</span><span class="sxs-lookup"><span data-stu-id="935bc-106">You can control in Azure AD who has access to Sansan</span></span>
- <span data-ttu-id="935bc-107">You can enable your users to automatically get signed-on to Sansan (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="935bc-107">You can enable your users to automatically get signed-on to Sansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="935bc-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="935bc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="935bc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="935bc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="935bc-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="935bc-110">Prerequisites</span></span>

<span data-ttu-id="935bc-111">To configure Azure AD integration with Sansan, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="935bc-111">To configure Azure AD integration with Sansan, you need the following items:</span></span>

- <span data-ttu-id="935bc-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="935bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="935bc-113">A Sansan single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="935bc-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="935bc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="935bc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="935bc-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="935bc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="935bc-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="935bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="935bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="935bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="935bc-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="935bc-118">Scenario description</span></span>
<span data-ttu-id="935bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="935bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="935bc-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="935bc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="935bc-121">Adding Sansan from the gallery</span><span class="sxs-lookup"><span data-stu-id="935bc-121">Adding Sansan from the gallery</span></span>
2. <span data-ttu-id="935bc-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="935bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-the-gallery"></a><span data-ttu-id="935bc-123">Adding Sansan from the gallery</span><span class="sxs-lookup"><span data-stu-id="935bc-123">Adding Sansan from the gallery</span></span>
<span data-ttu-id="935bc-124">To configure the integration of Sansan into Azure AD, you need to add Sansan from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="935bc-124">To configure the integration of Sansan into Azure AD, you need to add Sansan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="935bc-125">**To add Sansan from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="935bc-125">**To add Sansan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="935bc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="935bc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="935bc-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="935bc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="935bc-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="935bc-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="935bc-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="935bc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="935bc-133">In the search box, type **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="935bc-133">In the search box, type **Sansan**.</span></span>

    ![Creating an Azure AD test user](./media/sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="935bc-135">In the results panel, select **Sansan**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="935bc-135">In the results panel, select **Sansan**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="935bc-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="935bc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="935bc-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="935bc-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="935bc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sansan is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="935bc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sansan is to a user in Azure AD.</span></span> <span data-ttu-id="935bc-140">In other words, a link relationship between an Azure AD user and the related user in Sansan needs to be established.</span><span class="sxs-lookup"><span data-stu-id="935bc-140">In other words, a link relationship between an Azure AD user and the related user in Sansan needs to be established.</span></span>

<span data-ttu-id="935bc-141">In Sansan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="935bc-141">In Sansan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="935bc-142">To configure and test Azure AD single sign-on with Sansan, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="935bc-142">To configure and test Azure AD single sign-on with Sansan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="935bc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="935bc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="935bc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="935bc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="935bc-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - to have a counterpart of Britta Simon in Sansan that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="935bc-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - to have a counterpart of Britta Simon in Sansan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="935bc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="935bc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="935bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="935bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="935bc-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="935bc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="935bc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sansan application.</span><span class="sxs-lookup"><span data-stu-id="935bc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="935bc-150">**To configure Azure AD single sign-on with Sansan, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="935bc-150">**To configure Azure AD single sign-on with Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="935bc-151">In the Azure portal, on the **Sansan** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="935bc-151">In the Azure portal, on the **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="935bc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="935bc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="935bc-155">On the **Sansan Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="935bc-155">On the **Sansan Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="935bc-157">In the **Sign-on URL** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="935bc-157">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | <span data-ttu-id="935bc-158">Environment</span><span class="sxs-lookup"><span data-stu-id="935bc-158">Environment</span></span> | <span data-ttu-id="935bc-159">URL</span><span class="sxs-lookup"><span data-stu-id="935bc-159">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="935bc-160">PC web</span><span class="sxs-lookup"><span data-stu-id="935bc-160">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="935bc-161">Native Mobile app</span><span class="sxs-lookup"><span data-stu-id="935bc-161">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="935bc-162">Mobile browser settings</span><span class="sxs-lookup"><span data-stu-id="935bc-162">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    > [!NOTE] 
    > <span data-ttu-id="935bc-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="935bc-163">These values are not real.</span></span> <span data-ttu-id="935bc-164">Update these values with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="935bc-164">Update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="935bc-165">Contact [Sansan Client support team](https://www.sansan.com/form/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="935bc-165">Contact [Sansan Client support team](https://www.sansan.com/form/contact) to get these values.</span></span> 
     
4. <span data-ttu-id="935bc-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="935bc-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="935bc-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="935bc-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="935bc-170">Sansan application expects multiple **Identifiers** and **Reply URLs** to support multiple environments (PC web, Native Mobile app, Mobile browser settings), which can be configured using PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="935bc-170">Sansan application expects multiple **Identifiers** and **Reply URLs** to support multiple environments (PC web, Native Mobile app, Mobile browser settings), which can be configured using PowerShell script.</span></span> <span data-ttu-id="935bc-171">The detailed steps are explained below.</span><span class="sxs-lookup"><span data-stu-id="935bc-171">The detailed steps are explained below.</span></span>

7. <span data-ttu-id="935bc-172">To configure multiple **Identifiers** and **Reply URLs** for Sansan application using PowerShell script, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="935bc-172">To configure multiple **Identifiers** and **Reply URLs** for Sansan application using PowerShell script, perform following steps:</span></span>

    ![Configure Single Sign-On obj](./media/sansan-tutorial/tutorial_sansan_objid.png)  

    <span data-ttu-id="935bc-174">a.</span><span class="sxs-lookup"><span data-stu-id="935bc-174">a.</span></span> <span data-ttu-id="935bc-175">Go to the **Properties** page of **Sansan** application and copy the **Object ID** using **Copy** button and paste it into Notepad.</span><span class="sxs-lookup"><span data-stu-id="935bc-175">Go to the **Properties** page of **Sansan** application and copy the **Object ID** using **Copy** button and paste it into Notepad.</span></span>

    <span data-ttu-id="935bc-176">b.</span><span class="sxs-lookup"><span data-stu-id="935bc-176">b.</span></span> <span data-ttu-id="935bc-177">The **Object ID**, which you have copied from Azure portal will be used as **ServicePrincipalObjectId** in PowerShell script used later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="935bc-177">The **Object ID**, which you have copied from Azure portal will be used as **ServicePrincipalObjectId** in PowerShell script used later in the tutorial.</span></span> 

    <span data-ttu-id="935bc-178">c.</span><span class="sxs-lookup"><span data-stu-id="935bc-178">c.</span></span> <span data-ttu-id="935bc-179">Now open an elevated Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="935bc-179">Now open an elevated Windows PowerShell command prompt.</span></span>
    
    >[!NOTE] 
    > <span data-ttu-id="935bc-180">You need to install the AzureAD module (use the command `Install-Module -Name AzureAD`).</span><span class="sxs-lookup"><span data-stu-id="935bc-180">You need to install the AzureAD module (use the command `Install-Module -Name AzureAD`).</span></span> <span data-ttu-id="935bc-181">If prompted to install a NuGet module or the new Azure Active Directory V2 PowerShell module, type Y and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="935bc-181">If prompted to install a NuGet module or the new Azure Active Directory V2 PowerShell module, type Y and press ENTER.</span></span>

    <span data-ttu-id="935bc-182">d.</span><span class="sxs-lookup"><span data-stu-id="935bc-182">d.</span></span> <span data-ttu-id="935bc-183">Run `Connect-AzureAD` and sign in with a Global Admin user account.</span><span class="sxs-lookup"><span data-stu-id="935bc-183">Run `Connect-AzureAD` and sign in with a Global Admin user account.</span></span>

    <span data-ttu-id="935bc-184">e.</span><span class="sxs-lookup"><span data-stu-id="935bc-184">e.</span></span> <span data-ttu-id="935bc-185">Use the following script to update multiple URLs to an application:</span><span class="sxs-lookup"><span data-stu-id="935bc-185">Use the following script to update multiple URLs to an application:</span></span>

    ```poweshell
     Param(
    [Parameter(Mandatory=$true)][guid]$ServicePrincipalObjectId,
    [Parameter(Mandatory=$false)][string[]]$ReplyUrls,
    [Parameter(Mandatory=$false)][string[]]$IdentifierUrls
    )

    $servicePrincipal = Get-AzureADServicePrincipal -ObjectId $ServicePrincipalObjectId

    if($ReplyUrls.Length)
    {
    echo "Updating Reply urls"
    Set-AzureADServicePrincipal -ObjectId $ServicePrincipalObjectId -ReplyUrls $ReplyUrls
    echo "updated"
    }
    if($IdentifierUrls.Length)
    {
    echo "Updating Identifier urls"
    $applications = Get-AzureADApplication -SearchString $servicePrincipal.AppDisplayName 
    echo "Found Applications =" $applications.Length
    $i = 0;
    do
    {  
    $application = $applications[$i];
    if($application.AppId -eq $servicePrincipal.AppId){
    Set-AzureADApplication -ObjectId $application.ObjectId -IdentifierUris $IdentifierUrls
    $servicePrincipal = Get-AzureADServicePrincipal -ObjectId $ServicePrincipalObjectId
    echo "Updated"
    return;
    }
    $i++;
    }while($i -lt $applications.Length);
    echo "Not able to find the matched application with this service principal"
    }
    ```

8. <span data-ttu-id="935bc-186">After successfull completion of PowerShell script, the result of the script will be like this as shown below and the URL values get updated but they won't get reflected in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="935bc-186">After successfull completion of PowerShell script, the result of the script will be like this as shown below and the URL values get updated but they won't get reflected in Azure portal.</span></span> 

    ![Configure Single Sign-On script](./media/sansan-tutorial/tutorial_sansan_powershell.png)


9. <span data-ttu-id="935bc-188">On the **Sansan Configuration** section, click **Configure Sansan** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="935bc-188">On the **Sansan Configuration** section, click **Configure Sansan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="935bc-189">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="935bc-189">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/sansan-tutorial/tutorial_sansan_configure.png) 

10. <span data-ttu-id="935bc-191">To configure single sign-on on **Sansan** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Sansan support team](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="935bc-191">To configure single sign-on on **Sansan** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="935bc-192">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="935bc-192">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="935bc-193">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span><span class="sxs-lookup"><span data-stu-id="935bc-193">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="935bc-194">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="935bc-194">Creating an Azure AD test user</span></span>

<span data-ttu-id="935bc-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="935bc-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="935bc-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="935bc-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="935bc-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="935bc-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="935bc-200">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="935bc-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="935bc-202">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="935bc-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="935bc-204">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="935bc-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="935bc-206">a.</span><span class="sxs-lookup"><span data-stu-id="935bc-206">a.</span></span> <span data-ttu-id="935bc-207">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="935bc-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="935bc-208">b.</span><span class="sxs-lookup"><span data-stu-id="935bc-208">b.</span></span> <span data-ttu-id="935bc-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="935bc-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="935bc-210">c.</span><span class="sxs-lookup"><span data-stu-id="935bc-210">c.</span></span> <span data-ttu-id="935bc-211">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="935bc-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="935bc-212">d.</span><span class="sxs-lookup"><span data-stu-id="935bc-212">d.</span></span> <span data-ttu-id="935bc-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="935bc-213">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="935bc-214">Creating a Sansan test user</span><span class="sxs-lookup"><span data-stu-id="935bc-214">Creating a Sansan test user</span></span>

<span data-ttu-id="935bc-215">In this section, you create a user called Britta Simon in Sansan.</span><span class="sxs-lookup"><span data-stu-id="935bc-215">In this section, you create a user called Britta Simon in Sansan.</span></span> <span data-ttu-id="935bc-216">Sansan application needs the user to be provisioned in the application before doing SSO.</span><span class="sxs-lookup"><span data-stu-id="935bc-216">Sansan application needs the user to be provisioned in the application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="935bc-217">If you need to create a user manually or batch of users, you need to contact the [Sansan support team](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="935bc-217">If you need to create a user manually or batch of users, you need to contact the [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="935bc-218">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="935bc-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="935bc-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sansan.</span><span class="sxs-lookup"><span data-stu-id="935bc-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sansan.</span></span>

![Assign User][200] 

<span data-ttu-id="935bc-221">**To assign Britta Simon to Sansan, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="935bc-221">**To assign Britta Simon to Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="935bc-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="935bc-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="935bc-224">In the applications list, select **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="935bc-224">In the applications list, select **Sansan**.</span></span>

    ![Configure Single Sign-On](./media/sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="935bc-226">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="935bc-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="935bc-228">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="935bc-228">Click **Add** button.</span></span> <span data-ttu-id="935bc-229">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="935bc-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="935bc-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="935bc-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="935bc-232">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="935bc-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="935bc-233">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="935bc-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="935bc-234">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="935bc-234">Testing single sign-on</span></span>

<span data-ttu-id="935bc-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="935bc-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="935bc-236">When you click the Sansan tile in the Access Panel, you should get automatically signed-on to your Sansan application.</span><span class="sxs-lookup"><span data-stu-id="935bc-236">When you click the Sansan tile in the Access Panel, you should get automatically signed-on to your Sansan application.</span></span>
<span data-ttu-id="935bc-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="935bc-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="935bc-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="935bc-238">Additional resources</span></span>

* [<span data-ttu-id="935bc-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="935bc-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="935bc-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="935bc-240">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/sansan-tutorial/tutorial_general_01.png
[2]: ./media/sansan-tutorial/tutorial_general_02.png
[3]: ./media/sansan-tutorial/tutorial_general_03.png
[4]: ./media/sansan-tutorial/tutorial_general_04.png

[100]: ./media/sansan-tutorial/tutorial_general_100.png

[200]: ./media/sansan-tutorial/tutorial_general_200.png
[201]: ./media/sansan-tutorial/tutorial_general_201.png
[202]: ./media/sansan-tutorial/tutorial_general_202.png
[203]: ./media/sansan-tutorial/tutorial_general_203.png

