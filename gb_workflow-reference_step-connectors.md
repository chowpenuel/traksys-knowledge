# Step Connectors (Paths)

The visual diagraming editor allows Steps to be "connected" by dragging and drawing **Paths** between Steps. When a Step completes execution (unless an error stops Process execution), the Workflow engine moves processing to all of the Steps connected by an **Path** line (in the direction specified by the arrow tip).

## Multiple Outgoing Paths

All outgoing **Paths** are followed in parallel when a Step completes. As the Workflow engine supports multi-threaded execution, Workflow authors should create processes with the understanding that parallel paths may be executing simultaneously.

## Conditional Outgoing Paths

In some cases, an outgoing **Path** should only be followed if a specific condition is present. Once Double-clicking a **Path** opens a property page where this conditional logic can be specified.

A **Path's** condition can be specified using the following conceptual expression...

Path is followed if **OUT\_VALUE** _OPERATOR_ **COMPARE\_VALUE**.

The following properties allow specification of the comparison elements and label behavior.

### Process Step Parameter Key

This entry field allows a **Process Values** Key to be specified identifying the `OUT_VALUE` to be used for the condition. The Key can be hand entered or can be selected from the "picker" which contains known outgoing Keys.

### Operator

This dropdown allows the selection of the **OPERATOR** used for the condition. Options include =, >, >=, <, <= and <>.

### Value

This entry field allows a constant value to be specified identifying the **COMPARE\_VALUE** to be used for the condition.

### Label

This description will be rendered on the **Path** in the diagram. The label should describe the "meaning" if the condition is true.

### Label Mode

This selection controls how the label is displayed **IF** the **Label** value is **NOT** specified.

**Smart** - Given a Process Step Parameter Key of `Error`, if the **COMPARE\_VALUE** specified is 1, the Label is rendered as **Error**. If the **COMPARE\_VALUE** specified is 0, the Label is rendered as **! Error**.

**Normal** - Given a Process Step Parameter Key of `Job.State` and a **COMPARE\_VALUE** of 2, the Label is rendered as **State = 2** (note the prefix and the "dot" are trimmed).

**Verbose** - Given a Process Step Parameter Key of `Job.State` and a **COMPARE\_VALUE** of 2, the Label is rendered as **Job.State = 2** (note the prefix and the "dot" are NOT trimmed).
