---
redirect_url: https://docs.microsoft.com/azure/documentdb/documentdb-create-account
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 7695acc8067381d88d875c7e9a2eb392a369d34c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549511"
---
# <a name="create-a-documentdb-account-with-mongodb-api"></a><span data-ttu-id="39b70-101">Create a DocumentDB account with MongoDB API</span><span class="sxs-lookup"><span data-stu-id="39b70-101">Create a DocumentDB account with MongoDB API</span></span>
<span data-ttu-id="39b70-102">DocumentDB databases can now be used as the data store for apps written for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="39b70-102">DocumentDB databases can now be used as the data store for apps written for MongoDB.</span></span> <span data-ttu-id="39b70-103">To use this functionality, you need an Azure account and a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="39b70-103">To use this functionality, you need an Azure account and a DocumentDB account.</span></span> <span data-ttu-id="39b70-104">This tutorial walks you through the process of creating a DocumentDB account for use with MongoDB apps.</span><span class="sxs-lookup"><span data-stu-id="39b70-104">This tutorial walks you through the process of creating a DocumentDB account for use with MongoDB apps.</span></span> 

<span data-ttu-id="39b70-105">You can create a DocumentDB with support for MongoDB account using either the Azure portal or Azure CLI with Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="39b70-105">You can create a DocumentDB with support for MongoDB account using either the Azure portal or Azure CLI with Azure Resource Manager templates.</span></span> <span data-ttu-id="39b70-106">This article shows how to create a DocumentDB with support for MongoDB account using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="39b70-106">This article shows how to create a DocumentDB with support for MongoDB account using the Azure portal.</span></span> <span data-ttu-id="39b70-107">To create an account using Azure CLI with Azure Resource Manager, see [Automate Azure DocumentDB account management using Azure CLI 2.0](documentdb-automation-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="39b70-107">To create an account using Azure CLI with Azure Resource Manager, see [Automate Azure DocumentDB account management using Azure CLI 2.0](documentdb-automation-resource-manager-cli.md).</span></span>

## <a name="prerequisite"></a><span data-ttu-id="39b70-108">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="39b70-108">Prerequisite</span></span>
<span data-ttu-id="39b70-109">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="39b70-109">An Azure account.</span></span> <span data-ttu-id="39b70-110">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span><span class="sxs-lookup"><span data-stu-id="39b70-110">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span>
## <a name="create-a-documentdb-account"></a><span data-ttu-id="39b70-111">Create a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="39b70-111">Create a DocumentDB account</span></span>

1. <span data-ttu-id="39b70-112">In an internet browser, sign in to the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="39b70-112">In an internet browser, sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="39b70-113">In the left navigation, click on **NoSQL (DocumentDB)**.</span><span class="sxs-lookup"><span data-stu-id="39b70-113">In the left navigation, click on **NoSQL (DocumentDB)**.</span></span>

    ![Screen shot of the Portal left navigation, highlighting DocumentDB NoSQL entry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-create-mongodb-account/portalleftnav.png)

3. <span data-ttu-id="39b70-115">Alternatively, click **More services >**, type **DocumentDB** in the top search bar, and click **NoSQL (DocumentDB)**.</span><span class="sxs-lookup"><span data-stu-id="39b70-115">Alternatively, click **More services >**, type **DocumentDB** in the top search bar, and click **NoSQL (DocumentDB)**.</span></span>

    ![Screen shot of the More services blade, searching for DocumentDB NoSQL entry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-create-mongodb-account/more-services-search.PNG)

4. <span data-ttu-id="39b70-117">On the top of the **NoSQL (DocumentDB)** blade, click **+ Add** on the top action bar.</span><span class="sxs-lookup"><span data-stu-id="39b70-117">On the top of the **NoSQL (DocumentDB)** blade, click **+ Add** on the top action bar.</span></span>

    ![Screen shot of the Add button on the DocumentDB NoSQL resource blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-create-mongodb-account/add-documentdb-account.PNG)

5. <span data-ttu-id="39b70-119">In the **DocumentDB account** blade, specify the desired configuration for the account.</span><span class="sxs-lookup"><span data-stu-id="39b70-119">In the **DocumentDB account** blade, specify the desired configuration for the account.</span></span>

   ![Screen shot of the New DocumentDB with protocol support for MongoDB blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-create-mongodb-account/create-documentdb-mongodb-account.png)

    - <span data-ttu-id="39b70-121">In the **ID** box, enter a name to identify the account.</span><span class="sxs-lookup"><span data-stu-id="39b70-121">In the **ID** box, enter a name to identify the account.</span></span>  <span data-ttu-id="39b70-122">When the **ID** is validated, a green check mark appears in the **ID** box.</span><span class="sxs-lookup"><span data-stu-id="39b70-122">When the **ID** is validated, a green check mark appears in the **ID** box.</span></span> <span data-ttu-id="39b70-123">The **ID** value becomes the host name within the URI.</span><span class="sxs-lookup"><span data-stu-id="39b70-123">The **ID** value becomes the host name within the URI.</span></span> <span data-ttu-id="39b70-124">The **ID** may contain only lowercase letters, numbers, and the '-' character, and must be between 3 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="39b70-124">The **ID** may contain only lowercase letters, numbers, and the '-' character, and must be between 3 and 50 characters.</span></span> <span data-ttu-id="39b70-125">Note that *documents.azure.com* is appended to the endpoint name you choose, the result of which will become your account endpoint.</span><span class="sxs-lookup"><span data-stu-id="39b70-125">Note that *documents.azure.com* is appended to the endpoint name you choose, the result of which will become your account endpoint.</span></span>

    - <span data-ttu-id="39b70-126">For **NoSQL API**, select **MongoDB**.</span><span class="sxs-lookup"><span data-stu-id="39b70-126">For **NoSQL API**, select **MongoDB**.</span></span> <span data-ttu-id="39b70-127">This specifies the communication API you would like to use to interact with your DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="39b70-127">This specifies the communication API you would like to use to interact with your DocumentDB database.</span></span>

    - <span data-ttu-id="39b70-128">For **Subscription**, select the Azure subscription that you want to use for the account.</span><span class="sxs-lookup"><span data-stu-id="39b70-128">For **Subscription**, select the Azure subscription that you want to use for the account.</span></span> <span data-ttu-id="39b70-129">If your account has only one subscription, that account is selected by default.</span><span class="sxs-lookup"><span data-stu-id="39b70-129">If your account has only one subscription, that account is selected by default.</span></span>

    - <span data-ttu-id="39b70-130">In **Resource Group**, select or create a resource group for the account.</span><span class="sxs-lookup"><span data-stu-id="39b70-130">In **Resource Group**, select or create a resource group for the account.</span></span>  <span data-ttu-id="39b70-131">By default, an existing Resource group under the Azure subscription will be chosen.</span><span class="sxs-lookup"><span data-stu-id="39b70-131">By default, an existing Resource group under the Azure subscription will be chosen.</span></span>  <span data-ttu-id="39b70-132">You may, however, choose to select to create a new resource group to which you would like to add the account.</span><span class="sxs-lookup"><span data-stu-id="39b70-132">You may, however, choose to select to create a new resource group to which you would like to add the account.</span></span> <span data-ttu-id="39b70-133">For more information, see [Using the Azure portal to manage your Azure resources](../azure-portal/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="39b70-133">For more information, see [Using the Azure portal to manage your Azure resources](../azure-portal/resource-group-portal.md).</span></span>

    - <span data-ttu-id="39b70-134">Use **Location** to specify the geographic location in which to host the account.</span><span class="sxs-lookup"><span data-stu-id="39b70-134">Use **Location** to specify the geographic location in which to host the account.</span></span>

6. <span data-ttu-id="39b70-135">Once the new account options are configured, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="39b70-135">Once the new account options are configured, click **Create**.</span></span>  <span data-ttu-id="39b70-136">It can take a few minutes to create the account.</span><span class="sxs-lookup"><span data-stu-id="39b70-136">It can take a few minutes to create the account.</span></span>

   <span data-ttu-id="39b70-137">You can monitor your progress from the Notifications hub.</span><span class="sxs-lookup"><span data-stu-id="39b70-137">You can monitor your progress from the Notifications hub.</span></span>  

   ![Screen shot of the Notifications hub, showing that the DocumentDB account is being created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-create-mongodb-account/create-documentdb-mongodb-deployment-status.png)  

7. <span data-ttu-id="39b70-139">To access your new account, click **DocumentDB (NoSQL)** on the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="39b70-139">To access your new account, click **DocumentDB (NoSQL)** on the left-hand menu.</span></span> <span data-ttu-id="39b70-140">In your list of regular DocumentDB and DocumentDB with Mongo protocol support accounts, click on your new account's name.</span><span class="sxs-lookup"><span data-stu-id="39b70-140">In your list of regular DocumentDB and DocumentDB with Mongo protocol support accounts, click on your new account's name.</span></span>
8. <span data-ttu-id="39b70-141">Your DocumentDB account is now ready to use with your MongoDB app.</span><span class="sxs-lookup"><span data-stu-id="39b70-141">Your DocumentDB account is now ready to use with your MongoDB app.</span></span>

   ![Screen shot of the default account blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-create-mongodb-account/defaultaccountblade.png)

## <a name="next-steps"></a><span data-ttu-id="39b70-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="39b70-143">Next steps</span></span>
* <span data-ttu-id="39b70-144">Learn how to [connect](documentdb-connect-mongodb-account.md) to a DocumentDB account with protocol support for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="39b70-144">Learn how to [connect](documentdb-connect-mongodb-account.md) to a DocumentDB account with protocol support for MongoDB.</span></span>






