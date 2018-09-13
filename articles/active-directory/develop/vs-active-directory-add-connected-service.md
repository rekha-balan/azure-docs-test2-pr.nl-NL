---
title: Adding an Azure Active Directory by using Connected Services in Visual Studio
description: Add an Azure Active Directory by using the Visual Studio Add Connected Services dialog box
services: active-directory
author: ghogen
manager: douge
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.devlang: multiple
ms.topic: conceptual
ms.date: 03/12/2018
ms.author: ghogen
ms.openlocfilehash: 2e446bad042965e8466e74b9b1abd8661ea88f8b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857580"
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a><span data-ttu-id="c4068-103">Adding an Azure Active Directory by using Connected Services in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4068-103">Adding an Azure Active Directory by using Connected Services in Visual Studio</span></span>

<span data-ttu-id="c4068-104">By using Azure Active Directory (Azure AD), you can support Single Sign-On (SSO) for ASP.NET MVC web applications, or Active Directory Authentication in Web API services.</span><span class="sxs-lookup"><span data-stu-id="c4068-104">By using Azure Active Directory (Azure AD), you can support Single Sign-On (SSO) for ASP.NET MVC web applications, or Active Directory Authentication in Web API services.</span></span> <span data-ttu-id="c4068-105">With Azure AD Authentication, your users can use their accounts from Azure Active Directory to connect to your web applications.</span><span class="sxs-lookup"><span data-stu-id="c4068-105">With Azure AD Authentication, your users can use their accounts from Azure Active Directory to connect to your web applications.</span></span> <span data-ttu-id="c4068-106">The advantages of Azure AD Authentication with Web API include enhanced data security when exposing an API from a web application.</span><span class="sxs-lookup"><span data-stu-id="c4068-106">The advantages of Azure AD Authentication with Web API include enhanced data security when exposing an API from a web application.</span></span> <span data-ttu-id="c4068-107">With Azure AD, you do not have to manage a separate authentication system with its own account and user management.</span><span class="sxs-lookup"><span data-stu-id="c4068-107">With Azure AD, you do not have to manage a separate authentication system with its own account and user management.</span></span>

<span data-ttu-id="c4068-108">This article and its companion articles provide details of using the Visual Studio Connected Service feature for Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c4068-108">This article and its companion articles provide details of using the Visual Studio Connected Service feature for Active Directory.</span></span> <span data-ttu-id="c4068-109">The capability is available in both Visual Studio 2017 and Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c4068-109">The capability is available in both Visual Studio 2017 and Visual Studio 2015.</span></span>

<span data-ttu-id="c4068-110">At present, the Active Directory connected service does not support ASP.NET Core applications.</span><span class="sxs-lookup"><span data-stu-id="c4068-110">At present, the Active Directory connected service does not support ASP.NET Core applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4068-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c4068-111">Prerequisites</span></span>

