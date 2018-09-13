---
title: Configure secure Azure Service Fabric cluster connections | Microsoft Docs
description: Learn how to use Visual Studio to configure secure connections that are supported by the Azure Service Fabric cluster.
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 10/08/2015
ms.author: cawa
ms.openlocfilehash: f9376b30f8e9d1a693cc3006d40537e0f132e79b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564692"
---
# <a name="configure-secure-connections-to-a-service-fabric-cluster-from-visual-studio"></a>Configure secure connections to a Service Fabric cluster from Visual Studio
Learn how to use Visual Studio to securely access an Azure Service Fabric cluster with access control policies configured.

## <a name="cluster-connection-types"></a>Cluster connection types
Two types of connections are supported by the Azure Service Fabric cluster: **non-secure** connections and **x509 certificate-based** secure connections. (For Service Fabric clusters hosted on-premises, **Windows** and **dSTS** authentications are also supported.) You have to configure the cluster connection type when the cluster is being created. Once it's created, the connection type can’t be changed.

The Visual Studio Service Fabric tools support all authentication types for connecting to a cluster for publishing. See [Setting up a Service Fabric cluster from the Azure portal](service-fabric-cluster-creation-via-portal.md) for instructions on how to set up a secure Service Fabric cluster.

## <a name="configure-cluster-connections-in-publish-profiles"></a>Configure cluster connections in publish profiles
If you publish a Service Fabric project from Visual Studio, use the **Publish Service Fabric Application** dialog box to choose an Azure Service Fabric cluster by clicking the **Select** button in **Connection endpoint** section. You can sign in to your Azure account and then select an existing cluster under your subscriptions.

![The **Publish Service Fabric Application** dialog box is used to configure a Service Fabric connection.][publishdialog]

The **Select Service Fabric Cluster** dialog box automatically validates the cluster connection. If validation passes, it means that your system has the correct certificates installed to connect to the cluster securely, or your cluster is non-secure. Validation failures can be caused by network issues or by not having your system correctly configured to connect to a secure cluster.

![In the **Select Service Fabric Cluster** dialog box, you can configure an existing Service Fabric cluster connection or create and configure a new cluster connection.][selectsfcluster]

### <a name="to-connect-to-a-secure-cluster"></a>To connect to a secure cluster
1. Make sure you can access one of the client certificates that the destination cluster trusts. The certificate is usually shared as a Personal Information Exchange (.pfx) file. See [Setting up a Service Fabric cluster from the Azure portal](service-fabric-cluster-creation-via-portal.md) for how to configure the server to grant access to a client.
2. Install the trusted certificate. To do this, double-click the .pfx file, or use the PowerShell script Import-PfxCertificate to import the certificates. Install the certificate to **Cert:\LocalMachine\My**. It's OK to accept all default settings while importing the certificate.
3. Choose the **Publish...** command on the shortcut menu of the project to open the **Publish Azure Application** dialog box and then select the target cluster. The tool automatically resolves the connection and saves the secure connection parameters in the publish profile.
4. [Optional]: You can edit the publish profile to specify a secure cluster connection.
   
   Since you're manually editing the Publish Profile XML file to specify the certificate information, be sure to note the certificate store name, store location, and certificate thumbprint. You'll need to provide these values for the certificate's store name and store location. See [How to: Retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) for more information.
   
   You can use the *ClusterConnectionParameters* parameters to specify the PowerShell parameters to use when connecting to the Service Fabric cluster. Valid parameters are any that are accepted by the Connect-ServiceFabricCluster cmdlet. See [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) for a list of available parameters.
   
   If you’re publishing to a remote cluster, you need to specify the appropriate parameters for that specific cluster. The following is an example of connecting to a non-secure cluster:
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   Here’s an example for connecting to an x509 certificate-based secure cluster:
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. Edit any other necessary settings, such as upgrade parameters and Application Parameter file location, and then publish your application from the **Publish Service Fabric Application** dialog box in Visual Studio.

## <a name="next-steps"></a>Next steps
For more information about accessing Service Fabric clusters, see [Visualizing your cluster by using Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

<!--Image references-->
[publishdialog]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png


