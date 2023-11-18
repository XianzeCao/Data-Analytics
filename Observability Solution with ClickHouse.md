# Logs

Assume a modern architecture where logs are collected from K8s clusters, but this solutions should apply equally to any other setup.



### Naive/ direct approach 

 

<img src="https://clickhouse.com/uploads/agent_architecture_bd0e3a1af7.png" alt="agent_architecture_bd0e3a1af7" style="zoom:50%;" />

Agents deployed close to the data source, responsible for processing and sending data directly to Clickhosue via HTTP or native protocol 

Potential issue: could cause too many small inserts, if the agents are configured to flush frequently

### Asynchronous approach (on larger deployments) :

<img src="https://clickhouse.com/uploads/aggregator_architecture_8485f75130.png" alt="aggregator_architecture_8485f75130" style="zoom:50%;" />

Introduces an aggregator / gateway concept , avoids problem of "too many parts"

Agents forward data to the aggregator, the aggregator is responsible for processing steps such as enrichment, filtering, and ensuring a schema is applied, as well as batching and reliable delivery to Clickhosue 