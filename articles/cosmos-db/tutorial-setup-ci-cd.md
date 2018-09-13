---
title: Set up CI/CD pipeline with the Azure Cosmos DB emulator build task
description: Tutorial on how to set up build and release workflow in Visual Studio Team Services (VSTS) using the Cosmos DB emulator build task
services: cosmos-db
keywords: Azure Cosmos DB Emulator
author: deborahc
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: tutorial
ms.date: 8/28/2018
ms.author: dech
ms.openlocfilehash: 482c31e447203ccf7e682138f46a6b5f00145b69
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866928"
---
# <a name="set-up-a-cicd-pipeline-with-the-azure-cosmos-db-emulator-build-task-in-visual-studio-team-services"></a><span data-ttu-id="3be9c-104">Set up a CI/CD pipeline with the Azure Cosmos DB emulator build task in Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="3be9c-104">Set up a CI/CD pipeline with the Azure Cosmos DB emulator build task in Visual Studio Team Services</span></span>

<span data-ttu-id="3be9c-105">The Azure Cosmos DB emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span><span class="sxs-lookup"><span data-stu-id="3be9c-105">The Azure Cosmos DB emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="3be9c-106">The emulator allows you to develop and test your application locally, without creating an Azure subscription or incurring any costs.</span><span class="sxs-lookup"><span data-stu-id="3be9c-106">The emulator allows you to develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> 

<span data-ttu-id="3be9c-107">The Azure Cosmos DB emulator build task for Visual Studio Team Services (VSTS) allows you to do the same in a CI environment.</span><span class="sxs-lookup"><span data-stu-id="3be9c-107">The Azure Cosmos DB emulator build task for Visual Studio Team Services (VSTS) allows you to do the same in a CI environment.</span></span> <span data-ttu-id="3be9c-108">With the build task, you can run tests against the emulator as part of your build and release workflows.</span><span class="sxs-lookup"><span data-stu-id="3be9c-108">With the build task, you can run tests against the emulator as part of your build and release workflows.</span></span> <span data-ttu-id="3be9c-109">The task spins up a Docker container with the emulator already running and provides an endpoint that can be used by the rest of the build definition.</span><span class="sxs-lookup"><span data-stu-id="3be9c-109">The task spins up a Docker container with the emulator already running and provides an endpoint that can be used by the rest of the build definition.</span></span> <span data-ttu-id="3be9c-110">You can create and start as many instances of the emulator as you need, each running in a separate container.</span><span class="sxs-lookup"><span data-stu-id="3be9c-110">You can create and start as many instances of the emulator as you need, each running in a separate container.</span></span> 

<span data-ttu-id="3be9c-111">This article demonstrates how to set up a CI pipeline in VSTS for an ASP.NET application that uses the Cosmos DB emulator build task to run tests.</span><span class="sxs-lookup"><span data-stu-id="3be9c-111">This article demonstrates how to set up a CI pipeline in VSTS for an ASP.NET application that uses the Cosmos DB emulator build task to run tests.</span></span> 

## <a name="install-the-emulator-build-task"></a><span data-ttu-id="3be9c-112">Install the emulator build task</span><span class="sxs-lookup"><span data-stu-id="3be9c-112">Install the emulator build task</span></span>

