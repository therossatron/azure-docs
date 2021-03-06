---
title: Create Apache Hadoop clusters using a web browser - Azure HDInsight 
description: Learn how to create Apache Hadoop, Apache HBase, Apache Storm, or Apache Spark clusters on Linux for HDInsight using a web browser and the Azure preview portal.
services: hdinsight
author: hrasheed-msft
ms.reviewer: jasonh

ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 12/28/2018
ms.author: hrasheed

---
# Create Linux-based clusters in HDInsight using the Azure portal
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

The Azure portal is a web-based management tool for services and resources hosted in the Microsoft Azure cloud. In this article, you learn how to create Linux-based HDInsight clusters using the portal.

## Prerequisites
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **A modern web browser**. The Azure  portal uses HTML5 and Javascript, and may not function correctly in older web browsers.

## Create clusters
The Azure portal exposes most of the cluster properties. Using Azure Resource Manager templates, you can hide many details. For more information, see [Create Linux-based Apache Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Log in to the [Azure  portal](https://portal.azure.com).

1. From the left menu, select **+ Create a resource**.

1.  Under **Azure Marketplace**, select **Analytics**.

1.  Under **Featured**, select **HDInsight**.
   
    ![Creating a new cluster in the Azure portal](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster.png "Creating a new cluster in the Azure portal")

1. From the **HDInsight** page, select **Custom (size, settings, apps)**.

1. Select **1 Basics**, and then enter the following information:

	![Creating a new cluster in the Azure portal](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster-basics.png "Creating a new cluster in the Azure portal")

	* Enter **Cluster Name**: This name must be globally unique.

	* From the **Subscription** drop-down, select the Azure subscription that is used for the cluster.

	* Select **Cluster type**, and then select the type of cluster (Hadoop, Spark, etc.) you want to create. The **Operating system** will be **Linux**. Then select a cluster type version. Use the default version if you don't know what to choose. For more information, see [HDInsight cluster versions](hdinsight-component-versioning.md).
     
    	> [!IMPORTANT]  
    	> HDInsight clusters come in a variety of types, which correspond to the workload or technology that the cluster is tuned for. There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.
		
    * For **Cluster login username** and **Cluster login password**, provide the username and password for the admin user.

    * Enter an **SSH Username** and if you want to have the SSH password same as the admin password you specified earlier, select the **Use same password as cluster login** check box. If not, provide either a **PASSWORD** or **PUBLIC KEY**, which will be used to authenticate the SSH user. Using a public key is the recommended approach. Click **Select** at the bottom to save the credentials configuration.
   
	    For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    * For **Resource group**, specify whether you want to create a new resource group or use an existing one.

    * Specify a data center **location** where the cluster is created.

    * Select **Next** to move to the next page.

4. From **2 Security + networking**, you can connect your cluster to a virtual network using the provided dropdown. Select an Azure virtual network and the subnet if you want to place the cluster into a virtual network. For information on using HDInsight with a Virtual Network, including specific configuration requirements for the Virtual Network, see [Extend HDInsight capabilities by using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md). If you want to use the **Enterprise Security Package**, you can also follow instructions here: [Configure a HDInsight cluster with Enterprise Security Package by using Azure Active Directory Domain Services](https://docs.microsoft.com/azure/hdinsight/domain-joined/apache-domain-joined-configure-using-azure-adds).

    Select **Next** to move to the next page.


5. From **3 Storage**, specify whether you want Azure Storage (WASB) or Data Lake Storage as your default storage. Look at the table below for more information.

	 ![Creating a new cluster in the Azure portal](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster-storage.png "Creating a new cluster in the Azure portal")

	 | Storage                                      | Description |
	 |----------------------------------------------|-------------|
	 | **Azure Storage Blobs as default storage**   | <ul><li>For **Primary Storage type**, select **Azure Storage**. After that, for **Selection method**, you can choose **My subscriptions** if you want to specify a storage account that is part of your Azure subscription and then select the storage account. Otherwise, click **Access key** and provide the information for the storage account that you want to choose from outside your Azure subscription.</li><li>For **Default container**, you can choose to go with the default container name suggested by the portal or specify your own.</li><li>If you are using WASB as default storage, you can (optionally) click **Additional Storage Accounts** to specify additional storage accounts to associate with the cluster. For **Azure Storage Keys**, click **Add a storage key**, and then you can provide a storage account from your Azure subscriptions or from other subscriptions (by providing the storage account access key).</li><li>If you are using WASB as default storage, you can (optionally) click **Data Lake Storage access** to specify Azure Data Lake Storage as additional storage. For more information, see [Quickstart: Set up clusters in HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</li></ul> |
	 | **Azure Data Lake Storage as default storage** | For **Primary storage type**, select **Azure Data Lake Storage Gen1** or **Azure Data Lake Storage Gen2** and then refer to the article [Quickstart: Set up clusters in HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md) for instructions. |
	 | **External metastores**                      | Optionally, you can specify a SQL database to save Hive and Oozie metadata associated with the cluster. For **Select a SQL database for Hive** select a SQL database, and then provide the username/password for the database. Repeat these steps for Oozie metadata.<br><br>Some considerations while using Azure SQL database for metastores. <ul><li>The Azure SQL database used for the metastore must allow connectivity to other Azure services, including Azure HDInsight. On the Azure SQL database dashboard, on the right side, click the server name. This is the server on which the SQL database instance is running. Once you are on the server view, click **Configure**, and then for **Azure Services**, click **Yes**, and then click **Save**.</li><li>When creating a metastore, do not use a database name that contains dashes or hyphens, as this can cause the cluster creation process to fail.</li></ul> |

	 > [!WARNING]  
	 > Using an additional storage account in a different location than the HDInsight cluster is not supported.

	 Select **Next** to move to the next page.


6. From **4 Applications (optional)**, select any desired applications.  These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself. For more information, see [Install HDInsight applications](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).

    Select **Next** to move to the next page.


6. **5 Cluster size** displays information about the nodes that are used for this cluster. Set the number of worker nodes that you need for the cluster. The estimated cost of running the cluster is also shown.
   
    ![Node pricing tiers](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster-nodes.png "Specify number of cluster nodes")
   
   > [!IMPORTANT]  
   > If you plan on more than 32 worker nodes, either at cluster creation or by scaling the cluster after creation, then you must select a head node size with at least 8 cores and 14 GB RAM.
   > 
   > For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).
   
    Select **Next** to move to the next page.

8. From **6 Script actions**, you can customize a cluster to install custom components.  Use this option if you want to use a custom script to customize a cluster, as the cluster is being created. For more information about script actions, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).

   Select **Next** to move to the next page.

9. From **7 Summary**, verify the information you entered earlier and then select **Create**.

	 ![Node pricing tiers](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster-summary.png "Specify number of cluster nodes")
    
    > [!NOTE]  
    > It takes some time for the cluster to be created, usually around 20 minutes. Monitor **Notifications** to check on the provisioning process.

10. Once the creation process completes, select **Go to Resource** from the **Deployment succeeded** notification. The cluster window provides the following information.
    
    ![Cluster interface](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster-completed.png "Cluster properties")
    
    Use the following to understand the icons at the top.
    
    * **Overview** tab provides all the essential information about the cluster such as the name, the resource group it belongs to, the location, the operating system, URL for the cluster dashboard, etc.
    * **Dashboard** directs you to the Ambari portal associated with the cluster.
    * **Secure Shell**: Information needed to access the cluster using SSH.
    * **Scale cluster** lets you increase the number of worker nodes associated with the cluster.
	  * **Delete**: Deletes the HDInsight cluster.
    

## Customize clusters
* See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).
* See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).

