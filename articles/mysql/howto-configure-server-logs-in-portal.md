---
title: Configure and access server logs for Azure Database for MySQL in Azure Portal
description: This article describes how to configure and access the server logs in Azure Database for MySQL from the Azure Portal.
services: mysql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: eb35563bc21fc48d304f216e7b34cc9a77f35e83
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856667"
---
# <a name="configure-and-access-server-logs-in-the-azure-portal"></a><span data-ttu-id="39c62-103">Configure and access server logs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="39c62-103">Configure and access server logs in the Azure portal</span></span>

<span data-ttu-id="39c62-104">You can configure, list, and download the [Azure Database for MySQL server logs](concepts-server-logs.md) from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="39c62-104">You can configure, list, and download the [Azure Database for MySQL server logs](concepts-server-logs.md) from the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39c62-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="39c62-105">Prerequisites</span></span>
<span data-ttu-id="39c62-106">To step through this how-to guide, you need:</span><span class="sxs-lookup"><span data-stu-id="39c62-106">To step through this how-to guide, you need:</span></span>
- [<span data-ttu-id="39c62-107">Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="39c62-107">Azure Database for MySQL server</span></span>](quickstart-create-mysql-server-database-using-azure-portal.md)

## <a name="configure-logging"></a><span data-ttu-id="39c62-108">Configure logging</span><span class="sxs-lookup"><span data-stu-id="39c62-108">Configure logging</span></span>
<span data-ttu-id="39c62-109">Configure access to the MySQL slow query log.</span><span class="sxs-lookup"><span data-stu-id="39c62-109">Configure access to the MySQL slow query log.</span></span> 

