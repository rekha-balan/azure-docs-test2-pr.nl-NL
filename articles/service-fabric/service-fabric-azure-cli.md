---
title: Interacting with Service Fabric clusters using CLI | Microsoft Docs
description: How to use Azure CLI to interact with a Service Fabric cluster
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: subramar
ms.openlocfilehash: ec89c1ec999fa8d66338f61ecb2f409a0a4058a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554084"
---
# <a name="using-the-azure-cli-to-interact-with-a-service-fabric-cluster"></a><span data-ttu-id="a0774-103">Using the Azure CLI to interact with a Service Fabric Cluster</span><span class="sxs-lookup"><span data-stu-id="a0774-103">Using the Azure CLI to interact with a Service Fabric Cluster</span></span>
<span data-ttu-id="a0774-104">You can interact with Service Fabric cluster from Linux machines using the Azure CLI on Linux.</span><span class="sxs-lookup"><span data-stu-id="a0774-104">You can interact with Service Fabric cluster from Linux machines using the Azure CLI on Linux.</span></span>

<span data-ttu-id="a0774-105">The first step is get the latest version of the CLI from the git rep and set it up in your path using the following commands:</span><span class="sxs-lookup"><span data-stu-id="a0774-105">The first step is get the latest version of the CLI from the git rep and set it up in your path using the following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="a0774-106">For each command, it supports, you can type the name of the command to obtain the help for that command.</span><span class="sxs-lookup"><span data-stu-id="a0774-106">For each command, it supports, you can type the name of the command to obtain the help for that command.</span></span> <span data-ttu-id="a0774-107">Auto-completion is supported for the commands.</span><span class="sxs-lookup"><span data-stu-id="a0774-107">Auto-completion is supported for the commands.</span></span> <span data-ttu-id="a0774-108">For example, the following command gives you help for all the application commands.</span><span class="sxs-lookup"><span data-stu-id="a0774-108">For example, the following command gives you help for all the application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="a0774-109">You can further filter the help to a specific command, as the following example shows:</span><span class="sxs-lookup"><span data-stu-id="a0774-109">You can further filter the help to a specific command, as the following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="a0774-110">To enable auto-completion in the CLI, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="a0774-110">To enable auto-completion in the CLI, run the following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="a0774-111">The following commands connect to the cluster and show you the nodes in the cluster:</span><span class="sxs-lookup"><span data-stu-id="a0774-111">The following commands connect to the cluster and show you the nodes in the cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="a0774-112">To use named parameters, and find what they are, you can type --help after a command.</span><span class="sxs-lookup"><span data-stu-id="a0774-112">To use named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="a0774-113">For example:</span><span class="sxs-lookup"><span data-stu-id="a0774-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="a0774-114">When connecting to a multi-machine cluster from a machine **that is not part of the cluster**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a0774-114">When connecting to a multi-machine cluster from a machine **that is not part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="a0774-115">Replace the PublicIPorFQDN tag with the real IP or FQDN as appropriate.</span><span class="sxs-lookup"><span data-stu-id="a0774-115">Replace the PublicIPorFQDN tag with the real IP or FQDN as appropriate.</span></span> <span data-ttu-id="a0774-116">When connecting to a multi-machine cluster from a machine **that is part of the cluster**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a0774-116">When connecting to a multi-machine cluster from a machine **that is part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="a0774-117">You can use PowerShell or CLI to interact with your Linux Service Fabric Cluster created through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a0774-117">You can use PowerShell or CLI to interact with your Linux Service Fabric Cluster created through the Azure portal.</span></span> 

> [!WARNING]
> <span data-ttu-id="a0774-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding the public IP address in the cluster manifest.</span><span class="sxs-lookup"><span data-stu-id="a0774-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding the public IP address in the cluster manifest.</span></span>

