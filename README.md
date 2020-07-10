# GitHub Action - Generate Release Note
This GitHub action generates a release note text for a merged pull request by looking at the issues that it has solved.

![Github JavaScript Actions CI/CD](https://github.com/dolittle/generate-release-note-action/workflows/Github%20JavaScript%20Actions%20CI/CD/badge.svg)

### Pre requisites
Create a workflow `.yml` file in your `.github/workflows` directory. An [example workflow](#example-workflow) is available below.

For more information, reference the GitHub Help Documentation for [Creating a workflow file](https://help.github.com/en/articles/configuring-a-workflow#creating-a-workflow-file)

### Inputs
- `issues`: A json object with the issues that the pr has solved
- `version`: The version that triggerered the release

### Outputs
- `release-note`: The generated release note

### Example Workflow
```yaml
on:
  push:
    branches:
    - '**'
  pull_request:
    types: [closed]

name: GitHub action workflow name

jobs:
  context:
    name: Job name
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Generate release note
        uses: dolittle/generate-release-note-action@v1
        with:
          issues: '{"some issue title": { "reference": "org/repo/issues/123", "type": "bug" }}'
          version: 2.0.0
        
```
### Example Workflow - With dolittle/extract-issues-action
```yaml
on:
  push:
    branches:
    - '**'
  pull_request:
    types: [closed]

name: GitHub action workflow name

jobs:
  context:
    name: Job name
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Extract issues
        id: issues
        uses: dolittle/extract-issues-action@v1
      - name: Generate release note
        uses: dolittle/generate-release-note-action@v1
        with:
          issues: ${{ steps.issues.outputs.issues }}
          version: 2.0.0
        
```
## Contributing
We're always open for contributions and bug fixes!

### Pre requisites
node <= 12
yarn
git
