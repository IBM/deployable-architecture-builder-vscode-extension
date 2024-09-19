# IBM Cloud Deployable Architecture Builder VS Code extension (POC)

This extension assists IaC developers create and maintain deployable architectures (DAs) by combining capabilities found in IBM Cloud Projects, Global Catalog, and Schematics.

## Installing the extension

The extension can be installed with the .vsix file by downloading one of the [releases](https://github.ibm.com/arf/epx-vscode-ext-poc/releases) and using the provided [vsix_install.sh](https://github.ibm.com/arf/epx-vscode-ext-poc/blob/main/scripts/vsix-install.sh) script. Alternatively, download the .vsix file and execute the following command in a terminal: `code --install-extension path-to-file.vsix`.

## Getting started

You can use the extension to develop a DA from a locally-cloned Terraform module.

### Prerequisites

1. A Terraform module in a public or private GitHub repository that is cloned to a local folder. For experimentation, you can make a fork of this [sample Terraform module](https://github.com/l2fprod/simple-da). If your repository is private, you will need a personal access token with `repo` and `read:user` permissions.
2. The local folder has been added to the VS Code workspace.
3. The IBM Cloud Deployable Architecture Builder VS Code extension has been installed along with all dependent extensions.
4. You've logged into your GitHub account using VS Code's GitHub authentication. This is the same mechanism used to access your repositories in the Source Control view container.
5. An IBM Cloud account in Production (cloud.ibm.com) or Staging (test.cloud.ibm.com).
6. Node v20.x. Errors while logging into IBM Cloud have been observed with v21 or greater.

### Log into an IBM Cloud account

1. Open the VS Code Command Palette (View -> Command Palette) and select `IBM Cloud: Login`.
2. If you need to change the login environment (Production or Staging), select `Change login environment`. After updating the setting, run the command again.
3. Choose your login method and follow the prompts.
4. Select the account to use.

After logging in, the projects and catalogs in that account will be shown in the explorer views, if any.

### Validating a DA on IBM Cloud

These steps assume you have logged in as described above. To validate a local Terraform module as a DA on IBM Cloud:

1. Right-click on your module folder in the workspace in VS Code. The extension expects the folder to contain a main.tf or variables.tf file. If there isn't one, you will get an error.
2. In the context menu, select `IBM Cloud -> Add deployable architecture manifest files`. The manifest files are created. If you already have an ibm_catalog.json file, it will be used instead.
3. Right-click on the new `ibm_catalog.json` file and select `IBM Cloud -> Validate a deployable architecture on IBM Cloud (interactive)`.
4. Follow the prompts. One of the prompts expects an API key from the IBM Cloud account where the infrastructure resources will be deployed during validation. Another prompt expects a Git token if your module repository is private.
5. The YAML inputs file will be opened and a prompt will appear asking you to edit the module input variables before continuing. Edit the values under the `moduleVariables.inputs` property and save the file. Then click `Continue`.
6. The progress bar in the lower right will indicate the progress of the validation.
7. When validation begins, an Output channel will be opened showing the validation logs. If it does not, under the Output view, select the channel `DA Validation` channel in the dropdown with the name and version of your DA.

**Note:** Validation can take a long time to complete. The Output channel will automatically refresh with the latest logs. The Projects and Catalogs explorers will automatically refresh as changes are made. You can also use the refresh button to manually refresh them.

You can also retrieve logs later by right-clicking on the manifest or inputs YAML file and selecting `IBM Cloud -> Show deployable architecture validation logs`. If the validation has not begun, an error will be shown and you can try again later.

### Additional features

*   In the explorer trees, you can right-click on a project, configuration, environment, catalog, or DA product to open the item in a browser or view documentation for a deployable architecture.
*   In the Project explorer tree, right-click on a configuration to validate, approve, deploy, or show latest logs.
*   In the Catalog explorer tree, right-click on a DA version to validate it using a project or show validation logs.
*   Additional menu items when right-clicking on a manifest JSON or YAML inputs file:
    *   Share a DA in a private catalog using a release branch.
    *   Delete a DA
    *   Initiate a validation again without going through the prompts by selecting the validation menu item on the YAML inputs file.

## Troubleshooting

### Error signing into GitHub Enterprise

If you see an error about signing into GitHub Enterprise, set the GitHub Enterprise server in Settings -> Settings -> Extensions -> GitHub Enterprise Server Authentication Provider in the URI field to `https://github.ibm.com`.

### Extension logs

All logs for the extension can be found in the Output view in the `IBM Cloud Deployable Architecture Builder` channel. You can change the log level using the `Developer: Set Log Level` command in the Command Palette.
