# Creating a Custom ASP.NET chart

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360005772693-Creating-a-Custom-ASP-NET-chart*
*Last updated: 2025-05-21T22:52:20Z*

---

Applies To | TrakSYS 10+

### **Summary**

In the event that a built-in ASP.NET chart does not meet a project requirement, there is an opportunity to develop your a custom chart to fulfill the requirement. This is possible because the built-in ASP.NET charts use the standard `System.Web.UI.DataVisualization.Charting` namespace.

The following tutorial should serve as a guide when developing your own custom ASP.NET chart in TrakSYS 10. The tutorial is focused around customizing the SPC Individuals Chart which resembles the following:

![](https://portal.parsec-corp.com/hc/article_attachments/360007315553)

The customization being made will adjust the red, yellow, and green bands behind the chart to align with the control limit and spec limit lines.

### **Procedure**

Create or open an existing Visual Page definition.

Add a View Fragment part:

![](https://portal.parsec-corp.com/hc/article_attachments/18891773918611)

The View Fragment should contain HTML similar to the following. Make a note of the ID chosen here as that's how you will reference the chart object from the page Script ("myChart" is the chosen ID in this example).
    
    
    <div class="col-sm-12 tscontentpart-dynamic">
      <asp:Chart id="myChart" runat="server"></asp:Chart>
    </div>
    

Add a Data Table part. Since we're working with SPC for this guide, we'll need a Sample Sub-Groups (Variable) data table part:

![](https://portal.parsec-corp.com/hc/article_attachments/18891858016787)

After configuring the filters for the data table part, make a note of the Target Values Key since that will be used in later steps (the key is "Data.SampleSubGroupsVariable" in this example).

![](https://portal.parsec-corp.com/hc/article_attachments/18891929810195)

Navigate to the page Script and add the following `using` statement so you can take advantage of the Color struct later on:
    
    
    using System.Drawing;
    

  
The script block below leverages the ASP Chart object created in the View Fragment. The chart area controls the axes while the series will contain the data points. About half of the method is dedicated to the look-and-feel of the chart while the other half loops through the dataset to gather critical information and plot the datapoints in the series.
    
    
    private double _processLsl = -1;
    private double _processUsl = -1;
    private double _calculatedLcl;
    private double _calculatedUcl;
    
    private DateTime _minDateTime = DateTime.MaxValue;
    private DateTime _maxDateTime = DateTime.MinValue;
    
    private ApiService _api;
    
    /// *********************************************************
    protected override bool ContentPage_PartPreInit06()
    {
      _api = this.Ets.Api;
      
      // myChart object originates from View Fragment
      myChart.Width = 400;
      myChart.Height = 300;
    
      ChartArea ca = new ChartArea();
      
      // get theme for default fonts
      var theme  = new ETS.Ts.Core.ContentParts.Charts.NetChartTheme();
    
      // Y axis styling
      ca.AxisY.MajorTickMark.Enabled = false;
      ca.AxisY.LineColor = Color.Transparent;
      ca.AxisY.LabelStyle.ForeColor = TsColor.Slate.ToColor();
      ca.AxisY.LabelStyle.Font = theme.GetFont();
      ca.AxisY.MajorGrid.LineColor = TsColor.Gray.ToColor();
    
      // X axis styling
      ca.AxisX.MajorTickMark.Enabled = false;
      ca.AxisX.LabelStyle.Enabled = true;
      ca.AxisX.LabelStyle.ForeColor = TsColor.Slate.ToColor();
      ca.AxisX.LineColor = TsColor.Gray.ToColor();
      ca.AxisX.MajorGrid.Enabled = false;
      ca.AxisX.LabelStyle.Format = "hh:mm";
      ca.AxisX.LabelStyle.Font = theme.GetFont();
      ca.AxisX.IsMarginVisible = false;
      
      myChart.ChartAreas.Add(ca);
    
      // data line series styling
      Series s = new Series();
      s.ChartType = SeriesChartType.Line;
      s.Color = TsColor.Black.ToColor();
      s.BorderColor = TsColor.Black.ToColor();
      s.BorderWidth = 3;
      s.BackSecondaryColor = TsColor.Success.ToColor();
      s.XValueType = ChartValueType.DateTimeOffset;
    
      // data originates from SQL part
      var sourceData = this.Ets.Values.GetAs("Data.SampleSubGroupsVariable", (DataTable) null)
        .ThrowIfNull("'Data.SampleSubGroupsVariable' expects a datatable!");
      
      // initialize variables for data retrieval
      int samplesPerSubGroup = -1;
      List<double> listOfSampleRanges = new List<double>();
      List<double> listOfMovingRanges = new List<double>();
      
      int i = 0;
      
      foreach (DataRow row in sourceData.Rows)
      {
        // X coordinate
        var sampleSubGroupDateTime = row.GetDateTime("SampleSubGroupDateTimeOffset");
        
        // Y coordinate
        double sampleMean = row.GetDouble("SampleMean");
      
        s.Points.AddXY(sampleSubGroupDateTime, sampleMean);
        
        listOfSampleRanges.Add(sampleMean);
        
        _minDateTime = sampleSubGroupDateTime < _minDateTime ? 
                      sampleSubGroupDateTime : _minDateTime;
        _maxDateTime = sampleSubGroupDateTime > _maxDateTime ? 
                      sampleSubGroupDateTime : _maxDateTime;
                
        if(i != 0)
          listOfMovingRanges.Add(
              Math.Abs(listOfSampleRanges[i] - listOfSampleRanges[i-1])
              );
        else 
        {
          _processLsl = row.GetDouble("ProcessLsl");
          _processUsl = row.GetDouble("ProcessUsl");
          samplesPerSubGroup = row.GetInteger("SampleCount");
        }
        
        i++;
      }
      myChart.Series.Add(s);
      
      //this.AddSpcLimits(listOfSampleRanges, listOfMovingRanges);
      //this.AddSpcBands(ca);
      
      myChart.DataBind();
      
      return true;
    }
    

The View Fragment part added previously should now render a chart similar to the following:

![](https://portal.parsec-corp.com/hc/article_attachments/360007664993)

Comparing this chart to the original, we now have a series with the same datapoints. On the other hand, we still need the control/spec limit lines and sigma ranges. Instead of deriving their formulas from scratch, the TrakSYS API contains an `Spc` namespace that can be leveraged to calculate the Upper Control Limit (UCL), Lower Control Limit (LCL), Upper Specification Limit (USL), and Lower Specification Limit (LSL). As far as the chart is concerned, these limits are simply horizontal series lines. Once the method below has been added to the script of the page, uncomment the `AddSpcLimits` call in `ContentPage_PartPreInit06`.
    
    
    /// *********************************************************
    private void AddSpcLimits(List<double> listOfSampleRanges, List<double> listOfMovingRanges)
    {
      int sampleCount = listOfSampleRanges.Count;
      
      double xBar = _api.Spc.Variable.CalculateMean(listOfSampleRanges);
      double mrBar = _api.Spc.Variable.CalculateMean(listOfMovingRanges);
      double icl = this.Ets.Api.Spc.Variable.CalculateIndividualsControlLimit(mrBar);
      
      _calculatedUcl = xBar + icl;
      _calculatedLcl = xBar - icl;
      
      // LSL line
      Series LSL = new Series();
      LSL.ChartType = SeriesChartType.Line;
      LSL.Color = TsColor.Blue.ToColor();
      LSL.Points.AddXY(_minDateTime, _processLsl);
      LSL.Points.AddXY(_maxDateTime, _processLsl);
      LSL.MarkerStyle = MarkerStyle.None;
      LSL.BorderDashStyle = ChartDashStyle.Dot;
      LSL.BorderWidth = 3;
      
      myChart.Series.Add(LSL);
      
      // USL line
      Series USL = new Series();
      USL.ChartType = SeriesChartType.Line;
      USL.Color = TsColor.Red.ToColor();
      USL.Points.AddXY(_minDateTime, _processUsl);
      USL.Points.AddXY(_maxDateTime, _processUsl);
      USL.MarkerStyle = MarkerStyle.None;
      USL.BorderDashStyle = ChartDashStyle.Dot;
      USL.BorderWidth = 3;
      
      myChart.Series.Add(USL);
    
      // LCL line
      Series LCL = new Series();
      LCL.ChartType = SeriesChartType.Line;
      LCL.Color = TsColor.Blue.ToColor();
      LCL.Points.AddXY(_minDateTime, _calculatedLcl);
      LCL.Points.AddXY(_maxDateTime, _calculatedLcl);
      LCL.MarkerStyle = MarkerStyle.None;
      LCL.BorderDashStyle = ChartDashStyle.Dash;
      LCL.BorderWidth = 3;
      
      myChart.Series.Add(LCL);
      
      // UCL line
      Series UCL = new Series();
      UCL.ChartType = SeriesChartType.Line;
      UCL.Color = TsColor.Red.ToColor();
      UCL.Points.AddXY(_minDateTime, _calculatedUcl);
      UCL.Points.AddXY(_maxDateTime, _calculatedUcl);
      UCL.MarkerStyle = MarkerStyle.None;
      UCL.BorderDashStyle = ChartDashStyle.Dash;
      UCL.BorderWidth = 3;
      
      myChart.Series.Add(UCL);
    }
    

The chart should now resemble the following:

![](https://portal.parsec-corp.com/hc/article_attachments/360007708513)

Now all we're missing is the sigma ranges. Once the method below has been added to the script of the page, uncomment the `AddSpcBands` call in `ContentPage_PartPreInit06`.

So far, we've adhered to the built-in SPC Individuals chart, but the code below will place the sigma ranges between the existing limit lines. In other words, instead of the sigma ranges being auto calculated, we are forcing the green sigma range to fall between UCL and LCL, the yellow sigma range to fall between each USL/UCL and LSL/LCL, and the red sigma range to fall outside the USL and LSL lines: 
    
    
    /// *********************************************************
    private void AddSpcBands(ChartArea ca)
    {
      if(_processLsl <= 0)
        ca.AxisY.IsStartedFromZero = false;
      
      ca.RecalculateAxesScale();
      double yMin = ca.AxisY.Minimum;
      double yMax = ca.AxisY.Maximum;
      
      // sigma ranges
      double[] first = new double[] 
      { 
        yMin, 
        _processLsl < _calculatedLcl ? _processLsl-0.5 : _calculatedLcl-0.5 
      };
      double[] second = new double[] 
      { 
        _processLsl < _calculatedLcl ? _processLsl+0.5 : 0, 
        _processLsl < _calculatedLcl ? _calculatedLcl-0.5 : 0 
      };
      double[] third = new double[] 
      { 
        _calculatedLcl+0.5,  
        _calculatedUcl-0.5 
      };
      double[] fourth = new double[] 
      {  
        _processUsl > _calculatedUcl ? _calculatedUcl+0.5 : 0,  
        _processUsl > _calculatedUcl ? _processUsl-0.5 : 0 
      };
      double[] fifth = new double[] 
      { 
        _processUsl > _calculatedUcl ? _processUsl+0.5 : _calculatedUcl+0.5,  
        yMax 
      };
      
      List<double[]> rangeValues = new List<double[]>();
      rangeValues.Add(first);
      rangeValues.Add(second);
      rangeValues.Add(third);
      rangeValues.Add(fourth);
      rangeValues.Add(fifth);
      
      //transparent colours
      Color[] rangeColours = new Color[] { 
          Color.FromArgb(25, TsColor.Red.ToColor())
        , Color.FromArgb(25, TsColor.Yellow.ToColor())
        , Color.FromArgb(25, TsColor.GreenLight.ToColor())
        , Color.FromArgb(25, TsColor.Yellow.ToColor())
        , Color.FromArgb(25, TsColor.Red.ToColor())};
    
      for (int r = 0; r < rangeValues.Count; r++)
      {
        Series rangeSeries = new Series("rangeSeries"+r);
        rangeSeries.ChartType = SeriesChartType.Range;
        double[] range = rangeValues[r];
        DataPoint a = new DataPoint(_minDateTime.ToOADate(), range);
        rangeSeries.Points.Add(a);
        DataPoint b = new DataPoint(_maxDateTime.ToOADate(), range);
        rangeSeries.Points.Add(b);
        rangeSeries.Color = rangeColours[r];
    
        myChart.Series.Add(rangeSeries);
      }
      ca.AxisY.Maximum = yMax;
      ca.AxisY.Minimum = yMin;
    }
    

The chart finally resembles the following:

![](https://portal.parsec-corp.com/hc/article_attachments/360007715453)
