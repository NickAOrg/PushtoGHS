<!-- This is a comment in md (Markdown) format, it will not be visible to the end user -->


<!-- Update the below line with your artifact name -->


# MongoDB CRUD Automation

<!-- Leave TOC intact unless you've added or removed headers -->

## Table of Contents

*  [Overview](#overview)
*  [Features](#features)
*  [Requirements](#requirements)
*  [How to Run](#how-to-run)
*  [Components](#components)
*  [Workflows](#workflows)
*  [JSON Forms](#json-forms)
*  [Additional Information](#additional-information)

## Overview

The **Mongo CRUD Operations** artifact was built to showcase the basic operations that can be performed on MongoDB. More specifically, this artifact was created to automate some of the manual tasks that are performed directly in the Mongo UI. 

The Mongo CRUD Operations artifact was built to showcase the basic operations that can be performed on MongoDB. This was created to automate some of the manual tasks that was performed directly on the Mongo UI using the tasks exposed by the Itential open source adapter: **adpater_db-mongo**. A description for each operation is listed below:

*  **Create:** Create a new document and insert it into the desired collection in Mongo.
*  **Read:** Perform a search operation on the collection based on select filters and sort the output to display the list of documents.
*  **Update:** Search a desired document from a collection and perform an update operation on the result.
*  **Delete:** Search a desired document from a collection and perform a delete operation on the result.

<!-- Workflow(s) Image Placeholder - TO BE ADDED DIRECTLY TO GitLab -->

<!-- REPLACE COMMENT BELOW WITH IMAGE OF YOUR MAIN WORKFLOW -->

<table><tr><td>

<img  src="https://gitlab.com/itentialopensource/pre-built-automations/mongo-crud-operations/-/raw/master/images/Main_WF.png"  alt="workflow"  width="800px">

</td></tr></table>

This workflow serves as an entry point for Automation Catalog to run the use cases described above. The running path of the workflow depends on the operation selected by the user. To create a document, or to add filters and options to the search results, the user is provided with a JSON form to input data.

<!-- REPLACE COMMENT ABOVE WITH IMAGE OF YOUR MAIN WORKFLOW -->

## Features

For the **Mongo CRUD Operations** artifact:

* Each operation is designed as a stand-alone application (child workflows) which can be re-used in different workflows and applications.
* Provides an example to show creation of documents through JSON forms and addition to the collection.
* Performs a search operation on the collection by adding filters, sorting the search results, and limiting the number of results.
* Performs an update operation by choosing to update an existing document or by adding a new document to the collection.
* Performs a delete operation by filtering the search results and selecting the document to delete from the collection(currently only support string id).

## Requirements

* The main requirement to use this artifact is a running instance of the Itential OpenSource `adapter_db-mongo`, which can be found in [adapter-db_mongo](https://gitlab.com/itentialopensource/adapters/persistence/adapter-db_mongo).
* Itential Automation Platform
 * `^2021.1`


## How to Run

The artifact can be run using **Automation Catalog**. Use the following steps to complete the form:

1. Provide a suitable description for the job.
1. Select the appropriate **adapter db-mongo instance** from the dropdown.
1. Input the name of the **collection** that is needed to perform the CRUD operations.
1. Select the required **CRUD operation** to be performed from the dropdown.

> **Note:** All fields are mandatory except for the job description.

<table><tr><td>

<img  src="https://gitlab.com/itentialopensource/pre-built-automations/mongo-crud-operations/-/raw/master/images/AC_JSON_Form.png"  alt="form item"  width="600px">

</td></tr></table>

## Components

This artifact is comprised of a set of modular components intended to modularize and simplify the CRUD operations.

### Workflows

#### Sort and Filter Results

The Artifact provides the opportunity to sort, filter and limit the number of results from the collection. These options help in generating a customized result set based on the user's requirements. The input for the sort and filter are in the form of objects, whereas the limit includes the number of results the user expects to see. It also has the option to start the search from a specific number, thereby ignoring the documents which appear before the selected number. 

<table><tr><td>

<img  src="https://gitlab.com/itentialopensource/pre-built-automations/mongo-crud-operations/-/raw/master/images/Mongo_CRUD_Child_WF.png"  alt="Mongo Child Workflow"  width="600px">

</td></tr></table>

#### Create Document

There are multiple routes in the parent workflow which is run based on the user's selection. In the initial path, the user can **Create** a document and add it to the collection. Edit the form **Mongo_CRUD_Create_Form** to include the required fields that are to be added for the document. This allows the user to dynamically create an object to be sent to the **Mongo Create** task to be stored in the collection.

<table><tr><td>

<img  src="https://gitlab.com/itentialopensource/pre-built-automations/mongo-crud-operations/-/raw/master/images/Mongo_Create_WF.png"  alt="Mongo Create Workflow"  width="600px">

</td></tr></table>

#### Read Document

To perform a **Read** operation, the flow is directed to a child workflow to filter results and return those results in the desired manner. The child workflow is designed to take input from the **Mongo_CRUD_Search_Form** which provides options (i.e., filter, sort, start and limit) to filter the results and return the result in the desired manner. The output of the workflow is converted to string for readability.

<table><tr><td>

<img  src="https://gitlab.com/itentialopensource/pre-built-automations/mongo-crud-operations/-/raw/master/images/Mongo_Read_WF.png"  alt="Mongo Read Workflow"  width="600px">

</td></tr></table>

#### Update Document

The **Update** operation follows a similar path to the Read operation, by passing through the child workflow to filter out available documents based on the user's requirements. The available results can be used to display the required fields in a list that allows the user to select the intended document by choosing a value from the dropdown. The field can be selected by editing the query response. The ** Mongo Update** task requires the data to be updated on the document in the form of an object. Edit the form **Mongo_CRUD_Update_Form** to include the required fields to be updated for the document.

<table><tr><td>

<img  src="https://gitlab.com/itentialopensource/pre-built-automations/mongo-crud-operations/-/raw/master/images/Mongo_Update_WF.png"  alt="Mongo Update Workflow"  width="600px">

</td></tr></table>

#### Delete Document

The **Delete** operation is similar to the Update operation, where the results are filtered within the child workflow and the user can edit the query to retrieve the results and see the ID of the results within the dropdown. On selecting the document, the **deleteById** task performs a delete operation and the document is deleted from the collection in Mongo.

  <table><tr><td>

<img  src="https://gitlab.com/itentialopensource/pre-built-automations/mongo-crud-operations/-/raw/master/images/Mongo_Delete_WF.png"  alt="Mongo Delete Workflow"  width="600px">

</td></tr></table>
  
### JSON Forms

The JSON forms for the artifact are presented below.

#### Mongo_CRUD_Document_Form

This JSON form must be edited to include the fields that need to be reflected in the Mongo document. The existing elements in the form can be edited to include the required field names.

<table><tr><td>

<img  src="https://gitlab.com/itentialopensource/pre-built-automations/mongo-crud-operations/-/raw/master/images/Mongo_CRUD_Document_Form.png"  alt="crud_create_form"  width="400px">

</td></tr></table>

#### Mongo_CRUD_Search_Form

This JSON form allows the user to enter options to filter results for Read, Update, and Delete operations.

<table><tr><td>

<img  src="https://gitlab.com/itentialopensource/pre-built-automations/mongo-crud-operations/-/raw/master/images/Mongo_CRUD_Search_Form.png"  alt="crud_search_form"  width="400px">

</td></tr></table>

## Additional Information

Please use your Itential Customer Success account if support is needed when using this artifact.
