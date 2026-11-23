# Properties

The properties in this namespace are different depending on the DbEntity. While all DbEntities have access to this namespace, not all entities will have usable properties. The properties generated for each DbEntity will generally mirror the options that are available under the Actions section when viewing Configuration Entities in the TrakSYS Web. Entities that have multiple variations with different actions may have all properties available in the namespace for every possible variation.

## Examples

### Properties Available to Areas (Single Entity)

In general, there is only 1 type of Area available even though each Area can have a different **S95 Type**. Therefore, the Actions for this configuration entity (found on the third slice of a selected Area within the TrakSYS Web under **Configuration | Systems**) are the same. Besides the **Disable** and **Delete** actions, the entity has the following unique properties:

* **Set Logic Service**
* **Move**
* **Duplicate**

Therefore, the following properties within the `Api.Data.DbArea.Do` namespace contain the following properties to mirror the actions above:

```csharp
// Set Logic Service
this.Ets.Api.Data.DbArea.Do.SetLogicManagerToArea();

// Move
this.Ets.Api.Data.DbArea.Do.MoveToArea();

// Duplicate
this.Ets.Api.Data.DbArea.Do.Duplicate();
```

### Properties Available to Systems (Multiple Variations)

When configuring Systems, there are multiple variations available. This includes Discrete, Batching, Storage, Template Parent, and Template Child Systems. Some System types may have similar actions or may have actions that are unique to a specific variation. Between all possible variations, the following actions are available:

* **Set System Capture Scheme**
* **Set Job Capture Scheme (unique to Discrete Systems)**
* **Create Template Parent System**
* **Move**
* **Assign Tags From Template Parent (unique to Parent Template Systems)**
* **Detach From Template Parent (unique to Child Template Systems)**

As shown above, multiple variations of Systems share some actions, while other actions are unique to a specific System type. Therefore, the following properties in the `Api.Data.DbSystem.Do` namespace contain the following properties to mirror the actions above:

```csharp
// Set System Capture Scheme
this.Ets.Api.Data.DbSystem.Do.SetSystemCaptureScheme();

// Set Job Capture Scheme
this.Ets.Api.Data.DbSystem.Do.SetJobCaptureScheme();

// Create Template Parent System
this.Ets.Api.Data.DbSystem.Do.CreateAndSaveTemplateFromSystem();

// Move
this.Ets.Api.Data.DbSystem.Do.MoveToArea();

// Assign Tags From Template Parent
this.Ets.Api.Data.DbSystem.Do.AssignTagsFromTemplate();

// Detach From Template Parent
this.Ets.Api.Data.DbSystem.Do.DetachSystemFromTemplateParent();
```
