---
title: Default TEMP folder size is too small for a role | Microsoft Docs
description: A cloud service role has a limited amount of space for the TEMP folder. This article provides some suggestions on how to avoid running out of space.
services: cloud-services
documentationcenter: ''
author: simonxjx
manager: felixwu
editor: ''
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 4/6/2017
ms.author: v-six
ms.openlocfilehash: 715498701adb3e949d77a1a85061a00101814ce6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661582"
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="5eb1a-104">Default TEMP folder size is too small on a cloud service web/worker role</span><span class="sxs-lookup"><span data-stu-id="5eb1a-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="5eb1a-105">The default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span><span class="sxs-lookup"><span data-stu-id="5eb1a-105">The default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="5eb1a-106">This article describes how to avoid running out of space for the temporary directory.</span><span class="sxs-lookup"><span data-stu-id="5eb1a-106">This article describes how to avoid running out of space for the temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="5eb1a-107">Why do I run out of space?</span><span class="sxs-lookup"><span data-stu-id="5eb1a-107">Why do I run out of space?</span></span>
<span data-ttu-id="5eb1a-108">The standard Windows environment variables TEMP and TMP are available to code that is running in your application.</span><span class="sxs-lookup"><span data-stu-id="5eb1a-108">The standard Windows environment variables TEMP and TMP are available to code that is running in your application.</span></span> <span data-ttu-id="5eb1a-109">Both TEMP and TMP point to a single directory that has a maximum size of 100 MB.</span><span class="sxs-lookup"><span data-stu-id="5eb1a-109">Both TEMP and TMP point to a single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="5eb1a-110">Any data that is stored in this directory is not persisted across the lifecycle of the cloud service; if the role instances in a cloud service are recycled, the directory is cleaned.</span><span class="sxs-lookup"><span data-stu-id="5eb1a-110">Any data that is stored in this directory is not persisted across the lifecycle of the cloud service; if the role instances in a cloud service are recycled, the directory is cleaned.</span></span>

## <a name="suggestion-to-fix-the-problem"></a><span data-ttu-id="5eb1a-111">Suggestion to fix the problem</span><span class="sxs-lookup"><span data-stu-id="5eb1a-111">Suggestion to fix the problem</span></span>
<span data-ttu-id="5eb1a-112">Implement one of the following alternatives:</span><span class="sxs-lookup"><span data-stu-id="5eb1a-112">Implement one of the following alternatives:</span></span>

* <span data-ttu-id="5eb1a-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span><span class="sxs-lookup"><span data-stu-id="5eb1a-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="5eb1a-114">To access a local storage resource from code that is running within your application, call the [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span><span class="sxs-lookup"><span data-stu-id="5eb1a-114">To access a local storage resource from code that is running within your application, call the [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="5eb1a-115">Configure a local storage resource, and point the TEMP and TMP directories to point to the path of the local storage resource.</span><span class="sxs-lookup"><span data-stu-id="5eb1a-115">Configure a local storage resource, and point the TEMP and TMP directories to point to the path of the local storage resource.</span></span> <span data-ttu-id="5eb1a-116">This modification should be performed within the [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span><span class="sxs-lookup"><span data-stu-id="5eb1a-116">This modification should be performed within the [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="5eb1a-117">The following code example shows how to modify the target directories for TEMP and TMP from within the OnStart method:</span><span class="sxs-lookup"><span data-stu-id="5eb1a-117">The following code example shows how to modify the target directories for TEMP and TMP from within the OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // The local resource declaration must have been added to the
            // service definition file for the role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // The rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="5eb1a-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="5eb1a-118">Next steps</span></span>
<span data-ttu-id="5eb1a-119">Read a blog that describes [How to increase the size of the Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="5eb1a-119">Read a blog that describes [How to increase the size of the Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="5eb1a-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span><span class="sxs-lookup"><span data-stu-id="5eb1a-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="5eb1a-121">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="5eb1a-121">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
