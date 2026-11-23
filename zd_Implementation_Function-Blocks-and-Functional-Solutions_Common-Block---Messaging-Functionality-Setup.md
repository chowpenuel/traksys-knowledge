# Common Block - Messaging Functionality Setup

*Source: https://portal.parsec-corp.com/hc/en-us/articles/52050599619347-Common-Block-Messaging-Functionality-Setup*
*Last updated: 2026-06-19T00:19:18Z*

---

This article describes one supported pattern for configuring Microsoft Teams notifications with the Common Block messaging capabilities. It is intended as an implementation guide, not a complete reference for every Power Automate option, Teams configuration setting, or TrakSYS configuration setting.

**Recommendation:** Use a service account to own the Power Automate flows and maintain access to the Teams channels used by the implementation.

## Configuration overview

  * TrakSYS configuration: Defines the Channels, Users, and webhook values used by Common Block messaging.
  * Power Automate configuration: Creates the Microsoft Teams flows and provides the webhook URLs required by TrakSYS.



## Requirements

  * Access to a Microsoft Teams account that can post to the target Teams channels.
  * Access to Power Automate for creating and maintaining the required flows.
  * Access to the relevant TrakSYS configuration screens.
  * A TrakSYS email address for each user who should receive direct Teams messages.



## TrakSYS configuration

### Configure a Teams Channel

Create a new Channel from the Channel New/Edit screen. The Channel record creates a TrakSYS DbUser and stores the values used by the messaging service.

