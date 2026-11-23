# TrakSYS Bandwidth and Latency Requirements

*Source: https://portal.parsec-corp.com/hc/en-us/articles/1500002559941-TrakSYS-Bandwidth-and-Latency-Requirements*
*Last updated: 2025-05-21T22:08:47Z*

---

Applies To | TrakSYS 10+

### Introduction

When selecting a TrakSYS architecture and considering deployment to off-premises infrastructure (either in a data center or cloud-hosted), it is important to evaluate performance of the Internet connection between relevant clients and servers. This article describes some of the key communication pathways that should be considered, and their recommended Bandwidth/Latency requirements.

### Bandwidth Requirements

There are 3 main areas to consider when calculating the bandwidth requirements for a TrakSYS implementation. The general formulas and considerations are listed below. Note that these are based on semi-aggressive average measurements. Bandwidth can be complex to calculate precisely, and there are also periods of burst usage that may temporarily exceed these results.

#### OPC UA

For remote implementations, OPC UA is typically used to continuously transport real-time data from the site to the TrakSYS servers. The OPC server is typically located on-premises and configured to send messages to the TrakSYS servers whenever monitored automation data points (Tags) change value.

When Tag values change, the OPC server bundles all new values into a single message and broadcasts it to the TrakSYS server for processing. The size and quantity of the messages are dependent on several factors including number of Tag changes, frequency of Tag changes, and data types of the Tag values.

The following calculation can be used to estimate bandwidth in kilobytes-per-second, b, for OPC UA communication:

