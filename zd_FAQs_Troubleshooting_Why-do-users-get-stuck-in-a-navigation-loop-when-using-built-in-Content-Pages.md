# Why do users get stuck in a navigation loop when using built-in Content Pages?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360024515753-Why-do-users-get-stuck-in-a-navigation-loop-when-using-built-in-Content-Pages*
*Last updated: 2025-05-28T18:00:28Z*

---

Applies To | TrakSYS 10+

When navigating through multiple built-in pages, it is possible to get caught in a navigation loop if the pages are of c-equals type. A c-equals page will have a “c=‘PageKey’” in the URL. For example, the built-in Event List Attention page URL below:

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360037625634)

These pages use the default settings for a built-in instance of the page and cannot be modified. If a c-equals page includes a Back or Save button, it will redirect the user to the previous page after clicking. If a user navigates from one c-equals page to another, they will only redirect to each other creating a navigation loop. 

In order to preempt this scenario, an instance of each page must be created. This will allow modifying the links on any Back or Save buttons that may be present on the built-in page, giving the developer control of where the end-user is redirected when the buttons are clicked.
