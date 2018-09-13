---
title: Adding an Azure Active Directory by using Connected Services in Visual Studio | Microsoft Docs
description: Add an Azure Active Directory by using the Visual Studio Add Connected Services dialog box
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: tarcher
ms.openlocfilehash: 590442f462a9204860914edb6a70ab86d755c07e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554812"
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a><span data-ttu-id="f9557-103">Adding an Azure Active Directory by using Connected Services in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f9557-103">Adding an Azure Active Directory by using Connected Services in Visual Studio</span></span>
<span data-ttu-id="f9557-104">By using Azure Active Directory (Azure AD), you can support Single Sign-On (SSO) for ASP.NET MVC web applications, or Active Directory Authentication in Web API services.</span><span class="sxs-lookup"><span data-stu-id="f9557-104">By using Azure Active Directory (Azure AD), you can support Single Sign-On (SSO) for ASP.NET MVC web applications, or Active Directory Authentication in Web API services.</span></span> <span data-ttu-id="f9557-105">With Azure Active Directory Authentication, your users can use their accounts from Azure Active Directory to connect to your web applications.</span><span class="sxs-lookup"><span data-stu-id="f9557-105">With Azure Active Directory Authentication, your users can use their accounts from Azure Active Directory to connect to your web applications.</span></span> <span data-ttu-id="f9557-106">The advantages of Azure Active Directory Authentication with Web API include enhanced data security when exposing an API from a web application.</span><span class="sxs-lookup"><span data-stu-id="f9557-106">The advantages of Azure Active Directory Authentication with Web API include enhanced data security when exposing an API from a web application.</span></span> <span data-ttu-id="f9557-107">With Azure AD, you do not have to manage a separate authentication system with its own account and user management.</span><span class="sxs-lookup"><span data-stu-id="f9557-107">With Azure AD, you do not have to manage a separate authentication system with its own account and user management.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9557-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f9557-108">Prerequisites</span></span>
- <span data-ttu-id="f9557-109">Azure account - If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="f9557-109">Azure account - If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

### <a name="connect-to-azure-active-directory-using-the-connected-services-dialog"></a><span data-ttu-id="f9557-110">Connect to Azure Active Directory using the Connected Services dialog</span><span class="sxs-lookup"><span data-stu-id="f9557-110">Connect to Azure Active Directory using the Connected Services dialog</span></span>
1. <span data-ttu-id="f9557-111">In Visual Studio, create or open an ASP.NET MVC project, or an ASP.NET Web API project.</span><span class="sxs-lookup"><span data-stu-id="f9557-111">In Visual Studio, create or open an ASP.NET MVC project, or an ASP.NET Web API project.</span></span>

1. <span data-ttu-id="f9557-112">From the Solution Explorer, right-click the **Connected Services** node, and, from the context menu, select **Add Connected Services**.</span><span class="sxs-lookup"><span data-stu-id="f9557-112">From the Solution Explorer, right-click the **Connected Services** node, and, from the context menu, select **Add Connected Services**.</span></span>

