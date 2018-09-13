---
title: Streaming logs and console
description: Streaming logs and console overview
author: btardif
manager: erikre
editor: ''
services: app-service\web
documentationcenter: ''
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: 4c8536cf83da7f33518957d753f0e0230ef14403
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548863"
---
# <a name="streaming-logs-and-the-console"></a><span data-ttu-id="a94ef-103">Streaming Logs and the Console</span><span class="sxs-lookup"><span data-stu-id="a94ef-103">Streaming Logs and the Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="a94ef-104">Streaming Logs</span><span class="sxs-lookup"><span data-stu-id="a94ef-104">Streaming Logs</span></span>
<span data-ttu-id="a94ef-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span><span class="sxs-lookup"><span data-stu-id="a94ef-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="a94ef-106">Setting up this feature requires a few simple steps:</span><span class="sxs-lookup"><span data-stu-id="a94ef-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="a94ef-107">Write traces in your code</span><span class="sxs-lookup"><span data-stu-id="a94ef-107">Write traces in your code</span></span>
* <span data-ttu-id="a94ef-108">Enable Application **Diagnostic Logs** for your app</span><span class="sxs-lookup"><span data-stu-id="a94ef-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="a94ef-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="a94ef-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span></span>

### <a name="how-to-write-traces-in-your-code"></a><span data-ttu-id="a94ef-110">How to write traces in your code</span><span class="sxs-lookup"><span data-stu-id="a94ef-110">How to write traces in your code</span></span>
<span data-ttu-id="a94ef-111">Writing traces in your code is easy.</span><span class="sxs-lookup"><span data-stu-id="a94ef-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="a94ef-112">In C# it's as easy as writing the following code:</span><span class="sxs-lookup"><span data-stu-id="a94ef-112">In C# it's as easy as writing the following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="a94ef-113">The Trace class lives in the System.Diagnostics namespace.</span><span class="sxs-lookup"><span data-stu-id="a94ef-113">The Trace class lives in the System.Diagnostics namespace.</span></span>

<span data-ttu-id="a94ef-114">In a node.js app you can write this code to achieve the same result:</span><span class="sxs-lookup"><span data-stu-id="a94ef-114">In a node.js app you can write this code to achieve the same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a><span data-ttu-id="a94ef-115">How to enable and view the streaming logs</span><span class="sxs-lookup"><span data-stu-id="a94ef-115">How to enable and view the streaming logs</span></span>
<span data-ttu-id="a94ef-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span><span class="sxs-lookup"><span data-stu-id="a94ef-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="a94ef-117">Start by browsing to the site you would like to enable this feature on.</span><span class="sxs-lookup"><span data-stu-id="a94ef-117">Start by browsing to the site you would like to enable this feature on.</span></span>  

<span data-ttu-id="a94ef-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span><span class="sxs-lookup"><span data-stu-id="a94ef-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="a94ef-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span><span class="sxs-lookup"><span data-stu-id="a94ef-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span></span> <span data-ttu-id="a94ef-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span><span class="sxs-lookup"><span data-stu-id="a94ef-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span></span>

<span data-ttu-id="a94ef-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span><span class="sxs-lookup"><span data-stu-id="a94ef-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span></span>

> [!NOTE]
> <span data-ttu-id="a94ef-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span><span class="sxs-lookup"><span data-stu-id="a94ef-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span></span> <span data-ttu-id="a94ef-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span><span class="sxs-lookup"><span data-stu-id="a94ef-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="a94ef-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span><span class="sxs-lookup"><span data-stu-id="a94ef-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span></span> <span data-ttu-id="a94ef-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span><span class="sxs-lookup"><span data-stu-id="a94ef-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="a94ef-126">Console</span><span class="sxs-lookup"><span data-stu-id="a94ef-126">Console</span></span>
<span data-ttu-id="a94ef-127">The **Azure portal** provides console access to your app.</span><span class="sxs-lookup"><span data-stu-id="a94ef-127">The **Azure portal** provides console access to your app.</span></span> <span data-ttu-id="a94ef-128">You can explore your app's file system and run powershell/cmd scripts.</span><span class="sxs-lookup"><span data-stu-id="a94ef-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="a94ef-129">You are bound by the same permissions set as your running app code when executing console commands.</span><span class="sxs-lookup"><span data-stu-id="a94ef-129">You are bound by the same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="a94ef-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span><span class="sxs-lookup"><span data-stu-id="a94ef-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="a94ef-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span><span class="sxs-lookup"><span data-stu-id="a94ef-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span></span>

<span data-ttu-id="a94ef-132">To get familiar with the **console**, try basic commands like:</span><span class="sxs-lookup"><span data-stu-id="a94ef-132">To get familiar with the **console**, try basic commands like:</span></span>

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-streaming-logs-and-console/console.png




