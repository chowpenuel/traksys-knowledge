# Script Classes

From within Script Classes, `this.Api` or `Context.Api` can be used to access an instantiated and connected `ETS.Core.Api.ApiService` object. If using a custom class (i.e. one that doesn't inherit from a TrakSYS class), it is preferred to send the `Api` object in as a parameter/property to the class instead of accessing the `Global.Context.Api` object.

## Examples

The following example is used within the `PostScan()` method of a Logic Service Script Class.

<pre class="language-csharp"><code class="lang-csharp">/// ******************************************************************
/// &#x3C;summary>This method is called at the end of each Logic Service scan.&#x3C;/summary>
/// ******************************************************************
public override void PostScan(IPostScanContext context)
{
<strong>  ETS.Core.Api.ApiService api = context.Api;
</strong>  
  // The API object can now be used
}
</code></pre>
