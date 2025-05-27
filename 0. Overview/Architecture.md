[Back to README](../README.md) | Previous: [0. Overview.md](0. Overview.md) | Next: [DataSharing.md](DataSharing.md)

# Architecture #

Snowflake's architecture is a hybrid of traditional shared-disk and shared-nothing database architectures.
* Similar to shared-disk architectures:
  * Snowflake uses a central data repository for persisted data accessible from all compute nodes in the platform
  * Offers data management simplicity
* Similar to shared-nothing architectures (e.g. Hadoop, Spark)
  * Snowflake processes queries using virtual warehouses where each node in the cluster stores a portion of the entire data set locally
  * Offers performance and scale-out benefits

Advantages:
* Storage, compute and management services are decoupled and can scale independently
* There is virtually no limit on how much each layer can be scaled
* Workload isolation with virtual warehouses

## Snowflake Layers ##
Snowflake's unique architecture consists of three layers, all of them with High Availability. The price is also charged separately for each layer.

> In addition to the three layers mentioned, there is the Cloud Agnostic Layer - allows Snowflake to run on the major cloud providers: AWS, Azure, GCP and ensures Snowflake performs comparaby across providers.

![](../images/SnowflakeLayers.png)

### Storage Layer ###
* single copy and source of truth for the data
* virtually infinitely scalable
* inherits the cloud provider's availability and durability guarantees
  * e.g. AWS S3 replicates data across three different availability zones within a region
* data is stored in Snowflake's read-optimized proprietary compressed columnar format
  * due to columns containing similar data, the columnar format results in better compression
  * data is stored compressed
  * data is stored using AES-256 encryption
* Snowflake manages all aspects of how this data is stored.

### Compute (Query Processing) Layer ###
* provides the necessary compute resources to execute queries
* uses Virtual Warehouses
  * independent compute clusters
  * can be scaled up or down at any time
  * can be automatically scaled up or down
  * multiple Virtual Warehouses can access the same data without contention
  * Virtual Warehouses do not share compute resources
  * Virtual Warehouses do not share disk space
  * Virtual Warehouses are billed based on usage (per second)
* queries are processed in this layer
* query results are cached in this layer

### Cloud Services Layer ###
* collection of services that coordinate activities across Snowflake
* runs on Snowflake-managed compute
* responsible for:
  * Authentication
  * Access Control
  * Data Management
    * Metadata management
    * Query optimization
    * Transaction management
    * Security
  * Infrastructure Management
    * Virtual Warehouse management
    * Data storage management
    * Billing and usage monitoring
* processes queries that can be resolved from metadata without accessing the compute or storage layers
  * e.g. `SELECT COUNT(*) FROM table_name;`
  * Get statistics, e.g.: `MIN` and `MAX` of a column, `COUNT`, number of `NULL`s
  * DDL retrieval
* Metadata and Statistics collected and kept up-to-date
* Time Travel and Cloning
* Availability
* Transparent online updates and patches
* Runs on Snowflake-managed compute


[Back to README](../README.md) | Previous: [0. Overview.md](0. Overview.md) | Next: [DataSharing.md](DataSharing.md)
