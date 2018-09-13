---
title: 'Tutorial: Azure Active Directory integration with Atlassian Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Atlassian Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 8cbfdd74b5397df22da6c93a1bba39184b37e71b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563129"
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="b7855-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="b7855-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="b7855-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7855-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7855-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b7855-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b7855-106">You can control in Azure AD who has access to Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="b7855-106">You can control in Azure AD who has access to Atlassian Cloud</span></span>
- <span data-ttu-id="b7855-107">You can enable your users to automatically get signed-on to Atlassian Cloud (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="b7855-107">You can enable your users to automatically get signed-on to Atlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b7855-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="b7855-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="b7855-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b7855-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7855-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b7855-110">Prerequisites</span></span>

<span data-ttu-id="b7855-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b7855-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span></span>

- <span data-ttu-id="b7855-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b7855-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7855-113">A Atlassian Cloud single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b7855-113">A Atlassian Cloud single-sign on enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="b7855-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b7855-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7855-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b7855-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7855-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="b7855-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b7855-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7855-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="b7855-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b7855-118">Scenario description</span></span>
<span data-ttu-id="b7855-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b7855-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="b7855-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b7855-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7855-121">Adding Atlassian Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="b7855-121">Adding Atlassian Cloud from the gallery</span></span>
2. <span data-ttu-id="b7855-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="b7855-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-atlassian-cloud-from-the-gallery"></a><span data-ttu-id="b7855-123">Add Atlassian Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="b7855-123">Add Atlassian Cloud from the gallery</span></span>
<span data-ttu-id="b7855-124">To configure the integration of Atlassian Cloud into Azure AD, you need to add Atlassian Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b7855-124">To configure the integration of Atlassian Cloud into Azure AD, you need to add Atlassian Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b7855-125">**To add Atlassian Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7855-125">**To add Atlassian Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b7855-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b7855-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="b7855-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b7855-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="b7855-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b7855-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="b7855-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b7855-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="b7855-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="b7855-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="b7855-135">In the search box, type **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="b7855-135">In the search box, type **Atlassian Cloud**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_01.png)

7. <span data-ttu-id="b7855-137">In the results pane, select **Atlassian Cloud**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="b7855-137">In the results pane, select **Atlassian Cloud**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_02.png)

##  <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="b7855-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="b7855-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="b7855-140">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b7855-140">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b7855-141">For SSO to work, Azure AD needs to know what the counterpart user in Atlassian Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7855-141">For SSO to work, Azure AD needs to know what the counterpart user in Atlassian Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="b7855-142">In other words, a link relationship between an Azure AD user and the related user in Atlassian Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b7855-142">In other words, a link relationship between an Azure AD user and the related user in Atlassian Cloud needs to be established.</span></span>

<span data-ttu-id="b7855-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="b7855-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="b7855-144">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b7855-144">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b7855-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b7855-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b7855-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7855-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7855-147">**[Creating an Atlassian Cloud test user](#creating-Atlassian-cloud-test-user)** - to have a counterpart of Britta Simon in Atlassian Cloud that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="b7855-147">**[Creating an Atlassian Cloud test user](#creating-Atlassian-cloud-test-user)** - to have a counterpart of Britta Simon in Atlassian Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b7855-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b7855-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7855-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b7855-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="b7855-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="b7855-150">Configure Azure AD SSO</span></span>

<span data-ttu-id="b7855-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your Atlassian Cloud application.</span><span class="sxs-lookup"><span data-stu-id="b7855-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your Atlassian Cloud application.</span></span>


<span data-ttu-id="b7855-152">**To configure Azure AD single sign-on with Atlassian Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7855-152">**To configure Azure AD single sign-on with Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="b7855-153">In the classic portal, on the **Atlassian Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="b7855-153">In the classic portal, on the **Atlassian Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="b7855-155">On the **How would you like users to sign on to Atlassian Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b7855-155">On the **How would you like users to sign on to Atlassian Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_03.png) 

3. <span data-ttu-id="b7855-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7855-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_04.png) 
 1. <span data-ttu-id="b7855-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Atlassian Cloud application using the following pattern: `https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="b7855-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Atlassian Cloud application using the following pattern: `https://<instancename>.atlassian.net`</span></span>  
 2. <span data-ttu-id="b7855-160">In the **Identifier** textbox, type the URL with the following pattern: `https://id.atlassian.com/login`</span><span class="sxs-lookup"><span data-stu-id="b7855-160">In the **Identifier** textbox, type the URL with the following pattern: `https://id.atlassian.com/login`</span></span>

    >[!NOTE] 
    ><span data-ttu-id="b7855-161">You can get the exact value of the **Identifier** from the Atlassian Cloud SAML Configuration screen.</span><span class="sxs-lookup"><span data-stu-id="b7855-161">You can get the exact value of the **Identifier** from the Atlassian Cloud SAML Configuration screen.</span></span>
    >

 3. <span data-ttu-id="b7855-162">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b7855-162">click **Next**.</span></span>
 
