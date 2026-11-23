# Configuring an MQTT Connection Using Certificates (TLS)

*Source: https://portal.parsec-corp.com/hc/en-us/articles/39621778810387-Configuring-an-MQTT-Connection-Using-Certificates-TLS*
*Last updated: 2026-02-24T01:48:30Z*

---

Applies To | TrakSYS 13+

### Summary

**Note** : This article is an extension of the main [Configuring an MQTT Connection](https://portal.parsec-corp.com/hc/en-us/articles/38861856867219/live_preview/01JPXAZQE3FTZHYDQF213G9KZQ) article. To start from the beginning, please review that article before proceeding with the steps here. It is strongly recommended to follow the Eclipse Mosquitto installation steps and ensure that an Anonymous connection from TrakSYS to the Broker can be established.

Beginning with TrakSYS 13.0.0 it is possible to use the MQTT (Message Queuing Telemetry Transport) protocol to communicate with other devices. When configuring MQTT with TrakSYS, it is possible to enable One-Way TLS and Mutual TLS. This article will demonstrate how to configure these TLS options.

### One-Way TLS and Mutual TLS

  * **One-Way TLS -** This is also known as server-side TLS. This protocol ensures that the client verifies the broker/server’s certificate to confirm its authenticity. However, the broker/server does not verify the client’s identity. This provides a layer of security by ensuring the client connects to a trusted broker.
  * **Mutual TLS (mTLS) -** This protocol ensures that both the client and the broker/server authenticate each other using certificates. This adds an extra layer of security by ensuring that both parties are trusted before communication occurs.



If basic security is sufficient, One-Way TLS can be used. However, for enhanced security, Mutual TLS is recommended. Additionally, username and password authentication can be used alongside either TLS option. When this option is combined with Mutual TLS, it provides the highest level of security. Note that using Username and Password authentication is **NOT** required for either protocol.

### Installing and Configuring Certificates

While certificates are typically issued and managed through more robust solutions in enterprise environments, this guide demonstrates **untrusted** **certificate generation** using [OpenSSL](https://slproweb.com/products/Win32OpenSSL.html) for demonstration purposes. Note that untrusted certificates should only be used for testing and development purposes.

For simplicity, this example assumes that OpenSSL is installed on the same machine. The Command Prompt (CMD) will be used in several steps to generate and configure certificates with OpenSSL.

This article assumes the user has prior knowledge of certificate management and generation. 

**Notes** :

  * It is recommended to run Command Prompt as an administrator before executing the commands shown in the following steps to avoid any permissions-related issues.
  * While the mosquitto broker will leverage certificate files in .key and .pem format, other brokers may expect certificate files with different formats.



### One-Way TLS Configuration

Open a Command Prompt and navigate to the OpenSSL bin folder.

  1. Generate a Certificate Authority (CA) private key by running the following command:   
  
`openssl genrsa -out ca.key 2048  
`  
![](https://portal.parsec-corp.com/hc/article_attachments/39981667434771)  
  
The `ca.key` file should now be generated.  
  

  2. Create a CA certificate using the CA private key by executing the following command:  
  
`openssl req -new -x509 -days 365 -key ca.key -out ca.pem`  
  
OpenSSL will ask for certificate information. The Common Name should be provided with a descriptive name (e.g. MyMqttCa). All other information can be left blank by pressing enter.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39981644902035)  
  
The `ca.pem` file should now be generated.  
  

  3. Generate the broker's private key by executing the following command:  
  
`openssl genrsa -out <server_name>.key 2048  
`  
![](https://portal.parsec-corp.com/hc/article_attachments/39981644903827)  
  
The `<server_name>.key` file should now be generated.  
  

  4. Generate a Certificate Signing Request (CSR) for the broker by executing the following command:  
  
`openssl req -new -key <server_name>.key -out <server_name>.csr`  
  
OpenSSL will prompt the user for certificate information. The Common Name will need to be set to the host name that the clients will use to connect to the broker. All other information can be left blank by pressing enter.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39981667438099)  
  
The `<server_name>.csr` file should now be generated.  
  

  5. Sign the broker's CSR with the CA certificate by executing the following command:  
  
`openssl x509 -req -in <server_name>.csr -CA ca.pem -CAkey ca.key -CAcreateserial -out <server_name>.pem -days 365  
`  
![](https://portal.parsec-corp.com/hc/article_attachments/39981667439123)  
  
The `<server_name>.pem` file should now be generated.  
  

  6. All of the files should now be generated and should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39981644907539)  
  
For simplicity purposes, the ca.pem, <server_name>.pem, and <server_name>.key files will be moved to C folder (C:\\).  
  

  7. Add the following lines within the Mosquitto configuration file (mosquitto.conf).  

         
         listener 8883
         cafile C:\ca.pem
         certfile C:\<server_name>.pem
         keyfile C:\<server_name>.key  
         require_certificate false  
         # Leave this uncommented to use anonymous authentication  
         allow_anonymous true  
         # Uncomment this line to use Username and Password authentication instead  
         # allow_anonymous false

  
![](https://portal.parsec-corp.com/hc/article_attachments/40228193946131)  
  

     * **Listener:** This sets the to port 8883, which is used for authenticated MQTT communication
     * **Require Certificate:** This setting is set to false, meaning only the server requires a certificate (e.g., One-Way TLS).
     * **Files** : This maps the CA Certificate, Broker Certificate, and Broker's Private Key that Mosquitto requires for TLS.
  8. Start or restart the Mosquitto service to apply the changes.
  9. Open the currently configured MQTT Access Name.
  10. Set the TCP Port to 8883.
  11. Set the Authentication Type to One-Way TLS.
  12. Set the TLS Version to 1.3.
  13. Set Certificate Validation Mode to No Check.  
  
**Certificate Revocation , known as Certificate Validation Mode in TrakSYS**, controls how TrakSYS validates and verifies the broker server's certificate. Choose whether to skip validation and verification entirely, check against local trust stores only for verification, or perform online verification and it will fall back to local trust stores when necessary.  
  
For the purposes of this example, we will set it to No Check to skip the validation and verification.  
  

  14. The final result should look similar to the following:



![](https://portal.parsec-corp.com/hc/article_attachments/40346069251475)

Assuming that all configuration is correct, TrakSYS should now connect to the MQTT Broker using One-Way TLS. If issues in connection are experienced, please reference the MQTT Connection Troubleshooting Guide [here](https://portal.parsec-corp.com/hc/en-us/articles/38862002645011-MQTT-Connection-Troubleshooting-Guide) for troubleshooting suggestions.  
  


### Mutual TLS Configuration

To configure Mutual TLS, Certificates need to be generated for Logic Service. Starting with TrakSYS 13, certificates can now be generated from the Logic Service Instance configuration. This new method allows users to download certificate files in different formats through the TrakSYS Web. Note that as of TrakSYS 13.0.0, this method only applies to Logic Service.

**Note** : The TrakSYS certificate will act as the CA (Certificate Authority) certificate for this example.

  1. Navigate to **Configuration** | **Services** | **Logic Services.**
  2. Select the configured Logic Service instance on the first slice.
  3. Then, click Edit on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39623346605843)  
  

  4. Under the Certificate section, select the certificate lifetime (any value between 1 and 120) and check the Generate Certificate checkbox.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39623388668307)  
  

  5. Start or restart Logic Service.
  6. Go back to the Logic Service Instance. Options for Download and Clear Certificates should now appear in the second slice.
  7. Click the Download Certificate link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39623346609043)  
  

  8. Under the Certificate Type drop down, select the Privacy Enhanced Mail (.pem).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39623388669843)  
  

  9. Click the Download button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39623346612243)  
  

  10. Repeat steps 7 through 9. However, on step 8, select the Private Key (.key) option instead.
  11. The .pem and .key files should be downloaded.
  12. Generate the broker's private key by executing the following command:  
  
