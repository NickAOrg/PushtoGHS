# Pre-Built Wizard

## Table of Contents

- [Overview](#overview)
- [Installation Prerequisites](#installation-prerequisites)
- [What is Pre-Built Wizard](#what-is-Pre-Built-wizard)
- [How to Install](#how-to-install)
- [Supported Components](#supported-components)
- [Creating A New Pre-Built](#creating-a-new-Pre-Built-Bundle)
- [Updating A Pre-Built Bundle](#updating-a-Pre-Built-Bundle)
- [Additional Information](#additional-information)

## Overview

This pre-built includes both the Prebuilt Wizard and Prebuilt Wizard Re-Discovery automation catalog items. The Pre-Built Wizard AC focuses on pre-built creation and export. More information can be found in the [What is Pre-Built Wizard section](#what-is-Pre-Built-wizard) 

>**Note**: The terms `Artifact` and `Pre-built` are synonyms.

## Installation Prerequisites

Users must satisfy the following pre-requisites:

<!-- Include any other required apps or adapters in this list -->
<!-- Ex.: EC2 Adapter -->
* Itential Automation Platform
  * `^2021.2`
* App-Artifacts
  * `6.1.16-2021.1.2`


## What is Pre-Built Wizard

The Pre-Built Wizard pre-built is composed of two automation catalog entries to help you create and update pre-builts. Pre-Built Wizard allows you to create new bundles (shown as installed prebuilt in admin essentials) from pre-defined entrypoint list (Operations Manager(s), Automation Catalog(s), and/or Workflow(s)). After performing discovery, Pre-Built Wizard will display the full list of components that will be used to create the Pre-Built bundle's artifact.json file. Users have the option to modify this list during the automation, provided Zero Touch mode is not selected. Pre-Built Wizard will install the Pre-Built into Admin Essentials and provide a download link for the bundle file. If components of this Prebuilt change over time, the Prebuilt Wizard Re-Discovery automation catalog item can be used run discovery on the prebuilt again and update the component list in Admin Essentials.

## How to Install

To install Pre-Built Wizard, verify you are running a supported version of Itential Automation Platform (IAP) as listed above in the [Requirements](#requirements) section. If you do not currently have App-Artifacts installed as a service on your node, the `.tgz` file or "tarball" can be obtained from the [Nexus repository](https://registry.aws.itential.com/#browse/browse:app-prebuilt_automations). Please refer to the instructions included in the App-Artifacts README to install it.

Pre-Built Wizard can be installed from within Admin Essentials. Simply search for `prebuilt-wizard` and click the **Install** button as shown below.

<!-- ![install](https://gitlab.com/itentialopensource/pre-built-automations/prebuilt-wizard/-/raw/release/2021.2/images/install.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/prebuilt-wizard/-/raw/release/2021.2/images/install.png" alt="install" width="800px">
</td></tr></table>

Alternatively, you may download the `artifact.json` file, and import it through admin essentials app.

## Supported Components

The Itential Automation Platform components that Pre-Built Wizard can currently consume include:

- Automation Catalog items
- Operations Manager items
- Form Builder Forms
- JSON-Forms
- Mop-Templates
- Mop-Analytic Templates
- Workflows
- Transformations
- Jinja2 Templates
- TextFSM Templates
- Golden Configuration Trees

## Creating A New Pre-Built bundle

To create a new Pre-Built bundle, you must fill out the necessary form data for the automation. 
These fields include:
- scope
- pre-built name
- pre-built description
- License (optional)
- contributor
- README
- categories (optional)
- keywords (optional)
- entry point(s)

<!-- ![create new Pre-Built](https://gitlab.com/itentialopensource/pre-built-automations/prebuilt-wizard/-/raw/release/2021.2/images/run_new.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/prebuilt-wizard/-/raw/release/2021.2/images/run_new.png" alt="create new Pre-Built" width="600px">
</td></tr></table>

Pre-builts must have a scope specified. 

It is important to remember that the entry point to the bundle for the Pre-Built Wizard automation Catalog _must_ be an Operations Manager(s), Automation Catalog(s), Workflow item(s). The item(s) should supply both a workflow and a form as an entry point for the Pre-Built. Any job variables required for the workflow to run should be supplied by the accompanying form, and will be accessible to the workflow via the `formData` object.

After you click the **Run** button, Pre-Built Wizard will discover all dependencies required by the workflow selected in the Automation Catalog item, as well as version information for each IAP application required to install the bundled Pre-Built. The results of the discovery will be displayed for you to confirm (when not running in Zero Touch mode).


## Updating A Pre-Built Bundle

The Prebuilt Wizard Re-Discovery automation catalog item consists of a form with one required field: the name of the Prebuilt installed in admin essentials. After selecting the Prebuilt to run Re-Discovery on, press start. If there are components that are no longer inlucded in the Prebuilt, be sure to remove them when working the first manual task in the workflow. Further, if there are any components that were manually added to the Prebuilt, ensure that those items are still present in this manual task. Any new components will be discovered and the new prebuilt contents will replace the old in Admin Essentials.

<!-- ![discovery](https://gitlab.com/itentialopensource/pre-built-automations/prebuilt-wizard/-/raw/release/2021.2/images/discovery.png) -->
<table><tr><td>
<img src="https://gitlab.com/itentialopensource/pre-built-automations/prebuilt-wizard/-/raw/release/2021.2/images/discovery.png" alt="discovery" width="400px">
</td></tr></table>

## Additional Information

Please use your Itential Service Desk account if support is needed when using the Pre-Built Wizard.
