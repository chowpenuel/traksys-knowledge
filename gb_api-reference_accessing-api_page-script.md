# Page Script

From the code-behind script of the ASP.NET Page or Part, the page contains an `Ets.Api` (`this.Ets.Api`) member to access an instantiated and connected `ETS.Core.Api.ApiService` object.

## Examples

The following example is used in the `ContentPage_Init()` method of the C# Page Script for a Visual Page Definition.

<pre class="language-csharp"><code class="lang-csharp">/// ***********************************************************
/// &#x3C;remarks>
/// All Page level ContentProperties have been set from default
/// values or Ets.Values. Content Parts are not yet loaded/initialized.
///
/// Do things like:
///   Check Page Permissions
///   Set Resource Strings
/// &#x3C;/remarks>
/// ***********************************************************
protected override bool ContentPage_Init()
{
<strong>  ETS.Core.Api.ApiService api = this.Ets.Api;
</strong>  
  // The API object can now be used.
  
  return true;
}
</code></pre>
