<span data-ttu-id="63f67-101">Use the Azure CLI to get the remote deployment URL for your API App.</span><span class="sxs-lookup"><span data-stu-id="63f67-101">Use the Azure CLI to get the remote deployment URL for your API App.</span></span> <span data-ttu-id="63f67-102">In the following command, replace *\<app_name>* with your web app's name.</span><span class="sxs-lookup"><span data-stu-id="63f67-102">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="63f67-103">Configure your local Git deployment to be able to push to the remote.</span><span class="sxs-lookup"><span data-stu-id="63f67-103">Configure your local Git deployment to be able to push to the remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="63f67-104">Push to the Azure remote to deploy your app.</span><span class="sxs-lookup"><span data-stu-id="63f67-104">Push to the Azure remote to deploy your app.</span></span> <span data-ttu-id="63f67-105">You are prompted for the password you created earlier when you created the deployment user.</span><span class="sxs-lookup"><span data-stu-id="63f67-105">You are prompted for the password you created earlier when you created the deployment user.</span></span> <span data-ttu-id="63f67-106">Make sure that you enter the password you created in earlier in the quickstart, and not the password you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="63f67-106">Make sure that you enter the password you created in earlier in the quickstart, and not the password you use to sign in to the Azure portal.</span></span>

```bash
git push azure master
```
