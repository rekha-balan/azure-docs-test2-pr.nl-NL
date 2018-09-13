---
title: Develop locally with the DocumentDB Emulator | Microsoft Docs
description: Using the DocumentDB Emulator, you can develop and test your application locally for free, without creating an Azure subscription.
services: documentdb
documentationcenter: ''
keywords: DocumentDB Emulator
author: arramac
manager: jhubbard
editor: ''
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: documentdb
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: arramac
ms.openlocfilehash: c9912af568e302fc896085e59991d1ed01b54a1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550459"
---
# <a name="use-the-azure-documentdb-emulator-for-development-and-testing"></a>Use the Azure DocumentDB Emulator for development and testing

[**Download the Emulator**](https://aka.ms/documentdb-emulator)

The Azure DocumentDB Emulator provides a local environment that emulates the Azure DocumentDB service for development purposes. Using the DocumentDB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs. When you're satisfied with how your application is working in the DocumentDB Emulator, you can switch to using an Azure DocumentDB account in the cloud.

We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the DocumentDB Emulator.

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="system-requirements"></a>System requirements
The DocumentDB Emulator has the following hardware and software requirements:

* Software requirements
  * Windows Server 2012 R2, Windows Server 2016, or Windows 10
*   Minimum Hardware requirements
  * 2 GB RAM
  * 10 GB available hard disk space

## <a name="installation"></a>Installation
You can download and install the DocumentDB Emulator from the [Microsoft Download Center](https://aka.ms/documentdb-emulator). 

> [!NOTE]
> To install, configure, and run the DocumentDB Emulator, you must have administrative privileges on the computer.

## <a name="running-on-docker-for-windows"></a>Running on Docker for Windows

The DocumentDB Emulator can be run on Docker for Windows. The Emulator does not work on Docker for Oracle Linux.

Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).

```      
docker pull mominag/documentdb_emulator 
```
To start the image, run the following commands.

``` 
md %LOCALAPPDATA%\DocumentDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\DocumentDBEmulatorCert:c:\DocumentDBEmulator\DocumentDBEmulatorCert -P -t -i mominag/documentdb_emulator
```

The response looks similar to the following:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\DocumentDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.

Use the endpoint and master key in from the response in your client and import the SSL certificate into your host. To import the SSL certificate, do the following from an admin command prompt:

```
cd %LOCALAPPDATA%\DocumentDBEmulatorCert
powershell .\importcert.ps1
```

## <a name="checking-for-updates"></a>Checking for updates
The DocumentDB Emulator includes a built-in Azure DocumentDB Data Explorer to browse data stored within DocumentDB, create new collections, and let you know when a new update is available for download. 

> [!NOTE]
> Data created in one version of the DocumentDB Emulator is not guaranteed to be accessible when using a different version. If you need to persist your data for the long term, it is recommended that you store that data in an Azure DocumentDB account, rather than in the DocumentDB Emulator. 

## <a name="how-the-emulator-works"></a>How the Emulator works
The DocumentDB Emulator provides a high-fidelity emulation of the DocumentDB service. It supports identical functionality as Azure DocumentDB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers. You can develop and test applications using the DocumentDB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for DocumentDB.

While we created a high-fidelity local emulation of the actual DocumentDB service, the implementation of the DocumentDB Emulator is different than that of the service. For example, the DocumentDB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity. This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the DocumentDB Emulator.


## <a name="authenticating-requests"></a>Authenticating requests
Just as with Azure Document in the cloud, every request that you make against the DocumentDB Emulator must be authenticated. The DocumentDB Emulator supports a single fixed account and a well-known authentication key for master key authentication. This account and key are the only credentials permitted for use with the DocumentDB Emulator. They are:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> The master key supported by the DocumentDB Emulator is intended for use only with the emulator. You cannot use your production DocumentDB account and key with the DocumentDB Emulator. 

Additionally, just as the Azure DocumentDB service, the DocumentDB Emulator supports only secure communication via SSL.

## <a name="start-and-initialize-the-emulator"></a>Start and initialize the Emulator

To start the Azure DocumentDB Emulator, select the Start button or press the Windows key. Begin typing **DocumentDB Emulator**, and select the emulator from the list of applications. 

![Select the Start button or press the Windows key, begin typing **DocumentDB Emulator**, and select the emulator from the list of applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-local-emulator/azure-documentdb-database-local-emulator-start.png)

When the emulator is running, you'll see an icon in the Windows taskbar notification area. The DocumentDB Emulator by default runs on the local machine ("localhost") listening on port 8081.

![DocumentDB local emulator taskbar notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-local-emulator/azure-documentdb-database-local-emulator-taskbar.png)

The DocumentDB Emulator is installed by default to the `C:\Program Files\DocumentDB Emulator` directory. You can also start and stop the emulator from the command-line. See [command-line tool reference](#command-line) for more information.

## <a name="start-data-explorer"></a>Start Data Explorer

When the DocumentDB emulator launches it will automatically open the DocumentDB Data Explorer in your browser. The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the DocumentDB Emulator in the Windows Tray Icon as shown below.

![DocumentDB local emulator data explorer launcher](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-local-emulator/azure-documentdb-database-local-emulator-data-explorer-launcher.png)

## <a name="developing-with-the-emulator"></a>Developing with the Emulator
Once you have the DocumentDB Emulator running on your desktop, you can use any supported [DocumentDB SDK](documentdb-sdk-dotnet.md) or the [DocumentDB REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx) to interact with the Emulator. The DocumentDB Emulator also includes a built-in Data Explorer that lets you create collections, view and edit documents without writing any code. 

    // Connect to the DocumentDB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

If you're using [DocumentDB protocol support for MongoDB](documentdb-protocol-mongodb.md), please use the following connection string:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10250/admin?ssl=true&3t.sslSelfSignedCerts=true

You can use existing tools like [DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the DocumentDB Emulator. You can also migrate data between the DocumentDB Emulator and the Azure DocumentDB service using the [DocumentDB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).

Using the DocumentDB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection. For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).

## <a name="export-the-ssl-certificate"></a>Export the SSL certificate

.NET languages and runtime use the Windows Certificate Store to securely connect to the DocumentDB local emulator. Other languages have their own method of managing and using certificates. Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).

In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager. You can start it by running certlm.msc or follow the step by step instructions in [Export the DocumentDB Emulator Certificates](./documentdb-nosql-local-emulator-export-ssl-certificates.md). Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.

![DocumentDB local emulator SSL certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-local-emulator/azure-documentdb-database-local-emulator-ssl_certificate.png)

The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/en-us/azure/java-add-certificate-ca-store). Once the certificate is imported into the cacerts store Java and MongoDB applications will be able to connect to the DocumentDB Emulator.

