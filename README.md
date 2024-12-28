# CODTECH-TASK-3
What is AWS Lambda?
AWS Lambda is a serverless computing service provided by Amazon Web Services (AWS). Users of AWS Lambda create functions, self-contained applications written in one of the supported languages and runtimes, and upload them to AWS Lambda, which executes those functions in an efficient and flexible manner.

The Lambda functions can perform any kind of computing task, from serving web pages and processing streams of data to calling APIs and integrating with other AWS services.

The concept of “serverless” computing refers to not needing to maintain your own servers to run these functions. AWS Lambda is a fully managed service that takes care of all the infrastructure for you. And so “serverless” doesn’t mean that there are no servers involved: it just means that the servers, the operating systems, the network layer and the rest of the infrastructure have already been taken care of, so that you can focus on writing application code.

How does AWS Lambda work?
Each Lambda function runs in its own container. When a function is created, Lambda packages it into a new container and then executes that container on a multi-tenant cluster of machines managed by AWS. Before the functions start running, each function’s container is allocated its necessary RAM and CPU capacity. Once the functions finish running, the RAM allocated at the beginning is multiplied by the amount of time the function spent running. The customers then get charged based on the allocated memory and the amount of run time the function took to complete.

The entire infrastructure layer of AWS Lambda is managed by AWS. Customers don’t get much visibility into how the system operates, but they also don’t need to worry about updating the underlying machines, avoiding network contention, and so on—AWS takes care of this itself.

And since the service is fully managed, using AWS Lambda can save you time on operational tasks. When there is no infrastructure to maintain, you can spend more time working on the application code—even though this also means you give up the flexibility of operating your own infrastructure.

One of the distinctive architectural properties of AWS Lambda is that many instances of the same function, or of different functions from the same AWS account, can be executed concurrently. Moreover, the concurrency can vary according to the time of day or the day of the week, and such variation makes no difference to Lambda—you only get charged for the compute your functions use. This makes AWS Lambda a good fit for deploying highly scalable cloud computing solutions.

Why is AWS Lambda an essential part of the Serverless architecture?
When building Serverless applications, AWS Lambda is one of the main candidates for running the application code. Typically, to complete a Serverless stack you’ll need:

a computing service;
a database service; and
an HTTP gateway service.
Lambda fills the primary role of the compute service on AWS. It also integrates with many other AWS services and, together with API Gateway, DynamoDB and RDS, forms the basis for Serverless solutions for those using AWS. Lambda supports many of the most popular languages and runtimes, so it’s a good fit for a wide range of Serverless developers.

What are the most common use cases for AWS Lambda?
Due to Lambda’s architecture, it can deliver great benefits over traditional cloud computing setups for applications where:

individual tasks run for a short time;
each task is generally self-contained;
there is a large difference between the lowest and highest levels in the workload of the application.
Some of the most common use cases for AWS Lambda that fit these criteria are:
Scalable APIs. When building APIs using AWS Lambda, one execution of a Lambda function can serve a single HTTP request. Different parts of the API can be routed to different Lambda functions via Amazon API Gateway. AWS Lambda automatically scales individual functions according to the demand for them, so different parts of your API can scale differently according to current usage levels. This allows for cost-effective and flexible API setups.
‍
Data processing. Lambda functions are optimized for event-based data processing. It is easy to integrate AWS Lambda with datasources like Amazon DynamoDB and trigger a Lambda function for specific kinds of data events. For example, you could employ Lambda to do some work every time an item in DynamoDB is created or updated, thus making it a good fit for things like notifications, counters and analytics.

Task automation
With its event-driven model and flexibility, AWS Lambda is a great fit for automating various business tasks that don’t require an entire server at all times. This might include running scheduled jobs that perform cleanup in your infrastructure, processing data from forms submitted on your website, or moving data around between different datastores on demand.

Supported languages and runtimes
As of now, AWS Lambda doesn’t support all programming languages, but it does support a number of the most popular languages and runtimes. This is the full list of what’s supported:

Node.js 8.10
Node.js 10.x (normally the latest LTS version from the 10.x series)
Node.js 12.x (normally the latest LTS version from the 12.x series)
Python 2.7
Python 3.6
Python 3.7
Python 3.8
Ruby 2.5
Java 8 - This includes JVM-based languages that can run on Java 8’s JVM — the latest Clojure 1.10 and Scala 2.12 both run on Java 8 so can be used with AWS Lambda
Java 11
Go 1.x (latest release)
C# — .NET Core 1.0
C# — .NET Core 2.1
PowerShell Core 6.0
All these runtimes are maintained by AWS and are provided in an Amazon Linux or Amazon Linux 2 environment. For each of the supported languages, AWS provides an SDK that makes it easier for you to write your Lambda functions and integrate them with other AWS services.
‍
A few additional runtimes are still in the pre-release stage. These runtimes are being developed as a part of AWS Labs and are not mentioned in the official documentation:

