# IQ Assistant Thread Item

## Summary

### Entity Name

IQ Assistant Thread Item

### Database Table Name

`tIqAssistantThreadItem`

### API Object Name

`DbIqAssistantThreadItem`

### Entity Description

IQ Assistant Thread Items contain the chat history for a given Thread. They contain the user prompts, the responses, and the timing data for each message.

## Properties

`IqAssistantThreadID`

Specifies the ID of the IQ Assistant Thread associated with the current Thread Item.

`Question`

Contains the text of the prompt provided by the user. This is the prompt that is processed by TrakSYS IQ.

`Answer`

Contents the content provided for the answer to the original prompt.

`ErrorCode`

Provides the error code generated for the response. This field will be populated if TrakSYS IQ encounters any issues while trying to generate a response for a given prompt.

`ErrorContent`

Contains the text of the error message for a response. This field will be populated if TrakSYS IQ encounters any issues while trying to generate a response for a given prompt.

`RequestDateTime`

Specifies the Date/Time stamp of when a user submitted a prompt to TrakSYS IQ.

`ResponseDateTime`

Specifies the Date/Time stamp of when TrakSYS IQ provided a response to a given prompt.
