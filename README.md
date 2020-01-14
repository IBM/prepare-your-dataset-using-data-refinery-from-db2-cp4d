[![Build Status](https://travis-ci.org/IBM/watson-banking-chatbot.svg?branch=master)](https://travis-ci.org/IBM/https://github.com/IBM/prepare-your-dataset-using-data-refinery-from-db2-cp4d)

# Prepare your Dataset for your ML Models using Data Refinery from Db2 on Cloud Pak for Data

In this Tutorial, we will perform Data Engineering operations on multiple datasets using Watson Data Refinery on Cloud Pak for Data. 

A Data Scientist cannot directly build a model based on the dataset, the data collection and analysis is very essential before building a model. In this Tutorial we demonstrate how data scientists can easily collect data from databases, analyse the data and enhance the data according to their requirements with the help of Watson Data Refinery on Cloud Pak for Data.

When you have completed this code pattern, you will understand how to:

* Create a set of ordered steps to cleanse, shape, and enhance data. 
* Create a connection with any database and Data Refinery.
* Prepare datasets specific to your ML Model.
* Save the datasets in any database of your choice.

<!--add an image in this path-->
![architecture](doc/source/images/architecture.png)

<!--Optionally, add flow steps based on the architecture diagram-->
## Flow

1. Create a connection to Db2.
2. Load the four tables in Data Refinery.
3. Join the four tables based on the primary keys and foreign keys.
4. Run the Data Refinery Job to save the joined Table in Db2.

<!--Optionally, update this section when the video is created-->
# Watch the Video

[![video]()]()

# Steps

1. [Download the Data](#1-download-the-data).
2. [Load the data into tables in Db2](#2-load-the-data-into-tables-in-db2).
3. [Create a Project in Cloud Pak for Data](#3-create-a-project-in-cloud-pak-for-data)
4. [Add Db2 connection to the project](#4-add-db2-connection-to-the-project).
5. [Add Data Refinery to the project](#5-add-data-refinery-to-the-project).
6. [Perform Data Engineering Operations in Data Refinery](#6-perform-data-engineering-operations-in-data-refinery).
7. [Save the Enhanced Dataset to a table in Db2](#7-save-the-enhanced-dataset-to-a-table-in-db2).

### 1. Download the data.

In this Tutorial we are going to use **Brazilian E-Commerce Public Dataset by Olist** from Kaggle. Download the dataset from the link given below.

* https://www.kaggle.com/olistbr/brazilian-ecommerce

After Downloading, Extract the `brazilian-ecommerce.zip` file.

We’ll be using the following files: 
1. [`brazilian-ecommerce/olist_orders_dataset.csv`]() : This is the core dataset. From each order you might find all other information.

2. [`brazilian-ecommerce/olist_order_items_dataset.csv`]() : This dataset includes data about the items purchased within each order.

3. [`brazilian-ecommerce/olist_products_dataset.csv`]() : This dataset includes data about the products sold by Olist.

4. [`brazilian-ecommerce/olist_sellers_dataset.csv`]() : This dataset includes data about the sellers that fulfilled orders made at Olist.


### 2. Load the data into tables in Db2

**NOTE: We are Assuming you have already Provisioned a Db2 Instance in your Cloud Pak for Data. If you do not have Db2 Instance Provisioned you can also use other on-prem, public or private Databases of your choice and load the datasets.**

* Open the Db2 Instance and click on load data.

![loadData](doc/source/images/loadData.png)

* Select the **olist_orders_dataset.csv** file and select next.

![browseFile](doc/source/images/browseFiles.png)

* Choose your namespace and create a table named **ORDERS** and select next.

![createTable](doc/source/images/createTable.png)

* You can preview the metadata of the table and select next.

![tableMetaData](doc/source/images/viewTableMeta.png)

* Click on **Begin Load** to import the downloaded `.csv` file into your Db2.

![beginLoad](doc/source/images/beginLoad.png)

* Wait for the upload to finish and then you can add the other three datasets in the similar way.

![waitForUpload](doc/source/images/waitForUpload.png)

* Once the table is being created, click on **Load More Data** to add the other three datasets.

![loadMoreData](doc/source/images/loadMoreData.png)


### 3. Import the Watson Assistant workspace

* Find the Watson Assistant service in your IBM Cloud Dashboard.
* Select the service, and then click **Launch tool**.
* Go to the **Skills** tab.
* Click **Create skill**.
* Click the **Import skill** tab.
* Click **Choose JSON file**, go to your cloned repo dir, and `Open` the workspace.json file in `data/conversation/workspaces/banking.json` (or the old full version in `full_banking.json`).
* Select **Everything**, and click **Import**.

To find the `WORKSPACE_ID` for Watson Assistant:

* Go back to the **Skills** tab.
* Click the three dots in the upper-right corner of the **watson-banking-chatbot** card, and select **View API Details**.
* Copy the `Workspace ID` GUID.
  ![view_api_details](doc/source/images/view_api_details.png)

*Optionally*, to view the assistant dialog, select the workspace and choose the
**Dialog** tab. Here's a snippet of the dialog:

![dialog](doc/source/images/dialog.PNG)

### 4. Load the Watson Discovery documents

Launch the **Watson Discovery** tool. Create a **new data collection**,
and give the data collection a unique name.

> Save the **environment_id** and **collection_id** for your `.env` file in the next step.

Under **Add data to this collection**, use **Drag and drop your documents here or browse from computer** to seed the content with the five documents in `data/discovery/docs`.

### 5. Configure credentials

The credentials for IBM Cloud services (Watson Assistant, Watson Discovery, 
Watson Tone Analyzer and Watson Natural Language Understanding) can be found in the **Services** menu in IBM Cloud
by selecting the **Service Credentials** option for each service.

The other settings for Watson Assistant and Watson Discovery were collected during the
earlier setup steps (``DISCOVERY_COLLECTION_ID``, ``DISCOVERY_ENVIRONMENT_ID``, and
``WORKSPACE_ID``).

Copy the [`env.sample`](env.sample) to `.env`.

```bash
cp env.sample .env
```
Edit the `.env` file with the necessary settings.

#### `env.sample:`

```bash
# Copy this file to .env and replace the credentials with
# your own before starting the app.

# Note: If you are using older services, you may need _USERNAME and _PASSWORD
# instead of _IAM_APIKEY.

# Watson Assistant
WORKSPACE_ID=<add_assistant_workspace>
ASSISTANT_URL=<add_assistant_url>
ASSISTANT_IAM_APIKEY=<add_assistant_iam_apikey>

# Watson Discovery
DISCOVERY_URL=<add_discovery_url>
DISCOVERY_ENVIRONMENT_ID=<add_discovery_environment_id>
DISCOVERY_COLLECTION_ID=<add_discovery_collection_id>
DISCOVERY_IAM_APIKEY=<add_discovery_iam_apikey>

# Watson Natural Language Understanding
NATURAL_LANGUAGE_UNDERSTANDING_URL=<add_nlu_url>
NATURAL_LANGUAGE_UNDERSTANDING_IAM_APIKEY=<add_nlu_iam_apikey>

# Watson Tone Analyzer
TONE_ANALYZER_URL=<add_tone_analyzer_url>
TONE_ANALYZER_IAM_APIKEY=<add_tone_analyzer_iam_apikey>

# Run locally on a non-default port (default is 3000)
# PORT=3000
```

### 6. Run the application

1. Install [Node.js](https://nodejs.org/en/) runtime or NPM.
1. Start the app by running `npm install`, followed by `npm start`.
1. Use the chatbot at `localhost:3000`.

> Note: The server host can be changed as required in the server.js file, and `PORT` can be set in the `.env` file.

<!--Add a section that explains to the reader what typical output looks like, include screenshots -->

# Sample output

![sample_output](doc/source/images/sample_output.png)

<!--Optionally, include any troubleshooting tips (driver issues, etc)-->

# Troubleshooting

* Error: Environment {GUID} is still not active, retry once status is active

  > This is common during the first run. The app tries to start before the Watson Discovery
environment is fully created. Allow a minute or two to pass. The environment should
be usable on restart. If you used **Deploy to IBM Cloud** the restart should be automatic.

* Error: Only one free environment is allowed per organization

  > To work with a free trial, a small free Watson Discovery environment is created. If you already have
a Watson Discovery environment, this will fail. If you are not using Watson Discovery, check for an old
service thay you might want to delete. Otherwise, use the `.env DISCOVERY_ENVIRONMENT_ID` to tell
the app which environment you want it to use. A collection will be created in this environment
using the default configuration.

<!-- keep this -->
## License

This code pattern is licensed under the Apache License, Version 2. Separate third-party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1](https://developercertificate.org/) and the [Apache License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache License FAQ](https://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)

