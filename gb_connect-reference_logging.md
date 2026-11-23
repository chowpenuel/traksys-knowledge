# Logging

Connect includes dedicated logging infrastructure to automatically record each Interface Transaction and its corresponding log entries along with Content Pages to view and manage transactions and payloads.

{% hint style="info" %}
Custom log entries can be created as needed via the API for debugging or informational purposes by using the [Create Transaction Log](../api-reference/api-services-reference/api.connect/createtransactionlog) or [Create Transaction Logs from Result](../api-reference/api-services-reference/api.connect/createtransactionlogsfromresult) methods. Custom logging can be added during the intial Interface Transaction call as well as during post processing.
{% endhint %}

## tInterfaceTransaction

This is the main transaction database table. It contains header records for each executed Connect Interface Transaction, e.g. start datetime, end datetime, message and response payloads. For a complete description of its fields, see [Interface Transaction](../entity-reference/data-entities/interface-transaction).

## tInterfaceTransactionLog

This is a child table to `tInterfaceTransaction`, containing multiple log records for a given transaction under its header record. The transaction log records include informational entries as well as errors. For a complete description of its fields, see [Interface Transaction Log](../entity-reference/data-entities/interface-transaction-log).

## Interface Transaction Viewer

This page displays a filterable list of Connect Interface Transactions for the specified Interface Definition. The page is intended for a single Interface Definition, a separate instance is necessary for each Interface Definition of interest.

The page will display a table of transactions for the configured Interface Definition based on the user-defined page filters. Clicking on a transaction on the table will display its associated transaction log records which can also be clicked for additional details on the log entry. The table also includes actions to view the associated message and/or response payloads for the given transaction via a c-equals page of the Payload Viewer.

In addition, up to five distinct interface-specific custom actions are configurable on the page to appear as buttons on the row of the transaction table (e.g. redirect to a page that reprocesses the payload).

For a complete description of its fields, see [Interface Transaction Viewer](../tsweb/content-reference/content-page-reference/application/connect/interface-transaction-viewer).

## Payload Viewer

This page can be called with an Interface Transaction ID parameter to display the contents of the Transaction’s Payload field (XML, JSON, CSV, etc.). It is commonly used in conjunction with the Interface Transaction Viewer but can also be used on its own.

For a complete description of its fields, see [Payload Viewer](../tsweb/content-reference/content-page-reference/application/connect/payload-viewer).

{% hint style="info" %}
Unlike the regular TrakSYS Log viewer page, the Connect built-in Content Pages are not instanced by default in order to allow flexibility as to their placement in the application.
{% endhint %}
