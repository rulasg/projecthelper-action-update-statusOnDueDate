# ProjectHelper Update Status on Due Date

## Description

This actions allows you to update the status of project items based on the value of a date field. Status will be changed if the date field has a date before or equal to the current date.

## Calling the action

This workflow will update the status of project items based on the value of a date field. Status will be changed if the date field has a date before or equal to the current date.

For loading ProjectHelper module, the action will use the `rulasg/psmodule-setup-action` action. This action will install the ProjectHelper module from the PowerShell Gallery.

```yaml
name: Update Project Due Date
on:
  # Run manually
  workflow_dispatch:

    # run at 5am every morning
  schedule:
    - cron: '0 5 * * *' 
jobs:
  validation:
    name: Update Project Due Date
    runs-on: ubuntu-latest

    env:
      GH_TOKEN: ${{ secrets.GH_PAT }}
      DUE_OWNER: ${{ vars.DUE_OWNER }}
      DUE_PROJECT_NUMBER: ${{vars.DUE_PROJECT_NUMBER}}
      DUE_FIELD_NAME: ${{ vars.DUE_FIELD_NAME }}
      DUE_STATUS: ${{ vars.DUE_STATUS }}

    steps:

    # Install ProjectHelper module
      - name: Powershell Module Setup
        uses: rulasg/psmodule-setup-action@v2
        with:
          Name: ProjectHelper
          AllowPreReleaseVersions: true

      # ProjectHelper Update Status on Due Date run
      - name: Update Project Due Dates
        id: updated-due
        uses: rulasg/update-ProjectItemsStatusOnDueDate@mvp
        with:
          TOKEN: ${{ env.GH_TOKEN }}
          ProjectOwner: ${{ env.DUE_OWNER }}
          ProjectNumber: ${{ env.DUE_PROJECT_NUMBER }}
          DueDateFieldName: ${{ env.DUE_FIELD_NAME }}
          Status: ${{ env.DUE_STATUS }}

```
