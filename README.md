# Actions Composite Template

Composite action template to learn and seed other actions.

## Calling the action

This workflow will update 

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
    steps:

      - name: Powershell Module Setup
        uses: rulasg/psmodule-setup-action@dev
        with:
          Name: ProjectHelper
          AllowPreReleaseVersions: true
      
      - name: Check module installation
        shell: pwsh
        run: |
          Get-Module -ListAvailable
          Import-Module -Name ProjectHelper
          Get-Module -Name ProjectHelper

      - name: Update Project Due Dates
        id: udpate-due
        uses: rulasg/update-ProjectItemsStatusOnDueDate@mvp
        with:
          ProjectOwner: ${{ vars.DUE_OWNER }}
          ProjectNumber: ${{ vars.DUE_PROJECT_NUMBER }}
          DueDateFieldName: ${{ vars.DUE_FIELD_NAME }}
          Status: ${{ vars.DUE_STATUS }}
          TOKEN: ${{ secrets.GH_PAT }}
```