When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.

## <a id="command-line"></a>Command-line tool reference
From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.

### <a name="command-line-syntax"></a>Command-line Syntax

    DocumentDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

To view the list of options, type `DocumentDB.Emulator.exe /?` at the command prompt.

<table>
<tr>
  <td><strong>Option</strong></td>
  <td><strong>Description</strong></td>
  <td><strong>Command</strong></td>
  <td><strong>Arguments</strong></td>
</tr>
<tr>
  <td>[No arguments]</td>
  <td>Starts up the DocumentDB Emulator with default settings.</td>
  <td>DocumentDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Help]</td>
  <td>Displays the list of supported command-line arguments.</td>
  <td>DocumentDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Shutdown</td>
  <td>Shuts down the DocumentDB Emulator.</td>
  <td>DocumentDB.Emulator.exe /Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>DataPath</td>
  <td>Specifies the path in which to store data files. Default is %LocalAppdata%\DocumentDBEmulator.</td>
  <td>DocumentDB.Emulator.exe /DataPath=&lt;datapath&gt;</td>
  <td>&lt;datapath&gt;: An accessible path</td>
</tr>
<tr>
  <td>Port</td>
  <td>Specifies the port number to use for the emulator.  Default is 8081.</td>
  <td>DocumentDB.Emulator.exe /Port=&lt;port&gt;</td>
  <td>&lt;port&gt;: Single port number</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Specifies the port number to use for MongoDB compatibility API. Default is 10250.</td>
  <td>DocumentDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt;: Single port number</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Specifies the ports to use for direct connectivity. Defaults are 10251,10252,10253,10254.</td>
  <td>DocumentDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: Comma-delimited list of 4 ports</td>
