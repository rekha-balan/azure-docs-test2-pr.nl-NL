---
title: Enable Application Insights Profiler for applications that are hosted on Azure Cloud Services resources | Microsoft Docs
description: Learn how to set up Application Insights Profiler on an application running on Azure Cloud Services.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 10/16/2017
ms.reviewer: ramach
ms.author: mbullwin
ms.openlocfilehash: 2da281f52a85992c6fade360c94fbf473c38dc20
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856242"
---
# <a name="enable-application-insights-profiler-for-azure-vms-service-fabric-and-azure-cloud-services"></a><span data-ttu-id="06e5a-103">Enable Application Insights Profiler for Azure VMs, Service Fabric, and Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="06e5a-103">Enable Application Insights Profiler for Azure VMs, Service Fabric, and Azure Cloud Services</span></span>

<span data-ttu-id="06e5a-104">This article demonstrates how to enable Azure Application Insights Profiler on an ASP.NET application that is hosted by an Azure Cloud Services resource.</span><span class="sxs-lookup"><span data-stu-id="06e5a-104">This article demonstrates how to enable Azure Application Insights Profiler on an ASP.NET application that is hosted by an Azure Cloud Services resource.</span></span>

<span data-ttu-id="06e5a-105">The examples in this article include support for Azure Virtual Machines, virtual machine scale sets, Azure Service Fabric, and Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="06e5a-105">The examples in this article include support for Azure Virtual Machines, virtual machine scale sets, Azure Service Fabric, and Azure Cloud Services.</span></span> <span data-ttu-id="06e5a-106">The examples rely on templates that support the [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) deployment model.</span><span class="sxs-lookup"><span data-stu-id="06e5a-106">The examples rely on templates that support the [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) deployment model.</span></span>  


## <a name="overview"></a><span data-ttu-id="06e5a-107">Overview</span><span class="sxs-lookup"><span data-stu-id="06e5a-107">Overview</span></span>

<span data-ttu-id="06e5a-108">The following image shows how Application Insights Profiler works with applications that are hosted on Azure Cloud Services resources.</span><span class="sxs-lookup"><span data-stu-id="06e5a-108">The following image shows how Application Insights Profiler works with applications that are hosted on Azure Cloud Services resources.</span></span> <span data-ttu-id="06e5a-109">Azure Cloud Services resources include Virtual Machines, scale sets, cloud services, and Service Fabric clusters.</span><span class="sxs-lookup"><span data-stu-id="06e5a-109">Azure Cloud Services resources include Virtual Machines, scale sets, cloud services, and Service Fabric clusters.</span></span> <span data-ttu-id="06e5a-110">The image uses an Azure virtual machine as an example.</span><span class="sxs-lookup"><span data-stu-id="06e5a-110">The image uses an Azure virtual machine as an example.</span></span>  

  ![Diagram showing how Application Insights Profiler works with Azure Cloud Services resources](./media/enable-profiler-compute/overview.png)

<span data-ttu-id="06e5a-112">To fully enable Profiler, you must change the configuration in three locations:</span><span class="sxs-lookup"><span data-stu-id="06e5a-112">To fully enable Profiler, you must change the configuration in three locations:</span></span>

* <span data-ttu-id="06e5a-113">The Application Insights instance pane in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="06e5a-113">The Application Insights instance pane in the Azure portal.</span></span>
* <span data-ttu-id="06e5a-114">The application source code (for example, an ASP.NET web application).</span><span class="sxs-lookup"><span data-stu-id="06e5a-114">The application source code (for example, an ASP.NET web application).</span></span>
* <span data-ttu-id="06e5a-115">The environment deployment definition source code (for example, an Azure Resource Manager template in the .json file).</span><span class="sxs-lookup"><span data-stu-id="06e5a-115">The environment deployment definition source code (for example, an Azure Resource Manager template in the .json file).</span></span>


## <a name="set-up-the-application-insights-instance"></a><span data-ttu-id="06e5a-116">Set up the Application Insights instance</span><span class="sxs-lookup"><span data-stu-id="06e5a-116">Set up the Application Insights instance</span></span>

