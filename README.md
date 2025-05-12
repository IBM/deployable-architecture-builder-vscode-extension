# IBM Cloud Deployable Architecture Builder

IBM Cloud Deployable Architecture Builder extension for [Visual Studio Code](https://code.visualstudio.com/) assists infrastructure as code (IaC) developers to create and maintain deployable architectures by combining capabilities that are found in [IBM Cloud](https://cloud.ibm.com) Projects, Global Catalog, and Schematics. Deployable architectures can have one or more architecture variations and multiple configurations for those architectures based on the customer business needs. For more information, see [What are modules and deployable architectures?](https://cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-understand-module-da).

Use this extension to:

- Develop a deployable architecture from a locally-cloned Terraform module.
- Develop a new version of an existing deployable architecture in a public or private catalog.
- Onboard and validate deployable architectures in IBM Cloud from within the extension and monitor validation progress by using VS Code Output channel logging.
- Lint catalog JSON manifest files.

## Prerequisites

For information about prerequisites, see [Onboarding your deployable architecture by using a Visual Studio Code extension](https://cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-vs-code-extension&interface=ui#onboard-before).

## Log in to an IBM Cloud account

1. Open the VS Code Command Palette. Go to **View** > **Command Palette** and search for `IBM Cloud: Log in`.
2. Select **IBM Cloud: Log in** and log in with an API key, federated ID, or username and password, and select the account that you want to use.
3. (Optional): If you need to change the login environment, go to **View** > **Command Palette** and search `IBM Cloud: Log in`. Select **IBM Cloud: Log in** > **Change login environment**. From the dropdown, select **Production** or **Staging**. After updating the setting, run the command again.

After logging in, the projects and catalogs in that account will be shown in the explorer views, if any.

## Features

After you confirm all of the prerequisites, the following features are available. Many of these features are highlighted in the extension's walkthrough which you can open by navigating to **View** -> **Command Palette** -> **Welcome: Open Walkthrough** -> **Get started with IBM Cloud Deployable Architecture Builder** in the application's menu bar.

### Create and edit project configurations

You can create a configuration in a project from a deployable architecture.

1. In the **Catalogs** explorer tree, right-click on a deployable architecture version and select **Add to a project**.
2. Select an existing project or create a new one.
3. Provide a name for the configuration.

The new configuration is highlighted in the **Projects** explorer tree and a YAML file is opened containing the configuration properties that you can edit.

The configuration is validated automatically as you type. Errors, warnings, and informational messages are shown via squiggles and in the **Problems** view. You can also use completions and quick fixes to quickly and easily edit your configuration. Changes are automatically synced with IBM Cloud whenever you save. Changes from IBM Cloud are automatically synced in the background on an interval.

You can also edit existing configurations by right-clicking on them in the **Projects** explorer tree and selecting **Edit configuration**.

Configuration editing features are managed in a language server. To see errors, warnings, and informational messages from the language server, open the **IBM Cloud Deployable Architecture Builder Language Server** Output channel in the **Output** view.

### Insert references in configurations

You can insert references to properties in other configurations or to secrets in IBM Cloud Secrets Manager.

- When editing a configuration YAML file, bring up the code assist menu on an input property's value and select **Add reference**. Follow the prompts.
- When editing an API key or trusted profile ID under _authorizations_, bring up the code assist menu and select **Add a secret**. Follow the prompts.

References are automatically validated. An informational squiggly and associated **Problems** view entry indicates if the reference is valid.

### Stack configurations

You can manage stack configurations and their members in the **Projects** explorer tree in multiple ways.

- Select one or more configurations, right-click on them, and select **Stack**. Follow the prompts to create a new stack configuration or to select an existing one.
- To add configurations to an existing stack, select one or more configurations and drag them to the stack.
- To remove configurations from a stack, select the configurations under the stack that you want to remove and drag them to the **Configurations** node.

### Validating a deployable architecture on IBM Cloud

To validate a local Terraform module as a deployable architecture on IBM Cloud use the following steps.

1. Right-click on your module folder in the workspace in VS Code. The extension expects the folder to contain a `main.tf` or `variables.tf` file. If there isn't one, you will get an error.
2. Select **IBM Cloud** > **Add deployable architecture manifest files**. The manifest files are created. If you already have an `ibm_catalog.json` file, it will be used instead.
3. Right-click the `ibm_catalog.json` file and select **IBM Cloud** > **Validate a deployable architecture on IBM Cloud**.
4. Follow the prompts. One of the prompts expects an API key from the IBM Cloud account where the infrastructure resources will be deployed during validation. Another prompt expects a Git token if your module repository is private.
5. The YAML inputs file will be opened and a prompt will ask you to edit the module input variables before continuing. Edit the values under the `inputs` property and save the file. Then, click **Continue**. The progress bar will indicate the progress of the validation.
6. When validation begins, an Output channel will be opened showing the validation logs. If it does not, under the **Output** view, select the channel **DA Validation** in the dropdown with the name and version of your deployable architecture.

**Note:** Validation can take a long time to complete. The **Output** channel will automatically refresh with the latest logs. The **Projects** and **Catalogs** explorers will automatically refresh as changes are made. You can also use the refresh button to manually refresh them.

You can also retrieve logs later by right-clicking on the manifest file and selecting **IBM Cloud** > **Show deployable architecture validation logs**. If the validation doesn't begin or there is an error during the validation, an error will be shown and you can try again later.

## Additional features

- In the explorer trees, you can right-click on a project, configuration, environment, catalog, or deployable architecture product to open the item in a browser or view documentation for a deployable architecture.
- In the **Projects** explorer tree, right-click on a configuration to validate, approve, deploy, or show the latest logs.
- In the **Catalogs** explorer tree, right-click on a deployable architecture version to validate it using a project or show validation logs.
- Additional menu items when right-clicking on a manifest JSON or YAML inputs file:
    - Share a deployable architecture in a private catalog by using a release branch.
    - Delete a deployable architecture

## Troubleshooting

### Signing into IBM Cloud in multiple VS Code windows

There is a known issue that causes errors and unexpected behavior when signing into an IBM Cloud account in multiple windows in VS Code. A subsequent patch will address this issue.

### Error signing into GitHub Enterprise

If you see an error about signing into GitHub Enterprise, set the GitHub Enterprise server in Settings -> Settings -> Extensions -> GitHub Enterprise Server Authentication Provider in the URI field to `https://github.ibm.com`.

### Getting logged out

There's an error that might occur when you sign in to IBM Cloud via the extension. This error might happen because after you first install the extension from the marketplace and attempt to sign in, the authentication might not stick. So, you will see that you're signed in but then are signed out shortly after. To fix this issue, restart VS Code and attempt to sign in again.

### Extension logs

All logs for the extension can be found in the **Output** view in the `IBM Cloud Deployable Architecture Builder` channel. You can change the log level by using the `Developer: Set Log Level` command in the Command Palette.

## Accessing the walkthrough in VS Code

When you open a `ibm_catalog` JSON for the first time, the walkthrough for the IBM Cloud Deployable Architecture Builder extension is displayed.

You can also view the walkthrough at any time by following either of these steps:

- Select **Help** > **Welcome**. You might need to select **More...** to view additional walkthroughs.
- Select **View** > **Command Palette**, and type `walkthrough`. Select **Welcome: Open Walkthrough...**, and then select **Get started with IBM Cloud Deployable Architecture Builder**.
