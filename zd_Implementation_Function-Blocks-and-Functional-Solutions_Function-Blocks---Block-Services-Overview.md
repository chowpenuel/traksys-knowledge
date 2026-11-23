# Function Blocks - Block Services Overview

*Source: https://portal.parsec-corp.com/hc/en-us/articles/52513292383507-Function-Blocks-Block-Services-Overview*
*Last updated: 2026-06-19T00:19:18Z*

---

### General Overview

The Common Block provides the base Block service entry point. It is accessible through:
    
    
    Api.Blocks()
    

Most Blocks expose their own block-specific services from this base path. For example, the Orders Block is exposed through:
    
    
    Api.Blocks().Orders()
    

Block services may also expose child services for related functionality. For example, a Message service may be exposed from the Block service and used for message-related utilities.

The available methods and functionality are documented in the related Block documentation. As an example, the line below is used during Message processing to create an external URL:
    
    
    this.Ets.Api.Blocks().Message.MakeExternalUrl(this.Ets.Pages.FullUrlPath)
    

### Operations Pattern

In addition to general utilities, many Blocks include an operations pattern. This pattern provides a standard way to inject custom scripted logic into common workflows such as validation, execution, assignment, reset, or other Block-specific processing.

The exact operations may vary by Block, but the overall structure is generally consistent. This article uses the Orders Block as the example, with the understanding that the same pattern can be adapted for other Blocks.

### Orders Operations - Interface

The Orders Block includes the `IOrderOperations` interface. This interface defines the operations contract used by the Orders service. Below is a partial summary of the supported operations:

  * Validation for New, Update, Start, End, and Assign.
  * Execution for New, Update, Start, End, Assign, Unassign, Reset, and related supporting logic.



The interface defines which operations are available. Implementing classes then provide the actual behavior for those operations.

If a new operation is added, it should be added consistently across the operations pattern. This usually means updating the interface, the base operations class, any derived operations classes that need custom behavior, and the service method that routes calls to the selected operations implementation.

### Orders Operations - Operations Classes

The interface defines the structure, but it must be implemented before it can be used. In the Orders Block, the base implementation is the `OrderOperations` class.

`OrderOperations` implements `IOrderOperations` and provides shared default behavior used by derived operations classes. For example, it includes common validation for starting and ending Jobs, along with standard state changes for Start and End. Some methods contain default behavior. Others are intentionally left as no-op methods or default successful validations so that derived classes can override them when more specific logic is required.

For example, the logic needed to validate or assign a Job can differ between Discrete and Batch systems. The base class provides the shared pattern, while derived classes such as `OrderOperations_Batch` or `OrderOperations_Discrete` provide the system-specific behavior. The Orders service is responsible for selecting the appropriate operations implementation, which is covered in more detail below.

### Orders Operations - Calling an Operation

Operations are usually called through the Orders service rather than by directly creating an operations class. The service method acts as the public entry point, while the operations implementation provides the actual behavior.

For example, the Order Start page calls the Orders service from the standard form submit methods. During `FormSubmit_Validate`, it calls `ValidateForStart`:
    
    
    var res = this.Ets.Api.Blocks().Orders().ValidateForStart(_job, this.SystemID, this.Ets.User.Login);
    

Then, during `FormSubmit_Execute`, it calls `Start`:
    
    
    this.Ets.Api.Blocks().Orders().Start(_job, this.SystemID, this.Ets.User.Login, uow);
    

In both cases, the page calls the same Orders service path. The page does not need to know whether the System uses the Discrete, Batch, System Type-specific, or System-specific operations class. It passes the `systemID`, and the Orders service uses that value to resolve the correct operations implementation internally. This keeps the page logic consistent while still allowing the underlying behavior to change by System or System Type.

### Orders Operations - Implementation Selection

When an Orders service method is called, the service first resolves the operations implementation for the provided `systemID`. This is handled internally by loading the System record, checking the available configuration and naming conventions, and then creating an instance of the matching operations class.

The selection follows a specific order. First, the service checks for a System-specific class using the System Key. This allows a single System to have its own operations logic. If no System-specific class is found, the service checks the System Type. The System Type can either define an explicit script class name or rely on a naming convention based on the System Type Key. If none of those are found, the service falls back to the default implementation based on the S95 System Type. In that fallback case, a `ProductionLine` uses the Discrete operations implementation, while a `ProcessCell` uses the Batch operations implementation.

Other Blocks may use different names or operation types, but the pattern is generally the same. The Block service acts as the common entry point, resolves the appropriate operations implementation, and then delegates the requested action to that implementation.

### Orders Operations - Adding a New Implementation

The example below shows how to create a new operations implementation for the Orders Block. Other Blocks may use different class names, interfaces, or selection rules, but the overall pattern is similar: 

  1. Create a Block-specific implementation class.
  2. Inherit from the shared base class when available.
  3. Override the methods that need custom behavior.



To add a new operations implementation, create a new script class in the `Blocks.Orders` namespace. In most cases, the class should inherit from `OrderOperations` rather than implementing `IOrderOperations` directly. This allows the new class to reuse the shared default behavior and override only the operations that need custom logic.

For example, a System Type-specific implementation can be created using the following pattern:
    
    
    namespace Blocks.Orders
    {
      public class OrderOperations_SystemType_MySystemType : OrderOperations
      {
        public OrderOperations_SystemType_MySystemType(ApiService api) : base(api) {}
    
        public override Result<bool> ValidateForAssign(DbJobBatchComposite jobBatch, DbJobDiscreteComposite jobDiscrete, int systemID)
        {
          // custom validation logic
          return base.ValidateForAssign(jobBatch, jobDiscrete, systemID);
        }
    
        public override void Assign(DbJobBatchComposite jobBatch, DbJobDiscreteComposite jobDiscrete, int systemID, IUnitOfWork uow)
        {
          // custom assignment logic
          base.Assign(jobBatch, jobDiscrete, systemID, uow);
        }
      }
    }
    

Once the operations class exists, it needs to be associated with the appropriate configuration. In this example, the implementation is intended for a specific System Type, so the System Type Key is the important value.

For a System Type-specific implementation, name the class using the `OrderOperations_SystemType_{SystemTypeKey}` pattern, where `{SystemTypeKey}` matches the Key of the configured System Type. For example, if the System Type Key is `MySystemType`, the operations class would be named `OrderOperations_SystemType_MySystemType`.

Any System assigned to that System Type will then use the matching implementation, unless a more specific System-level implementation is available. This allows shared logic to be applied across multiple Systems through normal System Type assignment.

There are other ways to resolve an operations implementation. See the previous section on implementation selection, and review the related service logic directly to confirm the expected naming conventions and fallback behavior.
