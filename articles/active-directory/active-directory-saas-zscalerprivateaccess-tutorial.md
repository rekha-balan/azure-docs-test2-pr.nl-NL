---
title: 'Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA) | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zscaler Private Access (ZPA).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 4f4034dc663f481668f23e53d8599b267022f13d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555487"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="42e76-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="42e76-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="42e76-104">In this tutorial, you learn how to integrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42e76-104">In this tutorial, you learn how to integrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42e76-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="42e76-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42e76-106">You can control in Azure AD who has access to Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="42e76-106">You can control in Azure AD who has access to Zscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="42e76-107">You can enable your users to automatically get signed-on to Zscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="42e76-107">You can enable your users to automatically get signed-on to Zscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42e76-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="42e76-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="42e76-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42e76-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42e76-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42e76-110">Prerequisites</span></span>

<span data-ttu-id="42e76-111">To configure Azure AD integration with Zscaler Private Access (ZPA), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="42e76-111">To configure Azure AD integration with Zscaler Private Access (ZPA), you need the following items:</span></span>

- <span data-ttu-id="42e76-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="42e76-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42e76-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="42e76-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="42e76-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="42e76-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="42e76-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="42e76-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42e76-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="42e76-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="42e76-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42e76-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="42e76-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="42e76-118">Scenario description</span></span>
<span data-ttu-id="42e76-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="42e76-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42e76-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="42e76-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42e76-121">Adding Zscaler Private Access (ZPA) from the gallery</span><span class="sxs-lookup"><span data-stu-id="42e76-121">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
2. <span data-ttu-id="42e76-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="42e76-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-the-gallery"></a><span data-ttu-id="42e76-123">Adding Zscaler Private Access (ZPA) from the gallery</span><span class="sxs-lookup"><span data-stu-id="42e76-123">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
<span data-ttu-id="42e76-124">To configure the integration of Zscaler Private Access (ZPA) into Azure AD, you need to add Zscaler Private Access (ZPA) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="42e76-124">To configure the integration of Zscaler Private Access (ZPA) into Azure AD, you need to add Zscaler Private Access (ZPA) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42e76-125">**To add Zscaler Private Access (ZPA) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42e76-125">**To add Zscaler Private Access (ZPA) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42e76-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="42e76-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42e76-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="42e76-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42e76-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="42e76-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="42e76-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="42e76-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="42e76-133">In the search box, type **Zscaler Private Access (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="42e76-133">In the search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="42e76-135">In the results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="42e76-135">In the results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42e76-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="42e76-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42e76-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="42e76-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42e76-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access (ZPA) is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42e76-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access (ZPA) is to a user in Azure AD.</span></span> <span data-ttu-id="42e76-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access (ZPA) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="42e76-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access (ZPA) needs to be established.</span></span>

<span data-ttu-id="42e76-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="42e76-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="42e76-142">To configure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="42e76-142">To configure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42e76-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="42e76-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42e76-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42e76-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42e76-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="42e76-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="42e76-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="42e76-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42e76-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="42e76-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42e76-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="42e76-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42e76-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span><span class="sxs-lookup"><span data-stu-id="42e76-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="42e76-150">**To configure Azure AD single sign-on with Zscaler Private Access (ZPA), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42e76-150">**To configure Azure AD single sign-on with Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="42e76-151">In the Azure Management portal, on the **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="42e76-151">In the Azure Management portal, on the **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="42e76-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="42e76-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="42e76-155">On the **Zscaler Private Access (ZPA) Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="42e76-155">On the **Zscaler Private Access (ZPA) Domain and URLs** section, perform the following steps:</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="42e76-157">a.</span><span class="sxs-lookup"><span data-stu-id="42e76-157">a.</span></span> <span data-ttu-id="42e76-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="42e76-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="42e76-159">b.</span><span class="sxs-lookup"><span data-stu-id="42e76-159">b.</span></span> <span data-ttu-id="42e76-160">In the **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="42e76-160">In the **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42e76-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="42e76-161">Please note that these are not the real values.</span></span> <span data-ttu-id="42e76-162">You have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="42e76-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="42e76-163">Here we suggest you to use the unique value of URL in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="42e76-163">Here we suggest you to use the unique value of URL in the Identifier.</span></span> <span data-ttu-id="42e76-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span><span class="sxs-lookup"><span data-stu-id="42e76-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span></span>

