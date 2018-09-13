---
title: Connect to Azure Database for MySQL using Go
description: This quickstart provides several Go code samples you can use to connect and query data from Azure Database for MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 02/28/2018
ms.openlocfilehash: 8f11453cd7ccdd878e20d80469f12263e72166b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865059"
---
# <a name="azure-database-for-mysql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="77928-103">Azure Database for MySQL: Use Go language to connect and query data</span><span class="sxs-lookup"><span data-stu-id="77928-103">Azure Database for MySQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="77928-104">This quickstart demonstrates how to connect to an Azure Database for MySQL from Windows, Ubuntu Linux, and Apple macOS platforms by using code written in the [Go](https://golang.org/) language.</span><span class="sxs-lookup"><span data-stu-id="77928-104">This quickstart demonstrates how to connect to an Azure Database for MySQL from Windows, Ubuntu Linux, and Apple macOS platforms by using code written in the [Go](https://golang.org/) language.</span></span> <span data-ttu-id="77928-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span><span class="sxs-lookup"><span data-stu-id="77928-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="77928-106">This topic assumes that you are familiar with development using Go and that you are new to working with Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="77928-106">This topic assumes that you are familiar with development using Go and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77928-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="77928-107">Prerequisites</span></span>
<span data-ttu-id="77928-108">This quickstart uses the resources created in either of these guides as a starting point:</span><span class="sxs-lookup"><span data-stu-id="77928-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="77928-109">Create an Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="77928-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="77928-110">Create an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="77928-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="77928-111">Install Go and MySQL connector</span><span class="sxs-lookup"><span data-stu-id="77928-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="77928-112">Install [Go](https://golang.org/doc/install) and the [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own computer.</span><span class="sxs-lookup"><span data-stu-id="77928-112">Install [Go](https://golang.org/doc/install) and the [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own computer.</span></span> <span data-ttu-id="77928-113">Depending on your platform, follow the steps in the appropriate section:</span><span class="sxs-lookup"><span data-stu-id="77928-113">Depending on your platform, follow the steps in the appropriate section:</span></span>

### <a name="windows"></a><span data-ttu-id="77928-114">Windows</span><span class="sxs-lookup"><span data-stu-id="77928-114">Windows</span></span>
1. <span data-ttu-id="77928-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="77928-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="77928-116">Launch the command prompt from the start menu.</span><span class="sxs-lookup"><span data-stu-id="77928-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="77928-117">Make a folder for your project such.</span><span class="sxs-lookup"><span data-stu-id="77928-117">Make a folder for your project such.</span></span> <span data-ttu-id="77928-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="77928-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="77928-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="77928-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="77928-120">Set the environment variable for GOPATH to point to the source code directory.</span><span class="sxs-lookup"><span data-stu-id="77928-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="77928-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="77928-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="77928-122">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span><span class="sxs-lookup"><span data-stu-id="77928-122">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="77928-123">In summary, install Go, then run these commands in the command prompt:</span><span class="sxs-lookup"><span data-stu-id="77928-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="77928-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="77928-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="77928-125">Launch the Bash shell.</span><span class="sxs-lookup"><span data-stu-id="77928-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="77928-126">Install Go by running `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="77928-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="77928-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="77928-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="77928-128">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="77928-128">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="77928-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span><span class="sxs-lookup"><span data-stu-id="77928-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="77928-130">At the Bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span><span class="sxs-lookup"><span data-stu-id="77928-130">At the Bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="77928-131">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span><span class="sxs-lookup"><span data-stu-id="77928-131">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="77928-132">In summary, run these bash commands:</span><span class="sxs-lookup"><span data-stu-id="77928-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="77928-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="77928-133">Apple macOS</span></span>
1. <span data-ttu-id="77928-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install) matching your platform.</span><span class="sxs-lookup"><span data-stu-id="77928-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install) matching your platform.</span></span> 
2. <span data-ttu-id="77928-135">Launch the Bash shell.</span><span class="sxs-lookup"><span data-stu-id="77928-135">Launch the Bash shell.</span></span>
3. <span data-ttu-id="77928-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="77928-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="77928-137">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="77928-137">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="77928-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span><span class="sxs-lookup"><span data-stu-id="77928-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="77928-139">At the Bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span><span class="sxs-lookup"><span data-stu-id="77928-139">At the Bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="77928-140">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span><span class="sxs-lookup"><span data-stu-id="77928-140">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="77928-141">In summary, install Go, then run these bash commands:</span><span class="sxs-lookup"><span data-stu-id="77928-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="77928-142">Get connection information</span><span class="sxs-lookup"><span data-stu-id="77928-142">Get connection information</span></span>
<span data-ttu-id="77928-143">Get the connection information needed to connect to the Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="77928-143">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="77928-144">You need the fully qualified server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="77928-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="77928-145">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="77928-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="77928-146">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span><span class="sxs-lookup"><span data-stu-id="77928-146">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span></span>
3. <span data-ttu-id="77928-147">Click the server name.</span><span class="sxs-lookup"><span data-stu-id="77928-147">Click the server name.</span></span>
4. <span data-ttu-id="77928-148">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span><span class="sxs-lookup"><span data-stu-id="77928-148">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span></span> <span data-ttu-id="77928-149">If you forget your password, you can also reset the password from this panel.</span><span class="sxs-lookup"><span data-stu-id="77928-149">If you forget your password, you can also reset the password from this panel.</span></span>
 <span data-ttu-id="77928-150">![Azure Database for MySQL server name](./media/connect-go/1_server-overview-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="77928-150">![Azure Database for MySQL server name](./media/connect-go/1_server-overview-name-login.png)</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="77928-151">Build and run Go code</span><span class="sxs-lookup"><span data-stu-id="77928-151">Build and run Go code</span></span> 
1. <span data-ttu-id="77928-152">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span><span class="sxs-lookup"><span data-stu-id="77928-152">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="77928-153">If you prefer a richer Interactive Development Environment (IDE), try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="77928-153">If you prefer a richer Interactive Development Environment (IDE), try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="77928-154">Paste the Go code from the sections below into text files, and then save them into your project folder with file extension \*.go (such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`).</span><span class="sxs-lookup"><span data-stu-id="77928-154">Paste the Go code from the sections below into text files, and then save them into your project folder with file extension \*.go (such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`).</span></span>
3. <span data-ttu-id="77928-155">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and then replace the example values with your own values.</span><span class="sxs-lookup"><span data-stu-id="77928-155">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and then replace the example values with your own values.</span></span> 
4. <span data-ttu-id="77928-156">Launch the command prompt or Bash shell.</span><span class="sxs-lookup"><span data-stu-id="77928-156">Launch the command prompt or Bash shell.</span></span> <span data-ttu-id="77928-157">Change directory into your project folder.</span><span class="sxs-lookup"><span data-stu-id="77928-157">Change directory into your project folder.</span></span> <span data-ttu-id="77928-158">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="77928-158">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="77928-159">On Linux `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="77928-159">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="77928-160">Some of the IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span><span class="sxs-lookup"><span data-stu-id="77928-160">Some of the IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="77928-161">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span><span class="sxs-lookup"><span data-stu-id="77928-161">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="77928-162">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span><span class="sxs-lookup"><span data-stu-id="77928-162">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="77928-163">Connect, create table, and insert data</span><span class="sxs-lookup"><span data-stu-id="77928-163">Connect, create table, and insert data</span></span>
<span data-ttu-id="77928-164">Use the following code to connect to the server, create a table, and load the data by using an **INSERT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="77928-164">Use the following code to connect to the server, create a table, and load the data by using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="77928-165">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span><span class="sxs-lookup"><span data-stu-id="77928-165">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="77928-166">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and it checks the connection by using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="77928-166">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and it checks the connection by using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="77928-167">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span><span class="sxs-lookup"><span data-stu-id="77928-167">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="77928-168">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several DDL commands.</span><span class="sxs-lookup"><span data-stu-id="77928-168">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several DDL commands.</span></span> <span data-ttu-id="77928-169">The code also uses [Prepare()](http://go-database-sql.org/prepared.html) and Exec() to run prepared statements with different parameters to insert three rows.</span><span class="sxs-lookup"><span data-stu-id="77928-169">The code also uses [Prepare()](http://go-database-sql.org/prepared.html) and Exec() to run prepared statements with different parameters to insert three rows.</span></span> <span data-ttu-id="77928-170">Each time, a custom checkError() method is used to check if an error occurred and panic to exit.</span><span class="sxs-lookup"><span data-stu-id="77928-170">Each time, a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="77928-171">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span><span class="sxs-lookup"><span data-stu-id="77928-171">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "mydemoserver.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@mydemoserver"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a><span data-ttu-id="77928-172">Read data</span><span class="sxs-lookup"><span data-stu-id="77928-172">Read data</span></span>
<span data-ttu-id="77928-173">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="77928-173">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="77928-174">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span><span class="sxs-lookup"><span data-stu-id="77928-174">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="77928-175">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="77928-175">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="77928-176">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span><span class="sxs-lookup"><span data-stu-id="77928-176">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="77928-177">The code calls the [Query()](https://golang.org/pkg/database/sql/#DB.Query) method to run the select command.</span><span class="sxs-lookup"><span data-stu-id="77928-177">The code calls the [Query()](https://golang.org/pkg/database/sql/#DB.Query) method to run the select command.</span></span> <span data-ttu-id="77928-178">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) to iterate through the result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) to parse the column values, saving the value into variables.</span><span class="sxs-lookup"><span data-stu-id="77928-178">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) to iterate through the result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) to parse the column values, saving the value into variables.</span></span> <span data-ttu-id="77928-179">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span><span class="sxs-lookup"><span data-stu-id="77928-179">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="77928-180">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span><span class="sxs-lookup"><span data-stu-id="77928-180">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "mydemoserver.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@mydemoserver"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from the table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a><span data-ttu-id="77928-181">Update data</span><span class="sxs-lookup"><span data-stu-id="77928-181">Update data</span></span>
<span data-ttu-id="77928-182">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="77928-182">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="77928-183">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span><span class="sxs-lookup"><span data-stu-id="77928-183">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="77928-184">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="77928-184">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="77928-185">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span><span class="sxs-lookup"><span data-stu-id="77928-185">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="77928-186">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the update command.</span><span class="sxs-lookup"><span data-stu-id="77928-186">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the update command.</span></span> <span data-ttu-id="77928-187">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span><span class="sxs-lookup"><span data-stu-id="77928-187">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="77928-188">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span><span class="sxs-lookup"><span data-stu-id="77928-188">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "mydemoserver.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@mydemoserver"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a><span data-ttu-id="77928-189">Delete data</span><span class="sxs-lookup"><span data-stu-id="77928-189">Delete data</span></span>
<span data-ttu-id="77928-190">Use the following code to connect and remove data using a **DELETE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="77928-190">Use the following code to connect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="77928-191">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span><span class="sxs-lookup"><span data-stu-id="77928-191">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="77928-192">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="77928-192">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="77928-193">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span><span class="sxs-lookup"><span data-stu-id="77928-193">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="77928-194">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the delete command.</span><span class="sxs-lookup"><span data-stu-id="77928-194">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the delete command.</span></span> <span data-ttu-id="77928-195">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span><span class="sxs-lookup"><span data-stu-id="77928-195">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="77928-196">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span><span class="sxs-lookup"><span data-stu-id="77928-196">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "mydemoserver.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@mydemoserver"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a><span data-ttu-id="77928-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="77928-197">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="77928-198">Migrate your database using Export and Import</span><span class="sxs-lookup"><span data-stu-id="77928-198">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
