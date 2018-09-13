---
title: Azure CLI Samples - Azure SignalR Service | Microsoft Docs
description: Azure CLI Samples - Azure SignalR Service
services: signalr
documentationcenter: signalr
author: sffamily
manager: cfowler
editor: ''
tags: azure-service-management
ms.service: signalr
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: signalr
ms.date: 04/20/2018
ms.author: zhshang
ms.custom: mvc
ms.openlocfilehash: a1ca02a5e058816c133accf3027f0a951db42cf2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857943"
---
# <a name="azure-cli-samples"></a><span data-ttu-id="5fb02-103">Azure CLI Samples</span><span class="sxs-lookup"><span data-stu-id="5fb02-103">Azure CLI Samples</span></span>

<span data-ttu-id="5fb02-104">The following table includes links to bash scripts for the Azure SignalR Service using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5fb02-104">The following table includes links to bash scripts for the Azure SignalR Service using the Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="5fb02-105">**Create**</span><span class="sxs-lookup"><span data-stu-id="5fb02-105">**Create**</span></span>||
| [<span data-ttu-id="5fb02-106">Create a new SignalR Service and resource group</span><span class="sxs-lookup"><span data-stu-id="5fb02-106">Create a new SignalR Service and resource group</span></span>](scripts/signalr-cli-create-service.md) | <span data-ttu-id="5fb02-107">Creates a new Azure SignalR Service resource in a new resource group with a random name.</span><span class="sxs-lookup"><span data-stu-id="5fb02-107">Creates a new Azure SignalR Service resource in a new resource group with a random name.</span></span>  |
|<span data-ttu-id="5fb02-108">**Integrate**</span><span class="sxs-lookup"><span data-stu-id="5fb02-108">**Integrate**</span></span>||
| [<span data-ttu-id="5fb02-109">Create a new SignalR Service and Web App configured to use SignalR</span><span class="sxs-lookup"><span data-stu-id="5fb02-109">Create a new SignalR Service and Web App configured to use SignalR</span></span>](scripts/signalr-cli-create-with-app-service.md) | <span data-ttu-id="5fb02-110">Creates a new Azure SignalR Service resource in a new resource group with a random name.</span><span class="sxs-lookup"><span data-stu-id="5fb02-110">Creates a new Azure SignalR Service resource in a new resource group with a random name.</span></span> <span data-ttu-id="5fb02-111">Also adds a new Web App and App Service plan to host a ASP.NET Core Web App that uses the SignalR Service.</span><span class="sxs-lookup"><span data-stu-id="5fb02-111">Also adds a new Web App and App Service plan to host a ASP.NET Core Web App that uses the SignalR Service.</span></span> <span data-ttu-id="5fb02-112">The web app is configured with an App Setting to connect to the new SignalR service resource.</span><span class="sxs-lookup"><span data-stu-id="5fb02-112">The web app is configured with an App Setting to connect to the new SignalR service resource.</span></span> |
| [<span data-ttu-id="5fb02-113">Create a new SignalR Service and Web App configured to use SignalR, and GitHub OAuth</span><span class="sxs-lookup"><span data-stu-id="5fb02-113">Create a new SignalR Service and Web App configured to use SignalR, and GitHub OAuth</span></span>](scripts/signalr-cli-create-with-app-service-github-oauth.md) | <span data-ttu-id="5fb02-114">Creates a new Azure SignalR Service resource in a new resource group with a random name.</span><span class="sxs-lookup"><span data-stu-id="5fb02-114">Creates a new Azure SignalR Service resource in a new resource group with a random name.</span></span> <span data-ttu-id="5fb02-115">Also adds a new Azure Web App and hosting plan to host a ASP.NET Core Web App that uses the SignalR Service.</span><span class="sxs-lookup"><span data-stu-id="5fb02-115">Also adds a new Azure Web App and hosting plan to host a ASP.NET Core Web App that uses the SignalR Service.</span></span> <span data-ttu-id="5fb02-116">The web app is configured with app settings for the connection string to the new SignalR service resource, and client secrets to support [GitHub authentication](https://developer.github.com/v3/guides/basics-of-authentication/) as demonstrated in the [authentication tutorial](signalr-authenticate-oauth.md).</span><span class="sxs-lookup"><span data-stu-id="5fb02-116">The web app is configured with app settings for the connection string to the new SignalR service resource, and client secrets to support [GitHub authentication](https://developer.github.com/v3/guides/basics-of-authentication/) as demonstrated in the [authentication tutorial](signalr-authenticate-oauth.md).</span></span> <span data-ttu-id="5fb02-117">The web app is also configured to use a local git repository deployment source.</span><span class="sxs-lookup"><span data-stu-id="5fb02-117">The web app is also configured to use a local git repository deployment source.</span></span> |
| | |
