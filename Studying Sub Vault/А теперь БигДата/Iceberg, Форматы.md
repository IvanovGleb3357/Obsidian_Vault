## ORC VS Parquet VS AVRO
Avro
- row-oriented
- schema-evolution
- good for writing bad for readin
Parquette
- Column-oriented
- Footer, min, max
- Bloom filter
- Compression (based on values, incremental)
- expensive schema evolution
Orc
- column-oriented
- like parquet but not that compressedable



iceberg - не взаимозаменяет hive

orc / parquett



dwh - elt
datalake - etl

yarn - res manager vs node manager
broh

hash join
skew join
rdd 


spark minus
select 1

chunks batch - почитать в pandas
parquet vs orc


@task
@python operator
@pg operator, sql operator
@bash operator
@s3 operator

kafka 3 - отказоустойчивость
- acknowledgement
- column
да mpp clickhouse

топик в кафке - 6 партиций
кол-во партиций = кол-во хостов


CI/CD - создать dag
конфликты через среду разработки
create table if not 

процент заполнение, уникальность, дубли, каунт
ссылочная целостность
полнота, уникальность, консистентность

json
lineage - граф






