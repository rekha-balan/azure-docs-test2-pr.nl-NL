---
title: Secure an Azure Service Fabric cluster on Windows using certs | Microsoft Docs
description: This article describes how to secure communication within the standalone or private cluster as well as between clients and the cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: ryanwi
ms.openlocfilehash: 8f8d6b4d76a0c519075cad9d0af4779663c85dcb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562716"
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="93941-103">Secure a standalone cluster on Windows using X.509 certificates</span><span class="sxs-lookup"><span data-stu-id="93941-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="93941-104">This article describes how to secure the communication between the various nodes of your standalone Windows cluster, as well as how to authenticate clients connecting to this cluster, using X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="93941-104">This article describes how to secure the communication between the various nodes of your standalone Windows cluster, as well as how to authenticate clients connecting to this cluster, using X.509 certificates.</span></span> <span data-ttu-id="93941-105">This ensures that only authorized users can access the cluster, the deployed applications and perform management tasks.</span><span class="sxs-lookup"><span data-stu-id="93941-105">This ensures that only authorized users can access the cluster, the deployed applications and perform management tasks.</span></span>  <span data-ttu-id="93941-106">Certificate security should be enabled on the cluster when the cluster is created.</span><span class="sxs-lookup"><span data-stu-id="93941-106">Certificate security should be enabled on the cluster when the cluster is created.</span></span>  

<span data-ttu-id="93941-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="93941-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="93941-108">Which certificates will you need?</span><span class="sxs-lookup"><span data-stu-id="93941-108">Which certificates will you need?</span></span>
<span data-ttu-id="93941-109">To start with, [download the standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) to one of the nodes in your cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-109">To start with, [download the standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) to one of the nodes in your cluster.</span></span> <span data-ttu-id="93941-110">In the downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span><span class="sxs-lookup"><span data-stu-id="93941-110">In the downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="93941-111">Open the file and review the section for **security** under the **properties** section:</span><span class="sxs-lookup"><span data-stu-id="93941-111">Open the file and review the section for **security** under the **properties** section:</span></span>

```JSON
"security": {
    "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            }, 
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint" : "[Thumbprint]",
                "IsAdmin": true
            }
        ]
        "ReverseProxyCertificate":{
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        }
    }
}
```

<span data-ttu-id="93941-112">This section describes the certificates that you need for securing your standalone Windows cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-112">This section describes the certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="93941-113">If you are specifying a cluster certificate, set the value of **ClusterCredentialType** to _**X509**_.</span><span class="sxs-lookup"><span data-stu-id="93941-113">If you are specifying a cluster certificate, set the value of **ClusterCredentialType** to _**X509**_.</span></span> <span data-ttu-id="93941-114">If you are specifying server certificate for outside connections, set the **ServerCredentialType** to _**X509**_.</span><span class="sxs-lookup"><span data-stu-id="93941-114">If you are specifying server certificate for outside connections, set the **ServerCredentialType** to _**X509**_.</span></span> <span data-ttu-id="93941-115">Although not mandatory, we recommend to have both these certificates for a properly secured cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-115">Although not mandatory, we recommend to have both these certificates for a properly secured cluster.</span></span> <span data-ttu-id="93941-116">If you set these values to *X509* then you must also specify the corresponding certificates or Service Fabric will throw an exception.</span><span class="sxs-lookup"><span data-stu-id="93941-116">If you set these values to *X509* then you must also specify the corresponding certificates or Service Fabric will throw an exception.</span></span> <span data-ttu-id="93941-117">In some scenarios, you may only want to specify the _ClientCertificateThumbprints_ or _ReverseProxyCertificate_.</span><span class="sxs-lookup"><span data-stu-id="93941-117">In some scenarios, you may only want to specify the _ClientCertificateThumbprints_ or _ReverseProxyCertificate_.</span></span> <span data-ttu-id="93941-118">In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ to _X509_.</span><span class="sxs-lookup"><span data-stu-id="93941-118">In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ to _X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="93941-119">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is the primary identity of a certificate.</span><span class="sxs-lookup"><span data-stu-id="93941-119">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is the primary identity of a certificate.</span></span> <span data-ttu-id="93941-120">Read [How to retrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) to find out the thumbprint of the certificates that you create.</span><span class="sxs-lookup"><span data-stu-id="93941-120">Read [How to retrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) to find out the thumbprint of the certificates that you create.</span></span>
> 
> 

