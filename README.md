# Example Project to Decouple session for .NET, and .NET Cores MVC

## Information
- AWS Accounts

- .NET knowledge, C#

- This is for example reference only, You can copy, and tweak it, based on your application requirements.

--- 
## 1.) Implement Session State in ASP.NET

AWS has provide Amazon DynamoDB Session State Provider allows ASP.NET applications store their sessions inside DynamoDB. This helps applications scale across multiple application servers while maintaining session state across the system.

This is quite straght forward how to implement it, I would suggest to look at the link below:
    
    https://github.com/aws/aws-dotnet-session-provider
    
    https://www.youtube.com/watch?v=9iphbb0w-ig&t=419s

You can refer to my example code file name "aspdotnetmvc_sessionstate.zip"
(It's has been tested, and deploy with Multi node elastic beantalk on Windows 2009 IIS 10.)

---
## 2.) Implement Session State in ASP.NET Core

Kirk Davis has implemented ASP.NET Core session state using DynamoDB to hold session state itself, and SSM Parameter Store to hold the cookie encryption keys (Necessary if you want to have session state across more than one instance/container/Lambda-function).

The solution consisted of two main parts:

1.)DynamoDbCache, which implements IDistributedCache, along with some helper classes for options, and a class that enables using it with DI in Startup.

The files you want are: DynamoDbCache.cs, DynamoDbCacheOptions.cs, DynamoDbCacheServiceCollectionExtensions.cs

2.) PsXmlRepository, AWS released a NuGet package that implements IXmlRepository, and stores the keys in Parameter Store.

Finally for SSM, The package name is Amazon.AspNetCore.DataProtection.SSM

You can read the blog announcement for this package for detailed instructions on using the package: 
   
    https://aws.amazon.com/blogs/developeraws-ssm-asp-net-core-data-protection-provider/

3.) In .NET core project, please get all required package from NuGet
                    
    * AWSSDK.DynamoDBv2
    * AWSSDK.Extensions.NETCore.Setup
    * Amazon.AspNetCore.DataProtection.SSM
    * Newtonsoft.Json






    
Credit: Kirk Davis

Reference Project:
    
    https://github.com/Kirkaiya/AwsReinventWIN401/tree/master/CartService/Session

