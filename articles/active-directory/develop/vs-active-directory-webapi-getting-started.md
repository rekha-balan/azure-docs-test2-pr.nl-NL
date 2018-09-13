---
title: Get Started with Azure AD in Visual Studio WebApi projects | Microsoft Docs
description: How to get started using Azure Active Directory in WebApi projects after connecting to or creating an Azure AD using Visual Studio connected services
services: active-directory
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: tarcher
ms.openlocfilehash: 333db54fe01aad42cfcd050995b64f3725b31ae9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556250"
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="f16b8-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span><span class="sxs-lookup"><span data-stu-id="f16b8-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [Getting Started](vs-active-directory-webapi-getting-started.md)
> * [What Happened](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="f16b8-106">Requiring authentication to access controllers</span><span class="sxs-lookup"><span data-stu-id="f16b8-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="f16b8-107">All controllers in your project were adorned with the **Authorize** attribute.</span><span class="sxs-lookup"><span data-stu-id="f16b8-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="f16b8-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span><span class="sxs-lookup"><span data-stu-id="f16b8-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="f16b8-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span><span class="sxs-lookup"><span data-stu-id="f16b8-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="f16b8-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span><span class="sxs-lookup"><span data-stu-id="f16b8-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f16b8-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="f16b8-111">Next steps</span></span>
[<span data-ttu-id="f16b8-112">Learn more about Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f16b8-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

