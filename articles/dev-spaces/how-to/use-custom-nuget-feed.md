---
title: How to use a custom NuGet feed in Azure Dev Spaces | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: johnsta
ms.author: johnsta
ms.date: 05/11/2018
ms.topic: article
description: Use a custom NuGet feed to access and use NuGet packages in an Azure Dev Space.
keywords: Docker, Kubernetes, Azure, AKS, Azure Container Service, containers
manager: ghogen
ms.openlocfilehash: 3badd15bcfd09c97b43744a20c5df05f4ff57e84
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967399"
---
#  <a name="use-a-custom-nuget-feed-in-an-azure-dev-space"></a><span data-ttu-id="7c1bd-104">Use a custom NuGet feed in an Azure Dev Space</span><span class="sxs-lookup"><span data-stu-id="7c1bd-104">Use a custom NuGet feed in an Azure Dev Space</span></span>

<span data-ttu-id="7c1bd-105">A NuGet feed provides a convenient way to include package sources in a project.</span><span class="sxs-lookup"><span data-stu-id="7c1bd-105">A NuGet feed provides a convenient way to include package sources in a project.</span></span> <span data-ttu-id="7c1bd-106">Azure Dev Spaces will need to be able to access this feed in order for dependencies to be properly installed in the Docker container.</span><span class="sxs-lookup"><span data-stu-id="7c1bd-106">Azure Dev Spaces will need to be able to access this feed in order for dependencies to be properly installed in the Docker container.</span></span>

## <a name="set-up-a-nuget-feed"></a><span data-ttu-id="7c1bd-107">Set up a NuGet feed</span><span class="sxs-lookup"><span data-stu-id="7c1bd-107">Set up a NuGet feed</span></span>

<span data-ttu-id="7c1bd-108">To set up a NuGet feed:</span><span class="sxs-lookup"><span data-stu-id="7c1bd-108">To set up a NuGet feed:</span></span>
1. <span data-ttu-id="7c1bd-109">Add a [package reference](https://docs.microsoft.com/en-us/nuget/consume-packages/package-references-in-project-files) in the `*.csproj` file under the `PackageReference` node.</span><span class="sxs-lookup"><span data-stu-id="7c1bd-109">Add a [package reference](https://docs.microsoft.com/en-us/nuget/consume-packages/package-references-in-project-files) in the `*.csproj` file under the `PackageReference` node.</span></span>

   ```xml
   <ItemGroup>
       <!-- ... -->
       <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
       <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="7c1bd-110">Create a [NuGet.Config](https://docs.microsoft.com/en-us/nuget/reference/nuget-config-file) file in the project folder.</span><span class="sxs-lookup"><span data-stu-id="7c1bd-110">Create a [NuGet.Config](https://docs.microsoft.com/en-us/nuget/reference/nuget-config-file) file in the project folder.</span></span>
     * <span data-ttu-id="7c1bd-111">Use the `packageSources` section to reference your NuGet feed location.</span><span class="sxs-lookup"><span data-stu-id="7c1bd-111">Use the `packageSources` section to reference your NuGet feed location.</span></span> <span data-ttu-id="7c1bd-112">Important: The NuGet feed must be publicly accessible.</span><span class="sxs-lookup"><span data-stu-id="7c1bd-112">Important: The NuGet feed must be publicly accessible.</span></span>
     * <span data-ttu-id="7c1bd-113">Use the `packageSourceCredentials` section to configure username and password credentials.</span><span class="sxs-lookup"><span data-stu-id="7c1bd-113">Use the `packageSourceCredentials` section to configure username and password credentials.</span></span> 

   ```xml
   <packageSources>
       <add key="Contoso" value="https://contoso.com/packages/" />
   </packageSources>

   <packageSourceCredentials>
       <Contoso>
           <add key="Username" value="user@contoso.com" />
           <add key="ClearTextPassword" value="33f!!lloppa" />
       </Contoso>
   </packageSourceCredentials>
   ```

3. <span data-ttu-id="7c1bd-114">If you're using source code control:</span><span class="sxs-lookup"><span data-stu-id="7c1bd-114">If you're using source code control:</span></span>
    - <span data-ttu-id="7c1bd-115">Reference `NuGet.Config` in your `.gitignore` file so you don't accidentally commit credentials to your source repository.</span><span class="sxs-lookup"><span data-stu-id="7c1bd-115">Reference `NuGet.Config` in your `.gitignore` file so you don't accidentally commit credentials to your source repository.</span></span>
    - <span data-ttu-id="7c1bd-116">Open the `azds.yaml` file in your project, and locate the `build` section, and insert the following snippet to ensure that the `NuGet.Config` file will be synced to Azure so that it used during the container image build process.</span><span class="sxs-lookup"><span data-stu-id="7c1bd-116">Open the `azds.yaml` file in your project, and locate the `build` section, and insert the following snippet to ensure that the `NuGet.Config` file will be synced to Azure so that it used during the container image build process.</span></span> <span data-ttu-id="7c1bd-117">(By default, Azure Dev Spaces does not synchronize files that match `.gitignore` and `.dockerignore` rules.)</span><span class="sxs-lookup"><span data-stu-id="7c1bd-117">(By default, Azure Dev Spaces does not synchronize files that match `.gitignore` and `.dockerignore` rules.)</span></span>

        ```yaml
        build:
        useGitIgnore: true
        ignore:
        - “!NuGet.Config”
        ```


## <a name="next-steps"></a><span data-ttu-id="7c1bd-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c1bd-118">Next steps</span></span>

<span data-ttu-id="7c1bd-119">Once you have completed the above steps, the next time you run `azds up` (or hit `F5` in VSCode or Visual Studio), Azure Dev Spaces will synchronize the `NuGet.Config` file to Azure, which is then utilized by `dotnet restore` to install package dependencies in the container.</span><span class="sxs-lookup"><span data-stu-id="7c1bd-119">Once you have completed the above steps, the next time you run `azds up` (or hit `F5` in VSCode or Visual Studio), Azure Dev Spaces will synchronize the `NuGet.Config` file to Azure, which is then utilized by `dotnet restore` to install package dependencies in the container.</span></span>

