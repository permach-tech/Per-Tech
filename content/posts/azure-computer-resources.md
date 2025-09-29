+++
date = '2025-09-23T02:57:20Z'
draft = false
title = 'Azure Automation Services'
featuredImage = '/img/banners/azure-automations.jpg'
tags = ["Azure", "Automation"]
categories = ["Automation"]
summary = "A comparison of Azure Logic Apps, Azure Functions, and Azure Runbooks for automation tasks."
+++

## Azure Automation Services: Logic Apps, Functions, and Runbooks
You and I both love automation right? I mean, who doesn't want to save time and effort by automating repetitive tasks? In the world of cloud computing, Azure offers several services that can help you achieve this goal. But if you are starting out, often times you ask, just which service should I use?

In this post, we will discuss and compare the 3 Azure Automation services: Azure Logic Apps, Azure Functions, and Azure Runbooks. Each of these services has its own strengths and use cases, so let's dive in and see which one might be the best fit for your automation needs.

## Types of Azure Automation Services

1. **Azure Logic Apps**: This is a cloud-based service that allows you to create workflows and automate processes with little to no code. One of the biggest benefits of Azure Logic Apps, is the ability to use pre-built connectors already included that facilitate integration with various services and platforms.

2. **Azure Functions**: A serverless compute offering, if you prefer a code-centric approach, Azure Functions might be the right choice for you. This service lets your run small pieces of code in response to events, triggers, or schedules. Azure Functions supports multiple programming languages, including C#, JavaScript, Python, PowerShell, and more. Functions are great for lightweight tasks and can be easily scaled to handle varying workloads. They are particularly useful for building APIs, processing data, and integrating with other services.

3. **Azure Runbooks**: Part of Azure Automation, Runbooks are scripts that automate repetitive tasks in your Azure environment. You can create Runbooks using PowerShell or Python, and they can be scheduled to run at specific times or triggered by events. Runbooks are perfect for managing infrastructure, deploying resources, and performing routine maintenance tasks. Ideal for simplicity and longer run times.

## Comparison of Azure Automation Services
| Feature                  | Azure Logic Apps                     | Azure Functions                     | Azure Runbooks                      |
|--------------------------|-------------------------------------|------------------------------------|-------------------------------------|
| **Ease of Use**          | Low-code, drag-and-drop interface   | Code-centric                       | Script-based, PowerShell/Python     |
| **Integration**          | Extensive pre-built connectors      | Custom integrations via code       | Limited connectors, mostly Azure services |
| **Scalability**          | Automatically scales with demand    | Automatically scales with demand   | Scales based on job queue           |
| **Cost**                 | Pay-per-use, based on actions       | Pay-per-use, based on executions    | Pay-per-use, based on job runtime    |
| **Use Cases**            | Workflow automation                | Event-driven tasks, APIs           | Infrastructure management, maintenance |
| **Programming Languages**| None (visual design)                | C#, JavaScript, Python, PowerShell | PowerShell, Python                     |    

## Examples
Now let's take a simple example scenario of each service to illustrate their use cases.
For this example we will get a user a using Microsoft Graph API.

### Azure Runbook
```powershell

# Get System Assigned Managed Identity Access Token
$url = $env:IDENTITY_ENDPOINT  
$headers = New-Object "System.Collections.Generic.Dictionary[[String],[String]]" 
$headers.Add("X-IDENTITY-HEADER", $env:IDENTITY_HEADER) 
$headers.Add("Metadata", "True") 
$body = @{resource='https://graph.microsoft.com/' } 
$token = Invoke-RestMethod $url -Method 'POST' -Headers $headers -ContentType 'application/x-www-form-urlencoded' -Body $body 
$accessToken = $token.access_token

#Form Headers
$headers = @{
    "Authorization" = "Bearer $accessToken"
    "Content-Type" = "application/json"
}

# Make GET Request to Microsoft Graph API
$uri="https://graph.microsoft.com/v1.0/users/barry.allen@persellmachucagmail.onmicrosoft.com"
$data = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

$data
```
![azure-runbook-get](/img/content/runbook-get.png)

### Azure Logic App
Built in connector to get user.

![azure-logic-app](/img/content/logicapp-getuser.png)