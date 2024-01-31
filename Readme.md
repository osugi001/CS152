# Lab 4

## Student information

* Full name: Owen Sugiarto
* E-mail: osugi001@ucr.edu
* UCR NetID: osugi001
* Student ID: 8632296300

## Answers

* (Q1) What do you think the line `job.setJarByClass(Filter.class);` does?
* This line tells Hadoop which jar file contains the classes needed for the MapReduce job.

* (Q2) What is the effect of the line `job.setNumReduceTasks(0);`?
* This sets the number of reduce tasks to zero,

* (Q3) Where does the `main` function run? (Driver node, Master node, or an executor node).
* The main function runs on the Driver node, also known as the Master node. It's responsible for setting up the job configuration and submitting the job. The actual data processing (map and reduce tasks) occurs on executor nodes within the cluster.

* (Q4) How many lines do you see in the output?
* 27972 Lines.
 ![Untitled-document-Google-Docs (6)](https://github.com/osugi001/CS152/assets/102548267/f10d2745-6738-4a52-97cb-2d36249063ab)

* (Q5) How many files are produced in the output?
![Untitled-document-Google-Docs (7)](https://github.com/osugi001/CS152/assets/102548267/3e9a7544-e908-4915-8dfa-7ab944076539)



* (Q6) Explain this number based on the input file size and default block size.
* The mapper task has been executed within the Filter program, resulting in a single output file named part-m-0000. This file comprises 27,972 entries, and each of these entries has a response code of 200.


* (Q7) How many files are produced in the output directory and how many lines are there in each file?
* 4 lines 00000 file and 0 lines in 00001 file
* ![Untitled-document-Google-Docs (8)](https://github.com/osugi001/CS152/assets/102548267/faec9692-6eb9-4ea5-ba2d-258356a04a12)


* (Q8) Explain these numbers based on the number of reducers and number of response codes in the input file.
* Same thing occur just like in question 6. The mapper task has been executed within the aggregation program, resulting in a double output file named part-m-0000. 


* (Q9) How many files are produced in the output directory and how many lines are there in each file?
* For r 000000 there are 5 lines for 000001 there are 2 lines
  ![Untitled-document-Google-Docs (8)](https://github.com/osugi001/CS152/assets/102548267/20bcb07d-b50c-415d-8b2f-56d655369b1d)


* (Q10) Explain these numbers based on the number of reducers and number of response codes in the input file.
* The entries were directed to a single reducer within the aggregation program, which explains why there is no data or output in the file part-r-00001. The output file lists the response codes of the entries along with the cumulative byte size for all entries that share the same response code.

* (Q11) How many files are produced in the output directory and how many lines are there in each file?
* 000000 file is 1, 000001 is 0
  ![Untitled-document-Google-Docs (9)](https://github.com/osugi001/CS152/assets/102548267/c3c0d631-d222-4e80-af54-73914c6fcb49)


* (Q12) Explain these numbers based on the number of reducers and number of response codes in the input file.
* The reason there is only a single output file is that the aggregation operation on the filtered data resulted in a dataset consisting exclusively of records with a response code of 200. This acts similarly to a join condition in a database. Consequently, all the entries were processed by only one reducer, which is why the part-r-00001 file is empty. Hence, the grand total of 37,551,809 bytes is calculated solely from the records that have a response code of 200.



