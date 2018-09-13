---
title: Connect to Azure Analysis Services with Excel | Microsoft Docs
description: Learn how to connect to an Azure Analysis Services server by using Excel.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 807496584acb3f93fccd3495de005792b769b37f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775521"
---
# <a name="connect-with-excel"></a><span data-ttu-id="bef58-103">Connect with Excel</span><span class="sxs-lookup"><span data-stu-id="bef58-103">Connect with Excel</span></span>

<span data-ttu-id="bef58-104">Once you've created a server, and deployed a tabular model to it, clients can connect and begin exploring data.</span><span class="sxs-lookup"><span data-stu-id="bef58-104">Once you've created a server, and deployed a tabular model to it, clients can connect and begin exploring data.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="bef58-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="bef58-105">Before you begin</span></span>
<span data-ttu-id="bef58-106">The account you log in with must belong to a model database role with at least read permissions.</span><span class="sxs-lookup"><span data-stu-id="bef58-106">The account you log in with must belong to a model database role with at least read permissions.</span></span> <span data-ttu-id="bef58-107">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="bef58-107">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span> 

## <a name="connect-in-excel"></a><span data-ttu-id="bef58-108">Connect in Excel</span><span class="sxs-lookup"><span data-stu-id="bef58-108">Connect in Excel</span></span>

<span data-ttu-id="bef58-109">Connecting to a server in Excel is supported by using Get Data in Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="bef58-109">Connecting to a server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="bef58-110">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span><span class="sxs-lookup"><span data-stu-id="bef58-110">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="bef58-111">**To connect in Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="bef58-111">**To connect in Excel 2016**</span></span>

1. <span data-ttu-id="bef58-112">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="bef58-112">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="bef58-113">In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI.</span><span class="sxs-lookup"><span data-stu-id="bef58-113">In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI.</span></span> <span data-ttu-id="bef58-114">For example, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="bef58-114">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span> <span data-ttu-id="bef58-115">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span><span class="sxs-lookup"><span data-stu-id="bef58-115">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bef58-116">If you log in with a Microsoft Account, Live ID, Yahoo, Gmail, etc., or you are required to sign in with multi-factor authentication, leave the password field blank.</span><span class="sxs-lookup"><span data-stu-id="bef58-116">If you log in with a Microsoft Account, Live ID, Yahoo, Gmail, etc., or you are required to sign in with multi-factor authentication, leave the password field blank.</span></span> <span data-ttu-id="bef58-117">You are prompted for a password after clicking Next.</span><span class="sxs-lookup"><span data-stu-id="bef58-117">You are prompted for a password after clicking Next.</span></span> 

    ![Connect from Excel logon](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="bef58-119">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bef58-119">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span></span>
   
    ![Connect from Excel select model](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="bef58-121">See also</span><span class="sxs-lookup"><span data-stu-id="bef58-121">See also</span></span>
<span data-ttu-id="bef58-122">[Client libraries](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="bef58-122">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="bef58-123">Manage your server</span><span class="sxs-lookup"><span data-stu-id="bef58-123">Manage your server</span></span>](analysis-services-manage.md)     


