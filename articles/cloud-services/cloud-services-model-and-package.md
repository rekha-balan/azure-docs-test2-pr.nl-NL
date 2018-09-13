---
title: What is a Cloud Service model and package | Microsoft Docs
description: Describes the cloud service model (.csdef, .cscfg) and package (.cspkg) in Azure
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 7aebd5bd168799e1a88bad0e78ba3a164bfcfccd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553858"
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="50590-103">What is the Cloud Service model and how do I package it?</span><span class="sxs-lookup"><span data-stu-id="50590-103">What is the Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="50590-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="50590-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="50590-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span><span class="sxs-lookup"><span data-stu-id="50590-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span></span> <span data-ttu-id="50590-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span><span class="sxs-lookup"><span data-stu-id="50590-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span></span> <span data-ttu-id="50590-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="50590-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="50590-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span><span class="sxs-lookup"><span data-stu-id="50590-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span></span>

## <a name="what-would-you-like-to-know-more-about"></a><span data-ttu-id="50590-109">What would you like to know more about?</span><span class="sxs-lookup"><span data-stu-id="50590-109">What would you like to know more about?</span></span>
* <span data-ttu-id="50590-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span><span class="sxs-lookup"><span data-stu-id="50590-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="50590-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span><span class="sxs-lookup"><span data-stu-id="50590-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="50590-112">I want to create the [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="50590-112">I want to create the [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="50590-113">I am using Visual Studio and I want to...</span><span class="sxs-lookup"><span data-stu-id="50590-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="50590-114">[Create a cloud service][vs_create]</span><span class="sxs-lookup"><span data-stu-id="50590-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="50590-115">[Reconfigure an existing cloud service][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="50590-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="50590-116">[Deploy a Cloud Service project][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="50590-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="50590-117">[Remote desktop into a cloud service instance][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="50590-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="50590-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="50590-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="50590-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span><span class="sxs-lookup"><span data-stu-id="50590-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span></span> <span data-ttu-id="50590-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span><span class="sxs-lookup"><span data-stu-id="50590-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span></span> <span data-ttu-id="50590-121">The following example shows the settings that can be defined for the Web and Worker roles:</span><span class="sxs-lookup"><span data-stu-id="50590-121">The following example shows the settings that can be defined for the Web and Worker roles:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="50590-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span><span class="sxs-lookup"><span data-stu-id="50590-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span></span>

<span data-ttu-id="50590-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="50590-123">**Sites**</span></span>  
<span data-ttu-id="50590-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span><span class="sxs-lookup"><span data-stu-id="50590-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="50590-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="50590-125">**InputEndpoints**</span></span>  
<span data-ttu-id="50590-126">Contains the definitions for endpoints that are used to contact the cloud service.</span><span class="sxs-lookup"><span data-stu-id="50590-126">Contains the definitions for endpoints that are used to contact the cloud service.</span></span>

<span data-ttu-id="50590-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="50590-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="50590-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="50590-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span></span>

<span data-ttu-id="50590-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="50590-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="50590-130">Contains the setting definitions for features of a specific role.</span><span class="sxs-lookup"><span data-stu-id="50590-130">Contains the setting definitions for features of a specific role.</span></span>

<span data-ttu-id="50590-131">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="50590-131">**Certificates**</span></span>  
<span data-ttu-id="50590-132">Contains the definitions for certificates that are needed for a role.</span><span class="sxs-lookup"><span data-stu-id="50590-132">Contains the definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="50590-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="50590-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span></span>

<span data-ttu-id="50590-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="50590-134">**LocalResources**</span></span>  
<span data-ttu-id="50590-135">Contains the definitions for local storage resources.</span><span class="sxs-lookup"><span data-stu-id="50590-135">Contains the definitions for local storage resources.</span></span> <span data-ttu-id="50590-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span><span class="sxs-lookup"><span data-stu-id="50590-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="50590-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="50590-137">**Imports**</span></span>  
<span data-ttu-id="50590-138">Contains the definitions for imported modules.</span><span class="sxs-lookup"><span data-stu-id="50590-138">Contains the definitions for imported modules.</span></span> <span data-ttu-id="50590-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="50590-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="50590-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="50590-140">**Startup**</span></span>  
<span data-ttu-id="50590-141">Contains tasks that are run when the role starts.</span><span class="sxs-lookup"><span data-stu-id="50590-141">Contains tasks that are run when the role starts.</span></span> <span data-ttu-id="50590-142">The tasks are defined in a .cmd or executable file.</span><span class="sxs-lookup"><span data-stu-id="50590-142">The tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="50590-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="50590-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="50590-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span><span class="sxs-lookup"><span data-stu-id="50590-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="50590-145">You specify the number of instances that you want to deploy for each role in this file.</span><span class="sxs-lookup"><span data-stu-id="50590-145">You specify the number of instances that you want to deploy for each role in this file.</span></span> <span data-ttu-id="50590-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="50590-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span></span> <span data-ttu-id="50590-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span><span class="sxs-lookup"><span data-stu-id="50590-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span></span> <span data-ttu-id="50590-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span><span class="sxs-lookup"><span data-stu-id="50590-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span></span>

<span data-ttu-id="50590-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span><span class="sxs-lookup"><span data-stu-id="50590-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span></span> <span data-ttu-id="50590-150">You can upload a new service configuration file without redeploying your cloud service.</span><span class="sxs-lookup"><span data-stu-id="50590-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="50590-151">The configuration values for the cloud service can be changed while the cloud service is running.</span><span class="sxs-lookup"><span data-stu-id="50590-151">The configuration values for the cloud service can be changed while the cloud service is running.</span></span> <span data-ttu-id="50590-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span><span class="sxs-lookup"><span data-stu-id="50590-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span></span>

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="50590-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span><span class="sxs-lookup"><span data-stu-id="50590-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span></span>

<span data-ttu-id="50590-154">**Instances**</span><span class="sxs-lookup"><span data-stu-id="50590-154">**Instances**</span></span>  
<span data-ttu-id="50590-155">Configures the number of running instances for the role.</span><span class="sxs-lookup"><span data-stu-id="50590-155">Configures the number of running instances for the role.</span></span> <span data-ttu-id="50590-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span><span class="sxs-lookup"><span data-stu-id="50590-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="50590-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span><span class="sxs-lookup"><span data-stu-id="50590-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="50590-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="50590-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="50590-159">Configures the settings for the running instances for a role.</span><span class="sxs-lookup"><span data-stu-id="50590-159">Configures the settings for the running instances for a role.</span></span> <span data-ttu-id="50590-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span><span class="sxs-lookup"><span data-stu-id="50590-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span></span>

<span data-ttu-id="50590-161">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="50590-161">**Certificates**</span></span>  
<span data-ttu-id="50590-162">Configures the certificates that are used by the service.</span><span class="sxs-lookup"><span data-stu-id="50590-162">Configures the certificates that are used by the service.</span></span> <span data-ttu-id="50590-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span><span class="sxs-lookup"><span data-stu-id="50590-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span></span> <span data-ttu-id="50590-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span><span class="sxs-lookup"><span data-stu-id="50590-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="50590-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span><span class="sxs-lookup"><span data-stu-id="50590-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span></span> <span data-ttu-id="50590-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50590-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="50590-167">Defining ports for role instances</span><span class="sxs-lookup"><span data-stu-id="50590-167">Defining ports for role instances</span></span>
<span data-ttu-id="50590-168">Azure allows only one entry point to a web role.</span><span class="sxs-lookup"><span data-stu-id="50590-168">Azure allows only one entry point to a web role.</span></span> <span data-ttu-id="50590-169">Meaning that all traffic occurs through one IP address.</span><span class="sxs-lookup"><span data-stu-id="50590-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="50590-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span><span class="sxs-lookup"><span data-stu-id="50590-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span></span> <span data-ttu-id="50590-171">You can also configure your applications to listen to well-known ports on the IP address.</span><span class="sxs-lookup"><span data-stu-id="50590-171">You can also configure your applications to listen to well-known ports on the IP address.</span></span>

<span data-ttu-id="50590-172">The following sample shows the configuration for a web role with a website and web application.</span><span class="sxs-lookup"><span data-stu-id="50590-172">The following sample shows the configuration for a web role with a website and web application.</span></span> <span data-ttu-id="50590-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span><span class="sxs-lookup"><span data-stu-id="50590-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-the-configuration-of-a-role"></a><span data-ttu-id="50590-174">Changing the configuration of a role</span><span class="sxs-lookup"><span data-stu-id="50590-174">Changing the configuration of a role</span></span>
<span data-ttu-id="50590-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span><span class="sxs-lookup"><span data-stu-id="50590-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span></span> <span data-ttu-id="50590-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span><span class="sxs-lookup"><span data-stu-id="50590-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span></span> <span data-ttu-id="50590-177">The following changes can be made to the configuration of a service:</span><span class="sxs-lookup"><span data-stu-id="50590-177">The following changes can be made to the configuration of a service:</span></span>

* <span data-ttu-id="50590-178">**Changing the values of configuration settings**</span><span class="sxs-lookup"><span data-stu-id="50590-178">**Changing the values of configuration settings**</span></span>  
  <span data-ttu-id="50590-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span><span class="sxs-lookup"><span data-stu-id="50590-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span></span>
* <span data-ttu-id="50590-180">**Changing the service topology of role instances**</span><span class="sxs-lookup"><span data-stu-id="50590-180">**Changing the service topology of role instances**</span></span>  
  <span data-ttu-id="50590-181">Topology changes do not affect running instances, except where an instance is being removed.</span><span class="sxs-lookup"><span data-stu-id="50590-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="50590-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span><span class="sxs-lookup"><span data-stu-id="50590-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span></span>
* <span data-ttu-id="50590-183">**Changing the certificate thumbprint**</span><span class="sxs-lookup"><span data-stu-id="50590-183">**Changing the certificate thumbprint**</span></span>  
  <span data-ttu-id="50590-184">You can only update a certificate when a role instance is offline.</span><span class="sxs-lookup"><span data-stu-id="50590-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="50590-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span><span class="sxs-lookup"><span data-stu-id="50590-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="50590-186">Handling configuration changes with Service Runtime Events</span><span class="sxs-lookup"><span data-stu-id="50590-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="50590-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span><span class="sxs-lookup"><span data-stu-id="50590-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span></span> <span data-ttu-id="50590-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span><span class="sxs-lookup"><span data-stu-id="50590-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="50590-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span><span class="sxs-lookup"><span data-stu-id="50590-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="50590-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span><span class="sxs-lookup"><span data-stu-id="50590-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span></span>
* <span data-ttu-id="50590-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span><span class="sxs-lookup"><span data-stu-id="50590-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="50590-192">Occurs after the configuration change is applied to a specified instance of a role.</span><span class="sxs-lookup"><span data-stu-id="50590-192">Occurs after the configuration change is applied to a specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="50590-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span><span class="sxs-lookup"><span data-stu-id="50590-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="50590-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="50590-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="50590-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span><span class="sxs-lookup"><span data-stu-id="50590-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span></span> <span data-ttu-id="50590-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50590-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span></span>

<span data-ttu-id="50590-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span><span class="sxs-lookup"><span data-stu-id="50590-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span></span> <span data-ttu-id="50590-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="50590-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="50590-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="50590-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span></span>

<span data-ttu-id="50590-200">**CSPack** is located at</span><span class="sxs-lookup"><span data-stu-id="50590-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="50590-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span><span class="sxs-lookup"><span data-stu-id="50590-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span></span>  
> 
> <span data-ttu-id="50590-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span><span class="sxs-lookup"><span data-stu-id="50590-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="50590-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span><span class="sxs-lookup"><span data-stu-id="50590-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span></span> <span data-ttu-id="50590-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span><span class="sxs-lookup"><span data-stu-id="50590-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span></span>
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a><span data-ttu-id="50590-205">Example command to package a cloud service</span><span class="sxs-lookup"><span data-stu-id="50590-205">Example command to package a cloud service</span></span>
<span data-ttu-id="50590-206">The following example creates an application package that contains the information for a web role.</span><span class="sxs-lookup"><span data-stu-id="50590-206">The following example creates an application package that contains the information for a web role.</span></span> <span data-ttu-id="50590-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span><span class="sxs-lookup"><span data-stu-id="50590-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="50590-208">If the application contains both a web role and a worker role, the following command is used:</span><span class="sxs-lookup"><span data-stu-id="50590-208">If the application contains both a web role and a worker role, the following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="50590-209">Where the variables are defined as follows:</span><span class="sxs-lookup"><span data-stu-id="50590-209">Where the variables are defined as follows:</span></span>

| <span data-ttu-id="50590-210">Variable</span><span class="sxs-lookup"><span data-stu-id="50590-210">Variable</span></span> | <span data-ttu-id="50590-211">Value</span><span class="sxs-lookup"><span data-stu-id="50590-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="50590-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="50590-212">\[DirectoryName\]</span></span> |<span data-ttu-id="50590-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span><span class="sxs-lookup"><span data-stu-id="50590-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span></span> |
| <span data-ttu-id="50590-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="50590-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="50590-215">The name of the service definition file.</span><span class="sxs-lookup"><span data-stu-id="50590-215">The name of the service definition file.</span></span> <span data-ttu-id="50590-216">By default, this file is named ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="50590-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="50590-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="50590-217">\[OutputFileName\]</span></span> |<span data-ttu-id="50590-218">The name for the generated package file.</span><span class="sxs-lookup"><span data-stu-id="50590-218">The name for the generated package file.</span></span> <span data-ttu-id="50590-219">Typically, this is set to the name of the application.</span><span class="sxs-lookup"><span data-stu-id="50590-219">Typically, this is set to the name of the application.</span></span> <span data-ttu-id="50590-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span><span class="sxs-lookup"><span data-stu-id="50590-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="50590-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="50590-221">\[RoleName\]</span></span> |<span data-ttu-id="50590-222">The name of the role as defined in the service definition file.</span><span class="sxs-lookup"><span data-stu-id="50590-222">The name of the role as defined in the service definition file.</span></span> |
| <span data-ttu-id="50590-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="50590-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="50590-224">The location of the binary files for the role.</span><span class="sxs-lookup"><span data-stu-id="50590-224">The location of the binary files for the role.</span></span> |
| <span data-ttu-id="50590-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="50590-225">\[VirtualPath\]</span></span> |<span data-ttu-id="50590-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span><span class="sxs-lookup"><span data-stu-id="50590-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span></span> |
| <span data-ttu-id="50590-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="50590-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="50590-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span><span class="sxs-lookup"><span data-stu-id="50590-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span></span> |
| <span data-ttu-id="50590-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="50590-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="50590-230">The name of the binary file for the role.</span><span class="sxs-lookup"><span data-stu-id="50590-230">The name of the binary file for the role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="50590-231">Next steps</span><span class="sxs-lookup"><span data-stu-id="50590-231">Next steps</span></span>
<span data-ttu-id="50590-232">I'm creating a cloud service package and I want to...</span><span class="sxs-lookup"><span data-stu-id="50590-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="50590-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="50590-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="50590-234">[Deploy a Cloud Service project][deploy]</span><span class="sxs-lookup"><span data-stu-id="50590-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="50590-235">I am using Visual Studio and I want to...</span><span class="sxs-lookup"><span data-stu-id="50590-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="50590-236">[Create a new cloud service][vs_create]</span><span class="sxs-lookup"><span data-stu-id="50590-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="50590-237">[Reconfigure an existing cloud service][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="50590-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="50590-238">[Deploy a Cloud Service project][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="50590-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="50590-239">[Setup remote desktop for a cloud service instance][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="50590-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
