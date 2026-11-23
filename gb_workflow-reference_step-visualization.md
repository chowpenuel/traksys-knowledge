# Step Visualization

The following sections describe the various Icons and Colors that are displayed for Steps in a Process Definition or Process diagram.

## State Icon and Color

As a Process is executed, Steps move through a series of States describing their execution. The States and corresponding Icons and Colors are described below.

{% hint style="info" %}
The State Icon and Color only appear in the runtime view of a Process displayed on a Content Part or Page. The designer view will never show a State Icon or Color.
{% endhint %}

### None

* **Blue Step**
* **No Icon \[ Upper Left ]**

Steps in the `None` State have not yet been entered/executed within the lifetime of the Process.

### In Progress (or Waiting)

* **Green Step**
* **Triangular Play Icon \[ Upper Left ]**

Steps in the `In Progress` State have been entered and are currently executing. Since most Step Types execute their main logic in milliseconds, a Step Type in the `In Progress` state for a period of time typically indicates the Step is "waiting" for some condition to become true.

### Success

* **Grey Step**
* **No Icon \[ Upper Left ]**

Steps in the `Success` State have completed execution with success. Note that Steps in the `Success` State may be re-entered later in the execution depending on looping logic.

### Timeout

* **Yellow Step**
* **Clock Icon \[ Upper Left ]**

Steps in the \`Timeout State have completed execution after "timing out". This typically means that the Step was waiting for a specified condition, and that condition never became true before reaching the configured timeout threshold.

### Error

* **Red Step**
* **Triangular Exclamation Icon \[ Upper Left ]**

Steps in the `Error` State have completed execution after "erroring". Depending on the error behavior configured for the Step, Process execution may have stopped after the error, or may have continued on to the next Steps.

## Merge Icon

When a Step has more than 1 incoming connector, a "Y" Icon is displayed in the upper **right corner**. This Icon is informational only and helps visually spot "merging" patterns in a workflow diagram.

## Split Icon

When a Step has more than 1 outgoing connector, an upside-down "Y" Icon is displayed in the **lower right** corner. This Icon is informational only and helps visually spot "splitting" patterns in a workflow diagram.

## Decision Icon

When a Step has 1 or more outgoing connectors that include conditional logic, a "diamond" Icon is displayed in the **lower left** corner. This Icon is informational only and helps visually spot "decision" patterns in a workflow diagram.
