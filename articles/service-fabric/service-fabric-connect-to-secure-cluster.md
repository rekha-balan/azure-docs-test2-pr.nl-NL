---
title: Connect securely to an Azure Service Fabric cluster | Microsoft Docs
description: Describes how to authenticate client access to a Service Fabric cluster and how to secure communication between clients and a cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: ryanwi
ms.openlocfilehash: e44ecf5860becffb39d199e36d36d96f50bf7cf3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671104"
---
# <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="7c2d2-103">Connect to a secure cluster</span><span class="sxs-lookup"><span data-stu-id="7c2d2-103">Connect to a secure cluster</span></span>
<span data-ttu-id="7c2d2-104">When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="7c2d2-104">When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="7c2d2-105">This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-105">This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="7c2d2-106">Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-106">Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.</span></span>  <span data-ttu-id="7c2d2-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="7c2d2-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="7c2d2-108">If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-108">If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-to-a-secure-cluster-using-azure-cli"></a><span data-ttu-id="7c2d2-109">Connect to a secure cluster using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7c2d2-109">Connect to a secure cluster using Azure CLI</span></span>
<span data-ttu-id="7c2d2-110">The following Azure CLI commands describe how to connect to a secure cluster.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-110">The following Azure CLI commands describe how to connect to a secure cluster.</span></span> 

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="7c2d2-111">Connect to a secure cluster using a client certificate</span><span class="sxs-lookup"><span data-stu-id="7c2d2-111">Connect to a secure cluster using a client certificate</span></span>
<span data-ttu-id="7c2d2-112">The certificate details must match a certificate on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-112">The certificate details must match a certificate on the cluster nodes.</span></span> 

<span data-ttu-id="7c2d2-113">If your certificate has Certificate Authorities (CAs), you need to add the parameter `--ca-cert-path` as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="7c2d2-113">If your certificate has Certificate Authorities (CAs), you need to add the parameter `--ca-cert-path` as shown in the following example:</span></span> 

```
 azure servicefabric cluster connect --connection-endpoint https://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```
<span data-ttu-id="7c2d2-114">If you have multiple CAs, use commas as the delimiter.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-114">If you have multiple CAs, use commas as the delimiter.</span></span> 

<span data-ttu-id="7c2d2-115">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-115">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification.</span></span> 

```
azure servicefabric cluster connect --connection-endpoint https://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 --strict-ssl-false 
```

<span data-ttu-id="7c2d2-116">If you would like to skip the CA verification, you could add the ``--reject-unauthorized-false`` parameter, like the following command:</span><span class="sxs-lookup"><span data-stu-id="7c2d2-116">If you would like to skip the CA verification, you could add the ``--reject-unauthorized-false`` parameter, like the following command:</span></span>

