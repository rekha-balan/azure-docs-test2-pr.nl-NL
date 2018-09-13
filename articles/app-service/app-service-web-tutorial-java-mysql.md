---
title: Build a Java and MySQL web app in Azure
description: Learn how to get a Java app that connects to the Azure MySQL database service working in Azure appservice .
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0baab86c0cb76bfeecb30cdb62c968a476e402b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855786"
---
# <a name="tutorial-build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="20866-103">Tutorial: Build a Java and MySQL web app in Azure</span><span class="sxs-lookup"><span data-stu-id="20866-103">Tutorial: Build a Java and MySQL web app in Azure</span></span>

> [!NOTE]
> <span data-ttu-id="20866-104">This article deploys an app to App Service on Windows.</span><span class="sxs-lookup"><span data-stu-id="20866-104">This article deploys an app to App Service on Windows.</span></span> <span data-ttu-id="20866-105">To deploy to App Service on _Linux_, see [Deploy a containerized Spring Boot app to Azure](/java/azure/spring-framework/deploy-containerized-spring-boot-java-app-with-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="20866-105">To deploy to App Service on _Linux_, see [Deploy a containerized Spring Boot app to Azure](/java/azure/spring-framework/deploy-containerized-spring-boot-java-app-with-maven-plugin).</span></span>
>

<span data-ttu-id="20866-106">This tutorial shows you how to create a Java web app in Azure and connect it to a MySQL database.</span><span class="sxs-lookup"><span data-stu-id="20866-106">This tutorial shows you how to create a Java web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="20866-107">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20866-107">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Java app running in Azure appservice](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="20866-109">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="20866-109">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="20866-110">Create a MySQL database in Azure</span><span class="sxs-lookup"><span data-stu-id="20866-110">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="20866-111">Connect a sample app to the database</span><span class="sxs-lookup"><span data-stu-id="20866-111">Connect a sample app to the database</span></span>
> * <span data-ttu-id="20866-112">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="20866-112">Deploy the app to Azure</span></span>
> * <span data-ttu-id="20866-113">Update and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="20866-113">Update and redeploy the app</span></span>
> * <span data-ttu-id="20866-114">Stream diagnostic logs from Azure</span><span class="sxs-lookup"><span data-stu-id="20866-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="20866-115">Monitor the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="20866-115">Monitor the app in the Azure portal</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="20866-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="20866-116">Prerequisites</span></span>

1. [<span data-ttu-id="20866-117">Download and install Git</span><span class="sxs-lookup"><span data-stu-id="20866-117">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="20866-118">Download and install the Java 7 JDK or above</span><span class="sxs-lookup"><span data-stu-id="20866-118">Download and install the Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="20866-119">Download, install, and start MySQL</span><span class="sxs-lookup"><span data-stu-id="20866-119">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

## <a name="prepare-local-mysql"></a><span data-ttu-id="20866-120">Prepare local MySQL</span><span class="sxs-lookup"><span data-stu-id="20866-120">Prepare local MySQL</span></span> 

<span data-ttu-id="20866-121">In this step, you create a database in a local MySQL server for use in testing the app locally on your machine.</span><span class="sxs-lookup"><span data-stu-id="20866-121">In this step, you create a database in a local MySQL server for use in testing the app locally on your machine.</span></span>

### <a name="connect-to-mysql-server"></a><span data-ttu-id="20866-122">Connect to MySQL server</span><span class="sxs-lookup"><span data-stu-id="20866-122">Connect to MySQL server</span></span>

<span data-ttu-id="20866-123">In a terminal window, connect to your local MySQL server.</span><span class="sxs-lookup"><span data-stu-id="20866-123">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="20866-124">You can use this terminal window to run all the commands in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="20866-124">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="20866-125">If you're prompted for a password, enter the password for the `root` account.</span><span class="sxs-lookup"><span data-stu-id="20866-125">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="20866-126">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="20866-126">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="20866-127">If your command runs successfully, then your MySQL server is already running.</span><span class="sxs-lookup"><span data-stu-id="20866-127">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="20866-128">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="20866-128">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="20866-129">Create a database</span><span class="sxs-lookup"><span data-stu-id="20866-129">Create a database</span></span> 

<span data-ttu-id="20866-130">In the `mysql` prompt, create a database and a table for the to-do items.</span><span class="sxs-lookup"><span data-stu-id="20866-130">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="20866-131">Exit your server connection by typing `quit`.</span><span class="sxs-lookup"><span data-stu-id="20866-131">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-the-sample-app"></a><span data-ttu-id="20866-132">Create and run the sample app</span><span class="sxs-lookup"><span data-stu-id="20866-132">Create and run the sample app</span></span> 

<span data-ttu-id="20866-133">In this step, you clone sample Spring boot app, configure it to use the local MySQL database, and run it on your computer.</span><span class="sxs-lookup"><span data-stu-id="20866-133">In this step, you clone sample Spring boot app, configure it to use the local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="20866-134">Clone the sample</span><span class="sxs-lookup"><span data-stu-id="20866-134">Clone the sample</span></span>

<span data-ttu-id="20866-135">In the terminal window, navigate to a working directory and clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="20866-135">In the terminal window, navigate to a working directory and clone the sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-the-app-to-use-the-mysql-database"></a><span data-ttu-id="20866-136">Configure the app to use the MySQL database</span><span class="sxs-lookup"><span data-stu-id="20866-136">Configure the app to use the MySQL database</span></span>

<span data-ttu-id="20866-137">Update the `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with the same root password used to open the MySQL prompt:</span><span class="sxs-lookup"><span data-stu-id="20866-137">Update the `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with the same root password used to open the MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-the-sample"></a><span data-ttu-id="20866-138">Build and run the sample</span><span class="sxs-lookup"><span data-stu-id="20866-138">Build and run the sample</span></span>

<span data-ttu-id="20866-139">Build and run the sample using the Maven wrapper included in the repo:</span><span class="sxs-lookup"><span data-stu-id="20866-139">Build and run the sample using the Maven wrapper included in the repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="20866-140">Open your browser to `http://localhost:8080` to see in the sample in action.</span><span class="sxs-lookup"><span data-stu-id="20866-140">Open your browser to `http://localhost:8080` to see in the sample in action.</span></span> <span data-ttu-id="20866-141">As you add tasks to the list,  use the following SQL commands in the MySQL prompt to view the data stored in MySQL.</span><span class="sxs-lookup"><span data-stu-id="20866-141">As you add tasks to the list,  use the following SQL commands in the MySQL prompt to view the data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="20866-142">Stop the application by hitting `Ctrl`+`C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="20866-142">Stop the application by hitting `Ctrl`+`C` in the terminal.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="20866-143">Create an Azure MySQL database</span><span class="sxs-lookup"><span data-stu-id="20866-143">Create an Azure MySQL database</span></span>

<span data-ttu-id="20866-144">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="20866-144">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="20866-145">You configure the sample application to use this database later on in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="20866-145">You configure the sample application to use this database later on in the tutorial.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="20866-146">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="20866-146">Create a resource group</span></span>

<span data-ttu-id="20866-147">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [`az group create`](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="20866-147">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [`az group create`](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="20866-148">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="20866-148">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="20866-149">The following example creates a resource group in the North Europe region:</span><span class="sxs-lookup"><span data-stu-id="20866-149">The following example creates a resource group in the North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="20866-150">To see the possible values you can use for `--location`, use the [`az appservice list-locations`](/cli/azure/appservice#list-locations) command.</span><span class="sxs-lookup"><span data-stu-id="20866-150">To see the possible values you can use for `--location`, use the [`az appservice list-locations`](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="20866-151">Create a MySQL server</span><span class="sxs-lookup"><span data-stu-id="20866-151">Create a MySQL server</span></span>

<span data-ttu-id="20866-152">In the Cloud Shell, create a server in Azure Database for MySQL with the [`az mysql server create`](/cli/azure/mysql/server?view=azure-cli-latest#az-mysql-server-create) command.</span><span class="sxs-lookup"><span data-stu-id="20866-152">In the Cloud Shell, create a server in Azure Database for MySQL with the [`az mysql server create`](/cli/azure/mysql/server?view=azure-cli-latest#az-mysql-server-create) command.</span></span>

<span data-ttu-id="20866-153">In the following command, substitute a unique server name for the *\<mysql_server_name>* placeholder, a user name for the *\<admin_user>*, and a password for the *\<admin_password>*  placeholder.</span><span class="sxs-lookup"><span data-stu-id="20866-153">In the following command, substitute a unique server name for the *\<mysql_server_name>* placeholder, a user name for the *\<admin_user>*, and a password for the *\<admin_password>*  placeholder.</span></span> <span data-ttu-id="20866-154">The server name is used as part of your PostgreSQL endpoint (`https://<mysql_server_name>.mysql.database.azure.com`), so the name needs to be unique across all servers in Azure.</span><span class="sxs-lookup"><span data-stu-id="20866-154">The server name is used as part of your PostgreSQL endpoint (`https://<mysql_server_name>.mysql.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span>

```azurecli-interactive
az mysql server create --resource-group myResourceGroup --name <mysql_server_name>--location "West Europe" --admin-user <admin_user> --admin-password <server_admin_password> --sku-name GP_Gen4_2
```

> [!NOTE]
> <span data-ttu-id="20866-155">Since there are several credentials to think about in this tutorial, to avoid confusion, `--admin-user` and `--admin-password` are set to dummy values.</span><span class="sxs-lookup"><span data-stu-id="20866-155">Since there are several credentials to think about in this tutorial, to avoid confusion, `--admin-user` and `--admin-password` are set to dummy values.</span></span> <span data-ttu-id="20866-156">In a production environment, follow security best practices when choosing a good username and password for your MySQL server in Azure.</span><span class="sxs-lookup"><span data-stu-id="20866-156">In a production environment, follow security best practices when choosing a good username and password for your MySQL server in Azure.</span></span>
>
>

<span data-ttu-id="20866-157">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="20866-157">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "location": "westeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "additionalProperties": {},
    "capacity": 2,
    "family": "Gen4",
    "name": "GP_Gen4_2",
    "size": null,
    "tier": "GeneralPurpose"
  },
  "sslEnforcement": "Enabled",
  ...   +  
  -  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="20866-158">Configure server firewall</span><span class="sxs-lookup"><span data-stu-id="20866-158">Configure server firewall</span></span>

<span data-ttu-id="20866-159">In the Cloud Shell, create a firewall rule for your MySQL server to allow client connections by using the [`az mysql server firewall-rule create`](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-create) command.</span><span class="sxs-lookup"><span data-stu-id="20866-159">In the Cloud Shell, create a firewall rule for your MySQL server to allow client connections by using the [`az mysql server firewall-rule create`](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-create) command.</span></span> <span data-ttu-id="20866-160">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="20866-160">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create --name allAzureIPs --server <mysql_server_name> --resource-group myResourceGroup --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP] 
> <span data-ttu-id="20866-161">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](app-service-ip-addresses.md#find-outbound-ips).</span><span class="sxs-lookup"><span data-stu-id="20866-161">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](app-service-ip-addresses.md#find-outbound-ips).</span></span>
>

## <a name="configure-the-azure-mysql-database"></a><span data-ttu-id="20866-162">Configure the Azure MySQL database</span><span class="sxs-lookup"><span data-stu-id="20866-162">Configure the Azure MySQL database</span></span>

<span data-ttu-id="20866-163">In the local terminal window, connect to the MySQL server in Azure.</span><span class="sxs-lookup"><span data-stu-id="20866-163">In the local terminal window, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="20866-164">Use the value you specified previously for _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="20866-164">Use the value you specified previously for _&lt;mysql_server_name>_.</span></span> <span data-ttu-id="20866-165">When prompted for a password, use the password you specified when you created the database in Azure.</span><span class="sxs-lookup"><span data-stu-id="20866-165">When prompted for a password, use the password you specified when you created the database in Azure.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="20866-166">Create a database</span><span class="sxs-lookup"><span data-stu-id="20866-166">Create a database</span></span> 

<span data-ttu-id="20866-167">In the `mysql` prompt, create a database and a table for the to-do items.</span><span class="sxs-lookup"><span data-stu-id="20866-167">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="20866-168">Create a user with permissions</span><span class="sxs-lookup"><span data-stu-id="20866-168">Create a user with permissions</span></span>

<span data-ttu-id="20866-169">Create a database user and give it all privileges in the `tododb` database.</span><span class="sxs-lookup"><span data-stu-id="20866-169">Create a database user and give it all privileges in the `tododb` database.</span></span> <span data-ttu-id="20866-170">Replace the placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span><span class="sxs-lookup"><span data-stu-id="20866-170">Replace the placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* TO '<Javaapp_user>';
```

<span data-ttu-id="20866-171">Exit your server connection by typing `quit`.</span><span class="sxs-lookup"><span data-stu-id="20866-171">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-the-sample-to-azure-app-service"></a><span data-ttu-id="20866-172">Deploy the sample to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="20866-172">Deploy the sample to Azure App Service</span></span>

<span data-ttu-id="20866-173">Create an Azure App Service plan with the **FREE** pricing tier using the  [`az appservice plan create`](/cli/azure/appservice/plan#az-appservice-plan-create) CLI command.</span><span class="sxs-lookup"><span data-stu-id="20866-173">Create an Azure App Service plan with the **FREE** pricing tier using the  [`az appservice plan create`](/cli/azure/appservice/plan#az-appservice-plan-create) CLI command.</span></span> <span data-ttu-id="20866-174">The appservice plan defines the physical resources used to host your apps.</span><span class="sxs-lookup"><span data-stu-id="20866-174">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="20866-175">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span><span class="sxs-lookup"><span data-stu-id="20866-175">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="20866-176">When the plan is ready, the Azure CLI shows similar output to the following example:</span><span class="sxs-lookup"><span data-stu-id="20866-176">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="20866-177">Create an Azure Web app</span><span class="sxs-lookup"><span data-stu-id="20866-177">Create an Azure Web app</span></span>

<span data-ttu-id="20866-178">In the Cloud Shell, use the [`az webapp create`](/cli/azure/webapp#az-webapp-create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span><span class="sxs-lookup"><span data-stu-id="20866-178">In the Cloud Shell, use the [`az webapp create`](/cli/azure/webapp#az-webapp-create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="20866-179">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span><span class="sxs-lookup"><span data-stu-id="20866-179">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="20866-180">Substitute the `<app_name>` placeholder with your own unique app name.</span><span class="sxs-lookup"><span data-stu-id="20866-180">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="20866-181">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="20866-181">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="20866-182">You can map a custom domain name entry to the web app before you expose it to your users.</span><span class="sxs-lookup"><span data-stu-id="20866-182">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="20866-183">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="20866-183">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="20866-184">Configure Java</span><span class="sxs-lookup"><span data-stu-id="20866-184">Configure Java</span></span> 

<span data-ttu-id="20866-185">In the Cloud Shell, set up the Java runtime configuration that your app needs with the  [`az webapp config set`](/cli/azure/webapp/config#az-webapp-config-set) command.</span><span class="sxs-lookup"><span data-stu-id="20866-185">In the Cloud Shell, set up the Java runtime configuration that your app needs with the  [`az webapp config set`](/cli/azure/webapp/config#az-webapp-config-set) command.</span></span>

<span data-ttu-id="20866-186">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="20866-186">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set --name <app_name> --resource-group myResourceGroup --java-version 1.8 --java-container Tomcat --java-container-version 8.0
```

### <a name="configure-the-app-to-use-the-azure-sql-database"></a><span data-ttu-id="20866-187">Configure the app to use the Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="20866-187">Configure the app to use the Azure SQL database</span></span>

<span data-ttu-id="20866-188">Before running the sample app, set application settings on the web app to use the Azure MySQL database you created in Azure.</span><span class="sxs-lookup"><span data-stu-id="20866-188">Before running the sample app, set application settings on the web app to use the Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="20866-189">These properties are exposed to the web application as environment variables and override the values set in the application.properties inside the packaged web app.</span><span class="sxs-lookup"><span data-stu-id="20866-189">These properties are exposed to the web application as environment variables and override the values set in the application.properties inside the packaged web app.</span></span> 

<span data-ttu-id="20866-190">In the Cloud Shell, set application settings using [`az webapp config appsettings`](https://docs.microsoft.com/cli/azure/webapp/config/appsettings) in the CLI:</span><span class="sxs-lookup"><span data-stu-id="20866-190">In the Cloud Shell, set application settings using [`az webapp config appsettings`](https://docs.microsoft.com/cli/azure/webapp/config/appsettings) in the CLI:</span></span>

```azurecli-interactive
az webapp config appsettings set --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" --resource-group myResourceGroup --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name --resource-group myResourceGroup --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set --settings SPRING_DATASOURCE_PASSWORD=Javaapp_password --resource-group myResourceGroup --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="20866-191">Get FTP deployment credentials</span><span class="sxs-lookup"><span data-stu-id="20866-191">Get FTP deployment credentials</span></span> 
<span data-ttu-id="20866-192">You can deploy your application to Azure appservice in various ways including FTP, local Git, GitHub, Azure DevOps, and BitBucket.</span><span class="sxs-lookup"><span data-stu-id="20866-192">You can deploy your application to Azure appservice in various ways including FTP, local Git, GitHub, Azure DevOps, and BitBucket.</span></span> <span data-ttu-id="20866-193">For this example, FTP to deploy the .WAR file built previously on your local machine to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="20866-193">For this example, FTP to deploy the .WAR file built previously on your local machine to Azure App Service.</span></span>

<span data-ttu-id="20866-194">To determine what credentials to pass along in an ftp command to the Web App, Use [`az appservice web deployment list-publishing-profiles`](https://docs.microsoft.com/cli/azure/webapp/deployment#az-appservice-web-deployment-list-publishing-profiles) command in the Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="20866-194">To determine what credentials to pass along in an ftp command to the Web App, Use [`az appservice web deployment list-publishing-profiles`](https://docs.microsoft.com/cli/azure/webapp/deployment#az-appservice-web-deployment-list-publishing-profiles) command in the Cloud Shell:</span></span> 

```azurecli-interactive
az webapp deployment list-publishing-profiles --name <app_name> --resource-group myResourceGroup --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-the-app-using-ftp"></a><span data-ttu-id="20866-195">Upload the app using FTP</span><span class="sxs-lookup"><span data-stu-id="20866-195">Upload the app using FTP</span></span>

<span data-ttu-id="20866-196">Use your favorite FTP tool to deploy the .WAR file to the */site/wwwroot/webapps* folder on the server address taken from the `URL` field in the previous command.</span><span class="sxs-lookup"><span data-stu-id="20866-196">Use your favorite FTP tool to deploy the .WAR file to the */site/wwwroot/webapps* folder on the server address taken from the `URL` field in the previous command.</span></span> <span data-ttu-id="20866-197">Remove the existing default (ROOT) application directory and replace the existing ROOT.war with the .WAR file built in the earlier in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="20866-197">Remove the existing default (ROOT) application directory and replace the existing ROOT.war with the .WAR file built in the earlier in the tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected to waws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-the-web-app"></a><span data-ttu-id="20866-198">Test the web app</span><span class="sxs-lookup"><span data-stu-id="20866-198">Test the web app</span></span>

<span data-ttu-id="20866-199">Browse to `http://<app_name>.azurewebsites.net/` and add a few tasks to the list.</span><span class="sxs-lookup"><span data-stu-id="20866-199">Browse to `http://<app_name>.azurewebsites.net/` and add a few tasks to the list.</span></span> 

![Java app running in Azure appservice](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="20866-201">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="20866-201">**Congratulations!**</span></span> <span data-ttu-id="20866-202">You're running a data-driven Java app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="20866-202">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="20866-203">Update the app and redeploy</span><span class="sxs-lookup"><span data-stu-id="20866-203">Update the app and redeploy</span></span>

<span data-ttu-id="20866-204">Update the application to include an additional column in the todo list for what day the item was created.</span><span class="sxs-lookup"><span data-stu-id="20866-204">Update the application to include an additional column in the todo list for what day the item was created.</span></span> <span data-ttu-id="20866-205">Spring Boot handles updating the database schema for you as the data model changes without altering your existing database records.</span><span class="sxs-lookup"><span data-stu-id="20866-205">Spring Boot handles updating the database schema for you as the data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="20866-206">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add the following imports to the class:</span><span class="sxs-lookup"><span data-stu-id="20866-206">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add the following imports to the class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="20866-207">Add a `String` property `timeCreated` to *src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span><span class="sxs-lookup"><span data-stu-id="20866-207">Add a `String` property `timeCreated` to *src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="20866-208">Add getters/setters for the new `timeCreated` property while you are editing this file.</span><span class="sxs-lookup"><span data-stu-id="20866-208">Add getters/setters for the new `timeCreated` property while you are editing this file.</span></span>

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. <span data-ttu-id="20866-209">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in the `updateTodo` method to set the timestamp:</span><span class="sxs-lookup"><span data-stu-id="20866-209">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in the `updateTodo` method to set the timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="20866-210">Add support for the new field in the `Thymeleaf` template.</span><span class="sxs-lookup"><span data-stu-id="20866-210">Add support for the new field in the `Thymeleaf` template.</span></span> <span data-ttu-id="20866-211">Update *src/main/resources/templates/index.html* with a new table header for the timestamp, and a new field to display the value of the timestamp in each table data row.</span><span class="sxs-lookup"><span data-stu-id="20866-211">Update *src/main/resources/templates/index.html* with a new table header for the timestamp, and a new field to display the value of the timestamp in each table data row.</span></span>

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. <span data-ttu-id="20866-212">Rebuild the application:</span><span class="sxs-lookup"><span data-stu-id="20866-212">Rebuild the application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="20866-213">FTP the updated .WAR as before, removing the existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading the updated .WAR file as ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="20866-213">FTP the updated .WAR as before, removing the existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading the updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="20866-214">When you refresh the app, a **Time Created** column is now visible.</span><span class="sxs-lookup"><span data-stu-id="20866-214">When you refresh the app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="20866-215">When you add a new task, the app will populate the timestamp automatically.</span><span class="sxs-lookup"><span data-stu-id="20866-215">When you add a new task, the app will populate the timestamp automatically.</span></span> <span data-ttu-id="20866-216">Your existing tasks remain unchanged and work with the app even though the underlying data model has changed.</span><span class="sxs-lookup"><span data-stu-id="20866-216">Your existing tasks remain unchanged and work with the app even though the underlying data model has changed.</span></span> 

![Java app updated with a new column](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="20866-218">Stream diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="20866-218">Stream diagnostic logs</span></span> 

<span data-ttu-id="20866-219">While your Java application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span><span class="sxs-lookup"><span data-stu-id="20866-219">While your Java application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span></span> <span data-ttu-id="20866-220">That way, you can get the same diagnostic messages to help you debug application errors.</span><span class="sxs-lookup"><span data-stu-id="20866-220">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="20866-221">To start log streaming, use the [`az webapp log tail`](/cli/azure/webapp/log?view=azure-cli-latest#az-webapp-log-tail) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="20866-221">To start log streaming, use the [`az webapp log tail`](/cli/azure/webapp/log?view=azure-cli-latest#az-webapp-log-tail) command in the Cloud Shell.</span></span>

```azurecli-interactive 
az webapp log tail --name <app_name> --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="20866-222">Manage your Azure web app</span><span class="sxs-lookup"><span data-stu-id="20866-222">Manage your Azure web app</span></span>

<span data-ttu-id="20866-223">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span><span class="sxs-lookup"><span data-stu-id="20866-223">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="20866-224">From the left menu, click **App Service**, then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="20866-224">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="20866-226">By default, your web app page shows the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="20866-226">By default, your web app page shows the **Overview** page.</span></span> <span data-ttu-id="20866-227">This page gives you a view of how your app is doing.</span><span class="sxs-lookup"><span data-stu-id="20866-227">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="20866-228">Here, you can also perform management tasks like stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="20866-228">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="20866-229">The tabs on the left side of the page show the different configuration pages you can open.</span><span class="sxs-lookup"><span data-stu-id="20866-229">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![App Service page in Azure portal](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="20866-231">These tabs in the page show the many great features you can add to your web app.</span><span class="sxs-lookup"><span data-stu-id="20866-231">These tabs in the page show the many great features you can add to your web app.</span></span> <span data-ttu-id="20866-232">The following list gives you just a few of the possibilities:</span><span class="sxs-lookup"><span data-stu-id="20866-232">The following list gives you just a few of the possibilities:</span></span>
* <span data-ttu-id="20866-233">Map a custom DNS name</span><span class="sxs-lookup"><span data-stu-id="20866-233">Map a custom DNS name</span></span>
* <span data-ttu-id="20866-234">Bind a custom SSL certificate</span><span class="sxs-lookup"><span data-stu-id="20866-234">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="20866-235">Configure continuous deployment</span><span class="sxs-lookup"><span data-stu-id="20866-235">Configure continuous deployment</span></span>
* <span data-ttu-id="20866-236">Scale up and out</span><span class="sxs-lookup"><span data-stu-id="20866-236">Scale up and out</span></span>
* <span data-ttu-id="20866-237">Add user authentication</span><span class="sxs-lookup"><span data-stu-id="20866-237">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="20866-238">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="20866-238">Clean up resources</span></span>

<span data-ttu-id="20866-239">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running the following command in the Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="20866-239">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running the following command in the Cloud Shell:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="20866-240">Next steps</span><span class="sxs-lookup"><span data-stu-id="20866-240">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="20866-241">Create a MySQL database in Azure</span><span class="sxs-lookup"><span data-stu-id="20866-241">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="20866-242">Connect a sample Java app to the MySQL</span><span class="sxs-lookup"><span data-stu-id="20866-242">Connect a sample Java app to the MySQL</span></span>
> * <span data-ttu-id="20866-243">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="20866-243">Deploy the app to Azure</span></span>
> * <span data-ttu-id="20866-244">Update and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="20866-244">Update and redeploy the app</span></span>
> * <span data-ttu-id="20866-245">Stream diagnostic logs from Azure</span><span class="sxs-lookup"><span data-stu-id="20866-245">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="20866-246">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="20866-246">Manage the app in the Azure portal</span></span>

<span data-ttu-id="20866-247">Advance to the next tutorial to learn how to map a custom DNS name to the app.</span><span class="sxs-lookup"><span data-stu-id="20866-247">Advance to the next tutorial to learn how to map a custom DNS name to the app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="20866-248">Map an existing custom DNS name to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="20866-248">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
