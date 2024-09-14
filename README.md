# data-pipelines
## Introduction
![Data Pipeline](https://i.imgur.com/inIcMc3.png)

* The data pipelines extract raw data from several sources (mostly APIs, one gsheet). The extract and load steps are implemented via python scripts. GCS Buckets or S3 Buckets are used in between the extract and load steps. The raw data are loaded into BigQuery. Data transformation is handled by dbt. The whole ETL process is orchestrated via Airflow, and all of these are running inside a GCP VM. Finally, Looker is used for data visualization.
* The python scripts, dbt, and Airflow are all under different git repos for modularity. Orchestrator can be easily replaced, etc. The following git repos are currently used:
    * [Airflow](https://github.com/kevinesg/airflow)
    * [dbt](https://github.com/kevinesg/dbt)
    * [scripts](https://github.com/kevinesg/scripts)
* Airflow and dbt are both free, which means the only cost in this data pipeline setup is mostly for the GCP VM (which can be removed by simply using a local VM). BigQuery cost can be removed by using a local data warehouse. The storage buckets have minimal costs since they're simply used to store the incremental raw data extracted (and deleted during the load step). Cloud services are used for VM and data warehouse in this project just for zero downtime.
* The Airflow Webserver is deployed to [airflow.kevinesg.com](https://airflow.kevinesg.com) with the following log-in credentials (this user only has read access to everything):
    ````
    username: viewer
    password: airflow
    ````
* conda is the package manager used here to separate environments, but of course other python virtual managers are perfectly fine too.

## Roadmap
    - [ ] create streaming / event-driven data pipelines
        * kafka
        * debezium
        * pyspark
    - [x] deploy Airflow localhost web UI to a website
        * nginx
        * cloudflare
        * domain provider (squarespace)
    - [ ] expose processed data via APIs
    - [ ] refactor existing extract-load scripts into modular and reusable custom functions
    - [ ] use github actions for automatic git pull (instead of relying on airflow tasks)
    - [ ] explore other cloud data warehouses / platforms
        * snowflake
        * databricks
        * redshift
    - [ ] explore other orchestrators
        * dagster
        * prefect
        * mage.ai
    - [ ] explore other data viz tools
##
Let me know if you have any questions! You can contact me at kevinlloydesguerra@gmail.com.