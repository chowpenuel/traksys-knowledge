# Referencing Pages

Content Pages, built-in and custom developed do not have to be instanced in the hierarchy. Instead, they can simply be linked to from any Page by using a standard QueryString structure.

## Content Key

The basic structure of the link to a Content Page revolves around the Content Key parameter (c) when calling a Page using the QueryString. The Content Key for the standard Content Pages can be found by browsing the New Page Definition list when in the TrakSYS Web application and selecting a Page.

For example:

`?c=ETS.Application.Event.EventAttention`

## Page Parameters

The standard Content Pages have been documented with what parameters are passed to them by default (see Content Page Reference's [Default Content topic](../content-reference/content-page-reference/default-content)). For example:

`?c=ETS.Application.Event.EventAttention&EventID={EventID}`

Additionally, if custom Content Pages are created, passing parameters which the custom Pages were designed to use is also permitted. For example:

`?c={CustomContentPageKey}&Parameter1={Parameter1Value}&Parameter2=5`