## <a name="using-the-azure-cli-to-connect-to-a-service-fabric-cluster"></a><span data-ttu-id="a0774-119">Using the Azure CLI to connect to a Service Fabric Cluster</span><span class="sxs-lookup"><span data-stu-id="a0774-119">Using the Azure CLI to connect to a Service Fabric Cluster</span></span>
<span data-ttu-id="a0774-120">The following Azure CLI commands describe how to connect to a secure cluster.</span><span class="sxs-lookup"><span data-stu-id="a0774-120">The following Azure CLI commands describe how to connect to a secure cluster.</span></span> <span data-ttu-id="a0774-121">The certificate details must match a certificate on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="a0774-121">The certificate details must match a certificate on the cluster nodes.</span></span>

```
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="a0774-122">If your certificate has Certificate Authorities (CAs), you need to add the --ca-cert-path parameter like the following example:</span><span class="sxs-lookup"><span data-stu-id="a0774-122">If your certificate has Certificate Authorities (CAs), you need to add the --ca-cert-path parameter like the following example:</span></span> 

```
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```
<span data-ttu-id="a0774-123">If you have multiple CAs, use a comma as the delimiter.</span><span class="sxs-lookup"><span data-stu-id="a0774-123">If you have multiple CAs, use a comma as the delimiter.</span></span>

<span data-ttu-id="a0774-124">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification as shown in the following command:</span><span class="sxs-lookup"><span data-stu-id="a0774-124">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification as shown in the following command:</span></span> 

```
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="a0774-125">If you would like to skip the CA verification, you could add the --reject-unauthorized-false parameter as shown in the following command:</span><span class="sxs-lookup"><span data-stu-id="a0774-125">If you would like to skip the CA verification, you could add the --reject-unauthorized-false parameter as shown in the following command:</span></span> 

```
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="a0774-126">After you connect, you should be able to run other CLI commands to interact with the cluster.</span><span class="sxs-lookup"><span data-stu-id="a0774-126">After you connect, you should be able to run other CLI commands to interact with the cluster.</span></span> 

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="a0774-127">Deploying your Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="a0774-127">Deploying your Service Fabric application</span></span>
<span data-ttu-id="a0774-128">Execute the following commands to copy, register, and start the service fabric application:</span><span class="sxs-lookup"><span data-stu-id="a0774-128">Execute the following commands to copy, register, and start the service fabric application:</span></span>

```
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```


## <a name="upgrading-your-application"></a><span data-ttu-id="a0774-129">Upgrading your application</span><span class="sxs-lookup"><span data-stu-id="a0774-129">Upgrading your application</span></span>
<span data-ttu-id="a0774-130">The process is similar to the [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="a0774-130">The process is similar to the [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="a0774-131">Build, copy, register, and create your application from project root directory.</span><span class="sxs-lookup"><span data-stu-id="a0774-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="a0774-132">If your application instance is named fabric:/MySFApp, and the type is MySFApp, the commands would be as follows:</span><span class="sxs-lookup"><span data-stu-id="a0774-132">If your application instance is named fabric:/MySFApp, and the type is MySFApp, the commands would be as follows:</span></span>

```
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="a0774-133">Make the change to your application and rebuild the modified service.</span><span class="sxs-lookup"><span data-stu-id="a0774-133">Make the change to your application and rebuild the modified service.</span></span>  <span data-ttu-id="a0774-134">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the Service (and Code or Config or Data as appropriate).</span><span class="sxs-lookup"><span data-stu-id="a0774-134">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="a0774-135">Also modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application, and the modified service.</span><span class="sxs-lookup"><span data-stu-id="a0774-135">Also modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application, and the modified service.</span></span>  <span data-ttu-id="a0774-136">Now, copy and register your updated application using the following commands:</span><span class="sxs-lookup"><span data-stu-id="a0774-136">Now, copy and register your updated application using the following commands:</span></span>

