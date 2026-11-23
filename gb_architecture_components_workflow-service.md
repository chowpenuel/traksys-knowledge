# Workflow Service

The TrakSYS Workflow Service is the decision control orchestration engine for Visual Workflow. This service is reponsible for the management and execution of process visualizations. The Workflow Service loads its configuration from the database (upon service start/restart) and runs constantly in the background.

{% hint style="warning" %}
The Workflow Service cannot be started unless there is at least one Process Definition configured.
{% endhint %}