Rust 1.31
C++
The C++ runtime also serves as an example for creating custom runtimes for AWS Lambda. See the AWS docs for the details of how to create a custom runtime if your language isn’t supported by default.

Benefits of using AWS Lambda
AWS Lambda has a few unique advantages over maintaining your own servers in the cloud. The main ones are:

Pay per use. In AWS Lambda, you pay only for the compute your functions use, plus any network traffic generated. For workloads that scale significantly according to time of day, this type of billing is generally more cost-effective.
‍
Fully managed infrastructure. Now that your functions run on the managed AWS infrastructure, you don’t need to think about the underlying servers—AWS takes care of this for you. This can result in significant savings on operational tasks such as upgrading the operating system or managing the network layer.
‍
Automatic scaling. AWS Lambda creates the instances of your function as they are requested. There is no pre-scaled pool, no scale levels to worry about, no settings to tune—and at the same time your functions are available whenever the load increases or decreases. You only pay for each function’s run time.
‍
Tight integration with other AWS products. AWS Lambda integrates with services like DynamoDB, S3 and API Gateway, allowing you to build functionally complete applications within your Lambda functions.

Limitations of AWS Lambda
While AWS Lambda has many advantages, there are a few things you should know before using it in production.

Cold start time
When a function is started in response to an event, there may be a small amount of latency between the event and when the function runs. If your function hasn’t been used in the last 15 minutes, the latency can be as high as 5-10 seconds, making it hard to rely on Lambda for latency-critical applications. There are ways to work around it, including a method we wrote about in our blog.

Function limits
The Lambda functions have a few limits applied to them:
‍
Execution time/run time. A Lambda function will time out after running for 15 minutes. There is no way to change this limit. If running your function typically takes more than 15 minutes, AWS Lambda might not be a good solution for your task.
‍
Memory available to the function. The options for the amount of RAM available to the Lambda functions range from 128MB to 3,008MB with a 64MB step.
‍
Code package size. The zipped Lambda code package should not exceed 50MB in size, and the unzipped version shouldn’t be larger than 250MB.
‍
Concurrency. By default, the concurrent execution for all AWS Lambda functions within a single AWS account are limited to 1,000. (You can request a limit increase for this number by contacting AWS support.)

Any Lambda executions triggered above your concurrency limit will be throttled and will be forced to wait until other functions finish running.
‍
Payload size. When using Amazon API Gateway to trigger Lambda functions in response to HTTP requests (i.e. when building a web application), the maximum payload size that API Gateway can handle is 10MB.

Not always cost-effective
On AWS Lambda, you pay only for the used function runtime (plus any associated charges like network traffic). This can produce significant cost savings for certain usage patterns, for example, with cron jobs or other on-demand tasks. However, when the load for your application increases, the AWS Lambda cost increases proportionally and might end up being higher than the cost of similar infrastructure on AWS EC2 or other cloud providers.

Limited number of supported runtimes
While AWS Lambda allows adding custom runtimes, creating them can be a lot of work. So if the version of the programming language you are using isn’t supported on Lambda, you might be better off using AWS EC2 or a different cloud provider.

AWS Lambda pricing
A number of AWS Lambda executions are included with the AWS Free Tier with every AWS account. Unlike some other services, the Lambda free tier isn’t limited to 12 months. Both existing and new accounts get 1 million AWS Lambda requests plus 400,000 GB-seconds per month — Lambda’s measure of function runtime and the memory allocated to a function.
‍
Beyond the free tier the pricing for AWS Lambda is as follows:

Aspect

Pricing

Comment

Requests

$0.20 per 1M requests

The free tier includes 1M requests.

Function memory and run time

$0.0000166667 per GB-second

The free tier includes 400,000 GB-seconds.

Inbound network traffic to the Lambda function

Free

Outbound network traffic—within the same AWS region

$0.01/GB

Outbound network traffic—to other AWS regions

$0.02/GB

Outbound network traffic—to public internet

$0.09/GB

Lower pricing per GB applies starting at 10TB/month.

Amazon API Gateway

$3.50 per 1M requests

If you are using API Gateway with Lambda functions. Lower pricing from 333M requests per month and up.

For each execution, the total cost will be the sum of all applicable factors, including the cost per request, the memory and run time, and the network traffic.

