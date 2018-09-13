---
title: Azure Service Fabric application deployment | Microsoft Docs
description: Use the FabricClient APIs to deploy and remove applications in Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/10/2017
ms.author: ryanwi
ms.openlocfilehash: 4c7a92352d4fef6a0e55b608bf5c957cd2c40332
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661179"
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>Deploy and remove applications using FabricClient
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient APIs](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster. Deployment involves the following three steps:

1. Upload the application package to the image store
2. Register the application type
3. Create the application instance

After an app is deployed and an instance is running in the cluster, you can delete the app instance and its application type. To completely remove an app from the cluster involves the following steps:

1. Remove (or delete) the running application instance
2. Unregister the application type if you no longer need it
3. Remove the application package from the image store

If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.  This script is found in the *Scripts* folder of the application project. This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio. 
 
## <a name="connect-to-the-cluster"></a>Connect to the cluster
Connect to the cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of the code examples in this article. For examples of connecting to a local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).  To connect to the local development cluster, run the following:

```csharp
// Connect to the local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-the-application-package"></a>Upload the application package
Suppose you build and package an app named *MyApplication* in Visual Studio. By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".  The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\username\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.

Uploading the application package puts it in a location that's accessible by internal Service Fabric components.
If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.

The [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method uploads the application package to the cluster image store. 

If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it to the imagestore using PowerShell. The compression reduces the size and the number of files.

See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.

## <a name="register-the-application-package"></a>Register the application package
The application type and version declared in the application manifest become available for use when the app package is registered. The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.  

The [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) method registers the application type in the cluster and make it available for deployment.

The [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) method lists all successfully registered application type versions and their registration status. You can use this command to determine when the registration is done.

## <a name="create-an-application-instance"></a>Create an application instance
You can instantiate an application from any application type version that has been registered successfully by using the [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) method. The name of each application must start with the *fabric:* scheme and be unique for each application instance. Any default services defined in the application manifest of the target application type are also created.

Multiple application instances can be created for any given version of a registered application type. Each application instance runs in isolation, with its own work directory and process.

To see which named apps and services are running in the cluster, run the [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) methods.

## <a name="create-a-service-instance"></a>Create a service instance
You can instantiate a service from a service type using the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) method.  If the service is declared as a default service in the application manifest, the service is instantiated with the application is instantiated.  Calling the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) method for a service that is already instantiated will return an exception. 

## <a name="remove-a-service-instance"></a>Remove a service instance
When a service instance is no longer needed, you can remove it from the running application instance by calling the [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) method.  This operation cannot be reversed, and service state cannot be recovered.

## <a name="remove-an-application-instance"></a>Remove an application instance
When an application instance is no longer needed, you can permanently remove it by name using the [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) method. [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong to the application as well, permanently removing all service state. This operation cannot be reversed, and application state cannot be recovered.

## <a name="unregister-an-application-type"></a>Unregister an application type
When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) method. Unregistering unused application types releases storage space used by the image store. An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.

## <a name="remove-an-application-package-from-the-image-store"></a>Remove an application package from the image store
When an application package is no longer needed, you can delete it from the image store to free up system resources using the [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) method.

## <a name="troubleshooting"></a>Troubleshooting
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString
The Service Fabric SDK environment should already have the correct defaults set up. But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using. You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/dotnet/api/system.fabric.fabricclient.clustermanagementclient.getclustermanifestasync) method.

The ImageStoreConnectionString is found in the cluster manifest:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.

### <a name="deploy-large-application-package"></a>Deploy large application package
Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method times out for a large application package (order of GB).
Try:
- Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter. By default, the timeout is 30 minutes.
- Check the network connection between your source machine and cluster. If the connection is slow, consider using a machine with a better network connection.
If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.
- Check if you are hitting external throttling. For example, when the image store is configured to use azure storage, upload may be throttled.

Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) method times out. Try:
- [Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.
The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform. The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.
- Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) method with `timeout` parameter.

### <a name="deploy-application-package-with-many-files"></a>Deploy application package with many files
Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).
Try:
- [Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store. The compression reduces the number of files.
- Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.

## <a name="code-example"></a>Code example
The following example copies an application package to the image store, provisions the application type, creates an application instance, creates a service instance, removes the application instance, un-provisions the application type, and deletes the application package from the image store.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\Users\username\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug";
    string serviceType = "Stateless1Type";

    // Connect to the cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy the application package to a location in the image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied to {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy to Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision the application.  "MyApplicationV1" is the folder in the image store where the app package is located. 
    // The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) 
    // is now registered in the cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create the application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create the stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create the service instance.  If the service is declared as a default service in the ApplicationManifest.xml,
    // the service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from the application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision the application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete the application package from a location in the image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>Next steps
[Service Fabric application upgrade](service-fabric-application-upgrade.md)

[Service Fabric health introduction](service-fabric-health-introduction.md)

[Diagnose and troubleshoot a Service Fabric service](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Model an application in Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md