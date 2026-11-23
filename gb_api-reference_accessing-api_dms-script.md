# Data Management Service Script

From within Data Management Service Script Module Steps, the `Global.Context.Api` member can be used to access an instantiated and connected `ETS.Core.Api.ApiService` object.

## Examples

The following example is used within the `Execute()` method of a Module Script Step.

<pre class="language-csharp"><code class="lang-csharp">/// ******************************************************************
/// &#x3C;summary>
/// This method is called each time this Step is executed within the Module.
/// This is where the main code for Step execution should be placed.
/// &#x3C;/summary>
/// ******************************************************************
public override bool Execute(IModuleContext ctx)
{
<strong>  ETS.Core.Api.ApiService api = ctx.Api;
</strong>  
  // The API object can now be used
  
  return true;
}
</code></pre>
