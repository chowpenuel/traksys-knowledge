# Adjusting Div/Element Spacing with CSS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004541728-Adjusting-Div-Element-Spacing-with-CSS*
*Last updated: 2025-05-21T22:52:00Z*

---

Applies To | TrakSYS 10+

### **Summary**

As a general best practice, where possible, it is advised to avoid inline styles. This is mainly to provide a consistency across the TrakSYS Web as subtle changes are made to how things are adjusted. In addition, Bootstrap screen sizes allow for an easy way to provide different UI Layout adjustments based on the actual screen size.

A common scenario is that additional spacing was needed on one page, so Developer A would add a spacing of 3px. On another page, another developer also needed extra spacing, and would add 5px. Over time, there is no consistency as to how things are laid out, and no easy way to resolve these differences.

Frequently though, extra padding or margin is needed to provide the subtle changes required. To help address these cases, TrakSYS 10 includes several built-in CSS classes to adjust the HTML.

### **Overview**

The following is a list of all the different types of TrakSYS-specific CSS classes that follow a pattern similar to Bootstrap.

#### **Margin and Padding**
    
    
    .tspadding-{screensize}-{location}-{amount}
    .tsmargin-{screensize}-{location}-{amount} 
      
    <div class="tsmargin-sm-left-small">indented</div>
    

This allows you to adjust margin and or padding by set amounts and be responsive based on screen size ({screensize} are the standard bootstrap screen sizes).

The locations are:

  * top
  * bottom
  * vertical
  * left
  * right
  * horizontal



The amounts are:

  * small
  * medium
  * large
  * jumbo



#### **Underline Text**
    
    
    .tstext-underline   
    
    Hello <span class="tstext-underline">this</span> is underlined.
    

Simply adds an underline to a span or text.

#### **Borders**
    
    
    .tsborder-top
    .tsborder-bottom
    .tsborder-horizontal
    .tsborder-left
    .tsborder-right
    .tsborder-vertical
    .tsborder-all
    
    .tsborder-c-{color}
    
    <div class="tsborder-all tsborder-c-red">I have a red box around me.</div>
    

This will add a 1px solid border, the color is specified with `.tsborder-c-{color}`.

The entire standard TrakSYS color palette is supported.

#### **Scrollable Div**
    
    
    .tsscroll-vertical
    
    <div class="tsscroll-vertical" style="height: 100px;">lots and lots of content</div>
    

An inline style must be used for this one in order to specify the height.

#### **The finger cursor**
    
    
    .tscursor
    
    <div class="tscursor">When you hover over me you get the link-able cursor</div>
    

For the typical "link" cursor.

#### **Vertical Align Table Cells**
    
    
    .tscell-vertical-top
    .tscell-vertical-middle
    .tscell-vertical-bottom
    
    <td class="tscell-vertical-middle">I am vertically aligned in the middle</td>
    

This is designed to work only if the `td` is in a bootstrap table `<table class="table ...">.`

#### **See Also**

  * [List of Colors](https://portal.parsec-corp.com/hc/en-us/articles/115004389727)
  * [Bootstrap : getbootstrap.com](http://getbootstrap.com)


