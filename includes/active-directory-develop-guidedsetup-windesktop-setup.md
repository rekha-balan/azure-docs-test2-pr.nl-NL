---
title: include file
description: include file
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: include
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/19/2018
ms.author: andret
ms.custom: include file
ms.openlocfilehash: c5d61da61f6ec98a1cac37ce9b12b28019ce2ae1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45012730"
---
## <a name="set-up-your-project"></a><span data-ttu-id="42039-103">Set up your project</span><span class="sxs-lookup"><span data-stu-id="42039-103">Set up your project</span></span>

<span data-ttu-id="42039-104">In this section you create a new project to demonstrate how to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so that the application can query Web APIs that require a token.</span><span class="sxs-lookup"><span data-stu-id="42039-104">In this section you create a new project to demonstrate how to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so that the application can query Web APIs that require a token.</span></span>

<span data-ttu-id="42039-105">The application that you create with this guide displays a button that's used to call a graph, an area to show the results on the screen, and a sign-out button.</span><span class="sxs-lookup"><span data-stu-id="42039-105">The application that you create with this guide displays a button that's used to call a graph, an area to show the results on the screen, and a sign-out button.</span></span>

> [!NOTE]
> <span data-ttu-id="42039-106">Prefer to download this sample's Visual Studio project instead?</span><span class="sxs-lookup"><span data-stu-id="42039-106">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="42039-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip), and skip to the [Configuration step](#register-your-application) to configure the code sample before you execute it.</span><span class="sxs-lookup"><span data-stu-id="42039-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip), and skip to the [Configuration step](#register-your-application) to configure the code sample before you execute it.</span></span>
>

<span data-ttu-id="42039-108">To create your application, do the following:</span><span class="sxs-lookup"><span data-stu-id="42039-108">To create your application, do the following:</span></span>
1. <span data-ttu-id="42039-109">In Visual Studio, select **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="42039-109">In Visual Studio, select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="42039-110">Under **Templates**, select **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="42039-110">Under **Templates**, select **Visual C#**.</span></span>
3. <span data-ttu-id="42039-111">Select **WPF App** or **WPF Application**, depending on the version of Visual Studio version you're using.</span><span class="sxs-lookup"><span data-stu-id="42039-111">Select **WPF App** or **WPF Application**, depending on the version of Visual Studio version you're using.</span></span>

## <a name="add-msal-to-your-project"></a><span data-ttu-id="42039-112">Add MSAL to your project</span><span class="sxs-lookup"><span data-stu-id="42039-112">Add MSAL to your project</span></span>
1. <span data-ttu-id="42039-113">In Visual Studio, select **Tools** > **NuGet Package Manager**> **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="42039-113">In Visual Studio, select **Tools** > **NuGet Package Manager**> **Package Manager Console**.</span></span>
2. <span data-ttu-id="42039-114">In the Package Manager Console window, paste the following Azure PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="42039-114">In the Package Manager Console window, paste the following Azure PowerShell command:</span></span>

    ```powershell
    Install-Package Microsoft.Identity.Client -Pre -Version 1.1.4-preview0002
    ```

    > [!NOTE] 
    > <span data-ttu-id="42039-115">This command installs Microsoft Authentication Library.</span><span class="sxs-lookup"><span data-stu-id="42039-115">This command installs Microsoft Authentication Library.</span></span> <span data-ttu-id="42039-116">MSAL handles acquiring, caching, and refreshing user tokens that are used to access the APIs that are protected by Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="42039-116">MSAL handles acquiring, caching, and refreshing user tokens that are used to access the APIs that are protected by Azure Active Directory v2.</span></span>
    >

    > [!NOTE]
    > <span data-ttu-id="42039-117">This quickstart does not use yet the latest version of MSAL.NET, but we are working on updating it</span><span class="sxs-lookup"><span data-stu-id="42039-117">This quickstart does not use yet the latest version of MSAL.NET, but we are working on updating it</span></span>
    > 

## <a name="add-the-code-to-initialize-msal"></a><span data-ttu-id="42039-118">Add the code to initialize MSAL</span><span class="sxs-lookup"><span data-stu-id="42039-118">Add the code to initialize MSAL</span></span>
<span data-ttu-id="42039-119">In this step, you create a class to handle interaction with MSAL, such as handling of tokens.</span><span class="sxs-lookup"><span data-stu-id="42039-119">In this step, you create a class to handle interaction with MSAL, such as handling of tokens.</span></span>

1. <span data-ttu-id="42039-120">Open the *App.xaml.cs* file, and then add the reference for MSAL to the class:</span><span class="sxs-lookup"><span data-stu-id="42039-120">Open the *App.xaml.cs* file, and then add the reference for MSAL to the class:</span></span>

    ```csharp
    using Microsoft.Identity.Client;
    ```
<!-- Workaround for Docs conversion bug -->

2. <span data-ttu-id="42039-121">Update the app class to the following:</span><span class="sxs-lookup"><span data-stu-id="42039-121">Update the app class to the following:</span></span>

    ```csharp
    public partial class App : Application
    {
        //Below is the clientId of your app registration. 
        //You have to replace the below with the Application Id for your app registration
        private static string ClientId = "your_client_id_here";

        public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

    }
    ```

## <a name="create-the-application-ui"></a><span data-ttu-id="42039-122">Create the application UI</span><span class="sxs-lookup"><span data-stu-id="42039-122">Create the application UI</span></span>

<span data-ttu-id="42039-123">This section shows how an application can query a protected back-end server such as Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="42039-123">This section shows how an application can query a protected back-end server such as Microsoft Graph.</span></span> 

<span data-ttu-id="42039-124">A *MainWindow.xaml* file should automatically be created as a part of your project template.</span><span class="sxs-lookup"><span data-stu-id="42039-124">A *MainWindow.xaml* file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="42039-125">Open this file, and then replace your application's *\<Grid>* node with the following code:</span><span class="sxs-lookup"><span data-stu-id="42039-125">Open this file, and then replace your application's *\<Grid>* node with the following code:</span></span>

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```

