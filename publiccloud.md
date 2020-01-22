# Deploy on IBM Cloud

### Step 1: Download the data

In this Tutorial we are going to use **Brazilian E-Commerce Public Dataset by Olist** from Kaggle. Download the dataset from the link given below.

* https://www.kaggle.com/olistbr/brazilian-ecommerce

After Downloading, Extract the `brazilian-ecommerce.zip` file.

We’ll be using the following files: 
1. [`brazilian-ecommerce/olist_orders_dataset.csv`]() : This is the core dataset. From each order you might find all other information.

2. [`brazilian-ecommerce/olist_order_items_dataset.csv`]() : This dataset includes data about the items purchased within each order.

3. [`brazilian-ecommerce/olist_products_dataset.csv`]() : This dataset includes data about the products sold by Olist.

4. [`brazilian-ecommerce/olist_sellers_dataset.csv`]() : This dataset includes data about the sellers that fulfilled orders made at Olist. 

### Step 2: Load the data into tables in Db2

**NOTE: You can Skip this step if you do not want to use Db2 Instance as you can use other on-prem, public or private Databases of your choice and load the datasets.**

* Create a [Db2 Resource](https://cloud.ibm.com/catalog/services/db2).
![db2Resource](doc/source/images/db2Resource.png)

* Once the Resource is ready click on **Service Credentials** on the left panel and then click **view credentials**.
![viewCredentials](doc/source/images/viewCredentials.png)

**NOTE: Copy these credentials as it will be used in [Step 4](#-4-add-db2-connection-to-the-project).**

* Now click on **Manage** on the left panel and then click on **Open Console** to open the Db2 Console.

![openConsole](doc/source/images/openConsole.png)

* Once the Db2 Console is opened, click on **load data.**

![loadData](doc/source/images/loadData.png)

* Select the **olist_orders_dataset.csv** file and select next.

![browseFile](doc/source/images/browseFiles.png)

* Choose your namespace and create a table named **ORDERS** and select next.

**Note: Make sure you have selected the default schema of your database. In case of Db2 your default Schema is your username.**

![createTable](doc/source/images/createTable.png)

* You can preview the metadata of the table and select next.

![tableMetaData](doc/source/images/viewTableMeta.png)

* Click on **Begin Load** to import the downloaded `.csv` file into your Db2.

![beginLoad](doc/source/images/beginLoad.png)

* Wait for the upload to finish.

![waitForUpload](doc/source/images/waitForUpload.png)

* Once the table is created, click on **Load More Data** to add the other three datasets.

![loadMoreData](doc/source/images/loadMoreData.png)

* Load the `olist_order_items_dataset.csv` and name the table **ORDERITEMS**, load `olist_products_dataset.csv` and name the table **PRODUCTS** & finally load `olist_sellers_dataset.csv` and name the table **SELLERS** by repeating the above steps.

### Step 3: Create a Watson Studio Service

Once the Database is ready, we will start using the database in our Watson Studio on IBM Cloud. 

* Create [**Watson Studio**](https://cloud.ibm.com/catalog/services/watson-studio) service.

![createwatsonstudio](/doc/source/images/createwatsonstudio.png)

* Then click on **Get Started**.

* In Watson Studio click **`Create a project > Create an empty project`** and name it **_`Retail`_**.

![watsonstudioproject](/doc/source/images/watsonstudioproject.png)

### Step 4: Add Db2 connection to the project

Now that we have created a project, we will start adding components to our project. We will start by adding Db2 Connection to our project first.

* Click on **Add to Project** and select **Connection**. If you have followed [step 2](#2-load-the-data-into-tables-in-db2) select **Db2** from the list and add the credentials of your provisioned Db2 Instance. If you have a different database then you can select that and fill in the credentials.

![gif](doc/source/images/create_connection2.gif)

* After filling the credentials click on **Create**.

![connection](doc/source/images/connImage2.png)

**NOTE: The Database Credentials are generated in [Step 2]()**

### Step 5: Add Data Refinery to the project and perform Data Engineering Operations

#### 5.1 Add Data Refinery to the project

We will add Data Refinery Flow in the similar way.

* Click on **Add to Project** and select **Data Refinery Flow**. 

![dataRefinery](doc/source/images/dataRefinery2.png)

* Under *Assets* click on *Connections* and then click on the connection that you created in [step 4](#4-add-db2-connection-to-the-project), click on the schema of your Database and select the table **ORDERS** and finally click on ADD.

![selectOrders](doc/source/images/selectOrders2.png)

* You will now see the Data Refinery Dashboard.

![dataRefineryDashboard](doc/source/images/dataRefineryDashboard2.png)

#### 5.2 Perform Data Engineering Operations

5.2.1 We will be performing the **Join** in this tutorial. Click on **Operation** on the top left and click on **Join**.

![joinOperation](doc/source/images/joinOperation2.png)

5.2.2 Select the **Inner Join** and add the second dataset from our db2 by clicking the button shown.

![addDataset](doc/source/images/addDataset12.png)

5.2.3 We will first join the ORDERS table with ORDERITEMS table from db2. Under *Assets* click on *Connections* and then click on the connection that you created in [step 4](#4-add-db2-connection-to-the-project), click on the schema of your Database and select the table **ORDERITEMS** and finally click on APPLY.

![selectOrderItems](doc/source/images/selectOrderItems2.png) 

5.2.4 Select the **JOIN KEYS** for ORDERS and ORDERITEMS as **order_id** and click NEXT.

![keyOrderId](doc/source/images/keyOrderId2.png) 

5.2.5 Click on *APPLY* to apply the Join Operation.

![applyOperation](doc/source/images/applyOperation2.png) 

* Repeat the _steps 5.2.1_ to _step 5.2.5_ to keep joining data to the original by product id and seller id.

* Select the **JOIN KEYS** for ORDERS and PRODUCTS as **product_id**.

![](doc/source/images/keyProductId2.png)

* Select the **JOIN KEYS** for ORDERS and SELLERS as **seller_id**.

![](doc/source/images/keySellerId2.png)

### Step 6: Save the Enhanced Dataset to a table in Db2 and Run the Job

Once the operations are performed its time to save the result in a table. By Default the resulting table will be saved as a `.csv` file in the project but we will change the output path to the Db2 database. 

#### 6.1 Save the Enhanced Dataset to a table in Db2

* Click on the **Edit** button on the top right as shown.

![editButton](doc/source/images/editButton2.png)

* Then click on the **Pencil button** as shown.

![edit2](doc/source/images/edit22.png)

* Click on **Change Location**, under *Assets* click on *Connections* and then click on the connection that you created in [step 4](#4-add-db2-connection-to-the-project), click on the schema of your Database and finally click on **SAVE LOCATION**.

![selectDbLocation](doc/source/images/selectDbLocation2.png)

* Name the Dataset **four_tables_merged** and click on done.
![tickButton](doc/source/images/tickButton2.png) 

#### 6.2 Run the Data Refinery Job

* Click on the **Save and create a Job** as shown.

![createJob](doc/source/images/createJob2.png)

* Give a name to the Job and finally click on **Create and Run**.

![createRun](doc/source/images/createRun2.png)

* The Job will start **running** and it will take approximately 4-5min to complete.

![runningJob](doc/source/images/runningJob2.png)

* Once The Job **Status** becomes **Completed**, you can check your database to see a new table with a name **four_tables_merged** with the result.
