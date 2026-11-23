# Creating a Custom Content Part

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360003914114-Creating-a-Custom-Content-Part*
*Last updated: 2025-05-21T22:52:27Z*

---

Applies To | TrakSYS 10+

### **Summary**

It's possible that while you are in the midst of building a custom Visual Page Definition, some project requirements will call for capabilities that are outside the scope of the built-in Content Parts. In these cases, a custom Content Part can be developed to not only fulfill the project requirements on that page but to also create a re-usable part for other pages.

The example below depicts how to create a custom Tile part (based on a built-in Tile Content Part). The primary difference between this custom Tile and the Tile that's built in is that the custom Tile changes color based on certain limits.

The following steps should serve as a tutorial for general guidance when developing your own custom content part.

### **Procedure**

From within the TS Web interface, navigate to **Developer | Content | Parts** and create a Content Part Group as well as the Content Part Definition.

![](https://portal.parsec-corp.com/hc/article_attachments/18994574291219)

To ease the development of the View script, you have the option of borrowing the HTML from an existing part by adding the existing part to a Visual Page Definition:

![](https://portal.parsec-corp.com/hc/article_attachments/18994703273491)

After viewing the page, leverage the DOM Explorer in the browser's Developer Tools (F12) to extrapolate the HTML from the existing part.

![](https://portal.parsec-corp.com/hc/article_attachments/18994764927379)

Copy the HTML from the existing part into the View script of the Content Part.

![](https://portal.parsec-corp.com/hc/article_attachments/18994825593107)

Two pieces of code can already be made more dynamic within our fledgling HTML: (1) Replace the hardcoded ID ("Part0" in this case) with a variable that will contain the actual client ID from the Part Editor and (2) replace the hardcoded CSS classes with a method which will return a list of CSS classes (more details will be given on the **`RootCss`** method in a later step): 
    
    
    <%@ Control Language="C#" AutoEventWireup="true" 
    Inherits="ETS.Ts.Content.ParsecTilesColorfulPart" %>
    
    <div class="<%: this.RootCss()%>" id="<%: this.ClientID%>" >
      
      <div class="tstile-body">
        <div class="tstile-upper">
          <div class="tstile-lower text-right"></div>
        </div>
      </div>
    </div>
    

Leaving the HTML for now, let's begin working on the C# Script. With any of the built-in TrakSYS Content Parts, there is a Part Editor form that allows the part to be tailored to the specific need of the page. For a built-in Tile, it resembles the following:

![](https://portal.parsec-corp.com/hc/article_attachments/18994892018963)

Within this form, there are groups (e.g. General, Text, Band, etc.) that contain subgroups (e.g. Icon [General], Click [General], Upper Left [Text], Lower Right [Text], etc.). The Part Editor form is programatically generated from properties that are declared with the **`ContentProperty`** Attribute in the Script of the Content Part. For this example, we need to declare at least three CSS color classes, a midpoint starting value, a midpoint ending value, a text field, and a source key field which will accept a Values Dictionary key containing a "target" date/time:
    
    
    /// ******************************************************
    //// Declare properties with ContentProperty Attribute 
    ///  so they are exposed for editing from the Part Editor
    /// ******************************************************
    
    [ContentProperty(
        Label="Source Key"
      , GroupKey=nameof(ContentPropertyGroup._GENERAL)
      , DisplayOrder=1
      , ShouldRenderKeyInput=false)]
    public string TargetDateTimeKey { get; set; } = "";
    
    // general color
    [ContentProperty(
        Label="Start Color"
      , GroupKey=nameof(ContentPropertyGroup._GENERAL)
      , SubGroupKey=nameof(ContentPropertySubGroup._GENERAL_COLOR)
      , DisplayOrder=1, ControlTypeKey = ControlTypeKey.ColorPalette)]
    public string StartingColorCss { get; set; } = "tscolor-success";
    
    [ContentProperty(
        Label="Mid Color"
      , GroupKey=nameof(ContentPropertyGroup._GENERAL)
      , SubGroupKey=nameof(ContentPropertySubGroup._GENERAL_COLOR)
      , DisplayOrder=3, ControlTypeKey = ControlTypeKey.ColorPalette)]
    public string MiddleColorCss { get; set; } = "tscolor-warning";
    
    [ContentProperty(
        Label="End Color"
      , GroupKey=nameof(ContentPropertyGroup._GENERAL)
      , SubGroupKey=nameof(ContentPropertySubGroup._GENERAL_COLOR)
      , DisplayOrder=5, ControlTypeKey = ControlTypeKey.ColorPalette)]
    public string EndingColorCss { get; set; } = "tscolor-alert";
    
    [ContentProperty(
        Label="Mid Start Value (Seconds)"
      , GroupKey=nameof(ContentPropertyGroup._GENERAL)
      , SubGroupKey=nameof(ContentPropertySubGroup._GENERAL_COLOR)
      , DisplayOrder=2)]
    public int MidStartValueSeconds { get; set; } = -1;
    
    [ContentProperty(
        Label="Mid End Value (Seconds)"
      , GroupKey=nameof(ContentPropertyGroup._GENERAL)
      , SubGroupKey=nameof(ContentPropertySubGroup._GENERAL_COLOR)
      , DisplayOrder=4)]
    public int MidEndValueSeconds { get; set; } = -1;
    
    // general text
    [ContentProperty(
        Label="Text"
      , GroupKey=nameof(ContentPropertyGroup._GENERAL)
      , SubGroupKey=nameof(ContentPropertySubGroup._GENERAL_TEXT)
      , DisplayOrder=1
      , ShouldRenderKeyInput=false
      , ControlTypeKey = ControlTypeKey.ProcessExpressionResourceItem)]
    public ResourceStringItem TextEx { get; set; } = "";
    

The resulting Part Editor will eventually appear similar to the picture below. Notice the sub groups, picker types, and expression syntax appearance of the Text field. It all originates from the **`ContentProperty`** attributes that are declared in the code.

![](https://portal.parsec-corp.com/hc/article_attachments/18995023885331)

The existing **`ContentPart_Init`** method should resemble the following. To set the initial color of the tile, the code calculates the time difference (in seconds) between the current site's date/time and the target date/time (set from the Part Editor). In addition to performing that calculation, this method calls another method to insert some JavaScript that's responsible for dynamically changing the tile's color when surpassing the limits (the full **`CreateJs`** method will be provided in a later step). 
    
    
    protected DateTimeOffset _targetDateTimeValue;
    
    protected override bool ContentPart_Init()
    {
      _targetDateTimeValue = this.Ets.Values.GetAsDateTimeOffset(
          this.TargetDateTimeKey
        , ETS.Core.Constants.NullDateTimeOffset
        );
      
      if (_targetDateTimeValue.IsNull()) 
        return this.Ets.Debug.FailContentPage("The TargetDateTimeKey is required");
      
      // calculate the color based on TargetDateTime
      DateTimeOffset currentDateTimeOffset = this.Ets.SiteNow;
      int durationInSeconds = (_targetDateTimeValue - currentDateTimeOffset).Seconds;
      
      _actualColorCss = this.StartingColorCss;
      
      if(durationInSeconds <= this.MidStartValueSeconds 
        && durationInSeconds > this.MidEndValueSeconds) 
      {
        _actualColorCss = this.MiddleColorCss;
      }
      else if(durationInSeconds < this.MidEndValueSeconds)
      {
        _actualColorCss = this.EndingColorCss;
      }  
      
      if (this.TextEx.IsNullOrWhiteSpace())
      {
        this.TextEx = "{" + this.TargetDateTimeKey + ":timer-down:hms} remaining";
      }
      
      this.Ets.Js.Add(CreateJs());
      
      return true;
    }
    

Now that the initial color is set when the part is initialized, we can override the `**RootCss**` method to apply the expected CSS classes of the built-in TrakSYS tile, the extra CSS class (if it's set in the Advanced properties of the Part Editor), and the color of the tile:
    
    
    protected string _actualColorCss;
    
    protected override string RootCss()
    {
      var cssList = new List<string>();
      cssList.Add("tstile");
      cssList.Add(base.RootCss());
      // height
      cssList.Add("tstile-h-medium");
      // width
      cssList.Add("col-sm-12");
      // color
      cssList.AddIfNotNull(this.CssClassExtra);
      
      var css = new System.Text.StringBuilder();
      bool isFirst = true;
      foreach (var s in cssList)
      {
        isFirst = css.AppendSeperatorIfNecessary(isFirst, " ");
        css.Append(s);
      }  
      
      return css.ToString();
    }
    

The **`DataBindProcessExpressionToChildControls`** method should be similar to the following. The one line to add in the existing method would be to process the text value given in the Property Editor of the part as a live expression. 
    
    
    protected IHtmlString _textValue;
    
    protected override bool DataBindProcessExpressionToChildControls()
    {
      if (!base.DataBindProcessExpressionToChildControls()) return false;
      
      _textValue = this.Ets.ProcessExpressionLive(this.TextEx, null, this.ID, "TextEx");
      
      return true;
    }
    

The `**_textValue**` will be passed to the View's HTML so it gets rendered when the part is displayed. In addition, the JavaScript code included in the next step will benefit from the use of data-* attributes in the HTML. The data-* attributes are used to store custom data private to the page. The stored data can then be used in the page's JavaScript to create a more engaging user experience (without any Ajax calls or server-side database queries). 
    
    
    <%@ Control Language="C#" AutoEventWireup="true" 
    Inherits="ETS.Ts.Content.ParsecTilesColorfulPart" %>
    
    <div class="<%: this.RootCss()%>" id="<%: this.ClientID%>" 
        data-targetdatetime="<%: _targetDateTimeValue.ToUniversalDateTimeString()%>"
        data-mid-start=     "<%: MidStartValueSeconds%>"
        data-mid-end=       "<%: MidEndValueSeconds%>"
        data-start-color=   "<%: StartingColorCss%>"
        data-midpoint-color="<%: MiddleColorCss%>"
        data-endpoint-color="<%: EndingColorCss%>"
      >
      
      <div class="tstile-body">
        <div class="tstile-upper">
          <div class="tstile-text-medium"><%: _textValue%></div>
        </div>
      </div>
    </div>
    

The following **`CreateJs`** method is provided to set the color when the operator is already viewing the page and one of the configured limits is surpassed. It performs a very similar calculation to the `**ContentPart_Init**` method when deciding which color to initially set on the Tile.
    
    
    private string CreateJs()
    {      
      string js = @"
      function "+this.ClientID+@"_UpdateTileState () {
        var $part = $('#"+this.ClientID+@"');
        
        var tdtString = $part.attr('data-targetdatetime');
        
        // calculate duration
        var tdt = ets.dateTime.getDateObjectFrom(tdtString);
        var now = ets.dateTime.getNow();
        var momentNow = moment(now, now.etsOffset);
        var durationInSeconds = (tdt - momentNow)/1000;
        
        // remove any color(s) from $part
        $part.removeClass (function (index, className) {
          return (className.match (/(^|\s)tscolor-\S+/g) || []).join(' ');
        });
    
        var startColor = $part.attr('data-start-color');
        var midColor = $part.attr('data-midpoint-color');
        var endColor = $part.attr('data-endpoint-color');
    
        var midStartValueSeconds = 
            ets.util.tryIntParse($part.attr('data-mid-start'),-1);
        var midEndValueSeconds = 
            ets.util.tryIntParse($part.attr('data-mid-end'),-1);
    
        // figure out what color to apply to $part
        if(durationInSeconds > midStartValueSeconds) {
          $part.addClass(startColor);
        }
        else if(durationInSeconds <= midStartValueSeconds 
               && durationInSeconds > midEndValueSeconds) {
          $part.addClass(midColor);
        }
        else if(durationInSeconds < midEndValueSeconds) {
          $part.addClass(endColor);
        }  
        
        ets.util.asyncWait(1000).then(function() {
         "+this.ClientID+@"_UpdateTileState();
       });
      }
      ets.ready(function(page) {
        "+this.ClientID+@"_UpdateTileState();
      });";
      
      return js;
    }
    

To test this newly developed part, you can add a script similar to the following to a Visual Page definition:
    
    
    protected override bool ContentPage_Init()
    {
      DateTimeOffset todayAtFivePM = this.Ets.SiteNow.Date.AddHours(17).AsDateTimeOffset(); 
    
      this.Ets.Values["TargetEndDateTime"] = todayAtFivePM; 
    
      return true; 
    }
    

The rest of the part's Property Editor can be set to your specifications:

![](https://portal.parsec-corp.com/hc/article_attachments/18995261669139)

The resulting page should now contain your custom Content Part!

![](https://portal.parsec-corp.com/hc/article_attachments/18995273620755)

This is just one example of how powerful a custom Content Part can be. The initial development has a level of complexity, but the resulting part is a reusable and robust option for any Visual Page developer.
