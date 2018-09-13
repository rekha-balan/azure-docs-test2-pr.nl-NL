---
title: Trace the flow in a Cloud Services Application with Azure Diagnostics | Microsoft Docs
description: Add tracing messages to an Azure application to help debugging, measuring performance, monitoring, traffic analysis, and more.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: ''
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: 35b4a4270846c54a1ca760e803ef7adba60cf03b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661274"
---
# <a name="trace-the-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="f4d32-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="f4d32-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="f4d32-104">Tracing is a way for you to monitor the execution of your application while it is running.</span><span class="sxs-lookup"><span data-stu-id="f4d32-104">Tracing is a way for you to monitor the execution of your application while it is running.</span></span> <span data-ttu-id="f4d32-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span><span class="sxs-lookup"><span data-stu-id="f4d32-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="f4d32-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4d32-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="f4d32-107">Use trace statements and trace switches</span><span class="sxs-lookup"><span data-stu-id="f4d32-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="f4d32-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span><span class="sxs-lookup"><span data-stu-id="f4d32-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="f4d32-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span><span class="sxs-lookup"><span data-stu-id="f4d32-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span></span> <span data-ttu-id="f4d32-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span><span class="sxs-lookup"><span data-stu-id="f4d32-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span></span>

<span data-ttu-id="f4d32-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4d32-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="f4d32-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span><span class="sxs-lookup"><span data-stu-id="f4d32-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="f4d32-113">This lets you monitor the status of your application in a production environment.</span><span class="sxs-lookup"><span data-stu-id="f4d32-113">This lets you monitor the status of your application in a production environment.</span></span> <span data-ttu-id="f4d32-114">This is especially important in a business application that uses multiple components running on multiple computers.</span><span class="sxs-lookup"><span data-stu-id="f4d32-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="f4d32-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4d32-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-the-trace-listener-in-an-azure-application"></a><span data-ttu-id="f4d32-116">Configure the trace listener in an Azure application</span><span class="sxs-lookup"><span data-stu-id="f4d32-116">Configure the trace listener in an Azure application</span></span>
<span data-ttu-id="f4d32-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span><span class="sxs-lookup"><span data-stu-id="f4d32-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span></span> <span data-ttu-id="f4d32-118">Listeners collect, store, and route tracing messages.</span><span class="sxs-lookup"><span data-stu-id="f4d32-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="f4d32-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span><span class="sxs-lookup"><span data-stu-id="f4d32-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="f4d32-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span><span class="sxs-lookup"><span data-stu-id="f4d32-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="f4d32-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span><span class="sxs-lookup"><span data-stu-id="f4d32-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span></span> <span data-ttu-id="f4d32-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="f4d32-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="f4d32-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span><span class="sxs-lookup"><span data-stu-id="f4d32-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="f4d32-124">Add a trace listener</span><span class="sxs-lookup"><span data-stu-id="f4d32-124">Add a trace listener</span></span>
1. <span data-ttu-id="f4d32-125">Open the web.config or app.config file for your role.</span><span class="sxs-lookup"><span data-stu-id="f4d32-125">Open the web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="f4d32-126">Add the following code to the file.</span><span class="sxs-lookup"><span data-stu-id="f4d32-126">Add the following code to the file.</span></span> <span data-ttu-id="f4d32-127">Change the Version attribute to use the version number of the assembly you are referencing.</span><span class="sxs-lookup"><span data-stu-id="f4d32-127">Change the Version attribute to use the version number of the assembly you are referencing.</span></span> <span data-ttu-id="f4d32-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span><span class="sxs-lookup"><span data-stu-id="f4d32-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span></span>
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > <span data-ttu-id="f4d32-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span><span class="sxs-lookup"><span data-stu-id="f4d32-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="f4d32-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span><span class="sxs-lookup"><span data-stu-id="f4d32-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="f4d32-131">Save the config file.</span><span class="sxs-lookup"><span data-stu-id="f4d32-131">Save the config file.</span></span>

<span data-ttu-id="f4d32-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4d32-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="f4d32-133">After you complete the steps to add the listener, you can add trace statements to your code.</span><span class="sxs-lookup"><span data-stu-id="f4d32-133">After you complete the steps to add the listener, you can add trace statements to your code.</span></span>

### <a name="to-add-trace-statement-to-your-code"></a><span data-ttu-id="f4d32-134">To add trace statement to your code</span><span class="sxs-lookup"><span data-stu-id="f4d32-134">To add trace statement to your code</span></span>
1. <span data-ttu-id="f4d32-135">Open a source file for your application.</span><span class="sxs-lookup"><span data-stu-id="f4d32-135">Open a source file for your application.</span></span> <span data-ttu-id="f4d32-136">For example, the <RoleName>.cs file for the worker role or web role.</span><span class="sxs-lookup"><span data-stu-id="f4d32-136">For example, the <RoleName>.cs file for the worker role or web role.</span></span>
2. <span data-ttu-id="f4d32-137">Add the following using statement if it has not already been added:</span><span class="sxs-lookup"><span data-stu-id="f4d32-137">Add the following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="f4d32-138">Add Trace statements where you want to capture information about the state of your application.</span><span class="sxs-lookup"><span data-stu-id="f4d32-138">Add Trace statements where you want to capture information about the state of your application.</span></span> <span data-ttu-id="f4d32-139">You can use a variety of methods to format the output of the Trace statement.</span><span class="sxs-lookup"><span data-stu-id="f4d32-139">You can use a variety of methods to format the output of the Trace statement.</span></span> <span data-ttu-id="f4d32-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4d32-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="f4d32-141">Save the source file.</span><span class="sxs-lookup"><span data-stu-id="f4d32-141">Save the source file.</span></span>

