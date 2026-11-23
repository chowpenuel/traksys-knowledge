# Exporting Pages to PDF

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360051910014-Exporting-Pages-to-PDF*
*Last updated: 2025-05-21T22:43:27Z*

---

Applies To | TrakSYS 11.1.1+

**Summary**

Starting in TrakSYS 11.1.1, TrakSYS Web pages can be exported to PDF. This feature can be useful for creating copies of a report for a specific period in time and for situations where it may be desirable to print a report. This functionality also has additional options that can be used to customize the formatting for the export process.

This functionality does not rely on one specific part or page, allowing users to export any page within the TrakSYS Web (e.g. Custom Visual Pages, Built-in Content Pages, Custom Content Pages, and built-in Configuration Pages). This article explains how to export a page to PDF and leverage the additional options to customize the formatting.

**Important**

TrakSYS 11 features an automatic "dimmed" splash screen that is displayed whenever page navigation response exceeds a minimum duration. When creating PDF export URLs as described below, `ets.ui.cancelLoadingScreen()` should be called on the client click in order to prevent Auto Splash and avoid undesirable behavior.

**Procedure**

To export a TrakSYS page to PDF, add **`ts_pdf=1`** to the URL of the page via the querystring. The export will not work if this parameter is only in the Values Dictionary. The following URL illustrates how to properly export a report:
    
    
    http://ServerName/TS/pages/home/myreport/**?ts_pdf=1**

If other parameters are present in the querystring, the PDF parameter can be added to these by using an ampersand (&) as shown in the following example:
    
    
    http://ServerName/TS/pages/home/myreport/?systemid=87&jobid=107**& ts_pdf=1  
    **

**Export Options**

The following options are available to further customize the file and format for the export process. All of the listed parameters can be used on the querystring or in the Values Dictionary.

The **`ts_pdf_filename`** option sets the file name of the exported PDF document. The example URL below defines the file name as "KPIReport.pdf."
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_filename=KPIReport.pdf**

The **`ts_pdf_orientation`** option sets the orientation of the file. Options include "L" for Landscape or "P" for Portrait. The example URLs below show both options.
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_orientation=P**

Or
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_orientation=L**

The **`ts_pdf_margins_in` **option sets the margins of the report in inches. The example URL below sets 1-inch margins for all sides of the document.
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_margins_in=1,1,1,1**

The **`ts_pdf_margins_cm`** option sets the margins of the report in centimeters. The example URL below sets 2-centimeter margins for all sides of the document.
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_margins_cm=2,2,2,2**

The **`ts_pdf_margins_pt`****** option sets the margins of the report in points. The example URL below sets 72-point margins for all sides of the document.
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_margins_pt=72,72,72,72**

**For TrakSYS 11.2.2+**

The **`ts_pdf_pagesize`** option sets the size of the file. The example URL below sets the page size to A4.
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_pagesize=A4**

The following values can be used for this parameter:

  * A1
  * A2
  * A3
  * A4
  * A5
  * Letter
  * HalfLetter
  * Ledger
  * Legal



The `**ts_pdf_maxpageloadtime**` option sets the timeout of the PDF export process. The default timeout value for this property is set to 60 seconds. The example URL below sets the timeout to 90 seconds.
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_maxpageloadtime=90**

**Note** : Greatly increasing the maximum timeout will not increase the timeout for other web elements. For example, if the timeout is greater than the [code execution timeout](https://portal.parsec-corp.com/hc/en-us/articles/6824879411731-Programmatically-Increasing-Page-Timeout), then the page will timeout anyway due to that limitation. Therefore, all timeouts that apply to this process must be increased to the user-specified value.

The `**ts_pdf_minpageloadtime**` option sets the amount of time that the PDF export process will wait until attempting to export the page. The default timeout value for this property is 2 seconds. The example URL below sets the timeout to 10 seconds.
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_minpageloadtime=10**

The `**ts_pdf_showfooterpagenumbers**` option will display the current page number along with the total number of pages at the footer of the PDF document. The text will always appear with centered alignment. A value of 1 should be included with this parameter to enable this functionality. An example of this is shown below.
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_showfooterpagenumbers=1**

The `**ts_pdf_webpagewidth**` option attempts to match the approximate width in which the web page should be rendered. If this parameter is not specified, its default value is 1280px. The example URL below sets this value to 1000px.
    
    
    http://ServerName/TS/pages/home/myreport/?ts_pdf=1**& ts_pdf_webpagewidth=1000**
