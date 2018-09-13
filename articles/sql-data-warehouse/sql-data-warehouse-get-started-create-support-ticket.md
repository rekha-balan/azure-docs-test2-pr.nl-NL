---
title: How to create a support ticket for Azure SQL Data Warehouse | Microsoft Docs
description: How to create a support ticket in Azure SQL Data Warehouse.
services: sql-data-warehouse
author: kevinvngo
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: manage
ms.date: 04/17/2018
ms.author: kevin
ms.reviewer: igorstan
ms.openlocfilehash: 12b12ff6a6dc616ec3bb592f54862535b1318e49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814540"
---
# <a name="how-to-create-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="adf07-103">How to create a support ticket for SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="adf07-103">How to create a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="adf07-104">If you are having any issues with your SQL Data Warehouse, create a support ticket so the engineering support team can assist you.</span><span class="sxs-lookup"><span data-stu-id="adf07-104">If you are having any issues with your SQL Data Warehouse, create a support ticket so the engineering support team can assist you.</span></span>

## <a name="create-a-support-ticket"></a><span data-ttu-id="adf07-105">Create a support ticket</span><span class="sxs-lookup"><span data-stu-id="adf07-105">Create a support ticket</span></span>
1. <span data-ttu-id="adf07-106">Open the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="adf07-106">Open the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="adf07-107">On the Home screen, click the **Help + support** tab.</span><span class="sxs-lookup"><span data-stu-id="adf07-107">On the Home screen, click the **Help + support** tab.</span></span>
   
    ![Help + support](./media/sql-data-warehouse-get-started-create-support-ticket/MainPage.PNG)
3. <span data-ttu-id="adf07-109">On the Help + Support blade, click **New support request** and fill out the **Basics** blade.</span><span class="sxs-lookup"><span data-stu-id="adf07-109">On the Help + Support blade, click **New support request** and fill out the **Basics** blade.</span></span>

   <span data-ttu-id="adf07-110">Select your [Azure support plan][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="adf07-110">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="adf07-111">**Billing, quota, and subscription management** support are available at all support levels.</span><span class="sxs-lookup"><span data-stu-id="adf07-111">**Billing, quota, and subscription management** support are available at all support levels.</span></span>
   * <span data-ttu-id="adf07-112">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct], or [Premier][Premier] support.</span><span class="sxs-lookup"><span data-stu-id="adf07-112">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct], or [Premier][Premier] support.</span></span> <span data-ttu-id="adf07-113">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused the problem.</span><span class="sxs-lookup"><span data-stu-id="adf07-113">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused the problem.</span></span>
   * <span data-ttu-id="adf07-114">**Developer mentoring** and **advisory services** are available at the [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span><span class="sxs-lookup"><span data-stu-id="adf07-114">**Developer mentoring** and **advisory services** are available at the [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="adf07-115">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on the [Microsoft Premier online portal][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="adf07-115">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on the [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="adf07-116">See [Azure support plans][Azure support plan] to learn more about the various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="adf07-116">See [Azure support plans][Azure support plan] to learn more about the various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
        
    <span data-ttu-id="adf07-117">![Basics blade](./media/sql-data-warehouse-get-started-create-support-ticket/Create_ticket_1.PNG)
    ![Basics blade1](./media/sql-data-warehouse-get-started-create-support-ticket/Create_ticket_2.PNG)</span><span class="sxs-lookup"><span data-stu-id="adf07-117">![Basics blade](./media/sql-data-warehouse-get-started-create-support-ticket/Create_ticket_1.PNG)
![Basics blade1](./media/sql-data-warehouse-get-started-create-support-ticket/Create_ticket_2.PNG)</span></span>
4. <span data-ttu-id="adf07-118">Fill out the **Problem** blade.</span><span class="sxs-lookup"><span data-stu-id="adf07-118">Fill out the **Problem** blade.</span></span>
    <span data-ttu-id="adf07-119">![Problem_blade](./media/sql-data-warehouse-get-started-create-support-ticket/Create_ticket_3.PNG)</span><span class="sxs-lookup"><span data-stu-id="adf07-119">![Problem_blade](./media/sql-data-warehouse-get-started-create-support-ticket/Create_ticket_3.PNG)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="adf07-120">By default, each SQL server (for example, myserver.database.windows.net) has a **DTU Quota** of 45,000.</span><span class="sxs-lookup"><span data-stu-id="adf07-120">By default, each SQL server (for example, myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="adf07-121">This quota is simply a safety limit.</span><span class="sxs-lookup"><span data-stu-id="adf07-121">This quota is simply a safety limit.</span></span> <span data-ttu-id="adf07-122">You can increase your quota by creating a support ticket and selecting *Quota* as the request type.</span><span class="sxs-lookup"><span data-stu-id="adf07-122">You can increase your quota by creating a support ticket and selecting *Quota* as the request type.</span></span> <span data-ttu-id="adf07-123">To calculate your DTU needs, multiply 7.5 by the total [DWU][DWU] needed.</span><span class="sxs-lookup"><span data-stu-id="adf07-123">To calculate your DTU needs, multiply 7.5 by the total [DWU][DWU] needed.</span></span> <span data-ttu-id="adf07-124">For example, you would like to host two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span><span class="sxs-lookup"><span data-stu-id="adf07-124">For example, you would like to host two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="adf07-125">You can view your current DTU consumption from the SQL server blade in the portal.</span><span class="sxs-lookup"><span data-stu-id="adf07-125">You can view your current DTU consumption from the SQL server blade in the portal.</span></span> <span data-ttu-id="adf07-126">Both paused and unpaused databases count toward the DTU quota.</span><span class="sxs-lookup"><span data-stu-id="adf07-126">Both paused and unpaused databases count toward the DTU quota.</span></span> 
   > 
   > 
   
5. <span data-ttu-id="adf07-127">Fill out your **contact information**.</span><span class="sxs-lookup"><span data-stu-id="adf07-127">Fill out your **contact information**.</span></span>
<span data-ttu-id="adf07-128">![Contact_information](./media/sql-data-warehouse-get-started-create-support-ticket/Create_ticket_4.PNG)</span><span class="sxs-lookup"><span data-stu-id="adf07-128">![Contact_information](./media/sql-data-warehouse-get-started-create-support-ticket/Create_ticket_4.PNG)</span></span>

    
6. <span data-ttu-id="adf07-129">Click **Create** to submit the support request.</span><span class="sxs-lookup"><span data-stu-id="adf07-129">Click **Create** to submit the support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="adf07-130">Monitor a support ticket</span><span class="sxs-lookup"><span data-stu-id="adf07-130">Monitor a support ticket</span></span>
<span data-ttu-id="adf07-131">After you have submitted the support request, the Azure support team will contact you.</span><span class="sxs-lookup"><span data-stu-id="adf07-131">After you have submitted the support request, the Azure support team will contact you.</span></span> <span data-ttu-id="adf07-132">To check your request status and details, click **All support requests** on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="adf07-132">To check your request status and details, click **All support requests** on the dashboard.</span></span>

![Check status](./media/sql-data-warehouse-get-started-create-support-ticket/Monitor_ticket.PNG)

## <a name="other-resources"></a><span data-ttu-id="adf07-134">Other resources</span><span class="sxs-lookup"><span data-stu-id="adf07-134">Other resources</span></span>
<span data-ttu-id="adf07-135">Additionally, you can connect with the SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on the [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="adf07-135">Additionally, you can connect with the SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on the [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

