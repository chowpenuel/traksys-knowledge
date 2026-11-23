# Historian Service

The TrakSYS Historian Service is a Windows service that collects inputs from automation (OPC) similar to the Logic Service, however, is primarily focused on historizing the collected data to the separate TrakSYS Historian database. The Historian Service loads its configuration from the database (upon service start/restart) and runs constantly in the background. The Service records Tag changes to the TrakSYS Historian database based on Tag History Definition configurations.

{% hint style="warning" %}
The Historian Service cannot be started unless there is at least one Tag History Definition configured.
{% endhint %}
