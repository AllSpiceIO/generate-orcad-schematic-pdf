# Generate a PDF from OrCAD schematics

Generate a PDF output file from an OrCAD schematic file on AllSpice Hub using
[AllSpice Actions](https://learn.allspice.io/docs/actions-cicd).

## Set up a Personal Access Token

Create a personal access token as an Actions
[secret](https://learn.allspice.io/docs/secrets-variables-keys-environment-vars).

In the following usage example, the personal access token is named PAT.

## Usage

Add the following steps to your actions:

```yaml
- name: Checkout
  uses: actions/checkout@v3

- name: Generate OrCAD Schematic PDF
  uses: https://hub.allspice.io/Actions/generate-orcad-schematic-pdf@v0.1
  with:
    # The repository that triggered this action
    repository: ${{ allspice.repository }}
    # The branch/ref that triggered this action
    ref: ${{ allspice.head_ref || allspice.ref_name }}
    # The sha that triggered this action
    sha: ${{ allspice.sha }}
    # URL of the AllSpice server
    allspice_hub_url: ${{ allspice.server_url }}
    # Name of the title block field to annotate with the AllSpice commit
    title_block_field: "Title"
    # Set this to true to commit back to the origin branch of the design file
    commit_to_branch: true
    # An auth token / personal access token with write permissions
    auth_token: ${{ secrets.PAT }}
```
