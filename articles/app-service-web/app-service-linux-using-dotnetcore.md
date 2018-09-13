---
title: Using .NET Core in Azure App Service Web Apps on Linux | Microsoft Docs
description: Using .NET Core in Azure App Service Web Apps on Linux.
keywords: azure app service, web app, dotnet, core, linux, oss
services: app-service
documentationCenter: ''
authors: aelnably
manager: erikre
editor: ''
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 7f5cfc24bc1392237f3992bab540c5a39ac87390
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553424"
---
# <a name="using-net-core-in-web-apps-on-linux"></a><span data-ttu-id="b7d61-104">Using .NET Core in Web Apps on Linux</span><span class="sxs-lookup"><span data-stu-id="b7d61-104">Using .NET Core in Web Apps on Linux</span></span> #

<span data-ttu-id="b7d61-105">With the latest update to our back end, we introduced support for .NET Core v.1.0.</span><span class="sxs-lookup"><span data-stu-id="b7d61-105">With the latest update to our back end, we introduced support for .NET Core v.1.0.</span></span> <span data-ttu-id="b7d61-106">By setting the configuration of your Linux web app, you can change the application stack.</span><span class="sxs-lookup"><span data-stu-id="b7d61-106">By setting the configuration of your Linux web app, you can change the application stack.</span></span>


## <a name="using-xplat-cli"></a><span data-ttu-id="b7d61-107">Using XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="b7d61-107">Using XPlat CLI</span></span> ##

<span data-ttu-id="b7d61-108">Using the latest Azure Cross Platform CLI, you can use the **azure webapp config set** command to change the application stack.</span><span class="sxs-lookup"><span data-stu-id="b7d61-108">Using the latest Azure Cross Platform CLI, you can use the **azure webapp config set** command to change the application stack.</span></span> <span data-ttu-id="b7d61-109">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="b7d61-109">Here is an example:</span></span>

        azure webapp config set --name ContosoAppServicePlan --resource-group ContosoLinuxAzureResourceGroup --netframeworkversion v1.0 --appcommandline aspnetcore.dll

<span data-ttu-id="b7d61-110">Tthe **aspnetcore.dll** file is the dll of your app.</span><span class="sxs-lookup"><span data-stu-id="b7d61-110">Tthe **aspnetcore.dll** file is the dll of your app.</span></span> <span data-ttu-id="b7d61-111">You can use any name you like in your app.</span><span class="sxs-lookup"><span data-stu-id="b7d61-111">You can use any name you like in your app.</span></span>

<span data-ttu-id="b7d61-112">This loads the .Net Core image and starts your web app.</span><span class="sxs-lookup"><span data-stu-id="b7d61-112">This loads the .Net Core image and starts your web app.</span></span> <span data-ttu-id="b7d61-113">You can check that the settings have been correctly set by using the **azure webapp config show**.</span><span class="sxs-lookup"><span data-stu-id="b7d61-113">You can check that the settings have been correctly set by using the **azure webapp config show**.</span></span> <span data-ttu-id="b7d61-114">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="b7d61-114">Here is an example:</span></span>

        azure webapp config show --name ContosoAppServicePlan --resource-group ContosoLinuxAzureResourceGroup

## <a name="next-steps"></a><span data-ttu-id="b7d61-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="b7d61-115">Next steps</span></span>
* [<span data-ttu-id="b7d61-116">What is App Service on Linux?</span><span class="sxs-lookup"><span data-stu-id="b7d61-116">What is App Service on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="b7d61-117">Creating Web Apps in App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="b7d61-117">Creating Web Apps in App Service on Linux</span></span>](./app-service-linux-how-to-create-a-web-app.md)
* [<span data-ttu-id="b7d61-118">Azure Web App Cross Platform CLI</span><span class="sxs-lookup"><span data-stu-id="b7d61-118">Azure Web App Cross Platform CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
* [<span data-ttu-id="b7d61-119">Azure App Service Web Apps on Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="b7d61-119">Azure App Service Web Apps on Linux FAQ</span></span>](app-service-linux-faq.md)