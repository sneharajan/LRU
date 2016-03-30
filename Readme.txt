                                                                           PROJECT 3 : README FILE
NAME : Sneha Rajan
UID:U95134515


The Zip folder consists of the source files of Buffermanager in PostgreSQL 8.2.19. These are modified to implement the LEAST RECENTLY USED(LRU) algorithm instead of clock algorithm in Postgres.

The List of source files changed to implement the LRU are as follows
1)freelist.c
2)localbuf.c
3)bufmgr.c

CLOCK SWEEP ALGORITHM
-> The variables used are 
1)usage_count
2)refcount

LEAST RECENTLY USED ALGORITHM
Variables
refcount - Similar to pincount
usage_count is not used.

IMPLEMENTATION
-> In clock algorithm, the page with refcount equal to zero and usage_count equal to zero will be considered as free to use for replacement.
-> LRU uses the refcount. 
-> Least Recently Used algorithm does not need usage_count, since it uses refcount which works same as pin_count.
-> When a page is accessed, we have to move the page out of the freelist and add it  to the tail  of the queue in freelist
-> LRU Algorthim ,the pages which has the zero value for refcount and this page will be considered for replacement.
-> If the refcount value is equal to zero for a page, then that page is included in the freelist and depending on which page was used least recently, that page will be selected for the replacement from the freelist.

-> The two function responsible for implementing this algorithm are

1)StrategyGetBuffer- returns appropriate page for replacement based on refcount
1) StrategyFreeBuffer - Adds page to freelist.

Process is tested using the log file and using the number of buffers to be  200

/usr/local/pgsql/bin/initdb -B 200 -D /usr/local/pgsql/data &

the applcation is tested using the input.sql 

The logfile is attached.



