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
    // db.tweets.insertOne({
  id: Long("921633456941125634"),
  place: { country_code: 'JP', name: 'Japan', place_type: 'city' },
  user: { user_name: 'xyz2', followers_count: [2100, 5000], statuses_count: 55000 },
  hashtags: ['nature'],
  lang: 'ja'
  })

    ```
    result :   acknowledged: true,
  insertedId: ObjectId('65dedccd757fc07eed884472')


* (Q9) Does MongoDB accept this document while the followers_count field has a different type than other records?
it does accept it
* (Q10) What is your command to insert this record?

    ```javascript
    db.tweets.insertOne({
  id: NumberLong('921633456941121354'),
  place: { country_code: 'JP', name: 'Japan', place_type: 'city' },
  user: { user_name: 'xyz3', followers_count: {last_month: 550, this_month: 2200}, statuses_count: 112000 },
  hashtags: ['art', 'tour'],
  lang: 'ja'
  })

    ```


* (Q11) Where did the two new records appear in the sort order?

*  {
*   followers_count: { last_month: 550, this_month: 2200 },
*    statuses_count: 112000
*  },
*  { followers_count: 6986, statuses_count: 113460 },
*  { followers_count: 6745, statuses_count: 111304 },
*  { followers_count: [ 2100, 5000 ], statuses_count: 55000 },
*  { followers_count: 4578, statuses_count: 52056 },
*  { followers_count: 2606, statuses_count: 65492 },
*  { followers_count: 2278, statuses_count: 52308 },
*  { followers_count: 2197, statuses_count: 51928 },
*  { followers_count: 2049, statuses_count: 52624 },
*  { followers_count: 1320, statuses_count: 59010 },
*  { followers_count: 1165, statuses_count: 57928 },
*  { followers_count: 1004, statuses_count: 94497 },
*  { followers_count: 769, statuses_count: 90326 },
*  { followers_count: 769, statuses_count: 90327 },
*  { followers_count: 769, statuses_count: 90328 },
*  { followers_count: 769, statuses_count: 90329 },
*  { followers_count: 754, statuses_count: 70166 },
*  { followers_count: 522, statuses_count: 56256 }

* (Q12) Why did they appear at these specific locations?
* Numeric values are sorted from highest to lowest.
An array ([2100, 5000]) is considered by its first element for sorting, placing it after singular numeric values higher than 2100.
An object ({last_month: 550, this_month: 2200}) is sorted last, as MongoDB sorts objects differently from simple numeric values, typically placing them at the end when sorting numerically.


* (Q13) Where did the two records appear in the ascending sort order? Explain your observation.
*[
*  { followers_count: 522, statuses_count: 56256 },
*  { followers_count: 754, statuses_count: 70166 },
*  { followers_count: 769, statuses_count: 90326 },
*  { followers_count: 769, statuses_count: 90327 },
*  { followers_count: 769, statuses_count: 90328 },
*  { followers_count: 769, statuses_count: 90329 },
*  { followers_count: 1004, statuses_count: 94497 },
*  { followers_count: 1165, statuses_count: 57928 },
*  { followers_count: 1320, statuses_count: 59010 },
*  { followers_count: 2049, statuses_count: 52624 },
*  { followers_count: [ 2100, 5000 ], statuses_count: 55000 },
*  { followers_count: 2197, statuses_count: 51928 },
*  { followers_count: 2278, statuses_count: 52308 },
*  { followers_count: 2606, statuses_count: 65492 },
*  { followers_count: 4578, statuses_count: 52056 },
*  { followers_count: 6745, statuses_count: 111304 },
*  { followers_count: 6986, statuses_count: 113460 },
*  {
*    followers_count: { last_month: 550, this_month: 2200 },
*    statuses_count: 112000
*  }

]
* The record with followers_count as an array [2100, 5000] was placed between the numeric followers_count values of 2049 and 2197. This indicates that MongoDB, for sorting purposes, likely considered the first element of the array (2100).

The record with followers_count as an object {last_month: 550, this_month: 2200} was placed at the end of the list. This positioning is because MongoDB sorts numeric values before object types, hence why a document with an object for followers_count appears after all documents with numeric followers_count values.


* (Q14) Is MongoDB able to build the index on that field with the different value types stored in the `user.followers_count` field?
Yes, MongoDB can build an index on a field even if the data types of the field's values vary across documents.

* (Q15) What is your command for building the index?

    ```javascript
    db.tweets.createIndex({ "user.followers_count": 1 })
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