1. <span data-ttu-id="39c62-110">Sign in to the [Azure portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="39c62-110">Sign in to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="39c62-111">Select your Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="39c62-111">Select your Azure Database for MySQL server.</span></span>

3. <span data-ttu-id="39c62-112">Under the **Monitoring** section in the sidebar, select **Server Logs**.</span><span class="sxs-lookup"><span data-stu-id="39c62-112">Under the **Monitoring** section in the sidebar, select **Server Logs**.</span></span> 
   <span data-ttu-id="39c62-113">![Select Server logs, Click to configure](./media/howto-configure-server-logs-in-portal/1-select-server-logs-configure.png)</span><span class="sxs-lookup"><span data-stu-id="39c62-113">![Select Server logs, Click to configure](./media/howto-configure-server-logs-in-portal/1-select-server-logs-configure.png)</span></span>

4. <span data-ttu-id="39c62-114">Select the heading **Click here to enable logs and configure log parameters** to see the server parameters.</span><span class="sxs-lookup"><span data-stu-id="39c62-114">Select the heading **Click here to enable logs and configure log parameters** to see the server parameters.</span></span>

5. <span data-ttu-id="39c62-115">Change the parameters that you need to adjust.</span><span class="sxs-lookup"><span data-stu-id="39c62-115">Change the parameters that you need to adjust.</span></span> <span data-ttu-id="39c62-116">All changes you make in this session are highlighted in purple.</span><span class="sxs-lookup"><span data-stu-id="39c62-116">All changes you make in this session are highlighted in purple.</span></span> 

   <span data-ttu-id="39c62-117">Once you have changed the parameters, you can click **Save**.</span><span class="sxs-lookup"><span data-stu-id="39c62-117">Once you have changed the parameters, you can click **Save**.</span></span> <span data-ttu-id="39c62-118">Or you can **Discard** your changes.</span><span class="sxs-lookup"><span data-stu-id="39c62-118">Or you can **Discard** your changes.</span></span>

   ![Click save or discard](./media/howto-configure-server-logs-in-portal/3-save-discard.png)

6. <span data-ttu-id="39c62-120">Return to the list of logs by clicking the **close button** (X icon) on the **Server Parameters** page.</span><span class="sxs-lookup"><span data-stu-id="39c62-120">Return to the list of logs by clicking the **close button** (X icon) on the **Server Parameters** page.</span></span>

## <a name="view-list-and-download-logs"></a><span data-ttu-id="39c62-121">View list and download logs</span><span class="sxs-lookup"><span data-stu-id="39c62-121">View list and download logs</span></span>
<span data-ttu-id="39c62-122">Once logging begins, you can view a list of available logs and download individual log files on the Server Logs pane.</span><span class="sxs-lookup"><span data-stu-id="39c62-122">Once logging begins, you can view a list of available logs and download individual log files on the Server Logs pane.</span></span> 

1. <span data-ttu-id="39c62-123">Open the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="39c62-123">Open the Azure portal.</span></span>

2. <span data-ttu-id="39c62-124">Select your Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="39c62-124">Select your Azure Database for MySQL server.</span></span>

3. <span data-ttu-id="39c62-125">Under the **Monitoring** section in the sidebar, select **Server Logs**.</span><span class="sxs-lookup"><span data-stu-id="39c62-125">Under the **Monitoring** section in the sidebar, select **Server Logs**.</span></span> <span data-ttu-id="39c62-126">The page shows a list of your log files, as shown:</span><span class="sxs-lookup"><span data-stu-id="39c62-126">The page shows a list of your log files, as shown:</span></span>

   ![List of Logs](./media/howto-configure-server-logs-in-portal/4-server-logs-list.png)

   > [!TIP]
   > <span data-ttu-id="39c62-128">The naming convention of the log is **mysql-slow-< your server name>-yyyymmddhh.log**.</span><span class="sxs-lookup"><span data-stu-id="39c62-128">The naming convention of the log is **mysql-slow-< your server name>-yyyymmddhh.log**.</span></span> <span data-ttu-id="39c62-129">The date and time used in the file name is the time is when the log was issued.</span><span class="sxs-lookup"><span data-stu-id="39c62-129">The date and time used in the file name is the time is when the log was issued.</span></span> <span data-ttu-id="39c62-130">Logs files are rotated every 24 hours or 7.5 GB, whichever comes first.</span><span class="sxs-lookup"><span data-stu-id="39c62-130">Logs files are rotated every 24 hours or 7.5 GB, whichever comes first.</span></span>

4. <span data-ttu-id="39c62-131">If needed, use the **search box** to quickly narrow down to a specific log based on date/time.</span><span class="sxs-lookup"><span data-stu-id="39c62-131">If needed, use the **search box** to quickly narrow down to a specific log based on date/time.</span></span> <span data-ttu-id="39c62-132">The search is on the name of the log.</span><span class="sxs-lookup"><span data-stu-id="39c62-132">The search is on the name of the log.</span></span>

5. <span data-ttu-id="39c62-133">Download individual log files using the **download** button (down arrow icon) next to each log file in the table row as shown:</span><span class="sxs-lookup"><span data-stu-id="39c62-133">Download individual log files using the **download** button (down arrow icon) next to each log file in the table row as shown:</span></span>

   ![Click download icon](./media/howto-configure-server-logs-in-portal/5-download.png)


## <a name="next-steps"></a><span data-ttu-id="39c62-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="39c62-135">Next steps</span></span>
- <span data-ttu-id="39c62-136">See [Access Server Logs in CLI](howto-configure-server-logs-in-cli.md) to learn how to download logs programmatically.</span><span class="sxs-lookup"><span data-stu-id="39c62-136">See [Access Server Logs in CLI](howto-configure-server-logs-in-cli.md) to learn how to download logs programmatically.</span></span>
- <span data-ttu-id="39c62-137">Learn more about [Server Logs](concepts-server-logs.md) in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="39c62-137">Learn more about [Server Logs](concepts-server-logs.md) in Azure Database for MySQL.</span></span> 
- <span data-ttu-id="39c62-138">For more information about the parameter definitions and MySQL logging, see the MySQL documentation on [Logs](https://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html).</span><span class="sxs-lookup"><span data-stu-id="39c62-138">For more information about the parameter definitions and MySQL logging, see the MySQL documentation on [Logs](https://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html).</span></span>