`openssl genrsa -out <server_name>.key 2048  
`  
![](https://portal.parsec-corp.com/hc/article_attachments/39981644903827)  
  
The `<server_name>.key` file should now be generated.  
  

  13. Generate a Certificate Signing Request (CSR) for the broker by executing the following command:  
  
`openssl req -new -key <server_name>.key -out <server_name>.csr`  
  
OpenSSL will prompt the user for certificate information. The Common Name will need to be set to the host name that the clients will use to connect to the broker. All other information can be left blank by pressing enter.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39981667438099)  
  
The `<server_name>.csr` file should now be generated.  
  

  14. Generate the broker's certificate and sign it with the CA certificate (TrakSYS Certificate) by executing the following command:  
  
`openssl x509 -req -in <server_name>.csr -CA <ca_cert>.pem -CAkey <ca_cert>.key -CAcreateserial -out <server_name>.pem -days 365`  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40533769838867)  
  
`C:\<server_name>.pem` should now be present.
  15. All of the files should now be generated and should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40533788613651)  
  
For simplicity, the Logic Service .pem, Logic Service .key, <server_name>.pem, and <server_name>.key files will be moved to root folder (C:\\).
  16. Add the following lines within the Mosquitto configuration file (mosquitto.conf)
         
         cafile C:\LogicManager1.pem
         certfile C:\<server_name>.pem
         keyfile C:\<server_name>.key  
         # Leave this uncommented to use anonymous authentication  
         allow_anonymous true  
         # Uncomment this line to use Username and Password authentication instead  
         # allow_anonymous false

  17. Open the currently configured MQTT Access Name.
  18. Set the TCP Port to 8883.
  19. Set the Authentication Type to Mutual TLS.
  20. Set the TLS Version to 1.3.
  21. Set Certificate Validation Mode
  22. The final result should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40346069251731)



Assuming that all configuration is correct, TrakSYS should now connect to the MQTT Broker using Mutual TLS. If experiencing any connection issues, please reference the MQTT Connection Troubleshooting Guide [here](https://portal.parsec-corp.com/hc/en-us/articles/38862002645011-MQTT-Connection-Troubleshooting-Guide).