1. <span data-ttu-id="06e5a-117">[Create a new Application Insights resource](https://docs.microsoft.com/azure/application-insights/app-insights-create-new-resource), or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="06e5a-117">[Create a new Application Insights resource](https://docs.microsoft.com/azure/application-insights/app-insights-create-new-resource), or select an existing one.</span></span> 

1. <span data-ttu-id="06e5a-118">Go to your Application Insights resource, and then copy the instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="06e5a-118">Go to your Application Insights resource, and then copy the instrumentation key.</span></span>

   ![Location of the instrumentation key](./media/enable-profiler-compute/CopyAIKey.png)

1. <span data-ttu-id="06e5a-120">To finish setting up the Application Insights instance for Profiler, complete the procedure that's described in [Enable Profiler.</span><span class="sxs-lookup"><span data-stu-id="06e5a-120">To finish setting up the Application Insights instance for Profiler, complete the procedure that's described in [Enable Profiler.</span></span> <span data-ttu-id="06e5a-121">You don't need to link the web apps, because the steps are specific to the app services resource.</span><span class="sxs-lookup"><span data-stu-id="06e5a-121">You don't need to link the web apps, because the steps are specific to the app services resource.</span></span> <span data-ttu-id="06e5a-122">Ensure that Profiler is enabled in the **Configure Profiler** pane.</span><span class="sxs-lookup"><span data-stu-id="06e5a-122">Ensure that Profiler is enabled in the **Configure Profiler** pane.</span></span>


## <a name="set-up-the-application-source-code"></a><span data-ttu-id="06e5a-123">Set up the application source code</span><span class="sxs-lookup"><span data-stu-id="06e5a-123">Set up the application source code</span></span>

### <a name="aspnet-web-applications-azure-cloud-services-web-roles-or-the-service-fabric-aspnet-web-front-end"></a><span data-ttu-id="06e5a-124">ASP.NET web applications, Azure Cloud Services web roles, or the Service Fabric ASP.NET web front end</span><span class="sxs-lookup"><span data-stu-id="06e5a-124">ASP.NET web applications, Azure Cloud Services web roles, or the Service Fabric ASP.NET web front end</span></span>
<span data-ttu-id="06e5a-125">Set up your application to send telemetry data to an Application Insights instance on each `Request` operation.</span><span class="sxs-lookup"><span data-stu-id="06e5a-125">Set up your application to send telemetry data to an Application Insights instance on each `Request` operation.</span></span>  

<span data-ttu-id="06e5a-126">Add the [Application Insights SDK](https://docs.microsoft.com/azure/application-insights/app-insights-overview#get-started) to your application project.</span><span class="sxs-lookup"><span data-stu-id="06e5a-126">Add the [Application Insights SDK](https://docs.microsoft.com/azure/application-insights/app-insights-overview#get-started) to your application project.</span></span> <span data-ttu-id="06e5a-127">Make sure that the NuGet package versions are as follows:</span><span class="sxs-lookup"><span data-stu-id="06e5a-127">Make sure that the NuGet package versions are as follows:</span></span>  
  - <span data-ttu-id="06e5a-128">For ASP.NET applications: [Microsoft.ApplicationInsights.Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) 2.3.0 or later.</span><span class="sxs-lookup"><span data-stu-id="06e5a-128">For ASP.NET applications: [Microsoft.ApplicationInsights.Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) 2.3.0 or later.</span></span>
  - <span data-ttu-id="06e5a-129">For ASP.NET Core applications: [Microsoft.ApplicationInsights.AspNetCore](https://www.nuget.org/packages/Microsoft.ApplicationInsights.AspNetCore/) 2.1.0 or later.</span><span class="sxs-lookup"><span data-stu-id="06e5a-129">For ASP.NET Core applications: [Microsoft.ApplicationInsights.AspNetCore](https://www.nuget.org/packages/Microsoft.ApplicationInsights.AspNetCore/) 2.1.0 or later.</span></span>
  - <span data-ttu-id="06e5a-130">For other .NET and .NET Core applications (for example, a Service Fabric stateless service or a Cloud Services worker role): [Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) or [Microsoft.ApplicationInsights.Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) 2.3.0 or later.</span><span class="sxs-lookup"><span data-stu-id="06e5a-130">For other .NET and .NET Core applications (for example, a Service Fabric stateless service or a Cloud Services worker role): [Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) or [Microsoft.ApplicationInsights.Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) 2.3.0 or later.</span></span>  

### <a name="azure-cloud-services-worker-roles-or-the-service-fabric-stateless-back-end"></a><span data-ttu-id="06e5a-131">Azure Cloud Services worker roles or the Service Fabric stateless back end</span><span class="sxs-lookup"><span data-stu-id="06e5a-131">Azure Cloud Services worker roles or the Service Fabric stateless back end</span></span>
<span data-ttu-id="06e5a-132">In addition to completing the preceding step, if your application is *not* an ASP.NET or ASP.NET Core application (for example, if it's an Azure Cloud Services worker role or Service Fabric stateless APIs), do the following:</span><span class="sxs-lookup"><span data-stu-id="06e5a-132">In addition to completing the preceding step, if your application is *not* an ASP.NET or ASP.NET Core application (for example, if it's an Azure Cloud Services worker role or Service Fabric stateless APIs), do the following:</span></span>  

  1. <span data-ttu-id="06e5a-133">Early in the application lifetime, add the following code:</span><span class="sxs-lookup"><span data-stu-id="06e5a-133">Early in the application lifetime, add the following code:</span></span>  

        ```csharp
        using Microsoft.ApplicationInsights.Extensibility;
        ...
        // Replace with your own Application Insights instrumentation key.
        TelemetryConfiguration.Active.InstrumentationKey = "00000000-0000-0000-0000-000000000000";
        ```
      <span data-ttu-id="06e5a-134">For more information about this global instrumentation key configuration, see [Use Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span><span class="sxs-lookup"><span data-stu-id="06e5a-134">For more information about this global instrumentation key configuration, see [Use Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>  

  1. <span data-ttu-id="06e5a-135">For any piece of code that you want to instrument, add a `StartOperation<RequestTelemetry>` **USING** statement around it, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="06e5a-135">For any piece of code that you want to instrument, add a `StartOperation<RequestTelemetry>` **USING** statement around it, as shown in the following example:</span></span>

        ```csharp
        using Microsoft.ApplicationInsights;
        using Microsoft.ApplicationInsights.DataContracts;
        ...
        var client = new TelemetryClient();
        ...
        using (var operation = client.StartOperation<RequestTelemetry>("Insert_Your_Custom_Event_Unique_Name"))
        {
          // ... Code I want to profile.
        }
        ```

        <span data-ttu-id="06e5a-136">Calling `StartOperation<RequestTelemetry>` within another `StartOperation<RequestTelemetry>` scope is not supported.</span><span class="sxs-lookup"><span data-stu-id="06e5a-136">Calling `StartOperation<RequestTelemetry>` within another `StartOperation<RequestTelemetry>` scope is not supported.</span></span> <span data-ttu-id="06e5a-137">You can use `StartOperation<DependencyTelemetry>` in the nested scope instead.</span><span class="sxs-lookup"><span data-stu-id="06e5a-137">You can use `StartOperation<DependencyTelemetry>` in the nested scope instead.</span></span> <span data-ttu-id="06e5a-138">For example:</span><span class="sxs-lookup"><span data-stu-id="06e5a-138">For example:</span></span>  
        
        ```csharp
        using (var getDetailsOperation = client.StartOperation<RequestTelemetry>("GetProductDetails"))
        {
        try
        {
          ProductDetail details = new ProductDetail() { Id = productId };
          getDetailsOperation.Telemetry.Properties["ProductId"] = productId.ToString();
        
          // By using DependencyTelemetry, 'GetProductPrice' is correctly linked as part of the 'GetProductDetails' request.
          using (var getPriceOperation = client.StartOperation<DependencyTelemetry>("GetProductPrice"))
          {
              double price = await _priceDataBase.GetAsync(productId);
              if (IsTooCheap(price))
              {
                  throw new PriceTooLowException(productId);
              }
              details.Price = price;
          }
        
          // Similarly, note how 'GetProductReviews' doesn't establish another RequestTelemetry.
          using (var getReviewsOperation = client.StartOperation<DependencyTelemetry>("GetProductReviews"))
          {
              details.Reviews = await _reviewDataBase.GetAsync(productId);
          }
        
          getDetailsOperation.Telemetry.Success = true;
          return details;
        }
        catch(Exception ex)
        {
          getDetailsOperation.Telemetry.Success = false;
        
          // This exception gets linked to the 'GetProductDetails' request telemetry.
          client.TrackException(ex);
          throw;
        }
        }
        ```

## <a name="set-up-the-environment-deployment-definition"></a><span data-ttu-id="06e5a-139">Set up the environment deployment definition</span><span class="sxs-lookup"><span data-stu-id="06e5a-139">Set up the environment deployment definition</span></span>

<span data-ttu-id="06e5a-140">The environment in which Profiler and your application execute can be a virtual machine, a virtual machine scale set, a Service Fabric cluster, or a cloud services instance.</span><span class="sxs-lookup"><span data-stu-id="06e5a-140">The environment in which Profiler and your application execute can be a virtual machine, a virtual machine scale set, a Service Fabric cluster, or a cloud services instance.</span></span>  

### <a name="virtual-machines-scale-sets-or-service-fabric"></a><span data-ttu-id="06e5a-141">Virtual machines, scale sets, or Service Fabric</span><span class="sxs-lookup"><span data-stu-id="06e5a-141">Virtual machines, scale sets, or Service Fabric</span></span>

<span data-ttu-id="06e5a-142">For full examples, see:</span><span class="sxs-lookup"><span data-stu-id="06e5a-142">For full examples, see:</span></span>  
  * [<span data-ttu-id="06e5a-143">Virtual machine</span><span class="sxs-lookup"><span data-stu-id="06e5a-143">Virtual machine</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)
  * [<span data-ttu-id="06e5a-144">Virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="06e5a-144">Virtual machine scale set</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)
  * [<span data-ttu-id="06e5a-145">Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="06e5a-145">Service Fabric cluster</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json)

<span data-ttu-id="06e5a-146">To set up your environment, do the following:</span><span class="sxs-lookup"><span data-stu-id="06e5a-146">To set up your environment, do the following:</span></span>
1. <span data-ttu-id="06e5a-147">To ensure that you're using [.NET Framework 4.6.1](https://docs.microsoft.com/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed) or later, it's sufficient to confirm that the deployed OS is `Windows Server 2012 R2` or later.</span><span class="sxs-lookup"><span data-stu-id="06e5a-147">To ensure that you're using [.NET Framework 4.6.1](https://docs.microsoft.com/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed) or later, it's sufficient to confirm that the deployed OS is `Windows Server 2012 R2` or later.</span></span>

1. <span data-ttu-id="06e5a-148">Search for the [Azure Diagnostics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics) extension in the deployment template file, and then add the following `SinksConfig` section as a child element of `WadCfg`.</span><span class="sxs-lookup"><span data-stu-id="06e5a-148">Search for the [Azure Diagnostics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics) extension in the deployment template file, and then add the following `SinksConfig` section as a child element of `WadCfg`.</span></span> <span data-ttu-id="06e5a-149">Replace the `ApplicationInsightsProfiler` property value with your own Application Insights instrumentation key:</span><span class="sxs-lookup"><span data-stu-id="06e5a-149">Replace the `ApplicationInsightsProfiler` property value with your own Application Insights instrumentation key:</span></span>  

      ```json
      "SinksConfig": {
        "Sink": [
          {
            "name": "MyApplicationInsightsProfilerSink",
            "ApplicationInsightsProfiler": "00000000-0000-0000-0000-000000000000"
          }
        ]
      }
      ```

      <span data-ttu-id="06e5a-150">For information about adding the Diagnostics extension to your deployment template, see [Use monitoring and diagnostics with a Windows VM and Azure Resource Manager templates](https://docs.microsoft.com/azure/virtual-machines/windows/extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06e5a-150">For information about adding the Diagnostics extension to your deployment template, see [Use monitoring and diagnostics with a Windows VM and Azure Resource Manager templates](https://docs.microsoft.com/azure/virtual-machines/windows/extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!TIP]
> <span data-ttu-id="06e5a-151">For Virtual Machines an alternative to the json based steps above is to navigate in the Azure portal to  **Virtual Machines** > **Diagnostic Settings** > **Sinks** > Set send diagnostic data to Application Insights to **Enabled** and either select an Application Insights account or a specific ikey.</span><span class="sxs-lookup"><span data-stu-id="06e5a-151">For Virtual Machines an alternative to the json based steps above is to navigate in the Azure portal to  **Virtual Machines** > **Diagnostic Settings** > **Sinks** > Set send diagnostic data to Application Insights to **Enabled** and either select an Application Insights account or a specific ikey.</span></span>

### <a name="azure-cloud-services"></a><span data-ttu-id="06e5a-152">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="06e5a-152">Azure Cloud Services</span></span>

1. <span data-ttu-id="06e5a-153">To ensure that you're using [.NET Framework 4.6.1](https://docs.microsoft.com/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed) or later, it's sufficient to confirm that the *ServiceConfiguration.\*.cscfg* files have an `osFamily` value of "5" or later.</span><span class="sxs-lookup"><span data-stu-id="06e5a-153">To ensure that you're using [.NET Framework 4.6.1](https://docs.microsoft.com/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed) or later, it's sufficient to confirm that the *ServiceConfiguration.\*.cscfg* files have an `osFamily` value of "5" or later.</span></span>

1. <span data-ttu-id="06e5a-154">Locate the [Azure Diagnostics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics) *diagnostics.wadcfgx* file for your application role, as shown here:</span><span class="sxs-lookup"><span data-stu-id="06e5a-154">Locate the [Azure Diagnostics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics) *diagnostics.wadcfgx* file for your application role, as shown here:</span></span>  

   ![Location of the diagnostics config file](./media/enable-profiler-compute/cloudservice-solutionexplorer.png)  

   <span data-ttu-id="06e5a-156">If you can't find the file, to learn how to enable the Diagnostics extension in your Azure Cloud Services project, see [Set up diagnostics for Azure Cloud Services and virtual machines](https://docs.microsoft.com/azure/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines#enable-diagnostics-in-cloud-service-projects-before-deploying-them).</span><span class="sxs-lookup"><span data-stu-id="06e5a-156">If you can't find the file, to learn how to enable the Diagnostics extension in your Azure Cloud Services project, see [Set up diagnostics for Azure Cloud Services and virtual machines](https://docs.microsoft.com/azure/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines#enable-diagnostics-in-cloud-service-projects-before-deploying-them).</span></span>

1. <span data-ttu-id="06e5a-157">Add the following `SinksConfig` section as a child element of `WadCfg`:</span><span class="sxs-lookup"><span data-stu-id="06e5a-157">Add the following `SinksConfig` section as a child element of `WadCfg`:</span></span>  

      ```xml
      <WadCfg>
        <DiagnosticMonitorConfiguration>...</DiagnosticMonitorConfiguration>
        <SinksConfig>
          <Sink name="MyApplicationInsightsProfiler">
            <!-- Replace with your own Application Insights instrumentation key. -->
            <ApplicationInsightsProfiler>00000000-0000-0000-0000-000000000000</ApplicationInsightsProfiler>
          </Sink>
        </SinksConfig>
      </WadCfg>
      ```

> [!NOTE]  
> <span data-ttu-id="06e5a-158">If the *diagnostics.wadcfgx* file also contains another sink of type `ApplicationInsights`, all three of the following instrumentation keys must match:</span><span class="sxs-lookup"><span data-stu-id="06e5a-158">If the *diagnostics.wadcfgx* file also contains another sink of type `ApplicationInsights`, all three of the following instrumentation keys must match:</span></span>  
>  * <span data-ttu-id="06e5a-159">The key that's used by your application.</span><span class="sxs-lookup"><span data-stu-id="06e5a-159">The key that's used by your application.</span></span>  
>  * <span data-ttu-id="06e5a-160">The key that's used by the `ApplicationInsights` sink.</span><span class="sxs-lookup"><span data-stu-id="06e5a-160">The key that's used by the `ApplicationInsights` sink.</span></span>  
>  * <span data-ttu-id="06e5a-161">The key that's used by the `ApplicationInsightsProfiler` sink.</span><span class="sxs-lookup"><span data-stu-id="06e5a-161">The key that's used by the `ApplicationInsightsProfiler` sink.</span></span>  
>
> <span data-ttu-id="06e5a-162">You can find the actual instrumentation key value that's used by the `ApplicationInsights` sink in the *ServiceConfiguration.\*.cscfg* files.</span><span class="sxs-lookup"><span data-stu-id="06e5a-162">You can find the actual instrumentation key value that's used by the `ApplicationInsights` sink in the *ServiceConfiguration.\*.cscfg* files.</span></span>  
> <span data-ttu-id="06e5a-163">After the Visual Studio 15.5 Azure SDK release, only the instrumentation keys that are used by the application and the `ApplicationInsightsProfiler` sink need to match each other.</span><span class="sxs-lookup"><span data-stu-id="06e5a-163">After the Visual Studio 15.5 Azure SDK release, only the instrumentation keys that are used by the application and the `ApplicationInsightsProfiler` sink need to match each other.</span></span>


## <a name="configure-environment-deployment-and-runtime"></a><span data-ttu-id="06e5a-164">Configure environment deployment and runtime</span><span class="sxs-lookup"><span data-stu-id="06e5a-164">Configure environment deployment and runtime</span></span>

1. <span data-ttu-id="06e5a-165">Deploy the modified environment deployment definition.</span><span class="sxs-lookup"><span data-stu-id="06e5a-165">Deploy the modified environment deployment definition.</span></span>  

   <span data-ttu-id="06e5a-166">To apply the modifications, usually involves a full template deployment or a cloud services based publish through PowerShell cmdlets or Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06e5a-166">To apply the modifications, usually involves a full template deployment or a cloud services based publish through PowerShell cmdlets or Visual Studio.</span></span>  

   <span data-ttu-id="06e5a-167">The following is an alternate approach for existing virtual machines that touches only the Azure Diagnostics extension:</span><span class="sxs-lookup"><span data-stu-id="06e5a-167">The following is an alternate approach for existing virtual machines that touches only the Azure Diagnostics extension:</span></span>  

    ```powershell
    $ConfigFilePath = [IO.Path]::GetTempFileName()
    # After you export the currently deployed Diagnostics config to a file, edit it to include the ApplicationInsightsProfiler sink.
    (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName "MyRG" -VMName "MyVM").PublicSettings | Out-File -Verbose $ConfigFilePath
    # Set-AzureRmVMDiagnosticsExtension might require the -StorageAccountName argument
    # If your original diagnostics configuration had the storageAccountName property in the protectedSettings section (which is not downloadable), be sure to pass the same original value you had in this cmdlet call.
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName "MyRG" -VMName "MyVM" -DiagnosticsConfigurationPath $ConfigFilePath
    ```

1. <span data-ttu-id="06e5a-168">If the intended application is running through [IIS](https://www.microsoft.com/web/downloads/platform.aspx), enable the `IIS Http Tracing` Windows feature by doing the following:</span><span class="sxs-lookup"><span data-stu-id="06e5a-168">If the intended application is running through [IIS](https://www.microsoft.com/web/downloads/platform.aspx), enable the `IIS Http Tracing` Windows feature by doing the following:</span></span>  

   <span data-ttu-id="06e5a-169">a.</span><span class="sxs-lookup"><span data-stu-id="06e5a-169">a.</span></span> <span data-ttu-id="06e5a-170">Establish remote access to the environment, and then use the [Add Windows features]( https://docs.microsoft.com/iis/configuration/system.webserver/tracing/) window, or run the following command in PowerShell (as administrator):</span><span class="sxs-lookup"><span data-stu-id="06e5a-170">Establish remote access to the environment, and then use the [Add Windows features]( https://docs.microsoft.com/iis/configuration/system.webserver/tracing/) window, or run the following command in PowerShell (as administrator):</span></span>  

    ```powershell
    Enable-WindowsOptionalFeature -FeatureName IIS-HttpTracing -Online -All
    ```  
   <span data-ttu-id="06e5a-171">b.</span><span class="sxs-lookup"><span data-stu-id="06e5a-171">b.</span></span> <span data-ttu-id="06e5a-172">If establishing remote access is a problem, you can use [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) to run the following command:</span><span class="sxs-lookup"><span data-stu-id="06e5a-172">If establishing remote access is a problem, you can use [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) to run the following command:</span></span>  

    ```powershell
    az vm run-command invoke -g MyResourceGroupName -n MyVirtualMachineName --command-id RunPowerShellScript --scripts "Enable-WindowsOptionalFeature -FeatureName IIS-HttpTracing -Online -All"
    ```


## <a name="enable-profiler-on-on-premises-servers"></a><span data-ttu-id="06e5a-173">Enable Profiler on on-premises servers</span><span class="sxs-lookup"><span data-stu-id="06e5a-173">Enable Profiler on on-premises servers</span></span>

<span data-ttu-id="06e5a-174">Enabling Profiler on an on-premises server is also known as running Application Insights Profiler in standalone mode.</span><span class="sxs-lookup"><span data-stu-id="06e5a-174">Enabling Profiler on an on-premises server is also known as running Application Insights Profiler in standalone mode.</span></span> <span data-ttu-id="06e5a-175">It's not tied to Azure Diagnostics extension modifications.</span><span class="sxs-lookup"><span data-stu-id="06e5a-175">It's not tied to Azure Diagnostics extension modifications.</span></span>

<span data-ttu-id="06e5a-176">We have no plan to officially support Profiler for on-premises servers.</span><span class="sxs-lookup"><span data-stu-id="06e5a-176">We have no plan to officially support Profiler for on-premises servers.</span></span> <span data-ttu-id="06e5a-177">If you are interested in experimenting with this scenario, you can [download support code](https://github.com/ramach-msft/AIProfiler-Standalone).</span><span class="sxs-lookup"><span data-stu-id="06e5a-177">If you are interested in experimenting with this scenario, you can [download support code](https://github.com/ramach-msft/AIProfiler-Standalone).</span></span> <span data-ttu-id="06e5a-178">We are *not* responsible for maintaining that code, or for responding to issues and feature requests that are related to the code.</span><span class="sxs-lookup"><span data-stu-id="06e5a-178">We are *not* responsible for maintaining that code, or for responding to issues and feature requests that are related to the code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06e5a-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="06e5a-179">Next steps</span></span>

- <span data-ttu-id="06e5a-180">Generate traffic to your application (for example, launch an [availability test](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability)).</span><span class="sxs-lookup"><span data-stu-id="06e5a-180">Generate traffic to your application (for example, launch an [availability test](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability)).</span></span> <span data-ttu-id="06e5a-181">Then, wait 10 to 15 minutes for traces to start to be sent to the Application Insights instance.</span><span class="sxs-lookup"><span data-stu-id="06e5a-181">Then, wait 10 to 15 minutes for traces to start to be sent to the Application Insights instance.</span></span>
- <span data-ttu-id="06e5a-182">See [Profiler traces](https://docs.microsoft.com/azure/application-insights/app-insights-profiler#enable-the-profiler) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="06e5a-182">See [Profiler traces](https://docs.microsoft.com/azure/application-insights/app-insights-profiler#enable-the-profiler) in the Azure portal.</span></span>
- <span data-ttu-id="06e5a-183">Get help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="06e5a-183">Get help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>
- <span data-ttu-id="06e5a-184">Read more about Profiler in [Application Insights Profiler](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="06e5a-184">Read more about Profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
