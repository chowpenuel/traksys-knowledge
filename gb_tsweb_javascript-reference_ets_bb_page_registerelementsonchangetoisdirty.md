# registerElementsOnChangeToIsDirty

```javascript
Boolean registerElementsOnChangeToIsDirty([Any elements])
```

This method tells the page to listen to the elements change event. When an element's value changes, it will set the `ets.bb.page.isDirty = true` and will cause a warning pop-up to show if the user tries to navigate away from the page. The warning pop-up can be ignored on an anchor tag by adding the CSS class `dirty-ignore`.

## Parameters

```javascript
Any elements = "input, select, textarea"
```

This property is a jQuery selector. Elements provided must support JavaScript's change event, ie: input, textarea.

## Examples

### Simple Content Page Form with IsDirty Check

* Create a Visual Content Page
* Add a Text Box part to the page
* Add a Buttons part to the page
* Edit the Buttons part
  * Set the Save button
    * Click Actions > On Client Click: `ets.bb.page.setIsDirty(false);`
    * Click Actions > On Server Click: `Save_Click`
  * Set the Cancel button
    * CSS Class: `dirty-ignore btn-default`
* Add code to page's Script

```csharp
protected void Save_Click(object sender, EventArgs e)
{
  // Do save stuff here
}

protected override void OnPreRender(EventArgs e)
{
  // bind isDirty check
  this.Ets.Js.AddBackBoneReadyJavascript("ets.bb.page.registerElementsOnChangeToIsDirty('input');");
}
```

* Preview the page. If you make any changes to the Text Box on the content page and try to navigate away, a warning pop-up will show.

{% hint style="info" %}
- Clicking on the browser's back button may not trigger a warning pop-up on \`isDirty = true\`.
- Changes to an input through JavaScript will **not** fire an element's change event. To support changes through JavaScript, have your code call `ets.bb.page.setIsDirty(true)`.
{% endhint %}
