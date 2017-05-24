## Programming Club Server Performance Report 

#  Sunil Kumar AND TEAM

     15th May 2017
     
 ### Table of Contents
 
 1. Introduction	1
 
 2. Experiment	1
 
 2.1. Experimental Procedure	1
 
 2.2. Results	2
 
 3. Conclusions	4
 
# References	4

 1. Introduction
 
An experiment was conducted to test the performance of the server for three different test cases, 
SingleRequest: Requests are made to a single webpage.
EqualNumber: Equal number of requests are made to all the apps.
BiasedRequest: High variance in number of request within apps.
 2. Experiment
 
An experiment was conducted to measure the performance of the Programming Club server.  The  server was set up on a machine 'A'. Then from other machines requests were made to the applications hosted on the server. Depending on the number of requests sent and the distribution of the requests amongst the applications we have classified them into three types as said above.
 2.1. Experimental Procedure
 
Setup Jmeter on 3 machines and pull the required script of testing from GitHub. 
SingleRequest : From the three machines send HTTP requests to a particular webpage.
EqualNumber : From each of the three machines send equal number of HTTP request to different webpages.
BiasedRequest : From three different machines send HTTP request which vary greatly in number to different applications. We sent 800 requests from machine B, 500 from machine C and 200 from machine D.
Jmeter(Ref. [1] ) is used to send HTTP requests to applications from different machines. We also analyze the number of 200 and 503 responses using Jmeter

  Compensation for Sources of Errors
  
Nginx was configured in such a way that it checks and distributes the requests depending on the distribution of previous requests and usage of resources.
Jmeter works on Java and JVM can run only a limited number of threads with a low default heap size. Due to this limitation,  we were not able to check the actual requests limit on the server. To allow more number of threads, we increased the heap size in the Jmeter script, but were still limited by number of threads.
Since it was difficult to check the performance of server at the actual requests limit, we changed our nginx.conf file to limit requests to 3000requests/sec.

  Machines Used
  
Machine A: server machine

RAM: 16GB

CPU:  Intel(R) Core(TM) i7-6700 CPU @ 3.40GHz

Operating System: Linux, Ubuntu 16.04

Machine B: where Jmeter is installed

RAM: 16GB

CPU: Intel(R) Core(TM) i7-4710HQ CPU @ 2.50GHz

Operating System: Linux, Ubuntu 16.04

Machine C: where Jmeter is installed:

RAM: 8GB

CPU:  Intel(R) Core(TM) i7-4710Q CPU @ 2.20GHz

Operating System: Linux, Ubuntu 16.04

Machine D: where Jmeter is installed:

RAM: 8GB

CPU: Intel(R) Core(TM) i7-4710Q CPU @ 2.20GHz

Operating System: Linux, Ubuntu 16.04

 2.2. Results
 
SingleRequest:

LIMIT =1000r/s	BURST = 0	WITHOUT LOAD BALANCING

Machine

No of Requests

Error Percentage

Throughput

Machine B

1000

66.7

170.0/sec

Machine C

1000

41.40

168.2/sec

Machine D

1000

72.20

294.6/sec

LIMIT =1000r/s	BURST =20	WITHOUT LOAD BALANCING
Machine

No of Requests

Error Percentage

Throughput

Machine B

1000

15.7

73.7/sec

Machine C

1000

1.90

165.9/sec

Machine D

1000

6.70

279.9/sec

INITIAL LIMIT =1000r/s	BURST =20	WITH LOAD BALANCING

Machine

No of Requests

Error Percentage

Throughput

Machine B

1000 users 20 times

8.04

290.8/sec

Machine C

1000 users 20 times

32.58

505.4/sec

Machine D

1000 users 20 times

28.70

429.9/sec


EqualNumber:

LIMIT =1000r/s	BURST = 20	WITHOUT LOAD BALANCING

Machine & Page

No of Requests

Error Percentage

Throughput

Machine B -> index.php

1000

31.1

67.7/sec

Machine C -> index1.php

1000

3.40

81.5/sec

Machine D -> index2.php

1000

10.80

272.8/sec


INITIAL LIMIT =1000r/s	BURST =20	WITH LOAD BALANCING

Machine

No of Requests

Error Percentage

Throughput

Machine B  -> index.php

1000 users 20 times

8.31

121.0/sec

Machine C  -> index1.php

1000 users 20 times

18.68

149.9/sec

Machine D  -> index2.php

1000 users 20 times

10.37

161.8/sec
	

BiasedRequests:

LIMIT =1000r/s	BURST = 20	WITHOUT LOAD BALANCING

Machine

No of Requests

Error Percentage

Throughput

Machine B -> index.php

800

32

130.0/sec

Machine C -> index1.php


500

0.0

48.7/sec

Machine D -> index2.php

200

39.0

552.0/sec


INITIAL LIMIT =1000r/s	BURST =20	WITH LOAD BALANCING

Machine

No of Requests

Error Percentage

Throughput

Machine B -> index.php

800 users 20 times

31.59

318.8/sec

Machine C -> index1.php

500 users 20 times

43.12

1271.0/sec

Machine D -> index2.php

200 users 20 times

21.15

676.5/sec


 3. Conclusions
 
The load balancing script works very well in responding to requests while allowing high throughput. In general, whenever throughput increases, error % increases as well. The possible future works include developing a better heuristic and algorithm for load balancing, reducing the update interval by using a faster file parser and better logs management. Also, we can experiment by changing the values of burst for each request zone and evaluate its effects on performance.
Here, summarise your work and give some of the important results and conclusions.  You may also have a paragraph on limitations and possible future work.
References

[1] What is Jmeter? , http://jmeter.apache.org/ , accessed on 15/05/17.

[2] Performance Comparisons of Docker, http://domino.research.ibm.com/library/cyberdig.nsf/papers/0929052195DD819C85257D2300681E7B/$File/rc25482.pdf  , accessed on 15/05/17

![img](https://cloud.githubusercontent.com/assets/18292636/26415467/38924d3e-40d0-11e7-8f4f-cb8166f02495.png)
