# National Dashboard API Performance Testing Specs and Benchmark

Since we have around 600 wards in Punjab, we decided to make the national dashboard service be robust enough to handle 600 requests simultaneously in a very short time( preferably midnight when the employees ingest that day’s data ).

\
The national dashboard service ingest API was made to undergo a very extensive stress testing where the service was tested for 25 concurrent threads( users ) targeting 100 requests per minute with each request payload containing 30 records (as the ingest API is a bulk API). The service passed all the tests with 0 percent error with a throughput of 21 requests per second with a total number of samples being 12671 in 10 minutes which roughly equals 21 requests per second.

&#x20;

The stress test ran with the following configuration and reliably persisted each and every record that was ingested -&#x20;

&#x20;

1.  National-dashboard-ingest service -&#x20;

    1. Number of pods- 5
    2. Number of threads for each pod- 25
    3. Heap memory- 750 mb
    4. Producer linger time- 1 ms


2. National dashboard kafka pipeline service -
   1. Number of pods- 3
   2. Number of threads for each pod- 10
   3. Heap memory- 512 mb
   4. Producer linger time- 1 ms

&#x20;

&#x20;
