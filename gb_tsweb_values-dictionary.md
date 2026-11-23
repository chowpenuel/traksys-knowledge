# Values Dictionary

The Values Dictionary, alternatively referred to as Values, ETS.Values, or the Values Collection is a repository for holding variables during page execution as a means of decoupling Content Parts. Values can be passed into a Page, created or manipulated on a Page, and passed on from a Page.

## Loading Values

Values are cleared and rebuilt on every Page GET and POST (refresh). The Dictionary is populated automatically by the TrakSYS infrastructure in the following order:

* Site
* Section
* Hub 1
* Hub 2
* Hub 3
* Spokes
* Session
* QueryString
* Form
* Page and Parts direct Loading

{% hint style="info" %}
As Values are loaded, existing Values are overwritten if the same Key already exists in the Dictionary.
{% endhint %}

## Writing Values

### QueryString

Values may be passed to the Page via the QueryString. For example: `http://localhost/ts/pages/ocv?SystemID=3`.

### Form POST

During a Form POST (e.g. - clicking Save on a form), Values are written to the Dictionary with the Form Key of each Content Part.

### ASP .NET Script

Values may be added to the Dictionary using ASP .NET Script in a Page's code behind, or Script. For example:

* `this.Ets.Values["SystemID"] = 3; // adds or overwrites`
* `this.Ets.Values.ContainsKey("SystemID"); // check if exists`

### Page Values

Values may be added to the Dictionary using the Values Editor of a Page Definition. See the Page Definition [Page Values topic](page-definitions/page-values).

## Reading Values

### Expressions

Most Standard Content Page and Standard Content Part Properties accept Expressions, including Property Fields with the Script Icon (\</>) or those with the small Key icon.

#### Basic Syntax

The basic expression syntax is Curly Braces around the desired Values Dictionary Key (e.g. - `{SystemID}`).

#### Formatting

Furthermore, a formatting suffix can be added to Expression using .NET Format Codes (i.e. - `{Key:FormatCode}`). In this example, the number value will be formatted with a single digit after the decimal point:

* `{Data.Quantity:N1}`

#### Default Values

Default Values can be provided within the Values Expression to handle cases when the Value is not present in the Dictionary. Defaults can be provided using Square Brackets immediately after the Values Key. For example:

* `{SystemID[-1]}`

#### Format and Default Value

Formatting and Default Value Expressions can be used in conjunction with one another. The Default Value always comes before the Formatting. For example:

* `{Number[0]:N1}`

### ASP .NET Script

Values can also be retrieved from the Dictionary in ASP .NET Script. For example:

* `int value = this.Ets.Values.GetAsInt("SystemID",-1);`
* `string value = this.Ets.Values.GetAsString("Name","");`

## Tracing

Enabling the ASP .NET Trace (using either the Eyeball icon in the Footer or using `&Trace=1` on the QueryString) displays the contents of the Values Dictionary in its entirety, which is often helpful when attempting to debug an issue.
