---
title: SQL Azure with Azure RemoteApp | Microsoft Docs
description: Learn how to use SQL Azure with Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: ericorman
manager: mbaldwin
editor: ''
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 24d41c7eb6b5bd34c07d21318740ecf4c6db2d22
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540838"
---
# <a name="sql-azure-with-azure-remoteapp"></a>SQL Azure with Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

Often when customers choose to host their Windows applications in the cloud with Azure RemoteApp they also want to migrate their data such as SQL servers into the cloud for an entire cloud deployment. This allows for entire cloud hosted solution that can be accessed anytime by any device anywhere using Azure RemoteApp. Below are links and references along with guidance to help you with this process.  

## <a name="migrate-your-sql-data"></a>Migrate your SQL data
Start with [Migrating a SQL Server database to Azure SQL Database](../sql-database/sql-database-cloud-migrate.md). 

## <a name="configure-azure-remoteapp"></a>Configure Azure RemoteApp
Host your Windows application in Azure RemoteApp. Below is a very high level step-by-step:

1. Create the [Azure RemoteApp template VM](remoteapp-imageoptions.md). 
2. Install the required application on the VM.
3. Configure the application so it connects to the SQL DB and confirm that it works.
4. Sysprep and shutdown the VM. Capture this as an image for use with Azure. **Note:** You will need to ensure that the application is able to retain the DB connectivity information through the sysprep process. If the application is unable to retain the DB connection information, you might want to engage the vendor of the application to check how we can specify the connection string.
5. Import the custom image into your Azure RemoteApp library selecting the proper geographical location that your SQL Azure deployment resides. 
6. Deploy a RemoteApp collection in the same data center as your SQL Azure deployment using the above template and publish the application. Deploying Azure RemoteApp in the same data center as your SQL Azure deployment helps ensure the fastest connection speeds and reduce latency. 

## <a name="app-and-sql-configuration-considerations"></a>App and SQL configuration considerations:
There are a few points to consider when using Azure SQL with RemoteApp:

Learn [how to configure an Azure SQL database firewall](../sql-database/sql-database-firewall-configure.md). An excerpt from the article states, "Initially, all access to your Azure SQL Database server is blocked by the firewall. In order to begin using your Azure SQL Database server, you must go to the Classic Portal and specify one or more server-level firewall rules that enable access to your Azure SQL Database server. Use the firewall rules to specify which IP address ranges from the Internet are allowed, and whether or not Azure applications can attempt to connect to your Azure SQL Database server."

Also, when a computer attempts to connect to your database server from the Internet, the firewall checks the originating IP address of the request against the full set of server-level and (if required) database-level firewall rules. "If the IP address of the request is within one of the ranges specified in the server-level firewall rules, the connection is granted to your Azure SQL Database server." Hence, we can make use of IP Ranges and not just individual source IP addresses.

Follow the step by step instructions in [How to: Configure firewall settings on SQL Database using the Azure Portal](../sql-database/sql-database-configure-firewall-settings.md) to specify the IP range. When you are configuring the SQL Firewall rules, please provide the IP range of the subnet that is specified for the Azure RemoteApp collection. This should allow the ARA servers to connect to the SQL DB even though they will have dynamically-assigned IP Addresses.

## <a name="troubleshooting"></a>Troubleshooting
If the experience of using a client application hosted in Azure RemoteApp that connects to a SQL database where hosted on Azure or on-premises is slow there could be a few reasons why.  

* Network latency from your device to Azure is high. Move to the best and fastest network connection you can for best performance. Use [azurespeed.com](http://azurespeed.com/) as a general tool to test your devices latency to Azure data center.  
* Client app hosted in Azure RemoteApp is under stress. Selecting a different billing plan such as Premium billing will improve performance. Another trick is to monitor the resources your application is consuming: during an active session perform a ctrl-alt-end key sequence which will launch the SAS screen, select Task Manager and observe resource utilization for your app.
* SQL server is under stress or not optimized. Follow SQL guidance for troubleshooting. 

