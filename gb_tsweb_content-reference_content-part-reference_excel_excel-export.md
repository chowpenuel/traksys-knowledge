# Excel Export

The Excel Export part allows for Values based data sources to be injected into a blank or pre-uploaded Excel file. After the data is inserted, the new Excel file is returned to the user's browser for download/saving.

## General

### Save As File Name

Specifies the file name that will be used (by default) when the user is prompted to save the file in their browser.

### Source Excel URL

Specifies the source URL for the Excel template to be used to inject data into. Note that the source file is not altered, rather a copy is taken before data is inserted and returned to the user. If this property is left blank, an empty Excel spreadsheet is used for the target of data insertion.

### Enabled

When True, this part executes, injecting the specified data into the specified Excel file and returning it to the user. When False, this part is dormant. The typical use is to embed this part on visual page or report with an "Export to Excel" button. When the export button is clicked, the browser is re-directed to the current page, passing in an "Export=1" variable on the QueryString. This property is mapped to the "Export" Values Dictionary entry. Upon clicking the export button, the page is re-run this time activating the export functionality.

## Data

### Set 1 - 20

Each Set below contains properties that control how a single Values based dataset is injected and mapped to the target Excel file.

### Set 1 - 20 | Enabled

Specifies if this Set is used. When False, the properties beneath this Set do nothing.

### Set 1 - 20 | Source Values Key

Specifies the Values Dictionary Key used to retrieve the dataset that will be used for this Set. The Values Dictionary item specified must contain either a .NET DataSet or DataReader object, or an IEnumerable list of objects.

### Set 1 - 20 | Target Location

Specifies an Excel sheet cell location where the source dataset will be inserted. The cell syntax is `<sheet name>!<column><row>` (for example Sheet1!B2). The specified cell will represent the top-left corner of the dataset.

### Set 1 - 20 | Include Table Header

When Yes, the column headers for the dataset will be included and inserted on the Excel sheet as the first row of the dataset.

### Set 1 - 20 | Include and Shift Down

When Yes, any content below or to the right of the Target Location cell will be shifted down (and right) based on the size of the dataset. When False, the dataset will overwrite the contents of any cells it covers.

## Advanced

### CSS Class

Any CSS class values added to this property will be rendered to the part's HTML. While the CSS is typically rendered to an outer DIV element, the exact HTML element that this CSS is added to is part specific.

### Visible

When false, this part will NOT be rendered to the browser. For most visual parts, this means that any processing (Values Dictionary manipulation, data retrieval, etc...) will not be executed. For Data Table parts, setting the Visible to false will still allow the part to execute its query and place its resultant dataset in the Values dictionary, however any visual debugging elements will not be rendered.

### Initialization Order

Indicates the order that this part will be loaded and executed on the containing page. This value also indicates which script method (ContentPage\_PartPreInitXX) should be used to initialize properties just before the part is loaded. If this property is left blank, each part will load using its own default Initialization Order.

### Initialization Order Sub

Indicates the order that this part will be loaded and executed on the containing page. This property value is used in conjunction with the Initialization Order value to create the final load sequence (the Initialization Order Sub value is used as a decimal value added to the Initialization Order). For example if the Initialization Order is 3 and the Order Sub is 2, the actual load order would be 3.2.

If this property is left blank, each part will load using its own default Initialization Order Sub (typically 1).
