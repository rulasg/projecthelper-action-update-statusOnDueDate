# Actions Composite Template

Composite action template to learn and seed other actions.

## Calling the action

This workflow will run a job with a step that will call the action and a job that will call the resusable workflow that will call the action.

```yaml
name: Call Actions Composite Template

on: 
  workflow_dispatch:

jobs:
  ACT-call:
    name: Call to Actions Composite template
    runs-on: ubuntu-latest

    steps:

      # call the action with no parameters
      - name: Execute Actions-composite-template action
        id: actions_composite
        uses: rulasg/actions-composite-template@main

      # Check step output value of the action
      - run: echo "The output was ${{ steps.actions_composite.outputs.random-number }}"
        shell: bash
       
      # call the action with parameters
      - uses: rulasg/actions-composite-template@main
        with:
          who-to-greet: "Raúl"

  ACT-reusable:
    # call the reusable WF
    uses: rulasg/actions-composite-template/.github/workflows/actions-composite-template.yaml@main
```
