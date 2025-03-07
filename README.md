# Generate SBOM Action

This GitHub Action generates a Software Bill of Materials (SBOM) for Node.js applications using CycloneDX and uploads it to Dependency Track. It helps ensure that your projects have a complete inventory of components and dependencies, which is essential for managing security vulnerabilities.

## Features
- **Node.js Support**: Specifically designed for Node.js applications.
- **SBOM Generation**: Uses CycloneDX Node.js Module to generate an SBOM.
- **Artifact Upload**: Uploads the generated SBOM as a GitHub artifact.
- **Integration with Dependency Track**: Uploads the SBOM to a Dependency Track server for further analysis.

## Inputs

| Name             | Description                                      | Required | Default               |
|------------------|--------------------------------------------------|----------|-----------------------|
| node_version     | Node.js version to set up                       | Yes      | 20                    |
| server_hostname   | Dependency Track server hostname                 | Yes      |                       |
| api_key          | API key for Dependency Track                     | Yes      |                       |
| project_name     | Project name for Dependency Track                | Yes      |                       |
| project_version   | Project version for Dependency Track             | Yes      |                       |
| bom_filename     | Filename for the BOM                             | No       | ./bom/bom.xml        |

## Usage

To use this action in your workflow, add the following steps to your job:

```yaml
name: Generate SBOM
on:
  push:
    branches: [ "dev" ]
  tags: [ 'v*.*.*' ]

jobs:
  build-and-upload:
    runs-on: ubuntu-latest
    steps:
    - name: Generate and Upload SBOM
      uses: your-username/your-action-repo@v1
      with:
        node_version: '20'
        server_hostname: 'ccte-api-dependency-track.epa.gov'
        api_key: ${{ secrets.SECRET_OWASP_DT_KEY }}
        project_name: 'Your-Project-Name'
        project_version: ${{ github.ref_name }}
