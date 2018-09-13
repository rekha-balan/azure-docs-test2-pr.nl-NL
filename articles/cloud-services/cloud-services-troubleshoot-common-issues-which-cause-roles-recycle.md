---
title: Common causes of Cloud Service roles recycling | Microsoft Docs
description: A cloud service role that suddenly recycles can cause significant downtime. Here are some common issues that cause roles to be recycled, which may help you reduce downtime.
services: cloud-services
documentationcenter: ''
author: simonxjx
manager: felixwu
editor: ''
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 4/6/2017
ms.author: v-six
ms.openlocfilehash: 0313d229a9f86d8550e9c6d9e5394ec61ff0fe60
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556497"
---
# <a name="common-issues-that-cause-roles-to-recycle"></a><span data-ttu-id="26554-104">Common issues that cause roles to recycle</span><span class="sxs-lookup"><span data-stu-id="26554-104">Common issues that cause roles to recycle</span></span>
<span data-ttu-id="26554-105">This article discusses some of the common causes of deployment problems and provides troubleshooting tips to help you resolve these problems.</span><span class="sxs-lookup"><span data-stu-id="26554-105">This article discusses some of the common causes of deployment problems and provides troubleshooting tips to help you resolve these problems.</span></span> <span data-ttu-id="26554-106">An indication that a problem exists with an application is when the role instance fails to start, or it cycles between the initializing, busy, and stopping states.</span><span class="sxs-lookup"><span data-stu-id="26554-106">An indication that a problem exists with an application is when the role instance fails to start, or it cycles between the initializing, busy, and stopping states.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a><span data-ttu-id="26554-107">Missing runtime dependencies</span><span class="sxs-lookup"><span data-stu-id="26554-107">Missing runtime dependencies</span></span>
<span data-ttu-id="26554-108">If a role in your application relies on any assembly that is not part of the .NET Framework or the Azure managed library, you must explicitly include that assembly in the application package.</span><span class="sxs-lookup"><span data-stu-id="26554-108">If a role in your application relies on any assembly that is not part of the .NET Framework or the Azure managed library, you must explicitly include that assembly in the application package.</span></span> <span data-ttu-id="26554-109">Keep in mind that other Microsoft frameworks are not available on Azure by default.</span><span class="sxs-lookup"><span data-stu-id="26554-109">Keep in mind that other Microsoft frameworks are not available on Azure by default.</span></span> <span data-ttu-id="26554-110">If your role relies on such a framework, you must add those assemblies to the application package.</span><span class="sxs-lookup"><span data-stu-id="26554-110">If your role relies on such a framework, you must add those assemblies to the application package.</span></span>

<span data-ttu-id="26554-111">Before you build and package your application, verify the following:</span><span class="sxs-lookup"><span data-stu-id="26554-111">Before you build and package your application, verify the following:</span></span>

* <span data-ttu-id="26554-112">If using Visual studio, make sure the **Copy Local** property is set to **True** for each referenced assembly in your project that is not part of the Azure SDK or the .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="26554-112">If using Visual studio, make sure the **Copy Local** property is set to **True** for each referenced assembly in your project that is not part of the Azure SDK or the .NET Framework.</span></span>
* <span data-ttu-id="26554-113">Make sure the web.config file does not reference any unused assemblies in the compilation element.</span><span class="sxs-lookup"><span data-stu-id="26554-113">Make sure the web.config file does not reference any unused assemblies in the compilation element.</span></span>
* <span data-ttu-id="26554-114">The **Build Action** of every .cshtml file is set to **Content**.</span><span class="sxs-lookup"><span data-stu-id="26554-114">The **Build Action** of every .cshtml file is set to **Content**.</span></span> <span data-ttu-id="26554-115">This ensures that the files will appear correctly in the package and enables other referenced files to appear in the package.</span><span class="sxs-lookup"><span data-stu-id="26554-115">This ensures that the files will appear correctly in the package and enables other referenced files to appear in the package.</span></span>

## <a name="assembly-targets-wrong-platform"></a><span data-ttu-id="26554-116">Assembly targets wrong platform</span><span class="sxs-lookup"><span data-stu-id="26554-116">Assembly targets wrong platform</span></span>
<span data-ttu-id="26554-117">Azure is a 64-bit environment.</span><span class="sxs-lookup"><span data-stu-id="26554-117">Azure is a 64-bit environment.</span></span> <span data-ttu-id="26554-118">Therefore, .NET assemblies compiled for a 32-bit target won't work on Azure.</span><span class="sxs-lookup"><span data-stu-id="26554-118">Therefore, .NET assemblies compiled for a 32-bit target won't work on Azure.</span></span>

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a><span data-ttu-id="26554-119">Role throws unhandled exceptions while initializing or stopping</span><span class="sxs-lookup"><span data-stu-id="26554-119">Role throws unhandled exceptions while initializing or stopping</span></span>
<span data-ttu-id="26554-120">Any exceptions that are thrown by the methods of the [RoleEntryPoint] class, which includes the [OnStart], [OnStop], and [Run] methods, are unhandled exceptions.</span><span class="sxs-lookup"><span data-stu-id="26554-120">Any exceptions that are thrown by the methods of the [RoleEntryPoint] class, which includes the [OnStart], [OnStop], and [Run] methods, are unhandled exceptions.</span></span> <span data-ttu-id="26554-121">If an unhandled exception occurs in one of these methods, the role will recycle.</span><span class="sxs-lookup"><span data-stu-id="26554-121">If an unhandled exception occurs in one of these methods, the role will recycle.</span></span> <span data-ttu-id="26554-122">If the role is recycling repeatedly, it may be throwing an unhandled exception each time it tries to start.</span><span class="sxs-lookup"><span data-stu-id="26554-122">If the role is recycling repeatedly, it may be throwing an unhandled exception each time it tries to start.</span></span>