Example cost calculations
Scheduled jobs. Imagine that you run cron jobs in your AWS infrastructure that perform database rollovers. The job runs every night and the average run time is 10 minutes. The function uses 1GB of memory while running. There is no outbound network traffic generated by the function as it connects to your RDS database in the same availability zone.
‍
Total compute: 30 days x 600 GB-seconds (10 minutes) = 18,000 GB-seconds Total requests: 30 days x 1 request per day = 30 requests
‍
This usage is within the AWS free tier, so you’ll be charged $0 for AWS Lambda. Note: You’ll still pay for the RDS usage according to the RDS price list.
‍
HTTP API. Let’s assume that you’re building a web application based entirely on an AWS Lambda backend. Let’s also assume that you’re great at marketing, so after a few months you’ll have 10,000 users in the app every day on average.

Each user’s actions within the app will result in 100 API requests per day, again, on average. Your API runs in Lambda functions that use 512MB of memory, and serving each API request takes 1 second.
‍
Total compute: 30 days x 10,000 users x 100 requests x 0.5GB RAM x 1 second = 15,000,000 GB-seconds Total requests: 30 days x 10,000 users x 100 requests = 30,000,000 requests
‍
For the 30M requests you’ll pay 30 x $0.20/1M requests = $6/month on AWS Lambda.
‍
All these requests go through Amazon API Gateway, so there for the 30M requests you’ll pay 30 x $3.50/1M requests = $105/month on API Gateway.
‍
For the monthly 15M GB-seconds of compute on AWS Lambda you’ll pay 15M * $0.0000166667/GB-second ~= $250/month.
‍
So the total cost of the API layer will be around $360/month with this load.

Frequently asked questions (FAQ)
No, AWS Lambda itself is a proprietary system that’s only available within AWS.

AWS Lambda provides an API that you can use to perform many kinds of operations on your functions, from deploying a new version of the function’s code to seeing the function’s layers to deleting functions. You can see the full description of the AWS Lambda API in the API reference docs. You can also use AWS Lambda to build your own APIs: check out the resources section of this article for more details.

Yes. One option is to use the Lambda API (invoked via the AWS SDK in your function code) to call another function. Another option is to use a queue service like Amazon SNS to create an SNS message from one function and then use it as an event to trigger the second function. Yet another option is to use AWS Step Functions to build a workflow that includes multiple functions.

Getting started with AWS Lambda
In this section we cover the steps needed to create, deploy and secure AWS Lambda functions. We cover two approaches: using the AWS console and API directly, and using the Serverless Framework.

Creating AWS Lambda functions using the AWS console
If you wish, you can use the AWS Lambda console to create your first function. In the AWS console, choose Lambda:


Once in the Lambda management console, click Create Function:


Add a name for your new function and choose the desired runtime. After that, click “Create function” to confirm the settings:


That’s it: the function is created, and you can now work on the function code and deploy the function directly in the Lambda console.


We don’t recommend creating production Lambda functions via the management console for a two reasons:

Your function code will be limited to 30MB.
You’ll need to use the AWS web IDE to write the code in the browser. This IDE only provides very basic revision tracking and limits the collaboration on the code.
Creating AWS Lambda functions using the Serverless Framework
We recommend getting started with AWS Lambda by using Serverless Framework. With the Serverless Framework, you can create Lambda functions using the tools you’re familiar with on your local machine and deploy to AWS in seconds. With this approach, your function’s code and configuration are located in the same Git repository which makes collaboration, change tracking and deployment of Lambda functions easier.

1. Install Serverless Framework on your machine:
‍
$ npm install serverless -g
‍
2. Create a new service:
‍
$ serverless
‍
3. Add the resources your function needs to the serverless.yml file. Check out the AWS Intro doc for an example of this file and the list of options you can configure there.
‍
4. Add code to your service. See the Serverless AWS provider docs for specific steps you can follow to create your functions.
‍
5. Deploy to AWS by running the deploy step:
‍
$ serverless deploy

That’s it! Your function will be deployed and you’ll see the URL of the function’s endpoint in your console.

We would be creating a simple web application called ‘To the Power Of Math’. The application will solve a simple Math problem where we will have a base, an exponent and a calculated result. So in a nutshell, we would host the webapp using Amplify, when we input our values and calculate, we would invoke a Lambda function using API Gateway and then the results will be stored in a DynamoDB table. Now lets get into the project and see how these services work together!

List of AWS Services used in this project;

AWS Amplify
Lambda
IAM
API Gateway
DynamoDB
OBJECTIVES

