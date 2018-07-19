# Testing DynamoDb & GraphQL with Serverless
Following [this guide from the Serverless website](https://serverless.com/blog/make-serverless-graphql-api-using-lambda-dynamodb/) on how to use GraphQL with DynamoDb.

# How to install
0. Install serverless with `yarn add global serverless` or  `npm install -g serverless`
1. Clone repo.
2. `yarn` or `npm install`
3. [Configure your AWS credentials](https://serverless.com/framework/docs/providers/aws/guide/credentials/)
4. `sls deploy` or `sls deploy --aws-profile serverless` (if `serverless` is your AWS cred name)
5. ????
6. Profit (see below)

# How to use
When deployed, this essentially "transpiles" down to a CloudFormation template. Everything from Serverless does.

Looking in [serverless.yml](serverless.yml) you'll see the config for:
1. DynamoDb table, in this case called `dynamo-testing-dev`
2. Lambda function called `handler` (see [handler.js](handler.js)) which runs the queries

That's all there is.

You can now call the API with cURL:

```bash
curl -Gv 'https://URL-FROM-TERMINAL/dev/query' --data-urlencode 'query={greeting(firstName: "Lee")}'
# {"data":{"greeting":"Hello, Lee."}}
```

Or through PostMan/browser with:
```
https://example.execute-api.eu-west-1.amazonaws.com/dev/query?query=%7Bgreeting%28firstName%3A%20"Lee"%29%7D
```

`URL-FROM-TERMINAL` is found in the terminal after running a deploy, e.g.:

```
$ sls deploy
...
Serverless: Stack update finished...
Service Information
service: dynamo-testing
stage: dev
region: eu-west-1
stack: dynamo-testing-dev
api keys:
  None
endpoints:
  GET - https://example.execute-api.eu-west-1.amazonaws.com/dev/query
functions:
  query: dynamo-testing-dev-query

```

See the [this guide from the Serverless website](https://serverless.com/blog/make-serverless-graphql-api-using-lambda-dynamodb/) for mutations.
