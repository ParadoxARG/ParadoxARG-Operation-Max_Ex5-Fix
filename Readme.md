# Help Desk Bot Hands-on Lab Exercise 5 FIX

## Overview

This is a brief explanation of all the changes you need to apply to the Exercise 4 solution to be able to deploy it in azure, after reading this guide you should complete the Exercise 5 steps to finish deploying the bot.
First we need to move all the user data from the bot-framework default storage(state) to Azure Cosmos DB, as the bot-framework V3 default storage has been deprecated. For this we will need to install and update some packages.
Lastly we will fix some code that needs to be refactored due to the packages updates.


## NuGet packages

We need to update `System.Identity.Token.Jwt`. This will fix the secure app connection.

![token](./images/token.png)

Next we need to install `Autofac.WebApi2`

![autofac](.images/autofac.png)

Finally we have to install `Microsoft.Bot.Builder.Azure v 3.16`

![azure](./images/azure.png)

## Configure CosmosDB

Follow the instructions [here](https://chatbotslife.com/managing-state-and-logging-chat-history-in-microsoft-bot-framework-aeb330c688c5)

## Fix package upgrade changes

Open RootDialog.CS and modify the category and severity retrieval with the following lines:

    ```csharp
    try
		{
			this.category = (string)((List<object>)categoryEntityRecommendation.Resolution["values"])[0];
		}
	catch { }
	try
		{
			this.severity = (string)((List<object>)severityEntityRecommendation.Resolution["values"])[0];
		}
	catch { }
    ```
	
## Special Note

You can download the project from this repository. If you do, don't forget to change your LuisModel account and the app settings credentials.