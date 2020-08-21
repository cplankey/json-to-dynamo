# json-to-dynamodb
The deployed lambda will perform take a JSON array and for each item it will insert a record into Amazon DynamoDB. There is a sample JSON file named `fileToImport` that you can modify from the Lambda Console and add your custom content to.


Deploy to your account in the AWS Console using the [Serverless Application Repository](https://serverlessrepo.aws.amazon.com/applications/arn:aws:serverlessrepo:us-east-1:675087241163:applications~json-to-dynamodb-importer)

### Caution!
This Lambda performs a Put event for every record in your array. If you are importing a large table you will want to know the following:
1. If you have set provisioned throughput, all these Put requests may hit the limit. The import will not complete if this happens.
2. The larger the JSON file, the more power you should give your Lambda. [Consider bumping the memory of your lambda](https://docs.aws.amazon.com/lambda/latest/dg/resource-model.html) to a higher setting if you get an error similar to:
```
Runtime exited with error: signal: killed
```
3. If you have a large JSON file the operation may take a longer time. If you experience a timeout in your Lambda, [increase your timeout duration](https://docs.aws.amazon.com/lambda/latest/dg/resource-model.html).



### Assumptions
This assumes you already have a JSON file ready to paste into the console and a DynamoDB table published with a key that matches one of your JSON keys


