# IQ Assistant Thread

## Summary

### Entity Name

IQ Assistant Thread

### Database Table Name

`tIqAssistantThread`

### API Object Name

`DbIqAssistantThread`

### Entity Description

IQ Assistant Thread serve as a record of past conversations using TrakSYS IQ. These Threads are unique based on the Site and User that used provided the prompts.

## Properties

`ThreadName`

Contains the title for the current Thread. This is usually based on the contents of the first prompt of the Thread.

`IqAssistantID`

Specifies the IQ Assistant currently associated with the configure Thread.

`AiThreadID`

Contains a unique identifier for the current Thread. This is the ID that is used to send and recieve responses from the AI service for the current Thread.

`UserID`

Specifies the ID of the user interacting with TrakSYS IQ.

`InitialContextSummary`

Specifies a human-readable output of additional context that was provided to TrakSYS IQ to help generate a more accurate response.

{% hint style="info" %}
The information provided in this field is different than the actual data sent with the prompt. The text in this prompt simply provides a description of the raw data was sent with the prompt.
{% endhint %}

`CreatedDateTime`

Contains the Date/Time stamp of when the Thread was initally created.
