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
# <a name="connect-to-a-secure-cluster"></a>Connect to a secure cluster
When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD). This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.  Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.  For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md). If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster. 

<a id="connectsecureclustercli"></a> 

## <a name="connect-to-a-secure-cluster-using-azure-cli"></a>Connect to a secure cluster using Azure CLI
The following Azure CLI commands describe how to connect to a secure cluster. 

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a>Connect to a secure cluster using a client certificate
The certificate details must match a certificate on the cluster nodes. 

If your certificate has Certificate Authorities (CAs), you need to add the parameter `--ca-cert-path` as shown in the following example: 

```
 azure servicefabric cluster connect --connection-endpoint https://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```
If you have multiple CAs, use commas as the delimiter. 

If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification. 

```
azure servicefabric cluster connect --connection-endpoint https://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 --strict-ssl-false 
```

If you would like to skip the CA verification, you could add the ``--reject-unauthorized-false`` parameter, like the following command:

```
azure servicefabric cluster connect --connection-endpoint https://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

For connecting to a cluster secured with a self-signed certificate, use the following command removing both the CA verification and Common Name verification:

```
azure servicefabric cluster connect --connection-endpoint https://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false --reject-unauthorized-false
```

After you connect, you should be able to [run other CLI commands](service-fabric-azure-cli.md) to interact with the cluster. 

<a id="connectsecurecluster"></a>

## <a name="connect-to-a-cluster-using-powershell"></a>Connect to a cluster using PowerShell
Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster. The cluster connection is used for all subsequent commands in the given PowerShell session.

### <a name="connect-to-an-unsecure-cluster"></a>Connect to an unsecure cluster

To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a>Connect to a secure cluster using Azure Active Directory

To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a>Connect to a secure cluster using a client certificate
Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access. Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management. The certificate details must match a certificate on the cluster nodes.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes. *FindValue* is the thumbprint of the admin client certificate.
When the parameters are filled in, the command looks like the following example: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-to-a-secure-cluster-using-windows-active-directory"></a>Connect to a secure cluster using Windows Active Directory
If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-to-a-cluster-using-the-fabricclient-apis"></a>Connect to a cluster using the FabricClient APIs
The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management. To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.

### <a name="connect-to-an-unsecure-cluster"></a>Connect to an unsecure cluster

To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address. FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a>Connect to a secure cluster using a client certificate

The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient). Following this process enables mutual authentication between the client and the cluster nodes.

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

### <a name="connect-to-a-secure-cluster-interactively-using-azure-active-directory"></a>Connect to a secure cluster interactively using Azure Active Directory

The following example uses Azure Active Directory for client identity and server certificate for server identity.

A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.

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

### <a name="connect-to-a-secure-cluster-non-interactively-using-azure-active-directory"></a>Connect to a secure cluster non-interactively using Azure Active Directory

The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.

For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).

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

### <a name="connect-to-a-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a>Connect to a secure cluster without prior metadata knowledge using Azure Active Directory

The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience. The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.

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

## <a name="connect-to-a-secure-cluster-using-service-fabric-explorer"></a>Connect to a secure cluster using Service Fabric Explorer
To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:

`http://<your-cluster-endpoint>:19080/Explorer`

The full URL is also available in the cluster essentials pane of the Azure portal.

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a>Connect to a secure cluster using Azure Active Directory

To connect to a cluster that is secured with AAD, point your browser to:

`https://<your-cluster-endpoint>:19080/Explorer`

You are automatically be prompted to log in with AAD.

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a>Connect to a secure cluster using a client certificate

To connect to a cluster that is secured with certificates, point your browser to:

`https://<your-cluster-endpoint>:19080/Explorer`

You are automatically be prompted to select a client certificate.

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-the-remote-computer"></a>Set up a client certificate on the remote computer
At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.  We recommend that you also use additional secondary certificates and client access certificates.  To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate. The certificate can be installed into the Personal (My) store of the local computer or the current user.  You also need the thumbprint of the server certificate so that the client can authenticate the cluster.

Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a>Next steps
* [Service Fabric Cluster upgrade process and expectations from you](service-fabric-cluster-upgrade.md)
* [Managing your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).
* [Service Fabric Health model introduction](service-fabric-health-introduction.md)
* [Application Security and RunAs](service-fabric-application-runas-security.md)