4. <span data-ttu-id="42e76-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="42e76-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)  

5. <span data-ttu-id="42e76-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="42e76-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="42e76-168">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="42e76-168">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="42e76-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="42e76-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="42e76-172">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="42e76-172">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="42e76-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="42e76-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="42e76-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="42e76-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="42e76-177">Navigate to **Administrator** and then click **Idp Configuration**.</span><span class="sxs-lookup"><span data-stu-id="42e76-177">Navigate to **Administrator** and then click **Idp Configuration**.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="42e76-179">In the **Idp Configuration** section, click **Add New IDP Configuration**.</span><span class="sxs-lookup"><span data-stu-id="42e76-179">In the **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="42e76-181">In the **New IDP Configuration** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="42e76-181">In the **New IDP Configuration** section, perform the following steps:</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="42e76-183">a.</span><span class="sxs-lookup"><span data-stu-id="42e76-183">a.</span></span> <span data-ttu-id="42e76-184">Click **Select File** and upload your downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="42e76-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="42e76-185">b.</span><span class="sxs-lookup"><span data-stu-id="42e76-185">b.</span></span> <span data-ttu-id="42e76-186">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="42e76-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42e76-187">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="42e76-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="42e76-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42e76-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="42e76-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42e76-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42e76-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="42e76-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42e76-193">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="42e76-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42e76-195">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="42e76-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42e76-197">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="42e76-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42e76-199">a.</span><span class="sxs-lookup"><span data-stu-id="42e76-199">a.</span></span> <span data-ttu-id="42e76-200">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42e76-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42e76-201">b.</span><span class="sxs-lookup"><span data-stu-id="42e76-201">b.</span></span> <span data-ttu-id="42e76-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="42e76-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42e76-203">c.</span><span class="sxs-lookup"><span data-stu-id="42e76-203">c.</span></span> <span data-ttu-id="42e76-204">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="42e76-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="42e76-205">d.</span><span class="sxs-lookup"><span data-stu-id="42e76-205">d.</span></span> <span data-ttu-id="42e76-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="42e76-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="42e76-207">Creating a Zscaler Private Access (ZPA) test user</span><span class="sxs-lookup"><span data-stu-id="42e76-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="42e76-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="42e76-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="42e76-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to add the users in the Zscaler Private Access (ZPA) platform.</span><span class="sxs-lookup"><span data-stu-id="42e76-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to add the users in the Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="42e76-210">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="42e76-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="42e76-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="42e76-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Zscaler Private Access (ZPA).</span></span>

![Assign User][200] 

<span data-ttu-id="42e76-213">**To assign Britta Simon to Zscaler Private Access (ZPA), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42e76-213">**To assign Britta Simon to Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="42e76-214">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="42e76-214">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="42e76-216">In the applications list, select **Zscaler Private Access (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="42e76-216">In the applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="42e76-218">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="42e76-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="42e76-220">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="42e76-220">Click **Add** button.</span></span> <span data-ttu-id="42e76-221">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="42e76-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="42e76-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="42e76-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42e76-224">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="42e76-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42e76-225">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="42e76-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="42e76-226">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="42e76-226">Testing single sign-on</span></span>

<span data-ttu-id="42e76-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="42e76-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="42e76-228">When you click the Zscaler Private Access (ZPA) tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access (ZPA) application.</span><span class="sxs-lookup"><span data-stu-id="42e76-228">When you click the Zscaler Private Access (ZPA) tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="42e76-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="42e76-229">Additional resources</span></span>

* [<span data-ttu-id="42e76-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42e76-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42e76-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42e76-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png

