<span data-ttu-id="3be9c-113">To use the build task, we first need to install it onto our VSTS organization.</span><span class="sxs-lookup"><span data-stu-id="3be9c-113">To use the build task, we first need to install it onto our VSTS organization.</span></span> <span data-ttu-id="3be9c-114">Find the extension **Azure Cosmos DB Emulator** in the [Marketplace](https://marketplace.visualstudio.com/items?itemName=azure-cosmosdb.emulator-public-preview) and click **Get it free.**</span><span class="sxs-lookup"><span data-stu-id="3be9c-114">Find the extension **Azure Cosmos DB Emulator** in the [Marketplace](https://marketplace.visualstudio.com/items?itemName=azure-cosmosdb.emulator-public-preview) and click **Get it free.**</span></span>

![Find and install the Azure Cosmos DB Emulator build task in the VSTS Marketplace](./media/tutorial-setup-ci-cd/addExtension_1.png)

<span data-ttu-id="3be9c-116">Next, choose the organization in which to install the extension.</span><span class="sxs-lookup"><span data-stu-id="3be9c-116">Next, choose the organization in which to install the extension.</span></span> 

> [!NOTE]
> <span data-ttu-id="3be9c-117">To install an extension to a VSTS organization, you must be an account owner or project collection administrator.</span><span class="sxs-lookup"><span data-stu-id="3be9c-117">To install an extension to a VSTS organization, you must be an account owner or project collection administrator.</span></span> <span data-ttu-id="3be9c-118">If you do not have permissions, but you are an account member, you can request extensions instead.</span><span class="sxs-lookup"><span data-stu-id="3be9c-118">If you do not have permissions, but you are an account member, you can request extensions instead.</span></span> [<span data-ttu-id="3be9c-119">Learn more.</span><span class="sxs-lookup"><span data-stu-id="3be9c-119">Learn more.</span></span>](https://docs.microsoft.com/vsts/marketplace/faq-extensions?view=vsts#install-request-assign-and-access-extensions) 

![Choose a VSTS organization in which to install an extension](./media/tutorial-setup-ci-cd/addExtension_2.png)

## <a name="create-a-build-definition"></a><span data-ttu-id="3be9c-121">Create a build definition</span><span class="sxs-lookup"><span data-stu-id="3be9c-121">Create a build definition</span></span>

<span data-ttu-id="3be9c-122">Now that the extension is installed, we need to add it to a [build definition.](https://docs.microsoft.com/vsts/pipelines/get-started-designer?view=vsts&tabs=new-nav)</span><span class="sxs-lookup"><span data-stu-id="3be9c-122">Now that the extension is installed, we need to add it to a [build definition.](https://docs.microsoft.com/vsts/pipelines/get-started-designer?view=vsts&tabs=new-nav)</span></span> <span data-ttu-id="3be9c-123">You may modify an existing build definition, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="3be9c-123">You may modify an existing build definition, or create a new one.</span></span> <span data-ttu-id="3be9c-124">If you already have an existing build definition, you may skip ahead to [Add the Emulator build task to a build definition](#addEmulatorBuildTaskToBuildDefinition).</span><span class="sxs-lookup"><span data-stu-id="3be9c-124">If you already have an existing build definition, you may skip ahead to [Add the Emulator build task to a build definition](#addEmulatorBuildTaskToBuildDefinition).</span></span>

<span data-ttu-id="3be9c-125">To create a new build definition, navigate to the **Build and Release** tab in VSTS.</span><span class="sxs-lookup"><span data-stu-id="3be9c-125">To create a new build definition, navigate to the **Build and Release** tab in VSTS.</span></span> <span data-ttu-id="3be9c-126">Select **+New.**</span><span class="sxs-lookup"><span data-stu-id="3be9c-126">Select **+New.**</span></span>

<span data-ttu-id="3be9c-127">![Create a new build definition](./media/tutorial-setup-ci-cd/CreateNewBuildDef_1.png) Select the desired team project, repository, and branch to enable builds.</span><span class="sxs-lookup"><span data-stu-id="3be9c-127">![Create a new build definition](./media/tutorial-setup-ci-cd/CreateNewBuildDef_1.png) Select the desired team project, repository, and branch to enable builds.</span></span> 

![<span data-ttu-id="3be9c-128">Select the team project, repository, and branch for the build definition</span><span class="sxs-lookup"><span data-stu-id="3be9c-128">Select the team project, repository, and branch for the build definition</span></span> ](./media/tutorial-setup-ci-cd/CreateNewBuildDef_2.png)

<span data-ttu-id="3be9c-129">Finally, select the desired template for the build definition.</span><span class="sxs-lookup"><span data-stu-id="3be9c-129">Finally, select the desired template for the build definition.</span></span> <span data-ttu-id="3be9c-130">We'll select the **ASP.NET** template in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="3be9c-130">We'll select the **ASP.NET** template in this tutorial.</span></span> 

![<span data-ttu-id="3be9c-131">Select the desired build definition template</span><span class="sxs-lookup"><span data-stu-id="3be9c-131">Select the desired build definition template</span></span> ](./media/tutorial-setup-ci-cd/CreateNewBuildDef_3.png)

<span data-ttu-id="3be9c-132">Now we have a build definition that we can set up to use the Azure Cosmos DB emulator build task that looks like the one below.</span><span class="sxs-lookup"><span data-stu-id="3be9c-132">Now we have a build definition that we can set up to use the Azure Cosmos DB emulator build task that looks like the one below.</span></span> 

![ASP.NET build definition template](./media/tutorial-setup-ci-cd/CreateNewBuildDef_4.png)

## <a name="addEmulatorBuildTaskToBuildDefinition"></a><span data-ttu-id="3be9c-134">Add the task to a build definition</span><span class="sxs-lookup"><span data-stu-id="3be9c-134">Add the task to a build definition</span></span>

<span data-ttu-id="3be9c-135">To add the emulator build task, search for **cosmos** in the search box and select **Add.**</span><span class="sxs-lookup"><span data-stu-id="3be9c-135">To add the emulator build task, search for **cosmos** in the search box and select **Add.**</span></span> <span data-ttu-id="3be9c-136">The build task will start up a container with an instance of the Cosmos DB emulator already running, so the task needs to be placed before any other tasks that expect the emulator to be running.</span><span class="sxs-lookup"><span data-stu-id="3be9c-136">The build task will start up a container with an instance of the Cosmos DB emulator already running, so the task needs to be placed before any other tasks that expect the emulator to be running.</span></span>

<span data-ttu-id="3be9c-137">![Add the Emulator build task to the build definition](./media/tutorial-setup-ci-cd/addExtension_3.png) In this tutorial, we'll add the task to the beginning of Phase 1 to ensure the emulator is available before our tests execute.</span><span class="sxs-lookup"><span data-stu-id="3be9c-137">![Add the Emulator build task to the build definition](./media/tutorial-setup-ci-cd/addExtension_3.png) In this tutorial, we'll add the task to the beginning of Phase 1 to ensure the emulator is available before our tests execute.</span></span>
<span data-ttu-id="3be9c-138">The completed build definition now looks like this.</span><span class="sxs-lookup"><span data-stu-id="3be9c-138">The completed build definition now looks like this.</span></span> 

![ASP.NET build definition template](./media/tutorial-setup-ci-cd/CreateNewBuildDef_5.png)

## <a name="configure-tests-to-use-the-emulator"></a><span data-ttu-id="3be9c-140">Configure tests to use the emulator</span><span class="sxs-lookup"><span data-stu-id="3be9c-140">Configure tests to use the emulator</span></span>
<span data-ttu-id="3be9c-141">Now, we'll configure our tests to use the emulator.</span><span class="sxs-lookup"><span data-stu-id="3be9c-141">Now, we'll configure our tests to use the emulator.</span></span> <span data-ttu-id="3be9c-142">The emulator build task exports an environment variable – ‘CosmosDbEmulator.Endpoint’ – that any tasks further in the build pipeline can issue requests against.</span><span class="sxs-lookup"><span data-stu-id="3be9c-142">The emulator build task exports an environment variable – ‘CosmosDbEmulator.Endpoint’ – that any tasks further in the build pipeline can issue requests against.</span></span> 

<span data-ttu-id="3be9c-143">In this tutorial, we'll use the [Visual Studio Test task](https://github.com/Microsoft/vsts-tasks/blob/master/Tasks/VsTestV2/README.md) to run unit tests configured via a **.runsettings** file.</span><span class="sxs-lookup"><span data-stu-id="3be9c-143">In this tutorial, we'll use the [Visual Studio Test task](https://github.com/Microsoft/vsts-tasks/blob/master/Tasks/VsTestV2/README.md) to run unit tests configured via a **.runsettings** file.</span></span> <span data-ttu-id="3be9c-144">To learn more about unit test setup, visit the [documentation](https://docs.microsoft.com/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file?view=vs-2017).</span><span class="sxs-lookup"><span data-stu-id="3be9c-144">To learn more about unit test setup, visit the [documentation](https://docs.microsoft.com/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file?view=vs-2017).</span></span>

<span data-ttu-id="3be9c-145">Below is an example of a **.runsettings** file that defines parameters to be passed into an application's unit tests.</span><span class="sxs-lookup"><span data-stu-id="3be9c-145">Below is an example of a **.runsettings** file that defines parameters to be passed into an application's unit tests.</span></span> <span data-ttu-id="3be9c-146">Note the `authKey` variable used is the [well-known key](https://docs.microsoft.com/azure/cosmos-db/local-emulator#authenticating-requests) for the emulator.</span><span class="sxs-lookup"><span data-stu-id="3be9c-146">Note the `authKey` variable used is the [well-known key](https://docs.microsoft.com/azure/cosmos-db/local-emulator#authenticating-requests) for the emulator.</span></span> <span data-ttu-id="3be9c-147">This `authKey` is the key expected by the emulator build task and should be defined in your **.runsettings** file.</span><span class="sxs-lookup"><span data-stu-id="3be9c-147">This `authKey` is the key expected by the emulator build task and should be defined in your **.runsettings** file.</span></span>

```csharp
<RunSettings>
    <TestRunParameters>
    <Parameter name="endpoint" value="https://localhost:8081" />
    <Parameter name="authKey" value="C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==" />
    <Parameter name="database" value="ToDoListTest" />
    <Parameter name="collection" value="ItemsTest" />
  </TestRunParameters>
</RunSettings>
```
<span data-ttu-id="3be9c-148">These parameters `TestRunParameters` are referenced via a `TestContext` property in the application's test project.</span><span class="sxs-lookup"><span data-stu-id="3be9c-148">These parameters `TestRunParameters` are referenced via a `TestContext` property in the application's test project.</span></span> <span data-ttu-id="3be9c-149">Here is an example of a test that runs against Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3be9c-149">Here is an example of a test that runs against Cosmos DB.</span></span> 

```csharp
namespace todo.Tests
{
    [TestClass]
    public class TodoUnitTests
    {
        public TestContext TestContext { get; set; }

        [TestInitialize()]
        public void Initialize()
        {
            string endpoint = TestContext.Properties["endpoint"].ToString();
            string authKey = TestContext.Properties["authKey"].ToString();
            Console.WriteLine("Using endpoint: ", endpoint);
            DocumentDBRepository<Item>.Initialize(endpoint, authKey);
        }
        [TestMethod]
        public async Task TestCreateItemsAsync()
        {
            var item = new Item
            {
                Id = "1",
                Name = "testName",
                Description = "testDescription",
                Completed = false,
                Category = "testCategory"
            };

            // Create the item
            await DocumentDBRepository<Item>.CreateItemAsync(item);
            // Query for the item
            var returnedItem = await DocumentDBRepository<Item>.GetItemAsync(item.Id, item.Category);
            // Verify the item returned is correct.
            Assert.AreEqual(item.Id, returnedItem.Id);
            Assert.AreEqual(item.Category, returnedItem.Category);
        }

        [TestCleanup()]
        public void Cleanup()
        {
            DocumentDBRepository<Item>.Teardown();
        }
    }
}
```

<span data-ttu-id="3be9c-150">Navigate to the Execution Options in the Visual Studio Test task.</span><span class="sxs-lookup"><span data-stu-id="3be9c-150">Navigate to the Execution Options in the Visual Studio Test task.</span></span> <span data-ttu-id="3be9c-151">In the **Settings file** option,  specify that the tests are configured using the **.runsettings** file.</span><span class="sxs-lookup"><span data-stu-id="3be9c-151">In the **Settings file** option,  specify that the tests are configured using the **.runsettings** file.</span></span> <span data-ttu-id="3be9c-152">In the **Override test run parameters** option, add in ` -endpoint $(CosmosDbEmulator.Endpoint)`.</span><span class="sxs-lookup"><span data-stu-id="3be9c-152">In the **Override test run parameters** option, add in ` -endpoint $(CosmosDbEmulator.Endpoint)`.</span></span> <span data-ttu-id="3be9c-153">Doing so will configure the Test task to refer to the endpoint of the emulator build task, instead of the one defined in the **.runsettings** file.</span><span class="sxs-lookup"><span data-stu-id="3be9c-153">Doing so will configure the Test task to refer to the endpoint of the emulator build task, instead of the one defined in the **.runsettings** file.</span></span>  

![Override endpoint variable with Emulator build task endpoint](./media/tutorial-setup-ci-cd/addExtension_5.png)

## <a name="run-the-build"></a><span data-ttu-id="3be9c-155">Run the build</span><span class="sxs-lookup"><span data-stu-id="3be9c-155">Run the build</span></span>
<span data-ttu-id="3be9c-156">Now, save and queue the build.</span><span class="sxs-lookup"><span data-stu-id="3be9c-156">Now, save and queue the build.</span></span> 

![Save and run the build](./media/tutorial-setup-ci-cd/runBuild_1.png)

<span data-ttu-id="3be9c-158">Once the build has started, observe the Cosmos DB emulator task has begun pulling down the Docker image with the emulator installed.</span><span class="sxs-lookup"><span data-stu-id="3be9c-158">Once the build has started, observe the Cosmos DB emulator task has begun pulling down the Docker image with the emulator installed.</span></span> 

![Save and run the build](./media/tutorial-setup-ci-cd/runBuild_4.png)

<span data-ttu-id="3be9c-160">After the build completes, observe that your tests pass, all running against the Cosmos DB emulator from the build task!</span><span class="sxs-lookup"><span data-stu-id="3be9c-160">After the build completes, observe that your tests pass, all running against the Cosmos DB emulator from the build task!</span></span>

![Save and run the build](./media/tutorial-setup-ci-cd/buildComplete_1.png)

## <a name="next-steps"></a><span data-ttu-id="3be9c-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="3be9c-162">Next steps</span></span>

<span data-ttu-id="3be9c-163">To learn more about using the emulator for local development and testing, see [Use the Azure Cosmos DB Emulator for local development and testing](https://docs.microsoft.com/azure/cosmos-db/local-emulator).</span><span class="sxs-lookup"><span data-stu-id="3be9c-163">To learn more about using the emulator for local development and testing, see [Use the Azure Cosmos DB Emulator for local development and testing](https://docs.microsoft.com/azure/cosmos-db/local-emulator).</span></span>

<span data-ttu-id="3be9c-164">To export emulator SSL certificates, see [Export the Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js](https://docs.microsoft.com/azure/cosmos-db/local-emulator-export-ssl-certificates)</span><span class="sxs-lookup"><span data-stu-id="3be9c-164">To export emulator SSL certificates, see [Export the Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js](https://docs.microsoft.com/azure/cosmos-db/local-emulator-export-ssl-certificates)</span></span>
