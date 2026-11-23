# showSplashScreen

```javascript
Boolean showSplashScreen()
```

Opens a gray splash background. Does not have a close button.

Always returns `false`.

## Examples

### Simple Splash Screen On Button Click

This example shows how to show a splash screen during a button's postback event. The splash screen will prevent the client from clicking anything on the screen while the event is running. After the postback completes, the splash screen will disappear.

* Create a `Visual` content page
* Add a `Buttons` part (TrakSYS > Buttons)
* In the `Part` editor screen, edit the `Buttons` part and set the following properties to the `Save` button

On Client Click:

```javascript
ets.ui.showSplashScreen(); return true;
```

On Server Click:

```csharp
Save_Click
```

* In the `Script` editor screen, add the following code in the page's class

```csharp
protected void Save_Click(object sender, EventArgs e)
{
  // Button's click event. Do something here
}
```