A way to create/host a webpage
A way to do some math
A way to invoke the math functionality
Somewhere to store/return the math result
A way to handle permissions
PREQUISITES

A text editor {Notepad++, Notepad, etc}
An AWS account and access to the console
Basic knowledge of AWS
First of all, on your local machine, create a new ‘index.html’ file. In my case, I used V.S Code (if you don’t have vs code you can make use of any other text editor like Notepad or Notepad++…). Next paste in the code below in your newly created file.

<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>To the Power of Math!</title>
</head>

<body>
    To the Power of Math!
</body>
</html>
We’re basically just going to display ‘To the power of math’ on our browser for now. Next, save it and zip up the file (in my case, I zipped up the file by sending to compressed folder).

Now open up the AWS Console and navigate to Amplify. We will be using Amplify to deploy and host our web page. Search Amplify (Do that by using the search bar at the top left) and select it.

Click Get started under Amplify Hosting.



Input the details as seen above.

Drag and drop the zip file you created earlier, then click save and deploy.


You can use the domain link available to check the page.

A way to do some Math
To achieve this, we would use a Lambda function. Lambda function is code that runs (serverlessly) and responds to some triggers.

So we’ll write some Python code and use the Python Math Library to do the calculations we need.

Head over to Lambda and create a function using Runtime (Python 3.9)


Scroll down to the code source under the code tab, and update the code with the code below.

# import the JSON utility package
import json
# import the Python math library
import math

# define the handler function that the Lambda service will use an entry point
def lambda_handler(event, context):

# extract the two numbers from the Lambda service's event object
    mathResult = math.pow(int(event['base']), int(event['exponent']))

    # return a properly formatted JSON object
    return {
    'statusCode': 200,
    'body': json.dumps('Your result is ' + str(mathResult))
    }

After inputting the code, save it (Ctrl+S) and most importantly, deploy it by clicking deploy at the top.

Next lets test to make sure this functions as we expect. Click Test > Configure test event.


Scroll down and edit ‘Event JSON’. Put in the values you want.


Click save.

Then click Test [What we did earlier was to configure the test event, now we would run the test by clicking the Test button]

We should get a status code of “200” and verification that your result is “8” [depending on the values you entered].


If you got that then your Lambda function is working!

So far we have our simple html page hosted on Amplify and a Lambda function to do some basic math.

A way to invoke the Math functionality
We would do this by invoking the Lambda function. For that, we would be using API Gateway. API Gateway is used to build HTTP, REST, and WebSocket APIs. So navigate to API Gateway console, we will be using a REST API.



Next create method.

Method type should be ‘POST’.

Integration type should be ‘Lambda function’ (Power of math function).

Then create method.



Next, we have to enable Cross Origin Resource Sharing (C.O.R.S). Enabling C.O.R.S allows a web application running in one origin or domain to be able to access resources on a different origin or domain. So because our web application is running in one domain on Amplify and our Lambda function will be running in another, we need to be able to work across these domains or origins that’s why we’re enabling C.O.R.S.



Select POST and leave the other settings as default and click save.

Now let’s deploy API so we can test it out.


Copy the Invoke URL and save it somewhere for later (You can save on your notepad or anywhere you want)


On the left hand side of your console click Resources, then click on POST. Go to Test.




If you see this then it works!

Now we can trigger our math function in Lambda with an API call.

Somewhere to store/return the math result
We would be using DynamoDB as our database.

NB: We don’t necessarily need to store the results anywhere, we could just return them straightaway but because most real world applications require databases let’s see how to set one up.

DynamoDB is a key value (NoSQL) database.

On your AWS console, navigate to DynamoDB console and create a table


Leave every other settings as default, then click Create table.

Save the Amazon Resource Name (ARN) for the table. Do so by clicking into the table, under General Information select Additional Info, copy the ARN and paste it into the same notepad or wherever you stored the other links.

A way to handle permission
We have to give our Lambda function permission to write to our database table. Go back to our Lambda function, go to the Configuration tab, click on permissions. Then click on the role name under Execution role.


The execution role should open up in a new tab in your browser. We need to add some additional permissions to what the role has already, permissions related to DynamoDB. On the right click on Add permissions > Create inline policy. Policy editor should be JSON.


Paste this JSON Policy.

{
"Version": "2012-10-17",
"Statement": [
    {
        "Sid": "VisualEditor0",
        "Effect": "Allow",
        "Action": [
            "dynamodb:PutItem",
            "dynamodb:DeleteItem",
            "dynamodb:GetItem",
            "dynamodb:Scan",
            "dynamodb:Query",
            "dynamodb:UpdateItem"
        ],
        "Resource": "YOUR-TABLE-ARN"
    }
    ]
}
And most importantly update the “Resource”: “YOUR-TABLE-ARN” with the table ARN you copied and saved a while ago.


