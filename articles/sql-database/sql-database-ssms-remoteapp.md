---
title: Connect to SQL Database using SQL Server Management Studio in Azure RemoteApp | Microsoft Docs
description: Use this tutorial to learn how to use SQL Server Management Studio in Azure RemoteApp for security and performance when connecting to SQL Database
services: sql-database
documentationcenter: ''
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: manage-how-to
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 82793c51df86805fb25ba285e78ec8cf8b6bf9bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552273"
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a>Use SQL Server Management Studio in Azure RemoteApp to connect to SQL Database

> [!IMPORTANT]
> Azure RemoteApp is being discontinued. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
>

## <a name="introduction"></a>Introduction
This tutorial shows you how to use SQL Server Management Studio (SSMS) in Azure RemoteApp to connect to SQL Database. It walks you through the process of setting up SQL Server Management Studio in Azure RemoteApp, explains the benefits, and shows security features that you can use in Azure Active Directory.

**Estimated time to complete:** 45 minutes

## <a name="ssms-in-azure-remoteapp"></a>SSMS in Azure RemoteApp
Azure RemoteApp is an RDS service in Azure that delivers applications. You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)

SSMS running in Azure RemoteApp gives you the same experience as running SSMS locally.

![Screenshot showing SSMS running in Azure RemoteApp][1]

## <a name="benefits"></a>Benefits
There are many benefits to using SSMS in Azure RemoteApp, including:

* Port 1433 on Azure SQL server does not have to be exposed externally (outside of Azure).
* No need to keep adding and removing IP addresses in the Azure SQL server firewall.
* All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol
* It is multi-user and can scale.
* There is a performance gain from having SSMS in the same region as the SQL Database.
* You can audit use of Azure RemoteApp with the Premium edition of Azure Active Directory which has user activity reports.
* You can enable multi-factor authentication (MFA).
* Access SSMS anywhere when using any of the supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.

## <a name="create-the-azure-remoteapp-collection"></a>Create the Azure RemoteApp collection
Here are the steps to create your Azure RemoteApp collection with SSMS:

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Create a new Windows VM from Image
Use the "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from the Gallery to make your new VM.

### <a name="2-install-ssms-from-sql-express"></a>2. Install SSMS from SQL Express
Go onto the new VM and navigate to this download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

There is an option to only download SSMS. After download, go into the install directory and run Setup to install SSMS.

You also need to install SQL Server 2014 Service Pack 1. You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.

### <a name="3-run-validate-script-and-sysprep"></a>3. Run Validate script and Sysprep
On the desktop of the VM is a PowerShell script called Validate. Run this by double-clicking. It will verify that the VM is ready to be used for remote hosting of applications. When verification is complete, it will ask to run sysprep - choose to run it.

When sysprep completes, it will shut down the VM.

To learn more about creating a Azure RemoteApp image, see: [How to create a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Capture image
When the VM has stopped running, find it in the current portal and capture it.

To learn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with the classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-to-azure-remoteapp-template-images"></a>5. Add to Azure RemoteApp Template images
In the Azure RemoteApp section of the current portal, go to the Template Images tab and click Add. In the pop-up box, select "Import an image from your Virtual Machines library" and then choose the Image that you just created.

### <a name="6-create-cloud-collection"></a>6. Create cloud collection
In the current portal, create a new Azure RemoteApp Cloud Collection. Choose the Template Image that you just imported with SSMS installed on it.

![Create new cloud collection][2]

### <a name="7-publish-ssms"></a>7. Publish SSMS
On the Publishing tab of your new cloud collection, select Publish an application from the Start Menu and then choose SSMS from the list.

![Publish App][5]

### <a name="8-add-users"></a>8. Add users
On the User Access tab you can select the users that will have access to this Azure RemoteApp collection which only includes SSMS.

![Add User][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a>9. Install the Azure RemoteApp client application
You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Configure Azure SQL server
The only configuration needed is to ensure that Azure Services is enabled for the firewall. If you use this solution, then you do not need to add any IP addresses to open the firewall. The network traffic that is allowed to the SQL Server is from other Azure services.

![Azure Allow][4]

## <a name="multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA)
MFA can be enabled for this application specifically. Go to the Applications tab of your Azure Active Directory. You will find an entry for Microsoft Azure RemoteApp. If you click that application and then configure, you will see the page below where you can enable MFA for this application.

![Enable MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Audit user activity with Azure Active Directory Premium
If you do not have Azure AD Premium, then you have to turn it on in the Licenses section of your directory. With Premium enabled, you can assign users to the Premium level.

When you go to a user in your Azure Active Directory, you can then go to the Activity tab to see login information to Azure RemoteApp.

## <a name="next-steps"></a>Next steps
After completing all the above steps, you will be able to run the Azure RemoteApp client and log-in with an assigned user. You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access to Azure SQL server.

For more information on how to make the connection to SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).

That's everything for now. Enjoy!

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/ssms.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/mfa.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/allowazure.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/publish.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/user.png





