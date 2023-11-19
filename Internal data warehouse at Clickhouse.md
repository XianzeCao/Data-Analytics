Incentive :  understand customer better

Data source : data plane (runs database pods) ,  control plane(customer facing UI & database operations),  AWS/GCP billing 

Architecture:

<img src="https://clickhouse.com/uploads/dwh_architecture_v2_40c61f64f6.png" alt="dwh_architecture_v2_40c61f64f6" style="zoom:50%;" />

### From a high level, the core components 

Clickhouse cloud -- main database 

Airflow -- scheduler 

AWS s3 -- immediate storage for raw data

Superset: internal BI & ah-hoc tool 



### Data source to S3:

Control plane, data plane etc    -- native functionality to export data

GCP billing,  BigQuery export queries -> 

















### Idempotency 

Most tables here use ReplicateReplacingMergeTree engine -- records with the same key will be squashed and only the last record will retain