4. <span data-ttu-id="b7855-163">On the **Configure single sign-on at Atlassian Cloud** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7855-163">On the **Configure single sign-on at Atlassian Cloud** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_05.png)
 1. <span data-ttu-id="b7855-165">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b7855-165">Click **Download certificate**, and then save the file on your computer.</span></span>
 2. <span data-ttu-id="b7855-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b7855-166">Click **Next**.</span></span>

5. <span data-ttu-id="b7855-167">To get SSO configured for your application, login to the Atlassian Portal using the administrator rights.</span><span class="sxs-lookup"><span data-stu-id="b7855-167">To get SSO configured for your application, login to the Atlassian Portal using the administrator rights.</span></span>

6. <span data-ttu-id="b7855-168">In the Authentication section of the left navigation click **Domains**.</span><span class="sxs-lookup"><span data-stu-id="b7855-168">In the Authentication section of the left navigation click **Domains**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)
 1. <span data-ttu-id="b7855-170">In the textbox, type your domain name, and then click **Add domain**.</span><span class="sxs-lookup"><span data-stu-id="b7855-170">In the textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)
 2. <span data-ttu-id="b7855-172">To verify the domain, click **Verify**.</span><span class="sxs-lookup"><span data-stu-id="b7855-172">To verify the domain, click **Verify**.</span></span> 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png) 
  3. <span data-ttu-id="b7855-174">Download the domain verification html file, upload it to the root folder of your domain's website, and then click **Verify domain**.</span><span class="sxs-lookup"><span data-stu-id="b7855-174">Download the domain verification html file, upload it to the root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)
  4. <span data-ttu-id="b7855-176">Once the domain is verified, the value of the **Stauts** field is **Verified**.</span><span class="sxs-lookup"><span data-stu-id="b7855-176">Once the domain is verified, the value of the **Stauts** field is **Verified**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

7. <span data-ttu-id="b7855-178">In the left navigation bar, click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="b7855-178">In the left navigation bar, click **SAML**.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

8. <span data-ttu-id="b7855-180">Create a new SAML Configuration and add the Identity provider configuration.</span><span class="sxs-lookup"><span data-stu-id="b7855-180">Create a new SAML Configuration and add the Identity provider configuration.</span></span>
  1. <span data-ttu-id="b7855-181">Copy the Entity ID value from Azure AD and paste it in the Identity Provider Entity ID field.</span><span class="sxs-lookup"><span data-stu-id="b7855-181">Copy the Entity ID value from Azure AD and paste it in the Identity Provider Entity ID field.</span></span>
  2. <span data-ttu-id="b7855-182">Copy the SAML SSO URL and paste it in the Identity Provider SSO URL box.</span><span class="sxs-lookup"><span data-stu-id="b7855-182">Copy the SAML SSO URL and paste it in the Identity Provider SSO URL box.</span></span>
  3. <span data-ttu-id="b7855-183">Open the downloaded certificate from Azure AD in Notepad and copy the values without the Begin and End lines and paste it in the Public X509 certificate box.</span><span class="sxs-lookup"><span data-stu-id="b7855-183">Open the downloaded certificate from Azure AD in Notepad and copy the values without the Begin and End lines and paste it in the Public X509 certificate box.</span></span>
  4. <span data-ttu-id="b7855-184">Save the settings.</span><span class="sxs-lookup"><span data-stu-id="b7855-184">Save the settings.</span></span>

      ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)
 
9. <span data-ttu-id="b7855-186">Update the Azure AD settings to make sure that you have setup the correct Identifier URL.</span><span class="sxs-lookup"><span data-stu-id="b7855-186">Update the Azure AD settings to make sure that you have setup the correct Identifier URL.</span></span>
  1. <span data-ttu-id="b7855-187">Copy the SP Identity ID from the SAML screen and paste it in Azure AD as the **Identifier** value.</span><span class="sxs-lookup"><span data-stu-id="b7855-187">Copy the SP Identity ID from the SAML screen and paste it in Azure AD as the **Identifier** value.</span></span>
  2. <span data-ttu-id="b7855-188">Sign On URL is the tenant URL of your Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="b7855-188">Sign On URL is the tenant URL of your Atlassian Cloud.</span></span>     

     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
