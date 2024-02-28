# Lab 8

## Student information

* Full name: Owen Sugiarto
* E-mail: osugi001@ucr.edu
* UCR NetID: osugi001
* Student ID: 862296300

## Answers

* (Q1) What is the schema of the file? Copy it to the README file and keep it for your reference.


    ![image](https://github.com/osugi001/CS152/assets/102548267/585f59ef-fc82-4539-acf1-18fd6ad5088c)


* (Q2) What is your command to import the `tweets.json` file?

    ```shell
    mongoimport --db DATA --collection tweets --file ~/tweets.json

    ```

* (Q3) What is the output of the import command?
```
2024-02-27T21:34:52.606-0800    1000 document(s) imported successfully. 0 document(s) failed to import.
```
![image](https://github.com/osugi001/CS152/assets/102548267/e27480d9-3894-4709-bca2-cd5f18bef71d)

* (Q4) What is your command to count the total number of records in the `tweets` collection and what is the output of the command?
* first I moved from test to my database which i name "DATA"
  ```
  use DATA
  ```
    ```javascript
    db.tweets.countDocuments({}) 
    ```

* (Q5) What is your command for this query?

    ```javascript
    db.tweets.aggregate([
  {
    $match: {
      "place.country_code": "JP",
      "user.statuses_count": { $gt: 50000 }
    }
  },
  {
    $project: {
      _id: 0,
      user_name: "$user.name",
      followers_count: "$user.followers_count",
      statuses_count: "$user.statuses_count"
    }
  },
  {
    $sort: { followers_count: 1 }
  }
])

    ```

* (Q6) How many records does your query return?
* 16

* (Q7) What is the command that retrieves the results without the _id field?

    ```javascript
    db.tweets.aggregate([
  {
    $match: {
      "place.country_code": "JP",
      "user.statuses_count": { $gt: 50000 }
    }
  },
  {
    $project: {
      _id: 0, 
      user_name: "$user.name",
      followers_count: "$user.followers_count",
      statuses_count: "$user.statuses_count"
    }
  },
  {
    $sort: { followers_count: 1 }
  }
])

    ```

* (Q8) What is the command to insert the sample document? What is the result of running the command?

    ```javascript
    // Replace here
    ```


* (Q9) Does MongoDB accept this document while the followers_count field has a different type than other records?

* (Q10) What is your command to insert this record?

    ```javascript
    // Replace here
    ```


* (Q11) Where did the two new records appear in the sort order?


* (Q12) Why did they appear at these specific locations?


* (Q13) Where did the two records appear in the ascending sort order? Explain your observation.


* (Q14) Is MongoDB able to build the index on that field with the different value types stored in the `user.followers_count` field?


* (Q15) What is your command for building the index?

    ```javascript
    // Replace here
    ```

* (Q16) What is the output of the create index command?

    ```text
    ```

* (Q17) What is your command for this query?

    ```javascript
    // Replace here
    ```

* (Q18) How many records are returned from this query?

    ```
    // Replace here
    ```

* (Q19) What is your command for this query?
    ```javascript
    // Replace here
    ```

* (Q20) What is the output of the command?

* (Q21) What is your command for this query?
    ```javascript
    // Replace here
    ```

* (Q22) What is the output of the command?
