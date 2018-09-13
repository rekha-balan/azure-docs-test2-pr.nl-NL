---
title: Release notes for Data Management Gateway | Microsoft Docs
description: Data Management Gateway tory release notes
services: data-factory
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: spelluru
published: true
ms.openlocfilehash: 9b8fccdca5d4419a401e7955365107b29728d09b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556200"
---
# <a name="release-notes-for-data-management-gateway"></a>Release notes for Data Management Gateway
One of the challenges for modern data integration is to seamlessly move data to and from on-premises to cloud. Data Factory makes this integration seamless with Data Management Gateway, which is an agent that you can install on-premises to enable hybrid data movement.

See the following articles for detailed information about Data Management Gateway and how to use it: 

*  [Data Management Gateway](data-factory-data-management-gateway.md)
*  [Move data between on-premises and cloud using Azure Data Factory](data-factory-move-data-between-onprem-and-cloud.md) 


## <a name="current-version-2762192"></a>CURRENT VERSION (2.7.6219.2)

### <a name="whats-new"></a>What’s new
- You can now authenticate into your Azure Data Lake Store using service principal. Previous we only supported OAuth.
- We have packaged new driver for reading data from Oracle on premise data store in gateway.

### <a name="enhancements-"></a>Enhancements-
- Improved data read performance from Oracle data source.
- Fixed: OData source OAuth token expiration issue.
- Fixed: Unable to read Oracle decimal over 28 bits issue.


## <a name="earlier-versions"></a>Earlier versions

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>What’s new
- Customers can provide feedback on gateway registering experience.
- Support a new compression format: ZIP (Deflate)

### <a name="enhancements-"></a>Enhancements-
- Performance improvement for Oracle Sink, HDFS source.
- Bug fix for gateway auto update, gateway parallel processing capacity.


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>Enhancements
- Improved and more robust Gateway registration experience- Now you can track progress status during the Gateway registration process, which makes the registration experience more responsive.
- Improvement in Gateway Restore Process- You can still recover gateway even if you do not have the gateway backup file with this update. This would require you to reset Linked Service credentials in Portal.
- Bug fix.

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>What’s new

- You can now store data source credentials locally. The credentials are encrypted. The data source credentials can be recovered and restored using the backup file that can be exported from the existing Gateway, all on premise. 

### <a name="enhancements-"></a>Enhancements-

- Improved and more robust Gateway registration experience.
- Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve the overall format detection accuracy.

## <a name="2361002"></a>2.3.6100.2

- Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.
- Enhance the stability of network connection between gateway and Service Bus
- A few bug fixes


## <a name="2260721"></a>2.2.6072.1

*  Supports setting HTTP proxy for the gateway using the Gateway Configuration Manager. If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.
*  Supports header handling for TextFormat when copying data from/to Azure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.
*  Supports copying data from Append Blob and Page Blob along with the already supported Block Blob.
*  Introduces a new gateway status **Online (Limited)**, which indicates that the main functionality of the gateway works except the interactive operation support for Copy Wizard.
*  Enhances the robustness of gateway registration using registration key.

## <a name="216040"></a>2.1.6040.

*  DB2 driver is included in the gateway installation package now. You do not need to install it separately. 
*  DB2 driver now supports z/OS and DB2 for i (AS/400) along with the platforms already supported (Linux, Unix, and Windows). 
*  Supports using DocumentDB as a source or destination for on-premises data stores
*  Supports copying data from/to cold/hot blob storage along with the already supported general-purpose storage account. 
*  Allows you to connect to on-premises SQL Server via gateway with remote login privileges.  

## <a name="2060131"></a>2.0.6013.1

*  You can select the language/culture to be used by a gateway during manual installation.

*  When gateway does not work as expected, you can choose to send gateway logs of last seven days to Microsoft to facilitate troubleshooting of the issue. If gateway is not connected to the cloud service, you can choose to save and archive gateway logs.  

*  User interface improvements for gateway configuration manager:

    *  Make gateway status more visible on the Home tab.

    *  Reorganized and simplified controls.

    *  You can copy data from a storage using the [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md). See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general. 
*  You can use Data Management Gateway to ingress data directly from an on-premises SQL Server database into Azure Machine Learning.

*  Performance improvements

    * Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.

## <a name="11259531"></a>1.12.5953.1

*  Bug fixes

## <a name="11159181"></a>1.11.5918.1

*  Maximum size of the gateway event log has been increased from 1 MB to 40 MB.

*  A warning dialog is displayed in case a restart is needed during gateway auto-update. You can choose to restart right then or later. 

*  In case auto-update fails, gateway installer retries auto-updating three times at maximum.

*  Performance improvements

    * Improve performance for loading large tables from on-premises server in code-free copy scenario.

*  Bug fixes

## <a name="11058921"></a>1.10.5892.1

*  Performance improvements

*  Bug fixes

## <a name="1958652"></a>1.9.5865.2

*  Zero touch auto update capability
*  New tray icon with gateway status indicators
*  Ability to “Update now” from the client
*  Ability to set update schedule time
*  PowerShell script for toggling auto-update on/off
*  Support for JSON format  
*  Performance improvements
*  Bug fixes

## <a name="1858221"></a>1.8.5822.1

*  Improve troubleshooting experience
*  Performance improvements
*  Bug fixes

### <a name="1757951"></a>1.7.5795.1

*  Performance improvements
*  Bug fixes

### <a name="1757641"></a>1.7.5764.1

*  Performance improvements
*  Bug fixes

### <a name="1657351"></a>1.6.5735.1

*  Support on-premises HDFS Source/Sink
*  Performance improvements
*  Bug fixes

### <a name="1656961"></a>1.6.5696.1

*  Performance improvements
*  Bug fixes

### <a name="1656761"></a>1.6.5676.1

*  Support diagnostic tools on Configuration Manager
*  Support table columns for tabular data sources for Azure Data Factory
*  Support SQL DW for Azure Data Factory
*  Support Reclusive in BlobSource and FileSource for Azure Data Factory
*  Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory
*  Support Copy Activity reporting progress for Azure Data Factory
*  Support Data Source Connectivity Validation for Azure Data Factory
*  Bug fixes

### <a name="1656721"></a>1.6.5672.1

*  Support table name for ODBC data source for Azure Data Factory
*  Performance improvements
*  Bug fixes

### <a name="1656581"></a>1.6.5658.1

*  Support File Sink for Azure Data Factory
*  Support preserving hierarchy in binary copy for Azure Data Factory
*  Support Copy Activity Idempotency for Azure Data Factory
*  Bug fixes

### <a name="1656401"></a>1.6.5640.1

*  Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)
*  Support quote character in csv parser for Azure Data Factory
*  Compression support (BZip2)
*  Bug fixes

### <a name="1556121"></a>1.5.5612.1

*  Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)
*  Compression support (Gzip and Deflate)
*  Performance improvements
*  Bug fixes

### <a name="1455491"></a>1.4.5549.1

*  Add Oracle data source support for Azure Data Factory
*  Performance improvements
*  Bug fixes

### <a name="1454921"></a>1.4.5492.1

*  Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services
*  Refine the Configuration UI and registration process
*  Azure Data Factory – Azure Ingress and Egress support for SQL Server data source

### <a name="1253031"></a>1.2.5303.1

*  Fix timeout issue to support more time-consuming data source connections. 

### <a name="1155268"></a>1.1.5526.8

*  Requires .NET Framework 4.5.1 as a prerequisite during setup.

### <a name="1051442"></a>1.0.5144.2

*  No changes that affect Azure Data Factory scenarios.
