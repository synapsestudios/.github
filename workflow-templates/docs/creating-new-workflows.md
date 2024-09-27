# Creating and Using Starter Workflows

## Creating starter workflows

Full documentation can be found [here](https://docs.github.com/en/actions/using-workflows/creating-starter-workflows-for-your-organization)

> Note: To avoid duplication among starter workflows you can call reusable workflows from within a workflow. This can help make your workflows easier to maintain. For more information, see "Reusing workflows."

This procedure demonstrates how to create a starter workflow and metadata file. The metadata file describes how the starter workflows will be presented to users when they are creating a new workflow.

### 1. Create your new workflow file inside the workflow-templates directory.  
---
If you need to refer to a repository's default branch, you can use the `$default-branch` placeholder. When a workflow is created the placeholder will be automatically replaced with the name of the repository's default branch.

For example, this file named `octo-organization-ci.yml` demonstrates a basic workflow.

```
name: Octo Organization CI

on:
  push:
    branches: [ $default-branch ]
  pull_request:
    branches: [ $default-branch ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Run a one-line script
        run: echo Hello from Octo Organization
```

### 2. Create a metadata file inside the `workflow-templates` directory. 
--- 
The metadata file must have the same name as the workflow file, but instead of the `.yml` extension, it must be appended with `.properties.json`. For example, this file named `octo-organization-ci.properties.json` contains the metadata for a workflow file named `octo-organization-ci.yml`:
```
{
    "name": "Octo Organization Workflow",
    "description": "Octo Organization CI starter workflow.",
    "iconName": "example-icon",
    "categories": [
        "Go"
    ],
    "filePatterns": [
        "package.json$",
        "^Dockerfile",
        ".*\\.md$"
    ]
}
```

### Metadata fields
- `name` - Required. The name of the workflow. This is displayed in the list of available workflows.
- `description` - Required. The description of the workflow. This is displayed in the list of available workflows.
- `iconName` - Optional. Specifies an icon for the workflow that's displayed in the list of workflows. The `iconName` must be the name of an SVG file, without the file name extension, stored in the `workflow-templates` directory. For example, an SVG file named `example-icon.svg` is referenced as `example-icon`.
- `categories` - Optional. Defines the language category of the workflow. When a user views the available starter workflows for a repository, the workflows that match the identified language for the project are featured more prominently. For information on the available language categories, see https://github.com/github/linguist/blob/master/lib/linguist/languages.yml.
- `filePatterns` - Optional. Allows the workflow to be used if the user's repository has a file in its root directory that matches a defined regular expression.

To add another starter workflow, add your files to the same workflow-templates directory.

## Using Starter Workflows

Full documentation can be found [here](https://docs.github.com/en/actions/using-workflows/using-starter-workflows)

Anyone with write permission to a repository can set up GitHub Actions starter workflows for CI/CD or other automation.

1. On GitHub.com, navigate to the main page of the repository.

2. Under your repository name, click the
Actions tab in the main repository navigation

3. If you already have a workflow in your repository, click New workflow.

4. The "Choose a workflow" page shows a selection of recommended starter workflows. Find the starter workflow that you want to use, then click `Configure`. To help you find the starter workflow that you want, you can search for keywords or filter by category.

5. If the starter workflow contains comments detailing additional setup steps, follow these steps. Many of the starter workflow have corresponding guides. For more information, see the [GitHub Actions guides](https://docs.github.com/en/actions/guides).

6. Some starter workflows use secrets. For example, `${{ secrets.npm_token }}`. If the starter workflow uses a secret, store the value described in the secret name as a secret in your repository. For more information, see "[Encrypted secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)."

7. Optionally, make additional changes. For example, you might want to change the value of `on` to change when the workflow runs.

8. Click `Start commit`.

9. Write a commit message and decide whether to commit directly to the default branch or to open a pull request.
