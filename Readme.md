### How To Create Index in mongoDB to increase the query performance

#### Pick the field in mongo collection which you plan the increase the result performance

#### But before proceeding to create index, measure your existing results by the using the below command

#### using explain("executionStats") in find command will give the details about the query plan

#### Example Run for query plan

> db.pupil.find({ points: { $gt : 444478, $lt : 66676} }).explain("executionStats")
{
        "queryPlanner" : {
                "plannerVersion" : 1,
                "namespace" : "test.pupil",
                "indexFilterSet" : false,
                "parsedQuery" : {
                        "$and" : [
                                {
                                        "points" : {
                                                "$lt" : 66676
                                        }
                                },
                                {
                                        "points" : {
                                                "$gt" : 444478
                                        }
                                }
                        ]
                },
                "winningPlan" : {
                        "stage" : "EOF"
                },
                "rejectedPlans" : [ ]
        },
        "executionStats" : {
                "executionSuccess" : true,
                "nReturned" : 0,
                "executionTimeMillis" : 0,
                "totalKeysExamined" : 0,
                "totalDocsExamined" : 0,
                "executionStages" : {
                        "stage" : "EOF",
                        "nReturned" : 0,
                        "executionTimeMillisEstimate" : 0,
                        "works" : 1,
                        "advanced" : 0,
                        "needTime" : 0,
                        "needYield" : 0,
                        "saveState" : 0,
                        "restoreState" : 0,
                        "isEOF" : 1,
                        "invalidates" : 0
                }
        },
        "serverInfo" : {
                "host" : "ip-172-31-37-195.ec2.internal",
                "port" : 27017,
                "version" : "4.0.2",
                "gitVersion" : "fc1573ba18aee42f97a3bb13b67af7d837826b47"
        },
        "ok" : 1
}

#### here Field ""executionTimeMillis" : 0," which denotes you query execution time in ms , 0 here means less than ms


#### Now below is the command to create index in field in mongoDB to optimize the results.

#### db.collection.createIndex( { name: -1 } )

#### Example : db.pupil.createIndex( { points: -1 } ), im creating index for field name 'points' in the pupil collection

#### Once the index is created measure the query plan and see the difference.


* * *

### How to import CSV File in MongoDB Collection

#### Command : mongoimport -d <DBNAME> -c <CollectionName> --type csv --file <CSV File Name> --headerline
####   here --headerline is optional, which only requires if your file has top line as headers

#### Example : mongoimport -d sample -c sample --type csv --file C2ImportCalEventSample.csv --headerline
