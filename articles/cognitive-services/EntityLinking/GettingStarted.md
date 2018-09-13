---
title: Get started with the Entity Linking API | Microsoft Docs
description: Analyze text and link named entities to relevant entries in a knowledge base by using the Entity Linking API in Cognition Services.
services: cognitive-services
author: DavidLiCIG
manager: wkwok
ms.service: cognitive-services
ms.technology: entitylinking
ms.topic: article
ms.date: 07/06/2016
ms.author: davl
ms.openlocfilehash: 946d94199dd2bd79591b415ba273d413f69b4218
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540893"
---
# <a name="get-started-with-entity-linking-api-in-c35"></a><span data-ttu-id="87cfe-103">Get Started with Entity Linking API in C&#35;</span><span class="sxs-lookup"><span data-stu-id="87cfe-103">Get Started with Entity Linking API in C&#35;</span></span>

<span data-ttu-id="87cfe-104">Microsoft's Entity Linking is a natural language processing tool to analyze text and link named-entities to relevant entries in a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="87cfe-104">Microsoft's Entity Linking is a natural language processing tool to analyze text and link named-entities to relevant entries in a knowledge base.</span></span> 

<span data-ttu-id="87cfe-105">This tutorial explores entity linking by using the Entity Linking Client Library as a NuGet package.</span><span class="sxs-lookup"><span data-stu-id="87cfe-105">This tutorial explores entity linking by using the Entity Linking Client Library as a NuGet package.</span></span> 

### <span data-ttu-id="87cfe-106"><a name="Prerequisites">Prerequisites</a></span><span class="sxs-lookup"><span data-stu-id="87cfe-106"><a name="Prerequisites">Prerequisites</a></span></span>

- <span data-ttu-id="87cfe-107">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="87cfe-107">Visual Studio 2015</span></span>
- <span data-ttu-id="87cfe-108">A Microsoft Cognitive Services API Key</span><span class="sxs-lookup"><span data-stu-id="87cfe-108">A Microsoft Cognitive Services API Key</span></span>
- <span data-ttu-id="87cfe-109">Get the client library and example</span><span class="sxs-lookup"><span data-stu-id="87cfe-109">Get the client library and example</span></span>
- <span data-ttu-id="87cfe-110">Microsoft Entity Linking NuGet Package</span><span class="sxs-lookup"><span data-stu-id="87cfe-110">Microsoft Entity Linking NuGet Package</span></span>

<span data-ttu-id="87cfe-111">You may download the Entity Linking Intelligence Service API Client Library via [SDK](https://www.github.com/microsoft/cognitive-entitylinking-windows).</span><span class="sxs-lookup"><span data-stu-id="87cfe-111">You may download the Entity Linking Intelligence Service API Client Library via [SDK](https://www.github.com/microsoft/cognitive-entitylinking-windows).</span></span> <span data-ttu-id="87cfe-112">The downloaded zip file needs to be extracted to a folder of your choice, many users choose the Visual Studio 2015 folder.</span><span class="sxs-lookup"><span data-stu-id="87cfe-112">The downloaded zip file needs to be extracted to a folder of your choice, many users choose the Visual Studio 2015 folder.</span></span>

### <span data-ttu-id="87cfe-113"><a name="step-1-subscribe-entity-linking-intelligence-service-and-get-your-own-key">Step 1: Subscribe to Entity Linking Intelligence Service and get your key</a></span><span class="sxs-lookup"><span data-stu-id="87cfe-113"><a name="step-1-subscribe-entity-linking-intelligence-service-and-get-your-own-key">Step 1: Subscribe to Entity Linking Intelligence Service and get your key</a></span></span>
<span data-ttu-id="87cfe-114">Before using Entity Linking Intelligence Service, you must sign up for an API key.</span><span class="sxs-lookup"><span data-stu-id="87cfe-114">Before using Entity Linking Intelligence Service, you must sign up for an API key.</span></span> <span data-ttu-id="87cfe-115">See [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="87cfe-115">See [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span> <span data-ttu-id="87cfe-116">Both the primary and secondary key can be used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="87cfe-116">Both the primary and secondary key can be used in this tutorial.</span></span>

### <span data-ttu-id="87cfe-117"><a name="step-2-create-a-new-project-in-visual-studio"> Step 2: Create a new project in Visual Studio</a></span><span class="sxs-lookup"><span data-stu-id="87cfe-117"><a name="step-2-create-a-new-project-in-visual-studio"> Step 2: Create a new project in Visual Studio</a></span></span>

<span data-ttu-id="87cfe-118">Let’s start by creating a new project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87cfe-118">Let’s start by creating a new project in Visual Studio.</span></span> <span data-ttu-id="87cfe-119">First, launch Visual Studio 2015 from the Start Menu.</span><span class="sxs-lookup"><span data-stu-id="87cfe-119">First, launch Visual Studio 2015 from the Start Menu.</span></span> <span data-ttu-id="87cfe-120">Then, create a new project by selecting **Installed → Templates → Visual C# → Windows Universal → Blank App** for your project template:</span><span class="sxs-lookup"><span data-stu-id="87cfe-120">Then, create a new project by selecting **Installed → Templates → Visual C# → Windows Universal → Blank App** for your project template:</span></span>

 ![Createa universal app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/EntityLinking/Images/CreateUWP.png)

### <span data-ttu-id="87cfe-122"><a name+"step-3-add-the-entity-linking-nuget-package-to-your-project">Step 3: Add the Entity Linking NuGet Package to your project</a></span><span class="sxs-lookup"><span data-stu-id="87cfe-122"><a name+"step-3-add-the-entity-linking-nuget-package-to-your-project">Step 3: Add the Entity Linking NuGet Package to your project</a></span></span>

<span data-ttu-id="87cfe-123">Entity Linking of Cognitive Services is released as a NuGet.org package and needs to be installed before you can use it.</span><span class="sxs-lookup"><span data-stu-id="87cfe-123">Entity Linking of Cognitive Services is released as a NuGet.org package and needs to be installed before you can use it.</span></span>
<span data-ttu-id="87cfe-124">To add it to your project, go to the **Solution Explorer** tab, right click your project, and select **Manage Nuget Packages**.</span><span class="sxs-lookup"><span data-stu-id="87cfe-124">To add it to your project, go to the **Solution Explorer** tab, right click your project, and select **Manage Nuget Packages**.</span></span>

<span data-ttu-id="87cfe-125">First, in the **NuGet Package Manager** window, select NuGet.org as your **Package Source** in the upper right corner.</span><span class="sxs-lookup"><span data-stu-id="87cfe-125">First, in the **NuGet Package Manager** window, select NuGet.org as your **Package Source** in the upper right corner.</span></span> <span data-ttu-id="87cfe-126">Select **Browse** in the upper left corner and in the search box type “ProjectOxford.EntityLinking”.</span><span class="sxs-lookup"><span data-stu-id="87cfe-126">Select **Browse** in the upper left corner and in the search box type “ProjectOxford.EntityLinking”.</span></span> <span data-ttu-id="87cfe-127">Select the **Microsoft.ProjectOxford.EntityLinking** NuGet package and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="87cfe-127">Select the **Microsoft.ProjectOxford.EntityLinking** NuGet package and click **Install**.</span></span>

<span data-ttu-id="87cfe-128">Next, search for Newtonsoft.Json and install.</span><span class="sxs-lookup"><span data-stu-id="87cfe-128">Next, search for Newtonsoft.Json and install.</span></span> <span data-ttu-id="87cfe-129">If you are prompted to review changes, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="87cfe-129">If you are prompted to review changes, click **OK**.</span></span> <span data-ttu-id="87cfe-130">If you are presented with the EntityLinking license terms, click **I Accept**.</span><span class="sxs-lookup"><span data-stu-id="87cfe-130">If you are presented with the EntityLinking license terms, click **I Accept**.</span></span>

<span data-ttu-id="87cfe-131">Entity Linking is now installed as part of your application.</span><span class="sxs-lookup"><span data-stu-id="87cfe-131">Entity Linking is now installed as part of your application.</span></span> <span data-ttu-id="87cfe-132">You can confirm this by checking that the\*\* Microsoft.ProjectOxford.EntityLinking\*\* reference is present as part of your project in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="87cfe-132">You can confirm this by checking that the\*\* Microsoft.ProjectOxford.EntityLinking\*\* reference is present as part of your project in Solution Explorer.</span></span>

 ![Included nuget library in project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/EntityLinking/Images/NugetLibraryInProject.png)
 
### <span data-ttu-id="87cfe-134"><a name="step-4-add-an-input-and-output-text-block-to-your-apps-xaml">Step 4: Add an input and output text block to your app’s XAML</a></span><span class="sxs-lookup"><span data-stu-id="87cfe-134"><a name="step-4-add-an-input-and-output-text-block-to-your-apps-xaml">Step 4: Add an input and output text block to your app’s XAML</a></span></span>
<span data-ttu-id="87cfe-135">Navigate to \*\* MainPage.xaml \*\* in **Solution Explorer**, then double click the file which will open it in a new window.</span><span class="sxs-lookup"><span data-stu-id="87cfe-135">Navigate to \*\* MainPage.xaml \*\* in **Solution Explorer**, then double click the file which will open it in a new window.</span></span> <span data-ttu-id="87cfe-136">For convenience, you can double click on the **XAML** button in the **Designer** tab, this will hide the **Visual Designer** and reserve all of the space for the code view.</span><span class="sxs-lookup"><span data-stu-id="87cfe-136">For convenience, you can double click on the **XAML** button in the **Designer** tab, this will hide the **Visual Designer** and reserve all of the space for the code view.</span></span>

 ![Included nuget library in project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/EntityLinking/Images/UWPMainPage.png)
 
<span data-ttu-id="87cfe-138">As a text service, the best way to visualize the functionality is creating an input and an output text block.</span><span class="sxs-lookup"><span data-stu-id="87cfe-138">As a text service, the best way to visualize the functionality is creating an input and an output text block.</span></span> <span data-ttu-id="87cfe-139">To do this, add the following XAML in the **Grid**.</span><span class="sxs-lookup"><span data-stu-id="87cfe-139">To do this, add the following XAML in the **Grid**.</span></span> <span data-ttu-id="87cfe-140">This code adds three components, an input text box, an output text block, and a start button.</span><span class="sxs-lookup"><span data-stu-id="87cfe-140">This code adds three components, an input text box, an output text block, and a start button.</span></span>
 
 ```XAML
 <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="*"/>
        <RowDefinition Height="*" />
        <RowDefinition Height="50" />
    </Grid.RowDefinitions>
    <TextBox x:Name="inputBox" Grid.Row="0" TextWrapping="Wrap" Text="Enter a paragraph" Margin="10" AcceptsReturn="True" />
    <TextBlock x:Name="outputBlock" Grid.Row="1" TextWrapping="Wrap" Text="Result will be here" Margin="10" />
    <Button x:Name="button" Grid.Row="2" Content="Get Result" />
</Grid>
 ```
 
### <span data-ttu-id="87cfe-141"><a name="step-5-proceed-to-add-entity-linking-intelligence-service">Step 5: Proceed to add Entity Linking Intelligence Service</a></span><span class="sxs-lookup"><span data-stu-id="87cfe-141"><a name="step-5-proceed-to-add-entity-linking-intelligence-service">Step 5: Proceed to add Entity Linking Intelligence Service</a></span></span>
 
<span data-ttu-id="87cfe-142">The user interface is now created.</span><span class="sxs-lookup"><span data-stu-id="87cfe-142">The user interface is now created.</span></span> <span data-ttu-id="87cfe-143">Before using the Entity Linking service, we need to add the button-Click handler.</span><span class="sxs-lookup"><span data-stu-id="87cfe-143">Before using the Entity Linking service, we need to add the button-Click handler.</span></span> <span data-ttu-id="87cfe-144">Open **MainPage.xaml** from **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="87cfe-144">Open **MainPage.xaml** from **Solution Explorer**.</span></span> <span data-ttu-id="87cfe-145">Add a button_Click handler in the end of the button.</span><span class="sxs-lookup"><span data-stu-id="87cfe-145">Add a button_Click handler in the end of the button.</span></span>
 
 ```XAML
 <Button x:Name="button" Grid.Row="2" Content="Get Result" Click="button_Click" />
 ```
 
<span data-ttu-id="87cfe-146">A button-Click handler needs to be implemented in the code.</span><span class="sxs-lookup"><span data-stu-id="87cfe-146">A button-Click handler needs to be implemented in the code.</span></span> <span data-ttu-id="87cfe-147">Open **MainPage.xaml.cs** from **Solution Explorer** to implement the button-Click.</span><span class="sxs-lookup"><span data-stu-id="87cfe-147">Open **MainPage.xaml.cs** from **Solution Explorer** to implement the button-Click.</span></span> <span data-ttu-id="87cfe-148">The EntityLinkingServiceClient is a wrapper to retrieve Entity Linking responses.</span><span class="sxs-lookup"><span data-stu-id="87cfe-148">The EntityLinkingServiceClient is a wrapper to retrieve Entity Linking responses.</span></span> <span data-ttu-id="87cfe-149">The constructor argument of EntityLinkingServiceClient is the Cognitive Services subscription key.</span><span class="sxs-lookup"><span data-stu-id="87cfe-149">The constructor argument of EntityLinkingServiceClient is the Cognitive Services subscription key.</span></span> <span data-ttu-id="87cfe-150">Paste in the subscription key you got in **Step 1** to call the Entity Linking service.</span><span class="sxs-lookup"><span data-stu-id="87cfe-150">Paste in the subscription key you got in **Step 1** to call the Entity Linking service.</span></span> 

<span data-ttu-id="87cfe-151">Below is example code, which adds the "wikipediaId" to the response by using Entity Linking Service.</span><span class="sxs-lookup"><span data-stu-id="87cfe-151">Below is example code, which adds the "wikipediaId" to the response by using Entity Linking Service.</span></span> 
 
 ```csharp
 private async void button_Click(object sender, RoutedEventArgs e)
{
    var text = this.inputBox.Text;
    var client = new EntityLinkingServiceClient("Your subscription key");
    var linkResponse = await client.LinkAsync(text);
    var result = string.Join(", ", linkResponse.Select(i => i.WikipediaID).ToList());
    this.outputBlock.Text = result;
}
 ```
 
<span data-ttu-id="87cfe-152">Now you are ready to run your first natural language processing Entity Linking App.</span><span class="sxs-lookup"><span data-stu-id="87cfe-152">Now you are ready to run your first natural language processing Entity Linking App.</span></span> <span data-ttu-id="87cfe-153">Press the **F5 key** to compile and launch the application.</span><span class="sxs-lookup"><span data-stu-id="87cfe-153">Press the **F5 key** to compile and launch the application.</span></span> <span data-ttu-id="87cfe-154">Paste text snippets or paragraphs into the input box.</span><span class="sxs-lookup"><span data-stu-id="87cfe-154">Paste text snippets or paragraphs into the input box.</span></span> <span data-ttu-id="87cfe-155">Press the "Get Result" button and observe the identified entities in the output block.</span><span class="sxs-lookup"><span data-stu-id="87cfe-155">Press the "Get Result" button and observe the identified entities in the output block.</span></span>
 
 ![UWP Sample result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/EntityLinking/Images/DemoCodeResult.png)
 
### <span data-ttu-id="87cfe-157"><a name="summary">Summary</a></span><span class="sxs-lookup"><span data-stu-id="87cfe-157"><a name="summary">Summary</a></span></span>
 
<span data-ttu-id="87cfe-158">In this tutorial you’ve learned how to create an application to leverage Entity Linking Intelligence Service Client Library with just a few lines of C# and XAML code.</span><span class="sxs-lookup"><span data-stu-id="87cfe-158">In this tutorial you’ve learned how to create an application to leverage Entity Linking Intelligence Service Client Library with just a few lines of C# and XAML code.</span></span> 