```
azure servicefabric cluster connect --connection-endpoint https://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="7c2d2-117">For connecting to a cluster secured with a self-signed certificate, use the following command removing both the CA verification and Common Name verification:</span><span class="sxs-lookup"><span data-stu-id="7c2d2-117">For connecting to a cluster secured with a self-signed certificate, use the following command removing both the CA verification and Common Name verification:</span></span>

```
azure servicefabric cluster connect --connection-endpoint https://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false --reject-unauthorized-false
```

<span data-ttu-id="7c2d2-118">After you connect, you should be able to [run other CLI commands](service-fabric-azure-cli.md) to interact with the cluster.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-118">After you connect, you should be able to [run other CLI commands](service-fabric-azure-cli.md) to interact with the cluster.</span></span> 

<a id="connectsecurecluster"></a>

## <a name="connect-to-a-cluster-using-powershell"></a><span data-ttu-id="7c2d2-119">Connect to a cluster using PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c2d2-119">Connect to a cluster using PowerShell</span></span>
<span data-ttu-id="7c2d2-120">Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-120">Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster.</span></span> <span data-ttu-id="7c2d2-121">The cluster connection is used for all subsequent commands in the given PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-121">The cluster connection is used for all subsequent commands in the given PowerShell session.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="7c2d2-122">Connect to an unsecure cluster</span><span class="sxs-lookup"><span data-stu-id="7c2d2-122">Connect to an unsecure cluster</span></span>

<span data-ttu-id="7c2d2-123">To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:</span><span class="sxs-lookup"><span data-stu-id="7c2d2-123">To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="7c2d2-124">Connect to a secure cluster using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c2d2-124">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="7c2d2-125">To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-125">To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="7c2d2-126">Connect to a secure cluster using a client certificate</span><span class="sxs-lookup"><span data-stu-id="7c2d2-126">Connect to a secure cluster using a client certificate</span></span>
<span data-ttu-id="7c2d2-127">Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-127">Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access.</span></span> <span data-ttu-id="7c2d2-128">Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-128">Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="7c2d2-129">The certificate details must match a certificate on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-129">The certificate details must match a certificate on the cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="7c2d2-130">*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-130">*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes.</span></span> <span data-ttu-id="7c2d2-131">*FindValue* is the thumbprint of the admin client certificate.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-131">*FindValue* is the thumbprint of the admin client certificate.</span></span>
<span data-ttu-id="7c2d2-132">When the parameters are filled in, the command looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="7c2d2-132">When the parameters are filled in, the command looks like the following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-to-a-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="7c2d2-133">Connect to a secure cluster using Windows Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c2d2-133">Connect to a secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="7c2d2-134">If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".</span><span class="sxs-lookup"><span data-stu-id="7c2d2-134">If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-to-a-cluster-using-the-fabricclient-apis"></a><span data-ttu-id="7c2d2-135">Connect to a cluster using the FabricClient APIs</span><span class="sxs-lookup"><span data-stu-id="7c2d2-135">Connect to a cluster using the FabricClient APIs</span></span>
<span data-ttu-id="7c2d2-136">The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-136">The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="7c2d2-137">To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-137">To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="7c2d2-138">Connect to an unsecure cluster</span><span class="sxs-lookup"><span data-stu-id="7c2d2-138">Connect to an unsecure cluster</span></span>

<span data-ttu-id="7c2d2-139">To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:</span><span class="sxs-lookup"><span data-stu-id="7c2d2-139">To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="7c2d2-140">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-140">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address.</span></span> <span data-ttu-id="7c2d2-141">FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-141">FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="7c2d2-142">Connect to a secure cluster using a client certificate</span><span class="sxs-lookup"><span data-stu-id="7c2d2-142">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="7c2d2-143">The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="7c2d2-143">The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="7c2d2-144">Following this process enables mutual authentication between the client and the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-144">Following this process enables mutual authentication between the client and the cluster nodes.</span></span>

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-to-a-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="7c2d2-145">Connect to a secure cluster interactively using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c2d2-145">Connect to a secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="7c2d2-146">The following example uses Azure Active Directory for client identity and server certificate for server identity.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-146">The following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="7c2d2-147">A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-147">A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-to-a-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="7c2d2-148">Connect to a secure cluster non-interactively using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c2d2-148">Connect to a secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="7c2d2-149">The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-149">The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="7c2d2-150">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c2d2-150">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-to-a-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="7c2d2-151">Connect to a secure cluster without prior metadata knowledge using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c2d2-151">Connect to a secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="7c2d2-152">The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-152">The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience.</span></span> <span data-ttu-id="7c2d2-153">The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-153">The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-to-a-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="7c2d2-154">Connect to a secure cluster using Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="7c2d2-154">Connect to a secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="7c2d2-155">To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span><span class="sxs-lookup"><span data-stu-id="7c2d2-155">To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="7c2d2-156">The full URL is also available in the cluster essentials pane of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-156">The full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="7c2d2-157">Connect to a secure cluster using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c2d2-157">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="7c2d2-158">To connect to a cluster that is secured with AAD, point your browser to:</span><span class="sxs-lookup"><span data-stu-id="7c2d2-158">To connect to a cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="7c2d2-159">You are automatically be prompted to log in with AAD.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-159">You are automatically be prompted to log in with AAD.</span></span>

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="7c2d2-160">Connect to a secure cluster using a client certificate</span><span class="sxs-lookup"><span data-stu-id="7c2d2-160">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="7c2d2-161">To connect to a cluster that is secured with certificates, point your browser to:</span><span class="sxs-lookup"><span data-stu-id="7c2d2-161">To connect to a cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="7c2d2-162">You are automatically be prompted to select a client certificate.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-162">You are automatically be prompted to select a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-the-remote-computer"></a><span data-ttu-id="7c2d2-163">Set up a client certificate on the remote computer</span><span class="sxs-lookup"><span data-stu-id="7c2d2-163">Set up a client certificate on the remote computer</span></span>
<span data-ttu-id="7c2d2-164">At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-164">At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="7c2d2-165">We recommend that you also use additional secondary certificates and client access certificates.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-165">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="7c2d2-166">To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-166">To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate.</span></span> <span data-ttu-id="7c2d2-167">The certificate can be installed into the Personal (My) store of the local computer or the current user.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-167">The certificate can be installed into the Personal (My) store of the local computer or the current user.</span></span>  <span data-ttu-id="7c2d2-168">You also need the thumbprint of the server certificate so that the client can authenticate the cluster.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-168">You also need the thumbprint of the server certificate so that the client can authenticate the cluster.</span></span>

<span data-ttu-id="7c2d2-169">Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-169">Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="7c2d2-170">If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.</span><span class="sxs-lookup"><span data-stu-id="7c2d2-170">If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="7c2d2-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c2d2-171">Next steps</span></span>
* [<span data-ttu-id="7c2d2-172">Service Fabric Cluster upgrade process and expectations from you</span><span class="sxs-lookup"><span data-stu-id="7c2d2-172">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* <span data-ttu-id="7c2d2-173">[Managing your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="7c2d2-173">[Managing your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>
* [<span data-ttu-id="7c2d2-174">Service Fabric Health model introduction</span><span class="sxs-lookup"><span data-stu-id="7c2d2-174">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="7c2d2-175">Application Security and RunAs</span><span class="sxs-lookup"><span data-stu-id="7c2d2-175">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)