[![](https://latex.codecogs.com/gif.latex?b_{opcua}\\text{&space;}\(KB/s\)&space;=&space;\\frac{\\varsigma_{m}&space;*&space;\\nu_{m}}{60\\text{&space;}s/min})](https://www.codecogs.com/eqnedit.php?latex=b_{opcua}\\text{&space;}\(KB/s\)&space;=&space;\\frac{\\varsigma_{m}&space;*&space;\\nu_{m}}{60\\text{&space;}s/min})

where

[![](https://latex.codecogs.com/gif.latex?\\varsigma_{m}&space;=&space;message\\text{&space;}size\\text{&space;}\(kilobytes\))](https://www.codecogs.com/eqnedit.php?latex=\\varsigma_{m}&space;=&space;message\\text{&space;}size\\text{&space;}\(kilobytes\))

[![](https://latex.codecogs.com/gif.latex?\\nu_{m}&space;=&space;message\\text{&space;}frequency\\text{&space;}\(messages/min\))](https://www.codecogs.com/eqnedit.php?latex=\\nu_{m}&space;=&space;message\\text{&space;}frequency\\text{&space;}\(messages/min\))

and

[![](https://latex.codecogs.com/gif.latex?\\varsigma_{m}\\text{&space;}\(KB\)&space;=&space;\\frac{m_{h}&space;+&space;\(2bpc*\\delta&space;_{d}\)&space;+&space;\(8bpc*\\delta&space;_{a}\)}{1024\\text{&space;}bytes/KB})](https://www.codecogs.com/eqnedit.php?latex=\\varsigma_{m}\\text{&space;}\(KB\)&space;=&space;\\frac{m_{h}&space;+&space;\(2bpc*\\delta&space;_{d}\)&space;+&space;\(8bpc*\\delta&space;_{a}\)}{1024\\text{&space;}bytes/KB})

where

[![](https://latex.codecogs.com/gif.latex?m_{h}&space;=&space;message\\text{&space;}header\\text{&space;}\(constant\\text{&space;}14\\text{&space;}bytes/message\))](https://www.codecogs.com/eqnedit.php?latex=m_{h}&space;=&space;message\\text{&space;}header\\text{&space;}\(constant\\text{&space;}14\\text{&space;}bytes/message\))

[![](https://latex.codecogs.com/gif.latex?bpc&space;=&space;bytes/count)](https://www.codecogs.com/eqnedit.php?latex=bpc&space;=&space;bytes/count)

[![](https://latex.codecogs.com/gif.latex?\\delta&space;_{d}&space;=&space;digital\\text{&space;}values\\text{&space;}change\\text{&space;}count)](https://www.codecogs.com/eqnedit.php?latex=\\delta&space;_{d}&space;=&space;digital\\text{&space;}values\\text{&space;}change\\text{&space;}count)

[![](https://latex.codecogs.com/gif.latex?\\delta&space;_{a}&space;=&space;analog\\text{&space;}values\\text{&space;}change\\text{&space;}count)](https://www.codecogs.com/eqnedit.php?latex=\\delta&space;_{a}&space;=&space;analog\\text{&space;}values\\text{&space;}change\\text{&space;}count)

For this calculation, message frequency, digital values change count, and analog values change count will depend entirely on the implementation as they will be a function of how many configured Tags are changing and how often.

**Example**

The required OPC UA bandwidth for an implementation having 100 digital values and 100 analog values changing per message at a rate of 60 messages per minute would be calculated as follows:

[![](https://latex.codecogs.com/gif.latex?b_{opcua}\\text{&space;}\(KB/s\)&space;=&space;\\left&space;\(&space;\\frac{14\\text{&space;}bytes/message&space;+&space;\(2bpc*100\\text{&space;}counts\)&space;+&space;\(8bpc*100\\text{&space;}counts\)}{1024\\text{&space;}bytes/KB}&space;\\right&space;\)\\left&space;\(&space;\\frac{60\\text{&space;}messages/min}{60\\text{&space;}s/min}&space;\\right&space;\))](https://www.codecogs.com/eqnedit.php?latex=b_{opcua}\\text{&space;}\(KB/s\)&space;=&space;\\left&space;\(&space;\\frac{14\\text{&space;}bytes/message&space;+&space;\(2bpc*100\\text{&space;}counts\)&space;+&space;\(8bpc*100\\text{&space;}counts\)}{1024\\text{&space;}bytes/KB}&space;\\right&space;\)\\left&space;\(&space;\\frac{60\\text{&space;}messages/min}{60\\text{&space;}s/min}&space;\\right&space;\))

resulting in a calculated bandwidth requirement of **0.99 KB/s**. 

#### TrakSYS Smart Devices

As an alternative to using OPC UA, TrakSYS Smart Devices connect off-the-shelf sensors to the TrakSYS server using a fast and lightweight protocol. On premises, Smart Data Collectors with sensors send changing values to a Smart Coordinator, which passes them onto the TrakSYS server via a web service call. The size and quantity of the messages are dependent on several factors including number of Data Collectors and frequency of Tag changes.

The following calculation can be used to estimate bandwidth in kilobytes-per-second, b, for TrakSYS Smart Devices communication:

[![](https://latex.codecogs.com/gif.latex?b_{sd}\\text{&space;}\(KB/s\)&space;=&space;\(\\mu&space;_s_d\)\\left&space;\(&space;\\frac{\\varsigma_{m}&space;*&space;\\nu_{m}}{60\\text{&space;}s/min}&space;\\right&space;\))](https://www.codecogs.com/eqnedit.php?latex=b_{sd}\\text{&space;}\(KB/s\)&space;=&space;\(\\mu&space;_s_d\)\\left&space;\(&space;\\frac{\\varsigma_{m}&space;*&space;\\nu_{m}}{60\\text{&space;}s/min}&space;\\right&space;\))

where

[![](https://latex.codecogs.com/gif.latex?\\mu_{sd}&space;=&space;total\\text{&space;}data\\text{&space;}collector\\text{&space;}units)](https://www.codecogs.com/eqnedit.php?latex=\\mu_{sd}&space;=&space;total\\text{&space;}data\\text{&space;}collector\\text{&space;}units)

[![](https://latex.codecogs.com/gif.latex?\\varsigma_{m}&space;=&space;message\\text{&space;}size\\text{&space;}\(constant\\text{&space;}2.46\\text{&space;}kilobytes\))](https://www.codecogs.com/eqnedit.php?latex=\\varsigma_{m}&space;=&space;message\\text{&space;}size\\text{&space;}\(constant\\text{&space;}2.46\\text{&space;}kilobytes\))

[![](https://latex.codecogs.com/gif.latex?\\nu_{m}&space;=&space;message\\text{&space;}frequency\\text{&space;}\(messages/min\))](https://www.codecogs.com/eqnedit.php?latex=\\nu_{m}&space;=&space;message\\text{&space;}frequency\\text{&space;}\(messages/min\))

For this calculation, message frequency will depend entirely on the implementation as it will be a function of how many configured Tags are changing and how often. Similarly, the number of installed Data Collectors will also depend on the nature of the implementation.

**Example**

The required Smart Devices bandwidth for an implementation having 1 Data Collector sending updates at a rate of 60 messages per minute would be calculated as follows:

[![](https://latex.codecogs.com/gif.latex?b_{sd}\\text{&space;}\(KB/s\)&space;=&space;\(1\)\\left&space;\(&space;\\frac{2.46\\text{&space;}KB/message&space;*&space;60\\text{&space;}messages/min}{60\\text{&space;}s/min}&space;\\right&space;\))](https://www.codecogs.com/eqnedit.php?latex=b_{sd}\\text{&space;}\(KB/s\)&space;=&space;\(1\)\\left&space;\(&space;\\frac{2.46\\text{&space;}KB/message&space;*&space;60\\text{&space;}messages/min}{60\\text{&space;}s/min}&space;\\right&space;\))

resulting in a calculated bandwidth requirement of **2.46 KB/s**. 

#### TS Web User Interaction

Regular user interaction via the TS Web application is a significant part of TrakSYS implementations. The TS Web serves all users including real-time operations, data entry, dashboards, reporting, analytics, and configuration.

The frequency of page requests is dependent on several factors including the type and number of concurrent users (Casual vs. Active). In this context, a Casual user is defined as one that is not utilizing the TS Web application continuously in given period (e.g. non-operator personnel viewing only a few reports at the end of a shift). An Active user is defined as one that utilizes the TS Web on an on-going basis throughout a given period (e.g. an overhead display with refreshing screens on the plant floor).

By definition, an Active user will make page requests at a much higher rate. A typical Casual user page request rate could be 5 pages per hour whereas an Active user page request rate could be 300 pages per hour.

The following calculation can be used to estimate bandwidth in kilobytes-per-second, b, for different types of TS Web users:

[![](https://latex.codecogs.com/gif.latex?b_{tsweb}\\text{&space;}\(KB/s\)&space;=&space;\\frac{\\varsigma&space;_{p}&space;*&space;\(\(\\mu_{c}*\\delta_{c}\)&space;+&space;\(\\mu_{a}*\\delta_{a}\)\)}{3600\\text{&space;}s/hr})](https://www.codecogs.com/eqnedit.php?latex=b_{tsweb}\\text{&space;}\(KB/s\)&space;=&space;\\frac{\\varsigma&space;_{p}&space;*&space;\(\(\\mu_{c}*\\delta_{c}\)&space;+&space;\(\\mu_{a}*\\delta_{a}\)\)}{3600\\text{&space;}s/hr})

where

[![](https://latex.codecogs.com/gif.latex?\\varsigma&space;_{p}&space;=&space;average\\text{&space;}page\\text{&space;}size\\text{&space;}\(\\sim&space;300\\text{&space;}KB\))](https://www.codecogs.com/eqnedit.php?latex=\\varsigma&space;_{p}&space;=&space;average\\text{&space;}page\\text{&space;}size\\text{&space;}\(\\sim&space;300\\text{&space;}KB\))

[![](https://latex.codecogs.com/gif.latex?\\mu_{c}&space;=&space;total\\text{&space;}concurrent\\text{&space;}casual\\text{&space;}users\\text{&space;})](https://www.codecogs.com/eqnedit.php?latex=\\mu_{c}&space;=&space;total\\text{&space;}concurrent\\text{&space;}casual\\text{&space;}users\\text{&space;})

[![](https://latex.codecogs.com/gif.latex?\\delta_{c}&space;=&space;concurrent\\text{&space;}casual\\text{&space;}user\\text{&space;}page\\text{&space;}request\\text{&space;}rate\\text{&space;}\(pages/hr\))](https://www.codecogs.com/eqnedit.php?latex=\\delta_{c}&space;=&space;concurrent\\text{&space;}casual\\text{&space;}user\\text{&space;}page\\text{&space;}request\\text{&space;}rate\\text{&space;}\(pages/hr\))

[![](https://latex.codecogs.com/gif.latex?\\mu_{a}&space;=&space;total\\text{&space;}concurrent\\text{&space;}active\\text{&space;}users\\text{&space;})](https://www.codecogs.com/eqnedit.php?latex=\\mu_{a}&space;=&space;total\\text{&space;}concurrent\\text{&space;}active\\text{&space;}users\\text{&space;})

[![](https://latex.codecogs.com/gif.latex?\\delta_{a}&space;=&space;concurrent\\text{&space;}active\\text{&space;}user\\text{&space;}page\\text{&space;}request\\text{&space;}rate\\text{&space;}\(pages/hr\))](https://www.codecogs.com/eqnedit.php?latex=\\delta_{a}&space;=&space;concurrent\\text{&space;}active\\text{&space;}user\\text{&space;}page\\text{&space;}request\\text{&space;}rate\\text{&space;}\(pages/hr\))

For this calculation, the number of users, their type, and their page request rates will depend entirely on the implementation as they will be a function of how many users are configured and how active each one is in terms of TS Web application use.

**Example**

The required TS Web bandwidth for an implementation having 1 Casual user making requests at 5 pages/hr, and 1 Active user making requests at 300 pages/hr would be calculated as follows:

[![](https://latex.codecogs.com/gif.latex?b_{tsweb}\\text{&space;}\(KB/s\)&space;=&space;\\frac{300\\text{&space;}KB/page&space;*&space;\(\(1&space;*&space;5\\text{&space;}pages/hr\)&space;+&space;\(1&space;*&space;300\\text{&space;}pages/hr\)\)}{3600\\text{&space;}s/hr})](https://www.codecogs.com/eqnedit.php?latex=b_{tsweb}\\text{&space;}\(KB/s\)&space;=&space;\\frac{300\\text{&space;}KB/page&space;*&space;\(\(1&space;*&space;5\\text{&space;}pages/hr\)&space;+&space;\(1&space;*&space;300\\text{&space;}pages/hr\)\)}{3600\\text{&space;}s/hr})

resulting in a calculated bandwidth requirement of **25.42 KB/s**. 

### Latency Requirements

In addition to bandwidth requirement considerations, poor (high) network latency can also have a negative effect on data collection and user-interface experience. As latency increases, requests for TS Web pages and other user-interface interactions will begin to "feel" sluggish as a noticeable delay occurs between a request and response. Note that a single page request is typically made of tens of individual server requests for scripts, CSS, images, etc. As a result, high latency will have a compounding effect on each of these transfers.

As a rule of thumb, network latency of less than 100 milliseconds (ms) will provide a normal browsing experience. Sub-100ms is also sufficient for most data-collection scenarios, as TrakSYS timestamps are typically rounded to the nearest second. However, if very specialized historian solutions that rely on accurate sub-second timestamps are being deployed, then the latency requirements should be adjusted accordingly.
