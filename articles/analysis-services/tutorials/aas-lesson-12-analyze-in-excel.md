---
title: 'Azure Analysis Services tutorial lesson 12: Analyze in Excel | Microsoft Docs'
description: Describes how to use Analyze in Excel in the Azure Analysis Services tutorial project.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 1e487f6778c45e554f95489e62ac2dedd01ee3f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857524"
---
# <a name="analyze-in-excel"></a>Analyze in Excel

In this lesson, you use the Analyze in Excel feature to open Microsoft Excel, automatically create a connection to the model workspace, and automatically add a PivotTable to the worksheet. The Analyze in Excel feature is meant to provide a quick and easy way to test the efficacy of your model design prior to deploying your model. You do not perform any data analysis in this lesson. The purpose of this lesson is to familiarize you, the model author, with the tools you can use to test your model design.   
  
To complete this lesson, Excel must be installed on the same computer as Visual Studio.
  
Estimated time to complete this lesson: **Five minutes**  
  
## <a name="prerequisites"></a>Prerequisites  
This topic is part of a tabular modeling tutorial, which should be completed in order. Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Browse using the Default and Internet Sales perspectives  
In these first tasks, you browse your model by using both the default perspective, which includes all model objects, and also by using the Internet Sales perspective you earlier. The Internet Sales perspective excludes the Customer table object.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>To browse by using the Default perspective  
  
1.  Click the **Model** menu > **Analyze in Excel**.  
  
2.  In the **Analyze in Excel** dialog box, click **OK**.  
  
    Excel opens with a new workbook. A data source connection is created using the current user account and the Default perspective is used to define viewable fields. A PivotTable is automatically added to the worksheet.  
  
3.  In Excel, in the **PivotTable Field List**, notice the **DimDate** and **FactInternetSales** measure groups appear. The **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.  
  
4.  Close Excel without saving the workbook.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>To browse by using the Internet Sales perspective  
  
1.  Click the **Model** menu, and then click **Analyze in Excel**.  
  
2.  In the **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in the **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  In Excel, in **PivotTable Fields**, notice the DimCustomer table is excluded from the field list.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Close Excel without saving the workbook.  
  
## <a name="browse-by-using-roles"></a>Browse by using roles  
Roles are an important part of any tabular model. Without at least one role to which users are added as members, users cannot access and analyze data using your model. The Analyze in Excel feature provides a way for you to test the roles you have defined.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>To browse by using the Sales Manager user role  
  
1.  In SSDT, click the **Model** menu, and then click **Analyze in Excel**.  
  
2.  In **Specify the user name or role to use to connect to the model**, select **Role**, and then in the drop-down listbox, select **Sales Manager**, and then click **OK**.  
  
    Excel opens with a new workbook. A PivotTable is automatically created. The Pivot Table Field List includes all the data fields available in your new model.  
      
3.  Close Excel without saving the workbook.  
  
## <a name="whats-next"></a>What's next?
Go to the next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).

  
  
  
