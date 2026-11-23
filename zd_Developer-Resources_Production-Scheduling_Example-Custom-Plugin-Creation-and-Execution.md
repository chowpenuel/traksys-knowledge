# Example Custom Plugin Creation and Execution

*Source: https://portal.parsec-corp.com/hc/en-us/articles/5508823062547-Example-Custom-Plugin-Creation-and-Execution*
*Last updated: 2023-11-08T18:00:30Z*

---

Applies To | TrakSYS 11 | TrakSYS 12

### Summary

When using the Production Scheduling functionality, it may be necessary to use custom plugins to help meet more specific implementation requirements. Custom plugins can help extend the functionality of the normal Production Scheduling engine to account for other necessary variables and constraints. These plugins can be executed with custom C# code using the TrakSYS API.

This article contains an example of how to create and execute a Production Scheduling Plugin. The example uses a Discrete Production Scheduling Plugin and adds a Custom Weight that is used as a part of the standard Production Scheduling algorithm.

Please note that within this example, the following assumptions are made:

  * The job data has been imported and exists within the TrakSYS installation.
  * Production Schedule Sets, Changeover Families, and Changeover Types have been configured.



### Example

#### **Creating the Custom Plugin**

  1. To begin, a Production Schedule Plugin should be created. To do this, go into the TrakSYS Web and navigate to **Developer | Scripts | Global**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222089704339)  
  

  2. Create a new Script Group or select an existing one.
  3. Select the Script Group and click the New button to create a new Global Script.
  4. For the purpose of this example, the Production Scheduling (Discrete) option was selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222120578707)  
  

  5. After providing a name to the plugin and saving the changes, select the newly created plugin on the second slice, and select the Script link on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222217194003)  
  

  6. The following code example can be placed within the Plugin.  
  

         
         using System;
         using System.Collections.Generic;
         using ETS.Core;
         using ETS.Core.Api;
         using ETS.Core.Api.Models;
         using ETS.Core.Api.Models.Data;
         using ETS.Core.Api.Models.DateAndTime;
         using ETS.Core.Api.Models.ProductionScheduling;
         using ETS.Core.Api.Models.ProductionScheduling.Plugins;
         using ETS.Core.Enums;
         using ETS.Core.Extensions;
         using ETS.Core.Scripting;
         
         namespace ETS.Core.Scripting.ProductionScheduling {
           /// ******************************************************************
           /// <summary>
           /// This class contains code that is executed during the execution of
           /// the Production Scheduling algorithm and allows customization through
           /// script to alter the default behavior, enabling the ability to control
           /// if jobs can be assigned and what the overall placement score is for
           /// each attempt.
           /// </summary>
           /// ******************************************************************
           public class CustomDiscreteProdSchedulePlugin: PsDiscreteJobPluginBase {
             private readonly ApiService _api;
             private IPsStatusUpdater _updater;
         
             // reset each jobsystem loop
             private double _maxTheo; // product.theoreticalrate
             private double _maxTarget; // product.targetrate
         
             public PsScheduleSettings Settings {
               get;
               set;
             }
             private int TheoreticalRateWeight; // default value is set to 0 as part of the constructor
             private int TargetRateWeight; // default value is set to 0 as part of the constructor
         
             /// ******************************************************************
             public CustomDiscreteProdSchedulePlugin(ApiService api, int theoreticalWeight = 0, int targetWeight = 0) {
               _api = api;
               this.Settings = null;
               this.TheoreticalRateWeight = theoreticalWeight;
               this.TargetRateWeight = targetWeight;
             }
         
             /// ******************************************************************
             /// <summary>
             /// This method is the first plugin method to be called.
             /// </summary>
             /// ******************************************************************
             public override Result < bool > Init(IPsGeneralInitContext context) {
               var r = new Result < bool > ();
               this.Settings = context.Settings;
               return r.AsSuccess(true);
             }
         
             /// ******************************************************************
             /// <summary>
             /// This method is called once the DbPsStage has been created and 
             /// therefore allows status messaging to be sent.
             /// </summary>
             /// ******************************************************************
             public override Result < bool > PostCreatePsStage(DbPsStage psStage, IPsStatusUpdater updater) {
               var r = new Result < bool > ();
               _updater = updater;
         
               // update the PsStage Notes to include the additional weights
               psStage.Notes += @" *
                 Theoretical Weight *: {
                   0
                 }
                 * Target Weight *: {
                   1
                 }
               ".FormatWith(this.TheoreticalRateWeight, this.TargetRateWeight);
         
               _api.Data.DbPsStage.Save.UpdateExisting(psStage).ThrowIfFailed("Failed to updated PsStage notes with custom weight values.");
         
               return r.AsSuccess(true);
             }
         
             // ***********************************************************
             public override Result < bool > PreScheduleInfoForJobSystems(IPsDiscreteJobGeneralScheduleInfoForJobSystemsContext context) {
               var r = new Result < bool > ();
         
               // reset max values to 0 for later use
               _maxTheo = 0;
               _maxTarget = 0;
         
               return r.AsSuccess(true);
             }
         
             // ***********************************************************
             public override Result < DbProduct > LoadProduct(IPsDiscreteJobProductContext context) {
               // update max with loaded products
               _maxTheo = context.Product.TheoreticalRateCalculationUnitsPerMinute.AtLeast(_maxTheo);
               _maxTarget = context.Product.TargetRateCalculationUnitsPerMinute.AtLeast(_maxTarget);
         
               // return product found by built-in logic
               return new Result < DbProduct > ().AsSuccess(context.Product);
             }
         
             /// ***********************************************************
             public override Result < double > CalculateCustomScore(IPsDiscreteJobScoreCustomContext context) {
               var r = new Result < double > ();
         
               switch (context.ScoreType) {
               case 1:
                 return r.AsSuccess(this.CalculateTheoreticalWeightedValue(context.ScoreInfo.Product.TheoreticalRateCalculationUnitsPerMinute));
                 break;
               case 2:
                 return r.AsSuccess(this.CalculateTargetWeightedValue(context.ScoreInfo.Product.TargetRateCalculationUnitsPerMinute));
                 break;
               }
         
               return r.AsSuccess(0);
             }
         
             /// ***********************************************************
             public override Result < bool > PostScheduleInfoForJobSystems(IPsDiscreteJobGeneralScheduleInfoForJobSystemsContext context) {
               // this will add messages into the tPsStageMessage table for debugging purposes.
               _updater.LogStageMessage("- Target Rate Scoring | Maximum: {0} | Selected Job: {1}".FormatWith(_maxTarget, context.BestJob.Product.TargetRateCalculationUnitsPerMinute));
               _updater.LogStageMessage("- Theoretical Rate Scoring | Maximum: {0} | Selected Job: {1}".FormatWith(_maxTheo, context.BestJob.Product.TheoreticalRateCalculationUnitsPerMinute));
         
               return new Result < bool > ().AsSuccess(true);
             }
         
             /// ***********************************************************
             private double CalculateTheoreticalWeightedValue(double selectedTheoreticalRate) {
               // if max theoretical or selected theoretical is 0, return 0;
               if (_maxTheo == 0 || selectedTheoreticalRate == 0) return 0;
         
               // scale the value based on total weight
               double relativeValue = selectedTheoreticalRate / _maxTheo * this.TheoreticalRateWeight;
               return relativeValue;
             }
             private double CalculateTargetWeightedValue(double selectedTargetRate) {
               // if max target or selected target is 0, return 0;
               if (_maxTarget == 0 || selectedTargetRate == 0) return 0;
         
               // scale the value based on total weight
               double relativeValue = selectedTargetRate / _maxTarget * this.TargetRateWeight;
               return relativeValue;
             }
           }
         }
         

  7. Once the code has been saved, click the Compile button to perform a Full Compile. **Note:** the logic service should be stopped **before** performing this action.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/5528487180691)



