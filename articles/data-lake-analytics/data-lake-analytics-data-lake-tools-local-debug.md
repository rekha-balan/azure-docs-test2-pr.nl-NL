---
title: Debug Azure Data Lake Analytics code locally
description: Learn how to use Azure Data Lake Tools for Visual Studio to debug U-SQL jobs on your local workstation.
services: data-lake-analytics
author: yanancai
ms.author: yanacai
ms.reviewer: jasonwhowell
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.topic: conceptual
ms.workload: big-data
ms.date: 07/03/2018
ms.openlocfilehash: 9e73fc4db1404842e6d3878d88d8f02511587bc9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857939"
---
# <a name="debug-azure-data-lake-analytics-code-locally"></a>Debug Azure Data Lake Analytics code locally

You can use Azure Data Lake Tools for Visual Studio to run and debug Azure Data Lake Analytics code on your local workstation, just as you can in the Azure Data Lake Analytics service.

Learn how to [run U-SQL script on your local machine](data-lake-analytics-data-lake-tools-local-run.md).

## <a name="debug-scripts-and-c-assemblies-locally"></a>Debug scripts and C# assemblies locally

You can debug C# assemblies without submitting and registering them to the Azure Data Lake Analytics service. You can set breakpoints in both the code-behind file and in a referenced C# project.

### <a name="debug-local-code-in-a-code-behind-file"></a>Debug local code in a code-behind file

1. Set breakpoints in the code-behind file.
2. Select **F5** to debug the script locally.

> [!NOTE]
   > The following procedure works only in Visual Studio 2015. In older Visual Studio versions, you might need to manually add the **PDB** files.  
   >
   >

### <a name="debug-local-code-in-a-referenced-c-project"></a>Debug local code in a referenced C# project

1. Create a C# assembly project, and build it to generate the output **DLL** file.
2. Register the **DLL** file by using a U-SQL statement:

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Set breakpoints in the C# code.
4. Select **F5** to debug the script by referencing the C# **DLL** file locally.


## <a name="next-steps"></a>Next steps

- For an example of a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
- To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).
- To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