## Delete the cluster
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## Troubleshoot

If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-hadoop-create-linux-clusters-portal.md).

## Next steps
Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster:

### Apache Hadoop clusters
* [Use Apache Hive with HDInsight](hadoop/hdinsight-use-hive.md)
* [UseApache Pig with HDInsight](hadoop/hdinsight-use-pig.md)
* [Use MapReduce with HDInsight](hadoop/hdinsight-use-mapreduce.md)

### Apache HBase clusters
* [Get started with Apache HBase on HDInsight](hbase/apache-hbase-tutorial-get-started-linux.md)
* [Develop Java applications for Apache HBase on HDInsight](hbase/apache-hbase-build-java-maven-linux.md)

### Apache Storm clusters
* [Develop Java topologies for Apache Storm on HDInsight](storm/apache-storm-develop-java-topology.md)
* [Use Python components in Apache Storm on HDInsight](storm/apache-storm-develop-python-topology.md)
* [Deploy and monitor topologies with Apache Storm on HDInsight](storm/apache-storm-deploy-monitor-topology-linux.md)

### Apache Spark clusters
* [Create a standalone application using Scala](spark/apache-spark-create-standalone-application.md)
* [Run jobs remotely on an Apache Spark cluster using Apache Livy](spark/apache-spark-livy-rest-interface.md)
* [Apache Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools](spark/apache-spark-use-bi-tools.md)
* [Apache Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results](spark/apache-spark-machine-learning-mllib-ipython.md)