- <span data-ttu-id="c4068-112">Azure account: if you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="c4068-112">Azure account: if you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
- <span data-ttu-id="c4068-113">**Visual Studio 2015** or later.</span><span class="sxs-lookup"><span data-stu-id="c4068-113">**Visual Studio 2015** or later.</span></span> <span data-ttu-id="c4068-114">[Download Visual Studio 2017 now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span><span class="sxs-lookup"><span data-stu-id="c4068-114">[Download Visual Studio 2017 now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span></span>

### <a name="connect-to-azure-active-directory-using-the-connected-services-dialog"></a><span data-ttu-id="c4068-115">Connect to Azure Active Directory using the Connected Services dialog</span><span class="sxs-lookup"><span data-stu-id="c4068-115">Connect to Azure Active Directory using the Connected Services dialog</span></span>

1. <span data-ttu-id="c4068-116">In Visual Studio, create or open an ASP.NET MVC project, or an ASP.NET Web API project.</span><span class="sxs-lookup"><span data-stu-id="c4068-116">In Visual Studio, create or open an ASP.NET MVC project, or an ASP.NET Web API project.</span></span> <span data-ttu-id="c4068-117">You can use the MVC, Web API, Single Page Application, Azure API App, Azure Mobile App, and Azure Mobile Service templates.</span><span class="sxs-lookup"><span data-stu-id="c4068-117">You can use the MVC, Web API, Single Page Application, Azure API App, Azure Mobile App, and Azure Mobile Service templates.</span></span>

1. <span data-ttu-id="c4068-118">Select the **Project > Add Connected Service...** menu command, or double-click the **Connected Services** node found under the project in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="c4068-118">Select the **Project > Add Connected Service...** menu command, or double-click the **Connected Services** node found under the project in Solution Explorer.</span></span>

1. <span data-ttu-id="c4068-119">On the **Connected Services** page, select **Authentication with Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4068-119">On the **Connected Services** page, select **Authentication with Azure Active Directory**.</span></span>

    ![Connected Services page](./media/vs-azure-active-directory/connected-services-add-active-directory.png)

1. <span data-ttu-id="c4068-121">On the **Introduction** page, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="c4068-121">On the **Introduction** page, select **Next**.</span></span> <span data-ttu-id="c4068-122">If you see errors on this page, refer to [Diagnosing errors with the Azure Active Directory Connected Service](vs-active-directory-error.md).</span><span class="sxs-lookup"><span data-stu-id="c4068-122">If you see errors on this page, refer to [Diagnosing errors with the Azure Active Directory Connected Service](vs-active-directory-error.md).</span></span>

    ![Introduction page](./media/vs-azure-active-directory/configure-azure-ad-wizard-1.png)

1. <span data-ttu-id="c4068-124">On the **Single-Sign On** page, select a domain from the **Domain** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="c4068-124">On the **Single-Sign On** page, select a domain from the **Domain** drop-down list.</span></span> <span data-ttu-id="c4068-125">The list contains all domains accessible by the accounts listed in the Account Settings dialog of Visual Studio (**File > Account Settings...**). As an alternative, you can enter a domain name if you don’t find the one you’re looking for, such as `mydomain.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="c4068-125">The list contains all domains accessible by the accounts listed in the Account Settings dialog of Visual Studio (**File > Account Settings...**). As an alternative, you can enter a domain name if you don’t find the one you’re looking for, such as `mydomain.onmicrosoft.com`.</span></span> <span data-ttu-id="c4068-126">You can choose the option to create an Azure Active Directory app or use the settings from an existing Azure Active Directory app.</span><span class="sxs-lookup"><span data-stu-id="c4068-126">You can choose the option to create an Azure Active Directory app or use the settings from an existing Azure Active Directory app.</span></span> <span data-ttu-id="c4068-127">Select **Next** when done.</span><span class="sxs-lookup"><span data-stu-id="c4068-127">Select **Next** when done.</span></span>

    ![Single-sign on page](./media/vs-azure-active-directory/configure-azure-ad-wizard-2.png)

1. <span data-ttu-id="c4068-129">On the **Directory Access** page, select the **Read directory data** option as desired.</span><span class="sxs-lookup"><span data-stu-id="c4068-129">On the **Directory Access** page, select the **Read directory data** option as desired.</span></span> <span data-ttu-id="c4068-130">Developers typically include this option.</span><span class="sxs-lookup"><span data-stu-id="c4068-130">Developers typically include this option.</span></span>

    ![Directory access page](./media/vs-azure-active-directory/configure-azure-ad-wizard-3.png)

1. <span data-ttu-id="c4068-132">Select **Finish** to start modifications to your project to enable Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="c4068-132">Select **Finish** to start modifications to your project to enable Azure AD authentication.</span></span> <span data-ttu-id="c4068-133">Visual Studio shows progress during this time:</span><span class="sxs-lookup"><span data-stu-id="c4068-133">Visual Studio shows progress during this time:</span></span>

    ![Active Directory connected service progress](./media/vs-azure-active-directory/active-directory-connected-service-output.png)

1. <span data-ttu-id="c4068-135">When the process is complete, Visual Studio opens your browser to one of the following articles, as appropriate to your project type:</span><span class="sxs-lookup"><span data-stu-id="c4068-135">When the process is complete, Visual Studio opens your browser to one of the following articles, as appropriate to your project type:</span></span>

    - [<span data-ttu-id="c4068-136">Get started with .NET MVC projects</span><span class="sxs-lookup"><span data-stu-id="c4068-136">Get started with .NET MVC projects</span></span>](vs-active-directory-dotnet-getting-started.md)
    - [<span data-ttu-id="c4068-137">Get started with WebAPI projects</span><span class="sxs-lookup"><span data-stu-id="c4068-137">Get started with WebAPI projects</span></span>](vs-active-directory-webapi-getting-started.md)

1. <span data-ttu-id="c4068-138">You can also see the Active Directory domain on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c4068-138">You can also see the Active Directory domain on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

## <a name="how-your-project-is-modified"></a><span data-ttu-id="c4068-139">How your project is modified</span><span class="sxs-lookup"><span data-stu-id="c4068-139">How your project is modified</span></span>

<span data-ttu-id="c4068-140">When you add the connected service the wizard, Visual Studio adds Azure Active Directory and associated references to your project.</span><span class="sxs-lookup"><span data-stu-id="c4068-140">When you add the connected service the wizard, Visual Studio adds Azure Active Directory and associated references to your project.</span></span> <span data-ttu-id="c4068-141">Configuration files and code files in your project are also modified to add support for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4068-141">Configuration files and code files in your project are also modified to add support for Azure AD.</span></span> <span data-ttu-id="c4068-142">The specific modifications that Visual Studio makes depend on the project type.</span><span class="sxs-lookup"><span data-stu-id="c4068-142">The specific modifications that Visual Studio makes depend on the project type.</span></span> <span data-ttu-id="c4068-143">See the following articles for details:</span><span class="sxs-lookup"><span data-stu-id="c4068-143">See the following articles for details:</span></span>

- [<span data-ttu-id="c4068-144">What happened to my .NET MVC project?</span><span class="sxs-lookup"><span data-stu-id="c4068-144">What happened to my .NET MVC project?</span></span>](vs-active-directory-dotnet-what-happened.md)
- [<span data-ttu-id="c4068-145">What happened to my Web API project?</span><span class="sxs-lookup"><span data-stu-id="c4068-145">What happened to my Web API project?</span></span>](vs-active-directory-webapi-what-happened.md)

## <a name="next-steps"></a><span data-ttu-id="c4068-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4068-146">Next steps</span></span>

- [<span data-ttu-id="c4068-147">Authentication scenarios for Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4068-147">Authentication scenarios for Azure Active Directory</span></span>](authentication-scenarios.md)
- [<span data-ttu-id="c4068-148">Add sign-in with Microsoft to an ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="c4068-148">Add sign-in with Microsoft to an ASP.NET web app</span></span>](quickstart-v1-aspnet-webapp.md)
