---
title: Deploy your Teams app to Azure
description: Deploying sample Teams application to Azure
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teams developer samples
---

# Deploy your Teams apps to Azure

This tutorial shows you the steps of deploying your Teams app to Azure using Teams Toolkit.

## Before you begin

Make sure your development environment is set up by installing the Prerequisites.

> [!div class="nextstepaction"]
> [Install Prerequisites](prerequisites.md)

Open an app project in Teams Toolkit. If you haven't created any Teams apps yet, try building the first app.

> [!div class="nextstepaction"]
> [Hello World - Build your first app](../get-started/first-app-react.md)

## Sign in to your Azure account

Use this account to access the Azure portal and to provision new cloud resources to support your app.


# [Visual Studio Code](#tab/viscode)

1. Open Visual Studio Code.
1. Select the Teams Toolkit  :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: icon in the sidebar.
1. Select **Sign in to Azure**.

    > [!TIP]
    > If you have the Azure Account extension installed and are using the same account, you can skip this step. Use the same account as you are using in other extensions.

    Your default web browser opens to let you sign in to the account.
1. Sign in to your Azure account using your credentials.
1. Close the browser when prompted, and return to Visual Studio Code.

    The **ACCOUNTS** section of the sidebar shows the two accounts separately. It also lists the number of usable Azure subscriptions available to you. Ensure you have at least one usable Azure subscription available. If not, sign out and use a different account.

    Now you're ready to deploy your app to Azure!

# [Visual Studio 2019](#tab/vscode)

Visual Studio 2019 prompts you to log into each service as required. You don't need to sign in to your Microsoft 365 and Azure accounts in advance.

# [Command line](#tab/cline)

1. Sign in to Microsoft 365 with the TeamsFx CLI:

    ``` bash
    teamsfx account login m365
    ```

    Your default web browser opens to let you sign in to the account. Sign in to your Azure account using your credentials. Close the browser when you're prompted.

2. Sign in to Azure with the TeamsFx CLI:

    ``` bash
    teamsfx account login azure
    ```

    Your default web browser opens to let you sign in to the account. Sign in to your Azure account using your credentials. Close the browser when you're prompted.

    The account logins are shared between Visual Studio Code and the TeamsFx CLI.

    Now that the development environment is configured, you can create, build, and deploy your first Teams app.

---


[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary>Learn what happens when you deployed your app to Azure</summary>

Before deployment, the application has been running locally:

* The backend runs using **Azure Functions Core Tools**.
* The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.

Deployment is a two-step process. You provision the resources on an active Azure subscription, and then deploy or upload the backend and frontend code for the application to Azure.

* The backend, if configured, uses various Azure services, including Azure App Service and Azure Storage.
* The frontend application will be deployed to an Azure Storage account configured for static web hosting.

</details>

## See also

* [Tutorials Overview](code-samples.md)
* [Create a conversational bot app](first-app-bot.md)
* [Create a messaging extension](first-message-extension.md)
* [Code Samples](https://github.com/OfficeDev/Microsoft-Teams-Samples)