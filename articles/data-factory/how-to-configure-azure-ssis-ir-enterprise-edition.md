---
title: Provision Enterprise Edition for the Azure-SSIS Integration Runtime | Microsoft Docs
description: This article describes the features of Enterprise Edition for the Azure-SSIS Integration Runtime and how to provision it
services: data-factory
documentationcenter: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/13/2018
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 73997345895bc54f54db1d66c0c6c24c24153dd2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866651"
---
# <a name="provision-enterprise-edition-for-the-azure-ssis-integration-runtime"></a>Provision Enterprise Edition for the Azure-SSIS Integration Runtime

The Enterprise Edition of the Azure-SSIS Integration Runtime lets you use the following advanced and premium features:
-   Change Data Capture (CDC) components
-   Oracle, Teradata, and SAP BW connectors
-   SQL Server Analysis Services (SSAS) and Azure Analysis Services (AAS) connectors and transformations
-   Fuzzy Grouping and Fuzzy Lookup transformations
-   Term Extraction and Term Lookup transformations

Some of these features require you to install additional components to customize the Azure-SSIS IR. For more info about how to install additional components, see [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md).

## <a name="enterprise-features"></a>Enterprise features

| **Enterprise Features** | **Descriptions** |
|---|---|
| CDC components | The CDC Source, Control Task, and Splitter Transformation are preinstalled on the Azure-SSIS IR Enterprise Edition. To connect to Oracle, you also need to install the CDC Designer and Service on another computer. |
| Oracle connectors | The Oracle Connection Manager, Source, and Destination are preinstalled on the Azure-SSIS IR Enterprise Edition. You also need to install the Oracle Call Interface (OCI) driver, and if necessary configure the Oracle Transport Network Substrate (TNS), on the Azure-SSIS IR. For more info, see [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md). |
| Teradata connectors | You need to install the Teradata Connection Manager, Source, and Destination, as well as the Teradata Parallel Transporter (TPT) API and Teradata ODBC driver, on the Azure-SSIS IR Enterprise Edition. For more info, see [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md). |
| SAP BW connectors | The SAP BW Connection Manager, Source, and Destination are preinstalled on the Azure-SSIS IR Enterprise Edition. You also need to install the SAP BW driver on the Azure-SSIS IR. These connectors support SAP BW 7.0 or earlier versions. To connect to later versions of SAP BW or other SAP products, you can purchase and install SAP connectors from third-party ISVs on the Azure-SSIS IR. For more info about how to install additional components, see [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md). |
| Analysis Services components               | The Data Mining Model Training Destination, the Dimension Processing Destination, and the Partition Processing Destination, as well as the Data Mining Query Transformation, are preinstalled on the Azure-SSIS IR Enterprise Edition. All these components support SQL Server Analysis Services (SSAS), but only the Partition Processing Destination supports Azure Analysis Services (AAS). To connect to SSAS, you also need to [configure Windows Authentication credentials in SSISDB](https://docs.microsoft.com/sql/integration-services/lift-shift/ssis-azure-connect-with-windows-auth). In addition to these components, the Analysis Services Execute DDL Task, the Analysis Services Processing Task, and the Data Mining Query Task are also preinstalled on the Azure-SSIS IR Standard/Enterprise Edition. |
| Fuzzy Grouping and Fuzzy Lookup transformations  | The Fuzzy Grouping and Fuzzy Lookup transformations are preinstalled on the Azure-SSIS IR Enterprise Edition. These components support both SQL Server and Azure SQL Database for storing reference data. |
| Term Extraction and Term Lookup transformations | The Term Extraction and Term Lookup transformations are preinstalled on the Azure-SSIS IR Enterprise Edition. These components support both SQL Server and Azure SQL Database for storing reference data. |

## <a name="instructions"></a>Instructions

1.  Download and install [Azure PowerShell (version 5.4 or later)](https://github.com/Azure/azure-powershell/releases/tag/v5.5.0-March2018).

2.  When you provision or reconfigure the Azure-SSIS IR with PowerShell, run `Set-AzureRmDataFactoryV2IntegrationRuntime` with **Enterprise** as the value for the **Edition** parameter before you start the Azure-SSIS IR. Here is a sample script:

    ```powershell
    $MyAzureSsisIrEdition = "Enterprise"

    Set-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $MyDataFactoryName
                                               -Name $MyAzureSsisIrName
                                               -ResourceGroupName $MyResourceGroupName
                                               -Edition $MyAzureSsisIrEdition

    Start-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $MyDataFactoryName
                                                 -Name $MyAzureSsisIrName
                                                 -ResourceGroupName $MyResourceGroupName
    ```

## <a name="next-steps"></a>Next steps

-   [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md)

-   [How to develop paid or licensed custom components for the Azure-SSIS integration runtime](how-to-develop-azure-ssis-ir-licensed-components.md)