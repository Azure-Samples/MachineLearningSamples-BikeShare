# Bike-share tutorial: Advanced data preparation with Azure Machine Learning Workbench

This is a companion sample project of the Azure Machine Learning and [Bike Share Tutorial](https://docs.microsoft.com/en-us/azure/machine-learning/preview/tutorial-bikeshare-dataprep). 


Azure Machine Learning services (preview) is an integrated, end-to-end data science, and advanced analytics solution for professional data scientists to prepare data, develop experiments and deploy models at cloud scale.

In this tutorial, you use Azure Machine Learning services (preview) to learn how to:
> [!div class="checklist"]
> * Prepare data interactively with the Azure Machine Learning Data Preparation tool
> * Import, transform, and create a test dataset
> * Generate a Data Preparation package
> * Run the Data Preparation Package using Python
> * Generate a training dataset by reusing the Data Preparation package for additional input files
> * Execute scripts in a local Azure CLI window.
> * Execute scripts in a cloud Azure HDInsight environment.


## Prerequisites
* Azure Machine Learning Workbench needs to be installed locally. For more information, follow the [installation Quickstart](quickstart-installation.md).
* If you don't have the Azure CLI installed, follow the instructions to [install the latest Azure CLI version].(https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
* An [HDInsights Spark cluster](how-to-create-dsvm-hdi.md#create-an-apache-spark-for-azure-hdinsight-cluster-in-azure-portal) needs to be created in Azure.
* An Azure Storage Account.
* Familiarity with creating a new project in the Workbench.
* Although it is not required, it is helpful to have [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/) installed so you can upload, download, and view the blobs in your storage account. 

## Data acquisition
This tutorial uses the [Boston Hubway dataset](https://s3.amazonaws.com/hubway-data/index.html) and Boston weather data from [NOAA](http://www.noaa.gov/).

1. Download the data files from the following links to your local development environment. 
   * [Boston weather data](https://azuremluxcdnprod001.blob.core.windows.net/docs/azureml/bikeshare/BostonWeather.csv). 
   * Hubway trip data from Hubway website.

      - [201501-hubway-tripdata.zip](https://s3.amazonaws.com/hubway-data/201501-hubway-tripdata.zip)
      - [201504-hubway-tripdata.zip](https://s3.amazonaws.com/hubway-data/201504-hubway-tripdata.zip)
      - [201510-hubway-tripdata.zip](https://s3.amazonaws.com/hubway-data/201510-hubway-tripdata.zip)
      - [201601-hubway-tripdata.zip](https://s3.amazonaws.com/hubway-data/201601-hubway-tripdata.zip)
      - [201604-hubway-tripdata.zip](https://s3.amazonaws.com/hubway-data/201604-hubway-tripdata.zip)
      - [201610-hubway-tripdata.zip](https://s3.amazonaws.com/hubway-data/201610-hubway-tripdata.zip)
      - [201701-hubway-tripdata.zip](https://s3.amazonaws.com/hubway-data/201701-hubway-tripdata.zip)

2. Unzip each .zip file after download.

## Upload data files to Azure Blob storage
You can use blob storage to host your data files.

1. Use the same Azure Storage account that is used for the HDInsight cluster you are using.

![hdinsightstorageaccount.png](media/hdinsightstorageaccount.png)

2. Create a new container named '**data-files**' to store the BikeShare data files.

4. Upload the data files. Upload the `BostonWeather.csv` to a folder named `weather`, and the trip data files to a folder named `tripdata`.

![azurestoragedatafile.png](media/azurestoragedatafile.png)

> [!TIP]
> You may also use **Azure Storage Explorer** to upload blobs. This tool can be used when you want to view the contents of any of the files generated in the tutorial as well.

## Learn about the datasets
1. The __Boston weather__ file contains the following weather-related fields, reported on hourly basis:
   * DATE
   * REPORTTPYE
   * HOURLYDRYBULBTEMPF
   * HOURLYRelativeHumidity
   * HOURLYWindSpeed

2. The __Hubway__ data is organized into files by year and month. For example, the file named `201501-hubway-tripdata.zip` contains a .csv file containing data for January 2015. The data contains the following fields, each row representing a bike trip:

   * Trip Duration (in seconds)
   * Start Time and Date
   * Stop Time and Date
   * Start Station Name & ID
   * End Station Name & ID
   * Bike ID
   * User Type (Casual = 24-Hour or 72-Hour Pass user; Member = Annual or Monthly Member)
   * ZIP Code (if user is a member)
   * Gender (self-reported by member)

