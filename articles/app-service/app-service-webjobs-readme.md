---
title: WebJobs in Azure App Service
description: Learn how to build WebJobs to run background tests, interact with services like Storage and Service Bus, and create scheduled tasks.
services: app-service
documentationcenter: ''
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551295"
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="24dcd-103">Using WebJobs in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="24dcd-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="24dcd-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="24dcd-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span></span> <span data-ttu-id="24dcd-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="24dcd-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="24dcd-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span><span class="sxs-lookup"><span data-stu-id="24dcd-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="24dcd-107">These programs run as WebJobs on a schedule (cron) or continuously.</span><span class="sxs-lookup"><span data-stu-id="24dcd-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="24dcd-108">The WebJobs SDK makes it easier to use Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24dcd-108">The WebJobs SDK makes it easier to use Azure Storage.</span></span> <span data-ttu-id="24dcd-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span><span class="sxs-lookup"><span data-stu-id="24dcd-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="24dcd-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24dcd-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="24dcd-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span><span class="sxs-lookup"><span data-stu-id="24dcd-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="24dcd-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span><span class="sxs-lookup"><span data-stu-id="24dcd-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span></span> <span data-ttu-id="24dcd-113">The dashboard also displays function runtimes and logging output.</span><span class="sxs-lookup"><span data-stu-id="24dcd-113">The dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

