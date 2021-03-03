# Test results

This topic describes the performance test results of ApsaraDB for MongoDB instances at different read/write ratios.

## Metrics

-   Count: the sum of the recordcount value and the operationcount value. The recordcount parameter indicates the number of existing records. The operationcount parameter indicates the number of the operations to be executed.
-   Threads: the number of threads that are used for the client test.

    **Note:** Four Elastic Compute Service \(ECS\) instances of 4 cores and 32 GB memory are used to evenly distribute threads for client concurrent testing.

-   Throughput: the number of read and write operations. Unit: ops/s.
-   RAL: the average latency of read operations. Unit: us.
-   WAL: the average latency of write operations. Unit: us.

## Test results at 50:50 read/write ratio

|Instance type|Count|Thread|Throughput|RAL|WAL|
|-------------|-----|------|----------|---|---|
|General-purpose, 1 core and 2 GB memory|1,000,000|100|3,997|22,080|27,934|
|General-purpose, 2 cores and 4 GB memory|2,000,000|100|7,674|11,778|14,271|
|General-purpose, 4 cores and 8 GB memory|4,000,000|100|17,002|5,249|6,502|
|General-purpose, 8 cores and 16 GB memory|8,000,000|100|30,500|3,027|3,520|
|General-purpose, 8 cores and 32 GB memory|16,000,000|100|33,655|2,679|3,253|
|General-purpose, 16 cores and 64 GB memory|32,000,000|100|64,883|1,322|1,761|
|Dedicated, 2 cores and 16 GB memory|100,000,000|150|4,354|30,674|38,167|
|Dedicated, 4 cores and 32 GB memory|100000000|150|10,890|12,517|15,019|
|Dedicated, 8 cores and 64 GB memory|100,000,000|150|21,145|6,347|7,826|
|Dedicated, 16 cores and 128 GB memory|100,000,000|150|50,625|2,589|3,323|
|Dedicated, 32 cores and 256 GB memory|100,000,000|150|65,472|1,982|2,588|
|Dedicated host, 30 cores and 220 GB memory|100,000,000|150|62,472|1,955|2,770|
|Dedicated host, 60 cores and 440 GB memory|100,000,000|150|90,181|1,410|1,870|

## Test results at 95:5 read/write ratio

|Instance type|Count|Thread|Throughput|RAL|WAL|
|-------------|-----|------|----------|---|---|
|General-purpose, 1 core and 2 GB memory|1,000,000|100|7,849|12,519|16,801|
|General-purpose, 2 cores and 4 GB memory|2,000,000|100|14,923|6,621|8,109|
|General-purpose, 4 cores and 8 GB memory|4,000,000|100|37,573|2,623|3,277|
|General-purpose, 8 cores and 16 GB memory|8,000,000|100|51,085|1,936|2,247|
|General-purpose, 8 cores and 32 GB memory|16,000,000|100|70,780|1,383|1,885|
|General-purpose, 16 cores and 64 GB memory|32,000,000|100|105,606|920|1,371|
|Dedicated, 2 cores and 16 GB memory|100,000,000|150|7,175|20,701|24,635|
|Dedicated, 4 cores and 32 GB memory|100,000,000|150|17,270|8,634|9,529|
|Dedicated, 8 cores and 64 GB memory|100,000,000|150|46,707|3,167|3,920|
|Dedicated, 16 cores and 128 GB memory|100,000,000|150|106,386|1,372|2,013|
|Dedicated, 32 cores and 256 GB memory|100,000,000|150|150,378|970|1,233|
|Dedicated host, 30 cores and 220 GB memory|100,000,000|150|132,717|1,100|1,405|
|Dedicated host, 60 cores and 440 GB memory|100,000,000|150|225,365|643|856|