<span data-ttu-id="93941-121">The following table lists the certificates that you will need on your cluster setup:</span><span class="sxs-lookup"><span data-stu-id="93941-121">The following table lists the certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="93941-122">**CertificateInformation Setting**</span><span class="sxs-lookup"><span data-stu-id="93941-122">**CertificateInformation Setting**</span></span> | <span data-ttu-id="93941-123">**Description**</span><span class="sxs-lookup"><span data-stu-id="93941-123">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="93941-124">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="93941-124">ClusterCertificate</span></span> |<span data-ttu-id="93941-125">This certificate is required to secure the communication between the nodes on a cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-125">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="93941-126">You can use two different certificates, a primary and a secondary for upgrade.</span><span class="sxs-lookup"><span data-stu-id="93941-126">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="93941-127">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span><span class="sxs-lookup"><span data-stu-id="93941-127">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="93941-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="93941-128">ServerCertificate</span></span> |<span data-ttu-id="93941-129">This certificate is presented to the client when it tries to connect to this cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-129">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="93941-130">For convenience, you can choose to use the same certificate for *ClusterCertificate* and *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="93941-130">For convenience, you can choose to use the same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="93941-131">You can use two different server certificates, a primary and a secondary for upgrade.</span><span class="sxs-lookup"><span data-stu-id="93941-131">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="93941-132">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span><span class="sxs-lookup"><span data-stu-id="93941-132">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="93941-133">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="93941-133">ClientCertificateThumbprints</span></span> |<span data-ttu-id="93941-134">This is a set of certificates that you want to install on the authenticated clients.</span><span class="sxs-lookup"><span data-stu-id="93941-134">This is a set of certificates that you want to install on the authenticated clients.</span></span> <span data-ttu-id="93941-135">You can have a number of different client certificates installed on the machines that you want to allow access to the cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-135">You can have a number of different client certificates installed on the machines that you want to allow access to the cluster.</span></span> <span data-ttu-id="93941-136">Set the thumbprint of each certificate in the **CertificateThumbprint** variable.</span><span class="sxs-lookup"><span data-stu-id="93941-136">Set the thumbprint of each certificate in the **CertificateThumbprint** variable.</span></span> <span data-ttu-id="93941-137">If you set the **IsAdmin** to *true*, then the client with this certificate installed on it can do administrator management activities on the cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-137">If you set the **IsAdmin** to *true*, then the client with this certificate installed on it can do administrator management activities on the cluster.</span></span> <span data-ttu-id="93941-138">If the **IsAdmin** is *false*, the client with this certificate can only perform the actions allowed for user access rights, typically read-only.</span><span class="sxs-lookup"><span data-stu-id="93941-138">If the **IsAdmin** is *false*, the client with this certificate can only perform the actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="93941-139">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="93941-139">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="93941-140">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="93941-140">ClientCertificateCommonNames</span></span> |<span data-ttu-id="93941-141">Set the common name of the first client certificate for the **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="93941-141">Set the common name of the first client certificate for the **CertificateCommonName**.</span></span> <span data-ttu-id="93941-142">The **CertificateIssuerThumbprint** is the thumbprint for the issuer of this certificate.</span><span class="sxs-lookup"><span data-stu-id="93941-142">The **CertificateIssuerThumbprint** is the thumbprint for the issuer of this certificate.</span></span> <span data-ttu-id="93941-143">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) to know more about common names and the issuer.</span><span class="sxs-lookup"><span data-stu-id="93941-143">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) to know more about common names and the issuer.</span></span> |
| <span data-ttu-id="93941-144">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="93941-144">ReverseProxyCertificate</span></span> |<span data-ttu-id="93941-145">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="93941-145">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="93941-146">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span><span class="sxs-lookup"><span data-stu-id="93941-146">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="93941-147">Here is example cluster configuration where the Cluster, Server, and Client certificates have been provided.</span><span class="sxs-lookup"><span data-stu-id="93941-147">Here is example cluster configuration where the Cluster, Server, and Client certificates have been provided.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace the localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificate": {
                    "Thumbprint": "a8 13 67 58 f4 ab 89 62 af 2b f3 f2 79 21 be 1d f6 7f 43 26",
                    "X509StoreName": "My"
                },
                "ServerCertificate": {
                    "Thumbprint": "a8 13 67 58 f4 ab 89 62 af 2b f3 f2 79 21 be 1d f6 7f 43 26",
                    "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="acquire-the-x509-certificates"></a><span data-ttu-id="93941-148">Acquire the X.509 certificates</span><span class="sxs-lookup"><span data-stu-id="93941-148">Acquire the X.509 certificates</span></span>
<span data-ttu-id="93941-149">To secure communication within the cluster, you will first need to obtain X.509 certificates for your cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="93941-149">To secure communication within the cluster, you will first need to obtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="93941-150">Additionally, to limit connection to this cluster to authorized machines/users, you will need to obtain and install certificates for the client machines.</span><span class="sxs-lookup"><span data-stu-id="93941-150">Additionally, to limit connection to this cluster to authorized machines/users, you will need to obtain and install certificates for the client machines.</span></span>

<span data-ttu-id="93941-151">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate to secure the cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-151">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate to secure the cluster.</span></span> <span data-ttu-id="93941-152">For details on obtaining these certificates, go to [How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="93941-152">For details on obtaining these certificates, go to [How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="93941-153">For clusters that you use for test purposes, you can choose to use a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="93941-153">For clusters that you use for test purposes, you can choose to use a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="93941-154">Optional: Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="93941-154">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="93941-155">One way to create a self-signed cert that can be secured correctly is to use the *CertSetup.ps1* script in the Service Fabric SDK folder in the directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="93941-155">One way to create a self-signed cert that can be secured correctly is to use the *CertSetup.ps1* script in the Service Fabric SDK folder in the directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="93941-156">Edit this file to change the default name of the certificate (look for the value *CN=ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="93941-156">Edit this file to change the default name of the certificate (look for the value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="93941-157">Run this script as `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="93941-157">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="93941-158">Now export the certificate to a PFX file with a protected password.</span><span class="sxs-lookup"><span data-stu-id="93941-158">Now export the certificate to a PFX file with a protected password.</span></span> <span data-ttu-id="93941-159">First get the thumbprint of the certificate.</span><span class="sxs-lookup"><span data-stu-id="93941-159">First get the thumbprint of the certificate.</span></span> <span data-ttu-id="93941-160">From the *Start* menu, run the *Manage computer certificates*.</span><span class="sxs-lookup"><span data-stu-id="93941-160">From the *Start* menu, run the *Manage computer certificates*.</span></span> <span data-ttu-id="93941-161">Navigate to the **Local Computer\Personal** folder and find the certificate you just created.</span><span class="sxs-lookup"><span data-stu-id="93941-161">Navigate to the **Local Computer\Personal** folder and find the certificate you just created.</span></span> <span data-ttu-id="93941-162">Double-click the certificate to open it, select the *Details* tab and scroll down to the *Thumbprint* field.</span><span class="sxs-lookup"><span data-stu-id="93941-162">Double-click the certificate to open it, select the *Details* tab and scroll down to the *Thumbprint* field.</span></span> <span data-ttu-id="93941-163">Copy the thumbprint value into the PowerShell command below, after removing the spaces.</span><span class="sxs-lookup"><span data-stu-id="93941-163">Copy the thumbprint value into the PowerShell command below, after removing the spaces.</span></span>  <span data-ttu-id="93941-164">Change the `String` value to a suitable secure password to protect it and run the following in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="93941-164">Change the `String` value to a suitable secure password to protect it and run the following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="93941-165">To see the details of a certificate installed on the machine you can run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="93941-165">To see the details of a certificate installed on the machine you can run the following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="93941-166">Alternatively, if you have an Azure subscription, follow the section [Add certificates to Key Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="93941-166">Alternatively, if you have an Azure subscription, follow the section [Add certificates to Key Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-the-certificates"></a><span data-ttu-id="93941-167">Install the certificates</span><span class="sxs-lookup"><span data-stu-id="93941-167">Install the certificates</span></span>
<span data-ttu-id="93941-168">Once you have certificate(s), you can install them on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="93941-168">Once you have certificate(s), you can install them on the cluster nodes.</span></span> <span data-ttu-id="93941-169">Your nodes need to have the latest Windows PowerShell 3.x installed on them.</span><span class="sxs-lookup"><span data-stu-id="93941-169">Your nodes need to have the latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="93941-170">You will need to repeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span><span class="sxs-lookup"><span data-stu-id="93941-170">You will need to repeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="93941-171">Copy the .pfx file(s) to the node.</span><span class="sxs-lookup"><span data-stu-id="93941-171">Copy the .pfx file(s) to the node.</span></span>
2. <span data-ttu-id="93941-172">Open a PowerShell window as an administrator and enter the following commands.</span><span class="sxs-lookup"><span data-stu-id="93941-172">Open a PowerShell window as an administrator and enter the following commands.</span></span> <span data-ttu-id="93941-173">Replace the *$pswd* with the password that you used to create this certificate.</span><span class="sxs-lookup"><span data-stu-id="93941-173">Replace the *$pswd* with the password that you used to create this certificate.</span></span> <span data-ttu-id="93941-174">Replace the *$PfxFilePath* with the full path of the .pfx copied to this node.</span><span class="sxs-lookup"><span data-stu-id="93941-174">Replace the *$PfxFilePath* with the full path of the .pfx copied to this node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="93941-175">Now set the access control on this certificate so that the Service Fabric process, which runs under the Network Service account, can use it by running the following script.</span><span class="sxs-lookup"><span data-stu-id="93941-175">Now set the access control on this certificate so that the Service Fabric process, which runs under the Network Service account, can use it by running the following script.</span></span> <span data-ttu-id="93941-176">Provide the thumbprint of the certificate and "NETWORK SERVICE" for the service account.</span><span class="sxs-lookup"><span data-stu-id="93941-176">Provide the thumbprint of the certificate and "NETWORK SERVICE" for the service account.</span></span> <span data-ttu-id="93941-177">You can check that the ACLs on the certificate are correct by opening the certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span><span class="sxs-lookup"><span data-stu-id="93941-177">You can check that the ACLs on the certificate are correct by opening the certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify the user, the permissions and the permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of the machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get the current acl of the private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add the new ace to the acl of the private key
    $acl.SetAccessRule($accessRule)
   
    # Write back the new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe the access rights currently assigned to this certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="93941-178">Repeat the steps above for each server certificate.</span><span class="sxs-lookup"><span data-stu-id="93941-178">Repeat the steps above for each server certificate.</span></span> <span data-ttu-id="93941-179">You can also use these steps to install the client certificates on the machines that you want to allow access to the cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-179">You can also use these steps to install the client certificates on the machines that you want to allow access to the cluster.</span></span>

## <a name="create-the-secure-cluster"></a><span data-ttu-id="93941-180">Create the secure cluster</span><span class="sxs-lookup"><span data-stu-id="93941-180">Create the secure cluster</span></span>
<span data-ttu-id="93941-181">After configuring the **security** section of the **ClusterConfig.X509.MultiMachine.json** file, you can proceed to [Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section to configure the nodes and create the standalone cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-181">After configuring the **security** section of the **ClusterConfig.X509.MultiMachine.json** file, you can proceed to [Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section to configure the nodes and create the standalone cluster.</span></span> <span data-ttu-id="93941-182">Remember to use the **ClusterConfig.X509.MultiMachine.json** file while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-182">Remember to use the **ClusterConfig.X509.MultiMachine.json** file while creating the cluster.</span></span> <span data-ttu-id="93941-183">For example, your command might look like the following:</span><span class="sxs-lookup"><span data-stu-id="93941-183">For example, your command might look like the following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="93941-184">Once you have the secure standalone Windows cluster successfully running, and have setup the authenticated clients to connect to it, follow the section [Connect to a secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) to connect to it.</span><span class="sxs-lookup"><span data-stu-id="93941-184">Once you have the secure standalone Windows cluster successfully running, and have setup the authenticated clients to connect to it, follow the section [Connect to a secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) to connect to it.</span></span> <span data-ttu-id="93941-185">For example:</span><span class="sxs-lookup"><span data-stu-id="93941-185">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="93941-186">You can then run other PowerShell commands to work with this cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-186">You can then run other PowerShell commands to work with this cluster.</span></span> <span data-ttu-id="93941-187">For example, [Get-ServiceFabricNode](/powershell/servicefabric/vlatest/get-servicefabricnode.md) to show a list of nodes on this secure cluster.</span><span class="sxs-lookup"><span data-stu-id="93941-187">For example, [Get-ServiceFabricNode](/powershell/servicefabric/vlatest/get-servicefabricnode.md) to show a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="93941-188">To remove the cluster, connect to the node on the cluster where you downloaded the Service Fabric package, open a command line and navigate to the package folder.</span><span class="sxs-lookup"><span data-stu-id="93941-188">To remove the cluster, connect to the node on the cluster where you downloaded the Service Fabric package, open a command line and navigate to the package folder.</span></span> <span data-ttu-id="93941-189">Now run the following command:</span><span class="sxs-lookup"><span data-stu-id="93941-189">Now run the following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="93941-190">Incorrect certificate configuration may prevent the cluster from coming up during deployment.</span><span class="sxs-lookup"><span data-stu-id="93941-190">Incorrect certificate configuration may prevent the cluster from coming up during deployment.</span></span> <span data-ttu-id="93941-191">To self-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="93941-191">To self-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

