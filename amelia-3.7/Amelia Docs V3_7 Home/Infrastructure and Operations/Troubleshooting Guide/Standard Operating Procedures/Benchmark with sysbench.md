-   [CPU](#Benchmarkwithsysbench-CPU)
-   [File IO](#Benchmarkwithsysbench-FileIO)
-   [MySQL](#Benchmarkwithsysbench-MySQL)
-   [Socket Test](#Benchmarkwithsysbench-SocketTest)
-   [HAproxy test](#Benchmarkwithsysbench-HAproxytest)
Amelia includes [sysbench](https://github.com/akopytov/sysbench) to benchmark technical performance.
# CPU
To benchmark CPU performance, run this command:
``` groovy
sysbench cpu --cpu-max-prime=20000 --threads=32 run
```
This command will generate output similar to this example:
``` groovy
sysbench 1.0.14 (using bundled LuaJIT 2.1.0-beta2)
Running the test with following options:
Number of threads: 32
Initializing random number generator from current time
Prime numbers limit: 20000
Initializing worker threads...
Threads started!
CPU speed:
events per second: 1384.59
General statistics:
total time: 10.0159s
total number of events: 13870
Latency (ms):
min: 2.76
avg: 22.81
max: 342.86
95th percentile: 97.55
sum: 316316.95
Threads fairness:
events (avg/stddev): 433.4375/14.77
execution time (avg/stddev): 9.8849/0.09
```
# File IO
To benchmark file I/O performance, run this command, ideally making this bigger than available memory:
``` groovy
cd /apps
sysbench fileio --file-total-size=15G prepare
sysbench fileio --file-total-size=15G --file-test-mode=rndrw --max-time=60 --max-requests=0 run
sysbench fileio --file-total-size=15G cleanup
```
This command will generate output similar to this example:
``` groovy
sysbench 1.0.14 (using bundled LuaJIT 2.1.0-beta2)
Running the test with following options:
Number of threads: 1
Initializing random number generator from current time
Extra file open flags: (none)
128 files, 120MiB each
15GiB total file size
Block size 16KiB
Number of IO requests: 0
Read/Write ratio for combined random IO test: 1.50
Periodic FSYNC enabled, calling fsync() each 100 requests.
Calling fsync() at the end of test, Enabled.
Using synchronous I/O mode
Doing random r/w test
Initializing worker threads...
Threads started!
File operations:
reads/s: 187.37
writes/s: 124.91
fsyncs/s: 398.91
Throughput:
read, MiB/s: 2.93
written, MiB/s: 1.95
General statistics:
total time: 60.0014s
total number of events: 42674
Latency (ms):
min: 0.00
avg: 1.40
max: 361.84
95th percentile: 7.70
sum: 59945.98
Threads fairness:
events (avg/stddev): 42674.0000/0.00
execution time (avg/stddev): 59.9460/0.00
```
# MySQL
To benchmark MySQL performance, run this command:
``` groovy
mysqladmin -S /apps/IPsoft/amelia/amelia-kdb-master/mysql.sock create sbtest
sysbench /usr/share/sysbench/oltp_insert.lua --db-driver=mysql --mysql-socket=/apps/IPsoft/amelia/amelia-kdb-master/mysql.sock --mysql-user=root --mysql-password=4296s639869876cssa6i --time=60 --max-requests=0 --threads=8 prepare
```
# Socket Test
To benchmark socket performance, run this command:
``` groovy
sysbench /usr/share/sysbench/oltp_insert.lua --db-driver=mysql --mysql-socket=/apps/IPsoft/amelia/amelia-kdb-master/mysql.sock --mysql-user=root --mysql-password=4296s639869876cssa6i --time=60 --max-requests=0 --threads=8 --report-interval=1 run
```
# HAproxy test
To benchmark HAproxy performance, run this command:
``` groovy
sysbench /usr/share/sysbench/oltp_insert.lua --db-driver=mysql --mysql-host=127.0.0.1 --mysql-port=13306 --mysql-user=root --mysql-password=4296s639869876cssa6i --time=60 --max-requests=0 --threads=8 --report-interval=1 run
mysql -S /apps/IPsoft/amelia/amelia-kdb-master/mysql.sock -e "DROP DATABASE IF EXISTS sbtest"
```
