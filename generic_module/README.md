![License: CISCO](https://img.shields.io/badge/License-CISCO-blue.svg)
[![published](https://static.production.devnetcloud.com/codeexchange/assets/images/devnet-published.svg)](https://developer.cisco.com/codeexchange/github/repo/chrivand/securex_incident_correlator)

# SecureX Incident Correlator: Generic Module [NEEDS TO BE CUSTOMIZED]

## Features
* Looks for target sightings of fresh IoC's and sends them to the **Main Workflow**.

### Workflow operations:
1. This generic workflow can be editted to find and parse text items related to new malware campaigns.
2. It can check if this is the first time the workflow has run or if there are new text items:
     * If there was an update -> parse all the new text items.
     * If there was no update -> do nothing.
3.	During the parsing of the text items, the SecureX API is used to retrieve all the observables (using the Inspect API endpoint).
4.  It then removes observables with a clean disposition to avoid false positives.
5.  It will then checks for Target Sightings. If there is a Sighting of a Target, the sighting JSON is cleaned and a permanent sighting is created in the Private Intel DB. This sighting JSON is then sent to the **Main Workflow**.

> **Note:** This workflow is not finished and serves as generic example to use any tex input. This workflow still needs to be customized to your needs. More modules will be added.

![](../screenshots/generic_module.png)

## Required Targets and Accounts keys
- SecureX Access Token
- SecureX Private Intel DB (uses SecureX Access Token)

## Required Atomic Workflows
- All used atomics are [System Objects](https://ciscosecurity.github.io/sxo-05-security-workflows/atomics/system) and do not need to be imported.

## Setup instructions

1. Browse to your SecureX orchestration instance. This wille be a different URL depending on the region your account is in: 

* US: https://securex-ao.us.security.cisco.com/orch-ui/workflows/
* EU: https://securex-ao.eu.security.cisco.com/orch-ui/workflows/
* APJC: https://securex-ao.apjc.security.cisco.com/orch-ui/workflows/

> **Note:** as the workflow contains the **Main Workflow** as sub workflow, it could be that it clones (or overwrites) this main workflow. In that case you need to be careful and select a cloned import. You can then manually change the sub workflow in the module to your original main workflow.

2. Click on **Browse** and copy paste the content of the [generic_module_workflow.json](https://raw.githubusercontent.com/chrivand/securex_incident_correlator/main/generic_module/generic_module_workflow.json) file inside of the text window and click **Import**. Select **Import as a new workflow (clone)** if you have a previous version of this workflow, and you do not want to overwrite it. Alternatively, you can also [import this from GitHub directly](https://ciscosecurity.github.io/sxo-05-security-workflows/importing).

![](../screenshots/copy-paste.png)

3. You will be prompted for some credentials and targets. Please follow the instructions to make sure there are no more orange errors in the workflow and you can click **VALIDATE** in the top right of the workflow edit pane.

## Author(s)

* Christopher van der Made (Cisco)
