# Lab 3

## Student information

* Full name: Owen Sugiarto
* E-mail:osugi001@ucr.edu
* UCR NetID: osugi001
* Student ID: 862296300

## Answers

* (Q1) Verify the file size and report the running time.
![Untitled-document-Google-Docs](https://github.com/osugi001/CS152/assets/102548267/9793983d-4d6d-4a32-a55d-bfc70e147890)


* (Q2) Report the running time of the copy command.
* Since I'm using Windows cmd, I need a workaround method, here it is calculated to be around 12 seconds but because I was typing as well, -6 seconds it is supposed to be around 5-6 seconds.
 ![1](https://github.com/osugi001/CS152/assets/102548267/53a9be79-045e-4e8f-b1ff-8b11d9fccfef)


* (Q3) How do the two numbers compare? (The running times of copying the file through your program and the operating system.) Explain IN YOUR OWN WORDS why you see these results.
*  the windows copy command is faster, I think it is because command line tools in general have more direct access, have less overhead and are optimized for specific tasks.


* (Q4) Does the program run after you change the default file system to HDFS? What is the error message, if any, that you get?
* In this part, I used 3 terminal, GIT, VSC, and windows terminal, one to run hdfs namenode -format, & hdfs namenode
* The other one to run hdfs datanode, and lastly to run hdfs dfsadmin -report

![Untitled-document-Google-Docs (1)](https://github.com/osugi001/CS152/assets/102548267/d3585624-a871-4d08-83c1-ad367d3e6259)
![Untitled-document-Google-Docs (2)](https://github.com/osugi001/CS152/assets/102548267/42718e03-6d4b-47aa-8201-8b9961a24e4d)
![Untitled-document-Google-Docs (3)](https://github.com/osugi001/CS152/assets/102548267/940f9100-3468-4a39-a9a2-a9a2d37812f0)



* (Q5) Use your program to test the following cases and record the running time for each case.
* Q5.)Configured Capacity: 207929917440 (193.65 GB)
Present Capacity: 200774180864 (186.99 GB)
DFS Remaining: 200774156288 (186.99 GB)
DFS Used: 24576 (24 KB)
DFS Used%: 0.00%
Replicated Blocks:
        Under replicated blocks: 0
        Blocks with corrupt replicas: 0
        Missing blocks: 0
        Missing blocks (with replication factor 1): 0
        Low redundancy blocks with highest priority to recover: 0
        Pending deletion blocks: 0
Erasure Coded Block Groups:
        Low redundancy block groups: 0
        Block groups with corrupt internal blocks: 0
        Missing block groups: 0
        Low redundancy blocks with highest priority to recover: 0
        Pending deletion blocks: 0

-------------------------------------------------
Live datanodes (1):

Name: 169.235.28.225:9866 (class-225.cs.ucr.edu)
Hostname: class-225.cs.ucr.edu


* (Q6) 
 ![Untitled-document-Google-Docs (4)](https://github.com/osugi001/CS152/assets/102548267/397a118e-7e2f-46ec-a083-fd5293bf6220)


* (Q7) the program runs
  ![Untitled-document-Google-Docs (5)](https://github.com/osugi001/CS152/assets/102548267/f26816f1-c48c-434c-b3ff-050873d69b02)

*(Q8)
*local to hdfs
Copied 2271210910 bytes from file:///c/Users/owens/cs167/workspace/osugi001_lab3/AREAWATER_osugi001.csv to hdfs:///user/osugi001/output.csv in 9.6415128 seconds
*hdfs to local
Copied 2271210910 bytes from hdfs:///user/osugi001/output.csv to file:///c/Users/owens/cs167/workspace/osugi001_lab3/AREAWATER_osugi001.csv in 10.2341245 seconds
*hdfs to hdfs
Copied 2271210910 bytes from hdfs:///user/osugi001/output.csv to hdfs:///user/osugi001/output2.csv in 10.2341249 seconds 
*(Q9) the run time compared to Q8 is a bit longer but not that different the average runtime is around 13 seconds.


