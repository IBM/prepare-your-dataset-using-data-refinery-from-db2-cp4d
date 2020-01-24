---
#Front matter (metadata).
abstract:               # REQUIRED

authors:
 - name: "Manoj Jahgirdar"
   email: "manoj.jahgirdar@in.ibm.com"
 - name: "Smruthi Raj Mohan"
   email: "smrraj32@in.ibm.com"
 - name: "Srikanth Manne"
   email: "srikanth.manne@in.ibm.com"
 - name: "Manjula G. Hosurmath"
   email: "mhosurma@in.ibm.com"

completed_date: 2020-01-20

components:
- slug: "ibm-db2-database"
  name: "IBM Db2 Database"
  url: "https://www.ibm.com/analytics/us/en/db2/"
  type: "component"
- slug: "cloud-pak-for-data"
  name: "IBM Cloud Pak for Data"
  url: "https://www.ibm.com/analytics/cloud-pak-for-data"
  type: "component"

draft: true|false       # REQUIRED

excerpt:                # REQUIRED

keywords:               # REQUIRED - comma separated list

last_updated:           # REQUIRED - Note: date format is YYYY-MM-DD

primary_tag:          # REQUIRED - Note: Choose only only one primary tag. Multiple primary tags will result in automation failure. Additional non-primary tags can be added below.

pta:                    # REQUIRED - Note: can be only one
# For a full list of options see https://github.ibm.com/IBMCode/Definitions/blob/master/primary-technology-area.yml
# Use the "slug" value found at the link above to include it in this content.
# Example (remove the # to uncomment):
 # - "cloud, container, and infrastructure"

pwg:                    # REQUIRED - Note: can be one or many
# For a full list of options see https://github.ibm.com/IBMCode/Definitions/blob/master/portfolio-working-group.yml
# Use the "slug" value found at the link above to include it in this content.
# Example (remove the # to uncomment):
# - "containers"

related_content:        # OPTIONAL - Note: zero or more related content
  - type: announcements|articles|blogs|patterns|series|tutorials|videos
    slug:

related_links:           # OPTIONAL - Note: zero or more related links
  - title:
    url:
    description:

runtimes:               # OPTIONAL - Note: Select runtimes from the complete set of runtimes below. Do not create new runtimes. Only use runtimes specifically in use by your content.
# For a full list of options see https://github.ibm.com/IBMCode/Definitions/blob/master/runtimes.yml
# Use the "slug" value found at the link above to include it in this content.
# Example (remove the # to uncomment):
 # - "asp.net 5"

series:                 # OPTIONAL
 - type:
   slug:

services:               # OPTIONAL - Note: please select services from the complete set of services below. Do not create new services. Only use services specifically in use by your content.
# For a full list of options see https://github.ibm.com/IBMCode/Definitions/blob/master/services.yml
# Use the "slug" value found at the link above to include it in this content.
# Example (remove the # to uncomment):
# - "blockchain"

subtitle:               # REQUIRED

tags:
# Please select tags from the complete set of tags below. Do not create new tags. Only use tags specifically targeted for your content. If your content could match all tags (for example cloud, hybrid, and on-prem) then do not tag it with those tags. Less is more.
# For a full list of options see https://github.ibm.com/IBMCode/Definitions/blob/master/tags.yml
# Use the "slug" value found at the link above to include it in this content.
# Example (remove the # to uncomment):
 # - "blockchain"

title:                  # REQUIRED

translators:             # OPTIONAL - Note: can be one or more
  - name:
    email:

type: tutorial

---

In this Tutorial, we will perform Data Engineering operations on multiple datasets using Watson Data Refinery on Cloud Pak for Data / Watson Studio on IBM Cloud.

A Data Scientist cannot directly build a model based on the dataset, the data collection and analysis is very essential before building a model. In this Tutorial we demonstrate how data scientists can easily collect data from databases, analyse the data and enhance the data according to their requirements with the help of Watson Data Refinery on Cloud Pak for Data / Watson Studio on IBM Cloud.

## Learning objectives

When you have completed this code pattern, you will understand how to:

* Create a set of ordered steps to cleanse, shape, and enhance data. 
* Create a connection with any database and Data Refinery.
* Prepare datasets specific to your ML Model.
* Save the datasets in any database of your choice.

## Prerequisites

1. Any SQL Database.
>In this Tutorial we have demonstrated with [Db2 on Cloud Pak for Data](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/svc/db2z/create_database_db2z.html) and [Db2 on Cloud](https://cloud.ibm.com/catalog/services/db2).

2. [IBM Cloud Account](https://cloud.ibm.com/) - If you prefer to deploy on IBM Cloud.

## Estimated time

Completing this tutorial should take about 30 minutes.

## Steps

Follow the **Deploy on Cloud Pak for Data** Tutorial if you wish to deploy on Cloud Pak for Data or **Deploy on IBM Cloud** Tutorial if you wish to deploy on IBM Cloud.

## Deploy on Cloud Pak for Data

Follow the tutorial to deploy on Cloud Pak for Data.

- [Deploy on Cloud Pak for Data](https://github.com/IBM/prepare-your-dataset-using-data-refinery-from-db2-cp4d/blob/master/cloudpak.md)

## Deploy on IBM Cloud

Follow the tutorial to deploy on IBM Cloud.

- [Deploy on IBM Cloud](https://github.com/IBM/prepare-your-dataset-using-data-refinery-from-db2-cp4d/blob/master/publiccloud.md)

## Summary

A Data Scientist cannot directly build a model based on the dataset, the data collection and analysis is very essential before building a model. This tutorial allows Data Scientists to perform data engineering operations to any data easily hence reducing the time spent on a data engineering operation and Data Scientists can focus mainly on building a model. The main advantage of the Data Refinery capabilities of IBM Cloud Pak for Data is Creating a set of ordered steps to cleanse, shape, and enhance data.