#### **Using a Custom Plugin**

Now that the plugin has been created, a Page Definition should be built to use and execute the logic. The following steps will create a simple, custom Visual Page Definition that will take the Custom Plugin into consideration when executing the Production Scheduling engine.

  1. Within the TrakSYS Web, navigate to **Developer | Page Definitions** and add a new Visual Page Definition.
  2. Select the newly created Page Definition and click the Spokes link on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222308893971)  
  

  3. When adding a new Spoke to the page, add the Production Schedule Stages (ETS.Application.Ps.PsStaged) Content Page. This page will display the generated Stages after executing the Production Scheduling engine.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222341314707)  
  

  4. For the purpose of this example a value of "prodschedspoke" was specified for the Key of this page. It is recommended to assign more meaningful Keys for real-world implementations.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222414589971)  
  

  5. After saving the changes, click the Parts link on the first slice. This will open up the Parts editor for the custom Visual Page Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222442279827)  
  

  6. In the editor, add a Buttons (ETS.TsButtons) Part to the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222513590803)  
  

  7. Within the properties of the Button Part, click the ellipsis (...) to open the Click Actions menu.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222556242067)  
  

  8. On the Click Actions menu, specify an On Server Click method. For the purposes of this example, a value of Button_Click was provided.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222576362131)  
  

  9. After saving the changes to the Buttons Part, navigate to the Script tab of the page properties.
  10. Within the C# code of the page, add the following using statements:  
  

         
         // Add Using Statements
         using ETS.Ts.Core.Services.Web.StatusActivities;
         using ETS.Core.Api.Services.StatusActivities;
         

  11. At the class level, add the following variables.  
  

         
         private Dictionary<string, string> _params; // Can be any entity. However, it is better if structured for specific properties
         private LongRunningActivityPageHelper _activityHelper;
         

  12. Next, add a button click handler for the Buttons Part. The method below contains code that will include the Production Scheduling Plugin and will set custom weights. For the purpose of this example, 23 and 67 have been provided for these weights. The code also includes notes that show these custom weight values. Comments within the code explain what each part is doing.   
  

         
         protected void Button_Click(object sender, EventArgs e)
         {
           _params = new Dictionary<string, string>();
           // Displays loading screen to show the status of the schedule being generated
           _activityHelper = this.Ets.Api.Create.InstanceOf<LongRunningActivityPageHelper>();
         
           // Connect to spoke page using the key of the page
           _activityHelper.DefaultWaitForSuccessUrl = "prodschedspoke";
           _activityHelper.RequestActivity(_params, this.GenerateSchedule, "Running Scheduler...");
           //return true;
         }
         
         private void GenerateSchedule(Dictionary<string, string> paramInfo, LongRunningActivityContext context)
         {
           try
           {
             var status = context.Status;
             // Display status during loading screen
             status.UpdateStatus("creating settings", 0);
             var psset = this.Ets.Api.Data.DbPsSet.Load.ByID(1);
         
             // Specify Production Schedule Set settings
             var _psSettings = this.Ets.Api.ProdSched.CreateSettingsFromParentPsSet(psset);
         
             _psSettings.Name = "Optimized by Custom Weight Plugin";
             _psSettings.PlannedStartDateTimeScoreWeight = 0;
             _psSettings.SortPriorityScoreWeight = 0;
             _psSettings.UnitDurationScoreWeight = 0;
             _psSettings.PaddingDurationScoreWeight = 0;
             _psSettings.GapDurationScoreWeight = 0;
             _psSettings.ChangeoverDurationScoreWeight = 0;
             _psSettings.PsRequestedDateTimeScoreWeight = 0;
             _psSettings.SystemPriorityScoreWeight = 0;
             _psSettings.PsPromisedDateTimeScoreWeight = 0;
             _psSettings.PsRequestedPriorityScoreWeight = 0;
             _psSettings.IsVerboseLoggingEnabled = true;
         
             // Display status during loading screen
             status.UpdateStatus("preparing plugin", 10);
         
             // Use the Production Scheduling custom script and set the weights
             var myPlugin = new ETS.Core.Scripting.ProductionScheduling.CustomDiscreteProdSchedulePlugin(this.Ets.Api, 23, 67);
         
             // Display status during loading screen
             status.UpdateStatus("starting scheduling algorithm", 50);
             var result = this.Ets.Api.ProdSched.Schedule(_psSettings, myPlugin).ThrowIfFailed("scheduling ps stage failed");
         
             // Display status during loading screen
             status.UpdateStatus("saving schedule stage", 90);
           }
         
           catch (Exception ex)
           {
             this.Ets.Api.Util.Log.WriteException(ex);
             context.Status.UpdateStatusAsFailure("One or more errors have occurred.");
           }
         }
         

  

  13. After saving the changes, the page can be previewed to view the final results. The Generate button should appear as well as the link for the Production Scheduling Stages spoke.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222603282451)  
  

  14. When the Generate button is clicked, it should generate a schedule based on the Production Scheduling Plugin and the custom values provided in the C# script. While the Scheduling Engine is processing, messages from status. UpdateStatus lines should appear.  
  

  15. The built-in Production Schedule Stages Content Page will show the currently generated schedule. On the third slice of the page, the custom Theoretical and Target Weights should display under the Notes field.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222700272019)
  16. Lastly, any messages that were generated can be seen under the Messages menu option. This includes both the standard messages and any plugin-specific messages.  
![](https://portal.parsec-corp.com/hc/article_attachments/18890338254739)


