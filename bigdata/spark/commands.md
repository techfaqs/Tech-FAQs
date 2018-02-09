# Spark Commands


### Spark Submit run command (to run a script on spark):

    spark-submit  - Mandatory to launch a Spark job to run script/code
    --class       - The entry point for your application (e.g. org.apache.spark.examples.SparkPi)
    --master      - The master URL for the cluster (e.g. spark://23.195.26.187:7077)
    --deploy-mode - Whether to deploy your driver on the worker nodes (cluster) or locally as an external client (client) (default: client) †
    --conf        - Arbitrary Spark configuration property in key=value format. For values that contain spaces wrap “key=value” in quotes (as shown).
    <application-jar>        - Path to a bundled jar including your application and all dependencies. The URL must be globally visible inside of your cluster, for instance, an hdfs:// path or a file:// path that is present on all nodes.
    [application-arguments]  - Arguments passed to the main method of your main class, if any

The master URL passed to Spark can be in one of the following formats:

|Master URL | Meaning |
|-----------|---------|
| local | Run Spark locally with one worker thread (i.e. no parallelism at all). |
| local[K] | Run Spark locally with K worker threads (ideally, set this to the number of cores on your machine). |
| local[K,F] | Run Spark locally with K worker threads and F maxFailures (see spark.task.maxFailures for an explanation of this variable) |
| local[*] | Run Spark locally with as many worker threads as logical cores on your machine. |
| local[*,F] | Run Spark locally with as many worker threads as logical cores on your machine and F maxFailures. |
| spark://HOST:PORT | Connect to the given Spark standalone cluster master. * |
| spark://HOST1:PORT1,HOST2:PORT2 | Connect to the given Spark standalone cluster with standby masters with Zookeeper.<br>The list must have all the master hosts in the high availability cluster set up with Zookeeper.*|
| mesos://HOST:PORT | Connect to the given Mesos cluster. The port is 5050 by default.<br> Or, for a Mesos cluster using ZooKeeper, use `mesos://zk://....`<br> To submit with `--deploy-mode cluster`, the `HOST:PORT` should be configured to connect to the `MesosClusterDispatcher`. |
| yarn | Connect to a YARN cluster in client or cluster mode depending on the value of `--deploy-mode`. The cluster location will be found based on the HADOOP_CONF_DIR or YARN_CONF_DIR variable.|

_**&ast;(The port must be whichever each master is configured to use, which is 7077 by default.)**_

### Spark SQL run command:

    spark-sql          – Mandatory to launch the Spark SQL shell
    –master            – Mandatory to execute the Spark Sql or Hive Queries in local, yarn mode
    –executor-memory   – Amount of Memory Required for a Container (Optional)
    –executor-cores    – Amount of Cores to be utilized for a Container(Optional)
    –queue             – Resource Manager Queue where job needs to be submitted(Optional)
    –conf              – Additional Configuration Parameters like for Yarn, Memory Settings,etc(Optional)
    –hiveconf          – Helps to execute Parameterized Hive Queries(Optional)
    
    
    Reference:
    
    [Spark Submit](https://spark.apache.org/docs/latest/submitting-applications.html)