1. <span data-ttu-id="f9557-113">On the **Connected Services** page, select **Authentication with Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9557-113">On the **Connected Services** page, select **Authentication with Azure Active Directory**.</span></span>
   
    ![Connected Services page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. <span data-ttu-id="f9557-115">On the **Introduction** page of the **Configure Azure AD Authentication** wizard, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f9557-115">On the **Introduction** page of the **Configure Azure AD Authentication** wizard, select **Next**.</span></span>
   
    ![Introduction page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. <span data-ttu-id="f9557-117">On the **Single-Sign On** page of the **Configure Azure AD Authentication** wizard, select a domain from the **Domain** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f9557-117">On the **Single-Sign On** page of the **Configure Azure AD Authentication** wizard, select a domain from the **Domain** drop-down list.</span></span> <span data-ttu-id="f9557-118">The list of domains contains all domains accessible by the accounts listed in the Account Settings dialog.</span><span class="sxs-lookup"><span data-stu-id="f9557-118">The list of domains contains all domains accessible by the accounts listed in the Account Settings dialog.</span></span> <span data-ttu-id="f9557-119">As an alternative, you can enter a domain name if you don’t find the one you’re looking for, such as `mydomain.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="f9557-119">As an alternative, you can enter a domain name if you don’t find the one you’re looking for, such as `mydomain.onmicrosoft.com`.</span></span> <span data-ttu-id="f9557-120">You can choose the option to create an Azure Active Directory app or use the settings from an existing Azure Active Directory app.</span><span class="sxs-lookup"><span data-stu-id="f9557-120">You can choose the option to create an Azure Active Directory app or use the settings from an existing Azure Active Directory app.</span></span> <span data-ttu-id="f9557-121">Select **Next** when done.</span><span class="sxs-lookup"><span data-stu-id="f9557-121">Select **Next** when done.</span></span>
   
    ![Single-sign on page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. <span data-ttu-id="f9557-123">On the **Directory Access** page of the **Configure Azure AD Authentication** wizard, ensure that the **Read directory data** option is checked.</span><span class="sxs-lookup"><span data-stu-id="f9557-123">On the **Directory Access** page of the **Configure Azure AD Authentication** wizard, ensure that the **Read directory data** option is checked.</span></span> 
   
    ![Directory access page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. <span data-ttu-id="f9557-125">Select **Finish** to add the necessary configuration code and references to enable your project for Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="f9557-125">Select **Finish** to add the necessary configuration code and references to enable your project for Azure AD authentication.</span></span> <span data-ttu-id="f9557-126">You can see the Active Directory domain on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f9557-126">You can see the Active Directory domain on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="f9557-127">Visual Studio will display a [What Happened](#how-your-project-is-modified) article to show you how your project was modified.</span><span class="sxs-lookup"><span data-stu-id="f9557-127">Visual Studio will display a [What Happened](#how-your-project-is-modified) article to show you how your project was modified.</span></span> <span data-ttu-id="f9557-128">If you want to check that everything worked, open one of the modified configuration files and verify that the settings mentioned in the article are there.</span><span class="sxs-lookup"><span data-stu-id="f9557-128">If you want to check that everything worked, open one of the modified configuration files and verify that the settings mentioned in the article are there.</span></span> 

## <a name="how-your-project-is-modified"></a><span data-ttu-id="f9557-129">How your project is modified</span><span class="sxs-lookup"><span data-stu-id="f9557-129">How your project is modified</span></span>
<span data-ttu-id="f9557-130">When you run the wizard, Visual Studio adds Azure Active Directory and associated references to your project.</span><span class="sxs-lookup"><span data-stu-id="f9557-130">When you run the wizard, Visual Studio adds Azure Active Directory and associated references to your project.</span></span> <span data-ttu-id="f9557-131">Configuration files and code files in your project are also modified to add support for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9557-131">Configuration files and code files in your project are also modified to add support for Azure AD.</span></span> <span data-ttu-id="f9557-132">The specific modifications that Visual Studio makes depend on the project type.</span><span class="sxs-lookup"><span data-stu-id="f9557-132">The specific modifications that Visual Studio makes depend on the project type.</span></span> <span data-ttu-id="f9557-133">For detailed information about how ASP.NET MVC projects are modified, see [What happened– MVC Projects](http://go.microsoft.com/fwlink/p/?LinkID=513809).</span><span class="sxs-lookup"><span data-stu-id="f9557-133">For detailed information about how ASP.NET MVC projects are modified, see [What happened– MVC Projects](http://go.microsoft.com/fwlink/p/?LinkID=513809).</span></span> <span data-ttu-id="f9557-134">For Web API projects, see [What happened – Web API Projects](http://go.microsoft.com/fwlink/p/?LinkId=513810).</span><span class="sxs-lookup"><span data-stu-id="f9557-134">For Web API projects, see [What happened – Web API Projects](http://go.microsoft.com/fwlink/p/?LinkId=513810).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9557-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9557-135">Next steps</span></span>
* [<span data-ttu-id="f9557-136">MSDN Forum for Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9557-136">MSDN Forum for Azure Active Directory</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [<span data-ttu-id="f9557-137">Azure Active Directory Documentation</span><span class="sxs-lookup"><span data-stu-id="f9557-137">Azure Active Directory Documentation</span></span>](https://azure.microsoft.com/documentation/services/active-directory/)
* [<span data-ttu-id="f9557-138">Blog Post: Intro to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9557-138">Blog Post: Intro to Azure Active Directory</span></span>](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)