10. <span data-ttu-id="b7855-190">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b7855-190">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="b7855-192">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b7855-192">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b7855-194">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b7855-194">Create an Azure AD test user</span></span>
<span data-ttu-id="b7855-195">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7855-195">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="b7855-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7855-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b7855-198">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b7855-198">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="b7855-200">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b7855-200">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="b7855-201">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b7855-201">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b7855-203">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="b7855-203">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="b7855-205">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7855-205">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="b7855-207">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="b7855-207">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="b7855-208">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7855-208">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="b7855-209">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b7855-209">Click **Next**.</span></span>

6.  <span data-ttu-id="b7855-210">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7855-210">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_06.png) 
   1. <span data-ttu-id="b7855-212">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b7855-212">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="b7855-213">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b7855-213">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="b7855-214">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b7855-214">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="b7855-215">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="b7855-215">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="b7855-216">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b7855-216">Click **Next**.</span></span>

7. <span data-ttu-id="b7855-217">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="b7855-217">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="b7855-219">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7855-219">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="b7855-221">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="b7855-221">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="b7855-222">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b7855-222">Click **Complete**.</span></span>   

### <a name="create-an-atlassian-cloud-test-user"></a><span data-ttu-id="b7855-223">Create an Atlassian Cloud test user</span><span class="sxs-lookup"><span data-stu-id="b7855-223">Create an Atlassian Cloud test user</span></span>

<span data-ttu-id="b7855-224">In this section, you create a user called Britta Simon in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="b7855-224">In this section, you create a user called Britta Simon in Atlassian Cloud.</span></span> <span data-ttu-id="b7855-225">It is important that user should be present in the Atlassian Cloud before doing SSO.</span><span class="sxs-lookup"><span data-stu-id="b7855-225">It is important that user should be present in the Atlassian Cloud before doing SSO.</span></span> 

<span data-ttu-id="b7855-226">Please login to your Atlassian Cloud instance with administrator rights and perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="b7855-226">Please login to your Atlassian Cloud instance with administrator rights and perform the following steps.</span></span>

>[!NOTE] 
><span data-ttu-id="b7855-227">You can also create the luck users by clicking on the **Bulk Create** button in the Users section.</span><span class="sxs-lookup"><span data-stu-id="b7855-227">You can also create the luck users by clicking on the **Bulk Create** button in the Users section.</span></span>

1. <span data-ttu-id="b7855-228">In the Site administration section click on the **Users** button</span><span class="sxs-lookup"><span data-stu-id="b7855-228">In the Site administration section click on the **Users** button</span></span>

    ![Create Atlassian Cloud User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="b7855-230">Click on the **Create User** button to create a user in the Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="b7855-230">Click on the **Create User** button to create a user in the Atlassian Cloud</span></span>

    ![Create Atlassian Cloud User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="b7855-232">Enter the user's Email address, Username and Full Name and assign the application access.</span><span class="sxs-lookup"><span data-stu-id="b7855-232">Enter the user's Email address, Username and Full Name and assign the application access.</span></span> 

    ![Create Atlassian Cloud User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="b7855-234">Click on **Create user** button, this will send the email invitation to the user and after accepting the invitation the user will be active in the system.</span><span class="sxs-lookup"><span data-stu-id="b7855-234">Click on **Create user** button, this will send the email invitation to the user and after accepting the invitation the user will be active in the system.</span></span> 

### <a name="assig-the-azure-ad-test-user"></a><span data-ttu-id="b7855-235">Assig the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b7855-235">Assig the Azure AD test user</span></span>

<span data-ttu-id="b7855-236">In this section, you enable Britta Simon to use Azure SSO by granting her access to Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="b7855-236">In this section, you enable Britta Simon to use Azure SSO by granting her access to Atlassian Cloud.</span></span>

![Assign User][200] 

<span data-ttu-id="b7855-238">**To assign Britta Simon to Atlassian Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7855-238">**To assign Britta Simon to Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="b7855-239">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b7855-239">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="b7855-241">In the applications list, select **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="b7855-241">In the applications list, select **Atlassian Cloud**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_50.png) 

3. <span data-ttu-id="b7855-243">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b7855-243">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203]

4. <span data-ttu-id="b7855-245">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b7855-245">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="b7855-246">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="b7855-246">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="b7855-248">Test Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b7855-248">Test Single Sign-On</span></span>

<span data-ttu-id="b7855-249">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b7855-249">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b7855-250">When you click the Atlassian Cloud tile in the Access Panel, you should get automatically signed-on to your Atlassian Cloud application.</span><span class="sxs-lookup"><span data-stu-id="b7855-250">When you click the Atlassian Cloud tile in the Access Panel, you should get automatically signed-on to your Atlassian Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b7855-251">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b7855-251">Additional resources</span></span>

* [<span data-ttu-id="b7855-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7855-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7855-253">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b7855-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_205.png




































