# Trino with Iceberg

Start Docker containers with
```shell
docker-compose up -d
```

Enter Trino shell
```shell
docker exec -it trino trino
```

Example SQL query

```sql
CREATE SCHEMA iceberg.test WITH (location = 'file:///var/trinodata/test');

CREATE TABLE iceberg.test.campaigns
WITH (
  format = 'PARQUET'
)
AS
SELECT * FROM (
    VALUES 
    ('adcampaign_11', ARRAY[100, 200, 150, 50] ,200),
    ('adcampaign_12', NULL ,50),
    ('adcampaign_13', ARRAY[100, NULL, 250, NULL] ,200),
    ('adcampaign_14', ARRAY[NULL, NULL, NULL, NULL] ,200)
) AS t(campaign_name, daily_adspend, daily_budget);


SELECT * FROM iceberg.test.campaigns;
```

Catalog is created with properties [iceberg.properties](./iceberg.properties).  