</tr>
<tr>
  <td>Key</td>
  <td>Authorization key for the emulator. Key must be the base-64 encoding of a 64-byte vector.</td>
  <td>DocumentDB.Emulator.exe /Key:&lt;key&gt;</td>
  <td>&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>Specifies that request rate limiting behavior is enabled.</td>
  <td>DocumentDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>Specifies that request rate limiting behavior is disabled.</td>
  <td>DocumentDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>NoUI</td>
  <td>Do not show the emulator user interface.</td>
  <td>DocumentDB.Emulator.exe /NoUI</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>Don't show document explorer on startup.</td>
  <td>DocumentDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>PartitionCount</td>
  <td>Specifies the maximum number of partitioned collections. See [Change the number of collections](#set-partitioncount) for more information.</td>
  <td>DocumentDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</td>
  <td>&lt;partitioncount&gt;: Maximum number of allowed single partition collections. Default is 25. Maximum allowed is 250.</td>
</tr>
</table>

## <a name="differences-between-the-documentdb-emulator-and-azure-documentdb"></a>Differences between the DocumentDB Emulator and Azure DocumentDB 
Because the DocumentDB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure DocumentDB account in the cloud:

* The DocumentDB Emulator supports only a single fixed account and a well-known master key.  Key regeneration is not possible in the DocumentDB Emulator.
* The DocumentDB Emulator is not a scalable service and will not support a large number of collections.
* The DocumentDB Emulator does not simulate different [DocumentDB consistency levels](documentdb-consistency-levels.md).
* The DocumentDB Emulator does not simulate [multi-region replication](documentdb-distribute-data-globally.md).
* The DocumentDB Emulator does not support the service quota overrides that are available in the Azure DocumentDB service (e.g. document size limits, increased partitioned collection storage).
* As your copy of the DocumentDB Emulator might not be up to date with the most recent changes with the Azure DocumentDB service, please [DocumentDB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.

## <a id="set-partitioncount"></a>Change the number of collections

By default, you can create up to 25 single partition collections, or 1 partitioned collection using the DocumentDB Emulator. By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).

If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

To change the number of collections available to the DocumentDB Emulator, do the following:

1. Delete all local DocumentDB Emulator data by right-clicking the **DocumentDB Emulator** icon on the system tray, and then clicking **Reset Data…**.
2. Delete all emulator data in this folder C:\Users\user_name\AppData\Local\DocumentDBEmulator.
3. Exit all open instances by right-clicking the **DocumentDB Emulator** icon on the system tray, and then clicking **Exit**. It may take a minute for all instances to exit.
4. Install the latest version of the [DocumentDB Emulator](https://aka.ms/documentdb-emulator).
5. Launch the emulator with the PartitionCount flag by setting a value <= 250. For example: `C:\Program Files\DocumentDB Emulator>DocumentDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Troubleshooting

Use the following tips to help troubleshoot issues you encounter with the DocumentDB emulator:

- If the DocumentDB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com).

- If you experience crashes in DocumentDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R` 

- If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com).

### <a id="trace-files"></a>Collect trace files

To collect debugging traces, run the following commands from an administrative command prompt:

1. `cd /d "%ProgramFiles%\DocumentDB Emulator"`
2. `DocumentDB.Emulator.exe /shutdown`. Watch the system tray to make sure the program has shut down, it may take a minute. You can also just click **Exit** in the DocumentDB emulator user interface.
3. `DocumentDB.Emulator.exe /starttraces`
4. `DocumentDB.Emulator.exe`
5. Reproduce the problem. If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.
5. `DocumentDB.Emulator.exe /stoptraces`
6. Navigate to `%ProgramFiles%\DocumentDB Emulator` and find the docdbemulator_000001.etl file.
7. Send the .etl file along with repro steps to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com) for debugging.


## <a name="next-steps"></a>Next steps
* To learn more about DocumentDB, see [Introduction to Azure DocumentDB](documentdb-introduction.md)
* To start developing against the DocumentDB Emulator, download one of the [supported DocumentDB SDKs](documentdb-sdk-dotnet.md).




