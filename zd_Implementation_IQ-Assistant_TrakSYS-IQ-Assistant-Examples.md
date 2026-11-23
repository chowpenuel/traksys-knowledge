# TrakSYS IQ Assistant Examples

*Source: https://portal.parsec-corp.com/hc/en-us/articles/45161626972307-TrakSYS-IQ-Assistant-Examples*
*Last updated: 2026-02-23T19:40:46Z*

---

### Summary

This article provides multiple examples demonstrating how TrakSYS IQ Assistant can be used to retrieve and present data effectively. The examples illustrate practical scenarios, such as diagnosing low performance for a specific System or production line, and assisting with tasks like retrieving and presenting information related to a product recall. Additional examples show how data can be visualized using charts and tables, which can be generated and modified through prompts submitted to TrakSYS IQ Assistant.

**Note** : The examples below assume that TrakSYS IQ Assistant has been fully configured as mentioned [**here**](https://portal.parsec-corp.com/hc/en-us/articles/44857917808275-Configuring-TrakSYS-IQ).

### Retrieving Data

TrakSYS IQ Assistant provides the ability to retrieve and aggregate a wide range of data for reporting purposes. It can also assist with investigating impacts to metrics and can provide recommendations. 

#### Investigating Low Performance for a Packaging Line

The example scenarios below provide demonstrations of how data can be retrieved and summarized for reporting and analysis purposes. The prompts in this scenario will retrieve data and information for a Packaging Line that has lower than expected OEE metric values.

To begin this example, a prompt has been given to return the overall KPI of a particular System for the last month. Note that if multiple entities of the same type (such as Systems) within TrakSYS have the same names, additional information such as Key or ID may need to be included in the prompt to help identify the correct entity.

![](https://portal.parsec-corp.com/hc/article_attachments/45447832213395)

The response gives the full aggregate results for the line and points out significant Metrics that have the most impact on the calculations.

![](https://portal.parsec-corp.com/hc/article_attachments/45447832217491)![](https://portal.parsec-corp.com/hc/article_attachments/45447865453459)

Furthermore, a conclusion is presented with some key, human-readable observations regarding the metrics and aggregated data.

![](https://portal.parsec-corp.com/hc/article_attachments/45447832222867)

Now that this data has been generated, it can be referenced for further prompts. Additionally, that context can be used to reference data related to the presented metrics. The prompt below further narrows the scope by asking about specific Jobs.

![](https://portal.parsec-corp.com/hc/article_attachments/45447832223891)

Along with this data, it also gives key observations and suggestions as to why these particular Jobs had low performance.

![](https://portal.parsec-corp.com/hc/article_attachments/45447865463699)

To further this investigation, data about other related entities can also be retrieved and analyzed. One of the major factors to OEE and the related metrics is Events. A large number of Events or Events with significant durations can negatively impact OEE metrics. Therefore, the prompt below asks for a summary of the Availability Loss Events that occurred during this period of time.

![](https://portal.parsec-corp.com/hc/article_attachments/45449604613907)

TrakSYS IQ Assistant gives the top 3 Event Definitions that generated the most amount of time during the full month period.

![](https://portal.parsec-corp.com/hc/article_attachments/45449616099987)

It further breaks down this information by providing individual Event entries that had the most impact. It also provides some observations as an overall summary.

![](https://portal.parsec-corp.com/hc/article_attachments/45449616102291)

Along with the local TrakSYS information, TrakSYS IQ Assistant can pull from outside information to provide additional context. For this example, information is being provided for a Packaging Line for a fictitious Pharmaceutical Company. Prompts can be generated to compare data against generally known metrics. In the example prompt below, the current OEE metrics are compared against the Pharmaceutical Industry.

![](https://portal.parsec-corp.com/hc/article_attachments/45449604623123)

TrakSYS IQ Assistant gives the Metrics for the current System and provides general ranges for the pharmaceutical industry.

![](https://portal.parsec-corp.com/hc/article_attachments/45450505837075)

It further expands on this data by providing comparisons and insights.

![](https://portal.parsec-corp.com/hc/article_attachments/45450510440723)

Based on this information, it gives suggestions on how to improve the OEE metrics and gives a final conclusion on the findings.

![](https://portal.parsec-corp.com/hc/article_attachments/45450510442259)

####    
Investigating a Product Recall

Using the configuration and data from the previous example, this scenario demonstrates a series of prompts designed to gather information related to a product recall. The prompts progress from a high-level overview and gradually drill down to specific entities to identify the exact batch of affected products.

**Note:** For this example, a new thread was created for the same IQ Assistant. It is recommended to create new threads for unrelated topics, as new threads do not pull information from previous ones. Using a single thread for multiple, unrelated topics may affect or skew the responses for newer prompts based on earlier interactions.

To start the example, a prompt was given to retrieve the Material Code for a configured Product.

![](https://portal.parsec-corp.com/hc/article_attachments/45457845815699)

Now that the Material Code is known, production data using that Material can be retrieved. In the example below, the prompt now asks for the Lots that were consumed by this specific Material. Note that for prompts like this, it is recommended to specify a Date or Date/Time range to help filter the results. This can also help speed up the response times for a given prompt.

![](https://portal.parsec-corp.com/hc/article_attachments/45457845818259)

Now that the list of Lots has been given, it is possible to filter further data as needed. The next prompt asks for the orders that consumed a specific Lot.

![](https://portal.parsec-corp.com/hc/article_attachments/45457845818771)

Additional information for the specific Jobs can be given to help refine the results. This practice is normally recommended for queries that may generate a very large number of entries. In this case, TrakSYS IQ Assistant is being prompted again to regenerate the data with additional information.

![](https://portal.parsec-corp.com/hc/article_attachments/45457870562067)

For this scenario, the user now has the Product, Material, Lot, and Jobs needed to take action. As mentioned in the previous example, TrakSYS IQ Assistant can pull from outside information to provide additional context or perform additional actions under the context of the queried information. For the following prompt, the user is creating an email draft to their Quality Manager summarizing the data related to the product recall.

![](https://portal.parsec-corp.com/hc/article_attachments/45457870565523)![](https://portal.parsec-corp.com/hc/article_attachments/45457870566931)

### Using and Customizing Charts

TrakSYS IQ Assistant provides the ability to display data in the form of graphs and charts. The charts are created from the chart.js library, which is already included in the TrakSYS software. This same library is used for the built-in JavaScript Interactive charts. Depending on the user prompt, charts can be customized to adjust colors, styles, text, limit lines, and other visual elements. The full list of supported charts can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/44857917808275). The full documentation for the Chart.js library (v2.9.4) can be found [**here**](https://www.chartjs.org/docs/2.9.4/).

**Note** : TrakSYS IQ Assistant may have limitations when customizing certain aspects of generated charts. This includes actions such as adding data value labels, resizing charts, adjusting bar width, and modifying bar spacing.

The following example demonstrates a sequence of prompts that show how data can be presented and manipulated using charts in TrakSYS IQ Assistant. Results may vary depending on the specific wording of the prompts and the data available.

To start the example, a prompt is used to retrieve the last 10 jobs completed on a specific System.

![](https://portal.parsec-corp.com/hc/article_attachments/45459209392531)![](https://portal.parsec-corp.com/hc/article_attachments/45459133007635)

Now that data has been generated, additional prompts can be used to generate charts under the context of the data set. The next prompt instructs TrakSYS IQ Assistant to display this information on a Bar Chart in chronological order and what should be plotted. Note that further information can be included in the prompt to further customize the chart. More specific instructions can usually yield better results.

![](https://portal.parsec-corp.com/hc/article_attachments/45459209394835)

Now that a chart has been generated, it is possible to further customize it as needed. For example, an instruction has been given to apply the color red to a specific Bar.

![](https://portal.parsec-corp.com/hc/article_attachments/45459209400851)

Depending on the chart used, it is possible to draw limit lines or place other objects on the chart. In the prompt below, a limit line has been inserted on the Y-Axis.

![](https://portal.parsec-corp.com/hc/article_attachments/45459133009683)

Because the previous prompt was not specific enough, a different color red was used for the limit line versus what was used to color the bar on the chart. Therefore, the following prompt was used to help further clarify.

![](https://portal.parsec-corp.com/hc/article_attachments/45459133011475)

While elements can be added to the chart, they can also be removed. In the example below, the prompt instructs TrakSYS IQ Assistant to remove the chart legend.

![](https://portal.parsec-corp.com/hc/article_attachments/45459209404947)

Additionally, existing elements can be modified as needed. The prompt below provides specific instructions to change the X-Axis label name.

![](https://portal.parsec-corp.com/hc/article_attachments/45459209406099)

From here, the chart can be further modified, or an entirely new chart can be generated using the same data. Once the desired chart has been generated, it is possible to view the source code that was used to create the chart. This can be useful for troubleshooting purposes or to make small, detailed modifications the further customize the chart. To see the source code of a specific chart, click the informational (i) icon typically at the top right corner of the chart.

![](https://portal.parsec-corp.com/hc/article_attachments/45475112157075)

This will reveal additional information about the chart and the specific response. Depending on the response, this menu can contain the original prompt, the time it took to generate the response, the SQL query used to generate the response, and more. On that menu, click the Chart link at the top right corner.

![](https://portal.parsec-corp.com/hc/article_attachments/45475145175955)

This will redirect the user to the IQ Assistant Chart Tool. The first slice shows the raw code used to generate the chart (in JSON format). The code can be manually modified to change the data and behavior of the chart. The Execute button above the editor will apply the code changes and display the final output in the second slice of the page.

![](https://portal.parsec-corp.com/hc/article_attachments/45475145178899)

Once the chart has been fully customized, the user can click the "Copy Chart" link on the top right corner of the second slice. This is useful for transferring the chart to external sources for reports, presentations, and more.

![](https://portal.parsec-corp.com/hc/article_attachments/45475112161171)

### Using and Customizing Tables

TrakSYS IQ Assistant also supports displaying data in table format. Tables and their contents can be modified through prompts to achieve the desired presentation. Customizations include operations such as sorting, filtering, adding or removing rows, adjusting font size, changing colors, and more.

**Note:** Tables rendered in chat by TrakSYS IQ Assistant are generated using Markdown. Customization options are therefore limited by Markdown capabilities. Certain styling adjustments, such as changing colors, font sizes, or applying HTML/CSS formatting, may not be possible for rendered tables.

The following example demonstrates a sequence of prompts showing how data can be presented and manipulated in tables using TrakSYS IQ Assistant. Results may vary depending on the specific wording of the prompts and the available data.

To begin the example, a prompt was given to get the total number of events and the aggregated downtime per day. This will be used as the dataset for the table.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45475588931859)

![](https://portal.parsec-corp.com/hc/article_attachments/45475588933011)

The next prompt instructs TrakSYS IQ Assistant to display this information in a table ordered by the Date in ascending order. While the prompt used is simplistic, more information can be provided to further customize the chart. Generally, more specific instructions can yield better results.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45475572707347)

Once the table has been generated, it is possible to further customize the look and behavior. For example, the prompt below changes the structure of the table.  


![](https://portal.parsec-corp.com/hc/article_attachments/45475572708499)

Furthermore, it is possible to modify the content of the table based on specific conditions (within the limitations of the Markdown language). The next prompt bolds all rows above 7 hours.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45475572709651)

![](https://portal.parsec-corp.com/hc/article_attachments/45475588936979)

Finally, the data itself can also be modified even after the table has been created. Specific conditions can also be applied to these types of operations. In the example below, the prompt instructs TrakSYS IQ Assistant to remove all rows that have less than 25 events.

![](https://portal.parsec-corp.com/hc/article_attachments/45475588937619)