After that scroll down and click on Next.

Give your policy a name like “PowerOfMathDynamoDBPolicy”.

Then proceed to create the policy.

Now let’s update the Lambda function to actually go right to the database. Go back to your Lambda function, under the Code tab, replace everything with this code.

# import the JSON utility package
import json
# import the Python math library
import math

# import the AWS SDK (for Python the package name is boto3)
import boto3
# import two packages to help us with dates and date formatting
from time import gmtime, strftime

# create a DynamoDB object using the AWS SDK
dynamodb = boto3.resource('dynamodb')
# use the DynamoDB object to select our table
table = dynamodb.Table('PowerOfMathDatabase')
# store the current time in a human readable format in a variable
now = strftime("%a, %d %b %Y %H:%M:%S +0000", gmtime())

# define the handler function that the Lambda service will use an entry point
def lambda_handler(event, context):

# extract the two numbers from the Lambda service's event object
    mathResult = math.pow(int(event['base']), int(event['exponent']))

# write result and time to the DynamoDB table using the object we instantiated and save response in a variable
    response = table.put_item(
        Item={
            'ID': str(mathResult),
            'LatestGreetingTime':now
            })

# return a properly formatted JSON object
    return {
    'statusCode': 200,
    'body': json.dumps('Your result is ' + str(mathResult))
    }
Then save (Ctrl+S) and Deploy.

After deploying click test. If your execution result is correct then you’re good to go!

Now let’s go look into our DynamoDB table. On your DynamoDB console, click into your PowerOfMathDB table and click Explore table items (This will show you what has been stored on your database).


As you can see, we have our result and also the time occurrence.

Next, let us update our index.html file. Paste in this final code.


<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>To the Power of Math!</title>
    <!-- Styling for the client UI -->
    <style>
    h1 {
        color: #FFFFFF;
        font-family: system-ui;
  margin-left: 20px;
        }
 body {
        background-color: #222629;
        }
    label {
        color:  #b871b7;
        font-family: system-ui;
        font-size: 20px;
        margin-left: 20px;
  margin-top: 20px;
        }
     button {
        background-color: #32c2c2;
  border-color: #b871b7;
        border-radius: 10px;
        border-width: 3px;
  color: #FFFFFF;
        font-family: system-ui;
        font-size: 20px;
  font-weight: bold;
        margin-left: 30px;
  margin-top: 20px;
  width: 140px;
        }
  input {
        color: #222629;
        font-family: system-ui;
        font-size: 20px;
        margin-left: 10px;
  margin-top: 20px;
  width: 100px;
        }
    </style>
    <script>
        // callAPI function that takes the base and exponent numbers as parameters
        var callAPI = (base,exponent)=>{
            // instantiate a headers object
            var myHeaders = new Headers();
            // add content type header to object
            myHeaders.append("Content-Type", "application/json");
            // using built in JSON utility package turn object to string and store in a variable
            var raw = JSON.stringify({"base":base,"exponent":exponent});
            // create a JSON object with parameters for API call and store in a variable
            var requestOptions = {
                method: 'POST',
                headers: myHeaders,
                body: raw,
                redirect: 'follow'
            };
            // make API call with parameters and use promises to get response
            fetch("https://4qn3bf7v59.execute-api.us-east-1.amazonaws.com/dev", requestOptions)
            .then(response => response.text())
            .then(result => alert(JSON.parse(result).body))
            .catch(error => console.log('error', error));
        }
    </script>
</head>
<body>
    <h1>TO THE POWER OF MATH!</h1>
 <form>
        <label>Base number: </label> 
        <input type="text" id="base"> <br> <br>
        <label>To the power of: </label> 
        <input type="text" id="exponent"> <br> <br>
        <!-- set button onClick method to call function we defined passing input values as parameters -->
        <button type="button" onclick="callAPI(document.getElementById('base').value,document.getElementById('exponent').value)">CALCULATE</button>
    </form>
</body>
</html>
In the script tag, you have to update your “API Gateway Endpoint”. So copy your Endpoint url from where you saved it earlier and update it.


So basically that is the code that will pass your base and exponent to the API Gateway Endpoint and we’ll get the alert back with the result of the calculation.

Next, delete the initial zip file created from the index.html file and then create a new zip file from the updated one. Then redeploy it on Amplify.

After successfully deploying it, you can click the domain link to check out your web application and test it out.


Put in some values and check that your application works correctly.
