---
title: Setup emulator express to debug Cloud Services applications in Visual Studio | Microsoft Docs
description: Explains how to install the C++ redistributable to enable Emulator Express in Visual Studio
services: cloud-services
documentationcenter: ''
author: cawa
manager: paulyuk
editor: ''
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: fbb002f888f115e2c1713007102fafe23d952f7b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552469"
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="7ae4c-103">Use Emulator Express to debug Cloud Services application in VS 2017</span><span class="sxs-lookup"><span data-stu-id="7ae4c-103">Use Emulator Express to debug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="7ae4c-104">This article explains how to use Emulator Express to debug Cloud Services applications in VS 2017.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-104">This article explains how to use Emulator Express to debug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="7ae4c-105">Background context</span><span class="sxs-lookup"><span data-stu-id="7ae4c-105">Background context</span></span>
<span data-ttu-id="7ae4c-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="7ae4c-107">This setting is specified in the Cloud Services project properties page.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-107">This setting is specified in the Cloud Services project properties page.</span></span>

![Open project properties][0]

![Emulator express is selected as default][1]

<span data-ttu-id="7ae4c-110">The [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-110">The [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="7ae4c-111">Currently it is not installed with the Azure workload.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-111">Currently it is not installed with the Azure workload.</span></span> <span data-ttu-id="7ae4c-112">Upon F5 gesture to debug a Cloud Services applications, Visual Studio would prompt to install this component and proceed with debugging.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-112">Upon F5 gesture to debug a Cloud Services applications, Visual Studio would prompt to install this component and proceed with debugging.</span></span>

![Prompt for install C++ Redistributable][2]

<span data-ttu-id="7ae4c-114">Click Yes to install C++ Redistributable.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-114">Click Yes to install C++ Redistributable.</span></span>

![Install C++ Redistributable][3]

<span data-ttu-id="7ae4c-116">Press F5 again to launch debugging sessions.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-116">Press F5 again to launch debugging sessions.</span></span>

![Start debugging][4]

![Debugging successful][5]

> <span data-ttu-id="7ae4c-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="7ae4c-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="7ae4c-121">Manual workaround</span><span class="sxs-lookup"><span data-stu-id="7ae4c-121">Manual workaround</span></span>
<span data-ttu-id="7ae4c-122">You can also install the [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span><span class="sxs-lookup"><span data-stu-id="7ae4c-122">You can also install the [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="7ae4c-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="7ae4c-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="7ae4c-124">[vcredist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="7ae4c-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ae4c-125">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7ae4c-125">Next Steps</span></span>
<span data-ttu-id="7ae4c-126">Learn more about using Azure Computer Emulator to debug your Cloud Services applications in Visual Studio: [Using Emulator Express to run and debug a cloud service on a local machine][Using Emulator Express to run and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="7ae4c-126">Learn more about using Azure Computer Emulator to debug your Cloud Services applications in Visual Studio: [Using Emulator Express to run and debug a cloud service on a local machine][Using Emulator Express to run and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-emulator-express-fix/vs-05.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-emulator-express-fix/vs-06.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-emulator-express-fix/vs-01.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-emulator-express-fix/vs-02.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-emulator-express-fix/vs-03.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-emulator-express-fix/vs-04.png