**Field** | **Mapped To** | **Description**  
---|---|---  
Name | Display name | The display name used internally by TrakSYS. Use a readable format such as **Teams Channel | <Channel Name>**.  
Webhook URL | Description field | The Power Automate trigger URL for the channel flow. This URL includes workflow identity and authorization/signature values. Treat it as sensitive.  
Channel URL | Notes field | The direct link to the Teams channel. In Microsoft Teams, right-click the channel and select Copy link. To open directly in the Teams app, replace the leading https:// with msteams://.  
![](https://portal.parsec-corp.com/hc/article_attachments/52050878133651)![](https://portal.parsec-corp.com/hc/article_attachments/52050849835923)

### Configure the User Webhook

Set up the shared User Webhook once per implementation. This webhook uses the same URL format as the Channel webhook URLs.

The User Webhook value is stored in TrakSYS as DbCustomData. The specific key is defined in the Common Block Blocks Setting script.

Each TrakSYS user must have an email address assigned to their account to receive messages through the User Webhook.

![](https://portal.parsec-corp.com/hc/article_attachments/52050849837587)![](https://portal.parsec-corp.com/hc/article_attachments/52050849838227)

## Power Automate configuration

### Configure a Channel Flow

1\. In Power Automate, select Create, then select Instant cloud flow. Skip the initial template dialog.

**![](https://portal.parsec-corp.com/hc/article_attachments/52050581892499)**

2\. Rename the flow to TrakSYS to Teams Channel [ <Channel Name>].

![](https://portal.parsec-corp.com/hc/article_attachments/52050581893011)

3\. Add the Microsoft Teams Webhook trigger named When a Teams webhook request is received.

![](https://portal.parsec-corp.com/hc/article_attachments/52050581893651)

![](https://portal.parsec-corp.com/hc/article_attachments/52050581894291)

4\. Set Who can trigger the flow? to Anyone. Close the trigger. You will return to the trigger later to copy the HTTP URL.

**![](https://portal.parsec-corp.com/hc/article_attachments/52050566049427)**

5\. Add a new action below the trigger and select Post card in chat or channel.

![](https://portal.parsec-corp.com/hc/article_attachments/52050566049939)

6\. Sign in with an organization Teams account that has access to the desired Team/channel, if prompted.

![](https://portal.parsec-corp.com/hc/article_attachments/52050581896467)

7\. Configure the action properties as follows:

**Property** | **Value** | **Notes**  
---|---|---  
Post as | Flow bot |   
Post in | Channel |   
Team | <Pick Team> | Select the target Microsoft Teams team.  
Channel | <Pick Channel> | Select the target Teams channel.  
Adaptive Card | triggerBody() | Set this value as an expression, not plain text.  
![](https://portal.parsec-corp.com/hc/article_attachments/52050581897363)

To set the Adaptive Card value as an expression, click into the Adaptive Card field, select the expression/function option, enter triggerBody(), and save the expression.

**![](https://portal.parsec-corp.com/hc/article_attachments/52050566050963)**

8\. Save the flow and wait until Power Automate confirms that the flow is ready.

![](https://portal.parsec-corp.com/hc/article_attachments/52050566052755)

9\. Open the trigger and copy the HTTP URL. Assign this URL to the matching TrakSYS Channel Webhook URL.

**![](https://portal.parsec-corp.com/hc/article_attachments/52050581898259)**

### Configure the User Flow

1\. In Power Automate, select Create, then select Instant cloud flow. Skip the initial template dialog.

![](https://portal.parsec-corp.com/hc/article_attachments/52050566053651)

2\. Rename the flow to TrakSYS to Teams [Users].

![](https://portal.parsec-corp.com/hc/article_attachments/52050599608723)

3\. Add the Microsoft Teams Webhook trigger named When a Teams webhook request is received.

![](https://portal.parsec-corp.com/hc/article_attachments/52050599609235)

4\. Set Who can trigger the flow? to Anyone. Close the trigger. You will return to the trigger later to copy the HTTP URL.

**![](https://portal.parsec-corp.com/hc/article_attachments/52050581904659)**

5\. Add a new action below the trigger and select Parse JSON.

![](https://portal.parsec-corp.com/hc/article_attachments/52050581905299)

6\. Configure the Parse JSON action as follows:

**Property** | **Value** | **Notes**  
---|---|---  
Content | triggerBody() | Set this value as an expression.  
Schema | See JSON schema below. |   
      
    
    {
      "type": "object",
      "properties": {
        "userEmail": {
          "type": "string"
        },
        "card": {
          "type": "object",
          "properties": {}
        }
      }
    }

To set the Content value as an expression, click into the Content field, select the expression/function option, enter `triggerBody()`, and save the expression.

**![](https://portal.parsec-corp.com/hc/article_attachments/52050581906451)**

7\. Add a new action below Parse JSON and select Post card in chat or channel.

![](https://portal.parsec-corp.com/hc/article_attachments/52050599613331)

Configure the action properties as follows:

**Property** | **Value**  
---|---  
Post as | Flow bot  
Post in | Chat with Flow bot  
Recipient | body('Parse_JSON')?['userEmail']  
Adaptive Card | body('Parse_JSON')?['card']  
  
![](https://portal.parsec-corp.com/hc/article_attachments/52050740773139)

To set the Recipient value, click the cog icon above the Recipient field and select **Use dynamic content**. Click into the Recipient field, select the expression/function option, enter `body('Parse_JSON')?['userEmail']`, and save the expression.

**![](https://portal.parsec-corp.com/hc/article_attachments/52050740775059)**

To set the Adaptive Card value as an expression, click into the Adaptive Card field, select the expression/function option, enter`body('Parse_JSON')?['card']`, and save the expression.

8\. Save the flow and confirm that Power Automate reports the flow as ready.

![](https://portal.parsec-corp.com/hc/article_attachments/52050745834771)

9\. Open the trigger and copy the HTTP URL. Assign this URL to the general User Webhook in TrakSYS.

![](https://portal.parsec-corp.com/hc/article_attachments/52050745835795)

## Maintenance notes

  * Webhook URLs include trigger authorization information. Store them carefully and replace them if they are exposed.
  * Use consistent flow names so each TrakSYS Channel can be matched back to the corresponding Power Automate flow.


