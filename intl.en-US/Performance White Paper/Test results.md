# Test results

This topic describes the performance test results of ApsaraDB for MongoDB with different read/write ratios.

## Parameters

-   Count: the sum of recordcount and operationcount.
-   Thread: the total number of threads used for the client test. In this test, four ECS instances of 4 cores and 32 GB are used as the clients for concurrent testing. The thread count is an average.
-   Throughput: the number of read and write operations. Unit: ops/s.
-   RAL: the average latency of read operations. Unit: us.
-   WAL: the average latency of write operations. Unit: us.

## Read/write ratio of 50:50

|Instance type|Count|Thread|Throughput|RAL|WAL|
|-------------|-----|------|----------|---|---|
|General-purpose, 1-core 2 GB|1000000|100|3997|22080|27934|
|General-purpose, 2-core 4 GB|2000000|100|7674|11778|14271|
|General-purpose, 4-core 8 GB|4000000|100|17002|5249|6502|
|General-purpose, 8-core 16 GB|8000000|100|30500|3027|3520|
|General-purpose, 8-core 32 GB|16000000|100|33655|2679|3253|
|General-purpose, 16-core 64 GB|32000000|100|64883|1322|1761|
|Dedicated, 2-core 16 GB|100000000|150|4354|30674|38167|
|Dedicated, 4-core 32 GB|100000000|150|10890|12517|15019|
|Dedicated, 8-core 64 GB|100000000|150|21145|6347|7826|
|Dedicated, 16-core 128 GB|100000000|150|50625|2589|3323|
|Dedicated, 32-core 256 GB|100000000|150|65472|1982|2588|
|Dedicated host, 30-core 220 GB|100000000|150|62472|1955|2770|
|Dedicated host, 60-core 440 GB|100000000|150|90181|1410|1870|

## Read/write ratio of 95:5

|Instance type|Count|Thread|Throughput|RAL|WAL|
|-------------|-----|------|----------|---|---|
|General-purpose, 1-Core 2 GB|1000000|100|7849|12519|16801|
|General-purpose, 2-core 4 GB|2000000|100|14923|6621|8109|
|General-purpose, 4-core 8 GB|4000000|100|37573|2623|3277|
|General-purpose, 8-core 16 GB|8000000|100|51085|1936|2247|
|General-purpose, 8-core 32 GB|16000000|100|70780|1383|1885|
|General-purpose, 16-core 64 GB|32000000|100|105606|920|1371|
|Dedicated, 2-core 16 GB|100000000|150|7175|20701|24635|
|Dedicated, 4-core 32 GB|100000000|150|17270|8634|9529|
|Dedicated, 8-core 64 GB|100000000|150|46707|3167|3920|
|Dedicated, 16-core 128 GB|100000000|150|106386|1372|2013|
|Dedicated, 32-core 256 GB|100000000|150|150378|970|1233|
|Dedicated host, 30-core 220 GB|100000000|150|132717|1100|1405|
|Dedicated host, 60-core 440 GB|100000000|150|225365|643|856|

