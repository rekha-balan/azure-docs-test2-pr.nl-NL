---
title: Using Elasticsearch as a Service Fabric application trace store | Microsoft Docs
description: Describes how Service Fabric applications can use Elasticsearch and Kibana to store, index, and search through application traces (logs)
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: ''
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostic-collect-logs-without-an-agent
ms.openlocfilehash: cef35bab6cf97253bde7c4b9fd075d6bb280db0c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662754"
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Use Elasticsearch as a Service Fabric application trace store
## <a name="introduction"></a>Introduction
This article describes how [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) applications can use **Elasticsearch** and **Kibana** for application trace storage, indexing, and search. [Elasticsearch](https://www.elastic.co/guide/index.html) is an open-source, distributed, and scalable real-time search and analytics engine that is well-suited for this task. It can be installed on Windows and Linux virtual machines running in Microsoft Azure. Elasticsearch can efficiently process *structured* traces produced using technologies such as **Event Tracing for Windows (ETW)**.

ETW is used by Service Fabric runtime to source diagnostic information (traces). It is the recommended method for Service Fabric applications to source their diagnostic information, too. Using the same mechanism allows for correlation between runtime-supplied and application-supplied traces and makes troubleshooting easier. Service Fabric project templates in Visual Studio include a logging API (based on the .NET **EventSource** class) that emits ETW traces by default. For a general overview of Service Fabric application tracing using ETW, see [Monitoring and diagnosing services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

For the traces to show up in Elasticsearch, they need to be captured at the Service Fabric cluster nodes in real time (while the application is running) and sent to an Elasticsearch endpoint. There are two major options for trace capturing:

* **In-process trace capturing**  
  The application, or more precisely, service process, is responsible for sending out the diagnostic data to the trace store (Elasticsearch).
* **Out-of-process trace capturing**  
  A separate agent is capturing traces from the service process or processes and sending them to the trace store.

Below, we describe how to set up Elasticsearch on Azure, discuss the pros and cons for both capture options, and explain how to configure a Service Fabric service to send data to Elasticsearch.

## <a name="set-up-elasticsearch-on-azure"></a>Set up Elasticsearch on Azure
The most straightforward way to set up the Elasticsearch service on Azure is through [**Azure Resource Manager templates**](../azure-resource-manager/resource-group-overview.md). A comprehensive [Quickstart Azure Resource Manager template for Elasticsearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) is available from Azure Quickstart templates repository. This template uses separate storage accounts for scale units (groups of nodes). It can also provision separate client and server nodes with different configurations and various numbers of data disks attached.

Here, we use another template, called **ES-MultiNode** from the [Azure diagnostic tools repository](https://github.com/Azure/azure-diagnostics-tools). This template is easier to use, and it creates an Elasticsearch cluster protected by HTTP basic authentication. Before you proceed, download the repository from GitHub to your machine (by either cloning the repository or downloading a zip file). The ES-MultiNode template is located in the folder with the same name.

### <a name="prepare-a-machine-to-run-elasticsearch-installation-scripts"></a>Prepare a machine to run Elasticsearch installation scripts
The easiest way to use the ES-MultiNode template is through a provided Azure PowerShell script called `CreateElasticSearchCluster`. To use this script, you need to install PowerShell modules and a tool called **openssl**. The latter is needed for creating an SSH key that can be used to administer your Elasticsearch cluster remotely.

`CreateElasticSearchCluster` script is designed for ease of use with the ES-MultiNode template from a Windows machine. It is possible to use the template on a non-Windows machine, but that scenario is beyond the scope of this article.

1. If you haven't installed them already, install [**Azure PowerShell modules**](http://aka.ms/webpi-azps). When prompted, click **Run**, then **Install**. Azure PowerShell 1.3 or newer is required.
2. The **openssl** tool is included in the distribution of [**Git for Windows**](http://www.git-scm.com/downloads). If you have not done so already, install [Git for Windows](http://www.git-scm.com/downloads) now. (The default installation options are OK.)
3. Assuming that Git has been installed but not included in the system path, open a Microsoft Azure PowerShell window and run the following commands:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Replace the `<Git installation folder>` with the Git location on your machine; the default is **"C:\Program Files\Git"**. Note the semicolon character at the beginning of the first path.
4. Ensure that you are logged on to Azure (via [`Add-AzureRmAccount`](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet) and that you have selected the subscription that should be used to create your Elastic Search cluster. You can verify that correct subscription is selected using `Get-AzureRmContext` and `Get-AzureRmSubscription` cmdlets.
5. If you haven't done so already, change the current directory to the ES-MultiNode folder.

### <a name="run-the-createelasticsearchcluster-script"></a>Run the CreateElasticSearchCluster script
Before you run the script, open the `azuredeploy-parameters.json` file and verify or provide values for the script parameters. The following parameters are provided:

| Parameter Name | Description |
| --- | --- |
| dnsNameForLoadBalancerIP |The name that is used to create the publicly visible DNS name for the Elastic Search cluster (by appending the Azure region domain to the provided name). For example, if this parameter value is "myBigCluster" and the chosen Azure region is West US, the resulting DNS name for the cluster is myBigCluster.westus.cloudapp.azure.com. <br /><br />This name also serves as a root name for many artifacts associated with the Elastic Search cluster, such as data node names. |
| adminUsername |The name of the administrator account for managing the Elastic Search cluster (corresponding SSH keys are generated automatically). |
| dataNodeCount |The number of nodes in the Elastic Search cluster. The current version of the script does not distinguish between data and query nodes; all nodes play both roles. Defaults to 3 nodes. |
| dataDiskSize |The size of data disks (in GB) that is allocated for each data node. Each node receives 4 data disks, exclusively dedicated to Elastic Search service. |
| region |The name of Azure region where the Elastic Search cluster should be located. |
| esUserName |The user name of the user that is configured to have access to ES cluster (subject to HTTP basic authentication). The password is not part of parameters file and must be provided when `CreateElasticSearchCluster` script is invoked. |
| vmSizeDataNodes |The Azure virtual machine size for Elastic Search cluster nodes. Defaults to Standard_D2. |

Now you are ready to run the script. Issue the following command:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

where 

| Script Parameter Name | Description |
| --- | --- |
| `<es-group-name>` |The name of the Azure resource group that will contain all Elastic Search cluster resources. |
| `<azure-region>` |The name of the Azure region where the Elastic Search cluster should be created. |
| `<es-password>` |The password for the Elastic Search user. |

> [!NOTE]
> If you get a NullReferenceException from the Test-AzureResourceGroup cmdlet, you have forgotten to log on to Azure (`Add-AzureRmAccount`).
> 
> 

If you get an error from running the script and you determine that the error was caused by a wrong template parameter value, correct the parameter file and run the script again with a different resource group name. You can also reuse the same resource group name and have the script clean up the old one by adding the `-RemoveExistingResourceGroup` parameter to the script invocation.

### <a name="result-of-running-the-createelasticsearchcluster-script"></a>Result of running the CreateElasticSearchCluster script
After you run the `CreateElasticSearchCluster` script, the following main artifacts will be created. For this example we assume that you have used "myBigCluster" as the value of the `dnsNameForLoadBalancerIP` parameter and that the region where you created the cluster is West US.

| Artifact | Name, location, and remarks |
| --- | --- |
| SSH key for remote administration |myBigCluster.key file (in the directory from which the CreateElasticSearchCluster was run). <br /><br />This key file can be used to connect to the admin node and (through the admin node) to data nodes in the cluster. |
| Admin node |myBigCluster-admin.westus.cloudapp.azure.com <br /><br />A dedicated VM for remote Elasticsearch cluster administration--the only one that allows external SSH connections. It runs on the same virtual network as all the Elasticsearch cluster nodes, but it does not run any Elasticsearch services. |
| Data nodes |myBigCluster1 … myBigCluster*N* <br /><br />Data nodes that are running Elasticsearch and Kibana services. You can connect via SSH to each node, but only via the admin node. |
| Elasticsearch cluster |http://myBigCluster.westus.cloudapp.azure.com/es/ <br /><br />The primary endpoint for the Elasticsearch cluster (note the /es suffix). It is protected by basic HTTP authentication (the credentials were the specified esUserName/esPassword parameters of the ES-MultiNode template). The cluster has also the head plug-in installed (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) for basic cluster administration. |
| Kibana service |http://myBigCluster.westus.cloudapp.azure.com <br /><br />The Kibana service is set up to show data from the created Elasticsearch cluster. It is protected by the same authentication credentials as the cluster itself. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>In-process versus out-of-process trace capturing
In the introduction, we mentioned two fundamental ways of collecting diagnostic data: in-process and out-of-process. Each has strengths and weaknesses.

Advantages of the **in-process trace capturing** include:

1. *Easy configuration and deployment*
   
   * The configuration of diagnostic data collection is just part of the application configuration. It is easy to always keep it "in sync" with the rest of the application.
   * Per-application or per-service configuration is easily achievable.
   * Out-of-process trace capturing usually requires a separate deployment and configuration of the diagnostic agent, which is an extra administrative task and a potential source of errors. The particular agent technology often allows only one instance of the agent per virtual machine (node). This means that configuration for the collection of the diagnostic configuration is shared among all applications and services running on that node.
2. *Flexibility*
   
   * The application can send the data wherever it needs to go, as long as there is a client library that supports the targeted data storage system. New sinks can be added as desired.
   * Complex capture, filtering, and data-aggregation rules can be implemented.
   * An out-of-process trace capturing is often limited by the data sinks that the agent supports. Some agents are extensible.
3. *Access to internal application data and context*
   
   * The diagnostic subsystem running inside the application/service process can easily augment the traces with contextual information.
   * In the out-of-process approach, the data must be sent to an agent via some inter-process communication mechanism, such as Event Tracing for Windows. This mechanism could impose additional limitations.

Advantages of the **out-of-process trace capturing** include:

1. *The ability to monitor the application and collect crash dumps*
   
   * In-process trace capturing may be unsuccessful if the application fails to start or crashes. An independent agent has a much better chance of capturing crucial troubleshooting information.<br /><br />
2. *Maturity, robustness, and proven performance*
   
   * An agent developed by a platform vendor (such as a Microsoft Azure Diagnostics agent) has been subject to rigorous testing and battle-hardening.
   * With in-process trace capturing, care must be taken to ensure that the activity of sending diagnostic data from an application process does not interfere with the application's main tasks or introduce timing or performance problems. An independently running agent is less prone to these issues and is specifically designed to limit its impact on the system.

It is possible to combine and benefit from both approaches. Indeed, it might be the best solution for many applications.

Here, we use the **Microsoft.Diagnostic.Listeners library** and the in-process trace capturing to send data from a Service Fabric application to an Elasticsearch cluster.

## <a name="use-the-listeners-library-to-send-diagnostic-data-to-elasticsearch"></a>Use the Listeners library to send diagnostic data to Elasticsearch
The Microsoft.Diagnostic.Listeners library is part of PartyCluster sample Service Fabric application. To use it:

1. Download [the PartyCluster sample](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) from GitHub.
2. Copy the Microsoft.Diagnostics.Listeners and Microsoft.Diagnostics.Listeners.Fabric projects (whole folders) from the PartyCluster sample directory to the solution folder of the application that is supposed to send the data to Elasticsearch.
3. Open the target solution, right-click the solution node in the Solution Explorer, and choose **Add Existing Project**. Add the Microsoft.Diagnostics.Listeners project to the solution. Repeat the same for the Microsoft.Diagnostics.Listeners.Fabric project.
4. Add a project reference from your service project(s) to the two added projects. (Each service that is supposed to send data to Elasticsearch should reference Microsoft.Diagnostics.EventListeners and Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![Project references to Microsoft.Diagnostics.EventListeners and Microsoft.Diagnostics.EventListeners.Fabric libraries][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Service Fabric General Availability release and Microsoft.Diagnostics.Tracing Nuget package
Applications built with Service Fabric General Availability release (2.0.135, released March 31, 2016) target **.NET Framework 4.5.2**. This version is the highest version of the .NET Framework supported by Azure at the time of the GA release. Unfortunately, this version of the framework lacks certain EventListener APIs that the Microsoft.Diagnostics.Listeners library needs. Because EventSource (the component that forms the basis of logging APIs in Fabric applications) and EventListener are tightly coupled, every project that uses the Microsoft.Diagnostics.Listeners library must use an alternative implementation of EventSource. This implementation is provided by the **Microsoft.Diagnostics.Tracing Nuget package**, authored by Microsoft. The package is fully backward-compatible with EventSource included in the framework, so no code changes should be necessary other than referenced namespace changes.

To start using the Microsoft.Diagnostics.Tracing implementation of the EventSource class, follow these steps for each service project that needs to send data to Elasticsearch:

1. Right-click on the service project and choose **Manage Nuget Packages**.
2. Switch to the nuget.org package source (if it is not already selected) and search for "**Microsoft.Diagnostics.Tracing**".
3. Install the `Microsoft.Diagnostics.Tracing.EventSource` package (and its dependencies).
4. Open the **ServiceEventSource.cs** or **ActorEventSource.cs** file in your service project and replace the `using System.Diagnostics.Tracing` directive on top of the file with the `using Microsoft.Diagnostics.Tracing` directive.

These steps will not be necessary once the **.NET Framework 4.6** is supported by Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Elasticsearch listener instantiation and configuration
The final step for sending diagnostic data to Elasticsearch is to create an instance of `ElasticSearchListener` and configure it with Elasticsearch connection data. The listener automatically captures all events raised via EventSource classes defined in the service project. It needs to be alive during the lifetime of the service, so the best place to create it is in the service initialization code. Here is how the initialization code for a stateless service could look after the necessary changes (additions pointed out in comments starting with `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add the following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is the entry point of the service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // The ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name to a .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of the class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that the ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Elasticsearch connection data should be put in a separate section in the service configuration file (**PackageRoot\Config\Settings.xml**). The name of the section must correspond to the value passed to the `FabricConfigurationProvider` constructor, for example:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
The values of `serviceUri`, `userName` and `password` parameters correspond to the Elasticsearch cluster endpoint address, Elasticsearch user name, and password, respectively. `indexNamePrefix` is the prefix for Elasticsearch indexes; the Microsoft.Diagnostics.Listeners library creates a new index for its data daily.

### <a name="verification"></a>Verification
That's it! Now, whenever the service is run, it starts sending traces to the Elasticsearch service specified in the configuration. You can verify this by opening the Kibana UI associated with the target Elasticsearch instance. In our example, the page address is http://myBigCluster.westus.cloudapp.azure.com/. Check that indexes with the name prefix chosen for the `ElasticSearchListener` instance have indeed been created and populated with data.

![Kibana showing PartyCluster application events][2]

## <a name="next-steps"></a>Next steps
* [Learn more about diagnosing and monitoring a Service Fabric service](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png