## <a name="role-returns-from-run-method"></a><span data-ttu-id="26554-123">Role returns from Run method</span><span class="sxs-lookup"><span data-stu-id="26554-123">Role returns from Run method</span></span>
<span data-ttu-id="26554-124">The [Run] method is intended to run indefinitely.</span><span class="sxs-lookup"><span data-stu-id="26554-124">The [Run] method is intended to run indefinitely.</span></span> <span data-ttu-id="26554-125">If your code overrides the [Run] method, it should sleep indefinitely.</span><span class="sxs-lookup"><span data-stu-id="26554-125">If your code overrides the [Run] method, it should sleep indefinitely.</span></span> <span data-ttu-id="26554-126">If the [Run] method returns, the role recycles.</span><span class="sxs-lookup"><span data-stu-id="26554-126">If the [Run] method returns, the role recycles.</span></span>

## <a name="incorrect-diagnosticsconnectionstring-setting"></a><span data-ttu-id="26554-127">Incorrect DiagnosticsConnectionString setting</span><span class="sxs-lookup"><span data-stu-id="26554-127">Incorrect DiagnosticsConnectionString setting</span></span>
<span data-ttu-id="26554-128">If application uses Azure Diagnostics, your service configuration file must specify the `DiagnosticsConnectionString` configuration setting.</span><span class="sxs-lookup"><span data-stu-id="26554-128">If application uses Azure Diagnostics, your service configuration file must specify the `DiagnosticsConnectionString` configuration setting.</span></span> <span data-ttu-id="26554-129">This setting should specify an HTTPS connection to your storage account in Azure.</span><span class="sxs-lookup"><span data-stu-id="26554-129">This setting should specify an HTTPS connection to your storage account in Azure.</span></span>

<span data-ttu-id="26554-130">To ensure that your `DiagnosticsConnectionString` setting is correct before you deploy your application package to Azure, verify the following:</span><span class="sxs-lookup"><span data-stu-id="26554-130">To ensure that your `DiagnosticsConnectionString` setting is correct before you deploy your application package to Azure, verify the following:</span></span>  

* <span data-ttu-id="26554-131">The `DiagnosticsConnectionString` setting points to a valid storage account in Azure.</span><span class="sxs-lookup"><span data-stu-id="26554-131">The `DiagnosticsConnectionString` setting points to a valid storage account in Azure.</span></span>  
  <span data-ttu-id="26554-132">By default, this setting points to the emulated storage account, so you must explicitly change this setting before you deploy your application package.</span><span class="sxs-lookup"><span data-stu-id="26554-132">By default, this setting points to the emulated storage account, so you must explicitly change this setting before you deploy your application package.</span></span> <span data-ttu-id="26554-133">If you do not change this setting, an exception is thrown when the role instance attempts to start the diagnostic monitor.</span><span class="sxs-lookup"><span data-stu-id="26554-133">If you do not change this setting, an exception is thrown when the role instance attempts to start the diagnostic monitor.</span></span> <span data-ttu-id="26554-134">This may cause the role instance to recycle indefinitely.</span><span class="sxs-lookup"><span data-stu-id="26554-134">This may cause the role instance to recycle indefinitely.</span></span>
* <span data-ttu-id="26554-135">The connection string is specified in the following [format](../storage/storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="26554-135">The connection string is specified in the following [format](../storage/storage-configure-connection-string.md).</span></span> <span data-ttu-id="26554-136">(The protocol must be specified as HTTPS.) Replace *MyAccountName* with the name of your storage account, and *MyAccountKey* with your access key:</span><span class="sxs-lookup"><span data-stu-id="26554-136">(The protocol must be specified as HTTPS.) Replace *MyAccountName* with the name of your storage account, and *MyAccountKey* with your access key:</span></span>    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  <span data-ttu-id="26554-137">If you are developing your application by using Azure Tools for Microsoft Visual Studio, you can use the property pages to set this value.</span><span class="sxs-lookup"><span data-stu-id="26554-137">If you are developing your application by using Azure Tools for Microsoft Visual Studio, you can use the property pages to set this value.</span></span>

## <a name="exported-certificate-does-not-include-private-key"></a><span data-ttu-id="26554-138">Exported certificate does not include private key</span><span class="sxs-lookup"><span data-stu-id="26554-138">Exported certificate does not include private key</span></span>
<span data-ttu-id="26554-139">To run a web role under SSL, you must ensure that your exported management certificate includes the private key.</span><span class="sxs-lookup"><span data-stu-id="26554-139">To run a web role under SSL, you must ensure that your exported management certificate includes the private key.</span></span> <span data-ttu-id="26554-140">If you use the *Windows Certificate Manager* to export the certificate, be sure to select **Yes** for the **Export the private key** option.</span><span class="sxs-lookup"><span data-stu-id="26554-140">If you use the *Windows Certificate Manager* to export the certificate, be sure to select **Yes** for the **Export the private key** option.</span></span> <span data-ttu-id="26554-141">The certificate must be exported in the PFX format, which is the only format currently supported.</span><span class="sxs-lookup"><span data-stu-id="26554-141">The certificate must be exported in the PFX format, which is the only format currently supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26554-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="26554-142">Next steps</span></span>
<span data-ttu-id="26554-143">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span><span class="sxs-lookup"><span data-stu-id="26554-143">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="26554-144">View more role recycling scenarios at [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="26554-144">View more role recycling scenarios at [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[Run]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx