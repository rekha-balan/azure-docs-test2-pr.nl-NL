1. <span data-ttu-id="88a72-101">In the Visual Studio **Solution Explorer**, right-click the project and select **Add > Docker Support** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="88a72-101">In the Visual Studio **Solution Explorer**, right-click the project and select **Add > Docker Support** from the context menu.</span></span>
   
    ![Add Docker Support context menu](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/vs-azure-tools-docker-add-docker-support/docker-support-context-menu.png)
2. <span data-ttu-id="88a72-103">Adding Docker support to an ASP.NET Core web project results in the addition of several Docker-related files being added to the project, including Docker-Compose files, deployment Windows PowerShell scripts, and Docker property files.</span><span class="sxs-lookup"><span data-stu-id="88a72-103">Adding Docker support to an ASP.NET Core web project results in the addition of several Docker-related files being added to the project, including Docker-Compose files, deployment Windows PowerShell scripts, and Docker property files.</span></span> 
   
    ![Docker files added to project](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/vs-azure-tools-docker-add-docker-support/docker-files-added.png)

> [!NOTE]
> <span data-ttu-id="88a72-105">If using the [Docker for Windows Beta](https://beta.docker.com), open Properties\Docker.props, remove the default value and restart Visual Studio for the value to take effect.</span><span class="sxs-lookup"><span data-stu-id="88a72-105">If using the [Docker for Windows Beta](https://beta.docker.com), open Properties\Docker.props, remove the default value and restart Visual Studio for the value to take effect.</span></span>
> 
> ```
> <DockerMachineName Condition="'$(DockerMachineName)'=='' "></DockerMachineName>
> ```
> 



