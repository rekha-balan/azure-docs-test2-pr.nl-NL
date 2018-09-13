---
title: Get Started with Azure AD in Visual Studio WebApi projects
description: How to get started using Azure Active Directory in WebApi projects after connecting to or creating an Azure AD using Visual Studio connected services
services: active-directory
author: ghogen
manager: douge
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/12/2018
ms.author: ghogen
ms.custom: aaddev, vs-azure
ms.openlocfilehash: 69f17b366b2480b34873d8fede223715619d0e66
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819200"
---
# <a name="get-started-with-azure-active-directory-webapi-projects"></a><span data-ttu-id="8b824-103">Get Started with Azure Active Directory (WebApi projects)</span><span class="sxs-lookup"><span data-stu-id="8b824-103">Get Started with Azure Active Directory (WebApi projects)</span></span>

> [!div class="op_single_selector"]
> - [Getting Started](vs-active-directory-webapi-getting-started.md)
> - [What Happened](vs-active-directory-webapi-what-happened.md)

<span data-ttu-id="8b824-106">This article provides additional guidance after you've added Active Directory to an ASP.NET WebAPI project through the **Project > Connected Services** command of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b824-106">This article provides additional guidance after you've added Active Directory to an ASP.NET WebAPI project through the **Project > Connected Services** command of Visual Studio.</span></span> <span data-ttu-id="8b824-107">If you've not already added the service to your project, you can do so at any time.</span><span class="sxs-lookup"><span data-stu-id="8b824-107">If you've not already added the service to your project, you can do so at any time.</span></span>

<span data-ttu-id="8b824-108">See [What happened to my WebAPI project?](vs-active-directory-webapi-what-happened.md) for the changes made to your project when adding the connected service.</span><span class="sxs-lookup"><span data-stu-id="8b824-108">See [What happened to my WebAPI project?](vs-active-directory-webapi-what-happened.md) for the changes made to your project when adding the connected service.</span></span>

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="8b824-109">Requiring authentication to access controllers</span><span class="sxs-lookup"><span data-stu-id="8b824-109">Requiring authentication to access controllers</span></span>

<span data-ttu-id="8b824-110">All controllers in your project were adorned with the `[Authorize]` attribute.</span><span class="sxs-lookup"><span data-stu-id="8b824-110">All controllers in your project were adorned with the `[Authorize]` attribute.</span></span> <span data-ttu-id="8b824-111">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span><span class="sxs-lookup"><span data-stu-id="8b824-111">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="8b824-112">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span><span class="sxs-lookup"><span data-stu-id="8b824-112">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="8b824-113">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span><span class="sxs-lookup"><span data-stu-id="8b824-113">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b824-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b824-114">Next steps</span></span>

- [<span data-ttu-id="8b824-115">Authentication scenarios for Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b824-115">Authentication scenarios for Azure Active Directory</span></span>](authentication-scenarios.md)
- [<span data-ttu-id="8b824-116">Add sign-in with Microsoft to an ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="8b824-116">Add sign-in with Microsoft to an ASP.NET web app</span></span>](quickstart-v1-aspnet-webapp.md)
