---
title: Deploy a Node.js application that uses MongoDB | Microsoft Docs
description: Walkthrough on how to package multiple guest executables to deploy to an Azure Service Fabric cluster
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: ''
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: d967d70c7fad45f7a10a5288623440491dcfffa3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669115"
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="48d2c-103">Deploy multiple guest executables</span><span class="sxs-lookup"><span data-stu-id="48d2c-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="48d2c-104">This article shows how to package and deploy multiple guest executables to Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="48d2c-104">This article shows how to package and deploy multiple guest executables to Azure Service Fabric.</span></span> <span data-ttu-id="48d2c-105">For building and deploying a single Service Fabric package read how to [deploy a guest executable to Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="48d2c-105">For building and deploying a single Service Fabric package read how to [deploy a guest executable to Service Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="48d2c-106">While this walkthrough shows how to deploy an application with a Node.js front end that uses MongoDB as the data store, you can apply the steps to any application that has dependencies on another application.</span><span class="sxs-lookup"><span data-stu-id="48d2c-106">While this walkthrough shows how to deploy an application with a Node.js front end that uses MongoDB as the data store, you can apply the steps to any application that has dependencies on another application.</span></span>   

<span data-ttu-id="48d2c-107">You can use Visual Studio to produce the application package that contains multiple guest executables.</span><span class="sxs-lookup"><span data-stu-id="48d2c-107">You can use Visual Studio to produce the application package that contains multiple guest executables.</span></span> <span data-ttu-id="48d2c-108">See [Using Visual Studio to package an existing application](service-fabric-deploy-existing-app.md#use-visual-studio-to-package-an-existing-executable).</span><span class="sxs-lookup"><span data-stu-id="48d2c-108">See [Using Visual Studio to package an existing application](service-fabric-deploy-existing-app.md#use-visual-studio-to-package-an-existing-executable).</span></span> <span data-ttu-id="48d2c-109">After you have added the first guest executable, right click on the application project and select the **Add->New Service Fabric service** to add the second guest executable project to the solution.</span><span class="sxs-lookup"><span data-stu-id="48d2c-109">After you have added the first guest executable, right click on the application project and select the **Add->New Service Fabric service** to add the second guest executable project to the solution.</span></span> <span data-ttu-id="48d2c-110">Note: If you choose to link the source in the Visual Studio project, building the Visual Studio solution, will make sure that your application package is up to date with changes in the source.</span><span class="sxs-lookup"><span data-stu-id="48d2c-110">Note: If you choose to link the source in the Visual Studio project, building the Visual Studio solution, will make sure that your application package is up to date with changes in the source.</span></span> 

## <a name="samples"></a><span data-ttu-id="48d2c-111">Samples</span><span class="sxs-lookup"><span data-stu-id="48d2c-111">Samples</span></span>
* [<span data-ttu-id="48d2c-112">Sample for packaging and deploying a guest executable</span><span class="sxs-lookup"><span data-stu-id="48d2c-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="48d2c-113">Sample of two guest exectuables (C# and nodejs) communicating via the Naming service using REST</span><span class="sxs-lookup"><span data-stu-id="48d2c-113">Sample of two guest exectuables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-the-multiple-guest-executable-application"></a><span data-ttu-id="48d2c-114">Manually package the multiple guest executable application</span><span class="sxs-lookup"><span data-stu-id="48d2c-114">Manually package the multiple guest executable application</span></span>
<span data-ttu-id="48d2c-115">Alternatively you can manually package the guest executable.</span><span class="sxs-lookup"><span data-stu-id="48d2c-115">Alternatively you can manually package the guest executable.</span></span> <span data-ttu-id="48d2c-116">For the manual packaging, this article uses the Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="48d2c-116">For the manual packaging, this article uses the Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-the-nodejs-application"></a><span data-ttu-id="48d2c-117">Packaging the Node.js application</span><span class="sxs-lookup"><span data-stu-id="48d2c-117">Packaging the Node.js application</span></span>
<span data-ttu-id="48d2c-118">This article assumes that Node.js is not installed on the nodes in the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="48d2c-118">This article assumes that Node.js is not installed on the nodes in the Service Fabric cluster.</span></span> <span data-ttu-id="48d2c-119">As a consequence, you need to add Node.exe to the root directory of your node application before packaging.</span><span class="sxs-lookup"><span data-stu-id="48d2c-119">As a consequence, you need to add Node.exe to the root directory of your node application before packaging.</span></span> <span data-ttu-id="48d2c-120">The directory structure of the Node.js application (using Express web framework and Jade template engine) should look similar to the one below:</span><span class="sxs-lookup"><span data-stu-id="48d2c-120">The directory structure of the Node.js application (using Express web framework and Jade template engine) should look similar to the one below:</span></span>

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

<span data-ttu-id="48d2c-121">As a next step, you create an application package for the Node.js application.</span><span class="sxs-lookup"><span data-stu-id="48d2c-121">As a next step, you create an application package for the Node.js application.</span></span> <span data-ttu-id="48d2c-122">The code below creates a Service Fabric application package that contains the Node.js application.</span><span class="sxs-lookup"><span data-stu-id="48d2c-122">The code below creates a Service Fabric application package that contains the Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="48d2c-123">Below is a description of the parameters that are being used:</span><span class="sxs-lookup"><span data-stu-id="48d2c-123">Below is a description of the parameters that are being used:</span></span>

* <span data-ttu-id="48d2c-124">**/source** points to the directory of the application that should be packaged.</span><span class="sxs-lookup"><span data-stu-id="48d2c-124">**/source** points to the directory of the application that should be packaged.</span></span>
* <span data-ttu-id="48d2c-125">**/target** defines the directory in which the package should be created.</span><span class="sxs-lookup"><span data-stu-id="48d2c-125">**/target** defines the directory in which the package should be created.</span></span> <span data-ttu-id="48d2c-126">This directory has to be different from the source directory.</span><span class="sxs-lookup"><span data-stu-id="48d2c-126">This directory has to be different from the source directory.</span></span>
* <span data-ttu-id="48d2c-127">**/appname** defines the application name of the existing application.</span><span class="sxs-lookup"><span data-stu-id="48d2c-127">**/appname** defines the application name of the existing application.</span></span> <span data-ttu-id="48d2c-128">It's important to understand that this translates to the service name in the manifest, and not to the Service Fabric application name.</span><span class="sxs-lookup"><span data-stu-id="48d2c-128">It's important to understand that this translates to the service name in the manifest, and not to the Service Fabric application name.</span></span>
* <span data-ttu-id="48d2c-129">**/exe** defines the executable that Service Fabric is supposed to launch, in this case `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="48d2c-129">**/exe** defines the executable that Service Fabric is supposed to launch, in this case `node.exe`.</span></span>
* <span data-ttu-id="48d2c-130">**/ma** defines the argument that is being used to launch the executable.</span><span class="sxs-lookup"><span data-stu-id="48d2c-130">**/ma** defines the argument that is being used to launch the executable.</span></span> <span data-ttu-id="48d2c-131">As Node.js is not installed, Service Fabric needs to launch the Node.js web server by executing `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="48d2c-131">As Node.js is not installed, Service Fabric needs to launch the Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="48d2c-132">`/ma:'bin/www'` tells the packaging tool to use `bin/ma` as the argument for node.exe.</span><span class="sxs-lookup"><span data-stu-id="48d2c-132">`/ma:'bin/www'` tells the packaging tool to use `bin/ma` as the argument for node.exe.</span></span>
* <span data-ttu-id="48d2c-133">**/AppType** defines the Service Fabric application type name.</span><span class="sxs-lookup"><span data-stu-id="48d2c-133">**/AppType** defines the Service Fabric application type name.</span></span>

<span data-ttu-id="48d2c-134">If you browse to the directory that was specified in the /target parameter, you can see that the tool has created a fully functioning Service Fabric package as shown below:</span><span class="sxs-lookup"><span data-stu-id="48d2c-134">If you browse to the directory that was specified in the /target parameter, you can see that the tool has created a fully functioning Service Fabric package as shown below:</span></span>

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="48d2c-135">The generated ServiceManifest.xml now has a section that describes how the Node.js web server should be launched, as shown in the code snippet below:</span><span class="sxs-lookup"><span data-stu-id="48d2c-135">The generated ServiceManifest.xml now has a section that describes how the Node.js web server should be launched, as shown in the code snippet below:</span></span>

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
<span data-ttu-id="48d2c-136">In this sample, the Node.js web server listens to port 3000, so you need to update the endpoint information in the ServiceManifest.xml file as shown below.</span><span class="sxs-lookup"><span data-stu-id="48d2c-136">In this sample, the Node.js web server listens to port 3000, so you need to update the endpoint information in the ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-the-mongodb-application"></a><span data-ttu-id="48d2c-137">Packaging the MongoDB application</span><span class="sxs-lookup"><span data-stu-id="48d2c-137">Packaging the MongoDB application</span></span>
<span data-ttu-id="48d2c-138">Now that you have packaged the Node.js application, you can go ahead and package MongoDB.</span><span class="sxs-lookup"><span data-stu-id="48d2c-138">Now that you have packaged the Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="48d2c-139">As mentioned before, the steps that you go through now are not specific to Node.js and MongoDB.</span><span class="sxs-lookup"><span data-stu-id="48d2c-139">As mentioned before, the steps that you go through now are not specific to Node.js and MongoDB.</span></span> <span data-ttu-id="48d2c-140">In fact, they apply to all applications that are meant to be packaged together as one Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="48d2c-140">In fact, they apply to all applications that are meant to be packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="48d2c-141">To package MongoDB, you want to make sure you package Mongod.exe and Mongo.exe.</span><span class="sxs-lookup"><span data-stu-id="48d2c-141">To package MongoDB, you want to make sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="48d2c-142">Both binaries are located in the `bin` directory of your MongoDB installation directory.</span><span class="sxs-lookup"><span data-stu-id="48d2c-142">Both binaries are located in the `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="48d2c-143">The directory structure looks similar to the one below.</span><span class="sxs-lookup"><span data-stu-id="48d2c-143">The directory structure looks similar to the one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="48d2c-144">Service Fabric needs to start MongoDB with a command similar to the one below, so you need to use the `/ma` parameter when packaging MongoDB.</span><span class="sxs-lookup"><span data-stu-id="48d2c-144">Service Fabric needs to start MongoDB with a command similar to the one below, so you need to use the `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path to data]
```
> [!NOTE]
> <span data-ttu-id="48d2c-145">The data is not being preserved in the case of a node failure if you put the MongoDB data directory on the local directory of the node.</span><span class="sxs-lookup"><span data-stu-id="48d2c-145">The data is not being preserved in the case of a node failure if you put the MongoDB data directory on the local directory of the node.</span></span> <span data-ttu-id="48d2c-146">You should either use durable storage or implement a MongoDB replica set in order to prevent data loss.</span><span class="sxs-lookup"><span data-stu-id="48d2c-146">You should either use durable storage or implement a MongoDB replica set in order to prevent data loss.</span></span>  
>
>

<span data-ttu-id="48d2c-147">In PowerShell or the command shell, we run the packaging tool with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="48d2c-147">In PowerShell or the command shell, we run the packaging tool with the following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path to data]' /AppType:NodeAppType
```

<span data-ttu-id="48d2c-148">In order to add MongoDB to your Service Fabric application package, you need to make sure that the /target parameter points to the same directory that already contains the application manifest along with the Node.js application.</span><span class="sxs-lookup"><span data-stu-id="48d2c-148">In order to add MongoDB to your Service Fabric application package, you need to make sure that the /target parameter points to the same directory that already contains the application manifest along with the Node.js application.</span></span> <span data-ttu-id="48d2c-149">You also need to make sure that you are using the same ApplicationType name.</span><span class="sxs-lookup"><span data-stu-id="48d2c-149">You also need to make sure that you are using the same ApplicationType name.</span></span>

<span data-ttu-id="48d2c-150">Let's browse to the directory and examine what the tool has created.</span><span class="sxs-lookup"><span data-stu-id="48d2c-150">Let's browse to the directory and examine what the tool has created.</span></span>

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="48d2c-151">As you can see, the tool added a new folder, MongoDB, to the directory that contains the MongoDB binaries.</span><span class="sxs-lookup"><span data-stu-id="48d2c-151">As you can see, the tool added a new folder, MongoDB, to the directory that contains the MongoDB binaries.</span></span> <span data-ttu-id="48d2c-152">If you open the `ApplicationManifest.xml` file, you can see that the package now contains both the Node.js application and MongoDB.</span><span class="sxs-lookup"><span data-stu-id="48d2c-152">If you open the `ApplicationManifest.xml` file, you can see that the package now contains both the Node.js application and MongoDB.</span></span> <span data-ttu-id="48d2c-153">The code below shows the content of the application manifest.</span><span class="sxs-lookup"><span data-stu-id="48d2c-153">The code below shows the content of the application manifest.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-the-application"></a><span data-ttu-id="48d2c-154">Publishing the application</span><span class="sxs-lookup"><span data-stu-id="48d2c-154">Publishing the application</span></span>
<span data-ttu-id="48d2c-155">The last step is to publish the application to the local Service Fabric cluster by using the PowerShell scripts below:</span><span class="sxs-lookup"><span data-stu-id="48d2c-155">The last step is to publish the application to the local Service Fabric cluster by using the PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="48d2c-156">Once the application is successfully published to the local cluster, you can access the Node.js application on the port that we have entered in the service manifest of the Node.js application--for example http://localhost:3000.</span><span class="sxs-lookup"><span data-stu-id="48d2c-156">Once the application is successfully published to the local cluster, you can access the Node.js application on the port that we have entered in the service manifest of the Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="48d2c-157">In this tutorial, you have seen how to easily package two existing applications as one Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="48d2c-157">In this tutorial, you have seen how to easily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="48d2c-158">You have also learned how to deploy it to Service Fabric so that it can benefit from some of the Service Fabric features, such as high availability and health system integration.</span><span class="sxs-lookup"><span data-stu-id="48d2c-158">You have also learned how to deploy it to Service Fabric so that it can benefit from some of the Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-to-an-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="48d2c-159">Adding more guest executables to an existing application using Yeoman on Linux</span><span class="sxs-lookup"><span data-stu-id="48d2c-159">Adding more guest executables to an existing application using Yeoman on Linux</span></span>

<span data-ttu-id="48d2c-160">To add another service to an application already created using `yo`, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48d2c-160">To add another service to an application already created using `yo`, perform the following steps:</span></span> 
1. <span data-ttu-id="48d2c-161">Change directory to the root of the existing application.</span><span class="sxs-lookup"><span data-stu-id="48d2c-161">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="48d2c-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span><span class="sxs-lookup"><span data-stu-id="48d2c-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="48d2c-163">Run `yo azuresfguest:AddService` and provide the necessary details.</span><span class="sxs-lookup"><span data-stu-id="48d2c-163">Run `yo azuresfguest:AddService` and provide the necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48d2c-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="48d2c-164">Next steps</span></span>
* <span data-ttu-id="48d2c-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="48d2c-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="48d2c-166">Sample for packaging and deploying a guest executable</span><span class="sxs-lookup"><span data-stu-id="48d2c-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="48d2c-167">Sample of two guest exectuables (C# and nodejs) communicating via the Naming service using REST</span><span class="sxs-lookup"><span data-stu-id="48d2c-167">Sample of two guest exectuables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
