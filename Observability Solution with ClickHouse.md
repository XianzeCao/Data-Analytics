# Logs

Assume a modern architecture where logs are collected from K8s clusters, but this solutions should apply equally to any other setup.



### Naive/ direct approach 

 

<img src="https://clickhouse.com/uploads/agent_architecture_bd0e3a1af7.png" alt="agent_architecture_bd0e3a1af7" style="zoom:50%;" />

Agents deployed close to the data source, responsible for processing and sending data directly to Clickhosue via HTTP or native protocol 

Potential issue: could cause too many small inserts, if the agents are configured to flush frequently

### Asynchronous approach (on larger deployments, simplified ) :

<img src="https://clickhouse.com/uploads/aggregator_architecture_8485f75130.png" alt="aggregator_architecture_8485f75130" style="zoom:50%;" />

Introduces an aggregator / gateway concept , avoids problem of "too many parts", aligns with clickhosue's best insert practice :

![image-20231118114151004](/Users/zaccao/Library/Application Support/typora-user-images/image-20231118114151004.png)

Agents forward data to the aggregator, the aggregator is responsible for processing steps such as enrichment, filtering, and ensuring a schema is applied, as well as batching and reliable delivery to Clickhosue 

Other aspects to consider: 

Data buffering, load-balancing , high availability, complex routing , separation of record(archive) and analysis systems 

### Open Telemetry (OTEL) 

A collection of tools, APIs, and SDKs for instrumenting, generating, collecting, and exporting Observability data.

Can be used as an aggregator or agent itself 

<img src="/Users/zaccao/Library/Application Support/typora-user-images/image-20231118120638007.png" alt="image-20231118120638007" style="zoom:50%;" />

### Optimizing query performance

Order the column in order of cardinality (e.g. for logs server /pod name first ,then followed by timestamp) limit columns to below 3-4

### Visualization 

Grafana is recommended 









# Traces

Definition: Telemetry is data emitted from a system about its behavior. This data can take the form of logs, metrics, and traces. 

A trace records the paths taken by requests as they propagate through multi-service architectures such as microservice and serverless applications. 

Trace spans:

<img src="https://clickhouse.com/uploads/traces_concept_4908965e1c.png" alt="traces_concept_4908965e1c" style="zoom:50%;" />