```
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="a0774-137">Now, you can start the application upgrade with the following command:</span><span class="sxs-lookup"><span data-stu-id="a0774-137">Now, you can start the application upgrade with the following command:</span></span>

```
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0  --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="a0774-138">You can now monitor the application upgrade using SFX.</span><span class="sxs-lookup"><span data-stu-id="a0774-138">You can now monitor the application upgrade using SFX.</span></span> <span data-ttu-id="a0774-139">In a few minutes, the application would have been updated.</span><span class="sxs-lookup"><span data-stu-id="a0774-139">In a few minutes, the application would have been updated.</span></span>  <span data-ttu-id="a0774-140">You can also try an updated app with an error and check the auto rollback functionality in service fabric.</span><span class="sxs-lookup"><span data-stu-id="a0774-140">You can also try an updated app with an error and check the auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a><span data-ttu-id="a0774-141">Converting from PFX to PEM and vice versa</span><span class="sxs-lookup"><span data-stu-id="a0774-141">Converting from PFX to PEM and vice versa</span></span>

<span data-ttu-id="a0774-142">You might need to install a certificate in your local machine (with Windows or Linux) to access secure clusters that may be in a different environment.</span><span class="sxs-lookup"><span data-stu-id="a0774-142">You might need to install a certificate in your local machine (with Windows or Linux) to access secure clusters that may be in a different environment.</span></span> <span data-ttu-id="a0774-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need to convert your certificate from PFX to PEM and vice versa.</span><span class="sxs-lookup"><span data-stu-id="a0774-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need to convert your certificate from PFX to PEM and vice versa.</span></span> 

<span data-ttu-id="a0774-144">To convert from a PEM file to a PFX file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a0774-144">To convert from a PEM file to a PFX file, use the following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="a0774-145">To convert from a PFX file to a PEM file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a0774-145">To convert from a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="a0774-146">Refer to [OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span><span class="sxs-lookup"><span data-stu-id="a0774-146">Refer to [OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>
## <a name="troubleshooting"></a><span data-ttu-id="a0774-147">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="a0774-147">Troubleshooting</span></span>
### <a name="copying-of-the-application-package-does-not-succeed"></a><span data-ttu-id="a0774-148">Copying of the application package does not succeed</span><span class="sxs-lookup"><span data-stu-id="a0774-148">Copying of the application package does not succeed</span></span>
<span data-ttu-id="a0774-149">Check if `openssh` is installed.</span><span class="sxs-lookup"><span data-stu-id="a0774-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="a0774-150">By default, Ubuntu Desktop doesn't have it installed.</span><span class="sxs-lookup"><span data-stu-id="a0774-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="a0774-151">Install it using the following command:</span><span class="sxs-lookup"><span data-stu-id="a0774-151">Install it using the following command:</span></span>

```
 sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="a0774-152">If the problem persists, try disabling PAM for ssh by changing the **sshd_config** file using the following commands:</span><span class="sxs-lookup"><span data-stu-id="a0774-152">If the problem persists, try disabling PAM for ssh by changing the **sshd_config** file using the following commands:</span></span>

```sh
 sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
 sudo service sshd reload
```

<span data-ttu-id="a0774-153">If the problem still persists, try increasing the number of ssh sessions by executing the following commands:</span><span class="sxs-lookup"><span data-stu-id="a0774-153">If the problem still persists, try increasing the number of ssh sessions by executing the following commands:</span></span>

```sh
 sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
 sudo service sshd reload
```
<span data-ttu-id="a0774-154">Using keys for ssh authentication (as opposed to passwords) isn't yet supported (since the platform uses ssh to copy packages), so use password authentication instead.</span><span class="sxs-lookup"><span data-stu-id="a0774-154">Using keys for ssh authentication (as opposed to passwords) isn't yet supported (since the platform uses ssh to copy packages), so use password authentication instead.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a0774-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0774-155">Next steps</span></span>
<span data-ttu-id="a0774-156">Set up the development environment and deploy a Service Fabric application to a Linux cluster.</span><span class="sxs-lookup"><span data-stu-id="a0774-156">Set up the development environment and deploy a Service Fabric application to a Linux cluster.</span></span>

